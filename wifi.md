# Switching between station mode and wifi mode

## Background

The drone operates in two modes: station mode and wifi mode.
Station mode means that the drone connects to an existing wifi router.
Wifi mode means that the drone creates a wifi and you may connect to it.

Neither of the two modes are perfect:
Camera-related stuff usually doesn't work in station mode.
Emergency shutdown button doesn't work in wifi mode.

## Which mode is it in right now?

1. Turn your drone on.
1. Use your mobile phone to scan existing wifi.
    * If you see a wifi named `TELLO-<droneId>`, then that must be in wifi mode.
    * If you can't see, then it is in station mode.

## Does the mode reset after removing the battery of the drone?

**No.** Mode won't change unless you purposefully do so.

## Switch from station mode to wifi mode

1. Turn your drone on if you haven't done so.
1. Press the power button on your drone for about 5 seconds and then release.
1. Your drone is now in wifi mode. Connect your laptop to `TELLO-<droneId>` to operate your drone.
1. Be mindful about the fact that you __no longer have emergency shutdown button__.

## Switch from wifi mode to station mode

1. **Update the ELE115 project template to the newest version (v1.4 or higher).**
([How?](https://github.com/ELE115/docs/blob/master/setup.md#appendix-keep-your-project-template-updated))
1. Create a project. We suggest you name it as `wifi-to-station`.

    **Note:** You don't have to setup Git for this.

1. Code `Main.java` as follow:

    ```java
    package com.github.ele115.<your_netid>.wifi_to_station;
    
    import com.github.ele115.tello_wrapper.Tello;
    
    public class Main
    {
        public static void main(String[] args)
        {
            var drone = Tello.Connect("<droneId>");
            drone.setStationMode("ELE115-TELLO", "<password>");
        }
    }
    ```

    **Note:** Don't include `<`,`>` into your code.

1. Turn your drone on if you haven't done so.
1. Wait for about 3 seconds.
1. Connect your laptop to the wifi named `TELLO-<droneId>`.
1. Run the code.
1. Wait for about 30 seconds.
1. Your drone is now in station mode. Connect your laptop to `ELE115-Tello` to operate your drone.

