# raspberry_printer_rp3160_gold
Raspberry Pi Software Setup | Update Packages, Install Libraries and Printer Essentials | Install Printer Driver | Raspberry PI 3 Connected TVS3160 GLOD




# CUPS filter for thermal printer TVS3160 GLOD

The linux driver provided on TVS3160 GLOD site unfortunately doesn't work. First, it is 32-bit binary (and so, on x64 system need some x86 libs to be installed). Second, it's PPD is not correct - it just doesn't show any advanced settings because of it. Finally, raster filter just crashes on any try to run it! But even if you run it, you'll see that it's working with printer is not optimal: for example, if it sees a blank line, it will send the blank raster to print (instead of just use 'feeding' command, which is definitely faster!)

This is the solution: PPD is fixed and works. Filter is provided as src (you can found a list of packages need to be installed in order to build it in the header of source). Also, printing of blank lines is optimized.

In order to re-compile the binary (e.g. on a Raspberry Pi), the following libraries must be installed:


Update Packages, Install Libraries and Printer Essentials
Once logged in, type the following at the command prompt (if logged in through ssh, you can copy-and-paste from this browser window to the terminal):


```
sudo apt-get update
sudo apt-get install git cups wiringpi build-essential libcups2-dev libcupsimage2-dev python-serial python-pil python-unidecode
```
The ```“update”``` step refreshes the list of available software packages and takes a couple of minutes.

The ```“install”``` step downloads and installs a number of packages…this may take 20 minutes or so.



# Install Printer Driver
The printer does not need to be connected yet. We can prepare the system the same regardless.
```
cd ~
git clone https://github.com/deepakschauhan/raspberry_printer_rp3160_gold
cd raspberry_printer_rp3160_gold/RP3160 GOLD
make
sudo ./install
```

Your thermal printer may have arrived with a test page in the box or the paper bay. If not, or if you threw that away, you can generate a new one by installing a roll of paper and holding the feed button while connecting power.

To set up this printer as the system default, we’ll be typing two lines similar to the following (but not necessarily identical…read on)…

# You Can use USB Port
```
sudo lpadmin -p <printername> -E -v usb://TVS%20Electronics/RP3160%20GOLD(U)1 -m RP3160/rp3160.ppd
sudo lpoptions -d <printername>
```
# You Can use Serial port--
```
sudo lpadmin -p <printername> -E -v serial:/dev/serial0?baud=19200 -m RP3160/rp3160.ppd
sudo lpoptions -d <printername>
```
  
On the first line, change the “baud” value to 9600 or 19200 as required for your printer. The rest of the line should be typed exactly as it appears above. Likewise for the second line, which needs no changes.


#  Finish Up
Shut down the system. We'll work on the case and wiring next, then return to the final software configuration later.
```
sudo shutdown -h now
 ``` 
  After about 30 seconds, you can disconnect the USB power cable.
