#第二个html游戏博客
##游戏策划
Setting: 角色为一个贪婪的勇者，在夺取宝物之后想离开险恶之地。<br />
但在离开的陆上，他遇到了一个墙上布满陷阱的迷宫，一碰就死。<br />
<br />
Gameplay:结合电流急急棒与迷宫的玩法，方向键控制角色，若触碰迷宫墙壁则死亡。<br />

ps. 勇者的hitbox只有一个小点，迷宫的hitbox是可视的黑线。

##游戏设计
Object: 勇者<br />
Attribute:![](images/hero.jpg),位于玩家入口处 <br />
Collaborator：迷宫 <br/>
Events & Actions: 按住方向键控制 & 碰到迷宫销毁自己<br />

Object: 迷宫<br />
Attribute:![](images/maze.jpg),位于底图层<br />
Collaborator：勇者 <br />
Events & Actions: 与勇者接触时销毁勇者<br />
 

成品gif
![img](images/game2.gif)