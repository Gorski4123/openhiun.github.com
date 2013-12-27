---
layout: post
title:  "Developing Server Application on Chromebook"
date:   2013-12-28 21:52:45
categories: e
permalink: /developing-server-application-on-chromebook
image: http://farm8.staticflickr.com/7404/11586972615_ff9e65e848_o.jpg
---

Last summer I got Samsung series 5 chromebook and trying to find way to developing PHP and NodeJS. 
Best way is install Linux beside on Chrome OS. And yet obviously Chrome OS is based on Linux at the beginning.

##Considerations

1.Coding
The main reason I want to developing on Chrome OS is performance. Chrome OS has quiet amazing performance for their hardware. I think the reason is optimization to purpose and restriction by Google. So Chrome OS os best place to googling and copy and pasting code and of course writing code. 

2.OS
Chromebook is built on top of linux. But we can't install PHP and NodeJS on Chrome OS natively. So we need to install Linux such as Ubuntu on alongside of Chrome OS.

There are 3 options.

- Install GUI Ubuntu natively.

- Install GUI Ubuntu on Chrome OS with crouton.

- Install CLI Ubuntu on Chrome OS with crouton.

As I said Chrome OS is pretty good for non-developing purpose stuff like web browsing for their hardware. I prefer to use Chrome OS for non-develpment stuff. GUI and CLI.. I prefer CLI to run software natively. We all familar to using SSH to linux server, and we don't need to another heavy-GUI OS on Chrome OS.

3.Integration
Integration is no-big deal. Just file sharing between Chroms OS and CLI ubuntu. The sharepoint is `Downloads` folder.

##Install Ubuntu

1.Download crouton at here [http://goo.gl/fd3zc](http://goo.gl/fd3zc).

2.Ctrl+Alt+T, type shell and hit enter.

3.Before installation you have to choose which OS and Version. To show available version type `~/Downloads/crouton -r ist` on the shell

And if you want to install Ubuntu 13.04 type `sh -e crouton -r raring -n ubuntu -t cli-extra`. You may notice `-r`is version code and `-n`is OS name and -t is type of GUI or CLI. More info in [official Github repo](https://github.com/dnschneid/crouton#i-dont-always-use-linux-but-when-i-do-i-use-cli).

4.After finishing install, That's It!! You've got fine new linux on Chrome OS!! You can install any application you used to.

##Code Editor

I think the best javascript based code editor on the planet is caret. It's called Sublime Text for Web. So we are gonna use this.
Just Install [caret](https://chrome.google.com/webstore/detail/caret/fljalecfjciodhpcledpamjachpmelml?hl=en) and use it! gorgeous text editor ever!

##Coding Fonts

I am extremely worried about fonts. But there is a way to do that. check out [here](http://blog.promevo.com/how-to-install-fonts-for-your-series-5-chromebook/)!
