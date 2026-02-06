# Datum

Datum data is measurement information critical for calculating weight and balance. The data consists of both distance (arm)
measurements, and weight limits. A typical weight and balance calculator will use these, along with other data available in
the aircraft configuration to generate cockpit placards (eg ballast blocks to min pilot weight).

## Limitations and Assumptions

Details vary greatly between each aircraft model and manufacturer. Also, some items that can have arm and weight 
limits are not something that can change regularly, so that data isn't captured here. For example, often there is
a forward located battery under the pilot's legs. Since that will always be installed in the glider and part of
the empty weight, it won't have an impact on weight and balance calculations, and particularly the pilot loading
charts. Therefore we choose to ignore them.

Within a model line of aircraft, individual builds will have different configurations. For example, the inclusion
of tail tanks for compensating the wing ballast tanks were often optional. This file attempts to capture all the 
data known about a particular model, regardless of individual builds. It is up to the W&B calculation user to
select the right bits of data to use.

Wing ballast tank arms are quite complex coming into the most modern forms of glider that have long swept back
wings. Some types, like the JS3 and Ventus3 give multiple arms for the ballast tanks, or a formula based on 
the amount of water in the tanks. Despite the accuracy, they have very little difference in the final max and
min pilot weights - typically only 1-2 Kg (ie 1-2%). Additionally, these modern gliders have tail tanks that 
are used to compensate for the CG movement of the water in the wings, so it has zero impact on the max pilot 
weight that can be used. Rather than go for full accuracy, we only record a single figure within the data, and
typically that will be the shortest arm. 

## Units

All units are metric and the typical values used for weight and balance calculations - millimetres for distance and 
kilograms for weight.

## File Description

The file format is standard CSV. String, will be quoted only if needed to escape a comma character.

|Column name| Data type| Description|
|----|----|----|
|Type certificate| string | The type certificate ID this data represents|
|category| enum | Enumeration of one of the CS22 categories |
|wingspan| number | The wingspan size for this specific datum. Often limits will change based on wingspan, so this can be used as a secondary key |
|variation| string | If there is further differentiation needed, this is a plain text string describing the variation. For example the change in Mauw can change based on application of technical notes from the manufacturer |
|location| string | Location of the datum. By convenience since the far majority of aircraft use the same refernce - WRLE means Wing Root Leading Edge |
|levelling instructions| string | How to level the aircraft before weighing on the scales|
|model| enum | Enumeration of the type of calculation model to use |
|mauw| number | Maximum all up weight |
|mdry| number | Maximum dry weight (ie without ballast, fuel etc). Often this is not specified in official documentation, so will be set to the same value as Mauw |
|mnlp| number | Maximum Non-Lifting Parts weight|
|max seat| number | Max permitted seat weight. Does not include other cockpit weights like baggage |
|min seat| number | Minimum permitted seat weight, excluding the use of cockpit ballast weights |
|fwd cg| number | Foward CG location |
|aft cg| number | Aft CG location|
|p1arm| number | Arm for Pilot 1|
|p1arm max| number | If a range is specified for the P1 arm, this is the value that is furthest from the datum |
|p2arm| number | Arm for Pilot 2. Only used in 2 seaters |
|cockpit ballast arm| number | Arm to the cockpit ballast location |
|tail ballast arm| number | Arm to the primary ballast in the tail for compensating for CG adjustment. |
|tail battery arm| number | Arm to the (often optional) battery located in the tail |
|wing ballast arm| number | Arm to the ballast tanks in the wing |
|baggage arm| number | Arm to the primary baggage compartment |
|wing fuel arm| number | Arm to fuel tanks located in the wings |
|fuselage fuel arm| number | Arm to the fuel tank located in the fuselage |
|p1 instrument arm| number | Arm to the instrument panel for Pilot 1|
|wheel to datum| number | Distance from the datum to the primary wheel - typically distance "a" in W&B diagrams |
|wheel to tailwheel| number | Distance from the primary wheel to the tail wheel/skid location - typically distance "b" in W&B diagrams |

### Category Enum

Represents the category under JAR22/CS22 that the aircraft operates as. If the aircraft could operated under
2 categories, but with different limitations,  then there will be 2 line items for data. 

The available types are:
* Utility
* Aerobatic
* Special  (any specialised category, such as non-aerobatic version )

### Model Enum

The weight and balance calculation model to use (ie to understand what the distances above in the table represents.)

|model_1| Traditional tail-dragger configuration with the main wheel just in front of the CG (but behind the datum) and tail wheel/skid on the ground |
|model_1a| Taildragger configuration with the main wheel in front of the datum. Not often found in gliders |
|model_2| Aircraft that primarily sit forward on the nose, with the tail in the air. Main wheel is behind CG and datum |
|model_3| Wheels are not considered in the weighing. Typically used if a forward skid touches the ground before the aircraft reachs the required levelling |
