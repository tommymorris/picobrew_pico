# picobrew_pico
This fork is intended for PicoBrew Z Series support using a Raspberry Pi 3 to run the server. 

The install scripts and RPI3 configuration here have not been tested for non-HTTPS Picobrew machines (Pico and Zymatic) but they should work.

The install scripts and RPI3 configuration here have not been tested for RPI4 but should work. Raspberry PI 0, 1, and 2 are not supported.

This repository is a fork of https://github.com/chiefwigms/picobrew_pico. Almost all code is theirs.  The scripts I added to enable Raspberry PI and create certificates for the Zseries are largely based on scripts from https://github.com/duffyco/planbeer.

## Requirements
Have a Raspberry PI 3.

The RPI3 will reside in your home next to your WIFI router. 
Plug a CAT6 cable into the back of your router and into the Ethernet port of your RPI3.

------   Ethernet(wire)     ----------     Wireless    -------------
Router  <-------------->      Rpi 3      <---------->   PicoBrew Z
------                      ----------                 -------------
                           OS: Raspbian
                            Vx: Docker
                               App


The RPI3 will be turned into a WIFI access point with the following credentials.
SSID: picobrewers
Passphrase: 12345678


### How to install, start the server, and brew a beer. 
1. Use Rufus (https://rufus.ie/ I use the portable version) and "burn" buster to sdcard.  Buster is the lastest version of the Raspberry PI Raspian operating system.

https://www.raspberrypi.org/downloads/raspbian/ - (2020-02-13 for the guide).

2. Go ahead and create an SSH file in the root.  This will activate the SSH server and save you from going downstairs.  I speak from experience.

For Windows users: navigate to D: | Create a Next Text Document | Change the Name to SSH  (no extension)

Eject the drive safely.

3. Start up your Raspberry PI 3. Default username/pass is pi/raspberry.  Change the default password:
 passwd 

5. Run the following:
sudo apt-get update

6. Clone the repo in the home directory:
 git clone https://github.com/chiefwigms/picobrew_pico 

7. Run the setup script.
cd ~/picobrew_pico/bin
sudo ./setupRPI3.sh 

This script does many things. There will be some error messages. Ignore the messages about isc-dhcp-server failing to start.
a. It sets up a subnet of 192.168.42.0.  Parameters are at the top of the file.  Adjust as needed.
b. It also makes your RPI3 an acess point on the wlan0 interface.
The SSID = picobrewers. The wifi passphrase = 12345678. You may adjust both of these in the setupRPI.sh file before running or just leave them alone. 
You can change the passphrase later by editing /etc/hostapd/hostapd.conf file.
c. It installs many needed packages.
d. It creates self signed certificates. 

8. Reboot your RPI3
sudo reboot

9. Start the server
cd /home/pi/picobrewr_pico
sudo bin/startup.sh

10. Connect to the recipe crafter.
a. On your RPI3: navigate to http://picobrew.com or localhost:8080 in the browser.
b. On another computer or phone you can join the picobrewers wireless lan, then navigate to https://picobrew.com in your browser.

Click 'Zseries Recipes' -> new to create a recipe.
Click 'Zseries Recipes' -> Library to view your recipes.

Recipes are created and displayed as machine steps. Copy the machine steps from the Picobrew.com website for your recipe.

11. Connect your Picobrew 
a. Turn on your Zseries
b. Update the Wifi settings on the Picobrew Z. Connect to SSID:picobrewers with passphrase: 12345678
c. brew

## Disclaimer
Except as represented in this agreement, all work product by Developer is provided ​“AS IS”. Other than as provided in this agreement, Developer makes no other warranties, express or implied, and hereby disclaims all implied warranties, including any warranty of merchantability and warranty of fitness for a particular purpose.
