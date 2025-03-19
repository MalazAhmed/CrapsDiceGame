import random

# Function to simulate rolling a six-sided die
def roll_die():
    return random.randint(1, 6)  # Rolls the die and returns a random number between 1 and 6

# Function to get a valid number of games from the user
def get_number_of_games():
    while True:
        try:
            games = int(input("How many games would you like to simulate? "))
            if games <= 0:
                print("Please enter a positive number.")
            else:
                return games
        except ValueError:
            print("Invalid input. Please enter a valid number.")

# Function to play a single game
def play_game():
    roll1 = roll_die()  # Roll the first die
    roll2 = roll_die()  # Roll the second die
    sum_roll = roll1 + roll2  # Calculate the sum of the dice rolls
    print(f"Rolled: {roll1} + {roll2} = {sum_roll}")  # Output the result

    # Immediate win/loss based on the first roll
    if sum_roll in [2, 3, 12]:
        return "lose"  # Player loses if the sum is 2, 3, or 12
    elif sum_roll in [7, 11]:
        return "win"  # Player wins if the sum is 7 or 11

    # If no immediate win/loss, set the point and continue rolling
    point = sum_roll
    print(f"Point is set to {point}. Rolling again...")
    
    while True:  # Keep rolling until player wins or loses
        roll1 = roll_die()  # Roll the first die
        roll2 = roll_die()  # Roll the second die
        sum_roll = roll1 + roll2  # Calculate the sum of the new dice roll
        print(f"Rolled: {roll1} + {roll2} = {sum_roll}")  # Output the result
        
        if sum_roll == 7:
            return "lose"  # Player loses if the sum is 7
        elif sum_roll == point:
            return "win"  # Player wins if the sum matches the initial point

# Main program to run multiple games
def main():
    wins = 0
    losses = 0
    games_played = 0
    rolls_count = 0

    # Ask the user for the number of games to simulate
    number_of_games = get_number_of_games()

    for _ in range(number_of_games):
        result = play_game()
        games_played += 1
        if result == "win":
            wins += 1
        else:
            losses += 1
        rolls_count += 1  # count each roll
    
    # Calculate and display statistics
    print(f"\nTotal Wins: {wins}")
    print(f"Total Losses: {losses}")
    print(f"Total Games Played: {games_played}")
    print(f"Average Rolls Per Game: {rolls_count / games_played:.2f}")
    print(f"Winning Percentage: {wins / games_played * 100:.2f}%")

# Run the program
if __name__ == "__main__":
    main()
