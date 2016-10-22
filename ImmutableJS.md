# Immutable JS

[https://www.youtube.com/watch?v=I7IdS-PbEgI&feature=youtu.be]  
*watch the video to see code explanations!!!*

```
List.prototype.push = function(value){
  // 1) make a copy
  var clone = deepCopy(this);
  // 2) edit the copy
  clone[clone.length] = value;
  // 3) return the copy
  //return clone;
}


// this is dumbed down a bit - only does prev arg
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

#### Mori Library 
  * [http://swannodette.github.io/mori/]
  * optimized immutable data structures
 
### Structural sharing  
   - Constant time overhead in time
   -  Log(n) overhead in memory
   
### Directed Acyclic Graph - DAG  
 - children cannot point back to parents
 - create copies of parents for new structure
 - most of the previous structure is still the same  
 
### Version of a DAG called a TRIE that we can use to model list of values and key/value pairs
  * Index Trie - each node is an array of a fixed size - the values are in the leaves
  * Depth First Traversal gets values in correct order _fast!_
  * Only ever need 8 hops
  * Make copies of only things that changed and make references to what did not change
 
### Hash Trie
  * Still have nodes that are arrays of fixed size
  * But some nodes are leafs that hold key/values
  * DFS iteration - do not expect a fixed order - _performant_
 
 
### *SO* Implementations are Tries and Interfaces are Lists and Maps  
 
```
import { Map } from 'immutable';
var first = Map({ key: 'value' });

var second = first.set('key', 'foo');
second === first; // false

var third = first.set('key', 'value');
third === first; // true

```

### Flux stores contain mutable data
  - see code at 27 minutes
  - PureRenderMixin
  
### Flux with UNDO
  - create a history array
  - save pre-edit values into history
  - undo action pops the value  
  
 
 
 
 
 
 
