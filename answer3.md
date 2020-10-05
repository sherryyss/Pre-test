### Answer 3:

The reason is that the closures of all these three functions are sharing the same lexical environment. The quickest way to solve this problem is to use const ```let``` instead of ```var```, which makes each closure pointing to the block scope variable ```i```.


```Javascript
function createArrayOfFunctions(y) {
    var arr = [];
    for(let i = 0; i < y; i++) {
        arr[i] = function(x) { 
        return x + i; 
        }
    }
    return arr;
}
```

or use an IIFE for each loop, to caches each ```i``` variable for each loop in an IIFE, which keeps it in scope.

```Javascript
function createArrayOfFunctions(y) {
    var arr = [];
    for (var i = 0; i < y; i++) {
        (function() {
            var _i = i;
            arr[_i] = function(x) {
            return x + _i;
            };
        })();
    }
    return arr;
}
```
