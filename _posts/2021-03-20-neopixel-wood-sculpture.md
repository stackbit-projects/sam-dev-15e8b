---
title: Neopixel Wood Sculpture
subtitle: >-
  Enhancing my woodworking with interactive smart lights.
excerpt: >-
  Enhancing my woodworking with interactive smart lights.
date: '2021-03-20'
thumb_img_path: images/p/neopixel-cover.jpg
thumb_img_alt: Wood sculpture with neopixels
content_img_path: images/p/npm/pic1.jpg
carousel:
  images: 
    - image: /images/p/npm/pic4.jpg
    - image: /images/p/npm/pic2.jpg
    - image: /images/p/npm/pic3.jpg
    - image: /images/p/npm/pic5.jpg
    - image: /images/p/npm/pic6.jpg
    - image: /images/p/npm/pic7.jpg
    - image: /images/p/npm/pic8.jpg
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

{% include carousel.html height="50" unit="%" duration="10" %}

I masterminded a crazy final art project for my wood working class at UMD in 2019. I was assigned a task: 

>Build a beautiful piece of wood working as a self portrait. It must be mixed media, and it must be taller than you. <cite>Professor Foon Sham</cite>

For some reason I only envisioned an art piece that was tall, but not big (Unlike my classmates who went big in every direction).
I made a plan to integrate my piece with LEDs, an Arduino, and a PIR sensor. It was going to be blue when nobody
was nearby, but then transition to red when people were detected nearby. This was to reflect my own energy as I am an
extreme extrovert and the bright red is my energy as I am approached by new people.

This is what I came up with by the end of the course:

![2019 art piece](/images/p/neopixel-original.gif)

I was disappointed. I had missed some key things:
1. **The interaction was inconsistently.** I gave up trying to get the PIR sensor working so I just made it work on a basic color loop.
2. **The wood was unfinished.** No coating, just plywood.
3. **40% of my LEDs didn't work!** The sculpture had 5 embedded LED rings, but my poor soldering only enabled 2.
4. **The power draw of the LEDs was too high.** My wires which were too thin to carry the power.
5. **My soldering was terrible.** The entire thing was haphazardly constructed, so when an entire chain of lights was unresponsive, I couldn't easily fix it without
tearing out all the wiring.

I worked 10 hours the day before it was due, and the last minute effort to get it working left me with sad results.
I just left this as a bucket list item: One day I would finish it and bring it glory.

*fast-forward -> 2020 pandemic happens, time to finish this...*

<h3>Cleaning up my wood work</h3>

I had successfully moved this sculpture from my college dorm in Maryland to my house in Seattle. To get started I ripped
off all the old NeoPixels and the wires.

![stripped clean](/images/p/np-1.jpeg)

I took it out to my garage and stained it with a natural stain. This made the color of the wood pop a little
more and now the wood had a decent protective finish on it.

![stained wood](/images/p/np-2.jpeg)

The joints were filled with some putty, but the putty got discolored after staining, so my girlfriend helped me
match some paint colors and *correct* the coloring of the putty. All in all, I was satisfied with the wood sultpure.

<h3>Embedding electronics</h3>

