# Drone Methods Cheat Sheet

## Movements
```
takeoff() – instructs a drone to take off
	parameters – No parameters
land() – instructs a drone to land
	parameters – No parameters
up(int c) – instructs a drone to go up by ‘c’ centimeters
	parameters – ‘c’
	Example: up(30) – move up by 30 cm
down(int c) – instructs a drone to go down by ‘c’ centimeters
	parameters – ‘c’
	Example: down(30) – move down by 30 cm
left(int c) – instructs a drone to move to the left by ‘c’ centimeters
	parameters – ‘c’
	Example: left(30) – move left by 30 cm
right(int c) – instructs a drone to move to the right by ‘c’ centimeters
	parameters – ‘c’
	Example: right(30) – move right by 30 cm
forward(int c) – instructs a drone to move forward by ‘c’ centimeters
	parameters – ‘c’
	Example: forward(30) – move forward by 30 cm
backward(int c) – instructs a drone to move backward by ‘c’ centimeters
	parameters – ‘c’
	Example: backward(30) – move forward by 30
turnLeft(int d) – instructs a drone to turn left by ‘d’ degrees
	parameters – ‘d’
	Example: turnLeft(90) – turn left by 90 degrees
turnRight(int d) – instructs a drone to turn right by ‘d’ degrees
	parameters – ‘d’
	Example: turnRight(90) – turn right by 90 degrees
flip(FlipDirection 'dir') - instructs a drone to make a flip in a specified direction. Possible directions are FlipDirection.LEFT, FlipDirection.RIGHT, FlipDirection.FORWARD, FlipDirection.BACKWARD
		parameters - 'dir'
	Example: flip(FlipDirection.BACKWARD) - instructs a drone to make a backward flip
move(int x, int y, int z, int speed) - move to a relative position (x, y, z) with a specified speed.
	parameters - 'x', 'y', 'z', 'speed'
	Example: move(100, 100, 0, 50) - move to a position (100, 100, 0) w.r.t. current position at speed 50.
	Note: for a drone, positive x-axis is in the direction of a camera, and positive y-axis is in the direction to left if you look from the top of a drone.
```    


## Setting Drone Parameters
```
setSpeed(int cmps) – set drone speed to ‘cmps’ centimeters/s
	parameters – ‘cpms’, 10 < cmps < 100
	Example: setSpeed(40) – set speed to 40 cm/s
```


## Streaming Video from a Drone
```
addVideoListener(VideoListener listener)– adds a new video listener to a drone, which receives video frames
	parameters – ‘listener’
Example: addVideoListener(new VideoWindow())- creates a new window which displays video frames received from a drone

setStreaming(bool enable) – enables/disables video streaming from a drone
	parameters – ‘enable’
	Example: setStreaming(true) – enable video stream
```
