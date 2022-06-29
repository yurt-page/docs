# Yurt Page: your own homepage website for free and for freedom
<details>
<summary>Intro: What is Yurt Page</summary>

Yurt is a small house that is easy to construct.

<img alt="Yurt near Issyk-Kul lake" width="320px" data-canonical-src="https://upload.wikimedia.org/wikipedia/commons/4/4f/YurtIssykFamily.jpg" src="https://camo.githubusercontent.com/69dd1b0c82aae39cf6322bde1384952e3fc7c23bdac2e15967ea794adf7eefea/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f342f34662f59757274497373796b46616d696c792e6a7067"/>

The YurtPage is a small homepage that all people can deploy on their own devices like router, Raspberry Pi, PC or even TV.
So you don't need to pay for hosting.
The main goal is to make a self hosted website as cheap as possible and typical usage is to have a closed family storage of photos or a small blog.

If you have friends with a YurtPage then your data will be encrypted and stored on their devices and this gives you a backup for free.
So the bigger your social network the better is for everybody.
This architecture improves privacy but also makes the internet more distributed and stable.
</details>

## Idealogy

* Old Web: peoples just readers of content on sites: news, books, portals like Yahoo or MSN.
* [Web2.0](https://en.wikipedia.org/wiki/Web_2.0): peoples now can create their own content and interact with each others: Wiki, YouTube, Facebook.
* [Web3](https://en.wikipedia.org/wiki/Web3): "decentralized" still nobody knows what it is but all talking about BlockChain, metaverse, NFT and other buzzwords.

> I don’t know what Web3 would be based on, but Web4 would be based on HTML and cgi-bin.
> — [Albert Einstein](https://twitter.com/marinintim/status/1471480630445813760)

And that's exactly what Yurt uses :) That's esseintal technologies that may work on a smallest devices.

Basically for the Yurt the terminology is not applied at all.
The main goal is to make a cheap web. Ideally just for free.
So small businesses can create a cheap site to sell their products without needing to pay to marketplaces.
So users may have cheap photos storage: just connect an SSD disk to your router.
So that authors can create and sell their content without needing to share money with platforms because their followers are seeding their content.


## Problems

Even today anybody can create its own site: buy a hosting for about 5$ per month, and also you have to buy some domain, then install WordPress blog engine and configure it.
But nobody will ever visit your site. Only occasional visits from Google search.
The problems are solved by social network: you see everything that your friends posted in a single place. Domains not needed. And that's for free.

Everybody won't buy a hosting. But everybody has a WiFi router or a friend with router. And we may host websites there.
Routers are very limited: typical memory from 4 to 16Mb, RAM from 32 to 128Mb, CPU from 400MHz to 800MHz. But personal sites shouldn't be so loaded: normally people has about [150 stable relationships](https://en.wikipedia.org/wiki/Dunbar%27s_number).

Another problem is connectivity. The [pagekite](https://pagekite.net/home/), [CloudFlare](https://www.cloudflare.com/products/tunnel/), [localhost.run](https://localhost.run/), ngrok.

Problems:
1. Not everybody has a router. But almost all has a friend or friend of friend with a router. For sure  We may store credentials on central server.
2. Router can be 
   1. broken: your data is lost. We must back up as much as possible but the decryption key must be stored on a central server.
   2. stolen: your data will be lost but the thrift can also read it. We can keep the decryption key in memory so on reboot it will be lost.
   3. hacked: ...we fucked up here. But! We may do many things as possible to minimise impact: for delete files only some long period (including backup files). 
4. 

## Similar projects or what do we have today
### Movements
#### IndieWeb
[IndieWeb](https://indieweb.org/) is a movement to leave social networks (they call them Silos) and use personal sites.
They're working on creation of easy to use small website engines, technologies and standards to simplify websites to interact with each others.
For example [WebMention](https://indieweb.org/Webmention) protocol allows to easily see when someone makes repost from your site.

* https://indieweb.org/
* https://github.com/pfefferle/awesome-indieweb

Yurt is not related to IndieWeb because ideologically is different (we are fine with some centralization) and almost nothing can't be reused from technology stack. But we'll try to align with this movement.

[unhosted web apps](http://unhosted.org/) also is a good resource

#### Freifunk
[Freifunk](https://en.wikipedia.org/wiki/Freifunk) is a community-driven radio network in Germany.
They developed the OpenWRT for their needs.

#### prpl Foundation 
[prpl Foundation ](https://prplfoundation.org/) is an attempt to collaborate between network equipment manufactures and network providers to create an OpenWrt based platform and use it instead of unknown and unsecure routers firmware.

### Site constructors
MySpace was probably the first popular personal websites hosting. But all users made their own design that sometimes looks terrible.
It's great that all peoples pages on Facebook looks the same. Even given a very bad UI on FB it simplifies navigation.
Yurt must provide some advanced website constructor. Without it peoples just will use something different that Yurt and the whole idea won't work.

* https://myspace.com/
* https://neocities.org/
* https://wix.com/
* https://narod.ru/

#### Small Web and their Site.JS 
Small Web https://small-tech.org/about/

### Software
#### WordPress
WordPress is a blog engine and most websites in web are running on WordPress.
It's a very bad software, written in PHP, heavy, has a lot of security vulnerabilities and they always changing it so one day it just becomes unusable.
WP uses a database but for Yurt we'll try to avoid it to keep size minimal.
Yurt Blog may store posts just in raw RSS to make it simpler to generate RSS feed. The same RSS may be fetched by AJAX and then converted to readable HTML.
I.e. from UI respective Yurt Blog can be just an in-browser RSS reader.  
BTW WordPress provides RSS feed but for example you can't read it from another site because is [blocked by CORS](https://core.trac.wordpress.org/ticket/50441).

#### NextCloud
NextCloud is a self-hosted "cloud" solution i.e. online disk like Google Photos and Google Disk.
You cun upload files like photos and see them from browser or mobile app.  
They are written in PHP which is too heavy for most routers. UI is also not perfect. API is problematic too.

### Why you no host? Because it's hard to configure. Ready to use self-hosting solutions
[Yunohost](https://yunohost.org/) (sounds like "Why you no host?") is an operating system that you can install to Raspberry Pi and use many apps like Mail or RSS reader from a single dashboard. The dashboard provides SSO authorization so you can open any app without being asked for a password.
App are well known existing solutions: RoundCube for Email, Wordpress for Blog etc.
It's a cool idea, but it's too heavy for most routers and Yurt must be simpler and more well integrated.

[SandStorm](https://sandstorm.io/) has better integrated apps with a good [secure sandbox model](https://sandstorm.io/how-it-works) based on Linux containers and probably Yurt must be just an app in sandstorm. But it also too heavy for a regular routers and doesn't have a social component.  

There is a lot of similar projects that provide a ready to use self-host solutions.  
See [Awesome Selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted#self-hosting-solutions), [Alternative Internet](https://github.com/redecentralize/alternative-internet) and [Awesome Piracy](https://github.com/Igglybuff/awesome-piracy)

### Devices

Hosting type  | CPU cores | RAM   | Disk  |  OS
--------------|-----------|-------|-------|-----
VPC           | 2         | 16GB  | 512GB | Linux
PC            | 4         | 16GB  | 1TB   | Most of them use Windows for games, in USA MacOS is also popular. We may use Docker. Important to have a tray icon.
Browser on PC | 1         | 2GB   | 50MB  | Chrome workers. Open tab, install app or extension
Laptop        | 2         | 8GB   | 200GB | Windows
TV/TV box     | 2         | 4GB   | 8GB   | AndroidTV. We may use Termux
Phone         | 2         | 8GB   | 128GB | Android. We may use Termux
NAS           | 1         | 8GB   | 2TB   | Proprietary Linux (Disk Station), TrueNAS, Docker
Raspberry Pi  | 1         | 8GB   | 8GB   | Debian
Router        | 0.5       | 128MB | 16MB  | OpenWRT, Linksys Linux
STM32         | 0.1       | 2MB   | 4MB   | Tasmota


#### Raspberry Pi: a single board computer
Raspberry Pi is an ARM based single board computer that doesn't have a fan and energy effective. 
Currently a lot of DYI projects uses Pi. It's not so fast as a usual PC but faster than routers.  
You can install a Debian with Python, PHP or Node.JS. So basically every today's software maybe slowly but can be run on Pi.

Most known project is [Pi-hole](https://pi-hole.net/) Ad Blocking proxy.
Mozilla WebThings is Python based and also targeted to be run on Pi.

Yurt must support Pi but since everybody in the World can't buy it we shouldn't be targeted to it as main platform.

#### NAS
Network Attached Storage (NAS) is a small server with a lot of disk space that you can install at home. Used as a family shared disk to store photos and videos.
Most popular NAS is Synology that has its own OS called [Disk Station Manager](https://www.synology.com/dsm).
It has a lot of cool features but not intended to become a social network. 
Also NAS devices aren't cheap, so we can't tell everybody in the world to buy them to run Yurt.
Main feature of NAS is a stack of disks: previously you needed a lot of disk to have at least a terabyte in RAID to survive after a disk failure.

But today you can buy a very cheap disk with few terabytes and just connect via USB to a usual router.
NAS has more advanced CPU but just for storing files even a router will be enough. Instead of RAID Yurt may back up data to your friend's 
So I believe NAS devices will be slowly replaced with advanced routers in feature. For example with Turris Omnia.

#### Turris Omnia: Router that can be a small server
[Turris Omnia](https://www.turris.com/en/omnia/overview/) is a most powerful router with a fast CPU that can be used as a NAS.
It uses OpenWRT and you can easily install other apps like NextCloud.
This router is a first attempt to make a special device for a self-hosting: it supports LXC containers out of the box and regular users may install a lot of things with just a single click.
A similar router with fast CPU and OpenWRT is the [GL.net Brume](https://www.gl-inet.com/products/gl-mv1000/) but it doesn't have such focus on self-hosting.


## Email
EMail is a corner stone of web, and it's important to give users and ability to send and receive them. You may not have anything except of email.
Good news is that EMail is already non-centralized. But it's too hard to use and especially hard to configure.
But most users for personal needs using silos: GMail, Hotmail, Yahoo, Yandex, iCloud. They have good anti-spam filters, but they're selling their users. Most users using http to check mail.
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

## Blog
See [yurt-blog](https://github.com/yurt-page/yurt-blog) engine

* RSS must be supported. Only it gives real freedom for readers. In fact only RSS will be enough to make life better for most peoples.
* The blog itself may be just an online RSS reader. I.e. you can read your own blog the same as any other.
* Multiple authors aren't necessary. We may have a very simple access list model.
* Friendly SEO is very wanted but not so important than everything else. I.e. not generate of pure HTML to be indexed. We may instead create some aggregator/proxy or maje our own "blog search" as Yandex.Blogs.
* Comments must be developed even better than posts: discussions are the main focus. Comments on habr.com are much valuable than post.
* But for some posts comments may be just disabled like in Telegram Channels. Such posts must have a different type like Note.
* So we must support different types of posts: articles (translatable and searchable), notes (not searchable), gists (not published in feed but searchable) etc. 
* Stats must be as good as possible (countries, unique readers, read time etc.) but in the same time we must value users privacy (do not use or leak third party data). Otherwise, users may start to use Google Analytics or other even worst spying systems. But some websites like e-commerce for marketing still needs more stats. We are fine to create own tracking system (at least we are not evil yet).
* Cross posting is very important. We must allow publishing to Twitter, FB, anything else.
* We must also be friendly for cross posting and support OData.
* Subscribe via email will be very nice. XMPP/Web/Telegram push.
* To minimize space and optimize speed we may store posts directly in RSS but each post separately. We are free to extend RSS with our elements like comments.
* Support for git/markdown static generators. We may create a plugin for Jekyl/Hugo.
* Maybe we can add a versioning and send only diffs on editing.
* Very basic WYSIWYG editor and use Markdown. But on saving convert MD to HTML/RSS.
* For API we may try to use AtomPub or even use raw WebDAV PUT.
* We must gzip post content on client before sending. Thus, we'll save resources on router.
* Spam Protection is the hardest thing to do


https://github.com/LukeSmithxyz/lb

## HTTP Web Servers
The main target devices for Yurt are routers with OpenWRT that uses uhttpd, other routers that uses LigHttpd, AndroidTV devices that may use Termux+Busybox HTTPD or LigHttpd or even some specialized Android app for the Yurt.
See [Web Servers](webservers.md)
