---
layout: post
title: just because
summary: The Miscellaneous folder - the "side projects" that select engineers like to constantly bring up in conversation
featured-img: heroshot-justcause
categories:
driveID-paddington: 1rsv2ZqRP9BzjRxJZFjqMIgs0mYUAywrB/preview
driveID-oscilloscope: 1FHsHbRkRPVA9ganmYhuZUxkJi5LNIg2a/preview
driveID-theremin: 16tglseGb4wNgALPlMIAbMkoPkzuudzIi/preview
---
## Introduction
Welcome to the miscellanea section! This is where things that are too small to showcase on their own go. There won't be any boring documentation, just a quick blurb to give context about what makes it cool.

Everything here is the product of a "that would be kind of cool to try" moment plus a couple hours of work. I had a blast making these and hope you enjoy, too. There's plenty more to come in the future!


# Paddington
{% include googleDrivePlayer.html id=page.driveID-paddington %} <br />

This fellow's name is Paddington. Although he's lost his blue coat and red hat, Paddy has picked up 23 global accents - and become a spirit medium! Jokes aside, Paddington's heart runs off a RaspberryPi ZeroW and a battery pack in a recycled anti-static bag. The script loop constantly queries designated GroupMe channels looking for new messages to read out with the help of MACS, so anyone with a phone can talk though him, no set up required.

