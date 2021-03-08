#include <windows.h>
#include <iostream>
#include <string>
#include <ctime>
using namespace std;


const int NONE = 0;
const int BLACK = 1;
const int WHITE = 2;
const int PAWN = 1;
const int BISHOP = 2;
const int KNIGHT = 3;
const int ROOK = 4;
const int QUEEN = 5;
const int KING = 6;

struct Square
{
	int color = 0;
	int piecetype = 0;
};

struct Position
{
	int x = 0;
	int y = 0;
};

bool canMovePiece(Square board[8][8], Position from, Position to, bool checkKingChecks = true);

void gotoyx(short y, short x)
{
	COORD coord = { x, y };
	SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), coord);
}

void printLogo()
{
	cout << "\t\t\t\t\t           88                                          "			<< endl;
	cout << "\t\t\t\t\t           88                                          "			<< endl;
	cout << "\t\t\t\t\t           88                                          "			<< endl;
	cout << "\t\t\t\t\t ,adPPYba, 88,dPPYba,   ,adPPYba, ,adPPYba, ,adPPYba,  "			<< endl;
	cout << "\t\t\t\t\ta8\"     \"\" 88P'    \"8a a8P_____88 I8[    \"\" I8[    \"\"  "	<< endl;
	cout << "\t\t\t\t\t8b         88       88 8PP\"\"\"\"\"\"\"  `\"Y8ba,   `\"Y8ba,   "	<< endl;
	cout << "\t\t\t\t\t\"8a,   ,aa 88       88 \"8b,   ,aa aa    ]8I aa    ]8I  "			<< endl;
	cout << "\t\t\t\t\t `\"Ybbd8\"' 88       88  `\"Ybbd8\"' `\"YbbdP\"' `\"YbbdP\"'  "	<< endl;
	cout << endl;
}

void resetBoard(Square board[8][8])
{
	for (int i = 0; i < 8; i++)
	{
		board[1][i].color = BLACK;
		board[1][i].piecetype = PAWN;
	}
	for (int i = 0; i < 8; i++)
	{
		board[6][i].color = WHITE;
		board[6][i].piecetype = PAWN;
	}

	board[0][0].color = BLACK;
	board[0][1].color = BLACK;
	board[0][2].color = BLACK;
	board[0][3].color = BLACK;
	board[0][4].color = BLACK;
	board[0][5].color = BLACK;
	board[0][6].color = BLACK;
	board[0][7].color = BLACK;

	board[0][0].piecetype = ROOK;
	board[0][1].piecetype = KNIGHT;
	board[0][2].piecetype = BISHOP;
	board[0][3].piecetype = QUEEN;
	board[0][4].piecetype = KING;
	board[0][5].piecetype = BISHOP;
	board[0][6].piecetype = KNIGHT;
	board[0][7].piecetype = ROOK;

	board[7][0].color = WHITE;
	board[7][1].color = WHITE;
	board[7][2].color = WHITE;
	board[7][3].color = WHITE;
	board[7][4].color = WHITE;
	board[7][5].color = WHITE;
	board[7][6].color = WHITE;
	board[7][7].color = WHITE;

	board[7][0].piecetype = ROOK;
	board[7][1].piecetype = KNIGHT;
	board[7][2].piecetype = BISHOP;
	board[7][3].piecetype = QUEEN;
	board[7][4].piecetype = KING;
	board[7][5].piecetype = BISHOP;
	board[7][6].piecetype = KNIGHT;
	board[7][7].piecetype = ROOK;
}

