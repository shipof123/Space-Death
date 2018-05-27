#include <ncurses.h>
#include <curses.h>
#include <unistd.h>
#include <stdlib.h>
#include <time.h>
#define OBSTACLES 400
#define DELAY 30000

struct cords
{
int x;
int y;
}obs[OBSTACLES],goal,max;
#define player2 obs[OBSTACLES-1]
int initobs()
{
  srand(time(0));
  int max_y,max_x;
  getmaxyx(stdscr, max_y, max_x);
  int c;
  int cc;
  int px=(rand()%(max_x-2))+2, py=(rand()%(max_y-2))+2;
  for(c=0;c<OBSTACLES-1;c++)
  {
    px=(rand()%(max_x-2))+2;
  py=(rand()%(max_y-2))+2;
  while(px==goal.x&&py==goal.y)
    {px=(rand()%(max_x-2))+2;
  py=(rand()%(max_y-2))+2;}
    obs[c].x=px;
	obs[c].y=py;
  }
  return 0;
}
bool win(int x,int y)
{
  if(goal.x==x&&goal.y==y)
  {
  return true;
  }
  if(goal.y==y+1&&goal.x==x)
  {
  return true;
  }
  if(goal.y==y+1&&goal.x==x+1)
  {
  return true;
  }
  if(goal.y==y+1&&goal.x==x+2)
  {
  return true;
  }
  if(goal.x==x+1&&goal.y==y)
  {
  return true;
  }
  if(goal.x==x+2&&goal.y==y)
  {
  return true;
  }
  return false;
}
bool can(int x,int y)
{
  int i;
  for(i=0;i<OBSTACLES;i++)
  {
  if(obs[i].x==x&&obs[i].y==y)
  {
  return false;
  }
  if(obs[i].y==y+1&&obs[i].x==x)
  {
  return false;
  }
  if(obs[i].y==y+1&&obs[i].x==x+1)
  {
  return false;
  }
  if(obs[i].y==y+1&&obs[i].x==x+2)
  {
  return false;
  }
  if(obs[i].x==x+1&&obs[i].y==y)
  {
  return false;
  }
  if(obs[i].x==x+2&&obs[i].y==y)
  {
  return false;
  }
  }
  return true;
}
/* AI?
int movep2()
{
    int nextx2= player2.x, nexty2 = player2.y;
    int direction2=rand()%5;
	direction2-=2;
	if(direction2==2||direction2==-2)
	{
		nexty2+=direction2/2;
	}
	else
	{
		nextx2+=direction2/2;
	}
	bool canmove2=(nextx2>-1&&nexty2 >= 0&&nextx2<(max.x-2)&&nexty2<=(max.y-1));
	if(!nextx2>-1&&nexty2 >= 0&&nextx2<(max.x-2)&&nexty2<=(max.y-1))
	{
	refresh();
		if(!canmove2)
		{
		direction2=rand()%5;
		direction2-=2;
		}
		if(!direction2%2)
		{
			nexty2+=(direction2);
		}
		else
		{
			nextx2+=direction2/2;
		}
	}
	player2.x=nextx2;
	player2.y=nexty2;
	
}
*/
int mvp2()
{
	static int cntr=0;
  	if(cntr<5)
	{
	   player2.x+=1;
	   cntr++;
	   return 0;
	}
	else if(cntr<10&&cntr>4)
	{
	   player2.y-=1;
	   cntr++;
	   return 0;
	}
	else if(cntr<15&&cntr>9)
	{
	  player2.x-=2;
	  cntr++;
	  return 0;
	}
	else if(cntr>14&&cntr<20)
	{
	  player2.y+=1;
	  cntr++;
	  return 0;
	}
   cntr=0;
}
int main(int argc, char * argv[])
{
  int x = 0, y= 0;
  int direction;
  int c =0;

  initscr();
  noecho();
  curs_set(0);
  keypad(stdscr,TRUE);  // remember, y hen x
  cbreak();
  box(stdscr,0,0);
  int nexty=0;
  int nextx=0;
  initobs(OBSTACLES);
  getmaxyx(stdscr, max.y, max.x);
  player2.x=max.x-20;
  player2.y=max.y-2;
  goal.x=max.x/1.1;
  goal.y=max.y/1.1;
  int cntr = 0;
  char xy='x';
  while(1)
  {
  clear();
  nextx =x;
  nexty =y;
  int nexty2=player2.y;
  int nextx2=player2.x;
  mvprintw(y+1,x," V");
  mvprintw(y,x,"<=>");
  mvprintw(goal.y,goal.x,"O");
  for(c=0;c<OBSTACLES;c++)
  {
    mvprintw(obs[c].y,obs[c].x,"|");
  }
  refresh();
  //movep2();
  direction=0;
  int direction2=0;
  int ch = getch();
  bool xk=false;
  switch(ch)
  {
    case KEY_LEFT:
    case 'a':
    direction = -1;
    nextx = x-1;
    xk=true;
    break;
    case 'd':
    case KEY_RIGHT:
    direction = 1;
    nextx = x + 1;
    xk=true;
    break;
    case 'w':
    case KEY_UP:
    direction = -1;
    nexty =y -1;
    break;
    case 's':
    case KEY_DOWN:
    direction = 1;
    nexty= y +1;
    break;
  }
    bool canmove=(nextx>-1&&nexty >= 0&&nextx<(max.x-2)&&nexty<=(max.y-1)&&can(nextx,nexty));
    if(win(nextx,nexty))//win returns false if you win
	{
	  clear();
	    curs_set(FALSE);
	  mvprintw(max.y/2-1,max.x/2,"YOU WIN!!!!");
	  mvprintw(max.y/2,max.x/2,"press space to play again");
	  refresh();
	  int brea = getch();
	  while(brea!=' ')
	   brea = getch();
	   x=0;
	   y=0;
	   player2.x=max.x-5;
	   player2.y=max.y+5;
	}
	if(canmove)
	{
      if(xk)
	  {
	  x+= direction;
	  }
	  else
	  {
	  y+= direction;
	  }
	}
	else if(!canmove)
	{
	clear();
	  curs_set(FALSE);
	  mvprintw(max.y/2,max.x/2,"GAME OVER!!! Press Space to Respawn");
	  refresh();
	  int brea = getch();
	  while(brea!=' ')
	   brea = getch();
	  x=0;
	  y=0;
	}
	mvp2();
	}
	endwin();
	return 0;
}
