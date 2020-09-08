# Higher Order Functions

A higher order function is a function that takes another function as an argument or returns a function. 

## A few of Swift built-in higher order functions 

* map 
* reduce 
* compactMap 
* filter
* sorted 
* flatMap
* compactMapValues

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

let combinedValues = values.reduce(initialValue) { (currentResult, currentValue) -> Int in
  return currentResult + currentValue
}

print(combinedValues) // 15

let shorthandReduce = values.reduce(0, +)

print(shorthandReduce) // 15

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

let booleanValues = values.compactMap { Bool($0) }

print(booleanValues) // [true, false, false]
```

## `filter`

`filter` takes a closure that operates as a predicate on the elements of a sequence and returns the results of the query. 

```swift 
let values = [1, 2, 3, 4]

let filteredResults = values.filter { $0 > 2 }

print(filteredResults) // [3, 4]
```


## `sorted`

`sorted` compares and sorts elemenents a sequence using a given predicate. 

```swift 
let values = [3, 1, 4, 2]

let sortedResults = values.sorted { (value1, value2) -> Bool in
  return value1 < value2
}

print(sortedResults) // [1, 2, 3, 4]

let shorthandSorted = values.sorted { $0 < $1 }

print(shorthandSorted) // [1, 2, 3, 4]
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
let cities =  Set([["London","New York"],["New York","Lima"],["Lima","Sao Paulo"]])
let flattenedCites = cities.flatMap { $0 }
print(flattenedCites) // ["Lima", "Sao Paulo", "New York", "Lima", "London", "New York"]
```

Above instead of the final result of the transformation being an array of arrays, `flapMap` will concatenate the values of this operations and return a single sequence.

## `compactMapValues`

`compactMapValues` is very similar to `compactMap` on an array. It returns non-nil `(key, value)` pairs from a given dictionary. 

```swift 
let gradesDict = ["michelle": "90", "paul": "eighty", "cindy": "96"]

let gradesMapValues = gradesDict.mapValues { Int($0) }
print(gradesMapValues) // ["paul": nil, "michelle": Optional(90), "cindy": Optional(96)]

let gradesCompactMapValues = gradesDict.compactMapValues { Int($0) }
print(gradesCompactMapValues) // ["cindy": 96, "michelle": 90]
```

## Challenges 

#### Challenge 1 

Write a function called `multiples(of:in)` that takes in an array of Ints and returns all of the Ints that are a multiple of a given number n. Use filter in your function.

_Sample Input: (3, [1, 2, 3, 4, 6, 8, 9, 3, 12, 11])_   
_Sample Output: [3, 6, 9, 3, 12]_  

<details>
  <summary>Solution</summary> 
  
```swift 
func multiples(of n: Int, in numbers: [Int]) -> [Int] {
  return numbers.filter { $0 % n == 0 }
}

multiples(of: 3, in:  [1, 2, 3, 4, 6, 8, 9, 3, 12, 11]) // [3, 6, 9, 3, 12]
```
  
</details>

</br> 

#### Challenge 2

Write a function called `largestValue(in:)` that finds the largest Int in an array of Ints. Use reduce to solve this exercise.

_Sample Input: [4, 7, 1, 9, 6, 5, 6, 9]_  
_Sample Output: 9_  

<details>
  <summary>Solution</summary> 
  
```swift 
func largestValue(in numbers: [Int]) -> Int {
  numbers.reduce(Int.min) { (currentResult, currentValue) -> Int in
    if currentValue > currentResult {
      return currentValue
    }
    return currentResult
  }
}

largestValue(in: [4, 7, 1, 9, 6, 5, 6, 9]) // 9
```
  
</details>

</br>

#### Challenge 3 

Write a function called `sortedNamesByLastName(in:)` that takes in an array of tuples of type (String, String) and returns an array of tuples sorted by last name.

```swift 
let firstAndLastTuples = [
    ("Johann S.", "Bach"),
    ("Claudio", "Monteverdi"),
    ("Duke", "Ellington"),
    ("W. A.", "Mozart"),
    ("Nicolai","Rimsky-Korsakov"),
    ("Scott","Joplin"),
    ("Josquin","Des Prez")
]
let expectedOutputFour = [
    ("Johann S.", "Bach"),
    ("Josquin","Des Prez"),
    ("Duke", "Ellington"),
    ("Scott","Joplin"),
    ("Claudio", "Monteverdi"),
    ("W. A.", "Mozart"),
    ("Nicolai","Rimsky-Korsakov")
]
```

<details>
  <summary>Solution</summary> 
  
```swift 
func sortedNamesByLastName(in names: [(firstName: String, lastName: String)]) -> [(firstName: String, lastName: String)] {
  return names.sorted { $0.lastName < $1.lastName }
}

let firstAndLastTuples = [
    ("Johann S.", "Bach"),
    ("Claudio", "Monteverdi"),
    ("Duke", "Ellington"),
    ("W. A.", "Mozart"),
    ("Nicolai","Rimsky-Korsakov"),
    ("Scott","Joplin"),
    ("Josquin","Des Prez")
]

print(sortedNamesByLastName(in: firstAndLastTuples))
/*
 [(firstName: "Johann S.", lastName: "Bach"),
 (firstName: "Josquin", lastName: "Des Prez"),
 (firstName: "Duke", lastName: "Ellington"),
 (firstName: "Scott", lastName: "Joplin"),
 (firstName: "Claudio", lastName: "Monteverdi"),
 (firstName: "W. A.", lastName: "Mozart"),
 (firstName: "Nicolai", lastName: "Rimsky-Korsakov")]
*/
```
  
</details>

</br>

#### Challenge 4 

Write a function called `sumOfSquaresOfOddNumbers(in:)` that returns the sum of the squares of all the odd numbers from an array of Ints.  Use filter, map and reduce in your function.

_Sample Input: [1, 2, 3, 4, 5, 6]_   
_Sample Output: 35_  

Explanation: 1 + 9 + 25 = 35

<details>
  <summary>Solution</summary>

```swift 
func sumOfSquaresOfOddNumbers(in numbers: [Int]) -> Int {
  return numbers.filter { $0 % 2 == 1 }
    .map { $0 * $0 }
    .reduce(0, +)
}

sumOfSquaresOfOddNumbers(in:  [1, 2, 3, 4, 5, 6]) // 35
```
  
</details>
