# Function
Functions are a first-class object in JavaScript

## Function Declarations
JavaScript moves declarations to the top of the scope before running the code.
```js
//           parameters
function add(num1, num2) {
  return num1 + num2;
}
// arguments
add(1, 3);
>>> 4
```

## How does return work
```js
const distanceWalkedMilesArr = [140, 153, 161, 153, 128, 148]
const conversionFactorMilesToKm = 1.6
```
* The `comma operator` in the return evaluates both expressions but returns only the last one.
```js
const distanceWalkedKmArr = distanceWalkedMilesArr.map(function(distanceMiles, index){
    return distanceMiles * conversionFactorMilesToKm, index
})

console.log(distanceWalkedKmArr)
>>> [0, 1, 2, 3, 4, 5]
```
* If we want to return more than 1 value, we can wrap them in an array or object
```js
const distanceWalkedKmArr = distanceWalkedMilesArr.map(function(distanceMiles, index){
    return [index, distanceMiles * conversionFactorMilesToKm]
})

console.log(distanceWalkedKmArr)
>>> [[0, 224], [1, 244.8], [2, 257.6], [3, 244.8], [4, 204.8], [5, 236.8]]
```
```js
const distanceWalkedKmArr = distanceWalkedMilesArr.map(function(distanceMiles, index){
    return `${index}: ${distanceMiles * conversionFactorMilesToKm}`
})

console.log(distanceWalkedKmArr)
['0: 224', '1: 244.8', '2: 257.6', '3: 244.8', '4: 204.8', '5: 236.8']
```

## Function Expression
Function Expression is assigned to a variable and is not hoisted.  
We need to declare a const and assign it with an anonymous function.  
```js
// in this example, the function returns nothing.  
const greeting = function(){
  console.log("Hello!");
};

console.log(greeting);
>>> [Function: result]

console.log(function(){
  console.log("Hello!");
})
>>> [Function (anonymous)]

// add () to invoke the function 
console.log(greeting())   
>>> Hello!  // this is from the console.log inside of the function
>>> undefined  // nothing is returned, so it is undefined. 


console.log(function(){
  console.log("Hello!");
}())
>>> Hello!
>>> undefined
```

If we add the `return`
```js
const greeting2 = function(){
  return "Hello World!"
};

console.log(greeting())   
>>> Hello World!
```

## Arrow function expression
- If the function body contains only a return statement, the {} and the return keyword can be omitted.   
- More complex logic requires the {} and the return keyword
```js
const addUpTwoNumbers = function(a1, a2){
  return a1 + a2
}

// equals to 
const addUpTwoNumbers = (a1, a2) => {
  return a1 + a2
}

// equals to 
const addUpTwoNumbers = (a1, a2) => a1 + a2
```

- If there is only `one` parameter, the parenthesis () can be omitted.   
 
```js
const multiply = a1 => a1 * 5
```
- 0 or 2 or more needs the parenthesis.   
```js
const zero = () => 0
```

## Default parameter
Give the argument = xx to replace the missing parameter.
```js
function calculateTotalCost(itemsBoughtArr, discount = 0) {

}
```

## ...name - Rest parameters 
* We got a function that takes in parameters but we don't know how many arguments that is going to be passed to it.   
* It captures all the arguments which don't explicitly match an exsiting parameter. 
* All the rest arguments will be wrapped in an `array`. 

```js
function setPermissionLevel(permissionLevel, ...names) {
    names.forEach((name)=> 
      console.log(`${name} now has ${permissionLevel} level access.`))   
}

setPermissionLevel('admin', 'Dave', 'Sally', 'Mike', 'Clare')
```

## Closures
```js
function makeCounter(){
    let count = 0;

    return function(){
        count ++;
        return count;
    };

}

const counter = makeCounter() // the counter here is atucally the whole function(){....} after return 

counter()
>>> 1

counter()
>>> 2

// when we run counter(), the let count = 0 will not run. 
// the count is stored. so the number is increasing. 
```
Example: Return a function that memoizes the last result.  If the arguments are the same as the last call, then memoized result returned.  
@param {function} f the transformation function to memoize, assumes takes two arguments 'x' and 'y'  
@returns {function} a function which takes x and y arguments, and will either return the saved result  
if the arguments are the same on subsequent calls, or compute a new result if they are different.  
```js
export function memoizeTransform(f) {
  let lastx;
  let lasty;
  let lastresult;
  return function(x, y){
    if(lastx===x && lasty ===y){
      return lastresult
    };
    
    lastx = x;
    lasty = y;
    lastresult = f(x, y);
    return lastresult;
  
  }
}
```

