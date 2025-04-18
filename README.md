package com.spielart;

/**
 * Der Code verwendet grundlegende Konzepte der objektorientierten Programmierung und der GUI-Entwicklung mit Java Swing
 * 
* Diese Klasse implementiert ein einfaches Tic-Tac-Toe-Spiel mit einer 4x4-Spielfeldmatrix.
* Das Spiel wird über eine grafische Benutzeroberfläche (GUI) gesteuert, die mit Java Swing erstellt wurde.

* Die Spieler (X und O) wechseln sich ab, um ihre Symbole in die Felder zu setzen. Das Spiel überprüft nach 
* jedem Zug, ob ein Spieler gewonnen hat, indem es alle möglichen Gewinnkombinationen überprüft. Wenn ein Spieler 
* gewinnt, werden die entsprechenden Felder hervorgehoben und das Spiel wird beendet.

* Die GUI besteht aus einem JFrame, das das Hauptfenster darstellt, und zwei JPanels: eines für den Titel und eines
* für die Schaltflächen des Spielfelds. Die Schaltflächen sind in einem 4x4-Grid angeordnet und reagieren auf Klicks,
* um die Züge der Spieler zu verarbeiten.

* Die Klasse implementiert das ActionListener-Interface, um auf Benutzeraktionen (Klicks auf die Schaltflächen) 
* zu reagieren.

* @author M. Boudni
* @version 1.0
*/

import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Font;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Random;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;

public class TicTacToe implements ActionListener { // Implementierung vom ActionListener-Interface

	// ****************** Instanzvariablen ********************

	/**
	 * GUI-Entwicklung mit Java Swing zur Darstellung und Steuerung des Spiels
	 */
	Random random = new Random(); // Zufälliger Startspieler

	JFrame frame = new JFrame(); // Hauptfenster des Spiels
	JPanel titleJPanel = new JPanel(); // für den Titel
	JPanel btnJPanel = new JPanel(); // für das Spielfeld
	JLabel textJLabel = new JLabel();
	JButton[] buttons = new JButton[16]; // 16 Buttons im Spielfeld sind Instanzen von JButton und in einem 4x4-Grid
											// angeordnet.
	boolean player1turn;

	// ****************** Konstruktor ********************

	public TicTacToe() {
		
		//******************* Frame-Konfiguration *********************
		
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		frame.setSize(800, 800);
		frame.setLayout(new BorderLayout());
		frame.getContentPane().setBackground(Color.gray);
		frame.setTitle("IT Alfatraining");

		frame.setVisible(true);

		textJLabel.setBackground(new Color(25, 25, 0));
		textJLabel.setForeground(new Color(25, 255, 0));
		textJLabel.setFont(new Font("Ink Free", Font.ITALIC, 75));
		textJLabel.setHorizontalAlignment(JLabel.CENTER);
		textJLabel.setText("test Text");
		textJLabel.setOpaque(true);

		btnJPanel.setLayout(new GridLayout(4, 4));

		// ******************* Button-Initialisierung *******************

		for (int i = 0; i < 16; i++) { // Erstellung und Konfigurierung der 16 Spielfeld-Buttons

			buttons[i] = new JButton();
			btnJPanel.add(buttons[i]);
			buttons[i].setFont(new Font("MV Boli", Font.ITALIC, 150));
			buttons[i].setFocusable(false);
			buttons[i].addActionListener(this);
		}

		titleJPanel.setLayout(new BorderLayout());
		titleJPanel.setBounds(0, 0, 800, 100);
		titleJPanel.add(textJLabel);
		frame.add(titleJPanel, BorderLayout.NORTH);
		frame.add(btnJPanel);

		firstTurn();   // Methodenaufruf am Ende des Konstruktors der TicTacToe-Klasse  
	}

	// ************** Implementierung der Hauptspiellogik *******************

	@Override
	public void actionPerformed(ActionEvent e) {

		for (int i = 0; i < 16; i++) {
			if (e.getSource() == buttons[i]) {
				if (player1turn) {
					if (buttons[i].getText() == "") {
						buttons[i].setText("X");
						buttons[i].setForeground(Color.green);

						player1turn = false;
						textJLabel.setText("O turn");
						checkwinner();
					}
				} else {
					if (buttons[i].getText() == "") {
						buttons[i].setText("O");
						buttons[i].setForeground(Color.red);

						player1turn = true;
						textJLabel.setText("X turn");
						
						checkwinner();
					}
				}
			}
		}
	}

	public void firstTurn() {  // Hier wird es zufällig bestimmt, welcher Spieler das Spiel beginnt.
		
		if (random.nextInt(2) == 0) {
			player1turn = true;
			textJLabel.setText("X turn");
		} else {
			player1turn = false;
			textJLabel.setText("O turn");
		}
	}
	
	//************ // Prüfung aller möglichen Gewinnkombinationen *************

