def print_board(board):
    for row in board:
        print(" | ".join(row))
        print("-" * 5)

def check_winner(board, player):
    # Check rows, columns, and diagonals
    for i in range(3):
        if all([cell == player for cell in board[i]]):  # rows
            return True
        if all([board[j][i] == player for j in range(3)]):  # columns
            return True
    if all([board[i][i] == player for i in range(3)]):  # main diagonal
        return True
    if all([board[i][2 - i] == player for i in range(3)]):  # other diagonal
        return True
    return False

def is_draw(board):
    return all(cell in ['X', 'O'] for row in board for cell in row)

def tic_tac_toe():
    board = [[" " for _ in range(3)] for _ in range(3)]
    current_player = "X"

    while True:
        print_board(board)
        print(f"Player {current_player}, enter your move (row and column from 1-3):")
        try:
            row = int(input("Row: ")) - 1
            col = int(input("Col: ")) - 1

            if board[row][col] != " ":
                print("Cell already taken. Try again.")
                continue

            board[row][col] = current_player

            if check_winner(board, current_player):
                print_board(board)
                print(f"Player {current_player} wins!")
                break
            elif is_draw(board):
                print_board(board)
                print("It's a draw!")
                break

            current_player = "O" if current_player == "X" else "X"
        except (ValueError, IndexError):
            print("Invalid input. Please enter row and column as numbers from 1 to 3.")

# Run the game
tic_tac_toe()
