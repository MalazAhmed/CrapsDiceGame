import random

# Function to simulate rolling a six-sided die
def roll_dice():
    return random.randint(1, 6) + random.randint(1, 6)  # Roll two dice and return sum

# Function to play a single game
def play_craps():
    initial_roll = roll_dice()
    print(f"Rolled: {initial_roll}")

    if initial_roll in [2, 3, 12]:
        return "lose"  # Instant loss
    elif initial_roll in [7, 11]:
        return "win"  # Instant win
    
    point = initial_roll  # Set point
    print(f"Point is now {point}. Rolling again...")
    
    while True:
        new_roll = roll_dice()
        print(f"Rolled: {new_roll}")
        if new_roll == 7:
            return "lose"
        elif new_roll == point:
            return "win"

# Function to handle user input
def get_game_count():
    while True:
        try:
            num = int(input("Enter the number of games: "))
            if num > 0:
                return num
            print("Please enter a positive number.")
        except ValueError:
            print("Invalid input. Enter a number.")

# Main function to run multiple games
def main():
    wins, losses = 0, 0
    games = get_game_count()
    for _ in range(games):
        result = play_craps()
        if result == "win":
            wins += 1
        else:
            losses += 1
    
    # Display results
    print(f"\nTotal Wins: {wins}")
    print(f"Total Losses: {losses}")
    print(f"Win Percentage: {wins / games * 100:.2f}%")

if __name__ == "__main__":
    main()
