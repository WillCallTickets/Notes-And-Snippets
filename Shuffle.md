#Algo
1 Swap first and a random element  
2 Move to next item and swap with a random element  
3 Continue until n-2 (last is aleady swapped!)

# Another method
```
var list = [1,2,3];
console.log(list.sort(function() { Math.random() - 0.5 })); // [2,1,3]
```
