
import random

# HANGMAN GAME

WORDS = [
    "python",
    "developer",
    "computer",
    "code alpha",
    "program"
]

MAX_WRONG_GUESSES = 6


def choose_word():
    """Choose a random word from the word list."""
    return random.choice(WORDS)


def display_word(word, guessed_letters):
    """Display guessed letters and hide unguessed letters."""
    result = ""

    for letter in word:
        if letter in guessed_letters:
            result += letter + " "
        else:
            result += "_ "

    return result.strip()


def get_guess(guessed_letters):
    """Get and validate a player's guess."""

    while True:
        guess = input("Enter a letter: ").lower().strip()

        if len(guess) != 1:
            print("⚠️ Please enter only ONE letter.")
            continue

        if not guess.isalpha():
            print("⚠️ Please enter a valid letter.")
            continue

        if guess in guessed_letters:
            print("⚠️ You already guessed that letter.")
            continue

        return guess


def play_game():
    """Run one complete Hangman game."""

    word = choose_word()
    guessed_letters = []
    wrong_guesses = 0

    print("\n" + "=" * 45)
    print("          🎮 HANGMAN GAME")
    print("=" * 45)

    print("Guess the hidden word one letter at a time.")
    print(f"You have {MAX_WRONG_GUESSES} incorrect guesses.\n")

    while wrong_guesses < MAX_WRONG_GUESSES:

        print("Word:", display_word(word, guessed_letters))

        if guessed_letters:
            print("Guessed letters:", " ".join(guessed_letters))
        else:
            print("Guessed letters: None")

        print(
            f"Wrong guesses: "
            f"{wrong_guesses}/{MAX_WRONG_GUESSES}"
        )

        guess = get_guess(guessed_letters)
        guessed_letters.append(guess)

        if guess in word:
            print("✅ Correct guess!")

        else:
            wrong_guesses += 1
            print("❌ Wrong guess!")

        # Check if every letter has been guessed
        if all(letter in guessed_letters for letter in word):
            print("\n" + "=" * 45)
            print("🎉 YOU WON!")
            print(f"The word was: {word.upper()}")
            print("=" * 45)
            return

        print()

    # Player loses
    print("\n" + "=" * 45)
    print("💀 GAME OVER!")
    print(f"The correct word was: {word.upper()}")
    print("=" * 45)


def main():
    """Start the Hangman application."""

    while True:

        play_game()

        choice = input(
            "\nDo you want to play again? (yes/no): "
        ).lower().strip()

        if choice != "yes":
            print("\nThanks for playing! 👋")
            break

        print("\nStarting a new game...")


# Program starts here
if __name__ == "__main__":
    main()
