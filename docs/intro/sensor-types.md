
---
title: Understanding Sensor Types
---


# Understanding Sensor Types
## Support for different sensor types

There are two types of motion sensors:

  1. Sends a signal when motion happens (instantaneous event)
  2. Sends a signal when motion happens, stays on for the duration of motion and sends an `off` signal when motion supposedly ceases. (duration)

By default, EC assumes you have a Type 1 motion sensor (event based), these are more useful in home automation because they supply raw, unfiltered and unprocessed data. No assumptions are made about how the motion event data will be used. Since entties are stateful, the motion sensor entity in the demo below is on for only a brief period. EC only cares about the state change from `off` to `on`. In the future, there will be support for listening to HA events as well, which means the need to create 'dummy' `binary_sensors` for motion sensors is removed. Check out my [`processor` component](https://github.com/danobot/mqtt_payload_processor) for more info.



If your motion sensor emits both `on` and `off` signals, then add `sensor_type: duration` to your configuration. This can be useful for motion sensors, door sensors and locks (not an exhaustive list). By default, the controller treats sensors as `event` sensors.

Control entities are turned off when the following events occur (whichever happens last):
  * the timer expires and sensor is off
  * the sensor state changes to `off` and timer already expired

The following demo shows the behaviour in those two scenarios:



If you want the timer to be restarted one last time when the sensor returns to `off`, then add `sensor_resets_timer: True` to your entity configuration.

#### Sensor Type Demonstrations

Notation for state transition demonstrations: 

* `[ ]` indicate internal event, 
* `( )` indicates external influence (sensor state change), 
* `...` indicates passage of time,
* `->` Indicates flow

**Normal sensor**

> Idle -> Active Timer -> [timer started] ... [timer expires] -> Idle

![Event Demo](../images/event.gif)

**Duration Sensor**

> Idle -> Active Timer -> [timer started] ... **[timer expires] ... (sensor goes to off)** -> Idle

![Duration Demo](../images/duration.gif)

**With `sensor_resets_timer`**

> Idle -> Active Timer -> [timer started] ... [timer expires] ... (sensor goes to off) ... **[timer restarted] ... [timer expires]** -> Idle

![Duration Demo](../images/duration_sensor_resets_timer.gif)
