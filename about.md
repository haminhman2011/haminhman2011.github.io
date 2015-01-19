---
layout: page
title: CSS dropdown menu
comments: yes
permalink: /about/
---



### The concept.

What a dropdown menu provides is a hierarchical overview of the subsections contained within the menu item that spawned it. Basically, it lists all the subsections within a section of a site when you hover your mouse cursor over it.
They are extremely useful in showing what a section of a site contains, and allowing you to access it from anyway else in that site, whether that be the parent page of that subsection, or a page in a different section altogether.

### The markup.

A lot of dropdown menus rely on bulky, extraneous markup and Javascript to work, ours will use only the cleanest HTML and some lean CSS, with some lovely progressive CSS3 for good measure.
{% highlight Bash shell scripts %}
<ul id="nav">
    <li>
        <a href="#">Home</a>
    </li>

    <li>
        <a href="#">About</a>
        <ul>
            <li><a href="#">The product</a></li>

            <li><a href="#">Meet the team</a></li>
        </ul>
    </li>
    <li>
        <a href="#">Services</a>

        <ul>
            <li><a href="#">Sevice one</a></li>
            <li><a href="#">Sevice two</a></li>

            <li><a href="#">Sevice three</a></li>
            <li><a href="#">Sevice four</a></li>
        </ul>

    </li>
    <li>
        <a href="#">Product</a>
        <ul>
            <li><a href="#">Small product (one)</a></li>

            <li><a href="#">Small product (two)</a></li>
            <li><a href="#">Small product (three)</a></li>
            <li><a href="#">Small product (four)</a></li>

            <li><a href="#">Big product (five)</a></li>
            <li><a href="#">Big product (six)</a></li>
            <li><a href="#">Big product (seven)</a></li>

            <li><a href="#">Big product (eight)</a></li>
            <li><a href="#">Enormous product (nine)</a></li>
            <li><a href="#">Enormous product (ten)</a></li>

            <li><a href="#">Enormous product (eleven)</a></li>
        </ul>
    </li>
    <li>
        <a href="#">Contact</a>

        <ul>
            <li><a href="#">Out-of-hours</a></li>
            <li><a href="#">Directions</a></li>

        </ul>
    </li>
</ul>
{% endhighlight %}

As you can see here the markup is simply a series of nested <ul>s. No verbose IDs/classes, no <div>s, just rich, semantic code.

The #nav <ul> contains a series of <li>s, and any that require a dropdown then contain another <ul>. Notice the dropdown <ul>s have no classes on them–this is because we use the cascade to style these, keeping our markup even cleaner.

### The CSS.

This is where the magic happens–we use CSS to transform a series of nested <ul>s into a smooth, easy to use, neat and self-contained dropdown menu.
{% highlight Bash shell scripts %}
/* BE SURE TO INCLUDE THE CSS RESET FOUND IN THE DEMO PAGE'S CSS */

/*------------------------------------*\
    NAV
\*------------------------------------*/
#nav{
    list-style:none;
    font-weight:bold;
    margin-bottom:10px;
    float:left; /* Clear floats */
    width:100%;
    /* Bring the nav above everything else--uncomment if needed.
    position:relative;
    z-index:5;
    */
}
#nav li{
    float:left;
    margin-right:10px;
    position:relative;
}
#nav a{
    display:block;
    padding:5px;
    color:#fff;
    background:#333;
    text-decoration:none;
}
#nav a:hover{
    color:#fff;
    background:#6b0c36;
    text-decoration:underline;
}

/*--- DROPDOWN ---*/
#nav ul{
    background:#fff; /* Adding a background makes the dropdown work properly in IE7+. Make this as close to your page's background as possible (i.e. white page == white background). */
    background:rgba(255,255,255,0); /* But! Let's make the background fully transparent where we can, we don't actually want to see it if we can help it... */
    list-style:none;
    position:absolute;
    left:-9999px; /* Hide off-screen when not needed (this is more accessible than display:none;) */
}
#nav ul li{
    padding-top:1px; /* Introducing a padding between the li and the a give the illusion spaced items */
    float:none;
}
#nav ul a{
    white-space:nowrap; /* Stop text wrapping and creating multi-line dropdown items */
}
#nav li:hover ul{ /* Display the dropdown on hover */
    left:0; /* Bring back on-screen when needed */
}
#nav li:hover a{ /* These create persistent hover states, meaning the top-most link stays 'hovered' even when your cursor has moved down the list. */
    background:#6b0c36;
    text-decoration:underline;
}
#nav li:hover ul a{ /* The persistent hover state does however create a global style for links even before they're hovered. Here we undo these effects. */
    text-decoration:none;
}
#nav li:hover ul li a:hover{ /* Here we define the most explicit hover states--what happens when you hover each individual link. */
    background:#333;
}
{% endhighlight %}

Just a regular horizontal navigation menu…

