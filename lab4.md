# Background

## Learning objectives

* Learn how to use one dimensional arrays
* Learn how to use multidimensional arrays
* Apply transformations to arrays using images as an example

## Story

In this lab we are going to test new drone capabilities. First, we will perform its characterization by comparing the drone's speed parameter setting versus the actual speed. Second, we will use the drone's camera to take photos (including selfies/dronies, if you want) and apply simple image effects. Later in the class when you learn how to work with files so you will be able to save and share your photos!

# Part 1: Drone's Speed Setting Testing

Before the next mission, we want to test different parameters of a drone and check that it behaves as expected. In particular, we will be setting the drone's parameter *speed* and comparing it to a measured speed value.

To measure how precise the speed setting of the drone is, we will perform multiple forward moves using a known distance. Before every move we will configure a drone to have a random speed. You can read that speed from a drone using *fetchSpeed()* method. We have already provided those function for you in the starter code:

```java
// Instruction: Please copy the following into Main.java

public static void makeMove(ITelloDrone drone, int move_dist_cm)
{
    drone.forward(move_dist_cm);
}

public static void prepareMove(ITelloDrone drone, int total_moves)
{
    Random rand = new Random();
    // Make it turn for a while
    drone.turnLeft(360 / total_moves + 360 * 2);
    int speed = 30 + rand.nextInt(70);
    drone.setSpeed(speed);
}
```

Since every move has a known distance, we need to time how long they take. To do this, we will use the motor time of the drone. It can be read from a drone using the *fetchMotorTime()* drone method. So, if we read it just before a move and just after it, we will be able to calculate a speed during a move by dividing distance over time.

We want to perform regular, automatic, testing of the drone's speed setting, therefore we do not want to ask the user for any input while the program is running. However, we do want to test it under different conditions, and therefore we want to use command line arguments to provide two parameters for our program: **number of moves** and **move distance**. You should use `args` parameter of `main` function to get those values.  Remember that the arguments passed on the command line show up as an array of strings `String[] args` which are passed into the main method.

At the end of our test, we have to print a report consisting of two parts:

Summary:
- min/max speed setting of a drone during the flight
- min/max calculated speed of a drone
- average speed across all move segments. This must be calculated using the total flown distance divided by the time **spent on flying**. You should not count time used for preparation between moves.

Details:

The next line for each segment:
- `Move#: <segment #> MT: <motor time> CS: <calculated speed> SS: <speed setting>`

For example, a report can look like this:

```
========================================
REPORT SUMMARY:
----------------------------------------
Speed setting : Min - 38.00, Max - 100.00
Speed measured: Min - 25.00, Max - 50.00
Speed average: 36.36
=========================================
DETAILED REPORT:
----------------------------------------
Move#: 0 MT: 2 MS: 50.00 SS: 100.00
Move#: 1 MT: 2 MS: 50.00 SS: 90.00
Move#: 2 MT: 3 MS: 33.33 SS: 55.00
Move#: 3 MT: 4 MS: 25.00 SS: 38.00
```

#### Requirements and assumptions:

1. You have to read *number of moves* and *distance of each move* from the command line program arguments. You can assume that they are always valid inputs.
2. Structure your code. Move common operations to functions, where every function performs a single task.
3. Do __NOT__ modify `makeMove` and `prepareMove` methods.
4. You have to print the Summary first and the Details after in the report.

# Part 2: Testing Video Capturing and Processing Images

We have now learned enough of the Java language to operate on complex, array-based, data.  It is time to test the drone's video streaming capability and take cool photos! In this part, you will write a program which will capture a specified number of consecutive frames from the drone by a command, show those frames on a screen, and apply simple visual effects to them, redisplaying them on the screen.

But before we start, we need to learn a bit about how images are stored on a computer and how they are displayed.

---

### Computer Image Representation
Computers store everything as a set of bits, and images are not an exception from that rule. An image is usually stored as a two-dimensional array of pixels, where every pixel has three color components - the amount of red, the amount of green, and the amount of blue (RGB). Every color component has 8 bits, therefore each color components takes on values from 0 to 255. So, for example, simple colors have the folowing Red Green Blue (RGB) values:

