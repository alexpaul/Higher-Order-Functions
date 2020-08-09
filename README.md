# Higher Order Functions

A higher order function is a function that takes another function as an argument or returns a function. 

## Swift built-in higher order functions 

* map 
* reduce 
* compactMap 
* filter
* sorted 
* flatMap

## `map`

`map` works on a colllections and performs a given transformation on each element and returns a new collection. 

```swift
let values = [1, 2, 3, 4, 5]

let transformedValues = values.map { return $0 % 2 == 0 } // (Int) -> [T]

print(transformedValues) // [false, true, false, true, false]
```

## `reduce`

`reduce` takes an initial value and a closure that combines the previous result and current value to return a combined value. 

```swift 
let values = [1, 2, 3, 4, 5]

let initialValue = 0

let transformedValues = values.reduce(initialValue) { prevResult, currentValue in
  print("\(prevResult), \(currentValue)")
  return prevResult + currentValue // running total
}

print(transformedValues)

/*
 0, 1
 1, 2
 3, 3
 6, 4
 10, 5
 15
*/
```


## `compactMap`

`compactMap` returns non-nil values from a given transformation. 

```swift
let values = ["true", "1", "0", "false", "false"]

let transformedValues = values.compactMap { Bool($0) }

print(transformedValues) // [true, false, false]
```
