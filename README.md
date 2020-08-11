# Higher Order Functions

A higher order function is a function that takes another function as an argument or returns a function. 

## Sequence and Collection Protocols 

A sequence is a list of values that you can step through one at a time. The most common way to iterate over the elements of a sequence is to use a for-in loop:

Collections are used extensively throughout the standard library. When you use arrays, dictionaries, and other collections, you benefit from the operations that the Collection protocol declares and implements. In addition to the operations that collections inherit from the Sequence protocol, you gain access to methods that depend on accessing an element at a specific position in a collection.

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

#### Writing the `map` funciton 

```swift
extension Sequence {
  func myMap<T>(closure: (Self.Element) -> (T)) -> [T] {
    var resuls = [T]()
    for value in self {
      let result = closure(value)
      resuls.append(result)
    }
    return resuls
  }
}

let values = [1, 2, 3, 4]

let transformedValues = values.myMap {  $0 * $0 }

print(transformedValues)
// [1, 4, 9, 16]
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

#### Writing the `reduce` function 

```swift 
let values = [1, 2, 3, 4]

// (initialResult, closure: (previousResult, currentResult) -> (result))
// (T, closure: (T, T) -> (T)) -> [T]

func myReduce(_ arr: [Int], initialResult: Int, _ closure: (Int, Int) -> (Int)) -> Int {
  var previousResult = initialResult
  for num in arr {
    let result = closure(previousResult, num)
    previousResult = result
  }
  return previousResult
}

let result = myReduce(values, initialResult: 0, +)
print(result) // 10
```


## `compactMap`

`compactMap` returns non-nil values from a given transformation. 

```swift
let values = ["true", "1", "0", "false", "false"]

let transformedValues = values.compactMap { Bool($0) }

print(transformedValues) // [true, false, false]
```

## `flatMap`

`flatMap` concatenates the elements of a given sequence 

#### Example 1

```swift 
let values = [1, 2, 3, 4]

let mappedValue = values.map { Array(repeating: $0, count: $0) }
print(mappedValue) // [[1], [2, 2], [3, 3, 3], [4, 4, 4, 4]]

// if we do not want an array of arrays like `map` gave us then we use `compactMap` as below
// `compactMap` will flatten the transformed results into one sequence by concatenated each result
let concatenatedValues = values.flatMap { Array(repeating: $0, count: $0) }
print(concatenatedValues) // [1, 2, 2, 3, 3, 3, 4, 4, 4, 4] 
```

#### Example 2 

```swift 
let values = [1, 2, 3, 4]

let mappedValues = values.map { int -> [Int] in
  return [int * int]
}
print(mappedValues) // [[1], [4], [9], [16]]

let flattenedValues = values.flatMap { int -> [Int] in
  return [int * int]
}
print(flattenedValues) // [1, 4, 9, 16]
```

Above instead of the final result of the transformation being an array of arrays, `flapMap` will concatenate the values of this operations and return a single sequence.
