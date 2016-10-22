# memoize

[https://www.youtube.com/watch?v=I7IdS-PbEgI&feature=youtu.be]  
*watch the video to see explanation of code!!!*

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
