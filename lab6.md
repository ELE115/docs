# Background

## Learning objectives

* Learn how to write classes
* Learn how to use classes

## Story

To write a program that controls one single drone is not hard.
Some day, you will be the boss controlling 100 drones with a single line of code.
Yet the road towards being a boss like that is hard.
We can make it easier by letting you play with multiple fake drones before you get to actual drones.

# Part 0: Fake Drone

(Name your project `lab6-fake-drone`)

You need **three** Java files: `Main.java`, `FakeDrone.java`, and `FakeDroneSwarm.java`.
Let's discuss them in detail.

## `Main.java`

We wrote this file for you!
Just copy and paste it into your `Main.java`.
**Keep your `package` line untouched, of course!**

```java
package ...

public class Main
{
    public static void main(String[] args)
    {
        int n = Integer.parseInt(args[0]);
        FakeDroneSwarm swarm = new FakeDroneSwarm(n);
        System.out.println(swarm); // Don't forget this line
        swarm.takeoff();
        System.out.println(swarm);
        swarm.forward(100);
        System.out.println(swarm);
        swarm.turnLeft(120);
        System.out.println(swarm);
        swarm.forward(100);
        System.out.println(swarm);
        swarm.turnLeft(120);
        System.out.println(swarm);
        swarm.forward(100);
        System.out.println(swarm);
        swarm.turnLeft(120);
        System.out.println(swarm);
        swarm.land();
        System.out.println(swarm);
        System.exit(0);
    }
}
```

## `FakeDrone.java`

**Please follow the guide carefully.**

1. To create this file, right click of your `Main.java` file. Click `New`/`Java Class`.
1. Type `FakeDrone` as the name.
1. Hit enter.
1. Now you should see a file with an empty class `public class FakeDrone { }`.
1. Inside the class braces, you need to create the following:
    * Some class member variables to store the **name** (`String`) and **flight status** of the drone. (What's flight status? You will learn about it soon.)
    _Q: Should these members be `public` or `private`?_
    * A constructor that takes **name** (`String`) and **initial position** (`double x`, `double y`).
    _Q: What should you write inside the contructor?_
    * A method `public String toString() { ... }`. This method shall return a `String` saying which drone `this` is and where `this` is.
    _Q: Should you call `System.out.println` here?_
    * A method `public void takeoff() { ... }`. This method shall modify the flight status.
    If the drone has already taken off, don't do anything.
    * A method `public void land() { ... }`. This method shall modify the flight status.
    If the drone has not yet taken off, don't do anything.
    * A method `public void turnLeft(double deg) { ... }`. This method shall modify the flight status.
    If the drone has not yet taken off, don't modify the flight status **and print error message to `System.err`.
    * A method `public void turnRight(double deg) { ... }`. This method shall modify the flight status.
    If the drone has not yet taken off, don't modify the flight status **and print error message to `System.err`.
    * A method `public void forward(double cm) { ... }`. This method shall modify the flight status.
    If the drone has not yet taken off, don't modify the flight status **and print error message to `System.err`.
    * A method `public void backward(double cm) { ... }`. This method shall modify the flight status.
    If the drone has not yet taken off, don't modify the flight status **and print error message to `System.err`.

So what is **flight status**?

* Has the drone taken off or not?
* Where is (i.e., the coordinates of) the drone? (**Note:** You don't need to track the Z-axis position because we don't implement `up` and `down`!)
* Which direction is the drone facing?

## `FakeDroneSwarm.java`

**Please follow the guide carefully.**

1. To create this file, right click of your `Main.java` file. Click `New`/`Java Class`.
1. Type `FakeDroneSwarm` as name.
1. Hit enter.
1. Now you should see a file with an empty class `public class FakeDroneSwarm { }`.
1. Inside the class braces, you need to create the following:
    * An array to store `FakeDrone`s.
    _Q: Should you initialize the array (like `... = new FakeDrone[...];`) right there? If yes, how large the array should it be? If not, where else should you initialize it?_
    * A constructor that takes **number of fake drones** (`int`).
    The (fake) drones should be named with the naming pattern, `Drone #0`, `Drone #1`, `Drone #2`, ... .
    The (fake) drones should be (virtually) placed at `(0, 0)`, `(100, 0)`, `(200, 0)`, ... .
    _Q: What should you write inside the contructor?_
    * A method `public String toString() { ... }`. This method shall return a `String` summarizing the information of _all_ of the fake drones.
    _Q: Should you call `System.out.println` here?_
    * A method `public void takeoff() { ... }`. This method shall command _every_ fake drone to take off.
    * A method `public void land() { ... }`. This method shall command _every_ fake drone to land.
    * A method `public void turnLeft(double deg) { ... }`. This method shall command _every_ fake drone to turn.
    * A method `public void turnRight(double deg) { ... }`. This method shall command _every_ fake drone to turn.
    * A method `public void forward(double cm) { ... }`. This method shall move _every_ fake drone forward.
    * A method `public void backward(double cm) { ... }`. This method shall move _every_ fake drone backward.

# Testing

When you've finished coding, click the blue button and set the Arguments to `3`.
If everything is correct, you should see something similar to:

```
Drone #0 0.0 0.0 90.0 landed
Drone #1 100.0 0.0 90.0 landed
Drone #2 200.0 0.0 90.0 landed

Drone #0 0.0 0.0 90.0 flying
Drone #1 100.0 0.0 90.0 flying
Drone #2 200.0 0.0 90.0 flying

Drone #0 6.123233995736766E-15 100.0 90.0 flying
Drone #1 100.0 100.0 90.0 flying
Drone #2 200.0 100.0 90.0 flying

Drone #0 6.123233995736766E-15 100.0 210.0 flying
Drone #1 100.0 100.0 210.0 flying
Drone #2 200.0 100.0 210.0 flying

Drone #0 -86.60254037844386 49.999999999999986 210.0 flying
Drone #1 13.397459621556138 49.999999999999986 210.0 flying
Drone #2 113.39745962155614 49.999999999999986 210.0 flying

Drone #0 -86.60254037844386 49.999999999999986 330.0 flying
Drone #1 13.397459621556138 49.999999999999986 330.0 flying
Drone #2 113.39745962155614 49.999999999999986 330.0 flying

Drone #0 -2.8421709430404007E-14 -5.6843418860808015E-14 330.0 flying
Drone #1 99.99999999999997 -5.6843418860808015E-14 330.0 flying
Drone #2 199.99999999999997 -5.6843418860808015E-14 330.0 flying

Drone #0 -2.8421709430404007E-14 -5.6843418860808015E-14 450.0 flying
Drone #1 99.99999999999997 -5.6843418860808015E-14 450.0 flying
Drone #2 199.99999999999997 -5.6843418860808015E-14 450.0 flying

Drone #0 -2.8421709430404007E-14 -5.6843418860808015E-14 450.0 landed
Drone #1 99.99999999999997 -5.6843418860808015E-14 450.0 landed
Drone #2 199.99999999999997 -5.6843418860808015E-14 450.0 landed

```

