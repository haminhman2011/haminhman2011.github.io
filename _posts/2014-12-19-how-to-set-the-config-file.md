---
layout: post
title: Ubuntu overview
modified: 2015-01-17
categories: [articles, Howto]
tags: 
  - configure
comments: true
---

**First part** Reach out and touch it

Enjoy the simplicity of Ubuntu's intuitive interface. Fast, secure and with thousands of apps to choose from, the sleek Ubuntu desktop experience is now optimised for multitouch devices, including laptop trackpads and touchscreens, as well as the familiar keyboard and mouse.

**Part 2** Smarter searching.

Ubuntu 14.04 LTS includes a wealth of smart filters to make it faster and easier to find the content you need, whether it’s stored on your computer or on the web.

Type any query into the Dash home and the Smart Scopes server will determine which categories of content are the most relevant to your search, returning only the best results. The server constantly improves its results by learning which categories and results are most useful to you over time.

{% highlight YAML %}
twitter_username: #your twitter handle  
github_username:  #your github account
disqus_shortname: #disqus shortname
favicon:     "images/favicon.ico"
aboutme: Hi, this is Lijia Yu. I made the Freshman21 theme. Please enjoy it. # these are shown on aboutme-box(sidebar).
aboutme_photo: http://assets.ubuntu.com/sites/ubuntu/1253/u/img/desktop/features/image-scopes.jpg # your personal photo.
{% endhighlight %}

**Part3**, Site setting:

{% highlight YAML %}
ShowContactInfo: "True" # Personal Info (twitter,github,email) can be seen on aboutme-sidebar, those info only shown where ShowContactInfo == True
default_column: "two" # blog style: two columns, if default_column != "two", you will see a one column blog.
default_locale: "en" # blog sidebar language set, only include: English(en) and Chinese (cn)
{% endhighlight %}


**Part4**, Blogroll info, only *name* tags can shown on the page.

{% highlight YAML %}
Blogroll:
      - name: Freshman
        href: http://yulijia.net/freshman
        title: Another Jekyll blog theme
      - name: author's website
        href: http://yulijia.net/
        title: Lijia Yu's website
{% endhighlight %}

**Part5**, Build settings

{% highlight YAML %}
markdown: kramdown
highlighter: pygments # highlight
paginate: 5  # how many post can seen in the main page
{% endhighlight %}

=====

<ul style='list-style-type:none;'> 
<li id="[1]"> [1], you can set those info at <strong>Part3</strong> or just delete the <q>aboutme.html</q> at <q>sidebar.html</q> in <code>_include</code> folder. </li>
</ul>

{% highlight HTML %}
<div class="col-sm-2">
  <!--\{\% include Aboutme.html \%\}-->
  \{\% include Copyright_Notice.html \%\}
  \{\% include Resent_Posts.html \%\}
  \{\% include Categories.html \%\}
  \{\% include Tags.html \%\}
  \{\% include Blogroll.html \%\}
  \{\% include Archives.html \%\}
</div>                                                                                                      
{% endhighlight %} 

