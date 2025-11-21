# Disk space

Routers have a very limited disk space.
You can strip OpenWrt firmware for TpLink WR740N by removing non-critical features like LUCI down to 2mb.
So on the 4mb router this gives 2mb of available space.
My [blog](https://stokito.wordpress.com/) when exported to RSS without images and compressed with gzip is about 2.3mb.
So basically even 2mb of the cheapest 4mb router is enough for a basic blog.

For basic usage when you need to receive and store emails and messages even 2mb are enough.
Then your email client can just download received mail for today and cleanup the mailbox.

The bigger problem is that routers have a flash that is not intended for many writes.
You can just brick your router if you'll write on it each day.

The router also has 32mb of RAM but after reloading everything stored there will be lost.

If we have two routers in different location then you can back up or share some data to the second router's RAM.
If one was rebooted then it can restore data from the second router.
This "friends in-memory cloud" may solve a lot of problems.
And the memory is going to be more available than flash storage in many cases.
After the router receives the live data (email, chat, etc.), it can encrypt it and store it online "in the cloud" (or on the router of one of our friend) and only hold onto the encryption key (or use public key cryptography).
Then it could serve the content to the user on demand as if it was stored locally.


If you have 16mb router then you have a USB and you can put a usual USB flash stick.
Today everybody have them at home.
They'll work slowly, but they have few Gb of space.

Also you may install yurt on other devices like TV, phone or even vacuum cleaner robot, and they also have few Gb of space.

And finally, you can connect a USB external disk. Today you can buy 1Tb for sane money.
It's enough to have one such disk for a family, and you can share it with friends.
Interesting is that cloud providers selling 1Tb of disk space for less money that the 1Tb disk divided on time of its warranty.
This is probably because they oversell the disk space or maybe because they are buying disk wholesale and using cheaper energy.
Users may use any cloud provider, and we can just encrypt all files so it will remain safe for users.
The files metadata may be stored on the yurt for a quick search.

To make it easier the jkl.mn website also must sell a storage cloud so that inexperienced users will have an easy and integrated solution.
