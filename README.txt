#include <iostream>
#include <conio.h>
#include <ctime>
#include <Windows.h>

using namespace std;

bool gameOver;
bool error = false;
const int height = 20; 
const int width = 30;
int heightMenu = 10;
int widthMenu = 50;
int l, GameMode;
int score, x, y, lives, s1, arrX[5], affX1[5], k, d, n, timer = 60000, a, f;

enum eDirection {STOP = 0, LEFT, RIGHT, UP};
eDirection dir;



void StartMenu()
{
	for (int i = 0; i < heightMenu; i++)
	{
		for (int k = 0; k < widthMenu; k++)
		{

			if (i == (heightMenu - 9) && k == (widthMenu / 2 - 5)) {
				cout << "BRICK GAME";
				l += 10;
			}
			if (i == (heightMenu - 7) && k == 5) {
				cout << "Enter Game Mode: ";
				cin >> GameMode;
				l += 15;
			}

			else if (i > 0 && i < (heightMenu - 1) && k>2 && k < (widthMenu - 1) && l == 0)cout << char(32);
			if (l > 0)l--;
		}
		cout << "\n";

	}

}

void End()
{
	if (score >= 1000)a = 3;
	if (score >= 10000)a = 5;
	if (score >= 100000)a = 6;
	if (score >= 1000000)a = 7;
	f = 12 + a;

	system("cls");

	for (int i = 0; i < height; i++)
	{
		for (k = 0; k < width; k++)
		{
			if (i == height - (height - 1) && k == 0)cout << " ";
			if (k == (width - (width - 1)) && i == height - (height - 1))cout << char(218);
			if (i == height - (height - 1) && k > 1 && k < (width - 2))cout << char(196);
			if (i == height - (height - 1) && k == (width - 1))cout << char(191);
			if (i > 1 && i < height - 1 && (k == width - (width - 1) || k == width - 3))cout << char(32) << char(179);
			if (i == height - 1 && k == 1)cout << char(192);
			if (i == height - 1 && k == 0)cout << " ";
			if (i == height - 1 && k == width - 3)cout << char(217);
			if (i == height - 1 && k > 0 && k < width - 3)cout << char(196);

			if (i == 6 && k == width / 2 - 4 && error)
			{
				cout << "Error";
				d += 5;

			}

			if (i == 8 && k == 8 && error)
			{
				cout << "Press any key";
				d += 13;

			}

			if (i == 9 && k == 4 && error)
			{
				cout << "to close this window";
				d += 20;

			}

			if (i == 6 && k == width / 2 - 4  && !error)
			{
				cout << "GAME OVER";
				d += 9;

			}

			if (i == 8 && k == width / 2 - 8&& !error)
			{
				cout << "YOUR SCORE " << score;
				d += f;

			}
			if (d > 0) d -= 1;
			else if (i > 1 && i < height - 1 && k > 1 && k < width - 1 && d == 0) cout << " ";

		}
		cout << "\n";
	}
	Sleep(9000);
}

void ErrorMenu()
{
	if (GameMode != 0 && GameMode != 1)
	{
		for (int i = 0; i < heightMenu; i++)
		{
			for (int k = 0; k < widthMenu; k++)
			{

				if (i == (heightMenu - 9) && k == (widthMenu / 2 - 5)) {
					cout << "ERROR";
					l += 10;
				}
				if (i == (heightMenu - 7) && k == 5) {
					cout << "Please change correct gamemode 0 or 1";
					l += 15;
				}

				else if (i > 0 && i < (heightMenu - 1) && k>2 && k < (widthMenu - 1) && l == 0)cout << char(32);
				if (l > 0)l--;
			}
			cout << "\n";

		}
		error = true;
	}
	
}

void Setup()
{
	StartMenu();
	ErrorMenu();
	gameOver = false;
	lives = 5;
	score = 0;
	dir = STOP;
	x = width / 2;
}