I promise its not just an audio file layered on top - I had to furiously type all the messages and commands each take, hence the long pauses! I actually plan to learn video editing and script-writing by making a series of skits with Paddy as the protagonist. However if you're interested in the code end of things, I'll go a bit further in depth in the [coding section](https://seth-so.github.io/portfolio/coding/){:target="_blank"}, so head there if you want more details!


<br />
# Theremin
Here's a theremin I made! I found a schematic from a 1961 issue of Electronics Illustrated (Rest in Peace) and immediately decided I had to make it. There are probably smaller, higher quality circuits, but the vacuum tubes really caught my interest since I'd never used them before. Breadboarding was actually pretty simple (power was landed to din rail-mounted terminal blocks). I probably should have made it on one board, but figured this way would be easier to mount different sections on the inside of a box.

Pitch Antenna Modulation            |  Pitch/Volume Mixer
:-------------------------:|:-------------------------:
![6BE6](https://github.com/seth-so/portfolio/raw/master/assets/img/justbecause/theremin-pitch.jpg) |  ![12AU7](https://github.com/seth-so/portfolio/raw/master/assets/img/justbecause/theremin-mixer.jpg)

Above are the 2 most important blocks of the schematic: the pitch receiver (left) and the volume mixer (right). The pitch receiver is driven by 2 6BE6 pentagrid converters, which modulates the input capacitance with a base reference frequency. The volume mixer is driven by the 12AU7 twin triode, which rides the pitch input with volume input (antenna oscillated with 500kHz crystal). The output sensitivity, octave, and range are controlled with 2 variable inductors. If you believe it, the whole thing worked first try, save for forgetting to make a power connection.

{% include googleDrivePlayer.html id=page.driveID-theremin %} <br />

I still need to make a nice box for it all and actually learn a song, but that isn't too high priority. If you're interested at all in making you're own, [here's the article](https://seth-so.github.io/portfolio/justcause/Theremin 1961 Electronics illustrated.pdf){:target="_blank"} that I used. Theremin making has a pretty welcoming niche on the internet, so google away! All data sheets are widely available.


<br />
# Swing Coach
![Swing Coach](https://github.com/seth-so/portfolio/raw/master/assets/img/justbecause/batterup.JPG "swing coach"){: .center-image }

This was a technology agnostic project in early school days (sophomore year?) before I knew how to make anything. The goal was to create a system to improve baseball bat-swing angle that was light weight and portable, specs predetermined. The end result was a modular stand assembly with a weight-shedded MDPE folding board.

The project actually had a "client" (non-paying 3rd party), and it was my first experience with building something for someone else. It went terribly. The deliverable was 2 months late, what was delivered failed on every spec. save that it stood upright, and the other 3 team members had pretty much quit on me half-way through. Still, I'm adamant it was a valuable learning experience. I managed to keep a dying project on life support and got a major crash-course in mechanical engineering! It was my first time with custom fasteners, CNC milling, Fusion360, and laser cutting - all tools that have become pretty integral to my fabrication skill set.


<br />
# Infinity Box
I'd wanted to make one of these ever since seeing my first infinity mirror, but never badly enough to make time. Well, quarantine happened and I got time to do so. So on one fine Saturday afternoon, I set out without a plan to make a box - and now I have one. The box is 13" x 13" x 12" made from acrylic applied with a one-way mirror film, framed with right angle pine trimmings from Home Depot, and all held together with general-purpose epoxy. The pine frame also hides a continous LED strip soldered in parallel to cover each inside edge. Below is a picture of the box with no lid covering a ceiling light!

![Infinity Box](https://github.com/seth-so/portfolio/raw/master/assets/img/justbecause/infinitybox.jpg "infinity box"){: .center-image }

Fun fact, the original intent for this build was to house my PC - due to eyeballed tolerances and a lack of clamps (pieces were held together by hand while curing), it didn't quite work out.  Now it sits on my shelf as a showcase for various objects around the house. The whole experience really brought a new appreciation for having the right tools for the job (including microfiber cloths to clean the fingerprints)!


<br />
# Blender
Blender was just one of those things that I decided to give a shot on a whim. I downloaded it thinking that it'd be super easy to pick it up since I have CAD sculpting experience, but boy was I wrong. My choice of learning method didn't quite speed things up either - I would skip to the hero shot of a tutorial video and try to recreate it on my own, using the actual content as hints. Solid in theory, except it took me about 6 hours to learn the UI that way.

![Still Life](https://github.com/seth-so/portfolio/raw/master/assets/img/justbecause/blender-stilllife.PNG "still life"){: .center-image }

Against all self-imposed odds, I managed to push through the initial learning curve and made it to a satisfactory point in a picnic scene. The table texture is procedurally generated, the apples and knife are painted with real picture projections onto a UV unwrapping, the water drops and grapes were generated with the particle system, and the cloth and swiss cheese were positioned using the in-house physics simulator. As I said earlier, this isn't quite done. I have a list of things to add to the scene (crackers, wine bottle + glasses, pears, dates, etc...), but those will be added more leisurely since I'm comfortable where this things are.

![Custom Blender](https://github.com/seth-so/portfolio/raw/master/assets/img/justbecause/blender-cathy.JPG "Cathedral of Learning"){: .center-image } <br />

Wow, did I really get that good at Blender that I can model a near [photo-perfect scene](https://github.com/seth-so/portfolio/raw/master/assets/img/justbecause/blender-cathy-compare.JPG){:target="_blank"}? Unfortunately not, but the real answer is pretty cool as well: Google Maps satellite mode may look 2D, but it actually contains hidden GIS metadata created by IDRISI Taiga. I used RenderDoc for process injection into Google Chrome to extract the map frame data into an .rdc file. With the help of extensions, Blender can interpret these files, import the height data, and skin the model according to satellite imagery. Add a point light and we have a nice sunset. <br /><br />
tl;dr - I made a 3D model from  Google Maps data - pretty cool, huh?

<br />
# ACCelerate Smithsonian Exhibition - Our Time is Up
*Our Time Is Up* was a civic engagement art exhibition at the Smithsonian (American History, Lemelson Center) for the inaugural ACCelerate Festival. The premise was a fictional audio drama made entirely from spliced bits of 2 unrelated autobiographical interviews from the [Legacy Project](https://www.legacyproject.org/){:target="_blank"}

I had the wonderful opportunity of designing and working on the physical component of the project. I designed and wired the electronics for the final display - an open air room, sparsely furnished, where the drama was supposedly taking place. The challenge was to integrate and wire 4 hidden 2-channel audio sources into the scene, and it took hollowing out everything and a lot of gaffer's tape top accomplish! Unforunately I don't have any pictures of my own, but here's the [exhibition page](http://acceleratefestival.com/acc_project/our-time-is-up/){:target="_blank"} to at least prove it exists. It was definitely a cool experience. I highly recommend you go if you're ever in the area during festival time.


<br />
# Sketches
Especially for engineers, the importance of sketching is super understated. It's an excellent real-time way to more clearly communicate with others and level expectations. I'm honestly surprised how many people readily dismiss it. It's better to spend 5 minutes sketching than committing hours to a CAD mock-up that the client doesn't even want. I'm definitely no artist, but I value it enough to practice! Check out some free-hand samples below:
![sketch collage](https://github.com/seth-so/portfolio/raw/master/assets/img/justbecause/sketch-collage.JPG "sketch collage"){: .center-image }


<br /><br />
# CRT Audio Oscilloscope
{% include googleDrivePlayer.html id=page.driveID-oscilloscope %} <br />

To cap things off is a project near and dear to my heart - my first electrical engineering project. This was the very definition of an amateur experience - solo late night near-death experiences, devolving my only laptop into an uncontrollable tinnitus machine, and best of all completely blowing out a university class' iMac right before final presentations were due. There are so many stories tied to this that I'll never forget.

The way it works is pretty simple. All you need to do is cross CRT i/o channels to create electronic synethesia (fancy speak for music visualizer). Switch x and y channels, replace video with audio to modulate the vertical deflection coil, toss in an amplifier, sprinkle in some balance-resistors, and voilà, you have an oscilloscope. Pretty simple process for an awesome result!

## More Coming Soon...
2. Rover - under construction
3. Jeff-Rosin Wooden Mirror - currently planning
