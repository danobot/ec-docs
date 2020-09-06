---
  title: Entity Types used in EC
---
# Entity Types used in EC
A component like EC unfortunately requires some domain specific language (jargon) to explain its functionality and enable people to adapt it for their use cases. There are four different types of entities used in EC. 

|Configuration|Description|
|---|---|
|control entities| The entities you wish to switch on and off depending on some trigger. EC will control these entities by turning them on or off.|
|[sensor entities](sensor-types.md)| Used as triggers. When these entities turn on, your _control entities_ will be switched on.|
|[state entities](state-entities.md)|Unless you wish to use non-stateful entities, you need not worry about state entities. Essentially, they allow you to define specific entities that will be used for state observation *in cases where control entities do not supply a usable state*. (As is the case with `scene`.) Optional.|
|[override entities](../config-basic/override-entities.md)| The entities used to override the entire EC logic. Optional.|

**Note:** Any entity in EC is just a normal Home Assistant entity.