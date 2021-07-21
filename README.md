# Yurt Page: own website for everybody on Earth and other planets
Yurt is a small house used my nomads. You can easily construct it.

* Web1.0: peoples just readers of others sites: news, books, portals like MSN
* Web2.0: peoples now can create their own content and interact with each others: Wiki, YouTybe, Facebook
* Web3.0: nobody knows but all talking about BlockChain, AI, VR and other buzzwords.
* ....
* This will be a Web100500

Even today anybody can create it's own site: buy a hosting for about 5$ per month and also you have to buy some domain, then install WordPress and configure it.
But nobody will ever visit your site. Only occasional visits from Google search.
The problems are solved by social network: you see everything that your friends posted in a single place. Domains not needed. And that's for free.

Everybody won't buy a hosting. But everybody have a WiFi router or a friend with router. And we may host websites there.
Routers are very limited: typical memory from 4 to 16Mb, RAM from 32 to 128Mb, CPU from 400MHz to 800MHz. But personal sites shouldn't be so loaded: norammly people has about [150 stable relationships](https://en.wikipedia.org/wiki/Dunbar%27s_number).

Another problem is connectivity.


## Similar projects or what do we have today
### Movements
#### IndieWeb
[IndieWeb](https://indieweb.org/) is a movement to leave social networks (they call them Silos) and use personal sites.
They're working on creation of easy to use small website engines, technologies and standards to simplify websites to interact with each others.
For example [WebMention](https://indieweb.org/Webmention) protocol allows to easily see when someone makes repost from your site.

* https://indieweb.org/
* https://github.com/pfefferle/awesome-indieweb

Yurt is not related to IndieWeb because ideologically is different (we are fine with some centralization) and almost nothing can't be reused from technology stack. But we'll try to align with this movement.

#### Freifunk
[Freifunk](https://en.wikipedia.org/wiki/Freifunk) is a communty-driven radio network in Germany.
They developed the OpenWRT for their needs.

#### prpl Foundation 
[prpl Foundation ](https://prplfoundation.org/) is an attempt to collaborate between network equipment manufactures and network providers to create an OpenWRT based platform and use it instead of unknown and unsecure routers firmware.

### Site constructors
MySpace was probably the first popular personal websites hosting. But all users made their own design that sometimes looks terrible.
It's great that all peoples pages on Facebook looks the same. Even given a very bad UI on FB it simplifies navigation.
Yurt must provide some advanced website constructor. Without it peoples just will use something different that Yurt and the whole idea won't work.

* https://myspace.com/
* https://neocities.org/
* https://narod.ru/
* https://wix.com/

### Software
#### WordPress
WordPress is a blog engine and most websites in web are running on WordPress.
It's a very bad software, written in PHP, heavy, has a lot of security vulnarabilities and they always changing it so one day it just become unusable.
WP uses a database but for Yurt we'll try to avoid it to keep size minimal.
Yurt Blog may store posts just in raw RSS to make it simpler to generate RSS feed. The same RSS may be fetched by AJAX and then converted to readabe HTML.
I.e. from UI respective Yurt Blog can be just an in-browser RSS reader.  
BTW WordPress provides RSS feed but for example you can't read it from another site becasue is [blocked by CORS](https://core.trac.wordpress.org/ticket/50441).

#### NextCloud
NextCloud is a self hosted "cloud" solution i.e. online disk like Google Phostos and Google Disk.
You cun upload files like photos and see them from browser or mobile app.  
They are written in PHP which is too heavy for most routers. UI is also not perfect. API is problematic too.

### Why you no host? Because it's hard to configure. Ready to use self-hosting solutions
[Yunohost](https://yunohost.org/) (sounds like "Why you no host?") is an operation system that you can install to Raspberry Pi and use many apps like Mail or RSS reader from a single dashboard. The dashboard provides SSO authorization so you can open any app without being asked for a password.
App are well known existing solutions: RoundCube for Email, Wordpress for Blog etc.
It's a cool idea but it's too heavy for most routers and Yurt must be simpler and more well integrated.

[SandStorm](https://sandstorm.io/) has better integrated apps with a good [secure sandbox model](https://sandstorm.io/how-it-works) based on Linux containers and probably Yurt must be just an app in sandstorm. But it also too heavy for a regular routers and doesn't have a social component.  

There is a lot of similar projects that provide a ready to use self-host solutions.  
See [Awesome Selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted#self-hosting-solutions)

### Devices

Hosting type  | CPU cores | RAM   | Disk  |  OS
--------------|-----------|-------|-------|-----
VPC           | 2         | 16GB  | 512GB | Linux
PC            | 4         | 16GB  | 1TB   | Most of them use Windows for games, in USA MacOS is also popular. We may use Docker. Important to have a tray icon.
Browser on PC | 1         | 2GB   | 50MB  | Chrome workers. Open tab, install app or extension
Laptop        | 2         | 8GB   | 200GB | Windows
TV/TV box     | 2         | 4GB   | 8GB   | AndroidTV. We may use Termux
Phone         | 2         | 8GB   | 128GB | Android. We may use Termux
Raspberry Pi  | 1         | 8GB   | 8GB   | Debian
Router        | 0.5       | 128MB | 16MB  | OpenWRT, Linksys Linux
STM32         | 0.1       | 2MB   | 4MB   |


#### Raspberry Pi: a single board computer
Raspberry Pi is an ARM based single board computer that doesn't have a fan and energy effective. 
Currently a lot of DYI projects uses Pi. It's not so fast as a usual PC but faster than routers.  
You can install a Debian with Python, PHP or Node.JS. So basically every today's sowftware maybe slowly but can be runned on Pi.

Most known project is [Pi-hole](https://pi-hole.net/) Ad Blocking proxy.
Mozilla WebThings is Python based and also targeted to be runned on Pi.

Yurt must support Pi but since everybody in the World can't buy it we shouldn't be targetted to it as main platform.

#### NAS
Network Attached Storage (NAS) is a small server with a lot of disk space that you can install at home. Used as a family shared disk to store photos and videos.
Most popular NAS is Synology that has its own OS called [Disk Station Manager](https://www.synology.com/dsm).
It has a lot of cool features but not intended to become a social network. 
Also NAS devices aren't cheap, so we can't tell everybody in the world to buy them to run Yurt.
Main feature of NAS is a stack of disks: previously you needed a lot of disk to have at least a terabyte in RAID to survive after a disk failure.

But today you can buy a very cheap disk with few terabytes and just connect via USB to a usual router.
NAS has more advanced CPU but just for storing files even a router will be enough. Instead of RAID Yurt may backup data to your friend's 
So I believe NAS devices will be slowly replaced with advanced routers in feature. For example with Turris Omnia.

#### Turris Omnia: Router that can be a small server
[Turris Omnia](https://www.turris.com/en/omnia/overview/) is a most powerful router with a fast CPU that can be used as a NAS.
It uses OpenWRT and you can easily install other apps like NextCloud.
This router is a first attemt to make a special device for a self hosting: it support LXC containers out of the box and regular users may install a lot of things with just a single click.
A similar router with fast CPU and OpenWRT is the [GL.net Brume](https://www.gl-inet.com/products/gl-mv1000/) but it doesn't have such focus on self hosting.


## Email
EMail is a corner stone of web and it's important to give users and ability to send and receive them. You may not have anything except of email.
A good news is that EMail is already non-centralized. But it's too hard to use and especially hard to configure.
But most users for personal needs using silos: GMail, Hotmail, Yahoo, Yandex, iCloud. They have good anti spam filters but they're selling their users. Most users using http to check mail.
Others using corporate email from their job or universities. They are mostly use MUA (Outlook, Thunderbird) but sometimes corporate email is based on silos (Microsoft Office 365).
Small amount of regular users using email from their internet provider (GMX) because they already have it.
Advanced users buys paid email services: Proton Mail, FastMail, Zoho.

Most emails of regular users are just simply notifications and marketing.
Emails are very important for privacy. If you read someone's email you know what they buy, what websites they visit, what happens in their life.
If email hacked then you can reset passwords on all websites.

We must provide at least ability to receive email. This will already cover 98% of usage.
Simplest SMTP server even without TLS will work perfectly.
But how to read received mails?
The simplest way to read them from MUA may download raw eml files (e.g. via sftp) and read it as from a local folder.
Or we may add a POP server. But it may be better to use lightweight JMAP but maybe we even can change it slightly to use JSON-RPC.

