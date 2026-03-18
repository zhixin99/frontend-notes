# Basic

## consolo.log()
```js
let firstName = "Jean";
let age = 26;

// console.log add a space between each element
console.log("Hello", firstName); 
>>> Hello Jean

console.log("Hello" + " " + firstName)
>>> Hello Jean
```

## Varible
A variable is a container to store data in two steps:
- Declaration (let, var, const)
- Assignment (= assignment operator)

### Constant
const is a variable that can't be reassigned once it has been declared.  
``` If possible, use const. If not, use let. ```

```js
const PI = 3.1415926;

PI = 20; // ❌ TypeError
```
const does NOT mean “value never changes”  
It means: The variable binding is constant, not the value itself    

```js
const user = { name: "Alice" };
```

This binding is fixed:   
user ───▶ object A

You cannot do:
```js
user = { name: "Bob" }; // ❌ breaks the binding
```
Because that would mean:   
user ───▶ object B   (changed binding)

```js
const user = { name: "Alice" };

user.name = "Bob";     // ✅ allowed
user.age = 30;         // ✅ allowed

user = {};             // ❌ NOT allowed

```
```js
const arr = [1, 2, 3];

arr.push(4);   // ✅ allowed
arr[0] = 99;   // ✅ allowed

arr = [];      // ❌ NOT allowed
```

## Import and export
```js
// file: data.js
export const dinnerPartyGuests = [
    'Elvis Presley', 
    'The Queen of England'
    ]

export const shortSpaceTripsArr = [
    {destination: 'Moon pass'},
    {destination: 'Orbit the Earth'}]


// or we can remove the export between each const, and put it here
export { 
  dinnerPartyGuests, 
  shortSpaceTripsArr
}
```
```html
<body>
    <script src="index.js" type="module"></script>
</body>
```
```js
import { 
  dinnerPartyGuests as guest, 
  shortSpaceTripsArr as trip
} from "/data.js"
```
### export default 
One file can only have one default export.  
We should change the file name and the function name to the same to avoid the confusion.   
```js
// getMatchingTripsArr.js
export default function getMatchingTripsArr(arr, keyword){
    return arr.filter(function(trip){
        return trip.description.toLowerCase().includes(keyword)
    })
}
```
```js
// index.js
// we can use any name here, but in convention, we shoud keep the name same as the file name and the function name.  
import getMatchingTripsArr from './getMatchingTripsArr.js'
```
## import from my own file
We should use `./` to indicate that I'm importing this from my own file and it is not from a third party package.
```jsx
import Header from "./Header.jsx"
```

## When to write semicolon?
If {} are part of a statement’s grammar, don’t write ;.  
Blocks (if, for, while, function declaration)→ structural, no value → no semicolon
```js
if (x > 0) {
  doSomething();
}

for (let i = 0; i < 3; i++) {
  console.log(i);
}

while (x > 0) {
  x--;
}

switch (x) {
  case 1:
    break;
}

function foo() {
  return 1;
}

```
If {} produce a value used in an expression, write ;.
```js
const obj = {
  a: 1,
  b: 2
}; 
```

## ??（Nullish Coalescing Operator）
if value is null or undefined, result = 'default'.
```js
const result = value ?? 'default';
```

## strictly equal ===
Primitive values → compare by value   
Objects → compare by reference (identity): it checks whether both variables reference the same object in memory, not whether their contents are identical.
```js
const A = { color: 'lime green' };
const B = { color: 'lime green' };

A.color === B.color // true

A === B  // false, A and B are different objects


const C = A

A === C  // true


5 === 5         // true
'hi' === 'hi'   // true
true === true   // true

```


## Check the type of a value or object
### typeof()
The output is a string matching the name of one of the `primitive` data types, except for "null". It can also be "function" or "object".
```js
typeof undefined;
// => "undefined"

typeof NaN;
// => "number"

typeof 42n;
// => "bigint"

typeof function () {
  return 'Hello, World';
};
// => "function"

typeof [1, 2, 3, 4];
// => "object"

typeof { city: 'Stockholm', country: 'Sweden' };
// => "object"

typeof null;
// => "object"
```

## Recursion
Recursion occurs when a function calls itself, either directly or indirectly. It's similar to a loop, but it involves breaking a problem down into smaller, more manageable sub-problems.

# Command
## Normal comment
```js
// this is a normal comment

/* this is also a normal comment */
```

## JSDoc
```js
/**
 * @param {string} name
 * @returns {number}
 * @typedef {TYPE} Name
 */
```
Example:  

Translation is a {} object, it has 2 keys: translation and quality. 
```js
/**
 * @typedef {{ translation: string, quality: number }} Translation
 * /
```

TranslatableValues is a map like `Record<key, value>`.  
key is a string, value is the an array. The array contains null or the Translation object. 
```js
 /**
 * @typedef {Record<string, Array<null | Translation>>} TranslatableValues
 */

// An exmaple of TranslatableValues
const values = {
  title: [
    { translation: "Hello", quality: 0.9 },
    null
  ],
          cription: [
    { translation: "World", quality: 0.8 }
  ],
  footer: [
    null,
    null
  ]
};

```

## JSON
Javascript object notation  
* Valid JSON: https://jsonlint.com/
* The key needs to be surrounded by `double quotes`
* In most cases, it would be 1 object or an array of objects
```json
// person.json
{
    "name": "Joe Schmoe",
    "age": 42,
    "adult": true,
    "hobbies": [
        "skiing",
        "surfing",
        "piccolo"
    ]
}
```
```json
[
    {
        "name": "Sarah",
        "age": 35,
        "birthplace": "Scotland",
        "hobbies": [
            "violin",
            "singing",
            "crafting"
        ]
    },
    {
        "name": "Michael",
        "age": 56,
        "birthplace": "South Africa",
        "hobbies": [
            "skateboarding",
            "guitar"
        ]
    }
]
```
* Check JSON in dev tool
* Network → Fetch/XHR = check the requested API
![Check JSON in dev tool](../Images/JSON-in-dev-tool.png)



