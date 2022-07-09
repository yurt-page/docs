# Similar projects or what do we have today
## Movements
### IndieWeb
[IndieWeb](https://indieweb.org/) is a movement to leave social networks (they call them Silos) and use personal sites.
They're working on creation of easy to use small website engines, technologies and standards to simplify websites to interact with each others.
For example [WebMention](https://indieweb.org/Webmention) protocol allows to easily see when someone makes repost from your site.

* https://indieweb.org/
* https://github.com/pfefferle/awesome-indieweb

Yurt is not related to IndieWeb because ideologically is different (we are fine with some centralization) and almost nothing can't be reused from technology stack. But we'll try to align with this movement.

[unhosted web apps](http://unhosted.org/) also is a good resource

### Freifunk
[Freifunk](https://en.wikipedia.org/wiki/Freifunk) is a community-driven radio network in Germany.
They developed the OpenWRT for their needs.

### prpl Foundation
[prpl Foundation ](https://prplfoundation.org/) is an attempt to collaborate between network equipment manufactures and network providers to create an OpenWrt based platform and use it instead of unknown and unsecure routers firmware.

## Site constructors
MySpace was probably the first popular personal websites hosting. But all users made their own design that sometimes looks terrible.
It's great that all peoples pages on Facebook looks the same. Even given a very bad UI on FB it simplifies navigation.
Yurt must provide some advanced website constructor. Without it peoples just will use something different that Yurt and the whole idea won't work.

* https://myspace.com/
* https://neocities.org/
* https://wix.com/
* https://narod.ru/

### Small Web and their Site.JS
Small 0Web https://small-tech.org/about/ is a site constructor with many features.

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

## Why you no host? Because it's hard to configure. Ready to use self-hosting solutions
[Yunohost](https://yunohost.org/) (sounds like "Why you no host?") is an operating system that you can install to Raspberry Pi and use many apps like Mail or RSS reader from a single dashboard. The dashboard provides SSO authorization so you can open any app without being asked for a password.
App are well known existing solutions: RoundCube for Email, Wordpress for Blog etc.
It's a cool idea, but it's too heavy for most routers and Yurt must be simpler and more well integrated.

[SandStorm](https://sandstorm.io/) has better integrated apps with a good [secure sandbox model](https://sandstorm.io/how-it-works) based on Linux containers and probably Yurt must be just an app in sandstorm. But it also too heavy for a regular routers and doesn't have a social component.

There is a lot of similar projects that provide a ready to use self-host solutions.  
See [Awesome Selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted#self-hosting-solutions), [Alternative Internet](https://github.com/redecentralize/alternative-internet) and [Awesome Piracy](https://github.com/Igglybuff/awesome-piracy)
