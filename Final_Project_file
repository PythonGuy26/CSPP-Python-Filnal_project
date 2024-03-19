"""
This script receives the name of a text file with lyrics and its location,
and returns information about:
A. How many lines are there in the file,
b. The longest word,
c. The character that repeated itself the most times,
in addition the script create a new file in the location of the original file with the name of the
file plus _analyzed, with the addition of an opening line: Beginning and an ending line: The End.
Before running the program checks if the entered output is correct and valid,
and if not it will ask the user to try another file
"""


def check_existing_analyzed_file(path_of_file):
    """
    :param path_of_file: Tha full path of the file as a string.
    :return: False if there is a file with the _analyzed extension in the path, and True if not exist.
    """
    try:
        valid_path = open(path_of_file[:-4] + "_analyzed.txt")
        valid_path.close()
        return False
    except FileNotFoundError:
        return True


def check_valid_path(path_of_file):
    """
    :param path_of_file: Tha full path of the file as a string.
    :return: True if the file exists in the path, and False if the file does not exist.
    """
    try:
        valid_path = open(path_of_file)
        valid_path.close()
        return True
    except (FileNotFoundError, OSError):  # OSError: Error code if the path is entered with quotation marks or incorrect location name
        return False


def check_txt_file(path_of_file):
    """
    :param path_of_file: Tha full path of the file as a string.
    :return:True if the file is a text file, and False ןf the file is not a text file.
    """
    try:
        with open(path_of_file) as valid:
            valid.readlines()
            return True
    except UnicodeDecodeError:
        return False


def the_most_frequent_letter(string_of_letters):
    """
    The function first create a dictionary with all the characters in the string and how many times they appeared,
    then it returns the character with the highest numerical value.
    :param string_of_letters: A sequence of characters as a string.
    :return:The character that appeared the most times (most_appeared_letters) and the number of times it appeared (the_number_of_appearance)
    """
    dic = {}
    for letter in string_of_letters:  # A loop that selects a letter in a string in order to count it
        num = 0
        if letter.lower() in dic.keys():  # The loop calculates with both uppercase and lowercase letters
            continue
        for letter_count in string_of_letters:  # An inner loop that goes through the string and counts the number of times the letter in the first loop appears
            if letter_count.lower() == letter.lower():
                num += 1
        dic[letter.lower()] = num
    most_appeared_letters = []
    the_number_of_appearance = 0
    for key_letter in dic:                        # The loop looks for the key with the highest value in the dictionary
        if dic[key_letter] > the_number_of_appearance:
            most_appeared_letters = [key_letter]
            the_number_of_appearance = dic[key_letter]
        elif dic[key_letter] == the_number_of_appearance:
            most_appeared_letters.append(key_letter)
    return most_appeared_letters, the_number_of_appearance


to_continue = "yes"                                     # Used if there is a problem with the path
while to_continue.lower() == "yes":
    file_location = input("Enter the file location:")
    file_name = input("Enter the file name with extension:")
    path = file_location + "\\" + file_name
    if check_valid_path(path):
        if check_txt_file(path):
            if check_existing_analyzed_file(path):
                with open(path, "r") as song_lyric_lines:     # Checking how many lines there are in the file
                    song_sentence = song_lyric_lines.readlines()
                    number_of_song_lines = len(song_sentence)

                with open(path, "r") as song_lyric:     # Checking which word in the file is the longest
                    song_words = song_lyric.read()
                    _analyzed_song_word = "Beginning\n" + song_words + "\nThe End"  # Preparing the content to be written to the new _analyzed file
                    song_words = song_words.replace("\n", " ")      # replacing all occurrences of \n with a space
                    list_of_the_word_in_song = song_words.split(" ")            # Creating a list with all the words of the file, a space is the sign of separation
                    longest_words = [""]                                        # variable save the longest word found
                    for word in list_of_the_word_in_song:                       # A loop that finds the longest word or words, the loop calculates with both uppercase and lowercase letters
                        if len(word) == len(longest_words[0]):
                            if word.lower() in longest_words:                   # Prevents the same word from entering the list several times
                                continue
                            else:
                                longest_words.append(word.lower())
                        elif len(word) > len(longest_words[0]):
                            longest_words = [word.lower()]
                    all_letters_in_the_song_as_one_string = "".join(list_of_the_word_in_song)  # Converting the list of words in the file into a single string without spaces
                    most_frequent_letter, number_of_appearance = the_most_frequent_letter(all_letters_in_the_song_as_one_string)  # Finding the letter that appears the most times in the file and how many times it appeared

                new_file = path[:-4] + "_analyzed.txt"    # Creating a path to the new file based on the original path
                with open(new_file, "w") as update_file:
                    update_file.write(_analyzed_song_word)  # Inserting the content prepared in line 94 into the new file

                print(f"\nThere are {number_of_song_lines} lines in the song")  # Printing the calculated data on the file
                if len(longest_words) == 1:
                    print("The longest word is", longest_words[0])
                else:
                    print("The longest words are:", " and ".join(longest_words))
                if len(most_frequent_letter) == 1:
                    print(f"And the letter that appeared the most times is {most_frequent_letter[0]} with {number_of_appearance} appearances")
                else:
                    print(f"And the letters that appeared the most times are {" and ".join(most_frequent_letter)} with {number_of_appearance} appearances")
                break  # If the path was valid the running of the 'while' loop will finish
            else:      # If the path was not valid the user could try another path or end the program
                print("\nIt seems that there is already an existing _analyzed file to this file.")
        else:
            print("\nIts seems that your file is not a text file.")
    else:
        print("\nIts seems that their is not such a file, check the path again.")
    to_continue = input("Do you want to try another file? Answer with 'Yes' or 'No': \n")
input("Enjoy your song!!")  # keep the last massage on the screen until the user press enter
