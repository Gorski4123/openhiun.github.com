---
layout: post
title:  "Getting php session to work on AWS"
date:   2013-11-15 23:59:59
categories:
permalink: /php-session-on-aws
---
I was digging over a month to getting php session work on Amazon Web Services Elastic Compute Cloud aka AWS EC2. 
It was make me crazy at that time but looking back (Like all digging thus) it's great jearney with quite simple solution.

I was developing PHP social networking application on top of AWS EC2 with nginx, PHP-FPM and Elastic Beanstalk with typical
LAMP stack. After I make some signup and signin feature, I try to both but failure. I really don't know why.

Ths problem is permission. When you see php.ini file which contain whole configuration of your PHP with following commends,

{% highlight php %}
$ find / -name php.ini
/etc/php.ini
$vim /etc/php.ini
{% endhighlight %}

you will find this line on ``session`` section.(approx 1277 line.)

{% highlight php %}
session.save_path = "/sessions"
{% endhighlight %}

This is the problem. You can permission them to 777 for just test. OR maybe folder is dosen't exist.
To successfully save session data, Create folder and make 777 permission by following commends.

{% highlight php %}
$ mkdir /sessions
$ sudo chmod 777 -R /sessions
{% endhighlight %}

Finally restart PHP-FPM for apply setting with following commends.
{% highlight python %}
service php-fpm restart
#or php5-fpm restart
#if you are using ubuntu or centos.
{% endhighlight %}
