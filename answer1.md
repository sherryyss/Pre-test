## Question 1

Write a function that takes two arrays as input, each array contains a list of A-Z; Your program should return True if the
2nd array is a subset of 1st array, or False if not.

For example:
* isSubset([A,B,C,D,E], [A,E,D]) = true
* isSubset([A,B,C,D,E], [A,D,Z]) = false
* isSubset([A,D,E], [A,A,D,E]) = true

Please explain the computational complexity of your answer in Big-O notation, i.e. O(log n) or O(n ^2)?		



### Answer:
```
const isSubset = (arrayA, arrayB) => {
    for (const itemOfArrayB of arrayB) {
      if (!arrayA.some(itemOfArrayA => itemOfArrayA === itemOfArrayB)) return false
    }
    return true
}
```

O(n^2), The worst case would be if the arrayB is the subset of the arrayA. In that case, we should go all over every item of the arrayA to check for every item of the arrayB, which takes a * b steps (a: length of the arrayA, b: length of the arrayB).
