---
  title: Stay Mode
---

# Stay Mode
This simple option will make EC give up control of entities after the initial trigger. EC will stay in `active_stay_on` state indefinitely until the control entity is manually turned off.
```yaml
override_example:
  sensor: binary_sensor.lounge_motion
  entity: light.lounge_lamp
  delay: 5
  stay_mode: on
```
