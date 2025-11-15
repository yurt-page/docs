# Similar projects or what do we have today
Ideas are not new and many existing projects working in this direction.
But there are always some difference in implementations,  

## Movements, communities and organizations

### Selfhosted communities and forums
* https://noted.lol/ web site dedicated to selfhosting
* [/r/selfhosted/](https://www.reddit.com/r/selfhosted/) reddit discussions
* [Awesome Selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted) directory of software
* [Self-Hosting Guide](https://github.com/mikeroyal/Self-Hosting-Guide)
* [wikipedia: Self-hosting](https://en.wikipedia.org/wiki/Self-hosting_(web_services)) is also a good source
* [IndieBits](https://forum.indiebits.io/) about tunneling (BoringTunnel, TakingNames.io)
* [Зачем нужен личный сайт в 2023 году](https://habr.com/en/companies/ruvds/articles/717952/)

### FUTO Circles
The [Circles app](https://circles.futo.org/about/) is an open source end to end encrypted social network for a family.
Based on Matrix protocol.

### IndieWeb
[IndieWeb](https://indieweb.org/) is a movement to leave social networks (they call them Silos) and use personal sites.
They're working on creation of easy to use small website engines, technologies and standards to simplify websites to interact with each others.
For example
* [Building blocks](https://indieweb.org/Category:building-blocks) are key design-patterns, technologies, and methods for building and improving your independent website.
* [WebMention](https://indieweb.org/Webmention) protocol allows to easily see when someone makes repost from your site.
* [IndieAuth](https://indieauth.net/) is OAuth extension to login from your domain but difficult to implement.
* Mastodon is twitter like selfhosting service.
* ActivityPub is a protocol to build a social network

See
* https://indieweb.org/
* https://github.com/pfefferle/awesome-indieweb

Yurt is not related to IndieWeb because ideologically is different (we are fine with some centralization) and almost nothing can't be reused from technology stack.
But we'll try to align with this movement.

### Personal data vaults

[Unhosted web apps](http://unhosted.org/) store user data to any server that user choose. E.g. a TODO app that stores tasks to Google Drive or even to you your own storage.
There is a dedicated [remoteStorage](https://remoteStorage.io) protocol that looks like [JSON based WebDAV](https://github.com/remotestorage/remotestorage.js/issues/1093) + OAuth.
Still, for most programs you need a server side with specific API. E.g. for a TODO app send an email with notification.
But anyway quite a lot of apps that are already exists and some of them are even useful and practical like [SuperProductivity](https://app.super-productivity.com/).

It was evolved into [Solid Project](https://solidproject.org/apps) under lead of inventor of web Tim Berns-Lee.
It looks overcomplicated but actively developing and already have some nice apps.

See also [CrossCloud](https://github.com/sandhawke/crosscloud/blob/master/overview.md)

Also interesting article from 2012 (!) [Personal Data Vaults Put You in Control of Your Data Online](https://www.pcworld.com/article/459825/personal_data_vaults_put_you_in_control_of_your_data_online.html) 


### Freifunk
[Freifunk](https://en.wikipedia.org/wiki/Freifunk) is a community-driven radio network in Germany.
They developed the OpenWRT, KadNode DNS and some other projects for their needs.

### Turris
[Turris](https://www.turris.com/) is an OpenWrt based router with powerful CPU that almost completely open source and can be used as a home server.
E.g. you can install NextCloud and other programs with just a click.
This is the closest to the Yurt idea and you can try it today.

### prpl Foundation
[prpl Foundation ](https://prplfoundation.org/) is an attempt to collaborate between network equipment manufactures and network providers to create an OpenWrt based platform and use it instead of unknown and unsecure routers firmware.

### iconet Foundation
The [iconet](https://iconet-foundation.org/) is an attempt to create a responsible social network

### Greenhouse
A lot of interesting and useful projects like:
* https://greenhouse.server.garden/ tunnel
* https://git.sequentialread.com/forest/tuber
* https://sequentialread.com/ author's blog

### Framasoft
A French not-for-profit association https://degooglisons-internet.org/
They created some interesting products like PeerTube.

### MobileMe
[MobileMe](https://en.wikipedia.org/wiki/MobileMe) was a nice service at me.com that was replaced with iCloud.
It allowed to make own website and had WebDAV integration.


## Site constructors
MySpace was probably the first popular personal websites hosting.
But all users made their own design that sometimes looks terrible.
It's great that all peoples pages on Facebook looks the same.
Even given a very bad UI on FB it simplifies navigation.
Yurt must provide some advanced website constructor.
Without it peoples just will use something different that Yurt and the whole idea won't work.

* https://myspace.com/ a previously popular social network where many people had their pages.
* https://neocities.org/ reincarnation of GeoCities free hosting. The goal if exactly the same: make home pages for regular peoples. See [High Volume, Bandwidth Heavy Infrastructure On The Cheap - Kyle Drake](https://www.youtube.com/watch?v=-i6wvix6buI)
* https://wix.com/ the most popular commercial constructor


## Software
### WordPress
WordPress is a blog engine and most websites in web are running on WordPress.
It's a very bad software, written in PHP, heavy, has a lot of security vulnerabilities and they always changing it so one day it just becomes unusable.
WP uses a database but for Yurt we'll try to avoid it to keep size minimal.
Yurt Blog may store posts just in raw RSS to make it simpler to generate RSS feed. The same RSS may be fetched by AJAX and then converted to readable HTML.
I.e. from UI respective Yurt Blog can be just an in-browser RSS reader.  
BTW WordPress provides RSS feed but for example you can't read it from another site because is [blocked by CORS](https://core.trac.wordpress.org/ticket/50441).

### NextCloud
NextCloud is a self-hosted "cloud" solution i.e. online disk like Google Photos and Google Disk.
You cun upload files like photos and see them from browser or mobile app.  
They are written in PHP which is too heavy for most routers. UI is also not perfect. API is problematic too.
Some older projects like the https://SparkleShare.org ( [GitHub repo](https://github.com/hbons/SparkleShare)) are a good alternative.


## Self-hosting Solutions
Installing and configuring own server is difficult. So you can use some special OS (usually for RaspberryPI or VPS) that already preconfigured and usually gives the following features:
* Web installer with a setup wizard
* Web UI to configure system settings
* App store where you can install something like NextCloud, mail server, RSS reader, file sharing just in one click.
* Dashboard with application icons
* Users management
* Automatic LetsEncrypt TLS certificate issuing
* DDNS or free subdomain. Also for each app is usually used a separate subdomain.
* Backups and snapshots

Usually developers of the projects also selling microcomputers with already installed OS so you can just plug into a router and start using.


### FreedomBox
[FreedomBox](https://freedombox.org/) is a Debian with some Web UI dashboard written in Python+Django. It's the oldest solution and uses traditional software and based by ideology.
It's made by a serious peoples and this is more like a proven solution than a research project.
Original idea was to sell a small server in a small box e.g. what we call today RaspberryPi but at that time it was a new specifically developed device.
See interesting talk [Eben Moglen: "FreedomBox Turns Ten"](https://www.youtube.com/watch?v=2U8PyukPyGE) about its philosophy.

The web panel is written in Python and Django. It lacks of usability e.g. they don't provide a DDNS out of the box.


### Yunohost
[Yunohost](https://yunohost.org/) (sounds like "Why you no host?") is more popular and Docker based solution.
The dashboard provides SSO authorization so you can open any app without being asked for a password.
App are mostly well known: RoundCube for Email, Wordpress for Blog etc.

### 0Web
Small 0Web https://small-tech.org/about/ is a site constructor with many features. [Site.JS](https://sitejs.org/) 
It's based on Node.JS and idea is to make an easy to setup website.
They have a good ideology manifest.

### Root project
https://therootcompany.com personal cloud. Again in Node.JS.
It's in development but some components like tunnel and JS crypto libraries are working and even used by other solutions.
Here is some description https://git.rootprojects.org/root/meta
It's author https://github.com/coolaj86 makes a lot of useful things for self-hosting a libre movement and a lot of video lectures.


## Many other interesting
There is a lot of similar projects that provide a ready to use self-host solutions.
Some noteworthy:

* [Tipi](https://github.com/meienberger/runtipi) a docker based with nice UI
* [umbrel.com](https://umbrel.com/) similar to Tipi, nice and shiny but not FOSS
* [Cloudron](https://cloudron.io/) nice but not FOSS
* [SandStorm](https://sandstorm.io/) has an advanced [secure sandbox model](https://sandstorm.io/how-it-works) based on Linux containers. The project is almost dead.
* [SynCloud](https://syncloud.org/) https://github.com/syncloud similar to FreedomBox but has DDNS and written in Golang.
* [KubeSail](https://kubesail.com/homepage) is a mini PC for homelab hosting.
* TheHelm.com was another one project sold a ready to use and configured microservers. It's closed now, but you may read [Helm Is a Private Home Email Server Anyone Can Use](https://theintercept.com/2019/04/30/helm-email-server/) or find videos.


You can find even more here:
* [Awesome Selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted#self-hosting-solutions),
* [Alternative Internet](https://github.com/redecentralize/alternative-internet)
* [Awesome Piracy: Dashboards](https://github.com/Igglybuff/awesome-piracy#dashboards-and-homepages)


Probably the Yurt project can implement as part of some of them.
But they are all too heavy for a regular routers and doesn't have a social component.

In fact the Yurt should be the same Self-hosting Solution but with a few differences:
1. Focus on small size and power efficiency.
   * So any PHP, NodeJS, Golang, Python based solution won't work for us. We need to use what the OpenWrt use e.g. plain C, Lua, Shell and recently Ucode which is JS dialect.
   * Apps that we use should be also small
   * Yeah, and we can't use Docker
2. Instead of a nice looking or good UX we have to use "simple" e.g. ugly but more error-prone design. For example use text instead of icons, don't use animation.
   * This is a very bad rule that we have to break. If users see that something looks good they think that internally it also works good (even if that is a slow CGI script)  
   * For most people the main motivation to have own site is to have own design and better customization. Users are curious and want's to enjoy. Maybe some more heavy existing solutions can satisfy such users. 
   * Basically this is the main problem that if solved at least partially can make many peoples happy. Maybe it's possible some attractive minimal but accurate "suckles" design. 
3. Almost all of them have a focus on privacy but for the Yurt it's totally fine to have some degree of centralization and to be more business friendly. E.g. if you wish to use analytic scripts then we weill add this option to you.

## Decentralized protocols
Many of them, good ideas but mostly bad implementations.
* https://willowprotocol.org/ a protocol for peer-to-peer data stores. Fine-grained permissions, a keen approach to privacy, destructive edits, and a dainty bandwidth and memory footprint. See its a good written [Comparison to Other Protocols](https://willowprotocol.org/more/compare/index.html)
* IPFS, FileCoin, Veilid - a torrent like p2p file storages
* Scuttlebutt, Hypercore - chats 
* Tangle Sync
* Earthstar
* Nostr
* EteSync - more similar to Unhosted remote storage.
* https://github.com/peter0x7f/DecentralizedTransferProtocol decentralize user data storage making running a web app less expensive, while also insuring user privacy.
