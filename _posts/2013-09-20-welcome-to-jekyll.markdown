---
layout: post
title:  "Welcome to Jekyll!"
date:   2013-09-20 15:11:26
categories: jekyll update
---

You'll find this post in your `_posts` directory - edit this post and re-build (or run with the `-w` switch) to see your changes!
To add new posts, simply add a file in the `_posts` directory that follows the convention: YYYY-MM-DD-name-of-post.ext.

`_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts``_posts`

Jekyll also offers powerful support for code snippets:

{% highlight perl %}
from django.shortcuts import render_to_response
from article.models import Article

# Create your views here.

def articles(request):
  return render_to_response('articles.html',
                           {'articles': Article.objects.all() })

def article(request, article_id=1):
  return render_to_response('article.html',
                           {'article': Article.objects.get(id=article_id) })
{% endhighlight %}

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll's GitHub repo][jekyll-gh].

[jekyll-gh]: https://github.com/mojombo/jekyll
[jekyll]:    http://jekyllrb.com
