# Preparation

> Estimated Time Cost: 20~40min.

Connect to our Wifi `ELE115-TELLO`. Ask the TA for password. **NEVER** share Wifi password(s) with anybody.
[Setup environment](https://github.com/ELE115/docs/blob/master/setup.md) if your haven't done so.

# Part I: Hello Java

> Estimated Time Cost: 10min.

1. **Read the whole [FAQ](https://github.com/ELE115/docs/blob/master/faq.md).**
1. Accept the GitHub Classroom assignment. See Canvas for the link.
1. **Follow the [guide](https://github.com/ELE115/idea-gradle-template/blob/master/README.md) to create a new project.**
**Name** your project as `lab1-hello-java`.

**Note:** You MUST follow the guide to create new projects. Do not try to setup a new project on your own.

Write your code now. Your project shall do (and only do) the following:
* Write `Hello Java` on the screen
* Exit afterwards

1. Hit Shift+F10 to confirm the correctness of your program. Fix problems and retry until success.
1. Once finished, show your `Hello Java` result to the TA.
1. Follow the [Guide on submitting projects to GitHub](https://github.com/ELE115/docs/blob/master/git.md#how-to-setup-git-for-a-single-project).
1. Proceed to Part II.

# Part II: Hello Robot

> Estimated Time Cost: 20min.

1. Accept the GitHub Classroom assignment. See Canvas for the link.
1. Get one Tello drone from the TA.
1. Confirm the content of your drone case:
  * Tello drone x 1, with four propellers and four propeller guards
  * Boards * 4
  * Setup guide x 1
  * User manual x 1
  * Micro USB Cable x 1
  * A small bag containing:
    * Replacement propellers x 4
    * Propeller replacement tool x 1
1. Find your drone Id. It is a 6-characters string located on the **inner surface** of the drone.
**Confirm** that the drone Id is identical to the drone Id labeled on the case.
1. Put some stickers on your drone. Be sure *NOT* to cover the heat sink at the bottom.
1. *Optionally* replace your propeller guards with fancier one(s).
1. **Confirm** with the TA that the drone Id is correct and nothing is missing from the drone case.
1. Get one battery from the TA.

Create **another** project `lab1-hello-robot`.
Code your project to do the following:
* Connect to **your** drone, which should be placed at the blue cross on the floor.
* Let your drone takeoff
* Let your drone fly to the green cross.
* Let your drone land at the green cross.
* Exit afterwards

**Note:** Distance between the two cross is approximately 350 centimeters.

**Note:** You don't have to land *exactly* at the green cross. Anywhere around the cross is acceptable.

To confirm the correctness of your program,
you need to do the following:

1. Power on your drone.
1. Put your drone at the blue cross on the floor.
1. Hit Shift+F10.
1. Collect your drone when it **fully stops**. Do **NEVER** touch a flying drone.

If you think your program is correct proceed to the following:

1. Show your program result (actual drone actually flying) to the TA.
1. Remove the battery from your drone.
1. Pack your drone, with one battery, in your drone case.
Always **double check** your drone Id.
1. Follow the [Guide on submitting projects to GitHub](https://github.com/ELE115/docs/blob/master/git.md#how-to-setup-git-for-a-single-project).
