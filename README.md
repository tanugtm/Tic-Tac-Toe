# Tic-Tac-Toe
board = [' ' for _ in range(9)]  # Creating a 3x3 board

def print_board():
    print(f"{board[0]} | {board[1]} | {board[2]}")
    print("--*---*--")
    print(f"{board[3]} | {board[4]} | {board[5]}")
    print("--*---*--")
    print(f"{board[6]} | {board[7]} | {board[8]}")

def play_game():
    print_board()  # Print the empty board at the start
    for _ in range(9):
        move = int(input("Player X, enter your move (1-9): ")) - 1
        board[move] = 'X'  # Assuming Player X for simplicity
        print_board()  # Print updated board after each move

import tkinter as tk
from tkinter import messagebox

# Initialize the Tkinter window
window = tk.Tk()
window.title("Tic-Tac-Toe")

# Variables for the game state
current_player = "X"
board = [" " for _ in range(9)]
buttons = []

def check_winner():
    # Possible winning combinations
    winning_combinations = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],  # Horizontal
        [0, 3, 6], [1, 4, 7], [2, 5, 8],  # Vertical
        [0, 4, 8], [2, 4, 6]              # Diagonal
    ]
    for combo in winning_combinations:
        if board[combo[0]] == board[combo[1]] == board[combo[2]] != " ":
            return board[combo[0]]
    return None

def button_click(index):
    global current_player
    if board[index] == " ":
        board[index] = current_player
        buttons[index].config(text=current_player)

        winner = check_winner()
        if winner:
            messagebox.showinfo("Tic-Tac-Toe", f"Player {winner} wins!")
            reset_game()
        elif " " not in board:
            messagebox.showinfo("Tic-Tac-Toe", "It's a draw!")
            reset_game()
        else:
            current_player = "O" if current_player == "X" else "X"

def reset_game():
    global board, current_player
    board = [" " for _ in range(9)]
    current_player = "X"
    for button in buttons:
        button.config(text=" ")

# Create buttons for the 3x3 grid
for i in range(9):
    button = tk.Button(window, text=" ", font=('normal', 40), width=5, height=2,
                       command=lambda i=i: button_click(i))
    button.grid(row=i//3, column=i%3)
    buttons.append(button)

# Start the game
window.mainloop()
