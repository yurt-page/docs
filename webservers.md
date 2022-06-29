# WebServer for small websiyes
The main target devices for Yurt are routers with OpenWRT that uses uhttpd, other routers that uses LigHttpd, AndroidTV devices that may use Termux+Busybox HTTPD or LigHttpd or even some specialized Android app for the Yurt.

For many regular users it may be too complicated to install a web server to run a yurt on their desktop computer. But this is an extremely important to support because desktop PC has a lot of storage and a really good CPU. This will be really needed for photos backup.
In fact, we have few options by implementation difficulty level:
1. Use an existing Web Servers and provide instructions how to configure Yurt.
2. Provide an installer that will set up the Yurt with one of the existing web server.
3. Create a Yurt as a separate program with an embedded webserver. This will give more independence and an ability to move faster but this also means that Yurt must always provide updates especially with security fixes.

We must start with the first option as an easier to begin with. Most target users of Yurt using Windows, macOS is too expensive for most peoples and Linux users... they know better how to install and use Yurt.

The baseline for Yurt is a BusyBox HTTPD because this is the most lightweight and widely deployed web server. Almost all Ubuntu have it pre-installed.


Windows:
* [MicroSoft IIS](https://www.iis.net/) relatively easy to install and has some GUI configuration. Supports WebDAV. May be challenging to use it.
* [XAMP](https://www.apachefriends.org/en/index.html) Apache + MariaDB + PHP and hase some Control Panel GUI. Easy to install, we may skip everything except of Apache, but even it is too heavy.
* [Open Server Panel](https://ospanel.io/) More advanced installer. Overkill but it supports Nginx. Nginx or any other webservers are too heavy and harder to configure.
* Tomcat: needs Java, slow, but (potentially) safer. Maybe we may create some GUI based on Jetty.
* [BusyBox W32](https://frippery.org/busybox/) may be good solution for us, but it doesn't have any GUI.
* [Miranda IM + HTTPServer plugin](https://github.com/miranda-ng/miranda-ng/tree/master/plugins/HTTPServer) surprisingly but this is one of the most easy to use solution. It even supports UPNP port forwarding (but no NAT-PMP/PCP). It even has some default website template that allows to see directory listing. It doesn't support CGI and needs to be revisited and improved. One good thing about it is that many users remember Miranda. It is also very lightweight and can be used to set up a Jabber/XMPP account.
* [200 OK  Server Chrome Plugin](https://chrome.google.com/webstore/detail/web-server-for-chrome/ofhbbkphhbklhfoeikjpcbhemlocgigb) a simple webserver that is very easy to install for experienced users. No CGI but has UPNP port forwarding (but no NAT-PMP/PCP). Maybe this is the only option for Chromebook.
* [Fenix Web Server](http://fenixwebserver.com/) looks good and supports MacOS. We must at least try to support it.
* Many shareware programs like [HFS](https://en.wikipedia.org/wiki/HTTP_File_Server). It's simply not safe, and they anyway won't support CGI.




https://www.npmjs.com/package/http-server NodeJS static HTTP server

Pre-historic:
* [ghttpd](http://gaztek.sourceforge.net/ghttpd/) an old server from 1999, had some vulnarabilities
* [micro_httpd](https://acme.com/software/micro_httpd/), [mini_httpd](https://acme.com/software/mini_httpd/) and [thttpd](https://acme.com/software/thttpd/) from the same author. Still are available in repos.

Modern but static files only:
* https://www.nongnu.org/mini-httpd/
* https://man.openbsd.org/httpd.8


* [mongoose](https://github.com/cesanta/mongoose) a networking library for embedded devices. http://brokenbrake.biz/2010/08/24/webserver-mongoose
* [MIDAS Web Server](https://midas.triumf.ca/MidasWiki/index.php/Mhttpd) mhttpd based on Mongoose

Mature but not well known:
* yaws
* cherokee

[How to easily start a webserver in any folder?](https://askubuntu.com/questions/377389/how-to-easily-start-a-webserver-in-any-folder/1256550#1256550)

File sharing:
* https://github.com/ltworf/weborf
* https://wiki.gnome.org/phodav
* https://gitlab.gnome.org/GNOME/gnome-user-share
* https://help.gnome.org/users/gnome-user-share/stable/gnome-user-share.html#:~:text=gnome%2Duser%2Dshare%20uses%20a,computer%20via%20Bluetooth%20via%20ObexPush.
