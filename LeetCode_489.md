# 489. Robot Room Cleaner

Problem link: [489. Robot Room Cleaner](https://leetcode.com/problems/robot-room-cleaner/description/)

* Level: [Hard](https://leetcode.com/problemset/all/?difficulty=Hard)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

The robot is "blind" - it can't get the whole graph and it can only move to its neighbour squares. Thus, this graph problem can only solved by DFS and we have to archive the robot's evey step. 

## Implementation

### C++ (beats 72.70%)
```C++
/**
 * // This is the robot's control interface.
 * // You should not implement it, or speculate about its implementation
 * class Robot {
 *   public:
 *     // Returns true if the cell in front is open and robot moves into the cell.
 *     // Returns false if the cell in front is blocked and robot stays in the current cell.
 *     bool move();
 *
 *     // Robot will stay in the same cell after calling turnLeft/turnRight.
 *     // Each turn will be 90 degrees.
 *     void turnLeft();
 *     void turnRight();
 *
 *     // Clean the current cell.
 *     void clean();
 * };
 */
class Solution {
private:
    
    char st = 'u';
    pair<int, int> cur = {0, 0};
    set<pair<int, int>> mem;
    stack<char> dfs;
    
    void faceUP(Robot& robot) {
       switch(st) {
            case 'l':
                robot.turnRight();
                break;
            case 'r':
                robot.turnLeft();
                break;
            case 'u':
                break;
            case 'd':
                robot.turnLeft();
                robot.turnLeft();
                break;
        }
        st = 'u';
        return; 
    }
    
    void faceDown(Robot& robot) {
        switch(st) {
            case 'l':
                robot.turnLeft();
                break;
            case 'r':
                robot.turnRight();
                break;
            case 'u':
                robot.turnRight();
                robot.turnRight();
                break;
            case 'd':
                break;
        }
        st = 'd';
        return;
    }
    
    void faceLeft(Robot& robot) {
        switch(st) {
            case 'l':
                break;
            case 'r':
                robot.turnLeft();
                robot.turnLeft();
                break;
            case 'u':
                robot.turnLeft();
                break;
            case 'd':
                robot.turnRight();
                break;
        }
        st = 'l';
        return;
    }
    
    void faceRight(Robot& robot) {
        switch(st) {
            case 'l':
                robot.turnRight();
                robot.turnRight();
                break;
            case 'r':
                break;
            case 'u':
                robot.turnRight();
                break;
            case 'd':
                robot.turnLeft();
                break;
        }
        st = 'r';
        return;
    }
    
    bool moveUP(Robot& robot) {
        faceUP(robot);
        if(robot.move()) {
            --cur.first;
            return true;
        }
        return false;
    }
    
    bool moveDown(Robot& robot) {
        faceDown(robot);
        if(robot.move()) {
            ++cur.first;
            return true;
        }
        return false;
    }
    
    bool moveLeft(Robot& robot) {
        faceLeft(robot);
        if(robot.move()) {
            --cur.second;
            return true;
        }
        return false;
    }
    
    bool moveRight(Robot& robot) {
        faceRight(robot);
        if(robot.move()) {
            ++cur.second;
            return true;
        }
        return false;
    }
    
    void archive(Robot& robot, char dir) {
        robot.clean();
        dfs.push(dir);
        mem.insert(cur);
    }
    
    bool checkUP() {
        return mem.count({cur.first - 1, cur.second}) == 1;
    }
    
    bool checkDown() {
        return mem.count({cur.first + 1, cur.second}) == 1;
    }
    
    bool checkLeft() {
        return mem.count({cur.first, cur.second - 1}) == 1;
    }
    
    bool checkRight() {
        return mem.count({cur.first, cur.second + 1}) == 1;
    }
    
public:
    void cleanRoom(Robot& robot) {
        archive(robot, 0);
        while(true) {
            if(!checkUP() && moveUP(robot)) {
                archive(robot, 'd'); continue;
            }
            if(!checkDown() && moveDown(robot)) {
                archive(robot, 'u'); continue;
            }
            if(!checkLeft() && moveLeft(robot)) {
                archive(robot, 'r'); continue;
            }
            if(!checkRight() && moveRight(robot)) {
                archive(robot, 'l'); continue;
            }
            char ret = dfs.top(); dfs.pop(); if(dfs.empty()) break;
            switch(ret) {
                case 'u': moveUP(robot); break;
                case 'd': moveDown(robot); break;
                case 'l': moveLeft(robot); break;
                case 'r': moveRight(robot); break;
            }
        }        
    }
};
```