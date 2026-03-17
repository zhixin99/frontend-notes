# Type conversions

## Convert between string and array
```JS
let myLeads = `["www.awesomelead.com"]`
// Turn the myLeads string into an array
myLeads = JSON.parse(myLeads)

// Turn the array into a string 
myLeads = JSON.stringify(myLeads)
```


## Convert object values into an array
```js
const loginCredentials = {
    "rafidhoda": "BestPassword123",
    "shahrukhkhan": "InBigCitiesSmallThingsHappen",
    "jackblack": "ThisIsNotTheGreatestPasswordInTheWorld"
}

console.log(Object.keys(loginCredentials))
>>> ['rafidhoda', 'shahrukhkhan', 'jackblack']

console.log(Object.values(loginCredentials))
>>> ['BestPassword123', 'InBigCitiesSmallThingsHappen', 'ThisIsNotTheGreatestPasswordInTheWorld']

console.log(Object.entries(loginCredentials))
//  array contains sub arrays
>>> [['rafidhoda', 'BestPassword123'], ['shahrukhkhan', 'InBigCitiesSmallThingsHappen'], ['jackblack', 'ThisIsNotTheGreatestPasswordInTheWorld']]
```

# Type conversion
## Get the type
```js
const y = 3
console.log(y, typeof y);
>>> 3 number
```

## Convert string to number
```js
                                    // input
const numOne = document.getElementById("num-one")
                                    // input
const numOne = document.getElementById("num-two")
const result = document.getElementById("result")

result.textContent = `${numOne.value} + ${numTwo.value} = ${Number(numOne.value) + Number(numTwo.value)}`
```


## String, number
```js
let age = window.prompt("How old are you?"); // window.prompt will return a string

consolo.log(tyepof age) // get the type 
>>> string

age = Number(age); 
consolo.log(tyepof age) 
>>> number
```
```js
let x;
let y;
let z;

x = Number("3.14");
console.log(x, typeof x)
>>> 3.14, number

Number('');
// => 0

/// If you try to convert a non-primitive value or a string that does not represent a number, the result is NaN (Not-A-Number).
Number({ num: 123 });
>>> NaN
```
```js
y = String(3.14);
console.log(y, typeof y);
>>> 3.14 string

String(null);
// => 'null'

String(undefined);
// => 'undefined'

// For arrays, the String function will apply the string conversion for each element and join the results with a comma.  Note that in these cases null and undefined will be converted to an empty string.
arr = [42, null, true, 'abc']
String(arr);
// => '42,,true,abc'

// use .join() to custom the separator
const result = arr.join("");

//For objects, by default String returns an unhelpful text.
String({ key: 'value' });
// => '[object Object]'
```
