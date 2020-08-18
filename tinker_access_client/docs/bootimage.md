## Creating a tinker-access-client boot image:

This document details the steps required to create a [Raspberry Pi OS](https://www.raspberrypi.org/downloads/raspberry-pi-os/) boot image and prepare it for the tinker-access-client.

There are many such guides that you can find, some with much more info, some with much less. I will let you pick your own poison, but its hard to beat [this guide](https://www.raspberrypi.org/documentation/installation/installing-images/README.md).

The intent of this guide is to document a few additional steps that will facilitate the install in a completely headless mode (i.e., not requiring a monitor and keyboard). In order to do a completely headless setup, there needs to be a method to determine the IP address assigned to the Pi, external to the Pi. Access to the network router/DHCP server would typically be the desired method. If such a method is not available, then the initial stages of setup will need to use a monitor and keyboard, until the IP address can be determined and the SSH and/or VNC services enabled. After that, the setup can continue in a headless mode.

1. Download the [Raspberry Pi OS image](https://www.raspberrypi.org/downloads/raspberry-pi-os/). The "Raspberry Pi OS (32-bit) with desktop" is the typical desired image. It is a somewhat light-weight image in that it does not include all of the recommended software of a full install, but it still includes the desktop.

2. Write the image to an SD card, using your preferred method. The standard method is the [Raspberry Pi Imager](https://www.raspberrypi.org/documentation/installation/installing-images/README.md).

#### Steps 3-8 are optional. If you do not want to start the install in a completely headless setup and are starting with a keyboard and monitor you can install the SD card in the Pi, power it up, and continue the setup starting at step 9.

3. Mount the *boot* partition of the SD card locally, so that you can add a couple of files to the root directory of the *boot* partition.

4. [Enable SSH for a headless Pi](https://www.raspberrypi.org/documentation/remote-access/ssh/#:~:text=Enable%20SSH%20on%20a%20headless%20Raspberry%20Pi). Create an empty file named *ssh* at the root of the *boot* partition. This will automatically enable the SSH service when the Raspberry Pi boots up, which is normally disabled by default.
+
From the root directory of the locally mounted *boot* partition run the following command:
+
```
sudo touch ssh
```

5. [Setup WiFi for a headless Pi](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md). Create a file named *wpa_supplicant.conf* in the root directory of the *boot* partition that contains your WiFi credentials. On the initial boot, the Raspberry Pi will copy this file to the appropriate location and use it to connect to your WiFi network so that you can continue to configure it via SSH.
+
From the root directory of the locally mounted *boot* partition run the following command:
+
```
sudo nano wpa_supplicant.conf
```
+
Paste the following contents into the file and save. Modify the SSID and password to match your actual WiFi access point credentials.
+
```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=US

network={
 ssid="<Name of your wireless LAN>"
 psk="<Password for your wireless LAN>"
}
```
6. Unmount the *boot* partition, remove the SD card, install in the Raspberry Pi, and power it up.

7. Connect to the Raspberry Pi via SSH and enable the VNC server to complete the install via the desktop via a VNC client running locally.

From your local machine, ssh into the Raspberry Pi. Use the actual IP address assigned to the Pi:

```
ssh pi@<Assigned IP address of PI>
```

The default pi username password of *raspberry*.

Enable the VNC server via *raspi-config*:

```
sudo raspi-config
```

Browse

![interface](/images/ssh_raspi_config_interface.png)
