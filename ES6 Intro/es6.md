# How to ES6
### A look into the future of JavaScript

---
#Sam Couch
###Software Engineer
###@SamuelCouch
####www.samcouch.com

---

# What's an ES6?
### Also known as `ECMAScript 6`...

*ECMAScript is the "proper" name for the language commonly referred to as JavaScript*

---
##OK, cool. So what?

---
> ES6 provides a lot of really awesome new features!

---
## What's new?
- `let` keyword
- Classes 
- Arrow Functions
- Modules
- Promises
- Rest Parameters
- Function Generators

---
##That's not everything,
###But it's a good start!

---
# Let's get into it!

---
## `let`
Typically in JavaScript we're used to 
<br />

```javascript
var myVar = 'variable';
```
<br />
ES6 gives us enhanced scoping  capabilities with variables with the use of the __let__ keyword.

---
## `let` vs. `var`

`var` is scoped to the nearest __function__ block (Or global if declared outside of a function)
<br />
`let` is scoped to the nearest __enclosing__ block (Or global is declared outside of any block)

---
##Gibberish... What's that even mean?

---
## `let` vs. `var`
```javascript
let dog = 'good'; //globally scoped
var cat = 'bad'; //globally scoped
```
```javascript
function simpleSampleFunctionBlock() {
    let kobe = 'GOAT'; //function block scoped
    var lebron = 'NOT GOAT'; //function block scoped
};
```

__These samples are all the same, nothing particularly new__

---
## `let` vs. `var`

```javascript
for(let i = 0; i < 10; i++){
  // `i` is ONLY  visible here
}

for(var j = 0; j < 10; j++){
  // `j` is visible here
}
// `j` is ALSO visible here
```

---
## Classes

```javascript
var Outdated = function(thing){
  this.lame = thing;
}
Outdated.prototype.getLameThing = function(){
  return this.lame;
}
```

__This isn't awful, but it could be prettier.__

---
##Classes
```javascript
class Modern {
  constructor(thing){
    this.cool = thing;
  }

  getCoolthing(){
    return this.cool
  }
}
```

__Now that's more like it!__

---
##Arrow Functions
```javascript
//ES5
app.get('/es5', function(req, res){
  res.send('This works');
});
//ES6
app.get('/es6', (req, res) => {
  res.send('Also works, and is awesome!');
});
```

__That may not seem all too useful, but it get's better.__

---
##Arrow Functions

```javascript
var numbers = [2, 4, 6, 8, 10];
var squares = numbers.map((num) => num*num);
console.log(squares); // [4, 16, 36, 64, 100] 
```

__Single line expressions are pretty rad I think!__

---
## Modules
### Back in the day we would rely on `module.exports`

---
##Modules (Export)

```javascript
//utils.js
function multiply(a, b){
  return (a*b)
}
function raddify(orig){
  return orig.replace('bad', 'rad')
}
export {multiply, raddify}
//Can even specify names
// export {multiply as mult, raddify as rad}
```

---
##Modules (Import)

```javascript
//app.js
import {multiply, raddify} from 'utils'

console.log(multiply(2, 4)); //8
var ex = 'This is pretty bad'
console.log(raddify(ex)); // 'This is pretty rad'
```

---
##Modules (...one more export...)

```javascript
//utils.js (ES6-ified)
var utils = {
  multiply: (a, b) => {
    return (a*b);
  },
  raddify: (orig) => {
    return orig.replace('bad', 'rad')
  }
}

export default utils;
```

And now...

```javascript
//app.js
import utils from 'utils'
console.log(utils.mutiply(2, 2)); //4
```

---
##Promises
Better than callbacks, **PROMISES** provide representation of a value that may be made available in the future.

###Packages that have been available
* promise
* q
* bluebird

---
##Promises

```javascript
var ourPromise = new Promise(function(resolve, reject) {
  // do a thing, possibly async, then…
  if (/* everything turned out fine */) {
    resolve("Stuff worked!");
  }
  else {
    reject(Error("It broke"));
  }
});

ourPromise.then(function(result) {
  console.log(result); // "Stuff worked!"
}, function(err) {
  console.log(err); // Error: "It broke"
});
```

---
##Promises

A "promisified" function is considered __thenable__. Which is to say, it has access to the __then__ method.

```javascript
Promise.then = (resolve, reject) => {
  if SUCCESS {
    resolve();
  }
  if ERROR {
    reject();
  }
}
```

---
##Rest Parameters
Sometimes you just don't know how many parameters you'll be receiving in a given function.

```javascript
//old.js
function getNames(){
  var names = Array.prototype.slice.call(arguments);
  names.forEach(function(name){
    console.log(name);
  })
}
```

You have to convert your arguments to an array before you can do anything with it.

---
##Rest Parameters

```javascript
//new.js
function getNames(...names){
  names.forEach(function(name){
    console.log(name);
  });
}
```

### Ain't that fancy!?

---
##Function Generators[^1]
Generators are *most* ideal for defining sequences of undetermined lengths. 

__A generator requires one (or more) `yield` expressions__

Uses the notation of __function* thing()__ 

[^1]: Function generators aren't **fully** supported yet, but it's getting there!

---
##Function Generators

```javascript
function* fibonacci(){
  let [prev, curr] = [0, 1];
  for (;;) {
    [prev, curr] = [curr, prev + curr];
    yield curr;
  }
}

//loop example
for (n of fibonacci()) {
  if (n > 20) //stop at 20
    break;
  console.log(n);
}
//using iterator methods
let fib = fibonacci();
for(var i =0; i<20; i++){
  console.log(fib.next());
}
```

---
# What now?

---
## What now?
To get started with ES6 **today** we have to rely on other tools in order to take our modern (ES6) code and translate it into the forms that our current tools can use.

---
#Compilers
#### (It's plural, but there's really only one that I'm recommending)

---
#Babel.js

---
##Babel.js
> Babel is a JavaScript compiler
###www.babeljs.io

---
##Using Babel
The easiest way (in my opinion) is to use the __require__ hook

__npm install babel__

```javascript
//index.js
require("babel/register");
module.exports = require('./lib');
```

---
##Using Babel
#### 2 Assumptions:
```javascript
//index.js
require("babel/register");
module.exports = require('./lib');
```

1. You have a __lib__ directory which contains your ES6-ified app
1. You run your app via __node index.js__

---
##More Resources
-  www.babeljs.io
-  www.github.com/ericdouglas/ES6-Learning
-  www.mzl.la/1dd9br6

---
## @SamuelCouch
