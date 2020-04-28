# ELE 115 – Lab 2

**Read the documentation for [Lab 2](https://github.com/ELE115/docs/blob/master/lab2.md)**

## **Part 3 - Exploring regular 2-D polygons until user issues a land command**

For now, we have been exploring only one polygon after taking off and returning to a base. Now let's write a program where we an operator can explore multiple polygons after taking off. When the drone finishes flying one polygon, a program must ask if the operator wants to continue and explore a new polygon or land. In this part the valid number of sides will be between 3 and 12, and 0 will be used to indicate the end of a mission.

1. Accept assignment by clicking on lab2-part3 invitation link on Canvas
2. Create a new project and configure files _build.gradle_ and _settings.gradle_ using your **netid** and `lab2-part3`/`lab2_part3` name for your project (see steps 2-4 on [https://github.com/ELE115/idea-gradle-template/blob/master/README.md](https://github.com/ELE115/idea-gradle-template/blob/master/README.md))
2. Create a new Java class (see [https://github.com/ELE115/idea-gradle-template/blob/master/README.md#6-start-programming-and-have-fun](https://github.com/ELE115/idea-gradle-template/blob/master/README.md#6-start-programming-and-have-fun)) with the next name: `com.github.ele115.<netid>.lab2_part3.Main`, replacing `<netid>` by your university netid. E.g. if your netid is `alavrov`, use `com.github.ele115.alavrov.lab2_part3.Main` for the class name.
4. Add the next code before your Main class to import libraries required to control the drone:

```java
import com.github.ele115.tello_wrapper.ITelloDrone;
import com.github.ele115.tello_wrapper.Tello;
```


5. Complete a main method of your class which will first ask an operator to provide number of sides for a polygon and checks its correctness (see the description above). If the input is valid, make the drone to fly a 2-D regular polygon with a side of 100 cm after taking off. When the drone returns to the base, ask the operator once again which polygon it wants the drone to fly, check correctness of an operator&#39;s input and make a drone to explore a polygon. The program must run until the operator enters 0 for the number of sides.
6. Show your code to a TA and submit this part to **github**


In addition to drone control commands from the previous two parts, you must use loop statements: *for/while*.

**The drone must land around the same point where it took off and it must face the same direction as before taking off!**

**Your program must exit after the drone lands!**
