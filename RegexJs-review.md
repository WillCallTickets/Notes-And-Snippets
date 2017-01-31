# A review of regex methods in JS

## 2 methods

### 1) Literal notation
does not use quotation marks - slashes  
use when the regex will remain constant

### 2) Constructor function
use when you know the regex expression will be changing  
or when the pattern will be dynamic aka via an input field


### Some common symbols
Symbol | Description | Example
--- | --- | ---
*|zero or more | {0,}
+|one or more | {1,}
?|zero or one | {0,1}
.|match any char but newline
(x)| match and remember
(?:x)|match - don't remember
{n}|match n occurrences
{n,m}|match at least n and at most m
\b | word boundary|
\B | non-word boundary|
\d|digit
\D|non-digit
\s|single white space
\S|anything but white space
\w|alphanumeric|[A-Za-z0-9_]
\W|non-alpha

#### Test the presence of a pattern in JavaScript
```
pattern = /test/;
pattern.test("This is a test");  // Returns true
```

#### Return all matched pattern into an array
```
var text = "This is an sentence";
var matches = text.match(/\w+/g);
if (matches != null) {
   var p1 = matches[0];  // return "This"
   var p2 = matches[1];  // "is"
}
```

#### Remove whitespace
```
.replace(/\s+/, "") 
.replace(/\s/g, "") 
```
