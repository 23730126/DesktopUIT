#include <iostream>
#include <windows.h>
#include <stdlib.h>
#include <conio.h>
using namespace std;

void gotoxy(short a, short b) //Custom gotoxy() function
{
    COORD coordinates; //Data type of co-ordinates
    coordinates.X = a; //Assign value to X- Co-ordinate
    coordinates.Y = b; //Assign value to Y Co-ordinate

SetConsoleCursorPosition(
        GetStdHandle(STD_OUTPUT_HANDLE), coordinates);

}

struct TPOINT{
    int x,y;
};
class SNAKE{
private:
    int Leng;
    TPOINT Body[100];
public:
    SNAKE(){
        Leng = 7;
        Body[0].x = 8; Body[0].y = 6;
        Body[1].x = 7; Body[1].y = 6;
        Body[2].x = 6; Body[2].y = 6;
        Body[3].x = 6; Body[3].y = 5;
        Body[4].x = 6; Body[4].y = 4;
        Body[5].x = 5; Body[5].y = 4;
        Body[6].x = 4; Body[6].y = 4;
    }
    void Draw(){
        for (int i = 0 ; i< Leng;i++){
            gotoxy(Body[i].x*2, Body[i].y);
            cout<<"XX";
        }
    }

    // Direction = 0 (right),1(down),2(left),3(up)
    void Go(int Direction){
        for (int i =  Leng; i>0 ;i--)
            Body[i] = Body[i-1];
        if (Direction == 0)         Body[0].x = Body[0].x + 1;
        else if (Direction == 1)    Body[0].y = Body[0].y + 1;
        else if (Direction == 2)    Body[0].x = Body[0].x - 1;
        else if (Direction == 3)    Body[0].y = Body[0].y - 1;
    }

};

int main(){
    SNAKE s;
    char tl;
    int Di = 0;
    while (1){
        if (kbhit()){
            tl = getch();
            if (tl == 'a') Di = 2;
            else if (tl == 'w') Di = 3;
            else if (tl == 'd') Di = 0;
            else if (tl == 'z') Di = 1;
            else if (tl == 'p') break;
        }
        s.Go(Di);
        s.Draw();
        Sleep(500);
        system("cls");
    }

    return 0;
}
