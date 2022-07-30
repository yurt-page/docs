# Domains

## nsupdate
If you have an own DNS zone e.g. jkl.mn then the DNS server supports a special command nsupdate which is an extension for DNS protocol.
So you can use the nsupdate command to change some subdomain records. This is used by administrators but not by routers.
The reason is because you need a pre-shared TSIG key and also the nsupdate utility is too heavy for routers.
Still OpenWrt has a support of this https://openwrt.org/docs/guide-user/services/ddns/client#bindnsupdate


### Knot DDNS
I thinked to use use the Knot DNS server for jkl.mn but now I don't think I need it. Still some useful links:
* https://jpmens.net/2013/03/12/knot-dns-dynamic-updates-and-a-bit-of-rrl/
* https://jpmens.net/2011/10/13/dynamically-or-not-dynamically-that-is-the-question/
* https://www.knot-dns.cz/docs/2.6/html/configuration.html#dynamic-updates
* https://habr.com/ru/post/101380/ Собственный Dynamic DNS
* https://doc.turris.cz/doc/en/public/dns_knot_misc

## DynDNS


### DynDNS2 API
All routers already have a support of no-ip.com or dyn.com (previously called DynDNS.com). A router just makes a GET request `nic/update?hostname={yoursubdomain}&password={pass}` to a server and it detects an IP and updates a DNS record. Since all DynDNS providers supports the same URL as DynDNS.com the API is unofficially called DynDNS2 i.e. DynDNS.com V2. Some protocol descriptions:
* https://www.dynu.com/en-US/DynamicDNS/IP-Update-Protocol#signoff
* https://nsupdateinfo.readthedocs.io/en/latest/standards.html
* https://help.dyn.com/remote-access-api/perform-update/

