# Aircraft Configuration

## File Format

The first line of the file is a header, describing each column name. After that, one row per type certificate ID. If a column does
not have data defined, it is left empty. All values are in metric units - metres and kilograms. The columns are, in order:

|Column name| Data type| Description|
|----|----|----|
|"Type certificate"| string | The type certificate ID this data represents|
|"flaps"| boolean | true if the aircraft has flaps |
|"trim"| boolean | true if the aircraft has movable trim tabs. Fix trim tabs, like on the Jantar Std 2 tailplane are false here |
|"ruddervator"| boolean | true if the aircraft has a V-tail style combined flaps and rudders, like a Salto |
|"fixed uc"| boolean | true if the aircraft has fixed undercarriage for the main wheel |
|"uc type"| Enum | The undercarriage configuration. Will be one of "inline", "trike_nosewheel" or "trike_taildragger"|
|"seat type"| How the seat(s) are arranged for the pilot and passengers. Will be one of "single", "tandem" or "side_by_side"|
|"fuselage max ballast"| number | If the fuselage can carry a ballast tank, max capacity of that tank|
|"wings max ballast"| number | If the wings can carry water ballast, the max capacity of ballast that can be carried |
|"tail ballast type"| Enum | If the tail has the ability to carry ballast to adjust CG, this defines the type. Note that this is for pure CG adjustment. If the tail tank is only to be used to balance the wing ballast, see the "tail wing compensation max ballast" column. Not some aircraft can have both types (eg DG1000). Will be one of "none", "water", "blocks". An aircraft may have a tail tank that can do dual duty for CG management independent of the wings (eg LS6C). In that case, this will be set to the appropriate type, a capacity given, and the wing compensation amount left blank|
|"tail ballast capacity"| number or formatted string | If tail ballast type is not "none" this defines the max capacity. Aircraft can have either water or blocks here, so depending on the value of the previous column, this will be defined either as a number (kg water), or a formatted string for how many blocks. See later description on how to parse the string|
|"tail wing compensation max ballast"| number | If there is a ballast tank that can only be used to adjust for the wing ballast tanks, this contains the max amount of water that can be used|
|"winspan primary"| number| The wingspan of the glider. If there are multiple options (eg 15 and 18m) this will be the lesser of the two spans|
|"wingspan alternate"| number | If the glider has two wingspan options, this will be the longer of the two|
|"wing panel count"| number|How many parts the wings can be disassembled into. Will be a number between 1 and 6|
|"winglets"| boolean | true if the wings have the option of installing winglets |
|"cockpit ballast count"| number| If there is the ability to have cockpit ballast blocks for light pilots, this is the max number of blocks|
|"cockpit ballast block weight"| number | If there is the ability to have cockpit ballast blocks, this is the individual weight per block. Assumes uniform block size|

When there is blocks defined for the tail CG compensation, the column is a formatted string. The format is a colon ':' separated set of
values, that appear in groups of three. Each group represents a single block configuration. The group consists of:

| Sub column| Data type | Description |
|----|----|----|
| label | string| A short label to identify this (typically something usable in a placard)|
| weight | number | The weight per block |
| count | number | The maximum number of these blocks that can be installed |

Note that some aircraft, like the DG1000 can have multiple block types installed. This column may contain multiple of these definitions
in different blocks. Using the DG1000, which can have 4 large blocks and 2 small blocks installed, you would see the following definition
in the column

```large:2.4:4:small:1.2:2```

This is 4 large blocks that weight 2.4Kg each, with a display label of "large", and 2 small blocks at 1.2kg each with a label of "small"
