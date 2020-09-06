
---
  title: Core Features
---


# Core Functionality
This component started out as an AppDaemon script implementation of motion activated lighting but it has since been generalised to be able to control any Home Assistant entity. I have discussed the set of original core requirements for motion lights [on my blog](https://www.danielbkr.net/2018/05/17/appdaemon-motion-lights.html). 

The basic responsibilities of EC are as follows:

* (1) turn on **control entities** when **sensor entities** are triggered
* (2) turn off **control entities** when **sensor entities** remain off for some time
* (3) Do not interfere with manually controlled entities (tricky and not so obvious)
* (3.1) An entity that is already on should not be affected by time outs. (EC should ignore it and not start a timer,[Read more on my blog...](https://danielbkr.net/2018/03/20/motion-sensor-lights.html#problem-motion-lights-turn-off-manually-controlled-lights-after-time-out-period-expires))
* (3.2) An entity that is manually controlled within the time-out period should have its timer cancelled, and therefore stay on.

In the original context of motion lighting, this means:

* (1) turn on light when motion is detected
* (2) turn off light when no motion is detected for some time
* (3) Do not interfere with manually activated lights 
* (3.1) A light that is already on must not be controlled. (EC should ignore it and not start a timer)
* (3.2) A light that is dimmed (or color changed) within the time-out period should have its EC timer cancelled, and therefore stay on.

This FSM implementation is by far the most elegant solution I have found for this problem as the typical "if/else" algorythm got way out of hand and unmanagable.

![Entity Controller State Diagram](../images/state_diagram.png)