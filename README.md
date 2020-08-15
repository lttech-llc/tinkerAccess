![taicon](/taicon.png)

# tinkerAccess
The tinkerAccess system is a Raspberry Pi based access control system that can be used to prevent unauthorized users 
from using devices that require special training. It could also conceivably be used to control electronic lock boxes 
or doors.

The system was originally designed and created by Matt Stallard, Ron Thomas, and Matt Peopping for TinkerMill a 
makerspace in Longmont, CO. It is continually being maintained and enhanced by other contributors in the community.

### Install the tinkerAccess system

There are two main components to the system. If you intend to use the client and server software on separate physical 
devices, then you will want to review the individual documents regarding the installation, configuration, and 
operation of each respective piece.

- [tinker-access-server](/tinker_access_server/README.md) 
- [tinker-access-client](/tinker_access_client/README.md)

If however, you intend to use both the server and client on the same physical device, then you can follow these 
simple instructions. 

From the Rasbian terminal:

```shell
git clone https://github.com/TinkerMill/tinkerAccess.git
cd tinkerAccess
sudo bash
./install.sh
```

After running the installation script, the configuration files for both the server and client are created, but they 
need to be modified for a proper setup before rebooting or restarting the services to take effect.

Edit the server configuation file:

```
sudo nano /opt/tinkeraccess/server.cfg
```

Edit the client configuation file:

```
sudo nano /etc/tinker-access-client.conf
```