### Providers
Some notable DDNS providers:
* [DynDNS](https://dyn.com)
* [No-IP](https://www.noip.com/)
* [Duck DNS](https://duckdns.org) free service, widely supported
* [nsupdate.info](https://www.nsupdate.info) has no limits and it's backend code is open sourced. But currently account registration is closed because of many abuses.
* [Free DNS](https://freedns.afraid.org) one of the oldest but uses own XML based protocol.


### DDNS Clients
* [OpenWrt DDNS client](https://openwrt.org/docs/guide-user/services/ddns/client) uses shell scripts but depends on OpenWrt libs and can't be used in Ubuntu.
* [In-a-Dyn](http://github.com/troglobit/inadyn) depends on [[GnuTLS]]. Has a package for Ubuntu
* [ddupdate](https://github.com/leamas/ddupdate) uses [[Python]]. Has a package for Ubuntu
* [ddclient](https://ddclient.net) uses [[Perl]]. Has a package for Ubuntu
* [DynDNS Simply Client](https://sourceforge.net/projects/dyndnssimplycl/) for Windows. Old but still works
* [DirectUpdate](https://www.directupdate.net/) for Windows. Rich options but paid.

### Software for DDNS providers
* [nsupdate.info](https://github.com/nsupdate-info/nsupdate.info) written in Python and Django, accepts DynDNS2 updates but then calls nsupdate for DNS server.
* [dprandzioch/docker-ddns](https://github.com/dprandzioch/docker-ddns) written in Go, no UI, accepts DynDNS2 updates but then calls nsupdate for DNS server.
* [olimpo88/PyDDNS](https://github.com/olimpo88/PyDDNS) UI for dprandzioch/docker-ddns written in Python и Django.
* [ddserver](https://github.com/ddserver/ddserver) written in Python, used as pipe-backend for PowerDNS
* [node-ddns](https://github.com/DSorlov/node-ddns) written in NodeJS, a standalone DNS server with basic support of DynDNS2
* [hoedlmoser/ddnss](https://github.com/hoedlmoser/ddnss) written in PHP, no UI, just accepts DynDNS2 updates and calls nsupdate
* [dyndns53](https://github.com/sTywin/dyndns53) written in Java for AWS Lambda
* [duckdns-mirror](https://github.com/BenjaminHCCarr/duckdns-mirror) written in Java, old source code of DuckDNS. Depends on AWS
* [GnuDip](http://gnudip2.sourceforge.net/gnudip-www/) another old and unpopular protocol. Some Huawei routers may support it.
* [x1angli/pyDDNS](https://github.com/x1angli/pyDDNS) not a DNS but updates a local /etc/hosts

I added links to a Wikipedia page to make them easier to find for a new users https://ru.wikipedia.org/wiki/%D0%94%D0%B8%D0%BD%D0%B0%D0%BC%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B9_DNS#%D0%9F%D0%BE_%D0%B4%D0%BB%D1%8F_DDNS_%D0%BF%D1%80%D0%BE%D0%B2%D0%B0%D0%B9%D0%B4%D0%B5%D1%80%D0%BE%D0%B2=
But these links may be removed any time because Wikipedics don't like them.

## Tor
All these problems are solved for Tor network and `*.onion` websites.
Single Onion Service is a good option: only four hops instead of a hidden service. But it's still slow and can be accessed only from Tor Browser.
Example of configuring a Single Onion Service https://gist.github.com/stokito/2a7ab43cb409afa9eef8061dd12ed82f
We can add to a Yurt the Single Onion Service by default but it will be accessable only via Tor Browser.
Also the Tor is too heavy for regular routers: it depends on OpenSSL (>1mb) and creates additional files https://lists.torproject.org/pipermail/tor-dev/2022-July/014751.html


## DDNS
The jkl.mn will offer a Dynamic DNS service.
Each subdmoain will be a random onion domain so that no needs to be registred.

https://github.com/yurt-page/dyndns-onion

* https://www.youtube.com/watch?v=zZzOVKPcIMg Jesse Victors - The Onion Name System: Tor-powered Decentralized DNS for Tor Onion Services
* https://www.sauteed-onions.org/ we can attach an existing domain to an .onion with a subdomain


## P2P DNS with DHT
DNS must be authorative but DHT doesn't guaratntee that a record will be found or that the returned record is not faked.
* https://github.com/mwarning/KadNode P2P DNS with content key, crypto key and PKI support. DynDNS alternative.
* https://www.youtube.com/watch?v=DFFNEoEYItE KadNode talk in German, use autotrsanslate

Other attempts and research
* https://github.com/Mononofu/P2P-DNS early attempt to introduce .p2p domain, abandoned
* https://blog.desdelinux.net/ru/p2p-dns-sera-posible-deshacernos-de-icann/
* https://www.networkworld.com/article/2195700/p2p-based-alternative-to-dns-hopes-to-challenge-icann.html
* https://www.scs.stanford.edu/20sp-cs244b/projects/pDNS.pdf
* https://ieeexplore.ieee.org/document/4583073
* https://wiki.p2pfoundation.net/Dot-P2P
* https://tools.ietf.org/id/draft-grothoff-iesg-special-use-p2p-names-01.html
* https://web.cs.ucla.edu/~lixia/papers/06INFOCOM.pdf
* https://www.kiv.zcu.cz/~ledvina/DHT/lecture13.pdf
* https://mkaczanowski.com/golang-build-dynamic-dns-service-go/

## GNUnet Name System
It also uses DHT a (but their own R5N) but very complicated to understand.
https://lsd.gnunet.org/lsd0001/

## DANE
DANE ptotocol used to set a TLS cert with DSN record. This makes possibe to have HTTPS for .bit and .onion domains i.e. without a CA.
* https://www.youtube.com/watch?v=nt261DzHdNU Use DANE for TLS cert for NameCoin
* https://habr.com/ru/company/1cloud/blog/454322/ DANE для браузеров провалилась



## DNS pull
This is not related but a good idea to improve privacy of DNS queries. 

> Looks like a DNS leak easily solved by just caching locally ALL domains. One rec is 100 bytes. IPv4 addr has 32 bits. 2^32 * 100 = 430Gb. It's fine for modern disks. And get few Gb of deltas daily. For most DNS with stable TTL this should work. More privacy than DNS over TLS
> https://twitter.com/stokito/status/1540107921324900356

This idea apeared before https://www.kiv.zcu.cz/~ledvina/DHT/lecture13.pdf:

There are 76.9 million domains registered
- Including generic TLDs and country-code TLDs
- Compressed file with all info: 7.5GB
- About 20,000 AS’s in the world
- Suppose each NS serves other 3 NS’s (23 GB pushed)
- Build delivery tree of depth 10 roughly
- Push updates daily
- About 760 KBytes / hour
- About 850 Kbps upload to three peers
- A lot of changes are for the same bindings
- 87% of domains do not change at all


Great latency performance!
- Akamai still works
- Backward-compatible with old DNS
- We are only adding prefetching to DNS
– Improve performance with affecting the systems architecture
- Idea for M.Sc. project: build push-based DNS!


I've sent a letter to author where asked for any futher research but didn't received a reply yet.
Anyway something similar can be implemented for yurt domains internally. Since we have a single jkl.mn DNS then we can easily track IP changes and yurts can download the DNS updates.
