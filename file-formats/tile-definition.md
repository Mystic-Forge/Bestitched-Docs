# Tile Definition
A tile definition is a toml file that defines a tile. The name of the toml file is the Id of the tile. 

## Basic tile definition
```
type = 'basic'

[fields]
material = 'stone'
```
The above file describes a `basic` tile with the material `stone`. The `type` field is used to determine which script to use. The `fields` table is where all the type specific fields are defined. In this example, the `basic` type has a single field `material`.

## Tile Types
Below is a list of all the tile types and their fields.

Shared fields:
| **Field** | **Type** | **Description**                |
| --------- | -------- | ------------------------------ |
| multi_tile_offsets  | int[3][]       | The offsets for the segments of a multi-tile. E.g: `[[0, 1, 0], [0, 2, 0]]` |

### Basic
id: `basic`

A basic tile is a simple voxel tile. You cannot change its mesh, but you can change the material that it uses.
| **Field** | **Type** | **Description**                |
| --------- | -------- | ------------------------------ |
| material  | Id       | The Id of the material to use. |

### Cardinal
id: `cardinal`

A cardinal tile takes a single mesh and provides 4 states, one for each cardinal direction.
| **Field** | **Type** | **Description**                |
| --------- | -------- | ------------------------------ |
| material  | Id       | The Id of the material to use. |
| mesh      | Id       | The Id of the mesh to use.     |

### Breakable Decoration
id: `breakable_decoration`

A breakable decoration is like a cardinal tile in that it can be rotated, but it also has a health state.

| **Field**           | **Type**   | **Description**                                                                                                                                                            |
| ------------------- | ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| material            | Id         | The Id of the material to use.                                                                                                                                             |
| damage_state_meshes | Id[health] | An array of Ids with the length equal to how much health the tile has. Each index directly corresponds to a health state. Index 0 is health 1, index 1 is health 2, etc... |
| max_health          | int        | The amount of damage this tile can sustain.                                                                                                                                |
| loot_table          | Id         | The Id of the loot table to use when the tile is destroyed.                                                                                                                |

## Field Types
