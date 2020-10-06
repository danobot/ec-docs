---
  title: Ignore State Attribute Changes
---
### Ignore State Attribute Changes

By default, any attribute change is considered significant and qualifies for entering the `blocked` state. However, in certain cases, you might want to ignore certain state changes caused by entity attributes.

For example, when using a component like `f.lux` or `circadianlighting`, the brightness and color temperature updates automatically, which triggers EC to believe there is a state change caused by something/someone else. This is not indicative of a manual change and EC should ignore it.

Another example is using [using custom service parameters](../config-advanced/custom-params.md) with the `transition` key supported by some services (most notably `light.turn_on`). After the service call the transition itself is handled on the device itself which would look like a manual control to Ec.

For these cases, add a `state_attributes_ignore` field to your EC instance with the attributes you want to ignore.

```yaml
mtn_office:
  sensor: binary_sensor.office_motion
  trigger_on_activate: light.office_led
  delay: 120
  state_attributes_ignore:
    - brightness
    - color_temp
```

The effect of this is that any state change triggered by an update to the `brightness` or `color_temp` attribute is discarded and no further processing in EC occurs.