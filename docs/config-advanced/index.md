---
  title: Advanced Configuration
---

## Advanced Configuration
The following is an example configuration used to control my outside light at night. The override is used to manually enable or disable this EC instance. Note that EC will call the `turn_on` service on its control entties, meaning you can use it to trigger different types of entities at the same time. My `buzz_short` script emits a short notification tone from a buzzer speaker attached to a Raspberry Pi GPIO pin. (See related [blog post](https://blog.danielbkr.net/2018/07/24/python-docker-mqtt-audio-buzzer.html) and [MQTT Audio Buzzer Repository](https://github.com/danobot/mqtt-audio-buzzer-rpi)).

```yaml
mtn_outside:
  sensor: 
    - binary_sensor.backyard_motion
    - binary_sensor.shed_door
    - binary_sensor.kitchen_door
    - binary_sensor.mtn_outside_2
  entities:
    - light.outside_light
    - script.buzz_short
  override: 
    - input_boolean.outside_motion
  state_entities:
    - light.outside_light
  delay: 120
  backoff: true
  start_time: 'sunset - 01:00:00'
  end_time: 'sunrise + 01:00:00'
```
