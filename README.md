#
# Raspberry Pi Setup System
#

I created this system to accelerate provisioning a Raspberry Pi from scratch, which is something I do on a regular basis, at least every time I start a new project. I hope you find this useful.

<h3>Step 1: Load Raspbian onto a Micro SD card</h3>

Note that these instructions work on my Macbook Pro running Mac OS X Mavericks. I haven't tested this on any other system. If you are using a different system and you would like to add to this, please let me know and I'll be glad to make room for your contribution.

1. Dowload the latest Raspbian build ZIP file from http://www.raspberrypi.org/downloads/

2. Open your terminal (Found in Applications/Utilities) for the rest of the operations. I created a directory where my raspbian images live at ~/dev/raspi_os. You should CD into that directory.

3. Unzip the raspbian image: ``` unzip ~/Downloads/<Raspbian image filename>.zip ./ ``` and remove the zip file from your Downloads: ``` rm -f ~/Downloads/<Raspbian image filename>.zip ```. Verify the presence of the image file in your current directory. it should be ``` <Raspbian image filename>.img ```

4. BEFORE you insert the SD Card, type ``` df -h ``` to list the mounted file systems. By doing this, you will be able to see which one is the SD Card.

5. Insert the SD Card into your Mac, wait a few seconds, and type ``` df -h ``` again. Compare the entries to see what device is your SD Card. Mine shows up as ``` /dev/disk1s1 ``` but it could be /dev/disk2s1 when my backup drive is connected. It's important to know that it's not necessarily always the same path.

6. Unmount the disk that you know is the SD Card: ``` sudo diskutil unmount /dev/disk1s1 ```

7. Write the image onto the card: ``` sudo dd bs=1m if=<Raspbian image filename>.img of=/dev/rdisk1 ``` (note that rdisk1 refers to your disk1s1) This operation may take a while.

8. Before removing the card, type ``` sudo diskutil eject /dev/rdisk1 ```

That's it. Remove the SD Card from your computer and load it into your Raspberry Pi. It is ready for first boot. Move on to the next section.

<h3>Step 2: Run your Raspberry Pi for the first time</h3>

1 - Make sure your raspberry pi is connected to the internet.  For me it's as simple as plugging an ethernet cable. The process takes you through configuring a wireless adapter (I am always using the EDIMAX EW7811, which is a tiny 802.11n USB adapter).

2 - Log into your raspberry pi using the 'pi' user and 'raspberry' as password. This the standard defined user. This process will secure this account so don't worry for now.

3 - Ensure that you have git installed (just type 'git' at the command prompt and see if it works). If it isn't installed, install it by typing:

```
	sudo apt-get install git-core
```

4 - Clone this repository: 

```
	cd ~
	git clone https://github.com/fpapleux/raspi
```
This will have created a raspi directory in the pi user's home.

5 - Next, execute 'init.sh' to go through the first part of the process:

```
	cd ~/raspi
	sudo ./init.sh
```
After updating the system, the script will force you to restart the machine. This is just a precaution I included to make sure that the next script will run with a fresh start.

6 - After rebooting, log in using your new user credentials and execute the second part of the process:

```
	cd ~/raspi
	sudo ./raspi.sh
```
Just follow the script's instructions. It should be clear enough. If it isn't, drop me a note...

<h3>Acknowledgments</h3>

I need to thank whoever wrote Wheezy installation self-help guide at Instant Support Site for the valuable information (http://www.instantsupportsite.com). It has been extremely useful.
