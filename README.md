# piProject
Raspberry pi project. Containing setup of a headless pi3.


## Setup 
Download the latest raspbian lite at: https://www.raspberrypi.org/downloads/raspbian/
Either write the image using etcher(or another tool) or do it in the commandline.(i used etcher)

### Network setup
First we want to set a static ip for the computer we are using. create a new wired network with ip 192.168.0.1/24.

use nm-connection editor to make the network "shared with other computers" in ipv4 settings.

__1. Open a terminal__
open dhcpdc config file on the sd card and uncomment the default eth0 interface.
```
  nano /media/rootf/etc/dhcpcd.conf
```

make sure it looks like this. The most important part is that the routers is the same ip as the wired network on your computer.
```
interface eth0
        static ip_address=192.168.0.10/24
        static ip6_address=fd51:42f8:caae:d92e::ff/64
        static routers=192.168.0.1
        static domain_name_servers=192.168.0.1 8.8.8.8 fd51:42f8:caae:d92e::1
```
__2. connect to the pi(WIRED)__
The raspberry pi has a standard login, with the name "pi" and password "raspberry". 
Connect with ssh and enter the password:
```
  ssh pi@192.168.0.10
```

Now the pi should have internet connection through you laptop and are able to connect to the pi via ssh. if this is not the case, you did something wrong.

__3. connect to the pi wirelessly__
You need to have completed step 2 to complete this step.

On the pi run raspi-config:
```
  sudo raspi-config
```

Navigate to network options and go into wi-fi to setup the wifi network.
Enter a SSID(wifi name) and the password. Now finish and aggree to reboot the pi. 
Now you should be able to connect via wifi to the pi. 

open ifconfig and locate the ip of the wifi network(often 192.168.X.X or 10.42.X.X).
```
  ifconfig
```
Now use nmap to search for other ip's on the network with the following command(exhange "WIFIIP" with the real ip, without the "").
```
  nmap -sP "WIFIIP"/24
```

The ip of the pi should pop up, locate it and connect with ssh and enter the password.

```
  ssh pi@"IP"
```

__4. (OPTIONAL) change the password__
change password with the following cmd:
```
  sudo passwd
```

## ROSBerryPi Setup
```
http://wiki.ros.org/ROSberryPi/Installing%20ROS%20Kinetic%20on%20the%20Raspberry%20Pi
```

## OpenCV 3.4.1 setup
```
https://www.deciphertechnic.com/install-opencv-python-on-raspberry-pi/
```

## Backup image and restoring
```
https://thepihut.com/blogs/raspberry-pi-tutorials/17789160-backing-up-and-restoring-your-raspberry-pis-sd-card
```
