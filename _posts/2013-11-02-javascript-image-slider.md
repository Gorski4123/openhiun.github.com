---
layout: post
title:  "Instagram, Y Combinator like javascript image slider"
date:   2013-10-21 15:48:50
categories:
permalink: /javascript-image-slider
---

I love startup and startup services. When I saw image slider in instagram in web interfaces, 
I just fall in love about the elegant, smooth fade effect. After few month I starting my own startup to solve 
problem about bring people together in on-offline, I googled simple image slider. which instagram and Y Combinator's 
main page are using.

It works like this.

<iframe width="100%" height="300" src="http://jsfiddle.net/6enP8/embedded/result" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

It is quiet simple. just check the code below.

{% highlight html %}
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1/jquery.min.js" type="text/javascript"></script>
<script type="text/javascript">
$(function () {
    $('.fadein img:gt(0)').hide();
    setInterval(function () {
        $('.fadein :first-child').fadeOut(1000).next('img').fadeIn(1000).end().appendTo('.fadein');
    }, 5000);
});
</script>

<style type="text/css">
.fadein { position:relative; height:250px; width:500px; }
.fadein img { position:absolute; left:0; top:0; }
</style>
</head>
<body>
<div class="fadein">
<img src="https://farm8.staticflickr.com/7299/10734165323_2771813937.jpg">
<img src="https://farm3.staticflickr.com/2879/10733946656_236d5ef400.jpg">
<img src="https://farm4.staticflickr.com/3692/10733946706_57768954ec.jpg">
<img src="https://farm6.staticflickr.com/5549/10734165073_a936b80780.jpg">
<img src="https://farm4.staticflickr.com/3792/10734164913_fe46b412aa.jpg">
<img src="https://farm8.staticflickr.com/7434/10733859955_d39c684fb2.jpg">
</div>
</body>
</html>
{% endhighlight %}

Are you getting it?? see the javascript code. it's really simple even begineer like me. 
I always sneak peek javascript code but this time i actually write and customizing this little code. ;)

{% highlight javascript %}
$(function () {
    $('.fadein img:gt(0)').hide();
    setInterval(function () {
        $('.fadein :first-child').fadeOut(1000).next('img').fadeIn(1000).end().appendTo('.fadein');
    }, 5000);
});
{% endhighlight %}

``fadeIn``and``fadeOut`` means how much time to run fading animation. and lastly ``5000`` means show each image while 5000 micro seconds 
aka 5 seconds. Every animation effect is powered by jQuery javascript library. ``fadeIn()``and ``fadeOut()`` called api.
if you want learn more check out [this][jquery-fade-api].

[jquery-fade-api]: http://api.jquery.com/category/effects/fading/
