#enter ur number
# This is a simple number guessing game with colored output.
import random

# ANSI escape codes for terminal colors and emphasis
RESET = "\033[0m"
BOLD = "\033[1m"
GREEN = "\033[32m"
YELLOW = "\033[33m"
RED = "\033[31m"
CYAN = "\033[36m"
MAGENTA = "\033[35m"

# Print a welcome message in bold cyan
print(f"{CYAN}{BOLD}Welcome to the Number Guessing Game!{RESET}")

play_again = True
# Main game loop: keeps playing until the user says no
while play_again:
    # Choose a random secret number between 1 and 100
    secret_num = random.randint(1, 100)
    found = False
    
    # Guessing loop: repeat until the correct number is found
    while not found:
        try:
            guess_input = input(f"{YELLOW}{BOLD}Your guess: {RESET}")
        except EOFError:
            # Handle unexpected end-of-input gracefully
            print(f"\n{RED}No input received. Exiting the game.{RESET}")
            play_again = False
            break

        try:
            # Convert the user's input into an integer guess
            guess = int(guess_input)
        except ValueError:
            # If the input is not a number, ask again
            print(f"{RED}Please enter a valid whole number.{RESET}")
            continue

        # Print the guess back to the user in cyan
        print(f"{CYAN}You guessed: {BOLD}{guess}{RESET}")

        # Check the guess against the secret number
        if guess == secret_num:
            print(f"{GREEN}{BOLD}You got it! The number is {secret_num}!{RESET}")
            found = True
            break
        elif guess > secret_num:
            # Guess is too high
            print(f"{RED}Too high! Try again.{RESET}")
        else:
            # Guess is too low
            print(f"{MAGENTA}Too low! Try again.{RESET}")

    # If the user ended input unexpectedly, stop the main loop too
    if not play_again:
        break

    # Ask whether the user wants to play again
    while True:
        try:
            answer = input(f"\n{CYAN}Play again? (y/n): {RESET}")
        except EOFError:
            print(f"\n{RED}No input received. Exiting the game.{RESET}")
            play_again = False
            break

        if answer.lower() in ("y", "yes"):
            # Start a new round
            break
        if answer.lower() in ("n", "no"):
            # End the game loop
            play_again = False
            break

        # If the answer is not valid, keep asking
        print(f"{RED}Please answer y or n.{RESET}")

# Print a goodbye message at the end
print(f"{CYAN}{BOLD}Thanks for playing!{RESET}")

 
