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

## `filter`

`filter` takes a closure that operates as a predicate on the elements of a sequence and returns the results of the query. 

```swift 
let values = [1, 2, 3, 4]

let results = values.filter { $0 > 3 }

print(results) // [4]
```


## `sorted`

`sorted` compares and sorts elemenents a sequence using a given predicate. 

```swift 
let values = [3, 1, 4, 2]

let sortedResults = values.sorted { (value1, value2) -> Bool in
  return value1 < value2
}

print(sortedResults) // [1, 2, 3, 4]
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

## CompactMapValues

```swift 
let gradesDict = ["michelle": "90", "paul": "eighty", "cindy": "96"]
let gradesMapValues = gradesDict.mapValues { Int($0) }
let gradesCompactMapValues = gradesDict.compactMapValues { Int($0) }

print(gradesMapValues) // ["paul": nil, "michelle": Optional(90), "cindy": Optional(96)]
print(gradesCompactMapValues) // ["cindy": 96, "michelle": 90]
```
