# Safety rules

> **Read this when** you are about to use any tool, machine or robot in the lab, before every new kind of experiment, and whenever something feels unsafe.

These are the lab's safety rules, from emergencies to cleaning up. Everyone who works in the Advanced Telerobotics Research Lab follows them, and each device page in [hardware](../hardware/README.md) adds rules for that device. The one thing to remember: **you are responsible for your own safety and your own actions**, and anyone may stop any activity they think is unsafe.

## Contents

- [Emergencies first](#emergencies-first)
- [Reporting injuries and hazards](#reporting-injuries-and-hazards)
- [Training](#training)
- [General rules](#general-rules)
- [Equipment rules](#equipment-rules)
- [Machine operation](#machine-operation)
- [Workbench and electronics](#workbench-and-electronics)
- [Robots in motion](#robots-in-motion)
- [Batteries](#batteries)
- [3D printing and resin](#3d-printing-and-resin)
- [Lasers and sensors](#lasers-and-sensors)
- [Safety mindset](#safety-mindset)
- [Safety attire](#safety-attire)
- [Cleanliness](#cleanliness)
- [Related](#related)

## Emergencies first

> [!CAUTION]
> **Fire, serious injury, smoke from a battery, someone unresponsive: call 911.** Kent State says to "Dial 9-1-1 for immediate help on all campuses" ([Campus safety](https://www.kent.edu/campus-safety)). Get yourself and others out first; then tell [lab safety contact] and the director.

| What | Where or who |
| --- | --- |
| Emergency (police, fire, medical) | **911** |
| Kent State Police, non-emergency | **330-672-2212**, Stockdale Safety Building, 530 East Summit Street ([Police Services](https://www.kent.edu/publicsafety/police-services)) |
| Kent State emergency guides (fire, tornado, hazardous materials, active threat) | [Emergency Management](https://www.kent.edu/publicsafety/emergency-management-services) |
| Emergency alerts | [Flash ALERTS](https://www.kent.edu/flashalerts): students, faculty and staff are enrolled automatically; keep your phone number current |
| First aid kit | [first aid kit location] |
| Fire extinguisher | [fire extinguisher location] |
| Eyewash station | [eyewash location] |
| Nearest exits and the building's evacuation assembly point | [evacuation route and assembly point] |
| Lab safety contact | [lab safety contact] |

Know the building's fire alarm, exits and evacuation procedure before your first day at the bench, and follow the instructions on safety signs and from emergency staff.

## Reporting injuries and hazards

- **Report every injury, however small, right away** to [lab safety contact] and the director, including cuts, burns and anything that touched your eyes.
- **Report every near miss and hazard** (a spill, a swollen battery, a robot that moved when it should not have, a broken guard, frayed wiring) to [lab safety contact], so it can be fixed before someone is hurt.
- **Kent State Environmental Health and Safety (EHS)** must also get a written report: 330-672-4347, <ehs@kent.edu>, Harbourt Hall, Room 323. The [incident reporting page](https://www.kent.edu/facilitiesplanning/incident-reporting) has three forms: an Employee Injury Report, a Lab Incident Report and a Non-employee Incident/Injury Report. EHS asks for injury reports within 48 hours, and notice within 8 hours for a serious injury; Kent State's [workers' compensation page](https://www.kent.edu/people-and-culture/benefits/workers-compensation) asks employees to report within 24 hours. Report the same day, and [lab safety contact] will help you pick the right form.

## Training

- Complete the lab safety orientation with [lab safety contact] before you use any tool, machine or robot.
- Never use a machine or robot until someone who is trained on it has trained you and signed you off: [how sign-offs are recorded].
- Ask [lab safety contact] which Kent State EHS courses you need (they run in FlashTrain). EHS courses must be repeated every three years ([EHS training](https://www.kent.edu/facilitiesplanning/training)).

## General rules

- Know the fire alarm, safety signs and the building evacuation procedure, and follow the instructions in an emergency.
- Know where the lab's safety equipment is and how to use it (see the [table above](#emergencies-first)).
- No eating or drinking in the lab.
- Report all injuries.
- Know all of these rules, and the rules on the device page before you use a device.
- Clean your area when you are done. If cleaning supplies have run out, report it.
- You are ultimately responsible for your own safety and actions.

## Equipment rules

- Wear the safety gear the task calls for: safety glasses, gloves, masks.
- Use only equipment you have been trained and allowed to use.
- Record every checkout and return of equipment ([equipment checkout](best-practices.md#equipment-checkout)).
- Unplug equipment and store it properly when you are done.
- Report any missing, malfunctioning or damaged equipment.
- Do not interrupt someone who is using equipment.

## Machine operation

- Never use a machine unless a trained lab staff member has trained you on it and you know how to use it safely. If you have questions, ask; nobody minds.
- Do not use any equipment that is not working properly. Report it to [lab safety contact], and put an "out of order" sign on it so nobody else uses it.
- Turn devices off when you are done.

## Workbench and electronics

Every student and researcher in the lab needs the skills to keep the bench safe for everyone.

### Soldering

> [!WARNING]
> A soldering iron tip is hot enough to burn skin instantly, and solder fumes irritate the lungs. Wear safety glasses and use the fume extractor every time.

- Wear safety glasses when you cut wire, trim component leads or solder; clipped leads fly.
- Never touch the tip of a soldering iron to find out whether it is hot. Return the iron to its stand every time you put it down.
- Do not melt a ball of solder on the tip and carry it to the joint. If the ball drops, molten solder splatters.
- Use the fume extractor to remove and filter the fumes whenever you solder.
- Wash your hands after soldering, especially before you eat.
- New to soldering? Watch a tutorial first, such as the [soldering tutorial for beginners (oneTesla)](https://www.youtube.com/watch?v=Qps9woUGkvI) or EEVblog's soldering tutorials ([part 1, tools](https://www.youtube.com/watch?v=J5Sb21qbpEQ); [part 2](https://www.youtube.com/watch?v=fYz5nIHH0iY)), and on fumes, [PACE's fume extraction video](https://www.youtube.com/watch?v=KVaN3vTXY9E).

### Components that can burst, burn or get hot

- **Electrolytic capacitors are polarized**: they have a "+" side and a "-" side, and they can burst open or explode if placed in a circuit backward ([video: reverse voltage](https://www.youtube.com/watch?v=jnPQCZ0Sfsg)).
- **Tantalum capacitors** can catch fire if used incorrectly ([video: SparkFun](https://www.youtube.com/watch?v=sW0a9d_vWoc)).
- **Never exceed a capacitor's voltage rating**; it may explode ([video: excessive voltage](https://www.youtube.com/watch?v=_WheLp0RdLQ)).
- **LEDs** can pop, burst or catch fire without a current-limiting resistor, or with one that is too small ([video](https://www.youtube.com/watch?v=ZXEZtePxa0U)).
- **Some parts run hot even when they work properly.** Linear voltage regulators, for example, are often bolted to a heat sink; without one, some get hot enough to cause severe burns. Touch-test nothing; use a thermometer or wait.

### Oscilloscopes and mains power

Some oscilloscopes have floating (isolated) inputs; on others, the probe ground is connected to mains earth, and clipping it to a live mains circuit creates a short. You often cannot tell which kind you have. **Do not measure mains power with an oscilloscope.** If a measurement on mains is unavoidable, ask [lab safety contact] first and use an isolation transformer.

### Before you start an experiment

- **Be prepared.** Read and understand the procedure for the experiment before you begin. If you do not understand it, see [lab safety contact].
- **Think safety.** Work deliberately and carefully. No horseplay.
- **Know the hazards** of every material and machine you use. The procedure, or the person supervising, will review specific safety issues before you run a test.
- **Wear the right protective equipment.** Safety goggles are worn whenever a lab experiment is being performed; some experiments need more.
- No food or drink at the workbench.
- Know the emergency procedures, fire escape routes and where the nearest phone is.
- **Report hazards immediately**: spills, equipment malfunctions, injuries and anything else that looks unsafe, to [lab safety contact].
- Keep your work area clean.

## Robots in motion

Robots are heavy, fast and strong, and they do not know you are there. These rules apply to every robot; each device page adds its own: [Unitree Go2](../hardware/unitree-go2.md#safety), [Booster K1](../hardware/booster-k1.md#safety), [OpenManipulator-X](../hardware/openmanipulator-x.md#safety), [LeRobot SO-101](../hardware/lerobot-so-101.md#safety) and [Yahboom ROSMASTER X3](../hardware/rosmaster-x3.md#safety).

> [!WARNING]
> Never stand in a robot's reach or path while it is powered and enabled, and never leave a powered robot unattended.

- **Only trained people operate a robot**, and one named person is in charge of each session.
- **Find the emergency stop first.** Before every session, locate the robot's stop (a button, a remote or the power switch) and test that it works. The operator keeps it within reach the whole time.
- **Clear and mark the area.** Move people, cables, bags and liquids out of the test area: [how the lab marks a robot test area]. Say "robot moving" before you enable motors.
- **New code runs in simulation first**, then on the real robot at low speed or torque, with a legged robot on its stand or in a safe lying position when the device page says so.
- **Keep hands, hair and cables away from pinch points**: arm joints and grippers, legs and wheels.
- **Legged and humanoid robots can fall, jump or kick.** Keep a spotter, keep the area clear of people who are not part of the test, and never try to catch a falling robot with your hands.
- **Teleoperation:** if the video lags or the connection drops, stop the robot before you try to fix it. Test what the robot does when it loses the connection before you rely on it.
- **Autonomous code, trained policies and AI coding agents** never run on a robot unless a person is watching with the stop in reach ([AI coding agents](../tech-stack/claude-code.md#lab-rules-for-ai-coding-agents)).
- **Visitors and minors** stay outside the test area and do not operate robots unless a trained member supervises them one-to-one.
- **When you are done**, disable motors, power the robot down, remove or disconnect its battery and put it back in its place.

## Batteries

Most lab robots run on lithium batteries (LiPo or Li-ion), which can catch fire if they are damaged, overcharged or short-circuited. Each device page has the rules for its own battery pack.

> [!CAUTION]
> If a battery smokes, hisses, swells quickly or catches fire, leave the room, pull the fire alarm and call 911. Do not try to put out a battery fire unless you are trained to.

- **Charging:** use only the charger made for that battery, or a balance charger set to the right chemistry and cell count. Charge on a non-flammable surface or in a fire-resistant charging bag or box, [battery charging location], and never leave a charging battery unattended or charging overnight.
- **Before you charge:** let a hot battery cool down first, and never charge a battery that is swollen, dented, punctured or leaking.
- **Storage:** store batteries in [battery storage location], in fire-resistant containers, away from heat and direct sun, at the storage charge level (most chargers have a "storage" mode). Do not store batteries inside robots.
- **Damaged cells:** a swollen ("puffy"), dented, punctured, leaking or unusually hot battery is out of service. Stop using it, move it into a fire-resistant container if you can do so safely, label it "damaged" and tell [lab safety contact]. Never put a lithium battery in the trash.
- **Disposal:** Kent State recycles rechargeable batteries, including lithium-ion, through the Call2Recycle program ([Kent State zero waste](https://www.kent.edu/sustainability/zero-waste)). For damaged batteries, ask EHS (330-672-4347, <ehs@kent.edu>) how to dispose of them.
- Tape over the terminals of loose batteries so they cannot short-circuit.

## 3D printing and resin

The Formlabs Form 3 prints with liquid photopolymer resin and parts are washed in isopropyl alcohol (IPA). Both are hazardous. The device rules are on the [Formlabs Form 3 page](../hardware/formlabs-form-3.md#safety).

- **Wear nitrile gloves and safety glasses** when you handle liquid resin, uncured parts or used IPA, and work with good ventilation. If resin touches your skin, wash it off with soap and water.
- **Read the safety data sheet (SDS)** for each resin before you use it: [SDS location].
- **IPA is flammable** ([Formlabs](https://formlabs.com/support/Isopropyl-Alcohol-IPA/)). Keep it closed, away from heat and sparks.
- **Never pour liquid resin, or IPA with resin in it, down a drain or into the trash** ([Formlabs: disposing of resin](https://formlabs.com/support/Disposing-of-resin/)). Fully cured resin can go in the regular trash; liquid resin and used IPA are handled as hazardous waste through Kent State EHS (330-672-4347, <ehs@kent.edu>): [lab resin and IPA waste procedure].

## Lasers and sensors

Lidars, depth cameras and some motion-capture systems emit laser or infrared light.

- **Check the laser class** on the device label or in its manual before you use it. Class 1 devices are safe under normal use.
- Do not stare into any emitter, and never look at one through binoculars, a camera lens or other optics.
- Do not bring a laser pointer or any laser above Class 2 into the lab without approval from [lab safety contact]. Ask Kent State EHS before anyone uses a Class 3B or Class 4 laser.
- Cameras and microphones on robots record people. Follow the [privacy rules](code-of-conduct.md#privacy) before you record anyone.

## Safety mindset

- Never work when you are tired, stressed or unable to work carefully.
- Never interrupt or distract a person operating a machine or robot, or walk directly behind them.
- Never put hands or other body parts near a cutting head, blade, drill, pinch point or any other moving, rotating or cutting part. Clear hand tools, accessories and other objects from the work area before you start a machine.
- Make sure all safety devices (guards, shields, light curtains, emergency stops) work and are in place before you operate any equipment.
- Keep aisles, exits and access to emergency equipment clear at all times.

## Safety attire

Wear clothing and personal protective equipment (PPE) that fit the task. In the lab at all times:

- **Footwear** covers the whole foot, stays secure on all sides and gives a stable, non-slip footing. Sandals, clogs, ballet flats and heels are not acceptable.
- **Long hair, including beards**, is tied back away from the face and neck. If it is long enough to tie back, tie it back.
- **No loose clothing**, including ties, scarves and loose sleeves.
- **Remove jewelry** before you start work: rings, earrings, necklaces, bracelets and watches.
- **Gloves** protect you from hot or hazardous materials, but never wear gloves when you operate a machine with moving parts; they can be pulled in.
- **No corded headphones or earbuds**: cords can catch in machinery, and you must be able to hear others in the lab at all times.
- **No phones or other personal devices** while you work at a machine.

## Cleanliness

A clean lab is a safer lab. Everyone cleans up after themselves and disposes of waste the right way, both while working and when finished.

- Never use compressed air to clean machinery, skin or clothing. Use a vacuum, broom and dustpan.
- Clean up spilled liquids right away. If the liquid is hazardous or oily (resin, IPA, battery electrolyte, oil), keep people away and contact [lab safety contact] so it is cleaned up the right way.
- Put tools back, and throw away solder scraps, wire clippings and packaging.

## Related

- [Lab rules](README.md)
- [Code of conduct](code-of-conduct.md) and [best practices](best-practices.md)
- [Hardware](../hardware/README.md): each device page has a safety section
- [Kent State Environmental Health and Safety](https://www.kent.edu/facilitiesplanning/environmental-health-and-safety)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/lab-rules/safety.md)</sub>
