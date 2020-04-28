# ELE 115 – Lab 2

**Read the documentation for [Lab 2](https://github.com/ELE115/docs/blob/master/lab2.md)**

## **Part 1  - Exploring every vertex of a regular 2-D triangle**

Let's start with a simple mission – exploring every vertex of a regular triangle!

Your task is to write a program which instructs a drone to fly a regular 2-D triangle in the air after a takeoff.

1. Accept assignment by clicking on lab2-part1 invitation link on Canvas
2. Create a new project and configure files _build.gradle_ and _settings.gradle_ using your **netid** and `lab2-part1`/`lab2_part1` name for your project (see steps 2-4 on [https://github.com/ELE115/idea-gradle-template/blob/master/README.md](https://github.com/ELE115/idea-gradle-template/blob/master/README.md))
2. Create a new Java class (see [https://github.com/ELE115/idea-gradle-template/blob/master/README.md#6-start-programming-and-have-fun](https://github.com/ELE115/idea-gradle-template/blob/master/README.md#6-start-programming-and-have-fun)) with the next name: `com.github.ele115.<netid>.lab2_part1.Main`, replacing `<netid>` by your university netid. E.g. if your netid is `alavrov`, use `com.github.ele115.alavrov.lab2_part1.Main` for the class name.
3. Add the next code before your Main class to import libraries required to control the drone:

```java
import com.github.ele115.tello_wrapper.ITelloDrone;
import com.github.ele115.tello_wrapper.Tello;
```

4. Complete a main method of your class which will make the drone to fly a 2-D triangle with a side of 100 cm after it takes off. You can use any of the next drone methods to move the drone (see [Drone Methods Cheat Sheet](https://github.com/ELE115/docs/blob/master/Drone_Methods_Cheat_Sheet.md) for more commands and description):

    *takeoff(), forward(int c), backward(int c), turnLeft(int d), turnRight(int d), land()*
5. Show your code to a TA and submit this part to **github**


**The drone must land around the same point where it took off and it must face the same direction as before taking off!**

**Your program must exit after the drone lands!**
