# Largest-Submatrix-With-Rearrangements

You are given a binary matrix matrix of size m x n, and you are allowed to rearrange the columns of the matrix in any order.

Return the area of the largest submatrix within matrix where every element of the submatrix is 1 after reordering the columns optimally.

 

Example 1:


Input: matrix = [[0,0,1],[1,1,1],[1,0,1]]
Output: 4
Explanation: You can rearrange the columns as shown above.
The largest submatrix of 1s, in bold, has an area of 4.
Example 2:


Input: matrix = [[1,0,1,0,1]]
Output: 3
Explanation: You can rearrange the columns as shown above.
The largest submatrix of 1s, in bold, has an area of 3.
Example 3:

Input: matrix = [[1,1,0],[1,0,1]]
Output: 2
Explanation: Notice that you must rearrange entire columns, and there is no way to make a submatrix of 1s larger than an area of 2.
 

Constraints:

m == matrix.length
n == matrix[i].length
1 <= m * n <= 105
matrix[i][j] is either 0 or 1.

class Solution:
    def largestSubmatrix(self, matrix: List[List[int]]) -> int:
        
        m = len(matrix)
        n = len(matrix[0])
        colConsecOnes = [[0]*n for _ in range(m)]
        
        # For each column, find the number of consecutive ones ending at each position.
        for j in range(n):
            count = 0
            for i in range(m):
                if matrix[i][j] == 1:
                    count += 1
                else:
                    count = 0
                colConsecOnes[i][j] = count
        
        # For each row, rearrange columns optimally by sorting heights
        largestArea = 0
        for i in range(m):
            colConsecOnes[i].sort()  # ascending
            for j in range(n):
                height = colConsecOnes[i][j]
                width = n - j
                largestArea = max(largestArea, height * width)

        return largestArea
        
