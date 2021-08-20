# Video Looper
This is a simplified guide for how to install the **Adafruits - Rpi Video Looper**. This is an application that turns your Raspberry Pi into a dedicated looping video playback device. This can be used in art installations, fairs, theatre, events, infoscreens, advertisment etc...

Original project can be found here: https://github.com/adafruit/pi_video_looper

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

To change settings of the Rpi Video Looper, type:

    sudo nano /boot/video_looper.ini

From here you can change a lot of things but here's some important ones:

* If you want to load videos from a USB drive, you don't need to change anything. Load up your favourite videos (placed in root of USB) and connect it to your Rpi.
* Although, if you have a Rpi ZERO, that's not so easy without adapters. Instead you can upload videos on the internal memory, but you'll need to change these parameters, like this:

        #file_reader = usb_drive
        file_reader = directory
        #file_reader = usb_drive_copymode

This will make the video looper look for videos in a directory on the internal memory, instead of the USB-drive. But, there's also some permission problems with the installed video directory `/home/pi/video`, so we use the `Videos` folder instead, like so:

        # The path to search for movies when using directory file reader.
        path = /home/pi/Videos

When your done, hit `CTRL+X` followed by `Y` and `ENTER`, to Save. 

For easier access to the video looper settings, you can also pull the SD-card out and connect it to your computer, open `video_looper.ini` which is located in the root of the SD-card with a text editor.

More info about the Video Looper settings can be found here: https://learn.adafruit.com/raspberry-pi-video-looper/usage

## Uploading videos (file_reader = directory)

The easiest way to upload videos to the Rpi, is to use a FTP software, like [FileZilla](https://filezilla-project.org/). Once connected with FTP, go to the folder we created earlier:
      
        home/pi/Videos
        
Now start uploading some awesome videos that will loop forever! :D
       
## Troubleshooting

When using the Raspberry Pi ZERO, you might want to use the Analog audio only. Using both HDMI and Analog audio out will cause stuttering because the Rpi ZERO is not powerful enough. You can change this in the `video_looper.ini` which is explained above:

       #sound = both
       #sound = hdmi
       sound = local

## To-do

- Add instructions for removing/disable the Video Looper.