It was time to get to wiring. I originally had 5 [Adafruit NeoPixels](https://www.amazon.com/dp/B00KAE3R1U/), but I did tests and found that not all 5 LED rings worked.
Notice how some LEDs got skipped in my tests? I think maybe during my soldering I fried some LEDs. Who knows.

Eventually I made good solder points and I got 3 neopixels I knew were going to work. So I set out to use 3 in the sculpture.

![broken](/images/p/np-3-broken.gif)
![working](/images/p/np-3-working.gif)

I 3D printed mounts for the LED rings, and setup a design which let me easily connect power, ground, and signal by wrapping
bare wire around screws. Tightening those screws got a solid electrical signal, but kept the design modular. 
If anything broke in the future, I'd be able to unscrew and replace these parts without having to rewire the entire sculpture.

![wiring style](/images/p/np-4.jpeg)

I decided to use the wire and stylistically wire it around the piece, and send all the wires into the driving circuit board through
the base. Underneath I had (naively) put a naked Raspberry Pi Zero W.

![initial wiring](/images/p/np-5.jpeg)
![base wiring](/images/p/np-6.jpeg)

I found out a couple problems based on this simple wiring:

1. Anytime the lights got turned on to 100% brightness, the Raspberry Pi would shut down due to power failure. 
Turns out Raspberry Pi Zero was not able to output enough power to my lights. I had to power 36 LEDs, but the power from the Pi was probably 5V ~1A. (Not enough)
2. The lights only worked around 50% of the time. Signal was muddy. Turned out the power draw from the lights would create noise
on the signal line and mess up the commands sent from my python scripts to the NeoPixels.
3. The Pi Zero was too slow for processing more complicated NeoPixel commands.

So I upgraded to a Pi 3, got a separate power supply, and addressed those wiring issues.

![wiring guide](/images/p/np-7a.jpeg)
![new wiring](/images/p/np-7.jpeg)

By this point, I had been fiddling with wires every night for a week and I was definitely fatigued with this entire project. 

I had originally wired all the power, ground, and signal in parallel so I didn't need to worry about a single point of failure
taking down all the other components, but the Raspberry Pi can only support 1 LED strip at a time, which I thought I could
be clever with code and thwart the restriction, but it ended up the hardware just wasn't able to do support 3 separate LED strips.
I had to rewire the 3 lights into series, and so now I'm doing a hybrid solution with power in parallel and signal in a series. 

I also managed to accidentally connect two live wires and blow out the LEDs on my top most ring, so I had to shovel out $10
for a replacement on Amazon, but since I made it so modular, the repair was just a 5 minute swap out to get it working again.

Now, I had complete control via a python script running on my headless Raspberry Pi and I can write some programs!

<h3>Making it pretty</h3>

I had working lights and now I wanted to make it meaningful. I had 3 lights so I set up a simple program.

- The top light was to Seattle - *my current home*
- The middle light represents Washington, DC - *my original home, and of 2 of my roommates*
- The bottom light represents Pheonix - *the original home of my third roommate*

The lights show me the weather of home by showing colors representing the temperature in those 3 cities.
I pull the weather data from [OpenWeather](https://openweathermap.org/)

- 25F - BLUE <span style="background-color:blue;color:white;">(0,0,255)</span>
- 40F - CYAN <span style="background-color:cyan;">(0,255,255)</span>
- 55F - WHITE (255,255,255)
- 70F - YELLOW <span style="background-color:yellow;">(255,255,0)</span>
- 90F - RED <span style="background-color:red;color:white;">(255,0,0)</span>

That gave us a nice variation of color such as this:
<span style="background-color:#00F;">=</span><span style="background-color:#04F;">=</span><span style="background-color:#08F;">=</span><span style="background-color:#0BF;">=</span><span style="background-color:#0FF;">=</span><span style="background-color:#4FF;">=</span><span style="background-color:#8FF;">=</span><span style="background-color:#BFF;">=</span><span style="background-color:#FFF;">=</span><span style="background-color:#FFB;">=</span><span style="background-color:#FF8;">=</span><span style="background-color:#FF4;">=</span><span style="background-color:#FF0;">=</span><span style="background-color:#FB0;">=</span><span style="background-color:#F80;">=</span><span style="background-color:#F40;">=</span><span style="background-color:#F00;">=</span>

Then I also mapped the color of the sky to various visual indicators. Since the API provides [icon weather indicators](https://openweathermap.org/weather-conditions)
I decided it'd be best to map these icons to colors.

Some of the icons included:
- 'clear sky': <span style="background-color:rgb(255,255,40)">[255,255,40]</span>
- 'scattered clouds': <span style="background-color:rgb(128,155,155)">[128,155,155]
- 'rain': <span style="background-color:rgb(0,10,224)">[0,10,224]</span>
- 'thunderstorm': <span style="background-color:rgb(255,121,0)">[255,121,0]</span>

And one that I felt helped me know when my family was end their day: 
- 'sunset' or 'night': <span style="background-color:rgb(70,0,132)">[70,0,132]</span> 

Given these two settings, I just let them fade between the two colors (temperature, and sky condition) every 30 seconds with a
very gradual 10 second transition. It's now the default state of my sculpture now, and I think the purple of the night is
very calming in the evenings.

![blue weather](/images/p/np-8.jpg)
![purple weather](/images/p/np-8b.jpg)

*sneak peak: I also made the lights synchronize to our sound system, but [that's another post](/posts/music-wood-sculpture/)!*

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
  width: 46.6%;
  float: left;
  margin-right: 10px;
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
img[alt="blue weather"] {
  width: 50%;
  float: left;
}
img[alt="purple weather"] {
  width: 50%;
}

</style>