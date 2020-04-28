# Background

## Learning objectives

* Learn how to write functions
* Learn how to use functions
* Learn that functions can be called from multiple different locations in your program
* Learn that the results of one function can pass into another
* Fly drone across a set of locations in the room

## Story

To demolish the outbreak of a new virus in F111, we need you to help us using your drone.
We have equipped your drone with our newest high-energy anti-virus weapon, waiting for the `FIRE` command.
Your mission is to hover your drone over the infectious spots (green crosses) and fire your anti-virus weapon by issuing the `FIRE` command to your program output.
You must take off and land your drone in non-infectious areas (blue crosses).

# Part I: Coordinate systems

To simplify your mission, we start by creating some simple building blocks - functions.

In this part, you need to write these 6 functions:

* `ftToM`: takes one input - number of feet (type `double`) - convert it to meter.
* `mToFt`: takes one input - number of meters (type `double`) - convert it to feet.
* `polarToCartesianX`: takes two input - `radius` and `angle` (both type `double`) - return x value in cartesian coordinate of the corresponding point
* `polarToCartesianY`: takes two input - `radius` and `angle` (both type `double`) - return y value in cartesian coordinate of the corresponding point
* `cartesianToPolarRadius`: takes two input - `x` and `y` (both type `double`) - return radius value in polar coordinate of the corresponding point
* `cartesianToPolarAngle`: takes two input - `x` and `y` (both type `double`) - return angle value (-180 to 180) in polar coordinate of the corresponding point

**Note: This is an engineering course - we use degrees for angles, not radians.**
Specifically, **0 degree is positive x**, 90 degree is positive y, 180 degree is negative x, 270 degree is negative y.
Also, -90 degree is negative y.

**Note:** In **NO** case should the functions output `NaN`.
Your drone will crash if you tell it to fly `NaN` centimeters!

**Hint:** You may want `Math.atan2(...)` and `Math.PI`. Note that `Math.atan2(...)` uses radians between `-Math.PI` and `Math.PI`.
Google is your friend.

To make sure that your mission does NOT fail due to careless mistakes in its building blocks,
you need to verify the correctness of your functions.

Write in your `main` function some program that displays the following report:
```
ftToM feet=2.0 return=...
ftToM feet=-4.6 return=...
mToFt meters=6.7 return=...
mToFt meters=-3.2 return=...
polarToCartesianX radius=5.0 angle=45.0 return=...
polarToCartesianX radius=5.0 angle=-100.0 return=...
polarToCartesianY radius=5.0 angle=45.0 return=...
polarToCartesianY radius=5.0 angle=-100.0 return=...
cartesianToPolarRadius x=0.0 y=0.0 return=...
cartesianToPolarRadius x=5.0 y=3.0 return=...
cartesianToPolarAngle x=-5.0 y=0.0 return=...
cartesianToPolarAngle x=0.0 y=-5.0 return=...
```

Show your code and the report to TAs.
Commit and push.

# Part II: Anti-virus challenge

In this part, you need to write a program that takes user input and flies your drone to the specified location.
Specifically, it shall do the following:

1. Take off your drone
1. Have the drone fly up another 50cm after the take off height.
1. Read from user input, and decide what to do:
    1. `l`: land **at the same spot facing the same direction as you took off** and exit your program.
    1. `c f <x> <y>`: hover over the point (**c**artesian coordinate, **f**eet) and then write `FIRE` to the screen.
    1. `c m <x> <y>`: similar as above (**c**artesian coordinate, **m**eter).
    1. `p f <radius> <angle>`: similar as above (**p**olar coordinate, **f**eet).
    1. `p m <radius> <angle>`: similar as above (**p**olar coordinate, **m**eter).
    1. Otherwise, tell the user that the command is invalid, but **DO NOT QUIT YOUR PROGRAM**.
    You should read one string from `System.in`, check if it is `l`, `c`, or `p`. If not, show warning and _start over_.
    If the string is `l`, do what's expected and exit your program.
    If the string is `c` or `p`, read another string from `System.in`, check if it is `f` or `m`. If not, show warning and _start over_.
    If the string is `f` or `m`, read two real numbers from `System.in` (you may assume that the user types two real numbers here), and do what's expected. Start over.

