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

## Collections
A collection is any enumerable set of data.

### For Loops
```rb
for item in collection do
    ...
end
```

### Where
`where` is a filter that can be applied to a collection to get a subset of the collection. `it` is a special variable that refers to the current item in the collection.
```rb
    temp numbers = [1, 2, 3, 4, 5]
    temp even_numbers = numbers where it % 2 is 0
```

### Ordering
Using `<collection> ordered by <number selector> <direction>` will sort the collection by the given collection in the given direction. Once again `it` is a special variable that refers to the current item in the collection.
```rb
    temp numbers = [5, 3, 1, 4, 2]
    temp ordered_numbers = numbers ordered by it ascending
    # ordered_numbers is now [1, 2, 3, 4, 5]
```

### Skip / Take
`<collection> skip <number>` will return a new collection with the first `<number>` items removed.
```rb
    temp numbers = [1, 2, 3, 4, 5]
    temp last_three_numbers = numbers skip 2
    # last_three_numbers is now [3, 4, 5]
```

`<collection> take <number>` will return a new collection with only the first `<number>` items.
```rb
    temp numbers = [1, 2, 3, 4, 5]
    temp first_three_numbers = numbers take 3
    # first_three_numbers is now [1, 2, 3]
```

Combining `skip` and `take` can be used to get a subset of a collection.
```py
    temp numbers = [1, 2, 3, 4, 5]
    temp middle_three_numbers = numbers skip 1 take 3
    # middle_three_numbers is now [2, 3, 4]
```

### Ranges
You can define a range of values using `<start> to <end> <inclusive/exclusive>`. Start will always be inclusive and end will be inclusive or exclusive depending on the keyword used.
```rb
    temp numbers = 1 to 5 inclusive
    # numbers is now [1, 2, 3, 4, 5]
```

```rb
    temp numbers = 1 to 5 exclusive
    # numbers is now [1, 2, 3, 4]
```

### Extracting Values
Similar to property access, you can use `of` to extract a value from a collection.

Providing a number will return the item at that index in the collection.
```rb
    temp numbers = [1, 2, 3, 4, 5]
    temp first_number = 0 of numbers
    # first_number is now 1
```

You can get a subset of the collection using a range.
```rb
    temp numbers = [1, 2, 3, 4, 5]
    temp first_three_numbers = 0 to 2 of numbers
    # first_three_numbers is now [1, 2, 3]
```



You 

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
| Operator | Usage        | Description                                                         |
| -------- | ------------ | ------------------------------------------------------------------- |
| `not`    | `not x`      | Returns `true` if `x` is `false` and `false` otherwise              |
| `is`     | `x is y`     | Returns `true` if `x` is equal to `y` and `false` otherwise         |
| `is not` | `x is not y` | Returns `true` if `x` is not equal to `y` and `false` otherwise     |
| `and`    | `x and y`    | Returns `true` if `x` and `y` are both `true` and `false` otherwise |
| `or`     | `x or y`     | Returns `true` if `x` or `y` are `true` and `false` otherwise       |
| `>`      | `x > y`      | Returns `true` if `x` is greater than `y` and `false` otherwise     |
| `<`      | `x < y`      | Returns `true` if `x` is less than `y` and `false` otherwise        |
| `>=`     | `x >= y`     | Returns `true` if `x` is greater than or equal to `y` and `false` otherwise |
| `<=`     | `x <= y`     | Returns `true` if `x` is less than or equal to `y` and `false` otherwise |