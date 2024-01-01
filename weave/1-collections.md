# Collections
A collection is any enumerable set of data.

## For Loops
```rb
for item in collection do
    ...
end
```

To skip the current item in the loop use `next`.
```rb
temp numbers = [1, 2, 3, 4, 5]
for item in numbers do
    if item % 2 is 0 then
        next
    end
end
# This loop will skip all even numbers
```

To stop a loop early use `stop`
```rb
temp numbers = [1, 2, 3, 4, 5]
for item in numbers do
    if item is 3 then
        stop
    end
end
# This loop will stop when it reaches the third item
```

## Where
`where` is a filter that can be applied to a collection to get a subset of the collection. `it` is a special variable that refers to the current item in the collection.
```rb
    temp numbers = [1, 2, 3, 4, 5]
    temp even_numbers = numbers where it % 2 is 0
```

## Ordering
Using `<collection> ordered by <number selector> <direction>` will sort the collection by the given collection in the given direction. Once again `it` is a special variable that refers to the current item in the collection.
```rb
    temp numbers = [5, 3, 1, 4, 2]
    temp ordered_numbers = numbers ordered by it ascending
    # ordered_numbers is now [1, 2, 3, 4, 5]
```

## Skip / Take
`<collection> skip <number>` will return a new collection with the first `<number>` items removed.
```rb
    temp numbers = [1, 2, 3, 4, 5]
    temp last_three_numbers = skip 2 of numbers
    # last_three_numbers is now [3, 4, 5]
```

`<collection> take <number>` will return a new collection with only the first `<number>` items.
```rb
    temp numbers = [1, 2, 3, 4, 5]
    temp first_three_numbers = take 3 of numbers
    # first_three_numbers is now [1, 2, 3]
```

Combining `skip` and `take` can be used to get a subset of a collection.
```py
    temp numbers = [1, 2, 3, 4, 5]
    temp middle_three_numbers = skip 1 take 3 of numbers
    # middle_three_numbers is now [2, 3, 4]
```

## Ranges
You can define a range of values using `<start> to <end> <inclusive/exclusive>`. Start will always be inclusive and end will be inclusive or exclusive depending on the keyword used.
```rb
    temp numbers = 1 to 5 inclusive
    # numbers is now [1, 2, 3, 4, 5]
```

```rb
    temp numbers = 1 to 5 exclusive
    # numbers is now [1, 2, 3, 4]
```

## Extracting Individual Items
You can extract individual items from a collection using `index <number> of <collection>`. The first item in a collection is at index 0.
```rb
    temp numbers = [1, 2, 3, 4, 5]
    temp first_number = index 0 of numbers
    # first_number is now 1
```