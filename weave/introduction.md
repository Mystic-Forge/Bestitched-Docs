# Lang Outline
This language is made with the goal of expressing ai behaviors in a way that is easy to read and write while also being flexible.

## Comments
Comments are used to add notes to your code that will be ignored by the compiler.

The syntax is undecided. Here are the current proposals:
```
# Single line comment

#-
Multi line comment
Wow!
-#
```

## Variables
### Temp
For declaring a temporary variable that will be lost beyond the current scope.
```rb
temp x = 1
```

## Accessors
### Of
For accessing a property of an object.
```lua
temp position = position of self
```

You can chain `of` to access nested properties.
```lua
temp x = x of position of self
```

### Save / Load
For declaring variables that can be saves to the current entities "memory" and loaded later.
```rb
temp x = 1
save x
...
load x
```

You can rename the loaded or saved variable with the `as` keyword.
```rb
save x as amazing_x
...
load amazing_x as x

```

You can also access memories of other entities using the `from` keyword.
```rb
load amazing_x from other_entity as x
```

> A handy shorthand for saving literals is to use the `as` keyword.
> ```rb
> save 1 as x
> ```

## Methods
Receiving a method from heaven?... Maaarc.
```rb
on my_method do
    ...
end
```

### Events
Broadcasting messages
```rb
broadcast enemy_scouted_event with nearby_enemy
```

Receiving broadcasted messages
```rb
receive some_broadcast with variable1, variable2 do
    ...
end
```

## Import / Export
An import is how we can access methods, variables, and litarals from other files.
```py
import builtin/math/distance_between as distance
```

An export is how we can make our methods, variables, or literals available to other files to import.
```ts
export "Coffee" as docs_author
```

## Expressions
### If
An if expression evaluates a condition and executes the `then` part if the condition was true.
```rb
if x is 1 then
    print "x is 1"
end
```

You can replace the `end` with an `else` to execute a different block of code if the condition was false.
```rb
if x is 1 then
    print "x is 1"
else
    print "x is not 1"
end
```

You can also chain `else if` statements to check multiple conditions.
```rb
if x is 1 then
    print "x is 1"
else if x is 2 then
    print "x is 2"
else if x is 3 then
    print "x is 3"
else
    print "x is not 1 or 2"
end
```

## Operators 
### Arithmetic
| Operator | Usage   | Description                              |
| -------- | ------- | ---------------------------------------- |
| `+`      | `x + y` | Adds `x` and `y`                         |
| `-`      | `x - y` | Subtracts `y` from `x`                   |
| `*`      | `x * y` | Multiplies `x` and `y`                   |
| `/`      | `x / y` | Divides `x` by `y`                       |
| `%`      | `x % y` | Gets the remainder of `x` divided by `y` |

### Comparison
| Operator | Usage        | Description                                                                 |
| -------- | ------------ | --------------------------------------------------------------------------- |
| `not`    | `not x`      | Returns `true` if `x` is `false` and `false` otherwise                      |
| `is`     | `x is y`     | Returns `true` if `x` is equal to `y` and `false` otherwise                 |
| `is not` | `x is not y` | Returns `true` if `x` is not equal to `y` and `false` otherwise             |
| `and`    | `x and y`    | Returns `true` if `x` and `y` are both `true` and `false` otherwise         |
| `or`     | `x or y`     | Returns `true` if `x` or `y` are `true` and `false` otherwise               |
| `>`      | `x > y`      | Returns `true` if `x` is greater than `y` and `false` otherwise             |
| `<`      | `x < y`      | Returns `true` if `x` is less than `y` and `false` otherwise                |
| `>=`     | `x >= y`     | Returns `true` if `x` is greater than or equal to `y` and `false` otherwise |
| `<=`     | `x <= y`     | Returns `true` if `x` is less than or equal to `y` and `false` otherwise    |