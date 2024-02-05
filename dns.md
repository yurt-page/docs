# Domains and DNS
Domains and DNS is surprisingly a very big problem for a self hosting.
You can buy a domain but...
* It's not that cheap. Children don't have their money at all.
* Those money goes to the DNS mafia basically for nothing.
* And don't forget to renew it. 146% of homepages had their domain expired. Then is can be hijacked by squatters.
* This is a manual step. And you have to find a good and free name.
* It complicated to configure: you need to understand what does it mean A, AAAA, MX, NS and other records.
* Zones have their own rules. You may be easily lost your domain or just blocked, censored or eliminated by a competitor.


The jkl.mn will offer a Dynamic DNS service.
Each subdomain will be a random onion domain so that no needs to be registered.

https://github.com/yurt-page/dyndns-onion

## nsupdate
If you have an own DNS zone e.g. example.com then the DNS server supports a special command nsupdate which is an extension for DNS protocol.
So you can use the nsupdate command to change some subdomain records. This is used by administrators but not by routers.
The reason is that you need a pre-shared TSIG key and also the nsupdate utility is too heavy for routers.
Still OpenWrt has a support of this https://openwrt.org/docs/guide-user/services/ddns/client#bindnsupdate


## DynDNS
All routers already have a support of no-ip.com or dyn.com (previously called DynDNS.com).
A router just makes a GET request `nic/update?hostname={yoursubdomain}&password={pass}` to a server.
It detects an IP and updates a DNS record. 

### DynDNS2 API
Since all DynDNS providers supports the same URL as DynDNS.com.
The API is unofficially called DynDNS2 i.e. DynDNS.com V2.

Some protocol descriptions:
* https://www.dynu.com/en-US/DynamicDNS/IP-Update-Protocol#signoff
* https://nsupdateinfo.readthedocs.io/en/latest/standards.html
* https://help.dyn.com/remote-access-api/perform-update/