```
black - R=0, G=0, B=0
read - R=255, G=0, B=0
green - R=0, G=255, B=0
orange - R=255, G=165, B=0
white - R=255, G=255, B=255
```

We will represent images of integer arrays with three dimensions.  The dimensions are `int [width][height][color_channel]`.  There are three color channels so the array will be `int [width][height][3]`.  Therefore to access a particular color value, you would initialize it like `int [][][] image = new [width][height][3];`.  To access the red value of the pixel at location (1, 2), you would use `image[1][2][0]`, the green value is `image[1][2][1]`, and the blue value is `image[1][2][2]`.

With this knowledge of computer image representation and Java we can create significant geometrical and color effects! Lets walk though the effects we will be creating.

### Image Effects

#### Filtering out all color components except one
The easiest image transformation is filtering out all components except one. For example, we can leave only the green component, and remove red and blue ones. To accomplish that, we have to keep the value of the green component of the pixel and set the blue and red components to zero for every pixel in an image.

#### Grey-scale Effect
The next transformation is converting a color image to a greyscale one. This can be achieved by averaging all three components of the original image and setting all three components (red, green, blue) to this value. For example, the orange color has component values of (255, 165, 0), and its corresponding greyscale representation will be (140, 140, 140).

#### Inverse Effect

The third simple effect if converting colors to their inverse. Though it sounds simple, it looks really cool! To convert an RGB color to its inverse counterpart, you need to subtract the current pixel's component value from its maximum (255). For example, the inverse of the color white(255,255,255) would be black (0, 0, 0), which is not surprising at all. Think about what happens, when you apply a inverse effect twice to same image?  Note to accomplish the inverse effect, you should subtract each component from 255.

----

To enable you to focus on image processing, we provide you with *FrameGrabber* class, which as you may guess grabs video frames from the drone's video stream. `FrameGrabber frameGrabber = new FrameGrabber(<int N>);` creates an object `frameGrabber` which can store N consecutive video frames. We want this parameter to be configurable through the program arguments, so you can specify how many frames to capture. You should use the following existing methods of the *FrameGrabber* class, which we provide for you:

```java
void recordAndDisplay() // records consecutive number of video frames specified when creating an object. After recording is finished, it shows every frame in a separate window with a corresponding name

// returns a three dimensional array where the first two indices are the the x location and y location
// the third is the color chanel R, G, B where R is index zero, G is index 1 and R is index 2
// note that the array is int[x][y][colorchannel] where color channel is {0, 1, 2}
public int[][][] getImageArray(int frameNumber) // gets image by frameNumber

public void setImageArray(int frameNumber, int[][][] theImage) // sets an frameNumber image to passed theImage

public void displayBufferedFrames() // displays the frames that are currently stored in new windows

```

You will need some code like this at the beginning of your program to set up the video.
```java
// created a frame grabber to grab the number passed to the new FrameGrabber
FrameGrabber frameGrabber = new FrameGrabber(framesToSave);
// Opens a live video window showing what the drone sees
drone.addVideoListener(new VideoWindow());
// Sets the export type to a BufferedImage.  This is needed in order to have FrameGrabber work
drone.setVideoExportType(TelloVideoExportType.BUFFERED_IMAGE);
// Sets frameGrabber to listen to video streams
drone.addVideoListener(frameGrabber);
// turns on the video
drone.setStreaming(true);
```

You have to write a program which takes the number of frames to record and display as a command line parameter, instructs a drone to take off, fly up an additional 50cm, and asks a user to input one of the next commands:

- `snap` - record video frames and display them
- `effect <name>` - apply effect to all saved frames and update corresponding windows. `<name>` has to be one of the effects: `"redonly", "greenonly", "blueonly", "grey", "negative"`
- `quit` - land the drone and exit

#### Requirements and assumptions:

1. You have to read number of frames to record and display as a command line argument
2. You should structure your code and group common operations into functions
3. You should check if the command is valid, and if not, print and error message and ask to enter it again. __Do not quit the program on incorrect input!__
4. The only file you should modify is `Main.java`

