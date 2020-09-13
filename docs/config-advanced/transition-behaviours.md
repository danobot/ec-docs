---
  title: Transition Behaviours
---




### Transition Behaviours (beta)
Transition Behaviours allow you to define what EC should do at these transition points.

**Use Case:**
> One use case for this is when lights turn on just before the end of the active period and then they never turn off because EC is constrained. For me, the light would be triggered by me walking into a room at 
7am and the constrain period would begin at 7:16am. Since the light duration is 20 minutes, EC will never turn off the light because it is in `constrained` state at 7:20am. This is annoying because the lights stay on all day. I can use `on_enter_constrained: "off"` to turn off all lights at 7:16am (when the EC is constrained).

```
transition_behaviours:   # light triggers on then off
    entities: 
      - input_boolean.lamp
    sensors:
      - sensor.motion_sensor
    overrides:
      - input_boolean.override_switch
    delay: 5
    behaviours:
      on_enter_constrained: "on"
    start_time: sunset
    end_time: "7:16:00"
```
**Notes about light flicker:** This can cause light flicker particularly for the `on_exit_*` behaviours. If your lights flicker, make sure you understand how this configuration is impacting them and use the `on_enter_*` behaviours instead.

 
#### Supported transition points:  
The following behaviours can be defined using the values `"on"`, `"off"` and the default being `"ignore"`. These must be in quotes to avoidconflicts with YAML truth values.


|Key|Description|
|---|---|
|on_enter_idle||
|on_exit_idle||
|on_enter_active||
|on_exit_active||
|on_enter_overridden||
|on_exit_overridden||
|on_enter_constrained||
|on_exit_constrained||
|on_enter_blocked||
|on_exit_blocked||

#### Supported transition behaviours:  
You must put these in quotes.

|Key|Description|
|---|---|
|"on"| Control entities will be explicitly turned on. |
|"off"| Control entities will be explicitly turned off. |
|"ignore"| (default) Nothing special will happen (control left to state machine) |

```yaml
  mtn_outside:
    sensor: 
      - binary_sensor.mtn_kitchen
    entities:
      - light.kitchen_led
    state_entities:
      - light.outside_light
    delay: 1200
    start_time: '18:00:00'
    end_time: '07:00:00'
    end_time_action: "off"                   # will turn off all control entities at 7am if they are on.
```