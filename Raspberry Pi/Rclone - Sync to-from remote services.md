# Rclone - Sync to/from remote services
Rclone can be used to sync raspberry pi computer folders/files to one or more remote services like Google Drive, Dropbox etc. This is a modified script of rclone called [**rclone4pi**](https://github.com/pageauc/rclone4pi) which makes the installation process super easy.

For more information about **rlone**, see https://rclone.org and/or https://github.com/ncw/rclone

## Installation
Connect through SSH (recommended) or typing directly on the RPi:

    curl -L https://raw.github.com/pageauc/rclone4pi/master/rclone-install.sh | bash
    
This will install rclone-install.sh, rclone-sync.sh and create a subfolder rpi-sync in users home eg. */home/pi/rpi-sync* 

## Configuration
Now we need to configure rclone to our preferred remote service (Google Drive, Dropbox etc.), so type:

    rclone config

A configuration wizard will pop up. We're setting up rclone for use with Google Drive, so start with creating a new remote by choosing: *n) New remote*

    No remotes found - make a new one
    n) New remote
    s) Set configuration password
    q) Quit config
    n/s/q> n

Enter a name for it:

    name> your-remote-name

Choose the remote service by typing in the corresponding number. We'll use 15 = Google Drive:

    Storage> 15

Next step, just press *ENTER* for the default:

    client_id> 

Next step, just press *ENTER* for the default:

    client_secret> 

Choose the level of requesting access from drive. We'll choose option 1: 

    scope> 1

Next step, just press *ENTER* for the default:

    root_folder_id> 

Next step, just press *ENTER* for the default:

    service_account_file>

Edit Advanced config, choose *No (default)*:

    Edit advanced config?
    y) Yes
    n) No (default)
    y/n> n

Use auto config? Choose *No*:

    Use auto config?
    * Say Y if not sure
    * Say N if you are working on a remote or headless machine

    y) Yes (default)
    n) No
    y/n> n

Here comes the important part! You'll need to give rclone access to your Google Drive account, so... 
* Copy the URL (in the terminal) and paste it in your web browser.
* Choose the Google account that you want to sync to/from.
* Click Allow.
* Now, copy the new authentification/access URL.
* Go back to the terminal and paste it.

Configure this as a Shared Drive (Team Drive)? Choose *No*:

    y) Yes
    n) No (default)
    y/n> n

That's it! If you're happy with your choices, type *Y*:

    y) Yes this is OK (default)
    e) Edit this remote
    d) Delete this remote
    y/e/d> y

Press *Q* to quit the rclone config.

## Script for syncing
Here's a command that you'll need to run everytime you want to start syncing. Rclone will not automatically recognize when new files are added on the remote service and vice versa. So you'll need to make it sync at boot or at a specific time. More on that later.

Let's create a script including that command:

    cd /home/pi/rpi-sync
    sudo nano rclone-simple-sync.sh

Paste this inside and change the paths, according to your remote service and rpi: 
    
    #!/bin/bash
    rclone sync -v name-of-your-remote:path/on/your/remote /home/pi/path_on_rpi --dry-run

Press *CTRL+X*, then *Y* and *ENTER*, to save.

This is just an example of what the command/script could look like:

    #!/bin/bash
    rclone sync -v rclone_drive:/Personal/Videos/Favourites /home/pi/Videos --dry-run

Give script execute permission:

        sudo chmod +x rclone-simple-sync.sh



A couple of important notes!
* If you have folder with spaces, you'll need to add *"quotation marks"* before and after, like so: 

        /Personal/Video/"Master of the PCBs"

* You can flip the paths in the command, to make it sync the other way around. 
        
        Remote service to Rpi:
        rclone_drive:/Personal/Videos /home/pi/Videos

        Rpi to remote service:
        /home/pi/Videos rclone_drive:/Personal/Videos

* Please, use the flag at the end *--dry-run* when you're testing/setting things up. Otherwise you can end up syncing and deleting files on your remote drive!! Remove *--dry-run* when you're sure everything works.

## Put script in crontab to get executed a specific time or on boot.

Add it to *crontab* to run it x times a day:

        sudo crontab -e

This makes it run every 5 minutes:
        
        */5 * * * * /home/pi/rpi-sync/rclone-simple-sync.sh

To make it run at startup, add this:

        @reboot /home/pi/rpi-sync/rclone-simple-sync.sh

Press *CTRL+X*, then *Y* and *ENTER*, to save. All Done!