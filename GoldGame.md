
```


package Test1;
import java.util.*;
 
public class GoldGame {
    public static void main(String[] args) {
        Game obj = new Game();
        do {
            obj.init();
            obj.print();
            obj.move();
        }while(obj.c!='o' && !obj.getGold(obj.mnstr) && !obj.getGold(obj.user) && !obj.attackMonster());
        obj.endprint();
    }
}
 
abstract class Sprite {
    int x=3; int y=3;
    int oldx, oldy;
    void previous() {
        oldx = x;
        oldy = y;
    }
    abstract void move(char c);
}
 
class Main extends Sprite { 
    void move(char c) {
        previous();
        if(c=='w') --x;
        else if(c=='a') --y;
        else if(c=='d') ++y;
        else if(c=='s') ++x;
        Game.invalidMove(this);
    }
}
 
class Monster extends Sprite {
    public Monster() {
        x = y = (int)Math.random()*8+1;
    }
    void move(char c) {
        previous();
        double d = Math.random();
        x += (d-0.25)>0? 1: -1;
        y +=(d-0.75)>0? 1:-1;
        Game.invalidMove(this);
    }
}
 
class Game {
    Scanner sc = new Scanner(System.in);
    static char[][] board = new char[10][19]; 
    char c;
    Main user = new Main();
    Monster mnstr = new Monster();
    static int gx,gy;
    
    Game() {
        for(int i =0;i<10;i++) {
            for(int j = 0; j<19;j++) {
                if(i==0||i==9)     board[i][j] = '#';
                else {
                    if(j==0||j==18) board[i][j] = '#';
                    else board[i][j] = ' ';
                }
            }
        }
        gold();
    }
    
    void print() {
        for(int i =0;i<10;i++) {
            for(int j = 0; j<19;j++) {
                System.out.print(board[i][j]);
            }
            System.out.println("");
        }
        System.out.print("left(a), right(d), up(w), down(s), QUIT(o): ");
        c = sc.next().charAt(0);
    }
 
    void gold() {
        gx = (int)(Math.random()*8+1);
        gy = (int)(Math.random()*17+1);
        board[gx][gy] = 'G';
    }
 
    void init() {
        board[user.x][user.y] = 'U';
        board[mnstr.x][mnstr.y] = 'M';
    }
 
    void move() {
        user.move(c);
        board[user.oldx][user.oldy] = ' ';
        mnstr.move(c);
        board[mnstr.oldx][mnstr.oldy] = ' ';
    }
 
    boolean getGold(Sprite s) {
        boolean get = false;
        if(s.x == gx && s.y == gy) get= true;
        return get;
    }
 
    boolean attackMonster() {
        boolean attack = false;
        if(user.x==mnstr.x && user.y==mnstr.y) attack = true;
        board[mnstr.x][mnstr.y] = 'M';
        return attack;
    }
 
    static void invalidMove(Sprite sprite) {
        if(sprite.x>8 || sprite.x<1) {
            sprite.x = sprite.oldx;
        }
        if(sprite.y>17 || sprite.y<1) {
            sprite.y = sprite.oldy;
        }
        if(sprite instanceof Main) System.out.println("you can't go there");
    }
 
    void endprint() {
        System.out.println("\n!!!!!!!!!!!!!!!!!!!");
        for(int i =0;i<10;i++) {
            for(int j = 0; j<19;j++) {
                System.out.print(board[i][j]);
            }
            System.out.println("");
        }
        System.out.println("!!!!!!!!!!!!!!!!!!!");
        System.out.println("Game ended");
        if(getGold(user)) System.out.println("you got the GOLD!");
        if(getGold(mnstr)) System.out.println("monster got the GOLD!");
        if(attackMonster()) System.out.println("monster ATTACKED you!");
    }
}
```
