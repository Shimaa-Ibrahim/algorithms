#  Queen's Attack II - Python 3
#### Description:
You will be given a square chess board with one queen and a number of obstacles placed on it. Determine how many squares the queen can attack.
A queen is standing on an  chessboard. The chess board's rows are numbered from  to , going from bottom to top. Its columns are numbered from  to , going from left to right. Each square is referenced by a tuple, , describing the row, , and column, , where the square is located.
The queen is standing at position . In a single move, she can attack any square in any of the eight directions (left, right, up, down, and the four diagonals). In the diagram below, the green circles denote all the cells the queen can attack from :
There are obstacles on the chessboard, each preventing the queen from attacking any square beyond it on that path. For example, an obstacle at location  in the diagram above prevents the queen from attacking cells , , and :
Given the queen's position and the locations of all the obstacles, find and print the number of squares the queen can attack from her position at . In the board above, there are  such squares.
Function Description
Complete the queensAttack function in the editor below.
queensAttack has the following parameters:
  - int n: the number of rows and columns in the board
  - nt k: the number of obstacles on the board
  - int r_q: the row number of the queen's position
  - int c_q: the column number of the queen's position
  - int obstacles[k][2]: each element is an array of  integers, the row and column of an obstacle

Returns
  - int: the number of squares the queen can attack

### Solution
```
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the queensAttack function below.
def queensAttack(n, k, r_q, c_q, obstacles):
    if n == 1:
        return 0;
    moves = 0
    if k == 0:
        moves = (4 * n) - 4 - abs(r_q - c_q) - abs(r_q + c_q - n - 1)
    else:
        # const r_q
        left = max((obs[1] for obs in obstacles if obs[0] == r_q and obs[1] < c_q),default= 0) + 1 
        right= min((obs[1] for obs in obstacles if obs[0] == r_q and obs[1] > c_q),default = n + 1)
        moves += (right - left - 1)
        
        # const c_q
        up = min((obs[0] for obs in obstacles if obs[1] == c_q and obs[0] > r_q),default= n + 1)
        down = max((obs[0] for obs in obstacles if obs[1] == c_q and obs[0] < r_q),default= 0) + 1
        moves += (up - down - 1)
        
        #positive slope
        upper = min((obs for obs in obstacles if obs[0] > r_q and obs[1] > c_q and obs[0] - r_q == obs[1] - c_q), default = None)

        lower= max((obs for obs in obstacles if obs[0] < r_q and obs[1] < c_q and obs[0] - r_q == obs[1] - c_q), default = None)
                
        if upper and lower:
            moves += (upper[0] - r_q - 1)  + (r_q - lower[0] - 1)
            
        elif upper and not lower: 
            num = min(r_q, c_q) - 1
            moves += (upper[0] - r_q - 1) + num
            
        elif lower and not upper: 
            num = n - max(r_q, c_q) 
            moves += num + (r_q - lower[0] - 1)
            
        else:
            moves += (n - abs(r_q - c_q) - 1)
    
        #negative slope
        upper = min((obs for obs in obstacles if obs[0] > r_q and obs[1] < c_q and obs[0] - r_q == c_q - obs[1]), default = None)

        lower= max((obs for obs in obstacles if obs[0] < r_q and obs[1] > c_q and r_q - obs[0] == obs[1] - c_q), default = None)
                
        if upper and lower:
            moves += (upper[0] - r_q - 1) + (r_q - lower[0] - 1)
            
        elif upper and not lower: 
            num = min((r_q - 1) , (n - c_q))
            moves += num + (upper[0] - r_q - 1)
            
        elif lower and not upper: 
            num = min((c_q - 1) , (n - r_q))
            moves += num + (r_q - lower[0] - 1)
            
        else:
            moves += (n - abs(r_q + c_q - n - 1) - 1)
            

    return moves

```
