---
layout: post
title: Migrating my blog
date: 2017-01-29
tags: []
tagline: From Tumblr to Jekyll
description: From Tumblr to Jekyll
---

### Reflection

It has been almost a year since I started my blog on Tumblr, and although I haven't always been consistent, I have managed to pump out on average two posts a month. I have talked about games I have been working on, personal adventures (i.e. stoicism, intermittent fasting) and lots of random little protoypes I have made.

But with the new year comes a time of reflection.

The reason I started was to have a dev log for the game I was making ([Homage](/2016/03/21/homage/)). But now, nearly 6 months since I touched that game I am still writing posts. Part of me really enjoys the writing aspect, part of me wants to gain some readers and part of me just wants to document the cool stuff I get to work on. Looking back on my posts from the last year I am really happy with some and cringe at others. Moving forward my aim is to improve the quality of my posts even if it does mean that I won't write as many. I want to write posts that I would want to read.

### Gross now on to real stuff

Tumblr was great when I started. I wanted a CMS with a nice public API so I could do just about anything with my own posts. Tumblr gave me this and more, I could create additional pages and I could style things exactly how I wanted by adding any custom html/css/js.

But I have unfortunately outgrown Tumblr. And this is why...

1. **Mobile Themes**. Tumblr never uses your own theme on mobile, which means an inconsistent feeling across desktop and mobile if you don't use their default theme.
2. **Posting**. Even though I could easily create a new post, if I wanted anything that was out of the ordinary (say an embedded youtube video) then I had to resort to using their very average html editor.
3. **Flexibility**. One thing I always wanted was a way to display the projects that I worked on, but I could never find a nice way to do this.

### Moving to Jekyll

Hardest part -> Setting up `rbenv` on my laptop just right.

After that I cloned the [Hyde](https://github.com/poole/hyde) Jekyll theme, made some minor changes to support Jekyll 3.x and I was flying. When I did this there were a few outstanding pull requests for these updates which made it super easy.

Next I imported all my Tumblr posts, [Jekyll Import](http://import.jekyllrb.com/) supports 37 different blogging platforms. And exporting my posts took no time at all, the only let down was having the image grabbing not work. So all the images are still hosted on Tumblr for now.

And with that I had a simple static site that was responsive. I had one of my Tumblr issues fixed already, I could have consistency across all platforms and could style it as much as I want.

One of the other reasons (for ditching Tumblr) was already solved too. By switching to Jekyll I could write all my posts in either `md` or `html` or even put html in my md. I still had a CMS if I chose to edit my posts on github.com (lets just forget about the terrible file editing experience on mobile for now) and I could use my text editor of choice for doing my posts on desktop.

My last point about flexability had been solved too, with Jekyll I have the ability to create my own `collections`, these are flexible objects that can be used site wide.

Just define the collection in your `_config.yml`.

```
collections:
    - projects
```

Then created a new `.md` file for each of my projects.

```
---
layout: page
title: Hashbrowns
tagline: Print your Jira tickets on Hashbrowns
date: 2017-01-24
link: http://jira.hashbrown.club/
---

That time that Jono wanted to print his JIRA tickets on Hashbrowns to impress everyone at work.
```

All I needed to do was make a page that looped through them all and displayed some of their contents.

{% raw %}
```
<!-- Displays Projects in correct order -->
{% for project in site.projects reversed %}
  <div class="project">
    <h4 class="project-title">
      <a href="{{ project.link }}">
        {{ project.title }}
      </a>
        {{ project.date | date_to_string }}
    </h4>
      {{project.content}}
  </div>
{% endfor %}
```
{% endraw %}

For my purposes Jekyll has been a lot more flexible. It has extra benefits too...

* Everything is under version control (Github).
* I can add literally anything that I want to the site (no longer have to play by Tumblr's rules).
* Custom 404 page. 

Later days.