### Providers
Some notable DDNS providers:
* [DynDNS](https://dyn.com)
* [No-IP](https://www.noip.com/)
* [Duck DNS](https://duckdns.org) free service, widely supported
* [DynV6](https://dynv6.com/) feature rich and cool API.
* [nsupdate.info](https://www.nsupdate.info) has no limits and it's backend code is open sourced. But currently [account registration is closed because of many abuses](https://github.com/nsupdate-info/nsupdate.info/issues/496).
* [Free DNS](https://freedns.afraid.org) one of the oldest but uses own XML based protocol.
* [dynu.com] looks like not working anymore but have a rich and well documented apii
* [freemyip.com](https://freemyip.com/) easy to start


### DDNS Clients
* [OpenWrt DDNS client](https://openwrt.org/docs/guide-user/services/ddns/client) uses shell scripts but depends on OpenWrt libs and can't be used in Ubuntu.
* [In-a-Dyn](http://github.com/troglobit/inadyn) depends on [[GnuTLS]]. Has a package for Ubuntu
* [ddupdate](https://github.com/leamas/ddupdate) uses [[Python]]. Has a package for Ubuntu
* [ddclient](https://ddclient.net) uses [[Perl]]. Has a package for Ubuntu
* [DynDNS Simply Client](https://sourceforge.net/projects/dyndnssimplycl/) for Windows. Old but still works
* [DirectUpdate](https://www.directupdate.net/) for Windows. Rich options but paid.
* [dynu.com](https://www.dynu.com/en-US/Resources/Downloads) works only with dynu but still interesting
* [AppQuarter](https://appquarter.com/) for MacOS
* [Dynephant](https://github.com/chriv/dynephant) for Windows from dynv6.com
* https://github.com/hamonikr/duckdns zenity base GUI for DuckjDNS
* https://minglebit.com/products/realdns.php RealDNS is a client for iOS and they support DuckDNS
* https://github.com/JozefJarosciak/DuckDNSClient
* https://github.com/BeyondCodeBootcamp/DuckDNS.sh
* [yaddns](https://yaddns.github.io/) https://github.com/yaddns/yaddns written in C and outdated
* https://github.com/mholt/caddy-dynamicdns/ for Caddy

### DNS API Libraries

* [Lexicon](https://github.com/AnalogJ/lexicon/) in Python [params](https://dns-lexicon.readthedocs.io/en/latest/configuration_reference.html#nfsn)
* https://github.com/octodns/octodns Python
* https://github.com/go-acme/lego Golang. Used by Caddy but bloated
* https://github.com/StackExchange/dnscontrol Golang
* OpenWrt ddns-scripts has API integrations https://github.com/openwrt/packages/tree/master/net/ddns-scripts/files/usr/lib/ddns
* Letsencrypt dns-01 needs for DNS API impementations and there is a lot of them:
  * https://letsencrypt.org/en/docs/client-options/ some clients support the dns-01
  * certbot has DNS api plugins written in Python
    * The [certbot](https://github.com/certbot/certbot) itself out of the box has `certbot-dns-*` plugins for ovh, DO, CF
    * https://github.com/infinityofspace/certbot_dns_duckdns
  * shell
    * `acme.sh`  https://github.com/acmesh-official/acme.sh/tree/master/dnsapi wget/curl and bloated [wiki](https://github.com/acmesh-official/acme.sh/wiki/dnsapi)
    * `getssl.sh` https://github.com/srvrco/getssl/blob/master/dns_scripts/  curl based simpler
    * `dehydrated` https://github.com/dehydrated-io/dehydrated/wiki
  * JS
     * Greenlock/acme.js https://git.rootprojects.org/explore/repos?tab=&sort=recentupdate&q=acme-dns-01-



### Software for DDNS providers
* https://github.com/sandstorm-io/sandcats DDNS service for sandstorm.io
* [nsupdate.info](https://github.com/nsupdate-info/nsupdate.info) written in Python and Django, accepts DynDNS2 updates but then calls nsupdate for DNS server.
* [dprandzioch/docker-ddns](https://github.com/dprandzioch/docker-ddns) written in Go, no UI, accepts DynDNS2 updates but then calls nsupdate for DNS server.
* [olimpo88/PyDDNS](https://github.com/olimpo88/PyDDNS) UI for dprandzioch/docker-ddns written in Python и Django.
* [ddserver](https://github.com/ddserver/ddserver) written in Python, used as pipe-backend for PowerDNS
* [node-ddns](https://github.com/DSorlov/node-ddns) written in NodeJS, a standalone DNS server with basic support of DynDNS2
* https://www.npmjs.com/package/ddnsd and https://github.com/coolaj86?tab=repositories&q=ddns from AJ ONeal (author of https://therootcompany.com/hub/)
* https://www.npmjs.com/search?q=ddns plenty of others like https://github.com/eugeneware/homer
* [hoedlmoser/ddnss](https://github.com/hoedlmoser/ddnss) written in PHP, no UI, just accepts DynDNS2 updates and calls nsupdate
* [dyndns53](https://github.com/sTywin/dyndns53) written in Java for AWS Lambda
* [duckdns-mirror](https://github.com/BenjaminHCCarr/duckdns-mirror) written in Java, old source code of DuckDNS. Depends on AWS
* [GnuDip](http://gnudip2.sourceforge.net/gnudip-www/) another old and unpopular protocol. Some Huawei routers support it.
* [x1angli/pyDDNS](https://github.com/x1angli/pyDDNS) not a DNS but updates a local /etc/hosts
* [Linux4/ddnsd](https://github.com/Linux4/ddnsd) Ddnsd is a background service to dynamically update your IP-Address in a DNS Zone file. It's code un unclear but looks like it uses the https://puck.nether.net/dns/login
* [fenderle/ddnsd](https://github.com/fenderle/ddnsd) Perl daemon that updates DNS zone with nsupdate
* [skx/dhcp.io](https://github.com/skx/dhcp.io) written in Perl, has UI and registration
* http://smarden.org/tinydyndns/ update DNS by POP3 O_o (from djbdns)

I added links to a Wikipedia page to make them easier to find for a new users https://ru.wikipedia.org/wiki/%D0%94%D0%B8%D0%BD%D0%B0%D0%BC%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B9_DNS#%D0%9F%D0%BE_%D0%B4%D0%BB%D1%8F_DDNS_%D0%BF%D1%80%D0%BE%D0%B2%D0%B0%D0%B9%D0%B4%D0%B5%D1%80%D0%BE%D0%B2=
But these links may be removed any time because Wikipedics don't like them.

Here is a prototype that I made https://github.com/yurt-page/go-ddnsd

We need to fight with abuses https://github.com/nsupdate-info/nsupdate.info/issues/496#issuecomment-1362854557


Keenetic routers have own DDNS service
https://help.keenetic.com/hc/en-us/articles/360000400919

But also supports others
https://help.keenetic.com/hc/en-us/articles/360000934780-Dynamic-DNS-client

Subproject:
[DNS API standard or specification](https://community.letsencrypt.org/t/dns-api-standard-or-specification/189887)


## Tor
All these problems are solved for Tor network and `*.onion` websites.
Single Onion Service is a good option: only four hops instead of a hidden service. But it's still slow and can be accessed only from Tor Browser.
Example of configuring a Single Onion Service https://gist.github.com/stokito/2a7ab43cb409afa9eef8061dd12ed82f
We can add to a Yurt the Single Onion Service by default but it will be accessible only via Tor Browser.
Also the Tor is too heavy for regular routers: it depends on OpenSSL (>1mb) and creates additional files https://lists.torproject.org/pipermail/tor-dev/2022-July/014751.html

It would be great to have a mnemonic names:
* https://www.youtube.com/watch?v=zZzOVKPcIMg Jesse Victors - The Onion Name System: Tor-powered Decentralized DNS for Tor Onion Services
* https://www.sauteed-onions.org/ we can attach an existing domain to an .onion with a subdomain



## P2P DNS based on DHT
DNS must be authoritative but DHT doesn't guarantee that a record will be found or that the returned record is not faked.

### KadNode - DynDNS alternative.
The [KadNode](https://github.com/mwarning/KadNode) is P2P DNS with content key, crypto key and PKI support.
See [KadNode talk](https://www.youtube.com/watch?v=DFFNEoEYItE). It's in German, use auto-translate.

This is basically DNS over Torrent DHT (Kadmelia). The DHT is slow so the domain may be not resolved before timeout.
The DHT is great because there is no a DB but also adds some level of stablity against outages or attacks.
The Tor network also uses own DHT but it's more advanced: not only faster but also makes re-hash daily to protect from generating of similar hashes for a specific domain and thus catching search requests and thus get approximate count of visits.
As a random source for re-hashing the Tor takes last block hash from Bitcoin blockchain which is a cool idea by itself and may be used in other places.

By itself the domains can be usual e.g. real registered or just a ECC public key e.g. free but ugly.
Once KadNode resolves an IP it will try to connect itself and check that cert corresponds.
This saves from connecting to another server with the IP of outdated domain.
E.g. KadNode makes the same check that a browser makes when checks that a cert's domain corresponding to the domain.
This adds an addional delay still, not so big.

The KadNode is based on mbedTLS that doesn't have ed25519 so it also can't generate onion-like domains.
This is not a big deal but having interchangable domains is a nice thing to have.

## IPNS from IPFS
https://docs.ipfs.tech/concepts/ipns/

## Local IP as domain + TLS
https://github.com/cunnie/sslip.io

### Other attempts and research
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

## DNS SEC
* https://mforney.org/blog/2020-05-21-securing-your-zone-with-dnssec-and-dane.html
* https://berthub.eu/dnssec/
* [DNSSEC Keys and Signing Process manually with openssl-tools](https://gist.github.com/stokito/e401279d405040565e8eb874c024a2c7)

## DANE
The DANE protocol used to set a TLS cert with DSN record. This makes possible to have HTTPS for .bit and .onion domains i.e. without a CA.
* https://www.youtube.com/watch?v=nt261DzHdNU Use DANE for TLS cert for NameCoin
* https://habr.com/ru/company/1cloud/blog/454322/ DANE для браузеров провалилась



## DNS pull
This is not related but a good idea to improve privacy of DNS queries.

> Looks like a DNS leak easily solved by just caching locally ALL domains. One rec is 100 bytes. IPv4 addr has 32 bits. 2^32 * 100 = 430Gb. It's fine for modern disks. And get few Gb of deltas daily. For most DNS with stable TTL this should work. More privacy than DNS over TLS
> https://twitter.com/stokito/status/1540107921324900356

This idea appeared before https://www.kiv.zcu.cz/~ledvina/DHT/lecture13.pdf:

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


I've sent a letter to author where asked for any further research but didn't receive a reply yet.
Anyway something similar can be implemented for yurt domains internally.
Since we have a single jkl.mn DNS then we can easily track IP changes and yurts can download the DNS updates.


## Making site offline
Some DDNS servers allows to turn off a website. Given that we should support websites from laptop that maybe on or off this is a good things to implement.
See also https://tomhummel.com/posts/website-business-hours/