void printSquare(Square board[8][8], const int piecetype, const int color, int rowNum)
{
	if (color == 0)
	{
		if (piecetype == NONE)
		{
			if (rowNum == 0)
			{
				cout << "                |";
			}
			else if (rowNum == 1)
			{
				cout << "                |";
			}
			else if (rowNum == 2)
			{
				cout << "                |";
			}
			else if (rowNum == 3)
			{
				cout << "                |";
			}
			else if (rowNum == 4)
			{
				cout << "                |";
			}
			else if (rowNum == 5)
			{
				cout << "                |";
			}
			else if (rowNum == 6)
			{
				cout << "                |";
			}
			else if (rowNum == 7)
			{
				cout << "----------------+";
			}
		}
	}

	else if (color == 1)
	{
		if (piecetype == PAWN)
	{
		if (rowNum == 0)
		{
			cout << "       __       |";
		}
		else if (rowNum == 1)
		{
			cout << "      (  )      |";
		}
		else if (rowNum == 2)
		{
			cout << "       ||       |";
		}
		else if (rowNum == 3)
		{
			cout << "      /__\\      |";
		}
		else if (rowNum == 4)
		{
			cout << "     (____)     |";
		}
		else if (rowNum == 5)
		{
			cout << "     B Pawn     |";
		}
		else if (rowNum == 6)
		{
			cout << "                |";
		}
		else if (rowNum == 7)
		{
			cout << "----------------+";
		}
	}

		else if (piecetype == BISHOP)
	{
		if (rowNum == 0)
		{
			cout << "       <>_      |";
		}
		else if (rowNum == 1)
		{
			cout << "     (\\)  )     |";
		}
		else if (rowNum == 2)
		{
			cout << "      \\__/      |";
		}
		else if (rowNum == 3)
		{
			cout << "     (____)     |";
		}
		else if (rowNum == 4)
		{
			cout << "      |__|      |";
		}
		else if (rowNum == 5)
		{
			cout << "     /____\\     |";
		}
		else if (rowNum == 6)
		{
			cout << "    B Bishop    |";
		}
		else if (rowNum == 7)
		{
			cout << "----------------+";
		}
	}

		else if (piecetype == KNIGHT)
	{
		if (rowNum == 0)
		{
			cout << "    __/\"\"\"\"\"\\   |";
		}
		else if (rowNum == 1)
		{
			cout << "   ]___ 0   }   |";
		}
		else if (rowNum == 2)
		{
			cout << "       /    }   |";
		}
		else if (rowNum == 3)
		{
			cout << "      /~    }   |";
		}
		else if (rowNum == 4)
		{
			cout << "      \\____/    |";
		}
		else if (rowNum == 5)
		{
			cout << "     (______)   |";
		}
		else if (rowNum == 6)
		{
			cout << "    B kNight    |";
		}
		else if (rowNum == 7)
		{
			cout << "----------------+";
		}
	}

		else if (piecetype == ROOK)
	{
		if (rowNum == 0)
		{
			cout << "     WWWWWW     |";
		}
		else if (rowNum == 1)
		{
			cout << "      |  |      |";
		}
		else if (rowNum == 2)
		{
			cout << "      |  |      |";
		}
		else if (rowNum == 3)
		{
			cout << "      |__|      |";
		}
		else if (rowNum == 4)
		{
			cout << "     /____\\     |";
		}
		else if (rowNum == 5)
		{
			cout << "    (______)    |";
		}
		else if (rowNum == 6)
		{
			cout << "     B Rook     |";
		}
		else if (rowNum == 7)
		{
			cout << "----------------+";
		}
	}

		else if (piecetype == QUEEN)
	{
		if (rowNum == 0)
		{
			cout << "       ()       |";
		}
		else if (rowNum == 1)
		{
			cout << "     <~~~~>     |";
		}
		else if (rowNum == 2)
		{
			cout << "      \\__/      |";
		}
		else if (rowNum == 3)
		{
			cout << "      |__|      |";
		}
		else if (rowNum == 4)
		{
			cout << "     /____\\     |";
		}
		else if (rowNum == 5)
		{
			cout << "    (______)    |";
		}
		else if (rowNum == 6)
		{
			cout << "    B Queen     |";
		}
		else if (rowNum == 7)
		{
			cout << "----------------+";
		}
	}

		else if (piecetype == KING)
	{
		if (rowNum == 0)
		{
			cout << "      .::.      |";
		}
		else if (rowNum == 1)
		{
			cout << "    _/____\\_    |";
		}
		else if (rowNum == 2)
		{
			cout << "     \\____/     |";
		}
		else if (rowNum == 3)
		{
			cout << "      |__|      |";
		}
		else if (rowNum == 4)
		{
			cout << "     /    \\     |";
		}
		else if (rowNum == 5)
		{
			cout << "    (______)    |";
		}
		else if (rowNum == 6)
		{
			cout << "     B King     |";
		}
		else if (rowNum == 7)
		{
			cout << "----------------+";
		}
	}
	}

	else if (color == 2)
	{
		if (piecetype == PAWN)
		{
			if (rowNum == 0)
			{
				cout << "       __       |";
			}
			else if (rowNum == 1)
			{
				cout << "      (  )      |";
			}
			else if (rowNum == 2)
			{
				cout << "       ||       |";
			}
			else if (rowNum == 3)
			{
				cout << "      /__\\      |";
			}
			else if (rowNum == 4)
			{
				cout << "     (____)     |";
			}
			else if (rowNum == 5)
			{
				cout << "      Pawn      |";
			}
			else if (rowNum == 6)
			{
				cout << "                |";
			}
			else if (rowNum == 7)
			{
				cout << "----------------+";
			}
		}

		else if (piecetype == BISHOP)
		{
			if (rowNum == 0)
			{
				cout << "       <>_      |";
			}
			else if (rowNum == 1)
			{
				cout << "     (\\)  )     |";
			}
			else if (rowNum == 2)
			{
				cout << "      \\__/      |";
			}
			else if (rowNum == 3)
			{
				cout << "     (____)     |";
			}
			else if (rowNum == 4)
			{
				cout << "      |__|      |";
			}
			else if (rowNum == 5)
			{
				cout << "     /____\\     |";
			}
			else if (rowNum == 6)
			{
				cout << "     Bishop     |";
			}
			else if (rowNum == 7)
			{
				cout << "----------------+";
			}
		}

		else if (piecetype == KNIGHT)
		{
			if (rowNum == 0)
			{
				cout << "    __/\"\"\"\"\"\\   |";
			}
			else if (rowNum == 1)
			{
				cout << "   ]___ 0   }   |";
			}
			else if (rowNum == 2)
			{
				cout << "       /    }   |";
			}
			else if (rowNum == 3)
			{
				cout << "      /~    }   |";
			}
			else if (rowNum == 4)
			{
				cout << "      \\____/    |";
			}
			else if (rowNum == 5)
			{
				cout << "     (______)   |";
			}
			else if (rowNum == 6)
			{
				cout << "      kNight    |";
			}
			else if (rowNum == 7)
			{
				cout << "----------------+";
			}
		}

		else if (piecetype == ROOK)
		{
			if (rowNum == 0)
			{
				cout << "     WWWWWW     |";
			}
			else if (rowNum == 1)
			{
				cout << "      |  |      |";
			}
			else if (rowNum == 2)
			{
				cout << "      |  |      |";
			}
			else if (rowNum == 3)
			{
				cout << "      |__|      |";
			}
			else if (rowNum == 4)
			{
				cout << "     /____\\     |";
			}
			else if (rowNum == 5)
			{
				cout << "    (______)    |";
			}
			else if (rowNum == 6)
			{
				cout << "      Rook      |";
			}
			else if (rowNum == 7)
			{
				cout << "----------------+";
			}
		}

		else if (piecetype == QUEEN)
		{
			if (rowNum == 0)
			{
				cout << "       ()       |";
			}
			else if (rowNum == 1)
			{
				cout << "     <~~~~>     |";
			}
			else if (rowNum == 2)
			{
				cout << "      \\__/      |";
			}
			else if (rowNum == 3)
			{
				cout << "      |__|      |";
			}
			else if (rowNum == 4)
			{
				cout << "     /____\\     |";
			}
			else if (rowNum == 5)
			{
				cout << "    (______)    |";
			}
			else if (rowNum == 6)
			{
				cout << "     Queen      |";
			}
			else if (rowNum == 7)
			{
				cout << "----------------+";
			}
		}

		else if (piecetype == KING)
		{
			if (rowNum == 0)
			{
				cout << "      .::.      |";
			}
			else if (rowNum == 1)
			{
				cout << "    _/____\\_    |";
			}
			else if (rowNum == 2)
			{
				cout << "     \\____/     |";
			}
			else if (rowNum == 3)
			{
				cout << "      |__|      |";
			}
			else if (rowNum == 4)
			{
				cout << "     /    \\     |";
			}
			else if (rowNum == 5)
			{
				cout << "    (______)    |";
			}
			else if (rowNum == 6)
			{
				cout << "      King      |";
			}
			else if (rowNum == 7)
			{
				cout << "----------------+";
			}
		}
	}
}

