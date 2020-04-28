# Background

## Learning objectives

* Learn how to use abstract data types
* Refactor code from [Lab 4](https://github.com/ELE115/docs/blob/master/lab4.md#part-2-testing-video-capturing-and-processing-images) using abstract data types

# Lab 5: More photo effects!

(Name your project as `lab5-part0`)

During the last lab we learned how to use multidimensional arrays to process images. However, Java has a [`BufferedImage` class](https://docs.oracle.com/en/java/javase/11/docs/api/java.desktop/java/awt/image/BufferedImage.html), which wraps raw image pixels and provides methods to work with an image. Another handy class which is provided in the `java.awt` library is the [`Color` class](https://docs.oracle.com/en/java/javase/11/docs/api/java.desktop/java/awt/Color.html), which provides manipulations with Red, Green, and Blue (RGB) colors.

In this lab, you need to refactor the code from Lab 4 Part 2 using `BufferedImage` and `Color` classes and add two more effects: *sepia* and *blackandwhite*.

You will be using the same `FrameGrabber` class as in [Lab 4](https://github.com/ELE115/docs/blob/master/lab4.md#part-2-testing-video-capturing-and-processing-images), but this time **you have to use its `getImages()` method, which returns an array of saved BufferedImage objects**.
As before, `FrameGrabber frameGrabber = new FrameGrabber(<int N>);` creates an object instance named `frameGrabber` which can store N consecutive video frames. We want this parameter (N) to be configurable through the program arguments, so you can specify how many frames to capture. You should use the following existing methods of the *FrameGrabber* class, which we provide for you:

```java
void recordAndDisplay() - records consecutive number of video frames specified when creating an object. After recording is finished, it shows every frame in a separate window with a corresponding name

BufferedImage[] getImages() - returns an array of recorded BufferedImage objects

void displayImages(BufferedImage[] imgs) - updates saved frames with new images and displays them

```

First, lets study how we can use aforementioned classes.

#### BufferedImage Class

You need to include `import java.awt.image.BufferedImage;` in your program to be able to use it. From the many methods in `BufferedImage`, we will need only few of them to operate on an image:

```
int getWidth(), int getHeight() - return image width and height in pixels correspondingly

int getRGB(int x, int y), void setRGB(int x, int y, int rgb) - get/set a pixel at a specified positing to an RGB value (stored as a single int)
````

#### Color Class

You need to include `import java.awt.Color;` in your program to be able to use it.
The next methods can be used to construct a particular color from its components and get components of a given color:

```
new Color(int rgb) - creates RGB color from combined RGB value stored in a single int (31 bit, red - bits 16-23, green - bits 8-15, blue - bits 0-7)
new Color(int r, int g, int b) - creates an RGB color from specified red, green, and blue components
int getRed(), int getGreen(), int getBlue() - gets corresponding color components
int getRGB() - gets a single RGB value representing the color
```

#### Sepia Effect
This effect makes a photo to look like an [old one](https://en.wikipedia.org/wiki/Sepia_(color)). For every pixel with (r,g,b) components we first calculate temporary values:

```
rtmp = 0.393*r + 0.769*g + 0.189*b
gtmp = 0.349*r + 0.686*g + 0.168*b
btmp = 0.272*r + 0.534*g + 0.131*b
```

and after that, set every component based on the following formula:

```
<c> = 255 if <c>tmp > 255 else <c>tmp, where <c> is one of {r,g,b}
```

To put it in words, new component is a temporary value that saturates at 255.

#### Black and White Effect
This effect transforms every image pixel to either a white or a black one. Remember that white pixel has (255, 255, 255) components, while black pixel has (0, 0, 0) components.
For every pixel in an original image, its weights are calculated first based on the next formula:

```
w = 0.3*r + 0.59*g + 0.11*b
```

and after that it is compared to a threshold value. If a pixel's weight is greater than the threshold, then the pixel becomes black, otherwise the pixel becomes white. We will use value 110 for the threshold.

----

Like in Lab 4, you will need some code like this at the beginning of your program to set up the video.
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
- `effect <name>` - apply effect to all saved frames and update corresponding windows. `<name>` has to be one of the effects: `"redonly", "greenonly", "blueonly", "grey", "negative", "sepia", "blackandwhite"`
- `quit` - land the drone and exit

#### Requirements and assumptions:

1. You have to read number of frames to record and display as a command line argument
2. You should structure your code and group common operations into functions
3. You have to use **BufferedImage** and **Color** classes and their methods to operate on image pixels and their colors (and not use multidimensional arrays)
3. You should check if the command is valid, and if not, print and error message and ask to enter it again. __Do not quit the program on incorrect input!__
4. The only file you should modify is `Main.java`

