### Slice returns a new array - Splice returns a mutation

# Slice 
[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice]  
The slice() method returns a shallow copy of a portion of an array into a new array object.  

`arr.slice([begin[, end]])`
#### Params
  * **begin**
    * Zero-based index at which to begin extraction.
    * As a negative index, begin indicates an offset from the end of the sequence. slice(-2) extracts the last two elements in the sequence.
    * If begin is undefined, slice begins from index 0.

  * **end**
    * Zero-based index at which to end extraction. slice extracts up to but not including end.
    * slice(1,4) extracts the second element through the fourth element (elements indexed 1, 2, and 3).
    * As a negative index, end indicates an offset from the end of the sequence. slice(2,-1) extracts the third element through the second-to-last element in the sequence.
    * If end is omitted, slice extracts through the end of the sequence (arr.length).


# Splice 
[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice]  
The splice() method changes the content of an array by removing existing elements and/or adding new elements.  

`array.splice(start[, deleteCount[, item1[, item2[, ...]]]])`
#### Params  
  * **start** 
    * Index at which to start changing the array (with origin 0). If greater than the length of the array, actual starting index will be set to the length of the array. If negative, will begin that many elements from the end of the array.
  * **deleteCount**
    * An integer indicating the number of old array elements to remove. If deleteCount is 0, no elements are removed. In this case, you should specify at least one new element. If deleteCount is greater than the number of elements left in the array starting at start, then all of the elements through the end of the array will be deleted.
    * If deleteCount is omitted, deleteCount will be equal to (arr.length - start).
  * **item1, item2, ...**
    * The elements to add to the array, beginning at the start index. If you don't specify any elements, splice() will only remove elements from the array.
