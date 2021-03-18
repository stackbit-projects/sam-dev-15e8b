---
title: Welcome to the new blog
subtitle: >-
  Today I am building a new site with Jekyll and Stackbit. Pretty interesting stuff.
excerpt: >-
  Today I am building a new site with Jekyll and Stackbit. Pretty interesting stuff.
date: '2021-03-16'
thumb_img_path: images/p/portrait.jpg
thumb_img_alt: Jekyll logo
content_img_path: images/p/portrait.jpg
seo:
  title: Welcome to the new blog
  description: >-
    Today I am building a new site with Jekyll and Stackbit. Pretty interesting stuff.
  extra:
    - name: 'og:type'
      value: article
      keyName: property
    - name: 'og:title'
      value: Welcome to the new blog
      keyName: property
    - name: 'og:description'
      value: >-
        Today I am building a new site with Jekyll and Stackbit. Pretty interesting stuff.
      keyName: property
    - name: 'og:image'
      value: images/10.jpg
      keyName: property
      relativeUrl: true
    - name: 'twitter:card'
      value: summary_large_image
    - name: 'twitter:title'
      value: Welcome to the new blog
    - name: 'twitter:description'
      value: >-
        Today I am building a new site with Jekyll and Stackbit. Pretty interesting stuff.
    - name: 'twitter:image'
      value: images/p/jekyll.jpg
      relativeUrl: true
layout: post
---

![Old Website](/images/p/oldwebsite.png)

I'm migrating off of my [old website](https://esaych.github.io/) today, and building a new one to better showcase my
thought process as I do my fun side projects.

The old website was a fun and beautiful UX design by my friend [Cat Chiang](https://www.linkedin.com/in/cat-chiang/) and my work
as a web developer brought it to life. I remember having fun writing the JavaScript transitions, and figuring out the mobile
view vs the desktop view was so complicated that I ended up writing separate webpages entirely based on the size of your window.

Anyways, I have grown out of that site. It was my pre-work life site, which showcased my work in bulk and didn't
really have any good ways to write about why I did my work. 

It's 2021. I've done a lot of projects during quarantine 2021, and I need a site to showcase my work. So here's my new site!
It's a showcase, and a blog! Still figuring out how I want to format it all, but I do want to share how easy this solution was.

<h3>Github Pages</h3>

![Github Pages](https://miro.medium.com/max/4800/1*UBPbXxCACLSygvXutPPGSA.jpeg)

So my last site was [hosted by Github](https://pages.github.com/). Github provides 1 free site to any user account. You
can only show static webpages (so no backend allowed), but it's perfect for portfolios or simple websites.

I wanted to keep this cheap hosting solution, so I looked around and found a best fit for Github ~ that led me to Jekyll.

<h3>Jekyll Static Website Builder</h3>

![Jekyll](https://miro.medium.com/max/4800/1*B3eU4xOLAB8_BPDh3pExdw.jpeg)

[Jekyll](https://jekyllrb.com/) is amazing as well, because it allows me to write a website up in markup! (which I've gotten very accustomed to
while writing docs at Amazon). And Jekyll can spin up locally and run on your computer, or be [computed by Github
to render your markup as part of a Github page](https://docs.github.com/en/github/working-with-github-pages/setting-up-a-github-pages-site-with-jekyll).

What's even better is that you can use many open source website templates which theme your Jekyll site, exactly how you need.

So it's a Tuesday afternoon, I've upgraded my Ruby and gotten Jekyll installed on my Mac and running the beginner website (which by the way is only 4 commands).
And I'm browsing Jekyll templates. There's so many. 

Some pretty ones I have to share:
- [Fjord](https://themes.stackbit.com/demos/fjord/) 
  - this site!
- [Creative](https://volny.github.io/creative-theme-jekyll/#)
  - actually kind of wanted this, but project blogging would've had the same issue
- [Hacker Style](https://akiritsu.github.io/pRoJEct-VeXEd/) 
  - I personally find this so ugly, but a younger version of me would've picked this one
- [portfolYOU](https://youssefraafatnasry.github.io/portfolYOU/projects/)
  - Simple, beautiful, but easily feels cluttered.
  
Anyways, I set my hearts desire on Fjord, and so I threw it into Jekyll with the [jekyll remote theme](https://github.com/benbalter/jekyll-remote-theme) gem.
That was a mission on its own, and it was beyond annoying that it extracted properly but just didn't copy into my rendered site. 
I kept getting themeless webpages. To troubleshoot, I tried Jekyll with the Creative theme, and it was working fine.
Nothing I did was making Fjord work. The [git repo](https://github.com/stackbit/stackbit-theme-fjord) had instructions to set it
up in Stackbit, but I really wanted to move forwards without creating a "Stackbit" account. 

And so... I finally caved and clicked "Create With Stackbit"

<h3>Stackbit</h3>

![Stackbit](https://miro.medium.com/max/2400/0*IpqdWIja-rXS0kXG.png)

I was hesitant at first, I had never heard of Stackbit. Once I associated my Github account it created a new website.
I immediately thought... oh this is another WordPress, or Drupal, or something, and rolled my eyes. But its not!

So when I initialized my site with Stackbit, it actually [made an entire Github repository](https://github.com/stackbit-projects/sam-dev-15e8b)
using the template, and started my site for me at a strange url: [https://sam-dev-15e8b.netlify.app/](https://sam-dev-15e8b.netlify.app/)

This actually removed the need to do any local work at all, just immediately setup a website, and gave me instructions on how
to configure my own domain for it. And apparently if you're just creating a blog like me, its 100% FREE.

I played around in the web based IDE they provided, and can completely see the appeal in it. They offer both the web editing view,
sort of like a WordPress experience (but much less ability to modify site design), and they offer a code editing view.
Both are pretty nice, and I'll definitely use in the future. But the nicest thing they provided was a "Develop Locally" menu,
which let me copy paste some commands and have my own local version of the site running in SECONDS.

Honestly, if you have >0 technical experience, I fully recommend Stackbit. Since they don't do any hosting, I'm not worried
they'll charge me extra one day. We'll see where this leads. But for now, I'm enjoying my new website building experience.
Way easier than css adjustments to align my div boxes manually like I did last time. Who knows, one day I might make a new
theme and the entire website will move with it.

**Mar 18 Edit:** Sad, Stackbit setup didn't give me permission to my own repo (I suppose this must be a bug). Their support
wasn't as helpful as I thought it would be.
I ended up requesting the entire repo get forked into [a repo fully owned by me](https://github.com/Esaych/sam-dev-15e8b). 
I also figured out that Stackbit integrates with [Netlify](https://www.netlify.com/) to do the Github deployment heavy lifting,
so I had to adjust the Netify software application to point to my new repository, and finally to get the web IDE
that Stackbit has, I needed to create a NEW site referring to my own repo in Stackbit. So now I have a duplicate site.
 
All in all, a workaround which will probably be resolved once Stackbit gets back to me on my support email, but I was impatient.

<style>
.site-header-bg {
  background-position: right;
}
</style>