---
layout: post
title: Animated Favicons
date: 2017-02-15
tags: []
tagline: Blink Blink
description: How to make an animated favicon? Is it too much?
---

### So you want to make a super badass animated favicon?

[...skip to the code](#code)

<img src="https://i.giphy.com/3o6Yg9HzWBCFhMdTa0.gif"/>

As per the W3 spec the browser looks for your favicon in the head of your HTML document. All major browsers support .ico and .png filetypes. The highest resolution combatible universally is 32x32 pixels.

This is generally what it will look like.

``` html
<link rel="icon" 
      type="image/png" 
      href="http://example.com/myicon.png">
```

Fantastic! So my initial idea was just to change the href attribute of the link element using javascript.

This had two downfalls though...

* Each new image had to be loaded first and the page would show the loading icon until each image frame of the animation had played.
* A request is made for every frame of the animation even if it has already loaded it once. The browser doesn't try to cache them.

So we get something that looks like this...

<img src="/public/images/favicon_requests.png"/>

This isn't very efficient, unless your intention is to slowly suck at your viewers data plan.

But there is another way to do it. I took inspiration from [DEFENDER OF THE FAVICON](http://www.p01.org/defender_of_the_favicon/), a game played entirely in the favicon of the webpage.

They render the game to a 16x16 pixel HTML5 canvas element then export each frame as a data: URI. A data: URI is the same data that makes up a png file, but base64 encoded and stored as a string.

Using a data: URI means that a request doesn't need to be made because the information is already there. Depending on how complex your animation is, this might be a good solution for you. But since mine was two frames it was much easier to just convert them and stick them straight in the header.

There are a few online tools that can do this, and they are just a quick google away. Or you can render them in a canvas element and call the `.toDataURL()` method to fetch them.

<a name="code">

### Code 

``` html
<link id="animated-favicon" rel="icon" type="image/png" href="">
<script>
    var currentIcon = false;
    function swapIcon(){
        var link = document.getElementById('animated-favicon');
        if(currentIcon){
            link.href = "data:image/png;base64,iVBORw0KGgoAAA.....";
        } else {
            link.href = "data:image/png;base64,iVBORw0KGgo.....";
        }
        currentIcon = !currentIcon;
    }
    setInterval(swapIcon, 1000);
</script>
```

### But should we?

The unwritten rules of the internet declare visual or auditory effects without user consent a big no no. Pop up boxes, autoplaying videos and big splash pages are generally considered to be very annoying.

So where does this stand amongst all that. In my opinion in depends on the context and the site's intention. Definitely think long and hard about why if you are considering animating your favicon.

PS. I am fully aware how annoying a low battery symbol is as a favicon. Enjoy!
