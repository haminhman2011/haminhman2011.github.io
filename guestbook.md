---
layout: post
title: jQuery 
comments: yes
permalink: /guestbook/

---
![Elaphurus davidianus](http://zlatanblog.com/wp-content/uploads/picture/fullscreen-page.jpg "Père David's deer")

## Create fullscreen slideshow with slides and jQuery plugin
Today's article will guide you to use slides and .resize plugin () event in jQuery to create a slideshow full sceen.
First we need to prepare jquery plugin slides and photos. You can go here to download:
http://slidesjs.com/ 
### Starting with HTML code.
{% highlight Bash shell scripts linenos%}
<div class="fullscreen">
    <div class="slides_container">
        <div class="slide">
            <img src="img/slide_1.jpg" alt="slide-1"/>
        </div>
        <div class="slide">
            <img src="img/slide_2.jpg" alt="slide-2"/>
        </div>
        <div class="slide">
            <img src="img/slide_3.jpg" alt="slide-3"/>
        </div>
        <div class="slide">
            <img src="img/slide_4.jpg" alt="slide-4"/>
        </div>
        <div class="slide">
            <img src="img/slide_5.jpg" alt="slide-5"/>
        </div>
        <div class="slide">
            <img src="img/slide_6.jpg" alt="slide-6"/>
        </div>
    </div><!--end slide container-->
     
    <div class="pagination_container">
        <ul class="pagination">
            <li class="current"><a href="#1"><img src="img/slide_1.jpg" width="137px" height="67px"/></a></li>
            <li><a href="#2"><img src="img/slide_2.jpg" width="137px" height="67px"/></a></li>
            <li><a href="#3"><img src="img/slide_3.jpg" width="137px" height="67px"/></a></li>
            <li><a href="#4"><img src="img/slide_4.jpg" width="137px" height="67px"/></a></li>
            <li><a href="#5"><img src="img/slide_5.jpg" width="137px" height="67px"/></a></li>
            <li><a href="#6"><img src="img/slide_6.jpg" width="137px" height="67px"/></a></li>
        </ul>
    </div><!--pagination-->
</div><!--end fullscreen-->
{% endhighlight %}
It is for the entire slideshow div.fullscreen, inside which contains the image slide div.slides_container card div.pagination_container card also contains the navigation buttons. NOTE let li card containing images and current first class turn to the href attribute of each card is a # 1 to # 6 (depending on the number of images).

### Slides Using jQuery Plugin.
To download the plugin on our slides embedded link it to the head of the jQuery library.
{% highlight Bash shell scripts linenos%}
<head>
    <script src="javascript/jquery.js"></script>
    <script src="javascript/slides.min.jquery.js"></script>
</head>
{% endhighlight %}
Then call the plugin with the following code
{% highlight Bash shell scripts linenos%}
(function($){
$(window).load(function(){
 
    // slides plugin
    $('.fullscreen').slides({
        generatePagination: false,  // disable automatically add the default navigation buttons
        prependPagination: true,  // create button enabled navigation
        effect:'fade',
        play:6000,  // time the slide show
        pause:1, 
        crossfade: true,
    });
 
});
})(jQuery);
{% endhighlight %}

### Uses CSS to create the interface.
{% highlight Bash shell scripts linenos%}
.fullscreen{
    position:fixed;
    z-index:0;
    width:100%;
    height:100%;
    left:0;
    top:0;
}
 
.slide img{
    width:100%; 
    height:100%;
}
 
.pagination_container{
    position:Absolute;
    z-index:10;
    bottom:0;
    left:0;
    width:100%;
    background:url(../img/bg.png);
    height:101px;
}
 
.pagination {
    width:918px;
    height:73px;
    margin:14px auto;   
}
 
.pagination a{
    float:left;
    display:block;
    font-size:0;
    margin-left:5px;
    margin-right:5px;
    border:3px solid #262626;
    opacity:0.5;
}
 
.pagination .current a{
    opacity:1;
}
{% endhighlight %}
Here we to value position: fixed for div.fullscreen with 100% width and height. Along with that also for two values of the image is 100% div.slide.
### Use .resize event () to create fullscreen slideshow.
{% highlight Bash shell scripts linenos%}
We will use the event .resize () stretch of jQuery to slide when resizing the browser.
Event .resize () in jquery effective implementation of the function inside it when you resize the browser.
{% endhighlight %}

{% highlight Bash shell scripts linenos%}
$(window).load(function(){
 
// create a fullscreen slide the screen resize 
$(window).resize(function(){
    // get the value of the width and length of the browser    _max_height = $(window).height();
    _max_width = $(window).width();
 
    // change the length and width to resize    $('.slides_container,.slide').css({
        width:_max_width,
        height:_max_height,
    })
});
 
// This function is called to perform functions on resize
$(window).resize();
 
});
{% endhighlight %}

### DEMO
{% highlight Bash shell scripts linenos%}
http://zlatanblog.com/demo/fullscreen-part-1/fullscreen.html
{% endhighlight %}
