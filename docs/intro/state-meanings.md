---
  title: Meaning of States
---

## State Meaning
Entity Controller is a finite state machine. This means it will be in one of many states at any point in time. The states represent what is going on with EC. 



|State|Description|
|---|---|
|idle|EC is waiting for stuff to happen, nothing else.|
|active|Momentary, internal state. You won't see EC in this state much at all.|
|active_timer|Control entities have been switched on and timer is running|
|active_stay_on|Control entities have been switched on and will remain on until they are switched off manually. This is used by [stay mode](../config-basic/stay-mode.md) if you added it to your configuration.|
|overridden|Entity is overridden by an [`override_entity`](../config-basic/override-entities.md)|
|blocked|When a control entity is already in `on` state and a sensor entity is triggered, EC will enter the `blocked` state. This is to ensure the controller does not interfere with other automations or manual control. The idea is, if the entity is already on, then the problem is already taken care of. EC will return to **idle** state once all `control_entites` return to `off` state.|
|constrained|Current time is outside of the [constrain time](../config-basic/time-constraints.md). EC is inactive until `start_time`.|


Note that `control_entities == state_entities` unless you specifically define `state_entities` in your configuration. [Read more about State Entities](state-entities.md)

