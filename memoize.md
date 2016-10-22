# memoize

[https://www.youtube.com/watch?v=I7IdS-PbEgI&feature=youtu.be]  

```
function memoize(fn) {
  var prevArg;
  var prevResult;
  return function(arg){
    return arg === prevArg ?
      prevResult : 
      (prevArg = arg, 
       prevResult = fn.call(this.arg);
  }
}
```
