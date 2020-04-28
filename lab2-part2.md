# ELE 115 – Lab 2

**Read the documentation for [Lab 2](https://github.com/ELE115/docs/blob/master/lab2.md)**

## **Part 2 - Exploring a regular 2-D polygon with 3, 4, 5, or 6 sides based on operator's Input**

Now when you can fly a regular 2-D triangle, let&#39;s make a program interactive and let a drone operator to choose which polygon to fly!

This time before taking off you should ask an operator which regular polygon he/she wants to explore. The operator needs to enter the number of sides before a drone takes off, check that provided input is a valid number, and after that fly a specified polygon. We assume that valid polygons are triangle, square, pentagon, and hexagon.  Therefore, number of sides can be either 3, 4, 5, or 6. In the case if the input is not valid, the program must print an error message and exit.

1. Accept assignment by clicking on lab2-part2 invitation link on Canvas
2. Create a new project and configure files _build.gradle_ and _settings.gradle_ using your **netid** and `lab2-part2`/`lab2_part2` name for your project (see steps 2-4 on [https://github.com/ELE115/idea-gradle-template/blob/master/README.md](https://github.com/ELE115/idea-gradle-template/blob/master/README.md))
2. Create a new Java class (see [https://github.com/ELE115/idea-gradle-template/blob/master/README.md#6-start-programming-and-have-fun](https://github.com/ELE115/idea-gradle-template/blob/master/README.md#6-start-programming-and-have-fun)) with the next name: `com.github.ele115.<netid>.lab2_part2.Main`, replacing `<netid>` by your university netid. E.g. if your netid is `alavrov`, use `com.github.ele115.alavrov.lab2_part2.Main` for the class name.
4. Add the next code before your Main class to import libraries required to control the drone:

```java
import com.github.ele115.tello_wrapper.ITelloDrone;
import com.github.ele115.tello_wrapper.Tello;
```

5. Complete a main method of your class which will first ask an operator to provide number of sides for a polygon and checks its correctness (see the description above). If the input is valid, make the drone to fly a 2-D regular polygon with a side of 100 cm after taking off and landing after finishing exploring a polygon.

6. Show your code to a TA and submit this part to **github**

In addition to drone control commands from Part I, you should use conditional statements: *if/if-else/switch*. In this part you are not required to use loop statements.

**The drone must land around the same point where it took off and it must face the same direction as before taking off!**

**Your program must exit after the drone lands!**
