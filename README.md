# Word-Game


import random

from random import randint



def read_words(filename):
    
    """
    
    This function reads a file and opens the inputs inside of it

    Args:
        filename: a file that needs to be read written as a string.
    
    Return:
        Returns the lines in the files inside the value of "words"
    """
    
    with open(filename, "r")as word_file:
        words = []
        
        for line in word_file:
            words.append(line.strip())
        return words
    
    
    
def set_to_string(set_obj):
    
    """
    This function takes a string and splits it with spaces.

    Args:
        set_obj: A string that will be split into spaces.
    
    Return:
        Returns the string but into spaces and capitalized.
    """

    object_set = ' '
    for value in set_obj:
        object_set += str(value) + ' '
        
        
    return object_set.upper()



def insert_letter(userinput, underscore_word, words):
    
    """
    This function takes in a userinput, a random word and the word incremented into blank spaces.

    Args:
        userinput: a letter that will be used to fill out the blank spaces.
        underscore_word: the level of blank spaces to be left after evaluating the length of "words".
        words: a random word that will be inputted from the file.
    
    Return:
        Returns an outut that fills the underscore_word with the letter inputted by the user.
    """

    newword = ''
    finalword = ''
    
    for alpha in words:
        if alpha != userinput:
            newword += '_'
        elif alpha == userinput:
            newword += userinput
            
    for alpha in range(len(newword)):
        if underscore_word[alpha] == '_':
            finalword += newword[alpha]
        elif underscore_word[alpha] != '_':
            finalword += underscore_word[alpha]
        
    return finalword



def play_wordgame(filename, total_life):
    
    """
    This function evaluates the entire game by taking in user input.

    Args:
        filename: a file that needs to be read and written in the parameter as a string.
        total_life: The number of incorrect guesses the user will be allowed to have.
    
    Return:
        Returns the game and output based on the users input.
    """

    words = read_words(filename)
    secret = random.choice(words)
    underscore_word = len(words)*"_"
    total_life = 7
    used_life = 0
    wrong_letter = set()

    
    while used_life <= total_life:
        remaining_guesses = total_life - used_life    
        print ("_ _ _ _ _ _ _ _ _ _ _ _ _ _ _")
        print ("Guessed Letters: " + set_to_string(wrong_letter))
        print ("Incorrect guesses left: " + "*" *(remaining_guesses))
        print ("Word: " + underscore_word)
        
        userinput = input("Guess a letter: ")
        
        if userinput in secret:
            if userinput in wrong_letter:
                print("Letter already guessed!")
            underscore_word = insert_letter(userinput, underscore_word, secret)
            
            wrong_letter.add(userinput)
            
        elif userinput not in secret:
            if userinput in wrong_letter:
                print("Letter already guessed!")
                
            else:
                wrong_letter.add(userinput)
                used_life += 1
                
        if used_life > total_life:
            print("The word was: " + str(secret))
            print("Better luck next time!")
            
        elif used_life <= total_life and underscore_word == secret:
            print("You win!")
            print ("The word was: " + secret)
            print("You guessed it with " + str(used_life) + " incorrect guesses")
            
            break
            
                 

if __name__ == '__main__':

    total_life = 7
    play_wordgame("cs_words.txt", total_life) 
    
    #Replace the "cs_words.txt" with a word file of your own that contains a dictionary or set of words.
    
