---
layout: post
title: "How To Set Up A Personal Server With A Raspberry Pi"
date: 2016-06-28 10:10:52 +0100
categories: blog
permalink: /server.html
---
**(formerly titled: "Full-Stack Computer Projects")**

*If you are reading this on mitchellmclaughlin.com, you are experiencing a technology stack (hardware, software, and design) I built using the tutorials listed below.*

**Table Of Contents:** (more tutorials coming soon...)

1. <a href="#project1">"Setting Up A Personal Web Server With The Raspberry Pi 3"</a> (Appeared as <a href="https://opensource.com/article/17/3/building-personal-web-server-raspberry-pi-3" target="_blank">"How To Set Up A Personal Web Server With A Raspberry Pi"</a> on **Opensource.com**)
2. <a href="#project2">"Building A Personal Website Using A Domain Name, GitHub Pages, Jekyll, Dynamic DNS (Domain Name Server), and Apache"</a>
3. <a href="#project3">"Securing A Website With HTTPS (Let's Encrypt)"</a>
4. <a href="#project4">"Protecting A Website With CloudFlare"</a>
5. <a href="#project5">"Setting Up Web Analytics & Website Monitoring"</a>
6. <a href="https://help.github.com/articles/creating-a-custom-404-page-for-your-github-pages-site/" target="_blank">"Creating A Custom 404 Page For Your Github Page Site"</a>
7. <a href="#project7">"Redirecting www Traffic To non-www With Apache"</a>
8. "Creating A Secure VPN (Virtual Private Network)"
9. <a href="#project9">"Setting Up Cloud-based Storage"</a>
10. "Creating A Secure, Private E-Mail Server"
11. <a href="#project17">"Basic Linux Commands"</a>
12. <a href="#project18">"Screenshots on Linux"</a>

