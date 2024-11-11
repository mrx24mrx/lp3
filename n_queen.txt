# Function to print the solution board
def print_solution(board):
    for row in board:
        for cell in row:
            print("Q" if cell else ".", end=" ")
        print()
    print()

# Function to check if a queen can be placed on the board at the given row and column
def is_safe(board, row, col, n):
    # Check this row on the left side
    for i in range(col):
        if board[row][i] == 1:
            return False

    # Check the upper diagonal on the left side
    for i, j in zip(range(row, -1, -1), range(col, -1, -1)):
        if board[i][j] == 1:
            return False

    # Check the lower diagonal on the left side
    for i, j in zip(range(row, n), range(col, -1, -1)):
        if board[i][j] == 1:
            return False

    return True

# Function to solve the N-Queen problem using backtracking
def solve_n_queens_util(board, col, n):
    # Base case: If all queens are placed, return True
    if col >= n:
        print_solution(board)
        return True

    # Consider this column and try placing this queen in all rows one by one
    for i in range(n):
        if is_safe(board, i, col, n):
            # Place the queen
            board[i][col] = 1

            # Recur to place the rest of the queens
            if solve_n_queens_util(board, col + 1, n):
                return True  # Stop after finding the first solution

            # If placing queen in the current row and column doesn't lead to a solution, remove the queen (backtrack)
            board[i][col] = 0

    # If no row is safe in this column, return False
    return False

# Function to solve the N-Queen problem
def solve_n_queens(n):
    board = [[0] * n for _ in range(n)]
    if not solve_n_queens_util(board, 0, n):
        print("No solution exists")

# Driver code
n = 4  # You can change this to any number for an N x N board
solve_n_queens(n)
