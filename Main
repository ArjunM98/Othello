/* 
 * File:   Lab6.c
 * Author: Arjun Mittal
 *
 * Created on March 7, 2017, 11:08 PM
 */

#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

//Returns if designated row and col are in the board space
bool positionInBounds (int row, int col, int boardSize) {
    
    char LETTER = 'a'; 
    
    if ((row >= 0) && (row <= boardSize)) {
        
        if ((col >= 0) && (col <= boardSize)) {
            return true; 
        }
      
    }
    
    //checks if the input is an !, the exit character
    else if ((row == col) && (row == -64)){
        return true; 
    }
    
    else {
        return false;
    }
    
}

//Checks whether the characters the user inputed were of correct value
bool correctInput (char userInput [3]) {
    
    if ((userInput[0] != 'W') && (userInput[0] != 'B') && (userInput[0] != '!')) {
        return false; 
    }
    
    else {
        return true; 
    }
    
}

//Input of intermediate values in game
void enterIntermediatePosition(char board[26][26], int boardSize){
    
    //general decleration of varibale
    char userInput[3]; 
    char LETTER = 'a'; 
    int row = 0; 
    int col = 0; 
    
    printf("Enter board configuration: \n"); 
    
    //Scans user input
    do {
        for (int i = 0; i < 3; i++){
            scanf(" %c", &userInput[i]);
            row = (int)(userInput[1] - LETTER);
            col = (int)(userInput[2] - LETTER);  
        }
    }
    while((correctInput(userInput) == false) || (positionInBounds(row, col, boardSize) == false)); 
    
    //stores user input into board
    while ((userInput[0] != userInput[1]) && (userInput[0] != userInput[2]) && (userInput[0] != '!')) {
        
        board[row][col] = userInput[0];
               

        do {
            for (int i = 0; i < 3; i++){
                scanf(" %c", &userInput[i]);
                row = (int)(userInput[1] - LETTER);
                col = (int)(userInput[2] - LETTER); 
            }
        }
        while((correctInput(userInput) == false) || (positionInBounds(row, col, boardSize) == false)); 
        
    }
    
}

//Initializes game board
void initializeBoard(char board[26][26], int boardSize) {
    
    int midPoint = (boardSize / 2) - 1; 
    int counter = 1; 
    
    for (int i = 0; i < boardSize; i++) {
        
        for (int j = 0; j < boardSize; j++) {
            
                board[i][j] = 'U';
                
            }
            
        }
    
    //Initializes the middle of the board    
    board[midPoint][midPoint] = 'W'; 
    board[midPoint][midPoint + 1] = 'B'; 
    board[midPoint + 1][midPoint] = 'B'; 
    board[midPoint + 1][midPoint + 1] = 'W'; 
    
}

//Initializes 2nd board which stroes location of correct moves
void initializeCorrectMovesBoard (bool board[26][26], int boardSize) {
    
    for (int i = 0; i < boardSize; i++) {
        
        for (int j = 0; j < boardSize; j++) {
            
                board[i][j] = false;
                
        }
            
    }
    
}

//prints board
void printBoard(char board[26][26], int boardSize) {
    
    char letter = 'a';
    
    printf("  ");
    for (int i = 0; i < boardSize; i++) {
        
        printf("%c", letter);
        letter += 1;
        
    }
    printf("\n");
    letter = 'a';
    
    for (int i = 0; i < boardSize; i++) {
        
        for (int j = 0; j <= boardSize; j++) {
               
                if (j == 0){
                    printf ("%c", letter + (i));
                    printf(" "); 
                }
                
                else {
                    printf("%c", board[i][j-1]);
                }
            }
        
        printf("\n");
        
    }
        
}

//checks if move is valid with respect to a specific direction
bool checkLegalInDirection (char board[26][26], int boardSize, int row, int col, char tile, int deltaRow, int deltaCol) {
    
    //Checks if they possible move is in bounds
    if (positionInBounds(row + (1*deltaRow), col + (1*deltaCol), boardSize)) {
        
        //Checks if the next square in specified direction hold the oponent tile
        if (board[row + (1*deltaRow)][col + (1*deltaCol)] == tile){
            
            row = row + (1 * deltaRow);
            col = col + (1 * deltaCol);
               
            //Checks if possible move direction contains your tile piece, enclosing the oponents pieces 
            while ((positionInBounds(row, col, boardSize)) && (board[row][col] != 'U')) {
                
                if (tile == 'W') {
                    if (board[row][col] == 'B') {
                        return true; 
                    }
                }
                
                else if (tile == 'B') {
                    if (board[row][col] == 'W') {
                        return true; 
                    }
                }
                
                    
                row = row + (1 * deltaRow);
                col = col + (1 * deltaCol); 
                   
            }
           
            return false;     
        }
    
        else {
            return false; 
        }
            
    }
}
        