Right, let’s now break that down… The first section is fairly self explanatory–here we are just setting up a regular horizontal navigation menu, the same as any other. However, notice that selectors such as #nav li and #nav li a will select all list items and links in the dropdowns too. Here we’re using the cascade sensibly.

One thing of note however is applying position:relative; to the list items, this allows us to use position:absolute; on the nested <ul>s later on.

### The nested lists.
{% highlight Bash shell scripts %}
#nav ul{
    background:#fff; /* Adding a background makes the dropdown work properly in IE7+. Make this as close to your page's background as possible (i.e. white page == white background). */
    background:rgba(255,255,255,0); /* But! Let's make the background fully transparent where we can, we don't actually want to see it if we can help it... */
    list-style:none;
    position:absolute;
    left:-9999px; /* Hide off-screen when not needed (this is more accessible than display:none;) */
}
{% endhighlight %}
Here we have the CSS that controls the <ul>s nested within the top level list items. Obviously we need to remove bullets with list-style:none;, then position:absolute; to position the dropdown above the list item that holds it.

A better, more accessible solution than display:none;…

The next line however is a point of interest. Usually, most people would use display:none; to hide the dropdown while it’s not being used, but due to a lot of screenreaders ignoring anything with display:none; applied, this is very inaccessible. What we do instead is take advantage of the fact the <ul> is absolutely positioned and just position it -9999px off screen when not in use.

Next up we declare opacity:0; for the hidden <ul> and then a Webkit only declaration which will smoothly fade the <ul> in from fully transparent when hovered.
{% highlight Bash shell scripts %}
#nav ul li{
    padding-top:1px; /* Introducing a padding between the li and the a give the illusion spaced items */
    float:none;
}
#nav ul a{
    white-space:nowrap; /* Stop text wrapping and creating multi-line dropdown items */
}
#nav li:hover ul{ /* Display the dropdown on hover */
    left:0; /* Bring back on-screen when needed */
}
{% endhighlight %}

Above: The 1px gap achieved by the padding-top:1px; applied to the list-item

Here we set up the default list item and link styles. Notice the padding-top:1px; on the <li>. As all the colours etc are applied to the <a>, putting a 1px padding on the <li> in effect pushes the <a>–and therefore the colour–away from the edge of the list item, giving it the illusion that they are all separated. Interestingly, IE will not recognise the layout of the <li> when hovered, closing the dropdown again. To get round this, I added a 1×1px transparent gif image as a background. Also here we remove the floats applied earlier.

Next, on #nav ul a, we apply white-space:nowrap; to prevent items wrapping onto two lines, ensuring a consistent display.

And this is where the magic happens…

The final bit of code is the bit that actually makes the dropdown appear when the list item that contains it is hovered. Now, as the :hover pseudo-class only works on the <a> element in IE6, the dropdowns won’t work in that browser. That can be alleviated by using a variety of fixes. However, as dropdowns are progressive, then we’re okay with them not working. If you do however want to get this working in IE6 then my favoured solutions is by using behaviours.
{% highlight Bash shell scripts %}
#nav li:hover a{ /* These create persistent hover states, meaning the top-most link stays 'hovered' even when your cursor has moved down the list. */
    background:#6b0c36;
    text-decoration:underline;
}
{% endhighlight %}

This gets tricky, but it should make sense.

This block of code here is where the hover styles come in, there’s a bit of nifty code in there which controls what we’ll call ‘persisting hover states’ on the top level item even when the user is hovering the dropdown items…

#nav li:hover a is what allows you to give the top level link a persisting hover state when hovering its ‘children’. This works by styling every link inside a list-item when that list-item is hovered. This bit gets a bit tricky but bear with me:

    The dropdown <ul> sits inside an <li>.
    If you are hovering over a link (<a>) in a dropdown (<ul>) then you are also, at the same time, still hovering the top level list-item (<li>) as you are hovering content inside it.
    Because you are technically still hovering the top level list-item, the #nav li:hover a remains true, leaving a persisting hover style on the top level list-item’s <a> so…

    …by hovering a dropdown item you are still hovering the top level list-item which means the cascade still styles all links in that list-item. Phew!

    #nav li:hover ul a{ /* The persistent hover state does however create a global style for links even before they’re hovered. Here we undo these effects. */ text-decoration:none; }

Here we override certain aspects of the persisting hover state so that the dropdowns differ from the top level link. In this case we merely decide not to underline them.

We also add a touch of Webkit goodness, telling the links to transform. -webkit-transition:-webkit-transform 0.075s linear; tells Webkit to animate the -webkit-transform we apply later on in the code over 0.075 seconds with no fade-in/out. Look out for the initiation of this in the next (and final) block of CSS.
{% highlight Bash shell scripts %}
#nav li:hover ul li a:hover{ /* Here we define the most explicit hover states--what happens when you hover each individual link. */
    background:#333;
}
{% endhighlight %}

### Link Demo.
{% highlight Bash shell scripts %}
http://csswizardry.com/demos/css-dropdown/
{% endhighlight %}




