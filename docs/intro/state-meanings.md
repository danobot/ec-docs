---
  title: Meaning of States
---
## State Meaning

|State|Description|
|---|---|
|idle|EC is observing states, nothing else.|
|active|Momentary, intermediate state. You won't see EC in this state much at all.|
|active_timer|Control entities have been switched on and timer is running|
|active_stay_on|Control entities have been switched on and will remain on until they are switched off manually.|
|overridden|Entity is overridden by an `override_entity`|
|blocked|When a control entity is already in `on` state and a sensor entity is triggered, EC will enter the `blocked` state. This is to ensure the controller does not interfere with other automations or manual control. The idea is, if the entity is already on, then the problem is already taken care of. EC will return to **idle** state once all `control_entites` return to `off` state.|
|constrained|Current time is outside of `start_time` and `end_time`. EC is inactive until `start_time`.|

Note that `control_entities == state_entities` unless you specifically define `state_entities` in your configuration.

