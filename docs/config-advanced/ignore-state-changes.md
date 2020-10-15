---
  title: Ignoring state updates from certain sources
---

# Ignoring state updates from certain sources

EC ignores state updates that are the result of its own service calls to control entities. This is done to avoid EC accidentally blocking itself and getting stuck there indefinitely.

There may come a time when you want to ignore state updates from a certain component, such as `adaptive_lighting`. Since the introduction of Home Assistant new `context` feature, we have much more information about `who` triggered a state change in Home Assistant state machine. EC utilizes this information and exposes the `ignored_event_sources` configuration key to allow you to add additional entries.

To find out what value to put here, open the logs in DEBUG mode and check the `Context ID` value. This is what you should add to the `ignored_event_sources` list. Note, wildcards (*) ARE supported in this field.

```yaml
motion_light:
  sensor: binary_sensor.living_room_motion
  entity: light.led                         # required
  ignored_event_sources:
    - adapt_lgt_.*
    - some_other_context_id
```

## Technical limitation

This feature requires other components to use Home Assistant's `context` API correctly. If they do not introduce themselves when making a service call (e.g. "Hi  I am adaptive lighting and please adjust the brightness on this light bulb") EC has no way to distinguish it from other components.

Since this is a fairly new change in Home Assistant's API you should expect wider adoption to take some time.
