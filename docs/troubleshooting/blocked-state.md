---
  title: EC goes into blocked state
---

# EC goes into blocked state
Check how long it takes your control entities to actually turn on after the service call is dispatched. The default `grace_period` is 2 seconds.
This means EC will make the call to turn on all entities and then it will ignore any state updates that come in for 2 seconds (default). The reason for this is that without this grace period, EC would actually block itself because it would interpret the state updates as manual control.

Unfortunately, it is not possible to detect *who* called a service in Home Assistant. If that was the case we could simply ignore any service calls originating from EC itself.

To solve your issue with EC ending up in `blocked` state, you can take a look at increasing the `grace_period` to something like 5 seconds. If your lights have a lot of latency then increasing this period will most likely resolve your issue.

```yaml
grace_period_ec:
  sensor: binary_sensor.living_room_motion
  entity: light.tv_backlight
  grace_period: 5                           # default is 2
```