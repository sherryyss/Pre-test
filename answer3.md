### Answer 3:

The reason is that the closures of all these three functions are sharing the same lexical environment.The quickest way to solve this problem is to use const / let instead of var, which makes each closure pointing to the block scope variable, i.


```
function createArrayOfFunctions(y) {
    var arr = [];
    for(let i = 0; i<y; i++) {
        arr[i] = function(x) { return x + i; }
    }
    return arr;
}
```
