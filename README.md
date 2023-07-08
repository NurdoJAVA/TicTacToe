# TicTacToe
import java.util.Random;
import java.util.Arrays;
import java.util.Scanner;
import java.util.ArrayList;
import java.util.List;

public class Main {

    static ArrayList<Integer> playerPositions = new ArrayList<Integer>();
    static ArrayList<Integer> pcPositions = new ArrayList<Integer>();

    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);

        char[][] gameBoard = {{' ', '|',' ','|',' '},
                {'-', '+','-','+','-'},
                {' ', '|',' ','|',' '},
                {'-', '+','-','+','-'},
                {' ', '|',' ','|',' '}};
        printGameBoard(gameBoard);

        while (true) {
            System.out.println("Enter your placement 1-9: ");
            int playerPos = scan.nextInt();
            while (playerPositions.contains(playerPos)||pcPositions.contains(playerPos)){
                System.out.println("Position is taken! Try correct position!");
                playerPos = scan.nextInt();
            }

            placePiece(gameBoard, playerPos, "player");
            String result = checkWinner();
            if (result.length()>0) {
                printGameBoard(gameBoard);
                System.out.println(result);
                break;
            }

            Random rand = new Random();
            int pcPos = rand.nextInt(9) + 1;
            while (playerPositions.contains(pcPos)||pcPositions.contains(pcPos)){
                pcPos = rand.nextInt(9) + 1;
            }
            placePiece(gameBoard, pcPos, "pc");

            printGameBoard(gameBoard);

            result = checkWinner();
            if (result.length()>0) {
                printGameBoard(gameBoard);
                System.out.println(result);
                break;
            }
        }
    }

    public static String checkWinner(){

        List topRow = Arrays.asList(1, 2, 3);
        List midRow = Arrays.asList(4, 5, 6);
        List botRow = Arrays.asList(7, 8, 9);
        List leftCol = Arrays.asList(1, 4, 7);
        List midCol = Arrays.asList(2, 5, 8);
        List rightCol = Arrays.asList(3, 6, 9);
        List cross1 = Arrays.asList(1, 5, 9);
        List cross2 = Arrays.asList(3, 5, 7);

        List<List> winning = new ArrayList<List>();
        winning.add(topRow);
        winning.add(midRow);
        winning.add(botRow);
        winning.add(leftCol);
        winning.add(midCol);
        winning.add(rightCol);
        winning.add(cross1);
        winning.add(cross2);

        for (List l : winning){
            if (playerPositions.containsAll(l)){
                return "You are the winner!";
            } else if (pcPositions.containsAll(l)) {
                return "PC is the winner!";
            } else if (playerPositions.size() + pcPositions.size() == 9) {
                return "DRAW!";
            }
        }

        return "";
    }

    public static void placePiece(char[][]gameBoard,int pos, String user) {

        char symbol =' ';
        if (user.equals("player")){
            symbol = 'X';
            playerPositions.add(pos);
        } else if (user.equals("pc")) {
            symbol = 'O';
            pcPositions.add(pos);
        }

        switch (pos){
            case 1:
                gameBoard[0][0] = symbol;
                break;
            case 2:
                gameBoard[0][2] = symbol;
                break;
            case 3:
                gameBoard[0][4] = symbol;
                break;
            case 4:
                gameBoard[2][0] = symbol;
                break;
            case 5:
                gameBoard[2][2] = symbol;
                break;
            case 6:
                gameBoard[2][4] = symbol;
                break;
            case 7:
                gameBoard[4][0] = symbol;
                break;
            case 8:
                gameBoard[4][2] = symbol;
                break;
            case 9:
                gameBoard[4][4] = symbol;
                break;
        }
    }
    public static void printGameBoard(char[][] gameBoard){
        for (char[] row: gameBoard){
            for (char c : row){
                System.out.print(c);
            }
            System.out.println();
        }
    }
}
