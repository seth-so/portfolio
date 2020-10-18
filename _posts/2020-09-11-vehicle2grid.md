---
layout: post
title: vehicle-2-grid
summary: Design, custom simulation, and testing of bidirectional charging loop between 2010 Chevy Volt and Eaton Power Systems Experience Center microgrid
featured-img: emile-perron-190221
categories: Design, Theory, Fabrication
driveID-oscilloscope: 1FHsHbRkRPVA9ganmYhuZUxkJi5LNIg2a/preview
---
## Introduction
Vehicle2Grid was a fantastic industry project experience from mid-late 2019. The project began as a pitch to [Eaton Corporation](https://www.eaton.com/us/en-us.html){:target="_blank"} to create a permanent demo installation at their Power Systems Experience Center ([PSEC](https://www.eaton.com/us/en-us/markets/eaton-experience-centers/pittsburgh.html){:target="_blank"}) in Pittsburgh, Pennsylvania - the concept was to use Eaton equipment to create a bidirectional charging loop that allowed them to both charge their Chevy Volt from the building, and charge their building from the Chevy Volt as well without affecting the driving capabilities of the car.

It'd be hard to condense such a big undertaking into so a short portfolio piece, so this will be pretty long. I'll still edit for brevity to avoid bringing up every thought, plan, and dead end we hit, but if you're looking to get the 1 minute version, here's a poster I made for the   

I'd like to thank Eaton for providing the opportunity and the whole crew at PSEC, especially Dan Carnovale, Eric Hurd, and Amit Gholam, for their unwavering support and technical advising throughout the process!

![V2Gschematic](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/intro-schematic.PNG){: .center-image }


# Vehicle2Grid
The national power grid is suffering from increasing instability due to 1. increased integration of unsteady renewable power generation like solar and wind, and 2. highly variable energy demand throughout the day. Additionally, smarter systems and distributed energy resources continue to add complexity in power systems. Due to its massive scale and inertia, this can cause primary generation to have trouble compensating for varying loads. Helping balance power demand and supply has been an core issue in the power industry, as an unstable grid can result in dirty power output and increased risk of black outs and shutdowns.

![duck-curve](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/problem-duck.PNG){: .center-image }

One of the main solutions to grid stability has been found in battery storage - battery systems charge can when energy demand is low and then return energy back to the power system when demand rises, therefore leveling demand. For the same sustainability objectives as renewables, there has been a growth in both hybrid EVs and pure EVs. As of 2016, there were around 2 million electric vehicles on the roads, and that number continues to rise. These EVs can serve as battery storage when they are not in use, which is often as at given time, 95% of cars are parked.

If an interface could be made to between EV battery and grid, the batteries could be tapped to act as peripheral generators and help stabilize demand fluctuations. Therefore, EVs have the potential to fill the gap between the need for energy storage and renewable energy integration and grid support. This emerging concept, known as Vehicle-to-Grid (V2G), has limited realization and no regular implementation in the U.S. V2G refers to load balancing through bidirectional power flow – that the grid can charge the EV, and the EV can also charge the grid. The use of HEVs/EVs and V2G-based energy redistribution could significantly aid the goal of achieving a horizontal demand load throughout the day, ultimately increasing grid reliability.


## Prior Art
While the concept of bidirectional charging has been around for a while, there had been very few realizations, and none between an electric vehicle and a [microgrid](https://en.wikipedia.org/wiki/Microgrid#:~:text=A%20microgrid%20is%20a%20decentralized,physical%20or%20economic%20conditions%20dictate.){:target="_blank"}, there have been few queries into this topic. In the 2018, the University of California, San Diego, has been implementing and observing the effects of a V2G fleet used solely on campus properties in order to help reach a carbon neutral footprint. In Japan, Toyota Tsusho has heavily invested in an upcoming V2G based company, Nuvve, in hopes of promoting virtual generation sources. This is the same company that is launched its pilot program at UCSD mentioned before. Additionally, Nissan has implemented their EV batteries in disaster relief scenarios as back-up battery walls. However no work has been done towards consumer side load-balancing, the goal of this project.

![v2g](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prior-concept.png){: .center-image }


## Project Scope
Before beginning the base requirements from the project were defined. While there was a lot of flexibility due to uncertain nature of the project, the proposed timeline spanned 15 weeks to accomplish the following 5 major tasks:

1. Reverse engineer the Volt’s communications system and hardware
2. Retrofit the microgrid and the Volt with custom adaptors to enable cross-compatibility
3. Design a high voltage control system to safely allow bidirectional current flow between the car and microgrid
4. Set up a local network to process data for control and a programmable user interface, including a full emulator routine.
5. Preserve all driving capabilities of the car.

Major hurdles included mapping out the car’s system safeties so that they could be bypassed and learning to manually override several car functions. Design iterations included changes in communication protocols, adding safety redundancies, and reconfiguring the schematic for compatibility and efficient design. The touch screen interface also underwent several graphical interfaces for more intuitive design, while still offering all salient power flow information.

My personal roles and contributions:


## Environment
The microgrid at PSEC has generation sources of the utility source, a 100kW generator, two photovoltaic solar panel arrays, lithium ion batteries, a windmill, and supercapacitor wall. The microgrid power system provides both 480-volt 3-phase and 208-volt 3-phase power to the building load systems and components. Integration of the Chevy Volt into the microgrid will provide another source of generation and load to the building power system. The figure below, taken directly from PSEC’s microgrid monitoring system, presents the software control interface for Eaton’s PSEC microgrid

![psec-microgrid](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/environment-psecgrid.png){: .center-image }

The graph at the bottom of the figure shows the breakdown of the generation sources and fluctuations in load demand throughout the day. It is apparent that the utility (yellow) does not have a level demand curve, that the solar generation (green) is highly variable on this specific day, and the load (red) contains much variation as well. However, looking at the battery storage (blue), its clear that through the use of charging and discharging, the battery storage is able to keep the utility close to horizontal during the first section of the day with high demand. This is exactly the idea of utilizing the battery component of an electric vehicle as an energy storage component for the purpose of utility grid stability. in this case a 16kWh-380V Chevy Volt battery

![chevyvolt](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/intro-car.PNG){: .center-image }


## Prototyping Milestones

### First Battery discharge with Volt

Test Load Circuit          |  Custom Connection to Volt Battery
:-------------------------:|:-------------------------:
![testload](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-testbed.png) |  ![battery-tap](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-batteryout.png)

feasibility testing - custom adaptor directly from car battery.


### Manually controlling battery contactors

![chevyvolt](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-hpcm.png){: .center-image }
contact control


### Resolving Diagnostic Trouble Codes

DTC Examples          |  Internal Software Lockouts
:-------------------------:|:-------------------------:
![dtc](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-dtcs.png) |  ![theft-screen](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-theft.png)

network, blackbox discussion, can, gmlan


### Integration of Eaton components into First Prototype

Core Components          |  Wired
:-------------------------:|:-------------------------:
![base](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-components.PNG) |  ![wired](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-board.png)


### Creating Local Network Gateway
several thousand lines of code to set up local host website for monitoring

### Signal Fuzzing
[[[picture of waking up car]]]

Relay Mount          |  Wake-up Signal Generator
:-------------------------:|:-------------------------:
![Pi-Relay](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-relays.png) |  ![wakeup](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-wakeup.png)


### Human Machine Interface
[[[HMI interface]]]


![HMI+Emulator](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-hmi.png){: .center-image }


## Completed System Design

![schematic](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-schematic.PNG){: .center-image }

![circuit](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-final.png){: .center-image }


not shown are: auxilary components (crydom rectifier, dc disconnect, ac disconnects, inverter)


## Final Implementation

![HMI+Emulator](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/final-context.png){: .center-image }

Closed          |  Open
:-------------------------:|:-------------------------:
![closed](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/final-closed.png) |  ![open](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/final-open.png)

[[[table of results]]]


### final timeline and component
