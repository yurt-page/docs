# Yurt Page: own website for everybody on Earth and other planets

* Web1.0: peoples just readers of others sites: news, books
* Web2.0: peoples now can create their own content and interact with each others: Wiki, YouTybe, Facebook
* Web3.0: nobody knows but all talking about BlockChain, AI, VR and other buzzwords.
* ....
* This will be a Web100500

## Similar projects or what do we have today
### Movements
[IndieWeb](https://indieweb.org/) is a movement to leave social networks (they call them Silos) and use personal sites.
They're working on creation of easy to use small website engines, technologies and standards to simplify websites to interact with each others.
For example [WebMention](https://indieweb.org/Webmention) protocol allows to easily see when someone makes repost from your site.

* https://indieweb.org/
* https://github.com/pfefferle/awesome-indieweb

Yurt is not related to IndieWeb because ideologically is different (we are fine with some centralization) and almost nothing can't be reused from technology stack. But we'll try to align with this movement.

### Site constructors
MySpace was probably the first popular personal websites hosting. But all users made their own design that sometimes looks terrible.
It's great that all peoples pages on Facebook looks the same. Even given a very bad UI on FB it simplifies navigation.
Yurt must provide some advanced website constructor. Without it peoples just will use something different that Yurt and the whole idea won't work.

* https://myspace.com/
* https://neocities.org/
* https://narod.ru/
* https://wix.com/

### NAS
Network Attached Storage (NAS) is a small server with a lot of disk space that you can install at home. Used as a family shared disk to store photos and videos.
Most popular NAS is Synology that has its own OS called [Disk Station Manager](https://www.synology.com/dsm).
It has a lot of cool features but not intended to become a social network. 
Also NAS devices aren't cheap, so we can't tell everybody in the world to buy them to run Yurt.
But today you can buy a very cheap disk with few terabytes and just connect via USB to a usual router.
NAS has more advanced CPU but just for storing files even a router will be enough.
So I believe NAS devices will be slowly replaced with advanced routers in feature. For example with Turris Omnia.

### Turris Omnia: Router that can be a small server
[Turris Omnia](https://www.turris.com/en/omnia/overview/) is a most powerful router with a fast CPU that can be used as a NAS.
It uses OpenWRT and you can easily install other apps like NextCloud.

### NextCloud
NextCloud (OwnCloud) is a self hosted cloud solution. You cun upload files like photos and see them from browser or mobile app.
They are written in PHP which is too heavy for most routers. UI is also not perfect. You can extend with some plugins.

### Why you no host? Because it's hard to configure
[Yunohost](https://yunohost.org/) (sounds like "Why you no host?") is an operation system that you can install to Raspberry Pi and use many apps like Mail or RSS reader from a single dashboard.
It's too heavy for routers and Yurt must be simpler and more well integrated.
There is a of other similar projects that tries to provide a ready to use solution.
[SandStorm](https://sandstorm.io/) is more simple but better integrated.
[Mail-in-a-Box](https://mailinabox.email/) is a preconfigured tools for email.

## Email
EMail is a corner stone of web and it's important to give users and ability to send and receive them. You may not have anything except of email.
A good news is that EMail is already non-centralized. But it's too hard to use and especially hard to configure.
But most users for personal needs using silos: GMail, Hotmail, Yahoo, Yandex, iCloud. They have good anti spam filters but they're selling their users. Most users using http to check mail.
Others using corporate email from their job or universities. They are mostly use MUA (Outlook, Thunderbird) but sometimes corporate email is based on silos (Office365).
Small amount of regular users using email from their internet provider (GMX) because they already have it.
Advanced users buys paid email services: Proton Mail, FastMail, Zoho.

Most emails of regular users are just simply notifications and marketing.
Emails are very important for privacy. If you read someone's email you know what they buy, what websites they visit, what happens in their life.
If email hacked then you can reset passwords on all websites.

We must provide at least ability to receive email. This will already cover 98% of usage.
Simplest SMTP server even without TLS will work perfectly.
But how to read received mails?
The simplest way to read them from MUA may download raw eml files (e.g. via sftp) and read it as from a local folder.

