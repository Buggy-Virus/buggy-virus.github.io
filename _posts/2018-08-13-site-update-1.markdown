---
layout: post
title:  "Site Update 1"
date:   2017-08-13 16:51:00 -0400
categories: this-site,
tags: this-site,
---
21 commits later the site is at a presentable point. I started off with the basic Minima theme that Jekyll sites are created with by default. It's a simple serviceable theme, you can check it out and see a demo at the [Minima Repository][minima].

I wanted to add a bit more personality to the site, so I tried to give it a slate style theme. I also cleaned up various parts of the site, such as replacing the text of the footer with dynamic links, setting up the header for the main pages, and adding project and contact pages. Overall I'm quite satisfied with the result:

<center><img src="/assets/site-update-1/front-page.png" alt="Front Page" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;">It will be weird to see a slightly smaller version of the site for people who are reading this post around the time it is published.</span></center>

&nbsp;

&nbsp;

## CSS

For any of the custom CSS styles I added to `assets\main.scss`, I named the style `.c-<name of style>`. This makes it exceedingly easy when inspecting the site page to tell which elements I styled, versus which elements are styled with Minima's default style.

&nbsp;

&nbsp;

## Theme

I've always been a big fan of themes that make use of mainly grays. It feels very clean to me, and I find it stressedul to commit to a specific color for your entire website. So I tend to stick to the whole slate theme.

The background is just a white isometric grid on top of a gray html gradient. Oririginally, the entire background was some 2560x1920 image of a gradiant, with a grid with its own gradient over it. For obvious reasons this increased load time immensely, so I switched to the current setup.

In terms of font, probably the most important decision, I went with [Avenir][avenir]. I've really been in love with Avenir since my friend introduced me to it, and I have been using it any time a sans serif font is necessary. It just looks so clean and stylish. Just read this and look at it. It really makes for a pleasant experience. I imagine my choice of font will compensate for my severe lack of talent as a writer.

&nbsp;

&nbsp;

## Header

&nbsp;

<center><img src="/assets/site-update-1/header.png" alt="Header" style="width:468px;height:70px;text-align:center;" markdown="1"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;" markdown="1">Just a standard header style that you could find anywhere.</span></center>

&nbsp;

By default Minima displays all markdown pages that aren't posts in the header. To setup a header, which only displays key pages I designate, I actually made use of liquid code that comes with the Minima theme in `_includes\header.html`.

&nbsp;

{% highlight liquid %}

{% raw %}

{% for path in page_paths %}
  {% assign my_page = site.pages | where: "path", path | first%}

  {% if my_page.title %}
  <a class="page-link" href="{{ my_page.url | relative_url }}">{{ my_page.title | escape }}</a>
  {% endif %}
{% endfor %}

{% endraw %}

{% endhighlight %}

&nbsp;

The code is fairly straight forward, going through the `page_paths`, filtering the through all the site pages and grabbing the one with the correct path, then creating a link to the page in the header. By default, `page_paths` is empty, and if this is the case, the site will just iterate through every page on the site and add it to the header. One just needs to specify in `_config.yml` the pages they want in the header to populate `page_paths`. Here's what I added to my `_config.yml`:

```yaml
header_pages:
  - projects.md
  - about.md
  - contact.md
```

&nbsp;

I know it's odd that this assigns the list of pages to `header_pages` and not to `page_paths`, but this later gets handled by assigning `page_paths` to `header_pages` in `_includes\header.html`. I'm not sure why they used this convoluted method, but I thought it best to leave the original code intact as much as possible.

Setting up the header actually proved to be the most frustrating part of updating the site. This was due to the liquid code not working when I initially added my list of `header_pages` to `_includes\header.html`, which prompted me to actually look under the hood and motivated me to learn the Liquid syntax.

After rewriting a good deal of the original Liquid code, adding a bunch of print statements to see what exactly was happening at every step, and setting up various tests, I got it working. I then commented out all my extra work, and was left with code identical to the original Minima code. I guess it will forever be one of those programming mysteries as to why it didn't work originally and what changed to cause it to finally work. 

Though, had this non-bug not occured, I likely wouldn't have bothered to spend any time learning the Liquid syntax and taking time to understand how it ineracted with the structure of the site. I would have likely created the rest of the pages using static CSS and html, which I would have needed to update manually whenever I added a new project until everything became too messy and I was forced to learn Liquid. So something good came out of all this.

Oh yeah, I also put my name up in the top left. It's ok I guess.

&nbsp;

&nbsp;

## Footer

&nbsp;

<center><img src="/assets/site-update-1/footer.png" alt="Footer" style="width:468px;height:70px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;">It lights up. Sometimes.</span></center>

&nbsp;

I wanted my footer function as a very simple means to get contact info or navigate to a couple of my profiles on important sites. So I whipped up some icons in photoshop, and just made the highlight color that of the company's logo (the highlight color of the mail icon is Gmail's), then slapped them onto the bottom.