void printBoard(Square board[8][8])
{
	HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);
	srand(time(0));
	cout << "\t\t\t\t\t\t\t  Welcome to Chess!" << endl;
	cout << "\t\t\t\t\t\tTo start playing choose the Game Mode!" << endl;
	cout << endl;
	printLogo();
	cout << "-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------" << endl;
	cout << endl;
	cout << endl;

	cout << "**********			\t\t\t\t\t\t\t\t" << "**********" << endl;
	cout << "**********   User 1		\t\t\t\t\t\t\t\t" << "**********   User 2" << endl;
	cout << "**********   Color - White	\t\t\t\t\t\t\t\t" << "**********   Color - Black" << endl;
	cout << "**********   Chance of wining: " << rand() % 99 + 1 << "%     \t\t\t\t\t\t\t\t" << "**********   Chance of wining: " << rand() % 99 + 1 << "%" << endl;
	cout << "**********			\t\t\t\t\t\t\t\t" << "**********" << endl;
	cout << endl;

	// Fancy version
	cout << "----------------+----------------+----------------+----------------+----------------+----------------+----------------+----------------+" << endl;
	for (int y = 0; y < 8; y++)
	{
		for (int rowNum = 0; rowNum < 8; rowNum++)
		{
			for (int x = 0; x < 8; x++)
			{
				printSquare(board, board[y][x].piecetype, board[y][x].color, rowNum);
			}
			cout << endl;
		}
	}

	gotoyx(17, 142);

	cout << "\t\t+---------White!----------|----------Black!---------+" << endl;
	for (int i = 0; i < 20; i++)
	{
		cout << "\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t|" << endl;
	}

	// Print the test board (Uses integers to display chess pieces)
	//cout << "  A B C D E F G H\n";
	//for (int i = 0; i < 8; i++)
	//{
	//	cout << 8 - i << " ";
	//	for (int j = 0; j < 8; j++)
	//	{
	//		cout << board[i][j].piecetype << " ";
	//	}
	//	cout << "\n";
	//}

	// Used to see the coordinates of the squares(y, x)
	//for (int i = 0; i < 8; i++)
	//{
	//	for (int j = 0; j < 8; j++)
	//	{
	//		cout << i << j << " ";
	//	}
	//	cout << "\n";
	//}
}