[//]: # 10. "Building A VoIP Service"

[//]: # 11. "Building A SMSoIP Service"

[//]: # 12. "Alexa + Pi"

[//]: # 13. "Building A Computer Cluster"

[//]: # 14. "Building An Open-source Router"

[//]: # 15. "Nintendo NES + Pi"

[//]: # 16. "Temperature Sensor + Pi"

<p id="project1"> </p>**Setting Up A Personal Web Server With The Raspberry Pi 3**

What is the value of building a personal web server?

A personal web server is "the cloud" essentially, except, in this case, you will own and control it. As opposed to a large corporation. And owning a little cloud has a lot of benefits. Customization. Free storage. Free internet services. A path into open-source software. High-quality security. Full control over your content. The ability to make quick changes. A place to experiment with code. And many more. Most of these benefits are immeasurable. But, financially these benefits can save you $100+/month.

AWS (Amazon Web Services) can give you some of these benefits for a small price. I could of used AWS. But, I prefer complete freedom, full control over security, and learning how things are built.

Free Services:

+ Self Web-Hosting -- No BlueHost or DreamHost
+ HTTPS -- Let's Encrypt
+ Analytics -- Google
+ OpenVPN -- Do Not Need Private Internet Access $7/month
+ Cloud Storage -- No Dropbox, Box, Google Drive, Microsoft Azure, iCloud, or AWS
+ On-Premise Security

[//]: # + VoIP (Wifi Calling) -- No Whatsapp, Messenger, etc.

[//]: # + SMS Over IP (Wifi Texting) -- No iMessage, Whatsapp, Messenger, etc.

[//]: # + Alexa + Pi -- Natural Language Processing In The Cloud

[//]: # + Computing Cluster -- On-Demand Computing Resources

Things I Used:

+ Raspberry Pi 3 Model B
+ MicroSD Card (32GB recommended, Raspberry Pi <a href="http://elinux.org/RPi_SD_cards" target="_blank">Compatible SD Cards</a>)
+ USB MicroSD Card Reader
+ Ethernet Cable
+ Router Connected To WiFi
+ Raspberry Pi Clear Plastic Case
+ Amazon Basics MicroUSB Cable (Power Supply)
+ Apple Wall Charger (Power Supply)
+ External Hard Drive (500GB, Storage/Memory)
+ USB Mouse
+ USB Keyboard
+ Amazon Basics HDMI Cable
+ Monitor (With HDMI input)
+ MacBook Pro Running OS X El Capitan

**STEP 1: SETTING UP THE RASPBERRY PI**

Download the most recent release of Raspbian (the Raspberry Pi operating system). <a href="https://www.raspberrypi.org/downloads/raspbian/" target="_blank">Raspbian Jessie</a> ZIP version is ideal<a href="#footnote1">[1]</a>. Unzip/extract the downloaded file. Now, you need to copy it onto the SD card. <a href="http://ivanx.com/raspberrypi/" target="_blank">Pi Filler</a> makes this process easy. Download <a href="http://ivanx.com/raspberrypi/files/PiFiller.zip" target="_blank">Pi Filer 1.3</a> or the most recent version. Unzip/extract the downloaded file again and open it. You should be greeted with this prompt reading "Pi Filler will assist with copying a Raspberry Pi operation system (available at www.raspberrypi.org) to an SD card. If you have already attached your SD card to your Mac, please eject it before continuing."

Make sure the USB card reader has NOT been inserted yet. If it has, eject it. Proceed by clicking continue. A file explorer should appear. Locate the uncompressed Raspberry Pi OS file from your Mac or PC and select it. You should see another prompt reading "Please insert the SD card you want to use for the Raspberry Pi. It should be at least 2 GB (preferably 4 GB or more). It will be completely ERASED. As a precaution, you may want to rename the card to "RASPBERRY" after inserting it, to minimize the chance of confusion with any other disks."

Insert the MicroSD card (32GB recommended, 16GB minimum) into the USB MicroSD Card Reader. Then, insert the USB reader into the Mac or PC. You can rename the SD card to "Raspberry" to distinguish it from others. Click continue. Make sure the SD card is empty. Pi Filler will ERASE all previous storage at runtime. If you need to backup the card do it now. When you are ready to continue, the Raspbian OS will be written to the SD card. It should take between 1-3 minutes. Once the write is completed, eject the USB reader, remove the SD card and insert it into the Raspberry Pi SD card slot. Give the Raspberry Pi power by plugging the power cord into the wall. It should start booting up. The Raspberry Pi default login is:

{% highlight shell %}
username: pi
password: raspberry
{% endhighlight %}

When the Raspberry Pi has completed booting for the first time, a configuration screen titled "Rasperry Pi Software Configuration Tool (raspi-config) and Setup Options" should appear<a href="#footnote2">[2]</a>.

Select the "1 Expand Filesystem" option and hit the enter key<a href="#footnote3">[3]</a>. 

Also, I recommend selecting the 2nd option "change user password". It is important for security. It also personalizes your Raspberry Pi.

Select the 3rd option in the setup options list, "Enable Boot To Desktop/Scratch" and hit the enter key. It will take you to another window titled "choose boot option".

In the "choose boot option" window, select the 2nd option, "Desktop Log in as user 'pi' at the graphical desktop" and hit the enter button<a href="#footnote4">[4]</a>. Once this is done you will be taken back to the "Setup Options" page. If not, select the "OK" button at the bottom of this window and you will be taken back to the previous window.

Once both these steps are done, select the "finish" button at the bottom of the page and it should reboot automatically. If it does not, then use the following command in the terminal to reboot.

{% highlight shell %}
$ sudo reboot
{% endhighlight %}

After the reboot from the previous step, if everything went right, you will end up on the desktop GUI.

Once you are on the desktop, open a terminal and enter the following commands to update the firmware of the Raspberry Pi.

{% highlight shell %}
$ sudo apt-get update
$ sudo apt-get upgrade-y
$ sudo apt-get dist-upgrade -y
$ sudo rpi-update
{% endhighlight %}

This may take a few minutes. Great, now the Raspberry Pi is up-to-date and running. 

**STEP 2: CONFIGURING THE RASPBERRY PI**

**SSH**, which stands for Secure Shell, is a cryptographic network protocol that lets you securely transfer data between your computer and your Raspberry Pi. You can control your Raspberry Pi from your Mac's command line without a monitor or keyboard.

To use SSH, first you need your Pi's IP address. Open the terminal and type:

{% highlight shell %}
$ sudo ifconfig
{% endhighlight %}

If you are using ethernet, look at the "eth0" section. If you are using wifi, look at the "wlan0" section.

Find "inet addr" followed by an IP address - something like 192.168.1.115, a common default IP I will use for the duration of this article.

With this address, open terminal and type:

{% highlight shell %}
$ ssh pi@192.168.1.115
{% endhighlight %}

SSH on PC, see footnote<a href="#footnote5">[5]</a>.

Enter the default password "raspberry" when prompted, unless you changed it.

You are now logged in via SSH.

**REMOTE DESKTOP**

Using a GUI (graphical-user interface) is easier than a command line. On the Raspberry Pi’s command line (using ssh) type:

{% highlight shell %}
$ sudo apt-get install xrdp
{% endhighlight %}

Xrdp supports the Microsoft Remote Desktop Client for Mac and PC.

On Mac, navigate to the app store and search for "Microsoft Remote Desktop". Download it. On PC, see footnote<a href="#footnote6">[6]</a>.

After installation, search your Mac for a program called "Microsoft Remote Desktop". Open it.

Click "New" to setup a remote connection. Fill in the blanks in the table as follows.

{% highlight shell %}
"Connection Name" pi
"PC Name" your_ip_address
"Gateway" select No gateway configured
"Credentials"
"User name" pi
"Password" *************
"Resolution" select Native
"Colors" select True Color (24 bit)
"Full screen mode" select OS X native
select Scale Content
{% endhighlight %}

Save it by exiting out of the "New" window.

You should now see the remote connection listed under "My Desktops". Double-click it.

After briefly loading, you should see your Raspberry Pi desktop GUI in a window on your screen.

Perfect. Now, you don't need a separate mouse, keyboard, or monitor to control the Pi. This is a much more elegant setup.

**STATIC LOCAL IP ADDRESS**

Sometimes the local IP address 192.168.1.115 will change. We need to make it static. Type:

{% highlight shell %}
$ sudo ifconfig
{% endhighlight %}

Write down from the "eth0" section or the "wlan0" section, the "inet addr" (Pi's current IP), the "bcast" (the broadcast IP range), and the "mask" (subnet mask address). Then, type:

{% highlight shell %}
$ netstat -nr
{% endhighlight %}

Write down the "destination" and the "gateway/network".

The culumlative records should look something like this:

{% highlight shell %}
net address 192.168.1.115
bcast 192.168.1.255
mask 255.255.255.0
gateway 192.168.1.1
network 192.168.1.1
destination 192.168.1.0
{% endhighlight %}

With this information, it is easy to set a static internal IP. Type:

{% highlight shell %}
$ sudo nano /etc/dhcpcd.conf
{% endhighlight %}

Do not use /etc/network/interfaces.

Then all you need to do is append this to the bottom of the file, substituting the correct IP address you want.

{% highlight shell%}
interface eth0
static ip_address=192.168.1.115
static routers=192.168.1.1
static domain_name_servers=192.168.1.1
{% endhighlight %}

Once you have set the static internal IP address, reboot the Raspberry Pi with:

{% highlight shell %}
$ sudo reboot
{% endhighlight %}

After rebooting, from terminal type:

{% highlight shell %}
$ sudo ifconfig
{% endhighlight %}

Your new static settings should appear for your Raspberry Pi.

**STATIC GLOBAL IP ADDRESS**

If your ISP (internet service provider) already gives you a static external IP address you can skip ahead to the port forwarding section. If not, continue.

You set up SSH, remote desktop, and a static internal IP address. So, computers inside the local network will know where to find the Pi. But, you still can not access your Raspberry Pi from outside the local wifi network. You need your Raspberry Pi to be publicly accessible from anywhere on the internet. This requires a static external IP address<a href="#footnote7">[7]</a>.

It can be a fragile process initially. Call your ISP and request a static external (sometimes referred to as static global) IP address. The ISP holds the decision-making power, so I would be extremely careful dealing with them. They may refuse your static external IP address request. You can not fault the ISP. There is legal and operational risk with this type of request. They particularly do not want customers running medium-to-large scale internet services. They might explicitly ask why you need a static external IP address. It is probably best to be honest and tell them you plan on hosting a low-traffic personal website or a similar small not-for-profit service. If all goes well, they should open a ticket and call you in a week or 2 with an address.

**PORT FORWARDING**

Great, now you obtained a static global IP address. However, this IP address your ISP assigned is for accessing the router. The Raspberry Pi is still unreachable. You need to set up port forwarding to access the Raspberry Pi specifically.

Ports are virtual pathways where information travels on the internet. You sometimes need to forward a port in order to make a computer, like the Raspberry Pi, accessible to the internet since it is behind a network router. A YouTube video helped me visually understand <a href="https://www.youtube.com/watch?v=iskxw6T1Wb8" target="_blank">ports</a>.

Port forwarding can be used for projects like a Raspberry Pi web server, or applications like VoIP, or peer-to-peer downloading. There are <a href="https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers" target="_blank">65,000+ ports</a> to choose from, so you can assign a different port for every internet applcation you build.

The way to set up port forwarding can depend on your router. If you have a Linksys like I do, this <a href="https://www.youtube.com/watch?v=i1vB7JnPvuE#t=07m08s" target="_blank">video</a> explains how to set it up. If you don't have a Linksys, read the documentation that comes with your router in order to customize and define ports to forward.

You will need to port forward for SSH as well as the remote desktop.

Once you believe you have port forwarding configured, check to see if it is working via ssh by typing:

{% highlight shell %}
$ ssh pi@your_global_ip_address
{% endhighlight %}

It should prompt you for the password.

Check to see if port forwarding is working for remote desktop as well. Open Microsoft Remote Desktop. Your previous remote connection settings should be saved. But, you need to update the "PC name" field with the static external IP address (for example, 195.198.227.116) instead of the static internal address (for example, 192.168.1.115).

Now, try connecting via remote desktop. It should briefly load and arrive at the Pi’s desktop GUI.

Good job. The Raspberry Pi is now accessible from the internet and ready for advanced projects.

As a bonus option, you can maintain 2 remote connections to your Pi. One via the internet and the other via the LAN (local area network). It's easy to setup. In Microsoft Remote Desktop, keep one remote connection called "Pi Internet" and another called "Pi Local". Configure Pi Internet's "PC name" to the static external IP address. For example, 195.198.227.116. Configure Pi Local's, "PC name" to the static internal IP address. For exmaple, 192.168.1.115. Now, you have the option to connect golbally or locally.  

Watch this awesome <a href="https://www.youtube.com/watch?v=i1vB7JnPvuE" target="_blank">video</a> as a transition into project 2. It will show you the techincal architecture behind your project. In this case, you are using a Raspberry Pi instead of a Ubuntu server. The dynamic DNS sits between the domain company and your router, which he leaves out. Beside this subtlety, the video is spot on explaining visually how the system works. You might notice project 1 covered the Raspberry Pi setup and port forwarding. This is the server-side or back end. Project 2 covers the the domain name, dynamic DNS, Jekyll (static HTML generator) and Apache (web hosting). This is the client-side or front end. 

<p id="project2"> </p>**Building A Personal Website Using A Domain Name, GitHub Pages, Jekyll, Dynamic DNS (Domain Name Server), and Apache**

If you already own a domain name skip to the next paragraph. If you need to acquire a domain name I recommend <a href="http://domains.google.com" target="_blank">Google Domains</a> or <a href="http://godaddy.com" target="_blank">GoDaddy</a>.

GitHub Pages are websites built on Jekyll and versioned using a git hosted repository on <a href="http://github.com" target="_blank">GitHub</a>. Jekyll is a simple, blog aware, static site generator. It takes <a href="https://daringfireball.net/projects/markdown/" target="_blank">Markdown</a>, a lightweight markup language, and spits out a complete, static HTML website suitable for serving with Apache or similar web server.

Let's get started by installing Ruby. Ruby is a programming language that uses a package manager called gems. Gems can install Jekyll. From your Raspberry Pi, in terminal type (using ssh or remote desktop):
{% highlight shell %}
$ sudo apt-get install ruby-dev
$ gem install jekyll
{% endhighlight %}

If 'gem install jekyll' fails try:
{% highlight shell %}
$ sudo gem install jekyll
{% endhighlight %}

You can find Jekyll documentation <a href="https://jekyllrb.com/" target="_blank">here</a>. Once you have Jekyll installed, you will want to create a directory for your blog.
{% highlight shell %}
$ jekyll new myblog
{% endhighlight %}

If 'jekyll new myblog' fails, again try:
{% highlight shell %}
$ sudo jekyll new myblog
{% endhighlight %}

Navigate to the myblog directory by typing:
{% highlight shell %}
$ cd myblog
{% endhighlight %}

If you plan on writing to your blog, I recommend installing <a href="http://git-scm.com" target="_blank">git</a>. The blog will evolve over time as content is added. Git creates a snapshot of your blog at some point in time. So, you have the option to rollback a mistake or revert to some point in the past. Git is an amazing tool. It has become widely-accepted as a standard for version control of software. Version control is a far-reaching idea itself. It's a solution to capture the evolution of an information system over time. For exmaple, writing a book, producing a movie, or writing software. It has endless applications in the arts. I witnessed organizations using it as a communication tool. I could forsee it being applied in genetic engineering. If Microsoft Word or PowerPoint crashes, you might recall the ability to recover a document from an earlier time. This is the same underlying version control technology. I could go on. Anyways, to begin install git, type:
{% highlight shell %}
$ sudo apt-get install git
{% endhighlight %}

Add the current folder to git by typing:
{% highlight shell %}
$ git add .
$ git commit -m 'initial commit'
{% endhighlight %}

Once you have git installed and made the initial commit, create a blog home page by typing:

{% highlight shell %}
$ nano index.html
{% endhighlight %}

In index.html, type "hello world". Save the file by hitting control+o (for Mac), then enter. Followed by control+x to exit.
Changes have been made so don't forget to reflect those changes to git. Type:
{% highlight shell %}
$ git add .
$ git commit -m 'created index.html file'
{% endhighlight %}

To test if hello world is working, type:
{% highlight shell %}
$ jekyll serve
{% endhighlight %}

This command tells Jekyll to serve myblog to the local network. You can test your web server by opening a web browser on your server and heading to the URL http://127.0.0.1/.

Check that you can see the website from http://127.0.0.1/. If you see the site, continue. If your server does not run, you may need to reconfigure.

Great, everything is installed and you have generated your site locally. This is a good checkpoint. Moving on, you will install Apache to generate your site to a domain name. Type:
{% highlight shell %}
$ sudo apt-get install apache2
{% endhighlight %}

Apache HTTP Server is the most popular web server technology in the world. As of November 2015, it serves 50% of all websites. It also happens to be the easiest to implement. When I was setting up my web server at first, I mistakenly thought I needed a LAMP architecture. The solution is actually much simpler with Apache.

**Dynamic DNS**

Create a new user account with this free, open-source dynamic DNS service <a href="http://freedns.afraid.org/" target="_blank">here</a>. Write down your user name and password. Once logged in, click the "domains" tab in the navigation panel on the left. You should be taken to this screen (pictured below).
<img src="https://cdn.pbrd.co/images/21wfxQrV.png">

Add your domain name. Once your domain is saved, click "edit secondaries". You should see a list of name servers (pictured below).

<img src="https://cdn.pbrd.co/images/21wuQWlJ.png">

Write down the first 2 name servers. For example, ns1.afraid.org and ns2.afraid.org.

Click "Dynamic DNS" in the navigation panel on the left. You should see a table appear at the bottom of the page (pictured below).
<img src="https://cdn.pbrd.co/images/21y0iZSh.png">

Again, if your domain name is not listed, add it. Then, click "edit record". Fill in the fields.

<img src="https://cdn.pbrd.co/images/239h5Q4W.png">

Repeat this process for the "edit record" of www.yourdomain.com.
<img src="https://cdn.pbrd.co/images/21yn3WKR.png">

DNS settings are now configured. These changes also need to be updated with your domain name provider (Google Domains, GoDaddy, or other).

I used GoDaddy. Upon logging in, I reached this screen (pictured below).
<img src="https://cdn.pbrd.co/images/21wUWa1z.png">

In the domain row, click "Manage". This is the screen I arrived at.
<img src="https://cdn.pbrd.co/images/21x2Y2Nj.png">

Click the gear icon and select "Manage DNS". Then, update the name servers (pictured below).

<img src="https://cdn.pbrd.co/images/21x9aKoh.png">

Allow up to 24 hours for the changes to be processed. After the waiting period, you can test the new configuration by typing:
{% highlight shell %}
$ ping your_domain_name
{% endhighlight %}

If all goes well, the pings should return data packets from your global IP address (pictured below).
<img src="https://cdn.pbrd.co/images/21xtKqH1.png">

To stop pinging, hit control+c.

Your domain name is now configured with a dynamic DNS.

The last hurdle is connecting all these pieces together, the domain name on top of the dynamic DNS (server-side), the GitHub Page on top of Jekyll and Apache (client-side).

Apache uses a VirtualHost to serve HTML files to the web. Some minor configurations are needed to tell it where to find the HTML files. From the Raspberry Pi, open terminal and type:
{% highlight shell %}
$ nano /etc/apache2/sites-available/000-default.conf
{% endhighlight %}

Copy the configurations (pictured below).
<img src="https://cdn.pbrd.co/images/21zDiUk8.png">
<img src="https://cdn.pbrd.co/images/21zB4hxe.png">

Repeat this process for the encrypted VirtualHost.
{% highlight shell %}
$ nano /etc/apache2/sites-available/000-default-le-ssl.conf
{% endhighlight %}

Copy the configurations (pictured below) except for the Let’s Encrypt section.
<img src="https://cdn.pbrd.co/images/21zRNWsK.png">
<img src="https://cdn.pbrd.co/images/21A1qw75.png">

For security reasons, the Apache web server does not listen to port 80 (http) or port 443 (https) by default. You need to open these for incoming web traffic requests. Type:
{% highlight shell %}
$ cd /etc/network
$ sudo iptables -A INPUT -p tcp - -sport 80 -j ACCEPT
$ sudo iptables -A INPUT -p tcp - -sport 443 -j ACCEPT
$ sudo iptables -L
$ sudo iptables-save
{% endhighlight %}

Your shell should return something similar to this (pictured below).
<img src="https://cdn.pbrd.co/images/21BxyDbm.png">

If you want to understand iptables, read the <a href="https://fedoraproject.org/wiki/How_to_edit_iptables_rules" target="_blank">documentation</a>.

To test ports at anytime, go to a browser and type your_domain_name:80 or your_domain_name:443.
<img src="https://cdn.pbrd.co/images/21BJNyaC.png">

Port 443 probably will not work yet since HTTPS is not set up. Port 80 should work. We will get to HTTPS in a <a href="#project3">later tutorial</a>.

You need build your website with Jekyll in the root directory of Apache. Navigate to the myblog directory. Type:
{% highlight shell %}
$ cd myblog
$ sudo jekyll build -d /var/www/html
{% endhighlight %}

This is Jekyll's way of spiting out the HTML documents to Apache’s root directory to be served to the web. The command line should return something like this (pictured below).

<img src="https://cdn.pbrd.co/images/21Cxrcvh.png">

Enter your domain name into a browser as a comprehensive final test. If you did it right, it should reveal your website. This was mine after completion (pictured below).

<img src="https://cdn.pbrd.co/images/21BYlHuL.png">

If you got this far, you are doing a hell of a job. Keep it up.

If you ever want to change the design of your website, check out this <a href="https://github.com/jekyll/jekyll/wiki/sites" target="_blank">list</a> of examples.

Watching this <a href="https://www.youtube.com/watch?v=i1vB7JnPvuE" target="_blank">video</a> again might crystallize your understanding of how the system works. 

<p id="project3"> </p>**Securing A Website With HTTPS (Let's Encrypt)**

<a href="https://letsencrypt.org" target="_blank">Let's Encrypt</a> is a certificate authority that provides free certificates for transport layer security (TLS) encryption via an automated process.

Have you ever landed on a red-padlocked webpage? It's because HTTPS is not enabled.

<img src="https://cdn.pbrd.co/images/231WqgM9.png">

In order to install Let's Encrypt on your server, you need to have the git package installed. If you installed git during the <a href="#project2"Jekyll tutorial</a>, skip this step. Otherwise, open terminal and type:

{% highlight shell %}
$ sudo apt-get install git
{% endhighlight %}

You need to navigate to the location you want to install Let's Encrypt. I recommend /myblog. Type:

{% highlight shell %}
$ cd ./myblog
$ sudo git clone https://github.com/letsencrypt/letsencrypt
{% endhighlight %}

Start the process of obtaining a SSL Certificate for Apache by typing:

{% highlight shell %}
$ cd /myblog/letsencrypt
$ sudo ./letsencrypt-auto
{% endhighlight %}

This should launch you into the blue setup screen.

<img src="https://cdn.pbrd.co/images/2335OJVV.png">

Agree to the Terms of Service. Enter your email address.

<img src="https://cdn.pbrd.co/images/233d9QMw.png">

"No names were found in your configuration files." Continue by selecting "Yes".

<img src="https://cdn.pbrd.co/images/233y1pnM.png">

Enter your domain names separated by commas. For example, I entered "mitchellmclaughlin.com, www.mitchellmclaughlin.com".

<img src="https://cdn.pbrd.co/images/233HXt50.png">

Select and modify option #3 "000-default-le-ssl.conf" file as shown below.

<img src="https://cdn.pbrd.co/images/233V0Dng.png">

<img src="https://cdn.pbrd.co/images/233ZNaWI.png">

Choose whether HTTPS access is required or optional. I recommend using "Secure".

<img src="https://cdn.pbrd.co/images/234kAqH8.png">

If the process worked properly, you will receive a follow-up message.

<img src="https://cdn.pbrd.co/images/234AA6RD.png">

You should also receive a congratulatory message and a URL to test your HTTPS.

<img src="https://cdn.pbrd.co/images/234MN2bD.png">

Test your domain.

<img src="https://cdn.pbrd.co/images/234QwOYt.png">

At this point, you have one final job. The certificates issued by Let's Encrypt expire every 90 days for security reasons. When they expire, you can execute a simple command to renew certificates. Type:

{% highlight shell %}
$ ./letsencrypt-auto renew
{% endhighlight %}

<img src="https://cdn.pbrd.co/images/234U6JTe.png">

Your certificates should be up to date. Success.

<p id="project4"> </p>**Protecting A Website With CloudFlare**

CloudFlare is an internet security service. It partly functions like a content delivery network (CDN). A content delivery network is a fancy term to describe a software networking technology which stores assets of a website like text, images, and other metadata locally for a geographic area. It speeds up user-side access to your website. CloudFlare also protects your website from unwanted threats like a distributed denial-of-service (DDoS) attack. For DDoS attacks, CloudFlare functions like a reverse proxy load-balancer against incoming web requests.

Let's get CloudFlare setup now. Go to <a href="http://cloudflare.com" target="_blank">cloudflare.com</a>. Create a new user account. It should then prompt you for your domain name. Continue by verifying your DNS records. Select a CloudFlare plan. I chose the free/basic plan. If all goes well, it should return CloudFlare name servers. Similar to my name servers pictured below.
<img src="https://cdn.pbrd.co/images/21dTNXS7.png">

Change your old DNS name servers to the new CloudFlare name servers. Once you make the change, allow up to 24 hours for processing.

<p id="project5"> </p>**Setting Up Web Analytics & Website Monitoring**

I like data. Web analytics is an easy way to learn more about your audience. If you try something new on your website, it's nice to receive feedback. Over time, analytics will help you feed the audience's desires.

I considered Google Analytics, Piwik, and Hotjar. Piwik was clunky and hard to implement. Hotjar was missing basic website metrics. So, I chose Google Analytics. It's easy to implement and lightweight.

Go to <a href="http://analytics.google.com" target="_blank">Google Analytics</a>. Create an account. If you already have a gmail account you might be able to sign in with it. After signing up, you will be given a "tracking code". This is code to be embedded into the HTML code of your website. Embed it. It should take a few hours to process. Once the waiting period is over, you can start creating dashboards with a variety of metrics.

Website monitoring can be used as a notification tool to alert you when your website crashes. I use <a href="http://uptimerobot.com" target="_blank">UptimeRobot</a>. Create an account and link your domain and you will be alerted if something crashes.

<p id="project7"> </p>**Redirecting www Traffic To non-www With Apache**

Shortly after I got my website working, I tested a variety of URL entry points. For example, mitchellmclaughlin.com, http://mitchellmclaughlin.com, https://mitchellmclaughlin.com, and mitchellmclaughlin.com:80 all correctly redirected to https://mitchellmclaughlin. But, www.mitchellmclaughlin.com and http://www.mitchellmclaughlin.com both landed at www.mitchellmclaughlin.com. Although viewable, there is a subtle problem. In the latter instances, HTTPS is not enabled. Ideally, all www traffic should be redirected to mitchellmclaughlin.com which further redirects to https://mitchellmclaughlin.com (a HTTPS enabled URL). The www and non-www discrepancy orignated from the invention of the world wide <a href="http://en.wikipedia.org/wiki/World_Wide_Web#WWW_prefix" target="_blank">web</a>. And <a href="http://computer.howstuffworks.com/internet/basics/question180.htm" target="_blank">"Why Do Some Websites Include www In The URL While Others Don't?"</a>.

Fortunately, the solution is quick and easy. I will warn you, I strongly advise against using the RewriteEngine solution. In the Pi terminal, type:

{% highlight shell %}
$ cd /etc/apache2/sites-available
$ sudo nano 000-default.conf
{% endhighlight %}

Find "</VirtualHost>", above that line type and insert:

{% highlight shell %}
ServerName www.yourdomain.com
Redirect permanent / http://yourdomain.com
{% endhighlight %}

The results should look like my configuration settings below.

<img src="https://cdn.pbrd.co/images/b9fUtIoln.png">

Save the changes to the file. There is nothing magical about doing it in the other direction. Simply swap www.youdomain and yourdomain.

Please remember, if you have configured Apache differently than I have in the preceeding projects this probably will not work.

After the changes have been saved, restart Apache.

{% highlight shell %}
$ sudo reboot
{% endhighlight %}

Test your new configuration settings by typing the www URLs into a browser. It if worked, you are successful.

I purposefully did not mention https://www.mitchellmclaughlin.com because as far as I know, it is not a valid http request. Same goes for mitchellmclaughlin.com:443.

<p id="project9"> </p>**Setting Up Cloud-based Storage**

Things I Used:

+ Seagate 1TB External Hard Drive
+ USB 2.0 Powered Hub

First, decide what you will be using for external storage. I picked a 1TB USB hard drive from Seagate. The Raspberry Pi does not have enough power to run most external hard drives or SSDs, so unless you have a drive with its own power supply, you will probably need a powered USB hub. Once you have the supplies, plug in the USB powered hub into a USB port on the Raspberry Pi. Then, plug in the external hard drive into a USB port on the USB powered hub. A folder should appear on the desktop of the Raspberry Pi. That's it. You can now download and upload files to this folder on-demand. To increase the amount of storage, simply add more external hard drives.

<p id="project17"> </p>**Basic Linux Commands**

{% highlight shell %}
network settings: $ sudo ifconfig
memory management tool: $ df -h
expand filesystem or change password: $ sudo raspi-config
linux display appearance: $ lxappearance
file transfer: $ scp /Users/mitchell/myblog.zip pi@your_ip_address:/home/pi
$ ssh pi@your_ip_address
$ ping your_ip_address
file permissions: $ chmod +x file-name.run, then ./file-name.run
$ sudo ./file-name-run
empty trash: $ rm -rf ~/.local/shared/Trash/*
reboot: sudo reboot
{% endhighlight %}

<p id="project18"> </p>**How To Take Screenshots On Raspberry Pi**

To take screenshots, open terminal and execute:
{% highlight shell %}
$ scrot
{% endhighlight %}

Here is how you would run scrot with a 10 second delay:
{% highlight shell %}
$ scrot -d 10
{% endhighlight %}

*If you want to contribute to this project, liked it, got stuck, or found errors, drop me a message at mitch(dot)mclaughlin1(at)gmail(dot)com.*

**Notes**
<p id="footnote1"> </p>[1] I do not recommend starting with the NOOBS operating system. I prefer starting with the fully-functional Raspbian Jessie operating system.
<p id="footnote2"> </p>[2] If "Setup Options" did not pop-up, you can always find it by opening terminal and executing this command:
{% highlight shell %}
$ sudo-rasps-config
{% endhighlight %}
<p id="footnote3"> </p>[3] We do this to make use of all the space present on the SD card as a full-partition. All this does is, expand the operating system to fit the whole space on the SD card which can then be used as storage memory for the Raspberry Pi.
<p id="footnote4"> </p>[4] We do this because we want to boot into the desktop environment which we are familiar with. If we do not do this step, the Raspberry Pi boots into a terminal each time with no graphical-user interface.
<p id="footnote5"> </p>[5] The prompt should be titled "PuTTY Config". "Basic options for your PuTTY session", then "Specify the destination you want to connect to", then "Host Name (or IP address)" which I entered, {% highlight shell %} 192.168.1.102 {% endhighlight %} then "Port" which I entered, {% highlight shell %} 22 {% endhighlight %} and finally "Connection Type" select SSH.

Download and run <a href="http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html" target="_blank">PuTTY</a> or another SSH client for Windows. Enter your IP address in the field, as shown in the above screenshot. Keep the default port at 22. Hit enter, and PuTTY will open a terminal window which will prompt you for your username and password. Fill those in, and begin working remotely on your Pi.
<p id="footnote6"> </p>[6] If it is not already installed, download <a href="https://www.microsoft.com/en-us/store/apps/microsoft-remote-desktop/9wzdncrfj3ps" target="_blank">Microsoft Remote Desktop</a>. Search your computer for Microsoft Remote Desktop. Run it. Input the IP address when prompted. Next, an xrdp window will pop up, prompting you for your username and password.
<p id="footnote7"> </p>[7] The router has a dynamically assigned external IP address. So in theory, it can be reached from the internet momentarily. But, we need the help of your ISP to make it permanently accessible. If this was not the case, the remote connection would need to be reconfigured on each use.

**Sources**

Orsini, Lauren. <a href="http://readwrite.com/2014/04/09/raspberry-pi-projects-ssh-remote-desktop-static-ip-tutorial/?awesm=readwr.it_b1UN" target="_blank">Raspberry Pi Projects SSH Remote Desktop Static IP Tutorial</a>

Pai, Akshay. <a href="https://www.howtoforge.com/tutorial/howto-install-raspbian-on-raspberry-pi/" target="_blank">How To Install Raspbian On Raspberry Pi</a>

<a href="https://pi-hole.net/faq/how-do-i-set-a-static-ip-address-in-raspbian-jessie-using-etcdhcpcd-conf/" target="_blank">How Do I Set A Static IP Address In Raspbian Jessie</a>

<a href="https://www.youtube.com/watch?v=i1vB7JnPvuE" target="_blank">How To Go Online With Your Apache Server</a>

**Further Reading**

+ <a href="http://raspberrywebserver.com/serveradmin/get-your-raspberry-pi-web-site-on-line.html" target="_blank">Get Your Raspberry Pi Website Online</a>
+ <a href="https://jekyllrb.com" target="_blank">Jekyll Documentation</a>
+ <a href="https://fedoraproject.org/wiki/How_to_edit_iptables_rules" target="_blank">How To Edit Iptables Rules</a>
