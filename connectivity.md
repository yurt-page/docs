# Expose web server without a public IP address




Connectivity is a problem even bigger than hosting devices.
Many consumer grade devices doesn't have a static IP so that nobody from internet can't connect directly.
Some providers allows to buy a static IP but it not so cheap. And again, the main goal is to make users not to pay anything.
Many ISPs gives a dynamic IP that is chaning from time to time. So you can't register a DNS record because when it will be changed you may not notice.

If your web server doesn't have a public or dynamic IP address e.g. behind NAT then it can't be accessd from internet.
So you need some public proxy that your sevrer will connect to and the proxy will redirect incoming request to your server.
Usually such proxies also gives you an unique subdomain and can enable HTTPS for you.

Here many problems arise:
1. The proxy has bandwith limits
2. HTTPS termination on proxy means that the proxy can read traffic
3. Subdomains may set a cookie to a parent domain
4. The biggest problem is to avoid botnets and fishing sites.

Tecnically speaking the tunnel between server and proxy is not so easy to implement.
It must be not a VPN but also simple SOCKS is not good here. So such tunneling services uses protocols like port forward over SSH or specialized multiplexing protocols.

## SSH tunnel
Dropbear supports the feature. But they are slow. OpenWrt has a sshtunnel package to reconnect but it depends on OpenSSH client.

## TCP tunnels providers
Here is a list (hope not complete) of such proxies services:
* [pagekite](https://pagekite.net/home/) Uses HTTP proxy like protocol with an additional encryption. One of the oldest. Has openwrt packages. Allows to deploy own instance (frontend). See [PageKite intro](https://www.youtube.com/watch?v=SRhK05KjxYA) and [Accessing your Mbed device from anywhere using Pagekite How to create a Mbed library for Pagekite](https://www.youtube.com/watch?v=23BS7kdQMzw)
* [CloudFlare](https://www.cloudflare.com/products/tunnel/)
* [localhost.run](https://localhost.run/) uses regular SSH tunnels. Here is some details about internals https://medium.com/localhost-run/localhost-run-the-origin-story-5aeaf5692dee
* [ngrok](https://ngrok.com/) one of the most popular. Needs for own client. First version was published on GitHub but seconds version is closed. Written in Go, quite heavy for routers.
* https://github.com/sleirsgoevy/ngrok-free ngrok v2 clone (reverse engineered)
* https://github.com/azimjohn/jprq ngrok alternative using WebSockets
* https://www.cloudflare.com/products/tunnel/ CloudFlare tunnel (Argo)
* https://localxpose.io/ very powerful tunnels and reverse proxy with many options and also a market
* https://webhookrelay.com/
* https://portmap.io/
* https://packetriot.com/
* https://vercel.com/ (formerly ZEIT)
* https://www.beame.io/insta-ssl
* https://yaler.net/
* https://openport.io/
* https://burrow.io/
* https://www.ultrahook.com/
* https://github.com/antoniomika/sish An open source serveo/ngrok alternative.
* https://www.raspberryanywhere.com/
* https://www.ultrahook.com/ Receive webhooks on localhost
* https://forwardhq.com/ not works anymore
* [serveo.net](https://github.com/u1i/tools/blob/master/serveo.md) ssh tunnel, not works anymore
* https://progsoft.net/en/software/pagekite other related software.


## Tor
All these problems are solved for Tor network and `*.onion` websites.
Single Onion Service is a good option: only four hops instead of a hidden service. But it's still slow and can be accessed only from Tor Browser.

## DDNS
The jkl.mn will offer a Dynamic DNS service.
Each subdmoain will be a random onion domain so that no needs to be registred.

https://github.com/yurt-page/dyndns-onion

## P2P DNS with DHT
DNS must be authorative but DHT doesn't guaratntee that a record will be found.
* https://github.com/mwarning/KadNode P2P DNS with content key, crypto key and PKI support. DynDNS alternative.
* https://www.youtube.com/watch?v=DFFNEoEYItE KadNode talk in German, use autotrsanslate

Old attempt
* https://github.com/Mononofu/P2P-DNS
* https://blog.desdelinux.net/ru/p2p-dns-sera-posible-deshacernos-de-icann/
* https://www.networkworld.com/article/2195700/p2p-based-alternative-to-dns-hopes-to-challenge-icann.html
* https://www.scs.stanford.edu/20sp-cs244b/projects/pDNS.pdf

