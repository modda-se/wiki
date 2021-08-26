# Video Looper
This is a simplified guide for how to install the [**Adafruits - Rpi Video Looper**](https://github.com/adafruit/pi_video_looper). It's an application that turns your Raspberry Pi into a dedicated looping video playback device. This can be used in art installations, fairs, theatre, events, info screens, advertisement etc...

## Installation

Let's start by installing the video looper:

    sudo apt-get update
      
    sudo apt-get install -y git

    cd /Downloads

    sudo git clone https://github.com/adafruit/pi_video_looper.git
       
    cd pi_video_looper
       
    sudo chmod +x install.sh
       
    sudo ./install.sh

All done! Now let's change some settings.

## Configuration

To change settings of the Video Looper, type:

    sudo nano /boot/video_looper.ini

From here you can change a lot of things but here's some important ones:

* If you want to load videos from a USB drive, you don't need to change anything. Load up your favourite videos (placed in root of USB) and connect it to your Rpi.
* Although, if you have a Rpi ZERO, that's not so easy without adapters. Instead you can upload videos to the SD-Card, but you'll need to change these parameters, like this:

        #file_reader = usb_drive
        file_reader = directory
        #file_reader = usb_drive_copymode

This will now make the video looper look for videos in a directory on the SD-card, instead of the USB drive. But, there's also some permission problems with the installed video directory `/home/pi/video`, so we use the `Videos` folder instead, like so:

        # The path to search for movies when using directory file reader.
        path = /home/pi/Videos

When your done, hit **CTRL+X** followed by **Y** and **ENTER**, to Save. 

**NOTE!** - If you have installed a **Lite** version of the Raspberry Pi OS, there's no `Videos` folder by default, so create one:

    mkdir /home/pi/Videos

For easier access to the video looper settings, you can also pull the SD-card out and connect it to your computer, open `video_looper.ini` which is located in the root of the SD-card with a text editor.

More info about the Video Looper settings can be found here: https://learn.adafruit.com/raspberry-pi-video-looper/usage

## Uploading videos
As described earlier, by default you transfer videos to a USB drive, plug it in, videos starts playing! 

But, when using the SD-card as storage, the easiest way to upload videos is to use a FTP software, like [FileZilla](https://filezilla-project.org/). Once connected with FTP, go to the folder we created earlier:
      
        home/pi/Videos
        
Now start uploading some awesome videos that will loop forever! :D

## Commands and file naming
* **ESC** - Exits video looper.
* **K** - Skips to next file.
* **S** - Stop/Start playback of current file.
* **P** - Shuts down RPi.

You can have one video repeated X times before playing the next by adding `_repeat_Nx` to the filename of a video, where N is a positive number, for example:
    
    Wedding_repeat_3x.mp4
    Divorce_repeat_x12.mp4

## Disable/Enable Video Looper
To **disable** and prevent the Video Looper from ever starting again at boot, run this script located in the `pi_video_looper` folder:

    sudo bash /home/pi/Downloads/pi_video_looper/disable.sh

To **enable** it again ,run:

    sudo bash /home/pi/Downloads/pi_video_looper/enable.sh

## To-do

- Add step to sync video folder with Rclone (Google Drive, Dropbox etc.)
