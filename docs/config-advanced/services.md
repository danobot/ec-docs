---
  title: Automation Support and Services
---
# Automation Support and Services

## Entity Services

The entity controller support a few services that can be used to extend the customization of the entity.

### Stay Mode

```yaml
service: entity_controller.enable_stay_mode
  entity_id: entity_controller.motion
```

This service takes an entity id and will enable stay mode which means that control entities will not be turned off once EC is triggered. All control entities must be manually turned off (or via other automations) before EC will return to `idle` state.

```yaml
service: entity_controller.disable_stay_mode
  entity_id: entity_controller.motion
```

This service takes an entity id and will disable stay mode. This does not transition EC to `idle` state if it is already in `active_stay_on` state. In this case you must turn off all entities manually.

**Note:** There is no attribute that exposes the stay flag state at this time.

### Clearing Blocking State

```yaml
service: entity_controller.clear_block
  entity_id: entity_controller.motion
```

This service will clear the blocking state, if it is set, the same as if the block timer was run down.
This allows for automations to react to the entity being blocked by a light on and clear the state is needed.

**Example**
```yaml
automations:
- id: example
  trigger:
  - platform: state
      entity_id: entity_controller.motion
      to: blocking
      for: 00:01:00
  action:
  - service: entity_controller.clear_block
    entity_id: entity_controller.motion
```
**Note:** The above example is functionally equivalent to setting a block timeout in the configuration.

### Set Night Mode

```yaml
service: entity_controller.set_night_mode
  entity_id: entity_controller.motion
  data:
    start_time: now
    end_time: constraint
```

This service is for customizing the night mode settings for more dynamic scripts. It will set the night mode start 
and stop times to the times specified. If only one or both times are provided, only those times are changed. If 
no time is provided night mode is effectivly disabled by setting both the start and end to midnight. This service takes
the same time rules as the configuration, plus supports two additional options that make sense with automations.

```yaml
start_time: now
```

This will set the start (or end) night mode time to the current time. This is usefull for turning night mode on or off instantly.

```yaml
end_time: constraint
```

This will set the end (or start) night mode time to the appropriate constraint time (start or end.) This is handy for starting or making
night mode last the same as the configured constraints. **Note:** This has no meaning if constraints are not set, so it would be equivilent to not providing a value.