The origin is where you take off.
Positive lab x-axis points to the **right** if you stand on a big blue cross and facing a big green cross.
Positive lab y-axis points to the **front** of your drone _before taking off_.
Remember, in polar coordinates, **0 degree is positive x**, 90 degree is positive y, 180 degree is negative x, 270 degree is negative y.  Note that the drone's method calls only accept positive angles.

**Important Note:** User **ALWAYS** types in global (absolute) coordinates.
It's your responsibility to transform it to drone commands.  Note that you will need to keep a set of current location variables.

**Important Note:** You may choose to rotate or not rotate your drone.
You get different grades based on the way you accomplish your mission.
If you do rotate your drone, be sure to rotate it back before landing.
Also, the oritentation of the coordinate system NEVER changes once you take off.

**Note:** To tell _user_ something went wrong, use `System.err.println`.
Writing anything except `FIRE` to `System.out.println` may turn the anti-virus weapon into an uncontrollable beast.
If you are interested in the differnence among `System.in`, `System.out`, and `System.err`, you may consult
[this](https://www.jstorimer.com/blogs/workingwithcode/7766119-when-to-use-stderr-instead-of-stdout)
or
[this](https://stackoverflow.com/questions/3385201/confused-about-stdin-stdout-and-stderr).

**Note:** To minimize rounding errors, please leverage `Math.round(...)` when converting `double` to `int`.

**Hint:** You may use the `drone.move(...)` command (see [Cheat Sheet](https://github.com/ELE115/docs/blob/master/Drone_Methods_Cheat_Sheet.md#movements)).
Be aware of couple details if you you `move`:
1) All coordinates provided as parameters to move are *relative* to the current position of a drone
2) When a drone is placed on the big blue cross and its camera faces the big green cross, positive _lab_ y-axis points the same direction. However, positive _drone's_ y-axis (expected in *move* command) points into the white wall (to the left if you look from the top and toward the big green cross).

**Hint:** You SHOULD reuse the functions you have created in Part 1.
You need two variables to store your current location
and, if you rotate your drone, one additional variable to store your drone's orientation.

**Hint:** Math in polar coordinate is hard. Math in cartesian coordinate is easy.
Google is your friend.

**Hint:** You may create more functions if you want.

Show your code and demonstrate your result to TAs.  The TAs will type in a sequence of absolute points in mixtures of units.
Commit and push.

As a bonus, if you want to rotate and fly forward, flying the shortest path, you will get some bonus points.  Note that this is not required and you can use the `drone.move(...)` command for full credit.  Turning and flying forward is more difficult as you need convert relative offsets to polar and track you current angle with a variable.

## Report from the scout

Thanks to the scout we sent out earlier this week, we have located the exact location of the virus.
If you take off at the big blue cross, coordinates of the five green crosses are:

| Description | `c f <x> <y>` | `c m <x> <y>` | `p f <radius> <angle>` | `p m <radius> <angle>` |
| --- | --- | --- | --- | --- |
| Right most | `c f 7 6` | `c m 2.3 2` | `p f 9 41` | `p m 3 41` |
| Front right | `c f 1.5 3` | `c m 0.5 1` | `p f 3.4 63` | `p m 1.1 63` |
| Middle (big) | `c f 0 10` | `c m 0 3.5` | `p f 10 90` | `p m 3.5 90` |
| Front left | `c f -1.5 3` | `c m -0.5 1` | `p f 3.4 117` | `p m 1.1 117` |
| Left most | `c f -7 6` | `c m -2.3 2` | `p f 9 139` | `p m 3 139` |


