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

It'd be hard to condense this into a short portfolio piece, so this will be pretty long. I'll still edit for brevity to avoid bringing up every thought, plan, and dead end we hit, but if you're looking to get the 1 minute version, here's a [poster version](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/poster-scrubbed.pptx) I made just for you. Probably the largest challenge in this project was the lack of available documentation. Aside from the odd YouTube video and connector pinout, the Chevy was essentially a black box. Troubleshooting problems often required hours of research to form a hypothesis and attempt a solution. Still, aside from a few blown fuses and sometimes something bigger, the project was a big success.

I'd like to thank Eaton for providing the opportunity and the whole crew at PSEC, especially Dan Carnovale, Eric Hurd, and Amit Gholam, for their unwavering support and technical advising throughout the process. None of this would have been possible without them! Team member contributions are at the end.

![V2Gschematic](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/intro-schematic.PNG){: .center-image }


# Vehicle2Grid
The national power grid is suffering from increasing instability due to 1. increased integration of unsteady renewable power generation like solar and wind, and 2. highly variable energy demand throughout the day. Additionally, smarter systems and distributed energy resources continue to add complexity in power systems. Due to its massive scale and inertia, primary generation can have trouble compensating for varying loads. Helping balance power demand and supply has been an core issue in the power industry, as an unstable grid can result in dirty power output and increased risk of black outs and shutdowns.

One of the main solutions to grid stability has been found in battery storage - battery systems charge can when energy demand is low and then return energy back when demand rises, therefore leveling demand. For the same sustainability objectives as renewables, there has been a growth in both hybrid EVs and pure EVs. As of 2016, there were around 2 million electric vehicles on the roads, and that number continues to rise. These EVs can serve as battery storage when they are not in use, which is often as at given time 95% of cars are parked.

![duck-curve](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/problem-duck.PNG){: .center-image }

If an interface could be made to between EV battery and grid, the batteries could be tapped to act as peripheral generators and help stabilize demand fluctuations. Therefore, EVs have the potential to fill the gap between the need for energy storage and renewable energy integration. This emerging concept, known as Vehicle-to-Grid (V2G), has limited realization and no regular implementation in the U.S. V2G refers to load balancing through bidirectional power flow – that the grid can charge the EV, and the EV can also charge the grid. The use of HEVs/EVs and V2G-based energy redistribution could significantly aid the goal of achieving a horizontal demand load throughout the day, ultimately increasing grid reliability.


