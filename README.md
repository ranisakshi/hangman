# hangman
import random

def display_hangman(tries):
    stages = [
        """
          --------
          |      |
          |      O
          |     \\|/
          |      |
          |     / \\
          -
        """,
        """
          --------
          |      |
          |      O
          |     \\|/
          |      |
          |     /
          -
        """,
        """
          --------
          |      |
          |      O
          |     \\|/
          |      |
          |
          -
        """,
        """
          --------
          |      |
          |      O
          |     \\|
          |      |
          |
          -
        """,
        """
          --------
          |      |
          |      O
          |      |
          |      |
          |
          -
        """,
        """
          --------
          |      |
          |      O
          |
          |
          |
          -
        """,
        """
          --------
          |      |
          |
          |
          |
          |
          -
        """
    ]
    print(stages[tries])

def play_hangman():
    words = ["python", "programming", "computer", "science", "algorithm", "hangman"]
    word = random.choice(words)
    word_length = len(word)
    guessed_letters = []
    tries = 6
    display = ["_"] * word_length
    game_over = False

    print("Welcome to Hangman!")
    display_hangman(tries)
    print(" ".join(display))

    while not game_over:
        guess = input("Guess a letter: ").lower()

        if len(guess) != 1 or not guess.isalpha():
            print("Invalid input. Please enter a single letter.")
            continue

        if guess in guessed_letters:
            print("You already guessed that letter.")
            continue

        guessed_letters.append(guess)

        if guess in word:
            for i in range(word_length):
                if word[i] == guess:
                    display[i] = guess
            print("Correct guess!")
        else:
            tries -= 1
            print("Incorrect guess. Tries remaining:", tries)
            display_hangman(tries)

        print(" ".join(display))

        if "_" not in display:
            print("Congratulations, you won! The word was:", word)
            game_over = True
        elif tries == 0:
            print("You lost. The word was:", word)
            game_over = True

play_hangman()