The method I'm currently using to make the icons light up on hover is that of changing the elements background image on hover.

&nbsp;

```css
.c-icon-contact {
	float: left;
	margin: 0px 10px 0px 10px;
	height: 46px;
	width: 46px;
	background-image: url('mail-fav-nh.png');
	position:relative;
}

.c-icon-contact:hover {
	background-image: url('mail-fav.png')
}
```

&nbsp;

This does present an issue where the image for the highlighted icon needs to load into cache when one first hovers over it, and the icon completely disappears while this happens. I know I really ought solve this by using CSS sprites, but I only read up on them after creating creating the seperate `.png` for each icon state and writing up the style. So rather than going back into photoshop and creating a new single image for both icon states, I just preload all the highlighted icon images in a div with `visibility: hidden;`.

&nbsp;

&nbsp;

## About

[Link to Page][about]

The about page isn't anything revolutionary. It has a description of the site and myself, then my CV and resume. I considered including links to some of my online profiles here, but I don't want it to become confusing. So I'm planning on dumping all those links onto the contacts page.

&nbsp;

&nbsp;

## Contacts

[Link to Page][contact]

<center><img src="/assets/site-update-1/contact-page.png" alt="Contact Page" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;">Links to my email and some of my profiles on other sites.</span></center>

&nbsp;

Again, a pretty straightforward page. Mainly it reuses the icons I made for the footer, but slightly larger this time. In the future I'll add some more links here that are unique from the footer, like my hackerrank, reddit, soundcloud etc.

&nbsp;

&nbsp;

## Projects

[Link to Page][projects]

<center><img src="/assets/site-update-1/projects-page.png" alt="Front Page" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;">A list of some of my past coding projects.</span></center>

&nbsp;

For the projects page, I wanted to easily showcase various projects I've worked on. So I used a scheme similar to that of the header, and created a list of `project_pages` in `_config.yml`. Then I used similar Liquid to populate the page with the various project button overview things.

&nbsp;

{% highlight liquid %}

{% raw %}

{% assign project_paths = site.project_pages | default: default_paths %}
{% for path in project_paths %}
  {% assign my_project = site.pages | where: "path", path | first%}
  <div class="c-project">
    <a class="c-project-link" href="{{ my_project.pseudo-path }}">
      <div class="c-project-title-box">
        <h2 class="c-project-title">{{ my_project.title }}</h2>
      </div>
    </a>

    <a href="{{ my_project.pseudo-path }}">
      <img src="{{ my_project.menu-img }}" alt="{{ my_project.menu-img-alt }}" style="width:355px;height:150px;">
    </a>

    <div class="c-project-bar">
      <p class="c-project-date">{{ my_project.given-date }}</p>

      {% if my_project.project-page %}
        <a href="{{ my_project.project-page }}" target="_blank">
          <div class="c-project-page-icon"></div>
        </a>
      {% elsif true %}
        <div class="c-project-no-page-icon"></div>
      {% endif %}

      {% if my_project.project-github %}
        <a href="{{ my_project.project-github }}" target="_blank">
          <div class="c-project-github-icon"></div>
        </a>
      {% elsif true %}
        <div class="c-project-no-github-icon"></div>
      {% endif %}
    </div>
  </div>
{% endfor %}

{% endraw %}

{% endhighlight %}

&nbsp;

From here you can get to any project's page on the site, the actual page of the project, and its Github. I'm going to add my coursework in CS classes to this page as well. When I do, there will also be an icon linking to the course page that makes it clear its Brown University coursework.

&nbsp;

#### Project Pages

[Check out the Project Page for This Site][this-site]

Each project has its own page, which contains a brief description, and the rest is filled with project details using Liquid. Additionally it displays all the posts tagged to the particular project using the Liquid below:

{% highlight liquid %}

{% raw %}

<ul class="post-list">
  {% for post in site.posts %}
    {% if post.tags contains page.tag %}
      <li>
        {% assign date_format = site.minima.date_format | default: "%b %-d, %Y" %}
        <span class="post-meta">{{ post.date | date: date_format }}</span>

        <h2>
          <a class="post-link" href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
        </h2>
      </li>
    {% endif %}
  {% endfor %}
</ul>

{% endraw %}

{% endhighlight %}

&nbsp;

&nbsp;

### Afterword

There is still a bunch more I should implement, like pagination and the ability to filter posts and projects by tag. But I'm going to focus on getting more content on the site first. As with how little content there is now, there's no real point in implementing those features.

Biggest regeret so far: trying to maintain the whitespace style for my html where each tab is two spaces, while Sublime thinks they are four spaces.

&nbsp;

&nbsp;

[minima]: https://github.com/jekyll/minima
[avenir]: https://www.myfonts.com/fonts/linotype/avenir/
[about]: /about/
[contact]: /contact/ 
[projects]: /projects/
[this-site]: /projects/this-site
