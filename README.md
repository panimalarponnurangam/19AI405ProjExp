# Implement a Sudoku Solver From Scratch
## Steps to solve the Sudoku Puzzle in Python
<ol>
  <li>In this method for solving the sudoku puzzle, first, we assign the size of the 2D matrix to a variable M (M*M).</li>
 <li>Then we assign the utility function (puzzle) to print the grid.</li>
<li>Later it will assign num to the row and col.</li>
<li>If we find the same num in the same row or same column or in the specific 3*3 matrix, ‘false’ will be returned.</li>
<li>Then we will check if we have reached the 8th row and 9th column and return true for stopping further backtracking.</li>
<li>Next, we will check if the column value becomes 9 then we move to the next row and column.</li>
<li>Further now we see if the current position of the grid has a value greater than 0, then we iterate for the next column.</li>
<li>After checking if it is a safe place, we move to the next column and then assign the num in the current (row, col) position of the grid. Later we check for the next possibility with the next column.</li>
<li>As our assumption was wrong, we discard the assigned num and then we go for the next assumption with a different num value</li>
</ol>

## Program:
```
Name: Panimalar P
Register Number: 212222110031
```
```python
# Size of the grid
M = 9

# Utility function to print the grid
def print_grid(grid):
    for i in range(M):
        for j in range(M):
            print(grid[i][j], end=" ")
        print()

# Function to check if it's safe to place a number at (row, col)
def is_safe(grid, row, col, num):
    # Check if 'num' is not in the current row
    for x in range(M):
        if grid[row][x] == num:
            return False

    # Check if 'num' is not in the current column
    for x in range(M):
        if grid[x][col] == num:
            return False

    # Check if 'num' is not in the current 3x3 subgrid
    start_row = row - row % 3
    start_col = col - col % 3
    for i in range(3):
        for j in range(3):
            if grid[i + start_row][j + start_col] == num:
                return False

    return True

# Main function to solve the Sudoku using Backtracking
def solve_sudoku(grid, row=0, col=0):
    # If we have reached the 9th row and 0th column, we're done
    if row == M - 1 and col == M:
        return True

    # If column value becomes 9, move to next row and column 0
    if col == M:
        row += 1
        col = 0

    # If the current position already contains a number, move to next column
    if grid[row][col] > 0:
        return solve_sudoku(grid, row, col + 1)

    for num in range(1, M + 1, 1):  # Numbers 1 to 9
        # Check if placing num at (row, col) is valid
        if is_safe(grid, row, col, num):
            grid[row][col] = num

            # Recur to check for next possibility
            if solve_sudoku(grid, row, col + 1):
                return True

        # If assumption was wrong, undo & try next number
        grid[row][col] = 0

    return False

# Example Sudoku puzzle to solve 
grid = [
    [3, 0, 0, 8, 0, 0, 0, 0, 0],
    [0, 0, 7, 0, 0, 0, 9, 0, 2],
    [0, 5, 0, 0, 0, 0, 0, 8, 4],
    [0, 0, 0, 0, 0, 7, 0, 0, 0],
    [0, 8, 0, 6, 0, 2, 0, 5, 0],
    [0, 0, 0, 5, 0, 0, 0, 0, 0],
    [7, 3, 0, 0, 0, 0, 0, 6, 0],
    [2, 0, 5, 0, 0, 0, 8, 0, 0],
    [0, 0, 0, 0, 0, 5, 0, 0, 9]
]

if solve_sudoku(grid):
    print_grid(grid)
else:
    print("No solution exists")


```

## Output:
![image](https://github.com/user-attachments/assets/f49a2967-359b-41ea-b1d2-4f201a98dee4)


## Result:
Thus the python program to implement a sudoko solver from scratch is executed sucessfully.
