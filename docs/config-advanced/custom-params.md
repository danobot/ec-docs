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