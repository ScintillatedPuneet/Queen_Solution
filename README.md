# Queen_Solution

import java.util.InputMismatchException;
import java.util.Scanner;

public class Queens {
	  public static void main(String[] args) {
	   
		int[][] board = new int[8][8];
	    for (int i = 0; i < 8; i++) {
	      for (int j = 0; j < 8; j++) {
	        System.out.print("" + i + "" + j + " ");
	      }
	      System.out.println();
	    }
	    
	    try {
	        Scanner sc = new Scanner(System.in);
	        System.out.println("Enter Number where you want to place your queen : ");
	        int num = sc.nextInt();
	        int row = num/10;
	        int col = num%10;
	        board[row][col] = 1;
	        
	        // Try to place the remaining 7 queens
	        placeQueens(board, 1, row, col);
          
	     }catch(ArrayIndexOutOfBoundsException e) {
	    	System.out.println("Please Enter a number from board.");
	     } 
	      catch(InputMismatchException ime) {
	        System.out.println("Invalid input. Please enter a number from board!");
	     }
	 }
	    

	  public static boolean placeQueens(int[][] board, int queensPlaced, int fixedRow, int fixedCol) {
	    if (queensPlaced == 8) {
	      // All queens have been placed successfully
	      printBoard(board);
	      return true;
	    }

	    // Try to place the next queen in each row
	    for (int row = 0; row < 8; row++) {
	      if (row == fixedRow) {
	        // Skip the row with the fixed queen
	        continue;
	      }
	      for (int col = 0; col < 8; col++) {
	        if (col == fixedCol) {
	          // Skip the column with the fixed queen
	          continue;
	        }
	        if (isValid(board, row, col)) {
	          // Place the queen and recursively try to place the remaining queens
	          board[row][col] = 1;
	          if (placeQueens(board, queensPlaced + 1, fixedRow, fixedCol)) {
	            return true;
	          }
	          // Backtrack and try the next column
	          board[row][col] = 0;
	        }
	      }
	    }
	    return false;
	  }

	  public static boolean isValid(int[][] board, int row, int col) {
	    // Check if the current position is under attack from any of the already placed queens
	    for (int i = 0; i < 8; i++) {
	      for (int j = 0; j < 8; j++) {
	        if (board[i][j] == 1 && (i == row || j == col || i + j == row + col || i - j == row - col)) {
	          return false;
	        }
	      }
	    }
	    return true;
	  }

	  public static void printBoard(int[][] board) {
	    for (int i = 0; i < 8; i++) {
	      for (int j = 0; j < 8; j++) {
	        System.out.print(board[i][j] + " ");
	      }
	      System.out.println();
	    }
	  }
	}