	public void checkwinner() { 

		if (buttons[0].getText() == "X" && buttons[1].getText() == "X" && buttons[2].getText() == "X"
				&& buttons[3].getText() == "X") {

			xWins(0, 1, 2, 3);
		}
		if (buttons[4].getText() == "X" && buttons[5].getText() == "X" && buttons[6].getText() == "X"
				&& buttons[7].getText() == "X") {

			xWins(4, 5, 6, 7);
		}
		if (buttons[8].getText() == "X" && buttons[9].getText() == "X" && buttons[10].getText() == "X"
				&& buttons[11].getText() == "X") {

			xWins(8, 9, 10, 11);
		}
		if (buttons[12].getText() == "X" && buttons[13].getText() == "X" && buttons[14].getText() == "X"
				&& buttons[15].getText() == "X") {

			xWins(12, 13, 14, 15);
		}
		if (buttons[0].getText() == "X" && buttons[4].getText() == "X" && buttons[8].getText() == "X"
				&& buttons[12].getText() == "X") {

			xWins(0, 4, 8, 12);
		}
		if (buttons[1].getText() == "X" && buttons[5].getText() == "X" && buttons[9].getText() == "X"
				&& buttons[13].getText() == "X") {

			xWins(1, 5, 9, 13);
		}

		if (buttons[2].getText() == "X" && buttons[6].getText() == "X" && buttons[10].getText() == "X"
				&& buttons[14].getText() == "X") {

			xWins(2, 6, 10, 14);
		}
		if (buttons[3].getText() == "X" && buttons[7].getText() == "X" && buttons[11].getText() == "X"
				&& buttons[15].getText() == "X") {

			xWins(3, 7, 11, 15);
		}
		if (buttons[0].getText() == "X" && buttons[5].getText() == "X" && buttons[10].getText() == "X"
				&& buttons[15].getText() == "X") {

			xWins(0, 5, 10, 15);
		}
		if (buttons[3].getText() == "X" && buttons[6].getText() == "X" && buttons[9].getText() == "X"
				&& buttons[12].getText() == "X") {

			xWins(3, 6, 9, 12);
		}

		if (buttons[0].getText() == "O" && buttons[1].getText() == "O" && buttons[2].getText() == "O"
				&& buttons[3].getText() == "O") {

			oWins(0, 1, 2, 3);
		}
		if (buttons[4].getText() == "O" && buttons[5].getText() == "O" && buttons[6].getText() == "O"
				&& buttons[7].getText() == "O") {

			oWins(4, 5, 6, 7);
		}
		if (buttons[8].getText() == "O" && buttons[9].getText() == "O" && buttons[10].getText() == "O"
				&& buttons[11].getText() == "O") {

			oWins(8, 9, 10, 11);
		}
		if (buttons[12].getText() == "O" && buttons[13].getText() == "O" && buttons[14].getText() == "O"
				&& buttons[15].getText() == "O") {

			oWins(12, 13, 14, 15);
		}
		if (buttons[0].getText() == "O" && buttons[4].getText() == "O" && buttons[8].getText() == "O"
				&& buttons[12].getText() == "O") {

			oWins(0, 4, 8, 12);
		}
		if (buttons[1].getText() == "O" && buttons[5].getText() == "O" && buttons[9].getText() == "O"
				&& buttons[13].getText() == "O") {

			oWins(1, 5, 9, 13);
		}
		if (buttons[2].getText() == "O" && buttons[6].getText() == "O" && buttons[10].getText() == "O"
				&& buttons[14].getText() == "O") {

			oWins(2, 6, 10, 14);
		}
		if (buttons[3].getText() == "O" && buttons[7].getText() == "O" && buttons[11].getText() == "O"
				&& buttons[15].getText() == "O") {

			oWins(3, 7, 11, 15);
		}
		if (buttons[0].getText() == "O" && buttons[5].getText() == "O" && buttons[10].getText() == "O"
				&& buttons[15].getText() == "O") {

			oWins(0, 5, 10, 15);
		}
		if (buttons[3].getText() == "O" && buttons[6].getText() == "O" && buttons[9].getText() == "O"
				&& buttons[12].getText() == "O") {

			oWins(3, 6, 9, 12);
		}
	}

	// ******************* Gewinner-Methoden *********************

	/**
	 * der Gewinnfall wird für beide Spieler behandelt
	 * 
	 * @param x
	 * @param y
	 * @param v
	 * @param z
	 */

	public void xWins(int x, int y, int v, int z) {
		buttons[x].setBackground(Color.yellow);
		buttons[y].setBackground(Color.yellow);
		buttons[v].setBackground(Color.yellow);
		buttons[z].setBackground(Color.yellow);

		for (int i = 0; i < 16; i++) {
			buttons[i].setEnabled(false);
		}
		textJLabel.setText("X gewinnt");
	}

	public void oWins(int x, int y, int v, int z) {
		buttons[x].setBackground(Color.yellow);
		buttons[y].setBackground(Color.yellow);
		buttons[v].setBackground(Color.yellow);
		buttons[z].setBackground(Color.yellow);

		for (int i = 0; i < 16; i++) {
			buttons[i].setEnabled(false);
		}
		textJLabel.setText("O gewinnt");
	}
public class Main {

	public static void main(String[] args) {
		
		TicTacToe ticTacToe = new TicTacToe();

	}
}

