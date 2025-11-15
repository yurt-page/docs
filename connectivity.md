# Connectivity
Possible connections:
* Yurt on router and a user connects from local network: we can use http with internal IP e.g. http://192.168.1.1. We may nake some domain like my.jkl.mn that return A record with the private IP
* Yurt on PC, Raspberry etc. and a connects from local network. Now here we would need for some local DNS with a plain name because yurt's IP may be any. Should be not complicated with MDNS but not sure it user's router supports this. We still can use plain HTTP.
* We need for some reverse proxy or some alternative.
* Yurt on a router and connect from internet:
  * Two yurts can talk with each other by plain http or with self signed TLS certs, or even by SSH, on any port and any protocol. We are in a full control here.
  * But to be opened in browser a Yurt needs for TLS and the TLS certs needs for a domain (DDNS we can give for free).
  * If the yurt's IP is public then we need to use DDNS
  * Some ports may be blocked by ISP e.g. incoming/outgoing 25 for mail. Two yurts may use alternative ports like 2525 as a fallback.
  * If a user is behind CGNAT then you can't connect directly from a browser
    * You may use a tunnel: SSH port forwarding or even VPN based.
    * Use [UDP hole punching](https://en.wikipedia.org/wiki/UDP_hole_punching)
      * Two yurts or a special client can use it. But in a browser only WebRTC can do that.
      * Some weird workaround. We may make a service to watch Yurt from a browser: use WebRTC as transport and make a HTTP-to-WebRTC proxy. We can then show a Yurt in IFRAME from jkl.mn
    

Connectivity is a problem even bigger than hosting devices.
Many consumer grade devices doesn't have a static IP so that nobody from internet can't connect directly.
But we need to expose web server without a public IP address.
Some providers allow to buy a static IP but it not so cheap. And again, the main goal is to make users not to pay anything.
Many ISPs give a dynamic IP that is changing from time to time. So you can't register a DNS record because when it will be changed you may not notice.

If your web server doesn't have a public or dynamic IP address e.g. behind CGNAT then it can't be accessed from internet.
You may try NAT punching. See [How NAT traversal works](https://tailscale.com/blog/how-nat-traversal-works/).
But it will work only for UDP. The WebRTC does this but it's too heavy for routers.
It is posible to build a proxy from WebRTC to plain HTTP so that we don't need to rewrite the entire system.
Anyway you won't be able to simply connect to a yurt, only two yurts can talk with each other.
The HTTP3 is UDP based so maybe it's possible to open directly in browser.

Even with symmetric NAT you can establish a connection if you have enough time https://habr.com/ru/post/155803/
So two yurts may connect with each other and start data exchange.



## Tunnels
In other cases you need some public proxy that your server will connect to and the proxy will redirect incoming request to your server.
Usually such proxies also gives you a unique subdomain and can enable HTTPS for you.

Here many problems arise:
1. The proxy has bandwidth limits
2. HTTPS termination on proxy means that the proxy can read traffic. Some proxies allow passthrough by SNI.
3. Subdomains may set a cookie to a parent domain
4. The biggest problem is to avoid botnets and fishing sites.

Technically speaking the tunnel between server and proxy is not so easy to implement.
It must be not a VPN but also simple SOCKS is not good here.
So such tunneling services uses protocols like port forward over SSH or specialized multiplexing protocols.

![network-protocol-software-terminology](https://user-images.githubusercontent.com/415502/223048886-f3e58d6f-8898-49f2-9174-eb140b2a15d3.png)

### Tor
Tor provides free to use Hidden Services (Onion Service) which will be proxied with 6 proxies: 3 from a client side and 3 to your site.
This makes it very slow. There is a Single Onion Service if you don't care about hiding your service location. Then you'll have 4 hops.
https://community.torproject.org/onion-services/overview/
A client also needs for Tor installed but also onion domains aren't human readable.
Still, this is a good option if you need to connect two yurts because the Tor is forever for free and stable.

**UPD** I added luci-app-tor so now users can configure an Onion Service from GUI.

## SSH tunnel
The OpenWrt's Dropbear ssh (dbclient) supports the port forwarding. But they are slow. OpenWrt has a sshtunnel package to reconnect but it depends on OpenSSH client.
I partially fixed this https://github.com/openwrt/packages/pull/21263

See https://openwrt.org/docs/guide-user/services/ssh/sshtunnel
**UPD** I added luci-app-sshtunnel so now users can configure tunnels from GUI.

### Tunnel providers and software
See [Awesome Tunneling](https://github.com/anderspitman/awesome-tunneling)

Most interesting are:
* [pagekite](https://pagekite.net/home/) Uses HTTP proxy like protocol with an additional encryption. One of the oldest. Has openwrt package and Luci app. Allows to deploy own server instance (called frontend). See [PageKite intro](https://www.youtube.com/watch?v=SRhK05KjxYA) and [Accessing your Mbed device from anywhere using Pagekite How to create a Mbed library for Pagekite](https://www.youtube.com/watch?v=23BS7kdQMzw). Paid plain is quite expensive.
* [CloudFlare](https://www.cloudflare.com/products/tunnel/) has a free plan but it's too havy for most routers.
* [localhost.run](https://localhost.run/) SSH tunnel. The server side is not FOSS. Here is some details about internals https://medium.com/localhost-run/localhost-run-the-origin-story-5aeaf5692dee. Paid plain is quite expensive and free plan doesn't allow for stable domain.
* https://git.sequentialread.com/sqr/greenhouse  https://greenhouse-alpha.server.garden/ TCP reverse tunnel in NodeJS. Free to use and the server side is FOSS
* https://telebit.cloud/ written in NodeJs
* https://github.com/azimjohn/jprq ngrok alternative using WebSockets.
* https://github.com/antoniomika/sish open source serveo/ngrok service alternative for SSH tunnels.

### VPN
Once you have a tunnel to your router you may want to also have an outgoing traffic tunnel e.g. VPN. So maybe just ot use VPN service that gives a public IP?
It looks like some VPN services do have such option and with the self-hosting arising more will start to sell this service.
The OpenVPN is based on TLS so we can reuse the existing libraries. It also almost always installed on routers.
This may be a good ready to go option that will cost almost noting to implement.

* https://security.stackexchange.com/questions/200248/difference-between-ssh-tunnel-proxy-and-vpn-in-terms-of-security


## UPnP and NATPMP/PCP
* See https://forum.openwrt.org/t/port-control-protocol-support/114411/17
* https://launchpad.net/upnp-router-control a GUI to open a port but for UPnP only.
* natpmpc a small utility that allows to open a port with NATPMP (PCP?)
* upnpc - miniupnpc library test client.
* https://github.com/rofl0r/nat-tunnel

## IoT
Basically each IoT platform has own gateways and other connectivity things. We may need to investigate this
* https://github.com/thin-edge/thin-edge.io
