# Lang Outline
This language is made with the goal of expressing ai behaviors in a way that is easy to read and write while also being flexible.

## Variables
### Temp
For declaring a temporary variable that will be lost beyond the current scope.
```
temp x = 1
```

### Save / Load
For declaring variables that can be saves to the current entities "memory" and loaded later.
```
temp x = 1
save x
...
load x
```

You can rename the loaded or saved variable with the `as` keyword.
```
save x as amazing_x
...
load amazing_x as x

```

You can also access memories of other entities using the `from` keyword.
```
load amazing_x from other_entity as x
```

> A handy shorthand for saving literals is to use the `as` keyword.
> ```
> save 1 as x
> ```

## Methods
Receiving a method from heaven?... Maaarc.
```
on my_method do
    ...
end
```

### Events
Receiving broadcasted events
```
receive some_broadcast with variable1, variable2 do
    ...
end
```

Broadcasting events
```
broadcast enemy_scouted_event with nearby_enemy
or ??
broadcast nearby_enemy as enemy_scouted_event
```

## Import / Export
An import is how we can access methods, variables, and litarals from other files.
```
import builtin/math/distance_between as distance
```

An export is how we can make our methods, variables, or literals available to other files to import.
```
export "Coffee" as docs_author
```

## Collections
A collection is any enumerable set of data.

### For Loops
```
for item in collection do
    ...
end
```

### Where
`where` is a filter that can be applied to a collection to get a subset of the collection. `it` is a special variable that refers to the current item in the collection.
```
    temp numbers = [1, 2, 3, 4, 5]
    temp even_numbers = numbers where it % 2 is 0
```

## Expressions
### If
An if expression evaluates a condition and executes the `then` part if the condition was true.
```
if x is 1 then
    say "x is 1"
end
```

You can replace the `end` with an `else` to execute a different block of code if the condition was false.
```
if x is 1 then
    say "x is 1"
else
    say "x is not 1"
end
```

You can also chain `else if` statements to check multiple conditions.
```
if x is 1 then
    say "x is 1"
else if x is 2 then
    say "x is 2"
else if x is 3 then
    say "x is 3"
else
    say "x is not 1 or 2"
end
```