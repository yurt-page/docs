Everybody in the world won't buy a hosting. But almost everybody has a Wi-Fi router or a friend with router. And we may host websites there.
Routers are very limited: typical memory from 4 to 16Mb, RAM from 32 to 128Mb, CPU from 400MHz to 800MHz.
But personal sites shouldn't be so loaded: normally people has about [150 stable relationships](https://en.wikipedia.org/wiki/Dunbar%27s_number).

A router can be:
1. broken: your data is lost. We must back up as much as possible but the decryption key must be stored on a central server.
2. stolen: your data will be lost but the thrift can also read it. We can keep the decryption key in memory so on reboot it will be lost.
3. hacked: ...we fucked up here. But! We may do many things as possible to minimise impact e.g. delete backup files from network only after some long period so a user can restore them on a new router.

### Devices

Hosting type  | CPU cores | RAM   | Disk  |  OS
--------------|-----------|-------|-------|-----
VPC           | 2         | 16GB  | 512GB | Linux
PC            | 4         | 16GB  | 1TB   | Most of them use Windows for games, in USA MacOS is also popular. We may use Docker. Important to have a tray icon.
Browser on PC | 1         | 2GB   | 50MB  | Chrome workers. Open tab, install app or extension
Laptop        | 2         | 8GB   | 200GB | Mostly Windows, MacOS. Sometimes Linux
Nettop        | 2 x86     | 8GB   | 200GB | Windows, Linux, [Low-power x86](https://sequentialread.com/i-was-wrong-about-arm-sbcs/). E.g. Lenovo ThinkCentre
TV/TV box     | 2 ARM     | 4GB   | 8GB   | AndroidTV. We may use Termux
Phone         | 2 ARM     | 8GB   | 128GB | Android. We may use Termux
NAS           | 1         | 8GB   | 2TB   | Proprietary Linux (Disk Station), TrueNAS, Docker
Raspberry Pi  | 1         | 8GB   | 8GB   | Debian
Router        | 0.5       | 128MB | 16MB  | OpenWrt, Linksys Linux
STM32         | 0.1       | 2MB   | 4MB   | Tasmota

See also https://en.wikipedia.org/wiki/Home_theater_PC


#### Raspberry Pi: a single board computer
Raspberry Pi is an ARM based single board computer that doesn't have a fan and energy effective.
Currently a lot of DYI projects uses Pi. It's not so fast as a usual PC but faster than routers.  
You can install a Debian with Python, PHP or Node.JS. So basically every today's software maybe slowly but can be run on Pi.

Most known project is [Pi-hole](https://pi-hole.net/) Ad Blocking proxy.
Mozilla WebThings is Python based and also targeted to be run on Pi.

Yurt must support Pi but since everybody in the World can't buy it we shouldn't be targeted to it as main platform.

#### NAS
Network Attached Storage (NAS) is a small server with a lot of disk space that you can install at home.
Used as a family shared disk to store photos and videos.
Most popular NAS is Synology that has its own OS called [Disk Station Manager](https://www.synology.com/dsm).
It has a lot of cool features but not intended to become a social network.
Also NAS devices aren't cheap, so we can't tell everybody in the world to buy them to run Yurt.
Main feature of NAS is a stack of disks: previously you needed a lot of disk to have at least a terabyte in RAID to survive after a disk failure.

But today you can buy a very cheap disk with few terabytes and just connect via USB to a usual router.
NAS has more advanced CPU but just for storing files even a router will be enough.
Instead of RAID Yurt may back up data to your friend's
So I believe NAS devices will be slowly replaced with advanced routers in feature.
For example with Turris Omnia.

#### Turris Omnia: Router that can be a small server
[Turris Omnia](https://www.turris.com/en/omnia/overview/) is a most powerful router with a fast CPU that can be used as a NAS.
It uses OpenWrt and you can easily install other apps like NextCloud.
This router is a first attempt to make a special device for a self-hosting: it supports LXC containers out of the box and regular users may install a lot of things with just a single click.
A similar router with fast CPU and OpenWRT is the [GL.net Brume](https://www.gl-inet.com/products/gl-mv1000/) but it doesn't have such focus on self-hosting.
