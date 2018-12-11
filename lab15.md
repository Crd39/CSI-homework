# 代码
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <windows.h>

#define SNAKE_MAX_LENGTH 20
#define SNAKE_HEAD 'H'
#define SNAKE_BODY 'X'
#define BLANK_CELL ' '
#define SNAKE_FOOD '$'
#define WALL_CELL '*'

//snakeMove(moveX,moveY)
void snakeMove(int, int, int);
//汜傖妘昜
void putMoney(void);
//岆瘁勛善妘昜
int eatFood(int, int);
//湖荂map
void output(char map[][12]);
//岆瘁湛傖蚔牁賦旰腔沭璃
int gameover(void);
//樵隅狟祭
char whereGoNext(int, int, int, int);
char map[12][12] = {
		"************",
		"*XXXXH     *",
		"*          *",
		"*          *",
		"*          *",
		"*          *",
		"*          *",
		"*          *",
		"*          *",
		"*          *",
		"*          *",
		"************"};
int snakeX[SNAKE_MAX_LENGTH] = {1,2,3,4,5};
int snakeY[SNAKE_MAX_LENGTH] = {1,1,1,1,1};
int snakeLength = 5;
//0測桶華芞羶妘昜
int foodFlag = 0;
int foodX = 0;
int foodY = 0;

int main(){
	//湔揣黍腔偌瑩
	char movement;

	//吨瞳梓妎
	int winFlag = 0;
	//湖荂
	output(map);
	putMoney();

	while(!gameover()){
		movement = whereGoNext(snakeX[snakeLength-1],snakeY[snakeLength-1],foodX,foodY);

		switch(movement){
		case 'w':snakeMove(0,-1,eatFood(0,-1));
			output(map);
			break;
		case 'a':snakeMove(-1,0,eatFood(-1,0));
			output(map);
			break;
		case 's':snakeMove(0,1,eatFood(0,1));
			output(map);
			break;
		case 'd':snakeMove(1,0,eatFood(1,0));
			output(map);
			break;
		}

		if(foodFlag){
			if(snakeLength==20){
				winFlag = 1;
				break;
			}else{
				putMoney();
				foodFlag = 0;
			}
		}
	}
	if(winFlag){
		printf("You Win!!\n");
	}else{
		printf("Game Over!!\n");
	}

	return 0;
}

void output(char map[][12]){
	int i;
	for(i=0;i<12;i++){
		int j;
		for(j=0;j<12;j++){
			printf("%c",map[i][j]);
		}
		printf("\n");
	}
}

int gameover(){
	int flag = 0;
	int i;
    //彴芛癲善旯极麼族寀蚔牁賦旰
	for(i=0;i<snakeLength-1;i++){
		if(snakeX[snakeLength-1] == snakeX[i] && snakeY[snakeLength-1] == snakeY[i]){
			flag = 1;
		}
	}
	if(snakeX[snakeLength-1]==11 || snakeY[snakeLength-1]==11 || snakeX[snakeLength-1]==0 || snakeY[snakeLength-1]==0){
		flag = 1;
	}
	if(flag){
		return 1;
	}else{
		return 0;
	}
}

void snakeMove(int x, int y, int eat){
	//載蜊彴旯迵彴芛腔醴梓
	if(!eat){
		map[snakeY[0]][snakeX[0]] = BLANK_CELL;
		int i;
		for(i=0;i<snakeLength-1;i++){
			snakeX[i] = snakeX[i+1];
			snakeY[i] = snakeY[i+1];
		}
		snakeX[snakeLength-1] += x;
		snakeY[snakeLength-1] += y;
		map[snakeY[snakeLength-2]][snakeX[snakeLength-2]] = SNAKE_BODY;
		map[snakeY[snakeLength-1]][snakeX[snakeLength-1]] = SNAKE_HEAD;
	}else{
		foodFlag = 1;
		snakeX[snakeLength] = snakeX[snakeLength-1] + x;
		snakeY[snakeLength] = snakeY[snakeLength-1] + y;
		map[snakeY[snakeLength-1]][snakeX[snakeLength-1]] = SNAKE_BODY;
		map[snakeY[snakeLength]][snakeX[snakeLength]] = SNAKE_HEAD;
		snakeLength++;
	}
}

int eatFood(int x, int y){
	if(snakeX[snakeLength-1]+x == foodX && snakeY[snakeLength-1]+y == foodY){
		return 1;
	}else{
		return 0;
	}
}

void putMoney(void){
	srand(time(NULL));
	foodX = 1+((int)rand())%10;
	foodY = 1+((int)rand())%10;
	int flag = 0;
	int i;
	for(i=0;i<snakeLength;i++){
		if(snakeX[i] == foodX && snakeY[i] == foodY){
			flag = 1;
		}
	}
	if(flag == 0){
		map[foodY][foodX] = SNAKE_FOOD;
	}else{
		putMoney();
	}
}

char whereGoNext(int x, int y, int fx, int fy){
	Sleep(100);
	char movable[4] = {'w','a','s','d'};
	int distance[4] ={0,0,0,0};

	distance[0] = abs(fx-x) + abs(fy-(y-1));
	if(map[y-1][x]!=BLANK_CELL && map[y-1][x]!=SNAKE_FOOD){
		distance[0] = 9999;
	}
	distance[1] = abs(fx-(x-1)) + abs(fy-y);
	if(map[y][x-1]!=BLANK_CELL && map[y][x-1]!=SNAKE_FOOD){
		distance[1] = 9999;
	}
	distance[2] = abs(fx-x) + abs(fy-(y+1));
	if(map[y+1][x]!=BLANK_CELL && map[y+1][x]!=SNAKE_FOOD){
		distance[2] = 9999;
	}
	distance[3] = abs(fx-(x+1)) + abs(fy-y);
	if(map[y][x+1]!=BLANK_CELL && map[y][x+1]!=SNAKE_FOOD){
		distance[3] = 9999;
	}

	int temp = distance[0];
	int target = 0;
	int i;

	for(i=1;i<4;i++){
		if(temp>distance[i]){
			temp = distance[i];
			target = i;
		}
	}
	return movable[target];
}

```

# 学习
这次智能蛇对我来说最大的问题就是linux的使用以及时不时陷入死循环的程序。
但最后都成功解决。