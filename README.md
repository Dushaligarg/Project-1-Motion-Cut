# Project-1-Motion-Cut
import random
import os

def create_default_files():
    """Creates default adjective and noun files if they do not exist."""
    adjectives_file = "adjectives.txt"
    nouns_file = "nouns.txt"

    if not os.path.exists(adjectives_file):
        with open(adjectives_file, "w") as f:
            f.write("Cool\nHappy\nBrave\nSneaky\nMighty\n")
    
    if not os.path.exists(nouns_file):
        with open(nouns_file, "w") as f:
            f.write("Tiger\nDragon\nFalcon\nNinja\nWizard\n")

def load_words(filename):
    """Load words from a file into a list."""
    try:
        with open(filename, 'r') as file:
            words = [line.strip() for line in file.readlines()]
        return words
    except FileNotFoundError:
        print(f"File {filename} not found. Using default words.")
        return []

def generate_username(adjectives, nouns, include_numbers=True, include_special=False):
    """Generate a random username by combining an adjective and a noun with optional numbers or special characters."""
    if not adjectives or not nouns:
        adjectives = ['Cool', 'Epic', 'Mighty', 'Sneaky', 'Brave']
        nouns = ['Tiger', 'Dragon', 'Wizard', 'Ninja', 'Falcon']
    
    username = f"{random.choice(adjectives)}{random.choice(nouns)}"
    
    if include_numbers:
        username += str(random.randint(10, 99))
    if include_special:
        username += random.choice('!@#$%^&*')
    
    return username

def save_username(username, filename="usernames.txt"):
    """Save the generated username to a file."""
    with open(filename, 'a') as file:
        file.write(username + "\n")
    print(f"Username '{username}' saved to {filename}.")

def main():
    create_default_files()
    adjectives = load_words("adjectives.txt")
    nouns = load_words("nouns.txt")
    
    while True:
        include_numbers = input("Include numbers? (y/n): ").strip().lower() == 'y'
        include_special = input("Include special characters? (y/n): ").strip().lower() == 'y'
        
        username = generate_username(adjectives, nouns, include_numbers, include_special)
        print("Generated Username:", username)
        
        save = input("Would you like to save this username? (y/n): ").strip().lower()
        if save == 'y':
            save_username(username)
        
        again = input("Generate another? (y/n): ").strip().lower()
        if again != 'y':
            break

if __name__ == "__main__":
    main()
    
