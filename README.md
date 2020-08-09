# Higher Order Functions

A higher order function is a function that takes another function as an argument or returns a function. 

## Swift built-in higher order functions 

* map 
* reduce 
* compactMap 
* filter
* sorted 

## `map`

`map` works on a colllections and performs a given transformation on each element and returns a new collection. 

```swift
let values = [1, 2, 3, 4, 5]

let transformedValues = values.map { return $0 % 2 == 0 } // (Int) -> [T]

print(transformedValues) // [false, true, false, true, false]
```
