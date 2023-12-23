# Selection Table
## Basic drop definition
The text in the brackets is the item id. For items outside of the Bestitched package, you will need quotes to allow for the colon.
```toml
[[coin]]

[["my_package:my_item"]]
```

## Defaults
```toml
drop_count = 1

[[...]]
weight = 1
always_drop = false
count = 1
stock = 1
cost = 0
groups = []
triggers = []
```

# Global fields
All of the possible fields relating to the selection table as a whole.

## Drop Count
This defines how many random pulls will be made from the selection table.

```toml
drop_count = 1
```
Drop Count can also be defined with [range syntax](#range-syntax) or [list syntax](#list-syntax).

# Drop Fields
All of the possible fields relating to a drop entry in the selection table.

## Weight
Assuming `always_drop` is false or not defined, this will act as the chance of this drop being selected.

```toml
# This has a 1 in 10 chance of being selected
[[bone]]
weight = 1

# this has a 9 in 10 chance of being selected
[[coin]]
weight = 9
```

## Always drop
If defined as `true`, this drop will always happen and will not consume a drop.

## Count
Defines the amount of this item that will be grabbed if this item is grabbed.
```toml
[[bone]]
count = 10 # Drops 10 bones
```
Count can also be defined with [range syntax](#range-syntax) or [list syntax](#list-syntax).

## Stock
This defines how many times this item can be randomly picked from the selection table.

At the start of a draw, all items (excluding those defining `always_drop` as true) are added to a "bag" `stock` number of times. 

>Importantly, this does not effect the chance of the item being drawn. You can have 10,000 bananas and 1 apple but both are equally likely to be drawn. 

Once an item has been drawn (either by the grabber, by groups, or by triggers) as many times as it's stock allows, it will never be drawn again (even if it's group is triggered).

```toml
[[bone]]
stock = 2 # This item can be grabbed 2 times at max
```
This field can not use any special syntax.

## Cost
With a default of 0, this field can be ignored in most cases. It is used as a way to "spend" a balance when selecting a table of things.
This is mostly used in the context of enemy wave spawning, but it can be used in other places too. For this example, we'll show it in the context of spawning enemies. Starting with a basic table file:
```toml
[[slime]]
cost = 1

[[slime_boss]]
cost = 20
```

Let's suppose you're spawning a wave of slimes. Passed into the `Draw` method will be a "balance" which will represent the difficulty of the wave to spawn. If that difficulty is over 20 then there will be a chance to spawn a `slime_boss`. For each grab, the cost of the grab is subtracted from the balance. This repeats until you either run out of `drops` or you run out of `balance`.


## Groups
When an item with groups is grabbed, all items that share a group are grabbed at the same time. This only consumes 1 grab.
```toml
[[bone]]
groups = [1]

[[coin]]
groups = [0]

[[soul]]
groups = [0, 1]
```

Importantly, groups do not trigger chain reactions. If `coin` was grabbed then it would also grab `soul`, but soul's groups are not then grabbed too, so `bone` is not grabbed.

## Triggers
A trigger is a one way group. It will cause anything in the specified group ids to be grabbed, but does not say anything about what group the item is in.

```toml
[[bone]]
triggers = [0]

[[coin]]
groups = [0]
```
If `bone` is grabbed then it triggers group `0` and grabs `coin`. If `coin` is grabbed, it also triggers group `0`, but since `bone` is not in that group it does nothing.

# Other stuff
## Range Syntax
Defienes an integer randomly chosen within the range `min..max`.
```toml
drops_count = "0..10" # Chooses a random number from 0 to 10 (inclusive).
```

## List Syntax
Defines an integer randomly chosen from a list `n1,n2,n3`
```toml
drops_count = "0,10" # Choses either 0 or 10
```

## Chance Object
To be used in place of Ranges or Lists, this alters the behaviour of integer functions and extends their capabilities. As it stands, there is only 1 possible extension.

Below is a basic use of a Chance Object:
```toml
drops_count = { value = "0..5", chance = 0.5 }
```

As it may be clear, this count will evaluate to a range between 0 and 5. However, unlike the Range Syntax, this range is weighted to give lower values more frequently than higher values. A chance below 1 will weigh towards the lower bound and a chance above 1 weighs towards the upper bound. A chance of exactly 1 means equal probability across all values. The bounds are never exceeded. 