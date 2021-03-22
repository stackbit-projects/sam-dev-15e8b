---
title: Neopixel Wood Sculpture
subtitle: >-
  Enhancing my woodworking with interactive smart lights.
excerpt: >-
  Enhancing my woodworking with interactive smart lights.
date: '2021-03-20'
thumb_img_path: images/p/neopixel-cover.jpg
thumb_img_alt: Wood sculpture with neopixels
content_img_path: images/p/neopixel-cover.jpg
seo:
  title: Neopixel Wood Sculpture
  description: >-
    Enhancing my woodworking with interactive smart lights.
  extra:
    - name: 'og:type'
      value: article
      keyName: property
    - name: 'og:title'
      value: Neopixel Wood Sculpture
      keyName: property
    - name: 'og:description'
      value: >-
        Enhancing my woodworking with interactive smart lights.
      keyName: property
    - name: 'og:image'
      value: images/p/neopixel-cover.jpg
      keyName: property
      relativeUrl: true
    - name: 'twitter:card'
      value: summary_large_image
    - name: 'twitter:title'
      value: Neopixel Wood Sculpture
    - name: 'twitter:description'
      value: >-
        Enhancing my woodworking with interactive smart lights.
    - name: 'twitter:image'
      value: images/p/neopixel-cover.jpg
      relativeUrl: true
layout: post
---

I masterminded a crazy final art project for my wood working class at UMD in 2019. I was assigned a task: 
*Build a beautiful piece of wood working as a symbol of ourselves, it must be mixed media, and...*

>it must be taller than you. <cite>Professor Foon Sham</cite>

So my mind was creative, but for some reason I only envisioned an art piece that was tall, but not big.
I made a plan to integrate my piece with LEDs, an Arduino, and a PIR sensor. It was going to be blue when nobody
was nearby, but then transition to red when people walked by. This was to reflect my own energy as I am an
extreme extrovert and the bright red is my energy as I am approached by new people.

This is what I came up with by the end of the course:

![2019 art piece](/images/p/neopixel-original.gif)

I was disappointed. I had missed some key things:
1. The PIR sensor only worked once. I gave up trying to get it working so I just made it work on a basic color loop.
2. The wood was unfinished, no coating, just plywood.
3. The sculpture had 5 embedded LEDs, but the wiring only worked with 2.
4. The power draw of the LEDs was too high and the wires were too thin to carry the power.
5. My soldering was terrible, I didn't test the product before, so an entire chain of lights was unresponsive.

I worked 10 hours the day before it was due, and the last minute effort to get it working left me with sad results.
I just kept it as a todo item. One day I would finish it and bring it glory.

*fast-forward -> 2020 pandemic happens, time to finish this...*

<h3>Cleaning up my wood work</h3>

I had successfully moved this sculpture from my college dorm in Maryland to my house in Seattle. To get started I ripped
off all the old neopixels and the wires.

![stripped clean](/images/p/np-1.jpeg)

I took it out to my garage and stained it with a natural stain. This made the color of the wood pop a little
more and now the wood had a decent protective finish on it.

![stained wood](/images/p/np-2.jpeg)

The joints were filled with some putty, but the putty got discolored after staining, so my girlfriend helped me
match some paint colors and *correct* the coloring of the putty. All in all, I was satisfied with the wood sultpure.

<h3>Embedding electronics</h3>

It was time to get to wiring. I originally had 5 neopixels, but I did tests and found that not all 5 LED rings worked.
Notice how some LEDs got skipped in my tests? I think maybe during my soldering I fried some LEDs. Who knows.

Eventually I made good solder points and I got 3 neopixels I knew were going to work. So I set out to use 3 in the sculpture.

![broken](/images/p/np-3-broken.gif)
![working](/images/p/np-3-working.gif)

I 3D printed mounts for the LED rings, and setup a design which let me easily connect power, ground, and signal by wrapping
bare wire around screws, and tightening those screws to get a solid electrical signal. If anything broke in the future, I'd be able
to unscrew and replace these parts without having to rewire the entire sculpture.

![wiring style](/images/p/np-4.jpeg)

I decided to use the wire and stylistically wire it around the piece, and send all the wires into the driving circuit board through
the base. And underneath I had (naively) put a naked raspberry pi zero w.

![initial wiring](/images/p/np-5.jpeg)
![base wiring](/images/p/np-6.jpeg)

I found out a couple problems based on this simple wiring.

1. Anytime the lights got turned on to 100%, the Raspberry Pi would shut down due to power failure. 
Turns out Raspberry Pi Zero was not able to output enough power to my lights. I had to power 36 LEDs and the power from the Pi was probably 5V ~1A. 
2. The lights only worked around 50% of the time. Signal was muddy. Turned out the power draw from the lights would create noise
on the signal line and mess up the commands sent from my python scripts to the NeoPixels.
3. The Pi Zero was too slow for processing more complicated NeoPixel commands.

So I upgraded to a Pi 3, got a separate power supply, and addressed those wiring issues.

![wiring guide](/images/p/np-7a.jpeg)
![new wiring](/images/p/np-7.jpeg)

By this point, I had been fiddling with wires every night for a week and I was definitely fatigued with this entire project. 

I had originally wired all the power, ground, and signal in parallel so I didn't need to worry about a single point of failure
taking down all the other components, but the Raspberry Pi can only support 1 LED strip at a time, 
so I had to rewire the 3 lights in series. I ended up doing a hybrid solution with power in parallel and signal in a series. 

I had managed to accidentally connect two live wires and blow out the LEDs on my top most ring, so I had to shovel out $10
for a replacement, but since I made it so modular, it was just a 5 minute swap out to get it working again.

Now, I had complete control via a python script running on my headless Raspberry Pi, and I could write some programs.

<h3>Making it pretty</h3>

\<tbd\>

<style>
img[alt="stripped clean"] {
  width: 50%;
}
img[alt="stained wood"] {
  width: 50%;
}
img[alt="broken"] {
  float: left;
  padding-right: 10px
}
img[alt="initial wiring"] {
  width: 45%;
  float: left;
  padding-right: 10px;
}
img[alt="base wiring"] {
  width: 45%;
}
img[alt="wiring guide"] {
  width: 45%;
  float: left;
  padding-right: 10px
}
img[alt="wiring guide"] {
  width: 30%;
}
img[alt="new wiring"] {
  width: 65%;
}

</style>