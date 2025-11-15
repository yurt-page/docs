# WebServer for small websites
> [!NOTE]
> [project tasks](https://github.com/orgs/yurt-page/projects/14)

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
* [XAMP](https://apachefriends.org/) Apache + MariaDB + PHP and hase some Control Panel GUI. Easy to install, we may skip everything except of Apache, but still it is too heavy.
* XAMP alternatives https://alternativeto.net/software/xampp/ like https://winginx.com/
* [Open Server Panel](https://ospanel.io/) More advanced installer. Overkill but it supports Nginx. Nginx or any other webservers are too heavy and harder to configure.
* Tomcat: needs Java, slow, but (potentially) safer. Maybe we may create some GUI based on Jetty.
* [BusyBox W32](https://frippery.org/busybox/) may be good solution for us, but it doesn't have any GUI.
* https://www.npmjs.com/package/http-server NodeJS static HTTP server. Not a just ready to use product but still something useful. Some PRs are waiting to be merged since 2016!
* [200 OK  Server Chrome Plugin](https://chrome.google.com/webstore/detail/web-server-for-chrome/ofhbbkphhbklhfoeikjpcbhemlocgigb) a simple webserver that is very easy to install for experienced users. No CGI but has UPNP port forwarding (but no NAT-PMP/PCP). Chrome removed socket api so it doesn't work anymore.
* [Simple Web Server](https://simplewebserver.org/) continuation of the 200 OK Server Chrome Plugin but as a standalone app. Loosed some features like UPnP but looks better. Has some PUT/DELETE support but not full WebDAV. 70mb installer - not so small but it's UI is very advanced. This is probably the most user friendly. But no CGI and generally it's too simple.
* [Fenix Web Server](http://fenixwebserver.com/) just plain static files but has UI and supports MacOS. 9mb installer. It's development looks stalled.
* [HFS2](https://github.com/rejetto/hfs2) written in Delphi for Windows. User-friendly.
* [HFS3](https://github.com/rejetto/hfs) completely rewritten HFS to TypeScript. Looks impressive!
* GNU libmicrohttpd is a small C library that is supposed to make it easy to run an HTTP server as part of another application. 190kb and many dependats. May be used to create a small server. See https://gitlab.com/karlson2k/libmicrohttpd/-/issues/1

Pre-historic, without TLS, abandoned or not well known but still used in wild:
* [ghttpd](http://gaztek.sourceforge.net/ghttpd/) an old server from 1999, had some vulnarabilities
* [micro_httpd](https://acme.com/software/micro_httpd/), [mini_httpd](https://acme.com/software/mini_httpd/) and [thttpd](https://acme.com/software/thttpd/) from the same author. Still are available in repos. The minihttpd is often used as Alpine container.
* [muhttpd](https://sourceforge.net/p/muhttpd/) used in some routers. Had (have?) backdoors.
* [webfs](https://linux.bytesex.org/misc/webfs.html) is old and small server for sharing a folder. Available in all repos, even in homebrew. See docs https://github.com/SalimF/webfs-doc. In Debian a lot of patches https://salsa.debian.org/friki/webfs/-/tree/master/
* [nostromo](https://www.nazgul.ch/dev_nostromo.html)
* https://github.com/nealey/eris HTTP/1.1, CGI, senfile virtual hosting
* https://github.com/troglobit/merecat/ - a tftpd for with Virtual Host support
* https://github.com/emikulic/darkhttpd - a small static webserver from darkstat author
* https://tools.suckless.org/quark/ - a suckless static webserver.
* https://github.com/rofl0r/pyhttpd - a python2 static webserver with suckless design
* https://github.com/gpg/boa - [Boa](https://en.wikipedia.org/wiki/Boa_(web_server)) discontinued

Modern but static files only:
* https://www.nongnu.org/mini-httpd/
* https://man.openbsd.org/httpd.8
* [mongoose](https://github.com/cesanta/mongoose) a networking library for embedded devices. http://brokenbrake.biz/2010/08/24/webserver-mongoose
* [MIDAS Web Server](https://midas.triumf.ca/MidasWiki/index.php/Mhttpd) mhttpd based on Mongoose


Mature but not well known:
* yaws written in Erlang O_o
* cherokee a very old and looks solid but nobody use it and never even heard
* https://github.com/nealey/eris HTTP/1.1 web server with CGI. It is very fast, uses very little memory, and has a tiny codebase. It relies on an external program, such as tcpserver or netcat, to handle networking, and expects to be run once for every connection. eris does simple virtual hosting.

Java
* https://github.com/NanoHttpd/nanohttpd
* https://github.com/theborakompanioni/ngtor Tor hidden service: tunnel and serve

### File sharing
See [Awesome WebDAV](https://github.com/fstanis/awesome-webdav/tree/main?tab=readme-ov-file#standalone).
The list here is mostly repeat it.

* https://github.com/ltworf/weborf a webserver with a Qt GUI to share local files over WebDAV. Has some CGI support (!). Has UPnP port forwarding. The Dav is very basic and doesn't use xml parsing. Maybe it's possible to reuse it for webdav-cgi. Has minimal dependencies and quite small. Linux only. Looks maintained but not actively developed.
* https://wiki.gnome.org/phodav command line tool to share a folder with WebDav. Uses Glib and libsoap. Sources are well structured. Bigger than weborf but should be more stable.
* https://gitlab.gnome.org/GNOME/gnome-user-share Adds to Gnome folder options a tab share local files with WebDAV but it just configures Apache. Looks abandoned but still has a package in repos so can be used just today. But... Apache. See [it's docs](https://help.gnome.org/users/gnome-user-share/stable/gnome-user-share.html)
* "Written in Rust". They all are similar to weborf by functionality but more advanced and fancy
  * https://github.com/svenstaro/miniserve most stars on GitHub
  * https://github.com/sigoden/dufs supports WebDAV
  * https://github.com/thecoshman/http supports WebDAV
  * https://github.com/messense/dav-server-rs library for WebDAV and there are a lot of small webservers based on it  https://github.com/messense/dav-server-rs/network/dependents
* https://github.com/browsefile/backend Written in Go
* https://github.com/filebrowser/filebrowser no webdav but looks good. Written in 
* https://github.com/nitroshare/nitroshare-desktop C++, outdated but has GUI
* https://github.com/mnutt/davros JS, used in Sandstorm by default. It's author is a cool guy.
* https://github.com/mraukhvarger/webfs JS and Java
* https://github.com/stackp/Droopy available from Debian repo




### WebDAV UI
* https://github.com/katomaso/webdave very basic but initial idea of author was to use it for bloging.
* https://github.com/dom111/webdav-js has some bugs and sources complicated.


## As a plugin to other apps
* [Miranda IM + HTTPServer plugin](https://github.com/miranda-ng/miranda-ng/tree/master/plugins/HTTPServer) surprisingly but this is one of the most easy to use solution. It even supports UPNP port forwarding (but no NAT-PMP/PCP). It even has some default website template that allows to see directory listing. It doesn't support CGI and needs to be revisited and improved. One good thing about it is that many users remember Miranda. It is also very lightweight and can be used to set up a Jabber/XMPP account.
* Torrent clients usually have a Web UI. And yes, they have a web server built-in. Deluge and Transmission have their admin UI just in a folder and we can add our own files.
* CUPS Printing daemon is pre-installed on Linux and macOS and basically it's a web server with CGI https://github.com/OpenPrinting/cups/tree/master/cgi-bin This is bad idea to use CUPS server but it may be a good solution to extract a small webserver part from it that can be used separately.

## See also
* [Awesome Webservers](https://github.com/imgarylai/awesome-webservers) - Collection of one-liner static server
* [How to easily start a webserver in any folder?](https://askubuntu.com/questions/377389/how-to-easily-start-a-webserver-in-any-folder/1256550#1256550)

## OpenSSL
The OpenSSL tools have [s_server](https://www.openssl.org/docs/manmaster/man1/openssl-s_client.html) command that can be used as a webserver. You need to create a `server.pem` file with both cert and key and then run  `openssl s_server -accept 4443 -WWW`
Then open in browser https://localhost:4443/index.html 

It won't show the index.html by default so you must specify a file.
Also see https://localhost:4443/stats this is testing page for the TLS params.
Ideally we need just a TLS termination proxy that will redirect to plain http of BusyBox httpd. Maybe we can ask the OpenSSL guys to implement/accept a PR.

Something like that also possible with GnuTLS but it always shows only a stats page:

    gnutls-serv -p 4443 --http  --x509certfile ./server.pem --x509keyfile ./server.pem



## Routers with WebDAV out of the box
* [keenetic](https://help.keenetic.com/hc/ru/articles/360012308540-%D0%9F%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BA-USB-%D0%B4%D0%B8%D1%81%D0%BA%D1%83-%D0%BF%D0%BE-%D0%BF%D1%80%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%BB%D1%83-WebDAV)

## Proxy
So we have different sites and use scenarios on a router:
* An admin site LICI/reFORIS etc. The admin should always work and ideally we shouldn't change any it's settings. They may be broken during an update.
* self-hosting services which can be
  * local only: webdav with media for a TV or for backup. Here TLS is not required. We can use a separate non-standard port like 8080 and most users should be fine.
  * available from public internet but with a limited access e.g webdav with a password, home automation dashboard. We need a TLS.
  * public service e.g. SMTP mail server, blog, site. Again, we need a TLS. We can't use a non-standard port because nobody will know it. Also need for some WAF to protects from DDoS and exploits.
* Just forwarding to a local computer (like NAS) with load balancing, auth and TLS.

So we need some reverse proxy and this is one of the biggest problems.
The reverse proxy can make a TLS termination and then we can try to use a BusyBox httpd which doesn't support the TLS.
We also need a TLS for SMTP/POP (465 port) but the EmailRelay can work with OpenSSL and mbedTLS so it's not critical.
Both uhttpd and Lighttpd also supports TLS but having a dedicated reverse proxy also allows to proxy by SNI e.g. by a domain name.
But also we can remove the TLS support from uhttpd and others to make them lighter.

Technically speaking it's not needed and even make all slower and maybe we can avoid it.
The key problem that it should solve is to listen `0.0.0.0` all interfaces IP and then route incoming traffic to ether local LUCI admin or a public website.
We can make a web/mail server to listen a public IP (if any) but if it's dynamic then we'll need to restart a server.

Maybe this can be handled with iptable e.g. always start on 127.0.0.1:8080 IP but redirect all other public IPs 80 port ot it.

**UPD** yes, this is possible and easy to do just as a regular port forwarding.
The OpenWrt firewall has redirects and we can start lighttp-wan on a `0.0.0.0:2080` and redirect the WAN 80 port to the `192.168.1.1`.
Redirection to localhost `127.0.0.1` didn't worked and just to simplify the 2080 port is used on all interfaces `0.0.0.0`. 
This allows to access the same lighttpd-wan instance directly from local network without the redirecter.
This may be useful if WAN network is down but all local devices may still get access to the webdav. 
CGI scripts will see the remote IP directly so there is no problems as with reverse proxy.
But we can't make a load balancing because the firewall doesn't track connections (or we can?).

https://community.home-assistant.io/t/why-use-reverse-proxy-vs-port-forwarding/101653/2

### Proxies solutions
* [Lighttpd mod_proxy](https://redmine.lighttpd.net/projects/lighttpd/wiki/Mod_proxy) doesn't support a raw TLS for SMTP. But we can PR this.
* Nginx (1mb) supports all but it's too heavy. It is used by [Sandstorm  for SMTP proxy](https://docs.sandstorm.io/en/latest/administering/email/#configure-port-25-the-advanced-way-proxy-smtp)
* haproxy... just to mention. 900kb not that bad.
* BusyBox httpd has some very basic http proxy which looks like more to be used as a forward proxy.
* TinyProxy - a forward proxy without TLS termination but looks like a good place where to add the functionality and it was requested few times. Already has OpenWrt package and developed by related peoples.
* [sslh](https://github.com/yrutschle/sslh) is a DPI miltiplexet when all ports except of 443 are blocked. You can use 443 port for both TLS and SSH the the sslh will split traffic. It can route HTTP and TLS based on SNI. It has an OpenWrt package and quite often used. But it's too big and actually can be reduced ten times.
* [sniproxy](https://github.com/dlundquist/sniproxy) It's only SNI e.g. no TLS termination. Has Ubuntu package. Used by Sandstorm.io.
* https://github.com/Intika-Linux-Proxy/SNI-SSL-Proxy SNI with forwarding to SOCKS5
* https://github.com/0x7a657573/zroxy SNI
* https://github.com/topics/tls-proxy?l=c&o=desc&s=stars manuy others written in C
* https://github.com/mtrojnar/stunnel full TLS termination. Only OpenSSL, code is complicated. Supports Windows.
* https://github.com/varnish/hitch  full TLS termination. 
* https://github.com/vesvault/snif something complicated but looks related. From author of https://vesmail.email/

One possible solution would be to add the TLS proxy functionality into OpenSSL tools.
Since we already have some kind of http server (see above) then by small extending this may become both basic http server and proxy and a highly useful tool for web developers.
This will make the OpenSSL __even bigger__ but from the other side it's already ported to all platforms and often is pre-installed by default.
With these changes almost all devs will have a basic http and proxy server for quick and simple tasks and be used in tutorials. This is not that weird idea.

#### ebpf routing
Basic HTTP and even TLS are not so dificult to parse. 
We can use ebpf to parse right in the kernel level and route to a specific port.
https://github.com/yurt-page/ebpf-web-proxy