//Finds the empty spaces in the board
void searchEmptySpaces (char board[26][26], int boardSize, int row, int col, char tile, bool correctMoves[26][26]) {
    
    //Checks the 8 directions around specified location to find an empty spot
    for (int i = (row - 1); i < (row + 2); i ++) {
        
        for (int j = (col -1); j < (col + 2); j++) {
            
            if ((positionInBounds(row, col, boardSize) == true)) {
                
                if (board[i][j] == 'U') { 
                    
                    //checks the 8 directions around empty location to determine if the current location is a valid move
                    for (int k = -1; k <= 1; k++) {
                        
                        for (int l = -1; l <= 1; l++) {
                            
                            if (checkLegalInDirection(board, boardSize, i, j, tile, k, l)) {
                                
                                correctMoves[i][j] = true; 
                    
                            }  
                            
                        }
                        
                    }
                    
                }
            }
            
        }
        
    }
    
}


void searchTile (char board[26][26], int boardSize, char tile, bool correctMoves[26][26]) {
   
    for (int i = 0; i < boardSize; i++) {
        
        for (int j = 0; j < boardSize; j++) {
            
            if (board[i][j] == tile) {
                
                searchEmptySpaces (board, boardSize, i, j, tile, correctMoves); 
                
            }
            
        }
    }
    
}

void printCorrectMoves (bool correctMoves [26][26], int boardSize) {
    
    char row = 0; 
    char col = 0; 
    
    for (int i = 0; i < boardSize; i++){
        
        for (int j = 0; j < boardSize; j++){
            
            if(correctMoves[i][j] == true) {
                
                row = (char)(i + 'a'); 
                col = (char)(j + 'a');
                
                printf("%c%c\n", row, col); 
                
            }
            
        }
    }
    
}

void storeAndChangeTile(char board[26][26], int boardSize, int row, int col, char tile, int deltaRow, int deltaCol) {
    
    while ((positionInBounds(row, col, boardSize)) && (board[row][col] != 'U')) {
                
        if (tile == 'W') {
            if (board[row][col] == 'W') {
                
                board[row][col] = 'B';
                
            }
        }
                
        if (tile == 'B') {
            if (board[row][col] == 'B') {
                
                board[row][col] = 'W';
                
            }
        }
                                 
        row = row + (1 * deltaRow);
        col = col + (1 * deltaCol); 
                   
    }
    
}

void userMove (char board[26][26], int boardSize) {
    
    char userInput[3]; 
    char LETTER = 'a'; 
    int row = 0; 
    int col = 0;
    char tile = 0; 
    int rowDir = 0; 
    int colDir = 0; 
    bool validMove = false; 
    
    printf("Enter a move: \n"); 
    
    do {
        for (int i = 0; i < 3; i++){
            scanf(" %c", &userInput[i]);
            row = (int)(userInput[1] - LETTER);
            col = (int)(userInput[2] - LETTER);  
        }
    }
    while((correctInput(userInput) == false) || (positionInBounds(row, col, boardSize) == false)); 
    
    if (userInput[0] == 'W') {
        tile = 'B';
    }
    else if (userInput[0] == 'B') {
        tile = 'W';
    }
    
    for (int i = -1; i <= 1; i++) {
                        
         for (int j = -1; j <= 1; j++) {
             
            if (checkLegalInDirection(board, boardSize, row, col, tile, i, j)){
                
                validMove = true; 
                board[row][col] = userInput[0]; 
                storeAndChangeTile (board, boardSize, row, col, tile, i, j);
                
            }
             
        }
         
    }
    
    if (validMove == false){
        printf("Invalid move.\n");
    }
    else if(validMove == true){
        printf("Valid move.\n"); 
    }
        
}

int main() {
    
    char board [26][26]; 
    bool correctMoves [26][26];
    int boardSize = 0; 
    
    do {
        printf("Enter the board dimension: "); 
        scanf("%d", &boardSize);
    } 
    
    while((boardSize < 0) || (boardSize > 26));

    initializeBoard(board, boardSize); 
    
    printBoard(board, boardSize);
    
    enterIntermediatePosition(board, boardSize);
    
    printBoard(board, boardSize);
    
    printf("Available moves for W: \n");
    initializeCorrectMovesBoard (correctMoves, boardSize); 
    searchTile(board, boardSize, 'B', correctMoves);    
    printCorrectMoves(correctMoves, boardSize);
    
    printf("Available moves for B: \n");
    initializeCorrectMovesBoard (correctMoves, boardSize); 
    searchTile(board, boardSize, 'W', correctMoves);    
    printCorrectMoves(correctMoves, boardSize);
    
    userMove(board, boardSize);
    
    printBoard(board, boardSize);
    
    return (EXIT_SUCCESS);
}