bool anyPieceInPosition(Square board[8][8], Position pos)
{
	return board[pos.y][pos.x].piecetype != NONE;
}

bool oppositeColors(Square board[8][8], Position from, Position to)
{
	if (board[to.y][to.x].piecetype == 0)
	{
		return true;
	}
	else if (board[to.y][to.x].piecetype == KING)
	{
		return false;
	}
	else if (board[from.y][from.x].color != board[to.y][to.x].color)
	{
		return true;
	}
	else
	{
		return false;
	}
}

void moveAPiece(Square board[8][8], Position from, Position to)
{
	board[to.y][to.x].piecetype = board[from.y][from.x].piecetype;
	board[to.y][to.x].color = board[from.y][from.x].color;

	board[from.y][from.x].color = NONE;
	board[from.y][from.x].piecetype = NONE;
}

// Pieces movement starts here----------------------------------------------------------
bool canPawnMove(Square board[8][8], Position from, Position to)
{

	// vertical movement
	if (abs(to.x - from.x) == 0 && !anyPieceInPosition(board, to))
	{
		if (abs(to.y - from.y) == 1 and ((to.y - from.y < 0 and board[from.y][from.x].color == BLACK) or (to.y - from.y > 0 and board[from.y][from.x].color == WHITE)))
		{
			return true;
		}

		// 2 move forward
		else if (abs(to.y - from.y) == 2 and (from.y == 6 or from.y == 1))
		{
			return true;
		}
	}
	// taking enemy piece
	else if (abs(to.x - from.x) == 1 and abs(to.y - from.y) == 1)
	{
		return anyPieceInPosition(board, to) and oppositeColors(board, from, to);
	}	

	return false;
}

