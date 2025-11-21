# Email
> [!NOTE]
> Project tasks https://github.com/orgs/yurt-page/projects/16

EMail is a cornerstone of Internet, and it's important to give users an ability to send and receive them.
Emails are very important for privacy: if you read someone's email you know what they buy, what websites they visit, what happens in their life.
If email hacked then you can reset passwords on all websites. **Unless you have a secure email you can't really be safe in internet.**
<details>
<summary>What is used nowadays</summary>

* Most users for personal needs using silos: GMail, Hotmail, Yahoo, Yandex, iCloud. They have good anti-spam filters, but they're selling their users. Most users using them just because they can check mail from a browser.
* Others using corporate email from their job or universities. They are mostly use MUA (Outlook, Thunderbird) but sometimes corporate email is based on silos like Microsoft Office 365.
* Small amount of regular users using email from their internet provider (e.g. GMX) because they already have it.
* Users who value privacy buys paid email services: Proton Mail, FastMail, Zoho. But in fact nobody stops the services from watching your mail.

Good news is that EMail is already non-centralized. But it's insanely too hard to configure.
That's why there is some installers like [Mail-in-a-Box](https://mailinabox.email), [MailCow](https://mailcow.email) or Luke Smith's [Email Wizard](https://github.com/LukeSmithxyz/emailwiz).

But where will you install your own server? If on a hosting then **you still have the problem with privacy and security**.
</details>

## How email works in short
Email transferred with SMTP protocol but this is server to server push style protocol.
Regular users also needs a MUA client with POP3 or newer IMAP to pull their received mail from the SMTP server. They may use web access instead.
When a user sends a letter from MUA it connects to configured Submitting SMTP server on port 587. It requires authorization.
It adds DKIM signature to confirm that the letter is sent from the domain and retransmitted to receiver's SMTP server over 25 port.

At beginning only the SMTP protocol existed. A user logged in to a terminal (that had an SMTP) and saw a received messages.
The POP protocol was created because many users didn't had own SMTP server and they had to fetch mail from another server.


## Technical problems
See [IndieWeb](https://indieweb.org/email)

### Dependency to DNS
Users may not have a domain or use a DDNS. Anyway configuring it manually is too complicated for most users.
The MX records in DNS actually can be omitted and then A record will be used. This is great.
But for the SPF, DKIM and DMARC we need to have at least a TXT record.
If using jkl.mn subdomain then this can be done automatically on jkl.mn.
But this allows us to make MITM attack.
But at least other SMTP servers will accept your email.
BTW other DDNS providers usually not supports the MX or TXT records.

### DKIM
Without the DKIM email won't be accepted by other SMTP servers or marked as spam.
The [opendkim](https://openwrt.org/packages/pkgdata/opendkim) package for OpenWrt is quite big and depends on OpenSSL.
And yes it's hard to configure it https://easydmarc.com/blog/how-to-configure-dkim-opendkim-with-postfix/

Most emails of regular users are just simply notifications and marketing like "Sales today".
So if we'll provide at least ability to receive email this will already cover 98% of usage of a regular user.
Still even for receiving a letter it would be nice have the DKIM signature check.

Also we may try to implement the https://en.bitcoin.it/wiki/Hashcash  or it's Outlook version "Email Postmark"
* [Email Postmark Validation Algorithm](https://learn.microsoft.com/en-us/openspecs/exchange_server_protocols/ms-oxpsval/f894e839-22a2-4f72-a1af-a7de40089bc8)
* [PennyPost: HashCash for Thunderbird](https://pennypost.sourceforge.net/PennyPost) sources: https://github.com/jonasbits/PennyPostTB 


### Port blocking
The 25 port is usually blocked by ISP. We may have a partial workaround by using another port and declaring it with SRV record in DNS.
There is even some [RFC6186 Use of SRV Records for Locating Email Submission/Access Services](https://www.rfc-editor.org/rfc/rfc6186) but it covers only submission e.g. 587 port. We may add `_smtp` record and use it instead of MX.
For our yurt clients we may perform our own lookup or just by default use some 2525 port.
* https://community.nethserver.org/t/rfc-6186-srv-template-records/18998
* https://itecnotes.com/server/vps-dns-setting-for-pop3-and-smtp-email/
* https://stackoverflow.com/questions/60298006/what-major-e-mail-clients-actually-make-use-of-dns-srv-autoconfiguration

### Spam, viruses and phishing
Since email can send almost everyone and that leads to abuse: viruses, spam, scam, "nigerian letters" and phishing.

This is a most severe problem evener than privacy. Without a good spam or phishing protection our users will be eventually hacked.
Or at least they'll move back to silos to clear mailbox.

For the spam protection the default solution is SpamAssassin but it's very slow, heavy and depends on Perl.
Good news that today we have more fast and effective [rspamd](https://rspamd.com/) but it wasn't ported to OpenWrt yet and still too heavy for routers.
This is really state-of-the-art system, see video [Rspamd — высокопроизводительная система фильтрации спама](https://www.youtube.com/watch?v=WPi4S3WniTs).
We may try to make something lighter than it just to skip the simplest mail bots.

The only relatively good solution for this is to generate an address per site so that if email was compromised you can simply block it.
See the idea description bellow.
But again, this doesn't protect from phishing and not all users can recognize spam.

### Block lists
Big email providers don't like to receive letters from independent servers. They are actively exchanging with lists of blocked domains.
Once you get to the list it's almost impossible to get out of it. Your IP may be already blocked years before.
Also they may not like to receive letters from ISP residential area IPs.
See the video [The Death of Decentralization in SMTP](https://www.youtube.com/watch?v=_-eqkiJMnUc)

### Backup SMTP
Your router may be out of power for a long period. Then you'll lose incoming letters. Not a big deal for most users.
Still we should provide a backup SMTP on the jkl.mn and put it to MX record with lower priority.

### Email addresses
If we'll generate an onion like subdomains for jkl.mn that means that users simply can remember their email address.
A browser's autocomplete and password managers can help but if we are going to use per-site generated addresses then a user must each time go to yurt and generate one.



## Email servers
This is a very sad story but currently there is no a good SMTP and POP3 daemons and SMTP clients.
And not many of them are ported to OpenWrt https://openwrt.org/packages/index/mail
Only Postfix, EXIM, EmailRelay and msmtp client.

The first SMTP server called Sendmail and it also provides a command line SMTP client `sendmail` that confuses users.
The Sendmail is just nightmare to configure but it was a default for a long time. Thankfully not anymore.
The Courier server was a popular replacement but it's development stalled.
Now most users use EXIM or Postfix which is easier to configure.
They may also provide their own `sendmail` client just because they anyway need to forward emails to other SMTPs.
The EXIM is too heavy but the Postfix can be installed on a router. Still it needs for a lot of disk space and hard to configure.

If you don't need an SMTP server but just send an email then you can install separately more lightweight `msmtp` client with the `sendmail`.
Interesting that BusyBox also has an extremely simple `sendmail` in about 14 Kb.
But it doesn't have TLS support and don't look for an MX record.
The BusyBox also have a POP3 client but we don't need it.

The OpenSMTPd is probably the simplest to configure and lightweight but it doesn't ported to OpenWrt and will be hard to configure with UCI.

### What can we use?
The basic SMTP and POP3 server in fact can be easily implemented in just hundreds of lines. This is literally a course work for students.
Just few samples:
* https://gist.github.com/PhirePhly/2914635
* https://github.com/joonicks/tmail/blob/master/main.c

I think we can add it to the BusyBox.

msmtpd proxy
* https://marlam.de/msmtp/msmtp.html#Minimal-SMTP-server-_0028msmtpd_0029
* https://github.com/marlam/msmtp-mirror/blob/master/src/msmtpd.c

sendmail with deliver
* https://github.com/richfelker/mxclient dnssec+beartls 
* https://github.com/corecode/dma makes MX lookup

Encryption:
* https://vesmail.email/ e2e encryption email utility

We can postpone this for latter but now start with a custom-built and stripped Postfix.
Or we can use the EmailRelay.

### EmailRelay
The [EmailRelay](http://emailrelay.sourceforge.net/) is a small SMTP and POP3 server written in C++.
It takes about 400Kb so it will never become a part of OpenWrt out of the box.
It also depends on libstdcpp (1mb) and OpenSSL but can be compiled with mbedtls.


Read wiki page about it https://openwrt.org/docs/guide-user/services/email/emailrelay

But it doesn't deliver mail directly to SMTP server e.g. not MX lookup it just forwards it.
Also it's bad for a regular server usage. But this is probably the only one thing that we can get working today.
I failed to configure it https://sourceforge.net/p/emailrelay/support-requests/75/

We need this patches to be applied:
* https://github.com/openwrt/packages/pull/18867
* https://github.com/openwrt/packages/pull/18536
* https://github.com/openwrt/luci/pull/5914

## Retrieve email
But how to read received mails?
The cheapest way is to fetch raw eml files (e.g. via sftp or webdav) and read it as from a local folder with MUA.
Then we don't need the POP3 or IMAP server.

For POP3 or IMAP you have only Dovecot and Cyrus. The Courier also has a POP3 daemon but very old.
Only the Dovecot ported to OpenWrt.
The IMAP protocol is complicated and in fact it just supports folders and long pooling.
It is also possible to use lightweight protocol [JMAP](https://jmap.io) developed by FastMail which is like IMAP but uses JSON-RPC like approach.
The advantage is that the same API may be used for a web client.
But it's complicated and isn't supported yet by most clients.

We can start with only POP3 support. The EmailRelay provides a small POP3 server.
Instead of folders we may just use different mailboxes because we aren't limited to create as many as we wish.
But this won't work nicely in MUA clients.
Anyway, we can have our own Web UI or even our own API.
The API may be even be the same as Gmail uses so that existing Gmail client apps may easily add a support of yurt.
I don't think that the IMAP worth implementing.

## Web UI
For the Web UI we can use the JMAP. We may try to use it with OpenWrt UBUS over JSON-RPC to minimize dependencies.
But for beginning the simplest UI can just work over WebDAV and show a letter by `GET`ting it's file directly from UI.
To send an email we may create a special folder Outgoing and trigger the ER to send all new files in it.
If we anyway have the WebDAV then we don't need any additional software.
Existing Webmail solutions:
* https://github.com/resend/react-email
* https://roundcube.net/

## Generate addresses
Similarly to Gmail `+` addresses:

    You can create variations of your email address where all messages arrive in your current inbox. Just add a plus sign (+) and any word before the @ sign in your current address. Messages sent to your current address or any variation with the plus sign, all arrive in your current inbox. You can then set up filters to route or handle the messages based on the address.
    If your Google Workspace email address is cassy@solarmora.com, you can:
    Sign up for newsletters with cassy+news@solarmora.com
    Let prospective clients or customers contact cassy+questions@solarmora.com
    Tell team members to surface urgent issues in your inbox by contacting cassy+urgent@solarmora.com
    You can then easily find or label messages sent to each address

We may have this feature extended:

1. Temporary address
2. Address for notifications or sites e.g. from noreply@example.com
3. Address for humans: we may respond and ask an additional captcha style question to avoid spam. For friends this check may be avoided.
4. Different folders or priority addresses e.g. urgent@example.jkl.mn or job@example.jkl.mn

We need a UI for this and store addresses because they may be used to restore a forgotten password.


## Sandstorm Email
They give you a subdomain and making all needed configuration of a DNS
https://docs.sandstorm.io/en/latest/administering/email/

## Cloudron Email

The Cloudron is Node.js based self-hosting solution most similar to Sandstorm.
It has build-in email server https://docs.cloudron.io/email/ that uses internally https://nodemailer.com/about/ and have some UI.
This is a very good example.

## Small mail servers and clients

* https://github.com/corecode/dma The DragonFly Mail Agent, a small Mail Transport Agent (MTA), designed for home and office use.
* http://acme.com/software/mini_sendmail/ (has Alpine package)
* https://haraka.github.io/
* https://blog.codinghorror.com/so-youd-like-to-send-some-email-through-code/
* https://www.vultr.com/docs/how-to-create-reverse-dns-or-ptr-records-in-the-vultr-control-panel

## Test
When configuring an email server you can check your rating on  https://www.mail-tester.com

https://toolbox.googleapps.com/apps/messageheader/analyzeheader analyze message headers to see dkim checks and delivery time

See also https://wiki.archlinux.org/title/Mail_server

## Hosting mail or outsourcing?
TL;DR Yes, setup it (if you have a time) but use a free mail (Gmail, iCloud etc.) and slowly try to use your own mailbox.

You have different properties of email:

Can it be public e.g. you publish on your site? If yes, then you'll need a good spam filter.
But also someone may attack you with fishing or DDoS.

Do you want to send email or just receive? If just receive then here you won't have any problems.
But for a sending you'll need to configure DNS with SPF and still your server may be blocked by most popular mail providers.

Should your mailbox be human-readable?
Many just want to have a nice address with own domain which looks cool. You may also need to say your email on phone.

Do you need a good security and privacy?
Generally speaking emails are bad for privacy.
But still if you are using Gmail then basically the Google knows almost everything about you including which sites you are visiting and to where traveling.

Robustness. If you don't have money to pay for your server then you'll lose it.
Also your server may be blocked and disk is full.

How many emails you need to send or receive? For receiving you may reach limit of the email provider.
For making an email campaign you need to use other services like Mailchimp because your server will be blocked quickly.

Lifetime: sometimes you need just a one time usage of email for example to quickly register on some site and just forgot it.

Personal usage can be:

You are registering new account on the mail. Then if you lost your server you'll lose access to many site.
But if you have your own mail server this also increases a security because nobody can't access you mailbox and restore forgotten password on all your sites.
This is unlikely if you don't have any problems with authority.
Also if you have an own server then you can have many mailboxes for each site.
Then if you'll start receive spam then you'll know who leaked your email and can just drop the compromised address.

So here for important sites you may use a free Gmail/iCloud mail but for others sites you may use your own mail server.

You'll receive a notifications from sites e.g. "someone answered to your question". But most time you'll receive some marketing engaging letters from sites where you registered. Here you don't really care about how your address looks like: it can be even a random number. With your server you can generate mail addresses per site.
You're receiving a personal mail (e.g. from a friend). You don't really afraid of spam because you're giving the address only to people whom you know. Here you want for some privacy, but also you need more robustness e.g. you don't want to lose you access. So here is better to use a free mail provider e.g. Gmail, iCloud etc.

I may continue but hope you got the idea.


https://www.reddit.com/r/selfhosted/comments/10k2h3e/comment/j5olqv7/

xampp uses mercury https://en.wikipedia.org/wiki/Mercury_Mail_Transport_System



