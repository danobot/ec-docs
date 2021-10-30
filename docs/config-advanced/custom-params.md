---
  title: Custom Service Call Parameters
---   

# Specifying Custom Service Call Parameters
Any custom service defined in EC configuration will be passed to the `turn_on` and `turn_off` calls of the control entities. Simply add a `service_data` or `service_data_off` field to the root or `night_mode` to pass custom service parameters along. An example is shown in below.

```yaml
ec_chandelier_light:
  sensor: binary_sensor.kitchen_motion
  entity: light.chandelier
  delay: 600
  service_data:
    brightness_pct: 50
  service_data_on: 
    transition: 2
  service_data_off: 
    transition: 120
```      

Note that all control entities must support the defined service data parameters. Some entities may reject unknown parameters and throw an error! In that case you may add those entities as activation/deactivation triggers instead.

When using activation/deactivation triggers it is possible to pass parameters to the Home Assistant script by using the a 'variables' object in the `service_data` or `service_data_off` object for example

```yaml
office_light:
  friendly_name: Office Light Motion Controller
  sensor:
    - group.office_motion
  state_entity:
    - group.office_lights
  trigger_on_activate: script.room_lights_motion
  trigger_on_deactivate: script.room_lights_off
  service_data:
    variables:
      room: "office"
  service_data_off:
    variables:
      room: "office"
  delay: 180
  backoff: true
  backoff_factor: 1.6
  backoff_max: 1800
  overrides:
    - group.office_switch
    - binary_sensor.office_has_light
 ```
