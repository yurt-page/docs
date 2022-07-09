# Email
EMail is a corner stone of web, and it's important to give users and ability to send and receive them. You may not have anything except of email.
Good news is that EMail is already non-centralized. But it's too hard to use and especially hard to configure.
But most users for personal needs using silos: GMail, Hotmail, Yahoo, Yandex, iCloud. They have good anti-spam filters, but they're selling their users. Most users using http to check mail.
Others using corporate email from their job or universities. They are mostly use MUA (Outlook, Thunderbird) but sometimes corporate email is based on silos (Microsoft Office 365).
Small amount of regular users using email from their internet provider (GMX) because they already have it.
Advanced users buys paid email services: Proton Mail, FastMail, Zoho.

Most emails of regular users are just simply notifications and marketing.
Emails are very important for privacy. If you read someone's email you know what they buy, what websites they visit, what happens in their life.
If email hacked then you can reset passwords on all websites.

We must provide at least ability to receive email. This will already cover 98% of usage.
But how to read received mails?
The simplest way to read them from MUA may download raw eml files (e.g. via sftp) and read it as from a local folder.
Or we may add a POP server. But it may be better to use lightweight JMAP but maybe we even can change it slightly to use JSON-RPC.

## EmailRelay
The [EmailRelay](http://emailrelay.sourceforge.net/) small SMTP and POP server which takes about 400Kb.
https://openwrt.org/docs/guide-user/services/email/emailrelay

The postfix is also applicable but it's much harder to configure it.

## Web UI
A simplest UI can just work over WebDAV and show a letter by downloading it's file.
To send an email we may create a special folder Outgoing and trigger the ER to send all new files in it.
