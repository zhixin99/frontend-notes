# String
Strings are immutable in JavaScript.
```js
let s = "hello";
s[0] = "H";
console.log(s); 

>>> "hello"  // still hello
```

## .length 
```js
let userName = "Jean";
console.log(userName.length); // no parentheses
>>> 4
```

## [] - Indexing
```js
let userName = "Jean Zhu";

console.log(userName[0])
>>> J

//  doesn't accpet negative index as the arguement
console.log(userName[-1]); 
>>> undefined
```

## .slice()
- We can use .slice(0, -1), which is the whole string but the last word.

```js
let firstName = userName.slice(0, 4) 
let lastName = userName.slice(5)  // without comma, it will take everything until the end


let index;
index = userName.indexOf(" ")
firstName = userName.slice(0, index) 
lastName = userName.slice(index+1)
```

## .split() - convert string to array
```jsx
const [currentWord, setCurrentWord] = useState("react")
const letterArray = currentWord.split("")
console.log(letterArray)

['r', 'e', 'a', 'c', 't']
```
```js
const str = '2022-02-09';

const result = str.split('-').at(-1);
console.log(result); // '09'
```

## Template strings 
It allows for embedding expressions in strings, and also break the string into lines. 
Backticks - (``) - are used to represent a template string.   
The `${...}` is to indicate the expression / variable.
```js
const num1 = 1;
const num2 = 2;
const sum = num1 + num2
const result = "Adding " + num1 + " and " + num2 " gives " + sum + "."
console.log(result)
>>> Adding 1 and 2 gives 3.

// or we can use a simpler way
console.log(`Adding ${num1} and ${num2} gives ${num1 + num2}.`);
>>> Adding 1 and 2 gives 3.
```
  
`All` types of expressions can be used with template strings.
```js
const track = 'JavaScript';

`This track on exercism.org is ${track.toUpperCase()}.`;
// => This track on exercism.org is JAVASCRIPT.
```

When you are needing to have strings formatted on multiple lines
```js
export function graduationFor(name, year) {
  return `Congratulations ${name}!
Class of ${year}`; 

>>> Congratulations Alice!
>>> Class of 2024
}
```
```js

return `Congratulations ${name}!
    Class of ${year}`;

>>> Congratulations Alice!
// Now the string literally contains four spaces before Class. 
// Those spaces are printed as part of the output, causing indentation. 
>>>     Class of 2024 
```

## includes()
same as array. 

## .indexOf() & .lastIndexOf() - Find the index
```js
let userName = "Jeane";
console.log(userName.indexOf("e")); // index of the first occurance of "e"
>>> 1

console.log(userName.lastIndexOf("e")); // index of the last occurance of "e"
>>> 4
```

## .trim() - Remove the spacing
- removing unwanted whitespace from the `beginning` and `end` of a string, but not the space between. 
```js
let userName = "   Jean   ";
console.log(userName.trim());
```

## .toUpperCase() & .toLowerCase()
```js
let userName = "   Jean   ";
console.log(userName.toUpperCase());
```

## .startsWith() & .endsWith()
```js
const str = "Saturday night plans";

console.log(str.startsWith("Sat"));
// Expected output: true
```

## .replaceAll()
```js
let userName = "Jean";
console.log(userName.replaceAll("J", "Z"));
>>> Zean
```

## Comparison
A dictionary (lexicographical) order is applied.
```js
'Apple' > 'Pear';
// => false

'a' < 'above';
// => true

'a' === 'A';
// => false
```