## Prior Art
While the concept of bidirectional charging has been around for a while, there have been very few realizations, and none between an electric vehicle and a [microgrid](https://en.wikipedia.org/wiki/Microgrid#:~:text=A%20microgrid%20is%20a%20decentralized,physical%20or%20economic%20conditions%20dictate.){:target="_blank"}. In the 2018, the University of California, San Diego, has been implementing and observing the effects of a V2G fleet used solely on campus properties in order to help reach a carbon neutral footprint. In Japan, Toyota Tsusho has heavily invested in an upcoming V2G based company, Nuvve, in hopes of promoting virtual generation sources. This is the same company that launched the pilot program at UCSD mentioned before. Additionally, Nissan has implemented their EV batteries in disaster relief scenarios as back-up battery walls. However no work has been done towards consumer side load-balancing, the goal of this project.

![v2g](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prior-concept.png){: .center-image }


## Project Scope
Before beginning the base requirements from the project were defined. While there was a lot of flexibility due to uncertain nature of the project, the proposed timeline spanned 15 weeks to accomplish the following 5 major tasks:

1. Reverse engineer the Volt’s communications system and hardware
2. Retrofit the microgrid and the Volt with custom adaptors to enable cross-compatibility
3. Design a high voltage control system to safely allow bidirectional current flow between the car and microgrid
4. Set up a local network to process data for control and a programmable user interface, including a full emulator routine.
5. Preserve all driving capabilities of the car.

Major hurdles included mapping out the car’s system safeties so that they could be bypassed and learning to manually override several car functions. Design iterations included changes in communication protocols, adding safety redundancies, and reconfiguring the schematic for compatibility and efficient design. The touch screen interface also underwent several graphical interfaces for more intuitive design, while still offering all salient power flow information.


## Environment
The microgrid at PSEC has generation sources of the utility source, a 100kW generator, two photovoltaic solar panel arrays, lithium ion batteries, a windmill, and supercapacitor wall. The microgrid power system provides both 480-volt 3-phase and 208-volt 3-phase power to the building load systems and components. Integration of the Chevy Volt into the microgrid will provide another source of generation and load to the building power system. The figure below, taken directly from PSEC’s microgrid monitoring system, presents the software control interface for Eaton’s PSEC microgrid

![psec-microgrid](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/environment-psecgrid.png){: .center-image }

The graph at the bottom of the interface shows the breakdown of the generation sources and fluctuations in load demand throughout the day. It is apparent that the utility (yellow) does not have a level demand curve, that the solar generation (green) is highly variable on this specific day, and the load (red) contains much variation as well. However, looking at the battery storage (blue), its clear that through the use of charging and discharging, the battery storage is able to keep the utility close to horizontal during the first section of the day with high demand by offsetting the variable load. This is exactly the idea of utilizing the battery component of an electric vehicle as an energy storage component for the purpose of utility grid stability. in this case a 16kWh-380V Chevy Volt battery

![chevyvolt](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/intro-car.PNG){: .center-image }


## Prototyping Milestones
These are the major milestones throughout the project, whether it be first power draw or establishing a new connection with a custom adaptor. It's not quite a linear presentation, but there's a full timeline at the end for that.


### First Battery discharge with Volt
The first big step was reading voltage off the main car battery. I spent several days looking at different Chevy Volt tear down videos before popping the hood. The inverter was easy to locate, and the primary battery connection was secured on with just 2 hex bolts. The first custom connection had to be made to interface snugly with the battery cable slat prongs. Additionally a high power testbed was quickly put together with a manual disconnect and fuses for safety.

Test Load Circuit          |  Custom Connection to Volt Battery
:-------------------------:|:-------------------------:
![testload](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-testbed.png) |  ![battery-tap](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-batteryout.png)

We quickly ran into built in safety nets. The battery has 2 signal controlled safety contactors to prevent accidental shorts. Additionally, these hot weld shut if forcefully switched under load, that is if the car is on. However, just under the passenger sheet is the hybrid power control module 2 (HPCM2). The HPCM2 connector establishes communication for various drive components of the car, including the controls for the battery contactors. This signal was tapped with a custom X1 connector in order to close the battery contactors for discharging by the system. The wire bundles allow for communications to be maintained between the vehicle’s modules. If these connections are not maintained, the vehicle will send a diagnostic trouble code (DTC), which will prevent the car from charging or turning on when the system is disconnected. To control the battery contactors, a 12V DC signal must be sent to pins 6, and 9 and pin 1 must be grounded to force the contactors to close to allow discharging to the microgrid. This method allows for control even when the car is off.

Custom HPCM connector      |  In Volt
:-------------------------:|:-------------------------:
![connector](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-hpcmconnect.png) |  ![hpcm](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-hpcm.png)

Connecting the car battery to this circuit was one of the most important steps, because it determined feasibility of the project - whether power could be drawn from the car without affecting driving afterwards. 380V was successfully at terminal connections, and the function behaved as expected. A lamp was connected in series for visualization but was blown out quickly.


### Resolving Diagnostic Trouble Codes
Diagnostic trouble codes (DTCs) were one of the biggest hurdles of the project. Before I mentioned that Volt was a black box, and this is where it really came into play. Now that we were tampering with car communications and power levels, the car was constantly seizing, locking, and misbehaving. I used a cheap OBDii reader to view these - different combinations of about 23 different triggers were tripped every time we connected cables in a different order, many of which were direct antitampering measures. This experience informed the design plan - originally the goal was to send manual signals to get various data off the car after tapping into the GMLAN and CAN networks, but
this wouldn't be feasible without proprietary knowledge.

DTC Examples               |  Internal Software Lockouts
:-------------------------:|:-------------------------:
![dtc](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-dtcs.png) |  ![theft-screen](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-theft.png)

Through sheer trial and error, we slowly mapped out what caused different flags, which were false signals, and most importantly which were legitimate system warnings. One of the difficult aspects was that the description was rarely relevant since we were inducing the DTCs artificially. By the end, we found P0AA1-00, P0C76-00, U1783-00 were the ones to avoid, each truly indicating physical hardware failure (That was P0C76-00 was a sign of primary contactor welding and completely locked out any user interaction). This process was one of the most stressful - it involved an internet wide puzzle hunt to pick up clues on what may actually be happening within the car. Every DTC that was thrown was its own roller coaster of emotion trying to figure it out - after several weeks and countless tests, we found a particular sequence that didn't trigger any DTCs.


### Integration of Eaton components into First Prototype
Eaton hardware was ideal for this project. At its core, the board needed to have controllable safety components that could all communicate with each other and reliable power supplies. The 6 core components we based the design around were 2 Power Defense Breakers (trip configurable, metered thermal breakers), an AC and DC contactor (not shown), and 12V and 24V power supplies. Two further components were integrated to allow for network communication, a Power Xpert ethernet network switch (collects the metered power information from the breakers) and a Power Xpert network gateway, (converts the breaker data from serial to ethernet protocol for communication with the RaspberryPi).

Core Components            |  Wired
:-------------------------:|:-------------------------:
![base](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-components.PNG) |  ![wired](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-board.png)

The left image shows the base components mentioned, and the right shows it all din-rail mounted and wired. It looks a little messy because of the excess wire lengths, but each connection was made carefully and tested sequentially during construction. All board-external input and outputs are landed to terminal blocks, fused, and spliced to medium voltage Eaton Arrow-Hart locking connectors. Completion of the hardware side meant that the software portion of the project could then begin - multithreading the main control algorithm with multiple safety contingencies, establishing communication between all components, and formatting data for the human machine interface (HMI) GUI.


### RaspberryPi
The brain of board is the RaspberryPi3b+. The RaspberryPi was chosen to handle the control of the system because a robust processor was needed to be able to run Python scripts to handle Modbus protocol communications, control the actuation of four relays, read and interpret Power Defense Breaker data, and convert and send data to the HMI to be displayed neatly for the user, as well as run multiple safety threads in the event of loss of communication with different components in the system.

A four-relay hat and a custom hardware solution for the CAN bus wake-up signal sit on top. The hat is used for several different aspects of the system. Relay 1 is used to control the switching of the CAN bus wake-up signal detailed below. Relay 2 is used to control the 12V signal for manual Volt HV contactor control, and Relays 3 and 4 are used for controlling the DC and AC power flow path contactors, respectively. All relays are actuated by 3.3V by assigning values to specific addresses defined by the board.

The RaspberryPi receives communications from all of the network devices on the board; it also obtains critical data from the vehicle via the OBDii port located to the left of the steering column in the Volt. Using an ELM327 OBD II connector hardwired to one of the RaspberryPi’s USB ports, the RaspberryPi can monitor the SoC of the battery by using a simple data polling script while the CAN network is awake. This is necessary for battery health and target setting control calculations.

![wakeup](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-pi.png){: .center-image }


### Signal Fuzzing
In order to properly obtain the SoC readings from the vehicle, the CAN network must remain on. This requirement does not pose a problem during charging; however, when the battery is discharging, it is critical that SoC be monitored properly. Since the car is off when charging and discharging are occurring for this system, the CAN network is also off. This either throws an error to the RaspberryPi or fuzzes the incoming data to be nonsensical as the signals attenuates.

Therefore, a solution was developed to ensure that the CAN network would remain on when the car is off and discharging. After identifying several wake-up options though OBD polling, I came up with a method of simulating a wireless unlock signal to ping the car and keep the network awake. To implement this, a secondary fob PCB was synced with the car and wires were soldered across the remote start button, broken in-between by the relay such that a close would emulate a button click. The PCB itself was powered by 3.3V from a GPIO pin on the RaspberryPi. The RaspberryPi is programmed to actuate the wake-up signal twice every 15 seconds while the battery is discharging and once every 5 minutes while the car is charging.

![wakeup](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-wakeup.png){: .center-image }


### Human Machine Interface (HMI)
HMIs are Eaton’s standard for user interfaces. It is a touchscreen programmed with Eaton’s Visual designer to help visualize power systems and is particularly useful for demonstrations. It also serves as a convenient way to control the system as well as display a simplified version of the overall system. I programmed the main GUI to reflect the current circuit status, real power time statistics, and a user control side.

The column in the left is a user-controlled section where desired parameters can be set to the system. In system mode, the user can choose between automated mode or manual mode. In manual mode, user has the ability to choose between charge, discharge, and idle whereas in automated mode, the charge/discharge will be triggered based on current state of charge. When targeted state of charge is higher/lower than the current state of charge, the system will automatically charge/discharge to the set target. Full power charging and half power charging are also given as an option for the user to charge the vehicle automatically to full power or half power, and these may be reprogrammed to any convenient settings.

![HMI+Emulator](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-hmi.png){: .center-image }

A global minimum and maximum state of charge may be set in order to keep the battery within optimal operating range. Using VBScript, the charging/discharging process will automatically stop when the current state of charge is at maximum/minimum. Another concern is addressed regarding the familiarity of state of charge term among user. To solve this issue, conversion is made by using algorithm obtained from state of charge-mileage mapping. So, when mileage is considered, it will then convert the value inputted to its respective state of charge.

Additionally, the RaspberryPi can be set to feed fake data to the HMI and act as a full emulator for demonstration purposes. In this case, an accelerated duck curve is generated to mimic daily load, and the user can control charge and discharge times to help flatten the curve (shown in the figure above).

## Completed System Design
The schematic from the very beginning is shown here in 4 blocks for charge loop, discharge loop, control network, and auxiliary circuitry:

![schematic](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-schematic.PNG){: .center-image }

The microgrid bus voltage flows into the charge path through a manual disconnect, where the path is protected and monitored by an Eaton Power Defense Breaker. The existing portable Eaton EV charger was then connected in series with the charge path breaker. From the charger, power flows through an AC contactor, which is controlled by the RaspberryPi. This power flow will charge the car battery through the existing J1772 charge port connector.

The discharge side of the system is similar. The system is connected to the Chevy Volt’s HV battery through a Power Inverter Module High Voltage Interface Cable which was modified to connect to the team’s system. The car connection is then wired through a manual disconnect for extra safety to the DC contactor, which is contained in a separate housing. This contactor connects the power flow to the Fronius Symo Advanced 10.0-3 208-240 inverter. From the inverter, the power flows through the discharge Power Defense Breaker, where it is then fed back into Eaton’s microgrid through the AC manual disconnect.

Communications were all ran through the RaspberryPi. Power Defense Breaker Data was sent to Power Xpert Gateway and communicated via a network switch to the RaspberryPi and HMI. The RaspberryPi communicated with the HMI and Gateway using Modbus-TCP, and with the Chevy volt using GDSii protocol, collating all data on a local Modbus server for easy monitoring and access through serial lines. All programming was done in Python.

Auxiliary components included a Crydom rectifier, various safety or power circuitry, as well as a 120V receptacle for convenience. Below is a picture of the circuit transferred to a 30"x30" steel back plate with panduit for cable management. Special attention was given to wire routing so as to minimize crossing signal and power wiring.

![circuit](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/prototype-final.png){: .center-image }

## Final Implementation
System specification and performance as an actual bidirectional charger between the PSCE microgrid and the EVs is as follows:
1. __Accuracy__
  - charge to set point target:            < 1% error
  - discharge to set point target:         < 1% error
  - estimated time to set point target:    < 5% error
2. __Speed__
  - full charge:                             6hrs  @ 3kW/hr
  - full discharge:                        1.5hrs  @ 10kW/hr
  - charge-discharge switch:                  90s
  - discharge-charge switch:                  15s
3. __Safety Algorithms__
  - event: HMI loses connection: open contactors
  - event: Pi loses connection: open contactors
  - event: Vehicle network fails: open contactors
  - event: Min/Max battery bounds exceeded: open contactors

Once all verification tests and safety checks had passed, the board and HMI were mounted into a custom Eaton box and mounted to the wall next to the entrance of PSEC where it sits today. When it is not attached to the Chevy Volt, it is running in emulator mode to help demonstrate load balancing and power redistribution to 7000 annual PSEC guests.

Closed                     |  Open
:-------------------------:|:-------------------------:
 ![closed](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/final-closed.png) |  ![open](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/final-open.png)

![mounted](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/final-context.png){: .center-image }


### Responsibilities
While both of our parts certainly overlapped and we worked together throughout the whole project, this was the general breakdown of roles by time spent:

My personal roles and contributions:
1. Led hardware and construction efforts, including prototyping, designing, constructing, and wiring both initial final board + making custom connectors
2. Troubleshot all DTC’s and came up with solutions or work arounds so that the system could interact with the car without causing errors
3. Research car communication systems to conceptualize and make wakeup signal generator
4. Programmed the user interface of the HMI and added data visualization
5. Completed all paperwork, documentation, and ordering

Nate Carnovale roles and contributions
1. Operated and set up Microcontroller
2. Programmed Multithreaded Control logic for all system functions
3. Created local network for data metering
4. Performed hardware testing and verified all expected function
5. Established inter-device communication and operation

### Miscellaneous
Final project timeline:
![timeline](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/final-schedule.PNG){: .center-image }

Final parts list:
![parts](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/final-parts.PNG){: .center-image }

First drawing of project plan on pizza plate:
![first](https://github.com/seth-so/portfolio/raw/master/assets/img/v2g/final-beginning.png){: .center-image }
