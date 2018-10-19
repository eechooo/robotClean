# robotClean

robot Clean 是google经典的面试题 leetcode 489. Robot Room Cleaner

大概的题意就是给你一个给你robot的对象，对象里面有方法turnLeft, trunRight, clean() 和 move()， turnLeft 和 turnRight 每次只能转变robot的方向九十度，但是robot是移动不了的
每次移动的操作 只能是由move()函数来完成

这道题有2个值得注意的地方

1. backtracking 在回溯的时候状态必须回到原始的状态，比如robot向下走的时候，走不动了，必须来个180度的大转弯， trunleft, trunleft, 然后向后退一步，继续保持原来的向下的状态（由向上转为向下，trunleft， trunleft）

that is why we have
```
                        robot.turnLeft();
                        robot.turnLeft();
                        robot.move()
                        robot.turnLeft();
                        robot.turnLeft();
```

2. 注意dir的写法，刚开始的的时候robot是face up，只能trunRight或者trunLeft, 所以第0个方向必须是[-1, 0],不能是[0, 1],如果是[0, 1]的话就会导致走错，而且每次进入dfs的过程当中方向都是不变的，k% 4

```python
# """
# This is the robot's control interface.
# You should not implement it, or speculate about its implementation
# """
#class Robot(object):
#    def move(self):
#        """
#        Returns true if the cell in front is open and robot moves into the cell.
#        Returns false if the cell in front is blocked and robot stays in the current cell.
#        :rtype bool
#        """
#
#    def turnLeft(self):
#        """
#        Robot will stay in the same cell after calling turnLeft/turnRight.
#        Each turn will be 90 degrees.
#        :rtype void
#        """
#
#    def turnRight(self):
#        """
#        Robot will stay in the same cell after calling turnLeft/turnRight.
#        Each turn will be 90 degrees.
#        :rtype void
#        """
#
#    def clean(self):
#        """
#        Clean the current cell.
#        :rtype void
#        """

class Solution(object):
    def cleanRoom(self, robot):
        """
        :type robot: Robot
        :rtype: None
        """
        
        dirs = [[-1, 0], [0, 1], [1, 0], [0, -1]]
        
        def dfs(i, j, d, visited, robot):
            path = str(i) + "|" + str(j)
            print visited
            if path not in visited:
                visited.add(path)
                robot.clean()
                for k in range(d, d + 4):
                    if robot.move():
                        dfs(i + dirs[k % 4][0], j + dirs[k % 4][1], k % 4, visited, robot)
                        robot.turnLeft();
                        robot.turnLeft();
                        robot.move()
                        robot.turnLeft();
                        robot.turnLeft();
                    robot.turnLeft()

        dfs(0, 0, 0, set(), robot);
                        
                
                
        
            
        
        
        
        
        
        
        
        
        


```





