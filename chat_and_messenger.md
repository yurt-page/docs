# Chat and instant messanger

> [!NOTE]
> Project tasks https://github.com/orgs/yurt-page/projects/17/

The first successful chat app was ICQ.
It had a central server and closed protocol so all alternative clients died quickly (QIP, Miranda, Pidgin).
As a alternative to it was created an open source Jabber protocol, but it's failed by all means.
It's failed from beginning even with a name: the Jabber had to rename to XMPP which is harder to remember and confused users. 
Later there was created another protocol Matrix and it's again a sad story with almost same problems of XMPP.
Basically the article is about "how to solve problems that XMPP failed to solve".

## Mass messangers
Chat apps are extremely dependant of a network effect e.g. the more users are using a chat the more it's useful.
All today's chat apps had an aggressive marketing to achieve their market share.
I call them "mass messangers" and today everybody forgot the old Instant Messangers (IM).
The main success was achieved by a few simple solutions and principles:

1. Big centralized silos that is easy to use. With the XMPP you must find yourself a server to trust and to talk with your buddy your servers must be in a federation. Each word in this sentence is a big pain.
2. Almost unlimitted cloud storage for photos, videos and voice messages. Many people just using messangers to transfer files. With XMPP servers that was almost not possible. 
3. Using just a phone number as your id instead of ICQ number or a XMPP `nickname@server`. This is reusing of an existing centralization.
4. Load all your phone contacts to a server and build your buddy list automatically. The contact discovery also has a downside that almost anyone can find your contacts https://habr.com/ru/companies/vdsina/articles/518298/.
5. Just don't use encryption and use a binary protocols for a best speed. XMPP folks spent a lot of time on this topic and mostly failed.
6. Mobile first design: chats just naturally and quickly replaced SMS **and calls** in mass market.
7. All the above also allowed to build a perfect system for surveillance and chat companies almost not faced big obstacles. 

An adoption of mass messangers was so fast that in almost all countries almost all users "belongs" to a just a few silos.
And unlike social networks which are mostly meme photos for teenagers here we received an extremely dangerous situation when talks of serious peoples like politics, businessman or military personnel are monitored in real time.
Many kids and old people become an easy target.
Amount of fraud, social engineering, bullying, attacks and spam is just astonishing.
People just didn't had enough of understanding of all danger. And they won't have it.
We have infinitive data leak: even if not from you then from your wife or coworkers.
A great news here is that messanger companies tried hard to at least stop botnets.

Interesting that even if some government decided to protect (or expose) citizens and block a messanger this was already too painful.
People consider their messangers as their private communication and react to blocking extremely negatively.


## Fragmentation

There wasn't a single flagship messenger for XMPP and people were confused which one to choose.
Interoperability was painful.
The best was a Psi but then it was a fork Psi+ and it's impossible to explain to an average user.

With a mass messangers you never had such a problem: you have only one client for a Viber protocol i.e. the Viber itself.
There are few open source forks of a Telegram but they just add some features like PGP encryption and their interface remains mostly same.

We must keep in mind that a fragmentation is an enemy number one of a network effect.
But it also can be useful in a natural way. For example I'm using different messangers for different needs:

* Viber when I need to chat with random people like a plumber or online shop. The online shop may start sending a marketing spam. I just have disabled notifications in Viber.
* Telegram to chat with some friends but mostly to read some channels. E.g. it's more for entertainment and I trying not to open it.
* Matrix to talk with other developers about OpenWrt and YurtPage projects.
* Skype to talk with recruiters when I'm searching for a job. Other time I'm using it to talk with parents: historically that was a first messanger that we started to use for calls.
* MS Teams, Flock, Slack or even Discord for a corporate job discussions.

## Own messanger
So for my family and friends I need my own messanger with a server. I need a server for a file storage, End-to-End (E2E) encryption and ideally ability to work on local network in serverless mode. It doesn't make sense to use Tox over Tot network to talk with my wife in another room. Privacy can be relaxed and it's ok to have a metadata leak and use direct p2p connections. 
And here we have not so many options:

* Telegram has [open source clones](https://alternativeto.net/software/telegram/) with E2E encryption but poorly implemented. If fix them then it would be almost zero problems with migration. Still centralized and Android only. But there are some alternative servers for telegram (like it was for ICQ) but they are doomed because the MProto itself is poorly designed and often changed.
* Signal, Wire etc. Not so many advantages over Telegram + E2E. Higher possibility that they will be blocked (or less given that TG is more popular). You can't use own server and most privacy features simply not needed.
* [Meshenger](https://github.com/meshenger-app/meshenger-android) P2P calls without the need for accounts or access to the Internet. There is no discovery mechanism, no meshing and no servers: just scan each others QR-Code. Android only. Works badly. It's author is known adequate man who developed KadNode. So even if now this may be not that good choise it may be mush easier to make the Meshanger as a good product. 
* Jami - a DHT based and somewhat can work locally if install their OpenDHT server. Looks more or less adequate. 
* Briar - mash messanger over Bluetooth. It was created for coordination of mass protests and almost not usable for regular users. 
* [Tox](https://en.wikipedia.org/wiki/Tox_(protocol)) P2P E2E DHT
* Own XMPP server. The [Prosody](https://prosody.im/) is small and written in Lua and easily installed on OpenWrt router. The XMPP can work in XEP-0174: Serverless Messaging over Bonjour/ZeroConf but there are no any mobile clients that support this: the Conversations app has a feature request but it's really far from implementing.
* Own Matrix server: written in Python and too heavy, now there are attempts to write a server in Rust. The main advantage that it has a well funded company behind and has good clients e.g. Element.io. Still, it's not that much better than XMPP which is developed in more open manner by FOSS enthusiasts. Today this is a default option for a user friendly secure messangers but in fact this is just XMPP clients are less developed. It would be beter to invest into XMPP ecosystem to get the same level of quality but more sustainable.
* [FChat](https://github.com/stokito/pidgin-fchat) a simple(st) UDP based chat for local network without a server. The only one in its class. **UPD** https://www.kouchat.net/ has even Android app.
* [NileshTrivedi/family](https://github.com/nileshtrivedi/family) A messaging app for closed, trusted groups. Outdated but has good design principles.
* Anything web based: WebRTC+WebSockets e.g. Jitsi. Needs for some TLS certificate. The WebRTC can work over local network but you still need for internet to SDP to resolve host candidates.
* [Android-Bonjour-WebRTC](https://github.com/warren-bank/Android-Bonjour-WebRTC) this is a good solution.
* https://conversejs.org/ an xmpp client in browser and with Electron on destop and mobile (TBD). This is a very nice idea. JS will eat world.

A best comparision of secure chats https://bkil.gitlab.io/secuchart/

## Spam
* https://github.com/JabberSPAM/jabber-spam-fighting-manifesto/blob/master/Freedom-and-Anonymity.md discussion and solutions to fight spam in Jabber/XMPP network
