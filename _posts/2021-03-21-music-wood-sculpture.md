---
title: Visualized house sound on my wooden sculpture
subtitle: >-
  Making pretty visualizations of music from our house sound system on my abstract wooden sculpture.
excerpt: >-
  Making pretty visualizations of music from our house sound system on my abstract wooden sculpture.
date: '2021-03-21'
thumb_img_path: images/p/npm/music-cover.gif
thumb_img_alt: Visualized house sound on my wooden sculpture
content_img_path: images/p/npm/pic1.jpg
carousel:
  images: 
    - image: /images/p/npm/pic2.jpg
    - image: /images/p/npm/pic3.jpg
    - image: /images/p/npm/pic4.jpg
    - image: /images/p/npm/pic5.jpg
    - image: /images/p/npm/pic6.jpg
    - image: /images/p/npm/pic7.jpg
    - image: /images/p/npm/pic8.jpg
seo:
  title: Visualized house sound on my wooden sculpture
  description: >-
    Making pretty visualizations of music from our house sound system on my abstract wooden sculpture.
  extra:
    - name: 'og:type'
      value: article
      keyName: property
    - name: 'og:title'
      value: Visualized house sound on my wooden sculpture
      keyName: property
    - name: 'og:description'
      value: >-
        Making pretty visualizations of music from our house sound system on my abstract wooden sculpture.
      keyName: property
    - name: 'og:image'
      value: images/p/np-music-cover.jpg
      keyName: property
      relativeUrl: true
    - name: 'twitter:card'
      value: summary_large_image
    - name: 'twitter:title'
      value: Visualized house sound on my wooden sculpture
    - name: 'twitter:description'
      value: >-
        Making pretty visualizations of music from our house sound system on my abstract wooden sculpture.
    - name: 'twitter:image'
      value: images/p/npm/music-cover.jpg
      relativeUrl: true
layout: post
---

I finished building my [electronic wooden sculpture](/posts/neopixel-wood-sculpture/), and I set up a wifi synchronized 
sound system in my house, so it only made sense to combine the two!



The system works by integrating SnapCast, C.A.V.A., and the NeoPixel library, all running on Raspberry Pis.

![system diagram](/images/p/npm/sys-diagram.png)

<h5>1. SnapCast Server</h5>

[Snapcast](https://github.com/badaix/snapcast) is an amazing piece of open source software. While I explain more in depth
in [this blog post](/posttbd/), we used the server from SnapCast on one of the Raspberry Pi's in our house
which acts as the hub for our sound system. The hub server has [other software](https://github.com/dtcooper/raspotify) 
which tricks devices on our home wifi to think it's a smart Spotify device, and then SnapCast translates that into a
 broadcast to our network to any SnapCast client to seamlessly synchronize and play to audio.

<h5>2. SnapCast Client</h5>

The Raspberry Pi at the bottom of [this wooden sculpture](/posts/neopixel-wood-sculpture/) is setup to have
a SnapCast client. It's able to automatically sync with the hub and emit sound to an audio output 
with perfect timing to other speakers in our house. In this case I set that output to be to named pipe on the file system (/tmp/snapfifo).

<h5>3. C.A.V.A.</h5>

[C.A.V.A.](https://github.com/karlstav/cava) is a bar spectrum audio visualizer for the Linux terminal. It is originally
built to analyze audio out of ALSA and generate a visualizer you would likely see in a [Rainmeter](https://www.rainmeter.net/)
background. 

![CAVA](https://raw.githubusercontent.com/karlstav/cava/master/example_files/cava.gif)

I used that visualizer to emit 3 bars, only 3 bars because there are 3 ring lights in my sculpture. Then I set the
output of the visualizer to be to another file pipe as an ascii output. That looked something like 0;0;0 for no music, 
bar heights are at 0. 255;0;0 for really loud frequency in the bass, and 0:0:255 for really loud frequency in the high notes.

<h5>4. Python Program</h5>

Then I got to work writing [a python program](https://github.com/Esaych/neopixel-server/blob/main/music.py) to read these 
bar data from the file pipe, and then used the [matplotlib cmap function](https://matplotlib.org/stable/gallery/color/colormap_reference.html)
to convert a # on a range from 0 to 255 to a color from #000000 to #FFFFFF. And matplotlib let you
do that in many many different ways.

So all I had to do was set a cool color range (we started with inferno), translate those into red green blue channels
 and then send those commands down the line to the LEDs!
 
Crediting my roommate [Robert Morrison](https://www.linkedin.com/in/robmorr/) for helping me find matplotlib cmap 
helping me write this bar height to color python script.

![Color Map](/images/p/npm/colormap.png)

<h5>5. NeoPixel</h5>

NeoPixel has really nice python support, so our [adapter](https://github.com/Esaych/neopixel-server/blob/main/control.py) proved pretty simple.
I originally wired the 3 [adafruit neopixel rings](https://www.amazon.com/dp/B00KAE3R1U/) with all three LEDs
on separate circuits and separate signal cables, but I had to go back and adjust the wiring so that the wiring was
done in parallel (due to Raspberry Pi hardware limitations). This let me send a single signal down the line which 
was designed for a strip of 36 LEDs. The base ring would read the first 12 channels of data and forward 24 channels to the second ring. 
The second ring would read 12 more, and forward the last 12 to the highest ring. This let me treat the entire sculpture like 1 LED strip.

<h3>Result</h3>

{% include carousel.html height="50" unit="%" duration="10" %}