---
layout: post
title:  "Getting php session to work on AWS"
date:   2013-11-15 23:59:59
categories: e
permalink: /php-session-on-aws
image: http://farm4.staticflickr.com/3693/11309946673_28eddf748c_o.jpg
---
I was digging over a month to getting php session work on Amazon Web Services Elastic Compute Cloud aka AWS EC2. 
It was make me crazy at that time but looking back (Like all digging thus) it's great jearney with quite simple solution.

I was developing PHP social networking application on top of AWS EC2 with nginx, PHP-FPM and also Elastic Beanstalk with typical
LAMP stack for testing. After I make some signup and signin feature, I try to both but failed. I really don't know why.

Ths problem is permission. When you see php.ini file which contain whole configuration of your PHP with following commends,

{% highlight bash %}
$ find / -name php.ini
/etc/php.ini
$ vim /etc/php.ini
{% endhighlight %}

you will find this line on session section.(approx 1277 line.)

{% highlight ini %}
session.save_path = "/your/session/path"
{% endhighlight %}

If i want to store session data in ``/sessions`` directory, change directory you want to store session.

{% highlight ini %}
session.save_path = "/sessions"
{% endhighlight %}

Finally create folder and change permission to 777 by following commends.

{% highlight bash %}
$ mkdir /sessions
$ sudo chmod 777 -R /sessions
{% endhighlight %}

If permission is 777 then PHP-FPM process can write data into folder. and immediately session will work.
so **it's all about permission is matter!**

Finally restart PHP-FPM for apply setting with following commends.
{% highlight bash %}
$ service php-fpm restart
//for php-fpm on ubuntu or centos with nginx
$ service php5-fpm restart
//for php on apache
$ apachectl restart
{% endhighlight %}

After restart I guess session will working correctly. It not only solution for PHP on AWS but solution for PHP on whole linux based system.
I hope this will helpful to you!

*Header Picture by <a href="http://www.flickr.com/photos/11904001@N00/3304736754/">Flickr</a> with <a href="http://creativecommons.org/licenses/by-nc-sa/2.0/">CC BY-NC-SA 2.0 License</a>*
