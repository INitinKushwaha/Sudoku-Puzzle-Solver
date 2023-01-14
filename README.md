# Sudoku-Puzzle-Solver
Here we use backtracking for sudoku solving problem
//
// Source code recreated from a .class file by IntelliJ IDEA
// (powered by FernFlower decompiler)
//

public class SudokuPuzzle {
    public SudokuPuzzle() {
    }

    public boolean isSafe(int[][] b, int r, int c, int n) {
        int sqt;
        for(sqt = 0; sqt < b.length; ++sqt) {
            if (b[r][sqt] == n) {
                return false;
            }
        }

        for(sqt = 0; sqt < b.length; ++sqt) {
            if (b[sqt][c] == n) {
                return false;
            }
        }

        sqt = (int)Math.sqrt((double)b.length);
        int boxRowSt = r - r % sqt;
        int boxColSt = c - c % sqt;

        for(int r1 = boxRowSt; r1 < boxRowSt + sqt; ++r1) {
            for(int d = boxColSt; d < boxColSt + sqt; ++d) {
                if (b[r1][d] == n) {
                    return false;
                }
            }
        }

        return true;
    }

    public boolean solveSudoku(int[][] b, int num) {
        int r = -1;
        int c = -1;
        boolean isVacant = true;

        int no;
        for(no = 0; no < num; ++no) {
            for(int j = 0; j < num; ++j) {
                if (b[no][j] == 0) {
                    r = no;
                    c = j;
                    isVacant = false;
                    break;
                }
            }

            if (!isVacant) {
                break;
            }
        }

        if (isVacant) {
            return true;
        } else {
            for(no = 1; no <= num; ++no) {
                if (this.isSafe(b, r, c, no)) {
                    b[r][c] = no;
                    if (this.solveSudoku(b, num)) {
                        return true;
                    }

                    b[r][c] = 0;
                }
            }

            return false;
        }
    }

    public void display(int[][] b, int n) {
        for(int i = 0; i < n; ++i) {
            for(int d = 0; d < n; ++d) {
                System.out.print(b[i][d]);
                System.out.print(" ");
            }

            System.out.print("\n");
            if ((i + 1) % (int)Math.sqrt((double)n) == 0) {
                System.out.print("");
            }
        }

    }

    public static void main(String[] argvs) {
        int[][] b = new int[][]{{7, 0, 0, 0, 0, 0, 2, 0, 0}, {4, 0, 2, 0, 0, 0, 0, 0, 3}, {0, 0, 0, 2, 0, 1, 0, 0, 0}, {3, 0, 0, 1, 8, 0, 0, 9, 7}, {0, 0, 9, 0, 7, 0, 6, 0, 0}, {6, 5, 0, 0, 3, 2, 0, 0, 1}, {0, 0, 0, 4, 0, 9, 0, 0, 0}, {5, 0, 0, 0, 0, 0, 1, 0, 6}, {0, 0, 6, 0, 0, 0, 0, 0, 8}};
        SudokuPuzzle obj = new SudokuPuzzle();
        int size = b.length;
        System.out.println("The grid is: ");

        for(int i = 0; i < size; ++i) {
            for(int j = 0; j < size; ++j) {
                System.out.print(b[i][j] + " ");
            }

            System.out.println();
        }

        System.out.println();
        if (obj.solveSudoku(b, size)) {
            System.out.println("The solution of the grid is: ");
            obj.display(b, size);
        } else {
            System.out.println("There is no solution available.");
        }

    }
}
