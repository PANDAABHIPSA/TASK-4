# TASK-4
def is_safe(board, row, col):
  # Check row and column for existing queens
  for i in range(len(board)):
    if board[i][col] == 1 or board[row][i] == 1:
      return False

  # Check diagonals
  for i, j in zip(range(row - 1, -1, -1), range(col - 1, -1, -1)):
    if board[i][j] == 1:
      return False
  for i, j in zip(range(row + 1, len(board)), range(col + 1, len(board))):
    if board[i][j] == 1:
      return False
  return True

def solve_n_queens(board, col):
  # Base case: All queens placed
  if col >= len(board):
    return True

  # Try placing queen in all safe rows in this column
  for i in range(len(board)):
    if is_safe(board, i, col):
      board[i][col] = 1
      if solve_n_queens(board, col + 1):
        return True
      board[i][col] = 0  # Backtrack

  # If no safe position found, return False
  return False

def print_board(board):
  for row in board:
    print(' '.join([str(x) for x in row]))

def main():
  n = int(input("Enter the number of queens (board size): "))
  board = [[0 for _ in range(n)] for _ in range(n)]

  if solve_n_queens(board, 0):
    print("Solution found:")
    print_board(board)
  else:
    print("No solution exists for", n, "queens")

if _name_ == "_main_":
  main()
