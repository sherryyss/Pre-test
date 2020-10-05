### Answer 1:
```
const isSubset = (arrayA, arrayB) => {
    for (const itemOfArrayB of arrayB) {
      if (!arrayA.some(itemOfArrayA => itemOfArrayA === itemOfArrayB)) return false
    }
    return true
}
```

O(n^2), The worst case would be if the arrayB is the subset of the arrayA. In that case, we should go all over every item of the arrayA to check for every item of the arrayB, which takes a * b steps (a: length of the arrayA, b: length of the arrayB).