void Draw()
{
	system("cls");
	
   for (int i = 0; i < height; i++)
   {
	   for ( k = 0; k < width; k++)
	   {
		   if (i == height - (height - 1) && k == 0)cout << " ";
		   if (k == (width - (width - 1)) && i == height - (height - 1))cout << char(218);
		   if (i == height - (height - 1) && k > 1 && k < (width - 2))cout << char(196);
		   if (i == height - (height - 1) && k == (width - 1))cout << char(191) << "\t" << "score: " << score;
		   if (i > 1 && i < height - 1 && (k == width - (width - 1) || k == width - 3))cout << char(32) << char(179);
		   if (i == height - 1 && k == 1)cout << char(192);
		   if (i == height - 1 && k == 0)cout << " ";
		   if (i == height - 1 && k == width - 3)cout << char(217);
		   if (i == height - 1 && k > 0 && k < width - 3)cout << char(196);
		   if (i == 4 && (k == width - 3))cout << "\t" << "lives: " << lives;
		   if (i == 6 && (k == width - 3) && GameMode == 0)cout << "\t" << "time(seconds): " << timer;
		   
		   if (i == height - 3 && k == x)
		   {
			   cout << "#";
			   d++;
		   }
		   if (i == height - 4 && k == x && dir == UP)
		   {
			   cout << "o";
			   d++;
			   s1 = k;
			   if (s1 != affX1[4] && s1 != affX1[1] && s1 != affX1[2] && s1 != affX1[3])
			   {
				   lives--;
			   }
			   if (s1 == affX1[1])
			   {
				   n--;
				   affX1[1] = arrX[1];
				   score += 500;
			   }
			   if (s1 == affX1[2])
			   {
				   n--;
				   affX1[2] = arrX[2];
				   score += 500;
			   }
			   if (s1 == affX1[3])
			   {
				   n--;
				   affX1[3] = arrX[3];
				   score += 500;
			   }
			   if (s1 == affX1[4])
			   {
				   n--;
				   affX1[0] = arrX[2];
				   score += 500;
			   }
		   }
		   if (i == height - 2 && k == x - 1)
		   {
			   cout << "###";
			   d+=3;
		   }
		   if (n < 5 && i == 2 && k > 2 && k < (width - 3) && ( k == arrX[1] || k == arrX[2] || k == arrX[3] || k == arrX[4]))
		   {
			   cout << "@";
			   n++;
			   if (k == arrX[1])affX1[1] = arrX[1];
			   if (k == arrX[2])affX1[2] = arrX[2];
			   if (k == arrX[3])affX1[3] = arrX[3]; 
			   if (k == arrX[4])affX1[4] = arrX[4];
		   }
		   if (i == 2 && k > 2 && k < (width - 3) && (k == affX1[1] || k == affX1[2] || k == affX1[3] || k == affX1[4]))
		   {
			   cout << "@";
			   d++;
			   
		   }
		   if (d > 0) d -= 1;
		   else if(i > 1 && i < height - 1 && k > 1 && k < width -1 && d == 0) cout << " ";
		   
	   }
	   cout << "\n";
   }
}

void Input()
{
	if (_kbhit())
	{
		switch (_getch())
		{
		case 'a':
			dir = LEFT;
			break;
		case 'w':
			dir = UP;
			break;
		case 'd':
			dir = RIGHT;
			break;
		case 'x':
			gameOver = true;
			break;
		}
	}
}

void Logic()
{
	
	
	
	if (GameMode == 0)
	{
		timer -= 1;
		Sleep(1);
		
	}

	

	for (int p = 0; p < 5; p++)
	{
		arrX[p] = rand() % (width - 4) + 2;
	}
		
	if (lives <= 0 || timer==0)
	{
		gameOver = true;
	}
	switch (dir)
	{
	case LEFT:
		x--;
		break;
	case UP:
		y--;
		break;
	case RIGHT:
		x++;
		break;
	}
	dir = STOP;
}  

int main()
{
	Setup();
	

	while (!gameOver && error == false)
	{
       Draw();
	   Input();
	   Draw();
	   Logic();
	   Draw();
	}

	End();
	
	

	return 0;
}
