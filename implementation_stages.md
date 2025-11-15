There is different stages to implement the project of self-hosting at home on cheap devices:
1. Compile my own OpenWrt firmware with everything needed or disabled for 16mb routers. Here we can compile the Lighttpd and pre-configure it.
  1.1 Prepare image for RaspberryPI and Ubuntu to use on microcomputers and VPS.
3. Then try to make everything work on a vanilla OpenWrt but with additional configuration. Ideally just copy files but some SSH and command may be needed. Here we need to make a configuration atomic in separate files so that a package update won't override a config file. Also for the vanilla OpenWrt we need to install the Lighttpd.
4. Try to make the vanilla OpenWrt to have the functionality out of the box. I'll have to ask OpenWrt devs to include all needed functionality (I already sent few patches). A user should just click on UI to enable WebDAV. But this means that I have to use the uhttpd only and it doesn't have the WebDAV. The WebDAV CGI might help here.
5. Support of smaller devices e.g. 4mb. Here I'm thinking to use the BusyBox httpd (8kb) and again the WebDAV CGI is the only option.

So at this moment I'm on the stage 1 but anyway I'm trying to make some work for the future stages or at least to understand better.

