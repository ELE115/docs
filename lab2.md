# ELE 115 – Lab #2

# Exploring an ELEDrone Planet


# Requirements

- Installed and configured tools: _Git_, _OpenJDK_, and _IntelliJ IDEA_
- Personal drone
- Understanding material from week 1/week 2

# Objectives

- Learning to use conditional statements: `if`/`else`
- Getting input from a user `Scanner`
- Using loop statements to do repetitive tasks `for`/`while`

# Description

In this lab you will use your knowledge of programming to control a drone and make it to fly a regular 2-D polygons. In three parts you will be exploring a new planet – **ELEDrone** - by navigating the drone, and you want to hover at every vertex of a polygon.

First, let's review regular polygons to make it easier to complete the task. In a regular polygon all sides have equal length and all angles are equal as well. We will consider only **convex polygons**, and therefore they will be a triangle, square, pentagon, etc.


**You must fly along every side of a polygon starting in any vertex. When you reach the next vertex, you must make an appropriate turn and continue flying along the next side.
The drone must land around the same point where it took off. More than that, its orientation must same as before taking off (it must face the same direction), so it is ready for the next mission.**

# Reading user input in a program
A drone can be completely autonomous and fly along a specified route. However, sometimes it might require a human help, for example, when a drone operator navigates the drone to avoid obstacles. In this case, the program should ask an operator for a new command after each completed step. Below we show how you can get two integer numbers in your program from a user and return their sum. 

**Note: Do not worry if some terms below are unfamiliar to you, they will be covered later in the class and you can come back to this example to understand all the details. Just focus on the high-level idea for now**.

To get user input, we will be using a `Scanner` class, which can be found in `java.util` package. Therefore, the first thing we have to do is to import it to our program in the same way as we do it for `Tello` package:

```java
import java.util.Scanner;
```

Next, we need to create a new object of a `Scanner` class which will get input from a standard input stream - `System.in` (compare it to a standard output stream `System.out` which we use for printing messages)

```java
Scanner keyboard = new Scanner(System.in);
```

After executing this line, we will have an object with a name `keyboard` (you can choose any name you want, just think about it as a variable) which will read characters from a standard input stream. Now we can use available methods for a Scanner object to get user input. For example, if we want to read an integer from a user, we use `nextInt()` method:

```java
int my_int = keyboard.nextInt();
```
When executing this statement, your program will try to read several characters until it encounters a space symbol and convert them to an integer. E.g. if you enter '1234' as a user input `my_int` will be equal to 1234.

`Scanner` class has more methods to read a string, byte, line, boolean (`next()`, `nextbyte()`, `nextLine()`, `nextBoolean()` respectively) to a list a few. You can find more of them in the Java documentation online.

Below is a simple program which asks a user to enter two number and returns their sum. Try to run it, experiment with different inputs (what happens if you enter a letter instead of a number?) and make sure you understand how it works. If you have any questions, ask a TA!

```java
import java.util.Scanner;

public class AddTwoNumbers
{
    public static void main(String[] args)
    {
        Scanner keyboard = new Scanner(System.in);
        int num1, num2, sum;

        System.out.println("I can add any numbers! Try it out!");
        
        System.out.print("Give me the first number: ");
        num1 = keyboard.nextInt();
        
        System.out.print("Give me the second number: ");
        num2 = keyboard.nextInt();

        sum = num1 + num2;
        System.out.println("Look! The sum is " + sum);
    }
}
```
