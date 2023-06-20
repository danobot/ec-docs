---
title: Disable Block Mode
---

# Disable Block Mode
You can set `disable_block` to `True` to disable the `block` state. If your entity is already on and a sensor changes to on, then EC will
transition to the `active_timer` state (or restart the timer if it is already running.)

```yaml
disable_blocked_mode_demo:
  sensor: binary_sensor.living_room_motion
  entity: light.lounge_lamp
  disable_block: True
```

If you have a entity that you *always* want to turn off after a timer (even if you turn it on manually using a switch), then you can put the entity ID in the `sensors` section:

```yaml
always_use_timer_demo:
  sensors:
    - binary_sensor.living_room_motion
    - light.lounge_lamp
  entity: light.lounge_lamp
  disable_block: True
```

**Note:** EC is designed to avoid any interference with external automations that might affect control entities. Using `disable_block` directly violates this principle. If you see unintended interference, reconsider your configuration and remove the `disable_block` option if necessary.
