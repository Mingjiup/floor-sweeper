# floor-sweeper
import java.util.Random;

public class FloorSweeper {
    private int[][] floor;
    private int x;
    private int y;
    
    //basic map
    public FloorSweeper(int size) {
        floor = new int[size][size];
        Random rand = new Random();
        x = rand.nextInt(size);
        y = rand.nextInt(size);
    }
    //determine where the dirt is
    public void sweep() {
        while (true) {
            if (floor[x][y] == 1) {
                System.out.println("Cleaning dirt at (" + x + ", " + y + ")");
                floor[x][y] = 0;
            }

            if (move()) {
                System.out.println("Moved to (" + x + ", " + y + ")");
            } else {
                System.out.println("Stuck at (" + x + ", " + y + ")");
                break;
            }
        }
    }

    private boolean move() {
        Random rand = new Random();
        int direction = rand.nextInt(4); // 0: up, 1: right, 2: down, 3: left

        switch (direction) {
            case 0:
                if (x > 0) {
                    x--;
                    return true;
                }
                break;
            case 1:
                if (y < floor.length - 1) {
                    y++;
                    return true;
                }
                break;
            case 2:
                if (x < floor.length - 1) {
                    x++;
                    return true;
                }
                break;
            case 3:
                if (y > 0) {
                    y--;
                    return true;
                }
                break;
        }

        return false;
    }

    public void addDirt(int x, int y) {
        floor[x][y] = 1;
    }

    public static void main(String[] args) {
        FloorSweeper sweeper = new FloorSweeper(10);
        sweeper.addDirt(3, 4);
        sweeper.addDirt(5, 7);
        sweeper.addDirt(8, 1);
        sweeper.sweep();
    }
}
