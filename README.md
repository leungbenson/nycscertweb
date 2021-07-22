# [Benson Leung's Portfolio](https://github.com/hunter-teacher-cert/work_csci70900-leungbenson)

## Programming in Java

- [1](https://github.com/hunter-teacher-cert/work_csci70900-leungbenson/tree/master/1)
- [2](https://github.com/hunter-teacher-cert/work_csci70900-leungbenson/tree/master/2)
- [3](https://github.com/hunter-teacher-cert/work_csci70900-leungbenson/tree/master/3/skel)
- [4](https://github.com/hunter-teacher-cert/work_csci70900-leungbenson/tree/master/4)
- [5](https://github.com/hunter-teacher-cert/work_csci70900-leungbenson/tree/master/5)
- [6](https://github.com/hunter-teacher-cert/work_csci70900-leungbenson/tree/master/6)
- [7](https://github.com/hunter-teacher-cert/work_csci70900-leungbenson/tree/master/7)

## [Data Structures](https://github.com/hunter-teacher-cert/work_csci70900-leungbenson/tree/master/DS)
- [Lists](https://github.com/hunter-teacher-cert/work_csci70900-leungbenson/tree/master/DS/lists)
- [Maze](https://github.com/hunter-teacher-cert/work_csci70900-leungbenson/tree/master/DS/maze)
- [Sort](https://github.com/hunter-teacher-cert/work_csci70900-leungbenson/tree/master/DS/sort1)
- [Mode](https://github.com/hunter-teacher-cert/work_csci70900-leungbenson/tree/master/DS/mode)


## [Methods I](https://github.com/hunter-teacher-cert/work_csci70900-leungbenson/tree/master/meth1)
- [01_lesson]()
- [06_unplugged]()
- [NetLogo](https://github.com/hunter-teacher-cert/work_csci70900-leungbenson/blob/master/meth1/NetLogo.md)
- [Graph.java](https://github.com/hunter-teacher-cert/work_csci70900-leungbenson/blob/master/meth1/Graph.java)
- [Graph Notes](https://jamboard.google.com/d/1l5c3wiCegt2PTr3TbW21lGiX3nhcE4AKyp79FPV1SNE/viewer?f=1)

## Exemplar Code:
### Game of Life
```java

  
import java.io.*;
import java.util.*;

/**
Dwayne, Jiyoon, and Benson
   The Rules of Life:
   Survivals:
   * A cell with 2 or 3 living neighbours will survive for the next generation.
   Death:
   * Each cell with >3 neighbours will die from overpopulation.
   * Every cell with <2 neighbours will die from isolation.
   Birth:
   * Each dead cell adjacent to exactly 3 living neighbours is a birth cell. It will come alive next generation.
   NOTA BENE:  All births and deaths occur simultaneously. Together, they constitute a single generation
*/

public class Cgol{
  //initialize empty board (all cells dead)
  public static char[][] createNewBoard(int rows, int cols) {
    char[][] result = new char[rows][cols];
    for (int r = 0; r < result.length; r++){
      for (int c = 0; c< result[r].length; c++){
        result[r][c] = '_';
      }
    }
    return result;
  }


  //print the board to the terminal
  public static void printBoard(char[][] board) {
    for (int i = 0; i < board.length; i++){
      for (int j = 0; j < board[i].length; j++){
        System.out.print(board[i][j]+" ");
      }System.out.println();
    }
    System.out.println();
  }


  //set cell (r,c) to val
  public static void setCell(char[][] board, int r, int c, char val){
    board[r][c] = val;
  }


  //return number of living neigbours of board[r][c]
  public static int countNeighbors(char[][] board, int r, int c) {
    int numNeighbor = 0;
    /*(r-1,c-1)   (r-1,c)  (r-1,c+1)
      (r, c-1)     (r,c)    (r,c+1)
      (r+1,c-1)   (r+1,c)  (r+1,c+1) 
    */
    //checking non-edge cases
    //check edge cases, where r == 0 or board.length -1
    //where c == 0 or or board[0].length-1

    //non corner top row
    if (r==0&& c!=0 &&c!=board[0].length-1){ 
      //starts at r to prevent going above
      for (int i = r; i<=r+1;i++){ 
        for (int j = c-1; j<=c+1;j++){
          if (board[i][j]=='X'){
            numNeighbor++;
          }
        }
      } 
    }
    
    //non corner left column
    else if (c==0&&r!=0&&r!=board.length-1){ 
      for (int i = r-1; i<=r+1;i++){
        for (int j = c; j<=c+1;j++){
          if (board[i][j]=='X'){
            numNeighbor++;
          }
        }
      }
    }
    
    //noncorner bottom row
    else if (r==board.length-1 && c!=0&&c!=board[0].length-1){ 
      for (int i = r-1; i<=r;i++){
        for (int j = c-1; j<=c+1;j++){
          if (board[i][j]=='X'){
            numNeighbor++;
          }
        }
      }
    }

    //noncorner right col
    else if (c==board[0].length-1 && r!=0&&r!=board.length-1){ 
      for (int i = r-1; i<=r+1;i++){
        for (int j = c-1; j<=c;j++){
        if (board[i][j]=='X'){
          numNeighbor++;
          }
        }
      }
    }
    
    //top left corner
    else if(c==0 && r == 0){ 
      for (int i = r; i<=r+1;i++){
        for (int j = c; j<=c+1;j++){
          if (board[i][j]=='X'){
            numNeighbor++;
          }
        }
      }
    }
    
    //top right corner
    else if(c==board[0].length-1 && r == 0){ 
      for (int i = r; i<=r+1;i++){
        for (int j = c-1; j<=c;j++){
          if (board[i][j]=='X'){
            numNeighbor++;
          }
        }
      }
    }
    
    //bottom left corner
    else if(c==0 && r == board.length-1){ 
      for (int i = r-1; i<=r;i++){
        for (int j = c; j<=c+1;j++){
          if (board[i][j]=='X'){
            numNeighbor++;
          }
        }
      }
    }
    
    //bottom right corner
    else if(c==board[0].length-1 && r == board.length-1){ 
      for (int i = r-1; i<=r;i++){
        for (int j = c-1; j<=c;j++){
          if (board[i][j]=='X'){
            numNeighbor++;
          }
        }
      }
    }
    
    //non edge cases
    else{ 
      for (int i = r-1; i<=r+1;i++){
        for (int j = c-1; j<=c+1;j++){
          if (board[i][j]=='X'){
            numNeighbor++;
          }
        }
      }
    }
    
    //Subtract the cell being checked
    if (board[r][c]=='X'){
      numNeighbor--;
    }
    
    return numNeighbor;
  }


  /**
     precond: given a board and a cell
     postcond: return next generation cell state based on CGOL rules
     (alive 'X', dead ' ')
  */
  public static char getNextGenCell(char[][] board,int r, int c) {
    int neigh = countNeighbors(board, r, c);
    if (neigh <2 || neigh >3){//die if 0 , 1, or 4+ neighbors
      return '_';
    }else if (neigh == 3){ //birth
      return 'X';
    }else if (neigh == 2){ //return current condition
      return board[r][c];
    }else{
      return '-';
    }
  }


  //generate new board representing next generation
  public static char[][] generateNextBoard(char[][] board) {

    //make new board
    char[][] newBoard = createNewBoard(board.length,board[0].length);
    //loop through new board
    for(int rowNB = 0; rowNB < newBoard.length; rowNB++){
      for (int colNB = 0; colNB < newBoard[0].length;colNB++){
            newBoard[rowNB][colNB] = getNextGenCell(board,rowNB,colNB);
    //      //use countNeighbor to figure out if alive or not
        }
     }
    return newBoard;

    //should represent the new amount of Xs and Os based on position of living cells
    //if cell next to [r][c] is dead then cell it self is deal
    //if cell next to current cell != 'X' then current cell itself is the '0'
    //
  }
  
// ^ Levene

  public static void main( String[] args )
  {
    //Initialize empty board

    char[][] board;
    board = createNewBoard(15,15);
    System.out.println("Empty Board:");
    printBoard(board);
    System.out.println("--------------------------\n\n");

    //breathe life into some cells:

    //Static
    setCell(board, 1, 1, 'X');
    setCell(board, 2, 1, 'X');
    setCell(board, 2, 2, 'X');
    setCell(board, 1, 2, 'X');
    
    //Oscillating
    setCell(board, 8, 13, 'X');
    setCell(board, 9, 13, 'X');
    setCell(board, 10, 13, 'X');
    // setCell(board, 4, 4, 'X');

    //Traveling
    setCell(board, 6, 5, 'X');
    setCell(board, 7, 6, 'X');
    setCell(board, 8, 6, 'X');
    setCell(board, 8, 5, 'X');
    setCell(board, 8, 4, 'X');
       
    //Print 1st Gen
    System.out.println("Gen X:");
    printBoard(board);
    System.out.println("--------------------------\n\n");

    //Print 2nd Gen
    System.out.println("Gen X+1:");
    board = generateNextBoard(board);
    printBoard(board);
    System.out.println("--------------------------\n\n");

    //Print 3rd Gen
    System.out.println("Gen X+2:");
    board = generateNextBoard(board);
    printBoard(board);
    System.out.println("--------------------------\n\n");

  }//end main()

}//end class