bool canKnightMove(Square board[8][8], Position from, Position to)
{
	// you are not a Pawn (P.S. -- Acts like a Pawn by moving 1 forward)
	if (to.x == from.x)
	{
		return false;
	}
	// 2 move forward/Right or Left
	else if (to.y + 2 == from.y and oppositeColors(board, from, to) == true and from.x + 1 == to.x or from.x - 1 == to.x)
	{
		return true;
	}
	// 2 move backward/Right or Left
	else if (to.y - 2 == from.y and oppositeColors(board, from, to) == true and from.x + 1 == to.x or from.x - 1 == to.x)
	{
		return true;
	}
	// 2 move leftward/Up or Down
	else if (to.x - 2 == from.x and oppositeColors(board, from, to) == true and from.y + 1 == to.y or from.y - 1 == to.y)
	{
		return true;
	}
	// 2 move rightward/Up or Down
	else if (to.x + 2 == from.x and oppositeColors(board, from, to) == true and from.y + 1 == to.y or from.y - 1 == to.y)
	{
		return true;
	}
	// no other situations left
	else
	{
		return false;
	}
}

bool canBishopMove(Square board[8][8], Position from, Position to)
{
	int directionX = 0, directionY = 0;

	if (from.x > to.x)
	{
		directionX = -1;
	}
	else
	{
		directionX = 1;
	}

	if (from.y > to.y)
	{
		directionY = -1;
	}
	else
	{
		directionY = 1;
	}

	// Check the distance
	if (abs(from.y - to.y) == abs(from.x - to.x))
	{
		for (int x = from.x + directionX; x != to.x; x += directionX)
		{
			for (int y = from.y + directionY; y != to.y; y += directionY)
			{
				if (board[y][x].piecetype != NONE)
				{
					return false;
				}
			}
		}
		return true;
	}

	// No Other Moves Left
	else
	{
		return false;
	}
}

bool canRookMove(Square board[8][8], Position from, Position to)
{
	// x Axis Movement Up
	if (from.x == to.x and from.y > to.y)
	{
		for (int i = to.y; i < from.y; i++)
		{
			if (board[i][from.x].piecetype != NONE)
			{
				return false;
			}
		}
		return true;
	}
	// x Axis Movement Down
	else if (from.x == to.x and from.y < to.y)
	{
		for (int i = from.y + 1; i <= to.y; i++)
		{
			if (board[i][from.x].piecetype != NONE)
			{
				return false;
			}
		}
		return true;
	}

	// y Axis Movement Right
	else if (from.y == to.y and from.x < to.x)
	{
		for (int i = from.x + 1; i <= to.x; i++)
		{
			if (board[from.y][i].piecetype != NONE)
			{
				return false;
			}
		}
		return true;
	}
	// y Axis Movement Left
	else if (from.y == to.y and from.x > to.x)
	{
		for (int i = to.x; i < from.x; i++)
		{
			if (board[from.y][i].piecetype != NONE)
				{
					return false;
				}
		}
		return true;
	}


	// No Other Moves Left
	else
	{
		return false;
	}
}

bool canQueenMove(Square board[8][8], Position from, Position to)
{
	int directionX = 0, directionY = 0;

	if (from.x > to.x)
	{
		directionX = -1;
	}
	else
	{
		directionX = 1;
	}

	if (from.y > to.y)
	{
		directionY = -1;
	}
	else
	{
		directionY = 1;
	}

	cout << from.x << ", " << from.y << " -> " << \
		to.x << ", " << to.y << endl;
	// Check the distance
	if (abs(from.y - to.y) == abs(from.x - to.x))
	{
		for (int x = from.x + directionX; x != to.x; x += directionX)
		{
			for (int y = from.y + directionY; y != to.y; y += directionY)
			{
				cout << x << ", " << y << " -> ";
				if (board[y][x].piecetype != NONE)
				{
					std::cout << "NOT EMPTY\n";
					return false;
				}
				std::cout << "EMPTY\n";
			}
		}
		return true;
	}

	// x Axis Movement Up
	if (from.x == to.x and from.y > to.y)
	{
		for (int i = to.y; i < from.y; i++)
		{
			if (board[i][from.x].piecetype != NONE)
			{
				return false;
			}
		}
		return true;
	}
	// x Axis Movement Down
	else if (from.x == to.x and from.y < to.y)
	{
		for (int i = from.y + 1; i <= to.y; i++)
		{
			if (board[i][from.x].piecetype != NONE)
			{
				return false;
			}
		}
		return true;
	}

	// y Axis Movement Right
	else if (from.y == to.y and from.x < to.x)
	{
		for (int i = from.x + 1; i <= to.x; i++)
		{
			if (board[from.y][i].piecetype != NONE)
			{
				return false;
			}
		}
		return true;
	}
	// y Axis Movement Left
	else if (from.y == to.y and from.x > to.x)
	{
		for (int i = to.x; i < from.x; i++)
		{
			if (board[from.y][i].piecetype != NONE)
			{
				return false;
			}
		}
		return true;
	}


	// No Other Moves Left
	else
	{
		return false;
	}
}

