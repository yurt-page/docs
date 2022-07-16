== Providers ==
Some notable DDNS providers:
* [DynDNS]]
* [No-IP]]
* [https://duckdns.org Duck DNS] free service, widely supported
* [https://www.nsupdate.info nsupdate.info] has no limits and it's backend code is open sourced.
* [https://freedns.afraid.org Free DNS] one of the oldest.


== DDNS Clients ==
* [https://openwrt.org/docs/guide-user/services/ddns/client DDNS client] for routers with OpenWrt
* [http://github.com/troglobit/inadyn In-a-Dyn] depends on [[GnuTLS]]
* [https://github.com/leamas/ddupdate ddupdate] uses [[Python]]
* [https://ddclient.net ddclient] uses [[Perl]]
* [https://sourceforge.net/projects/dyndnssimplycl/ DynDNS Simply Client] for Windows. Old but still works
* [https://www.directupdate.net/ DirectUpdate] for Windows. Rich options

== Software for DDNS providers ==
* [https://github.com/nsupdate-info/nsupdate.info nsupdate.info] written in Python and Django, accepts DynDNS2 updates but then calls nsupdate for DNS server.
* [https://github.com/dprandzioch/docker-ddns dprandzioch/docker-ddns] written in Go, no UI, accepts DynDNS2 updates but then calls nsupdate for DNS server.
* [https://github.com/olimpo88/PyDDNS olimpo88/PyDDNS] UI for dprandzioch/docker-ddns written in Python и Django.
* [https://github.com/ddserver/ddserver ddserver] written in Python, used as pipe-backend for PowerDNS
* [https://github.com/DSorlov/node-ddns node-ddns] written in NodeJS, a standalone DNS server with basic support of DynDNS2
* [https://github.com/hoedlmoser/ddnss hoedlmoser/ddnss] written in PHP, no UI, just accepts DynDNS2 updates and calls nsupdate
* [https://github.com/sTywin/dyndns53 dyndns53] written in Java for AWS Lambda
* [https://github.com/BenjaminHCCarr/duckdns-mirror duckdns-mirror] written in Java, old source code of DuckDNS
* [http://gnudip2.sourceforge.net/gnudip-www/ GnuDip] another old and unpopular protocol. Some Huawei routers may support it.
* [https://github.com/x1angli/pyDDNS x1angli/pyDDNS] not a DNS but updates a local /etc/hosts


## Tor
All these problems are solved for Tor network and `*.onion` websites.
Single Onion Service is a good option: only four hops instead of a hidden service. But it's still slow and can be accessed only from Tor Browser.

## DDNS
The jkl.mn will offer a Dynamic DNS service.
Each subdmoain will be a random onion domain so that no needs to be registred.

https://github.com/yurt-page/dyndns-onion

* https://ru.wikipedia.org/wiki/%D0%94%D0%B8%D0%BD%D0%B0%D0%BC%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B9_DNS#%D0%9F%D0%BE_%D0%B4%D0%BB%D1%8F_DDNS_%D0%BF%D1%80%D0%BE%D0%B2%D0%B0%D0%B9%D0%B4%D0%B5%D1%80%D0%BE%D0%B2=
* https://jpmens.net/2013/03/12/knot-dns-dynamic-updates-and-a-bit-of-rrl/
* https://jpmens.net/2011/10/13/dynamically-or-not-dynamically-that-is-the-question/
* https://openwrt.org/docs/guide-user/services/ddns/client#bindnsupdate

## P2P DNS with DHT
DNS must be authorative but DHT doesn't guaratntee that a record will be found.
* https://github.com/mwarning/KadNode P2P DNS with content key, crypto key and PKI support. DynDNS alternative.
* https://www.youtube.com/watch?v=DFFNEoEYItE KadNode talk in German, use autotrsanslate

Other attempts
* https://github.com/Mononofu/P2P-DNS
* https://blog.desdelinux.net/ru/p2p-dns-sera-posible-deshacernos-de-icann/
* https://www.networkworld.com/article/2195700/p2p-based-alternative-to-dns-hopes-to-challenge-icann.html
* https://www.scs.stanford.edu/20sp-cs244b/projects/pDNS.pdf
* https://ieeexplore.ieee.org/document/4583073
* https://wiki.p2pfoundation.net/Dot-P2P
* https://tools.ietf.org/id/draft-grothoff-iesg-special-use-p2p-names-01.html
* https://web.cs.ucla.edu/~lixia/papers/06INFOCOM.pdf
* https://www.kiv.zcu.cz/~ledvina/DHT/lecture13.pdf
* https://mkaczanowski.com/golang-build-dynamic-dns-service-go/





## DynDNS2 API
https://www.dynu.com/en-US/DynamicDNS/IP-Update-Protocol#signoff
https://nsupdateinfo.readthedocs.io/en/latest/standards.html
https://help.dyn.com/remote-access-api/perform-update/

## Knot DDNS
https://jpmens.net/2013/03/12/knot-dns-dynamic-updates-and-a-bit-of-rrl/
https://jpmens.net/2011/10/13/dynamically-or-not-dynamically-that-is-the-question/


## DNS pull
From https://www.kiv.zcu.cz/~ledvina/DHT/lecture13.pdf:

There are 76.9 million domains registered
– Including generic TLDs and country-code TLDs
– Compressed file with all info -- 7.5GB
• About 20,000 AS’s in the world
– Suppose each NS serves other 3 NS’s (23 GB pushed)
– Build delivery tree of depth 10 roughly
• Push updates daily
– About 760 KBytes / hour
– About 850 Kbps upload to three peers
• A lot of changes are for the same bindings
– 87% of domains do not change at all


Great latency performance!
• Akamai still works
• Backward-compatible with old DNS
• We are only adding prefetching to DNS
– Improve performance with affecting the systems’
architecture
• Idea for M.Sc. project:
– build push-based DNS!


https://twitter.com/stokito/status/1540107921324900356
