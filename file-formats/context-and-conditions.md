# Context & Conditions
When writing [Selection Tables](selection-table.md) you may run into situation where you only want a drop to happen under specific circumstances. That's where the concept of `context` and `conditions` comes in. A context is basically a big list of values that can be accessed with keys.

We'll start with an example of where a conditon could be used:
```
[[cooked_porkchop]]
condition = 'Attributes INCLUDES "fire"'

[[porkchop]]
condition = 'Attributes EXCLUDES "fire"'
```
As could be inferred, the cooked variant of the item will drop only if the interaction added "fire" to the "Attributes". But what are Attributes, and what are these keywords `INCLUDES` and `EXCLUDES`? For the rest of this page there will be no surrounding toml and examples will be given as the string value of the condition. Just remember that a condition is a string literal (something wrapped in 'single quotes') that follows a field `condition = `.

## Context
Context is dependant on where the selection table is being drawn from. If the table is being used when an entity drops items on death then it will have a bunch of context values associated with entity death. All possible contexts will be outlined here. 

> Each context table promises that the keys listed will be there.

### Context Tables
#### Entity Death
| **Key**     | **Value Type** | **Description**                                                  |
| ----------- | -------------- | ---------------------------------------------------------------- |
| Attributes  | string[]       | Various keywords relating to the death.                          |
| DeathReason | DeathReason    | An series of flags describing the reason for the entities death. |

### Operators
| **Operator** | **Usage**                    | **Description**                                                                |
| ------------ | ---------------------------- | ------------------------------------------------------------------------------ |
| ==           | <any> == <any>               | Check if 2 values are the same.                                                |
| !=           | <any> != <any>               | Check if 2 values are not the same.                                            |
| AND          | <bool> AND <bool>            | Check if both the left and right side are true.                                |
| OR           | <bool> OR <bool>             | Check if either the left or the right side is true.                            |
| >            | <int, float> > <int, float>  | Check if the left side value is greater than the right side value.             |
| <            | <int, float> < <int, float>  | Check if the left side value is less than the right side value.                |
| >=           | <int, float> >= <int, float> | Check if the left side value is greater than or equal to the right side value. |
| <=           | <int, float> <= <int, float> | Check if the left side value is less than or equal to the right side value.    |
| INCLUDES     | <any[]> INCLUDES <any>       | Check if the left side array contains the right side value.                    |
| EXCLUDES     | <any[]> EXCLUDES <any>       | Check if the left side array does not contain the right side value.            |
| +            | <int, float> + <int, float>  | Add the left side value to the right side value.                               |
| -            | <int, float> - <int, float>  | Subtract the right side value from the left side value.                        |
| *            | <int, float> * <int, float>  | Multiply the left side value by the right side value.                          |
| /            | <int, float> / <int, float>  | Divide the left side value by the right side value.                            |
| %            | <int, float> % <int, float>  | Get the remainder of the left side value divided by the right side value.      |

### Types
#### DeathReason
A death reason is a series of flags that describe the reason for an entities death. The following flags are available:
| **Flag** | **Description**               |
| -------- | ----------------------------- |
| ByEntity | Caused directly by an entity. |
| ByTile   | Caused directly by a tile.    |
| ByPlayer | Caused directly by a player.  |