bool canKingMove(Square board[8][8], Position from, Position to, bool checkKingChecks)
{
	// Cannot move more than one square in each direction
	if (abs(to.y - from.y) > 1 || abs(to.x - from.x) > 1)
	{
		return false;
	}

	// Just lazy :)
	Square king = board[from.y][from.x];

	// When checking if king can go to a
	// specific place, we don't need to check
	// if the king can go based on other
	// color (To avoid Stack Over Flow!)
	if (!checkKingChecks)
	{
		return true;
	}

	for (int y = 0; y < 8; y++)
	{
		for (int x = 0; x < 8; x++)
		{
			// We don't need to check pieces
			// of the same color and we don't care
			// about empty squares
			if (board[y][x].piecetype == NONE || board[y][x].color == king.color)
			{
				continue;
			}

			// Create Position object to pass to
			// canMoveX functions
			Position piecePos = { y, x };

			if (canMovePiece(board, piecePos, to, false))
			{
				return false;
			}
		}
	}
	return true;
}

bool canMovePiece(Square board[8][8], Position from, Position to, bool checkKingChecks)
{
	// TODO: Check other conditions here
	switch (board[from.y][from.x].piecetype)
	{
		case PAWN:		return canPawnMove(board, from, to);
		case KNIGHT:	return canKnightMove(board, from, to);
		case BISHOP:	return canBishopMove(board, from, to);
		case ROOK:		return canRookMove(board, from, to);
		case QUEEN:		return canQueenMove(board, from, to);
		case KING:		return canKingMove(board, from, to, checkKingChecks);
		default:
			return false;
	}
}

Position input()
{
	Position position = { 0, 0 };
	string inputedInfo;
	getline(cin, inputedInfo);

	if (inputedInfo.length() != 2)
	{
		cout << "Invalid piece assignment\n";
	}


	//--Start Converting---------------------------------------
	if (inputedInfo[0] > 96 and inputedInfo[0] < 123)
	{
		position.x = inputedInfo[0] - 17 - 48 - 32;
		position.y = 8 - (inputedInfo[1] - 48 - 1) - 1;
	}
	else if (inputedInfo[0] > 64 and inputedInfo[0] < 91)
	{
		position.x = inputedInfo[0] - 17 - 48;
		position.y = 8 - (inputedInfo[1] - 48 - 1) - 1;
	}


	//--cout << position.x << position.y << endl;--
	return position;
}

int main()
{
	//-----------------------SetUp!------------------------------
	Square board[8][8] = {};


	//-----------------------Welcome!------------------------------
	cout << "\t\t\t\t\t\t\t  Welcome to Chess!" << endl;
	cout << "\t\t\t\t\t\tTo start playing choose the Game Mode!" << endl;
	cout << endl;
	printLogo();


	//-----------------------GAME LOOP!------------------------------
	resetBoard(board);
	while (true)
	{
		system("CLS");
		printBoard(board);
		gotoyx(86, 0);
		Position from = input();
		gotoyx(86, 3);
		cout << ", ";
		Position to = input();

		// check if piece can move to destination
		if (canMovePiece(board, from, to, true))
		{

			// if it can, move the piece
			moveAPiece(board, from, to);
		}
	}
}
