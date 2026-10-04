# Backtracking

Backtracking is a general algorithmic technique used in computer science for solving problems incrementally, one piece at a time, and removing solutions that fail to satisfy the constraints of the problem at any point of time (i.e., constraints that are violated).

It is often employed in scenarios where there are multiple potential solutions, and the goal is to find one or all solutions that satisfy the given conditions.

## Key Characterist
- **Incremental Construction:** Build the solution step by step.
- **Constraints Checking**: At each step, check if the current partial solution is valid under the problem's constraints.
- **Backtrack**: If the current partial solution violates constraints or doesn't lead to a solution, discard it (backtrack) and try another path.

## Example: N-Queens Problem

The N-Queens problem involves placing N queens on an N×N chessboard such that no two queens threaten each other. 

Here's a high-level approach to solving it using backtracking:
- Place a queen in the first column of the first row.
- Move to the next row and place a queen in a column where it is not threatened by the previous queens.
- Continue this process row by row.
- If placing a queen in any column of a row is not possible (because it would be threatened), backtrack to the previous row and move the queen to the next possible column.
- Repeat until all queens are placed or all configurations have been tried.

### Python Implementation
```python
class NQueens:
    def __init__(self, n: int):
        self.size = n
        self.board = [[0] * n for _ in range(n)]

    def solve(self) -> None:
        self.place_queen(0)

    def print_solution(self) -> None:
        for row in self.board:
            print(" ".join("Q" if cell else "." for cell in row))
        print()

    def is_safe(self, row: int, col: int) -> bool:
        # Check the column
        if any(self.board[i][col] for i in range(row)):
            return False
        # Check the upper left diagonal
        i, j = row, col
        while i >= 0 and j >= 0:
            if self.board[i][j]:
                return False
            i, j = i - 1, j - 1
        # Check the upper right diagonal
        i, j = row, col
        while i >= 0 and j < self.size:
            if self.board[i][j]:
                return False
            i, j = i - 1, j + 1
        return True

    def place_queen(self, row: int) -> bool:
        if row == self.size:
            self.print_solution()
            return True

        found_solution = False
        for col in range(self.size):
            if self.is_safe(row, col):
                self.board[row][col] = 1  # Place the queen
                # Recursively place queens in the next row
                found_solution = self.place_queen(row + 1) or found_solution
                self.board[row][col] = 0  # Backtrack and remove the queen
        return found_solution


NQueens(4).solve()
```

### Runtime Complexity
The worst-case time complexity of the N-Queens problem using backtracking is O(N^N).
