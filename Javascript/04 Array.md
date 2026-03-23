# Array
An array is an ordered list of items. To create an array, add elements between square brackets [].     

It can hold any type of primitives or object(composite), even `mixed` types.  
```js
let myself = ["Jean", 27, true]
```
 
It is mutable.

## .length - property
1 larger than the final index
```js
const numbers = [1, 'two', 3, 'four'];
numbers.length;
// => 4
```

## [] - Indexing
It returns an element, no an sub-array.
```js
const numbers = [1, 'two', 3, 'four'];
numbers[2];
// => 3
```
We can't use **[-index]** !!!
```js
numbers[-1];
>>> undefined
```

To change an element in the array, you assign a value at the index:
```js
const numbers = [1, 'two', 3, 'four'];
numbers[0] = 'one';
console.log(numbers);

>>> ['one', 'two', 3, 'four']
```

## array.slice(start, end)
creates a `sub-array`
```js
let arr = [1, 2, 3, 4, 5];

let part = arr.slice(1, 4);

console.log(part); // [2, 3, 4]
```
it's ok to use -index in slice
```js
arr.slice(-1)
>>> [5]

arr.slice(-2)
>>>[4, 5]
```

### .includes() - determines whether an array includes a certain value
```js
const numbers = [1, 'two', 3, 'four']
numbers.includes(1)
>>> true

numbers.includes("1")
>>> false
```

## .filter()
* It is going through each of the element in an array and test one by one. 
* After testing, each of the element will return `true` or `false`
``` js
const ages = [1, 5, 9, 23, 56, 10, 47, 70, 10, 19, 23, 18]

// pass in a function, the parameter will be assign to each of the element in turn 
const adults = ages.filter(function(age){
    if (age >= 18){
        return true
    }
    else {
        return false
    }
})
```

This is too complex, and we can simplify it by 
```js
const adults = ages.filter(function(age){
    return age >= 18
})
```

Or with arrow function
```js
const adults = ages.filter(age => age >= 18)

console.log(adults)
>>> [23, 56, 47, 70, 19, 23, 18]
```

## .every() 
```js
const numbers = [1, 3, 5, 7, 9];
numbers.every((num) => num % 2 !== 0);
// => true
```

## .some()
returns true if some of the element meet the requirement
```js
[1, 3, 5].some(n => n % 2 === 0); // false
[1, 4, 5].some(n => n % 2 === 0); // true
```

## .push() & .unshift()  - Add element and return the length
The .push() method adds one or more elements to the `end` of an array and returns the new `length` of the array.
```js
const numbers = [1, 'two', 3, 'four'];
numbers.push(5); 
console.log(numbers);

>>>[1, 'two', 3, 'four', 5]
```
The unshift() method adds one or more elements to the `beginning` of an array and returns the new length of the array.4
```js
const numbers = [1, 'two', 3, 'four'];
numbers.unshift('one'); // => 5
numbers;
// => ['one', 1, 'two', 3, 'four']
```

## .pop() & .shift() - Remove and return the removed element
The pop() method removes the `last` element from an array and returns that element. 
```js
const numbers = [1, 'two', 3, 'four'];
numbers.pop(); 
console.log(numbers);

>>> [1, 'two', 3]
```
The shift() method removes the `first` element from an array.
```js
const numbers = [1, 'two', 3, 'four'];
numbers.shift(); 
console.log(numbers);

>>> ['two', 3, 'four']
```

## .join() method
concatenate elements of an array into a string and returns the new string
```js
const guestsArr = ['Amy', 'Clare', 'Keith', 'Dan'] 

console.log(guestsArr.join(''))

>>> AmyClareKeithDan
```

```js
console.log(guestsArr.join('🐶'))

>>> Amy🐶Clare🐶Keith🐶Dan
```
```js
console.log(guestsArr.join(' '))

>>> Amy Clare Keith Dan
```

## .map() method 
* It gives us a new `array` and we're going to store the array in a const.   
* If we don't need a new array it returns, we don't need to use map method.  

```js
function getLabelsHtml(text, sender, ...staffObjs) {
    return staffObjs.map(staffObj => 
        `<div class="label-card">
            <p>Dear ${staffObj.name}</p>
            <p>${text}</p>
            <p>Best wishes,</p>
            <p>${sender}</p>
        </div>`
    ).join('')
}

const text = 'Thank you for all your hard work throughout the year! 🙏🎁'
const sender = 'Tom'

document.getElementById('labels-container').innerHTML = getLabelsHtml(
    text, 
    sender, 
    {name: 'Sally'}, 
    {name: 'Mike'}, 
    {name: 'Rob'}, 
    {name: 'Harriet'}
    ) 
```
* We can also use .map() to only get a part of the array
```js
// turn the array into an array of string email addresses of only the people in the array who voted. 

const voters = [
    {name: "Joe", email: "joe@joe.com", voted: true},
    {name: "Jane", email: "jane@jane.com", voted: true},
    {name: "Bo", email: "bo@bo.com", voted: false},
    {name: "Bane", email: "bane@bane.com", voted: false}
]

const email = voters.filter(function(voter) {
    return voter.voted
}).map(function(voter) {
    return voter.email
})

console.log(email)

>>> ['joe@joe.com', 'jane@jane.com']
```

## .forEach() method
* Use the forEach() method when you don't need to create a new array
* **Never use return** in forEach
```js
// pass in an anonymous function with a parameter, which will be each individual element in the array
characters.forEach(function(character){
	console.log(character)
})
```

```js
// know the index of the element that you are working on
characters.forEach(function(character, index){
    console.log(character, index)
})

>>> 
0 Ninja
1 Sorcerer
```
### return undefined error
* It doesn't return a new array! It returns `undefined`! We need to avoid using `return` in the forEach() function. 
* The correct way is to create the array first and push element to the array. 
```js
const playlistHtml = []

playlistArr.forEach(function(track){
    playlistHtml.push( `
    <section class="card">
        <div class="card-start">
            <img src="/images/${track.albumArt}">
        </div>
    </section>
    `)
})  
document.getElementById('container').innerHTML = playlistHtml.join('') 
```

## .reduce() method
* Reduces the array into a single value.  
* It takes an `accumulator` and the `current element` in the array as parameters. 
* By default, **accumulator** will be the `first element` in the array, and **currentValue** will be the `2nd element` from the beginning. 
* then, the 2nd element is added up to the accumulator, and the 3nd element become the current Value.
```js
let arr = [1, 2, 3, 4]

arr.reduce((total, currentValue) => total + currentValue)
```
* with object, we shouldn't add the object together.
* We can give the `reduce` funtion `another parameter` 0
* It means that the first total is 0, and the first currentValue is the first element in the array
```js
const studentsArr = [
    {
        name: 'Mike',
        grade: 75
    },
    {
        name: 'Emma',
        grade: 83
    },
    {
        name: 'Seth',
        grade: 66
    }
]

studentsArr.reduce((total, currentValue) => 
  total + currentValue.grade, 0)   

```

```js
// Classify the numbers by whether they are odd or not
arr.reduce(
  (accumulator, currentValue) => {
    if (currentValue % 2 === 0) {
      accumulator.even.push(currentValue);
    } else {
      accumulator.odd.push(currentValue);
    }

    return accumulator;
  },
  { even: [], odd: [] },
);
// => { even: [2, 4], odd: [1, 3] }
```

## Spread operator 
It expands an array into `a list of elements`. Each of the element is `separate`！！！
```js
const lunchMenu = ['Greek Salad', 'Open Sandwich']

// it returns the individual element inside of the array
console.log(...lunchMenu)
>>> "Greek Salad", "Open Sandwich"
```
### Copy of an array
spread operator is used as a good way to copy an array
```js
const testArr = [1, 2, '3']

const testArrCopy = [...testArr]
```
### Find the max and min value in an array
```js
const averageSharePriceByMonthQ1 = [109.6, 103.3, 89.4]
const averageSharePriceByMonthQ2 = [109.3, 126.1, 103.3]
const averageSharePriceByMonthQ3 = [120.8, 102.3, 106.8]
const averageSharePriceByMonthQ4 = [110.9, 119.8, 113.7]

function findPriceExtremes(arr){
    const highest = Math.max(...arr) // it takes a sequence of individual numbers
    const lowest = Math.min(...arr)
    console.log(`The highest average share price was ${highest}`)
    console.log(`The lowest average share price was ${lowest}`)
}

findPriceExtremes([
    ...averageSharePriceByMonthQ1,
    ...averageSharePriceByMonthQ2,
    ...averageSharePriceByMonthQ3,
    ...averageSharePriceByMonthQ4
])
```

## + symbol
`+` does NOT merge arrays. What actually happens:
- Each array is converted to a string
- Then the strings are concatenated
```js
const friendsList = ['noodles', 'sauce', 'mozzarella', 'kampot pepper'];
const myList = ['noodles', 'meat', 'sauce', 'mozzarella'];

const totalList = friendsList + myList
totalList
>>> "noodles,meat,sauce,mozzarellanoodles,sauce,mozzarella,kampot pepper" 
```

## Array destructuring
It is a concise way to extract values from an array and assign them to distinct `variables`.

```js
const numberOfMoons = [0, 2, 14];
const [venus, mars, neptune] = numberOfMoons;

neptune;
// => 14
```
Leaving a position unnamed (by not writing any variable name) silently ignores that position.
```js
const deck = [5, 9, 7, 1, 8];

const [firstCard] = deck

console.log(firstCard)
>>> 5
```
Example: Elyse takes three cards and quickly moves the top card to the back, making the middle card the first card and the old bottom card the middle card. She doesn't need to call a single function.
```js
// we will pass in an array of 3 card as the parameter
export function shiftThreeCardsAround(deck) {
    const [firstCard, secondCard, thirdCard] = deck;
    return [secondCard, thirdCard, firstCard];
}
```

## Shallow copy
* When we are copying a `single object` from an `array`, if the object changes, the original array will also change. 
* When creating an const which holds an array of objects, JavaScript creates that array in memory. So the const holds a reference to the array in memory.   
* When we copy an object from that array, JS will not create the object in the memory. So the object also holds a reference to the original **array in the memory**. 
<img src="../Images/shallow-copy.png" width="400">

```js
const usersArray = [
    {
        userName: 'Tom',
        password: '123456'
    }
]

const userObj = usersArray[0]

userObj.userName = "Wayne"

console.log(usersArray)
console.log(userObj)

>>>

[{userName: 'Wayne', password: '123456'}]
{userName: 'Wayne', password: '123456'}
```
* In the filter example, remember to add `[0]` so it is an obejct instead of a new array. Only in this case, the original data will change!
```js
const orderedProduct = menuArray.filter(menu => menu.id === Number(e.target.dataset.id))[0]
```











## .find()
It returns the `value` of the first element in the array that passes the predicate test. The method returns undefined when none of the elements in the array pass the predicate test.
```js
const numbers = [1, 3, 5, 7, 9];
numbers.find((num) => num < 5);
// => 1
```

## .findIndex()
The findIndex(predicate) is the same as the find() method, but it returns the (first) `index` of the element that passes the predicate test instead of the value. The method returns -1 when none of the elements in the array pass the predicate test.
```js
const numbers = [1, 3, 5, 7, 9];
numbers.findIndex((num) => num > 7);
// => 4
numbers.findIndex((num) => num > 9);
// => -1
```

## .indexOf() - Get the first index of the value
```js
const numbers = [1, 'two', 3, 'four']
numbers.indexOf(1)
>>> 0
```

-------------------------------------------------------



## .reverse()
```js
const arr = [1, 2, 3]
arr.reverse();

>>> [3, 2, 1]
```

## .sort()
sorts the elements of an array by first converting them to `strings` and then applying string comparison   
sort also `returns that modified array` which is convenient if you want to chain other methods to it.   

```
```js
const arr = ['c', 'a', 'z', 'b'];
const result = arr.sort();

console.log(result);
// => ['a', 'b', 'c', 'z']

console.log(arr);
// => ['a', 'b', 'c', 'z']
```
To customize the sorting behavior, you can pass a comparison function as an argument.   
The comparison function itself is called with two arguments which are two elements of the array.   
It then needs to return the following:
- a negative number if the first argument should be sorted before the second
- a positive number if the first argument should be sorted after the second
- 0 if the order of the elements should stay the same


Sort the number. 
```js
// without the customized sorting: it is sorting the string, not the number value!
const arr = [10, 2, 30];

arr.sort();

arr;
>>> [10, 2, 30]

// the correct way
arr.sort((a, b) => a - b) // sort from small to big
arr.sort((a, b) => b - a) // sort from big to small
```

```js
const arr = [
  { name: 'Lydia', age: 7 },
  { name: 'Anne', age: 34 },
  { name: 'Holger', age: 59 },
];

// sort by lexicographical order
arr.sort((item1, item2) => {
  if (item1.name < item2.name) {
    return -1;
  }
  if (item1.name > item2.name) {
    return 1;
  }
  return 0;
});

// sort by age
arr.sort((item1, item2) => item1.age - item2.age)

// sort by age first, then name
arr.sort((item1, item2) => {
  if(item1.age == item2.age){
    if (item1.name < item2.name) {
    return -1;
  }
    if (item1.name > item2.name) {
    return 1;
  }
    return 0;
  }
  return item1.age - item2.age;}
)
```


```






### array.splice(start, deleteCount, item1, item2, ...)
The splice() method changes the contents of an array by removing or replacing existing elements and/or adding new elements in place. This method returns an `array` containing the deleted elements.
```js
array.splice(startIndex, deleteCount, item1, item2, ...)
```

``` js
// replace
const numbers = [1, 'two', 3, 'four'];
numbers.splice(2, 1, 'one'); // => [3]
numbers;
// => [1, 'two', 'one', 'four']

// add
const numbers = [1, 'two', 3, 'four'];
numbers.splice(2, 0, 'one', 3); // => []
numbers;
// => [1, 'two', 'one', 3, 3, 'four']

// delete
const numbers = [1, 'two', 3, 'four'];
numbers.splice(2, 2); // => [3, 'four']
numbers;
// => [1, 'two']
```



### Rest operator
When ... appears on the left-hand side of an assignment, those three dots are known as the rest operator. The three dots together with a variable name is called a `rest element`. It collects zero or more values, and stores them into a single array.  

```js
// ...everythingElse is called a rest element
const [a, b, ...everythingElse] = [0, 1, 1, 2, 3, 5, 8];
a;
// => 0
b;
// => 1
everythingElse;
// => [1, 2, 3, 5, 8]
```
A rest element cannot have a trailing comma. It must be the last element in a destructuring assignment.
```js
const [...items, last] = [0, 1, 1, 2, 3, 5, 8];

>>> SyntaxError
```
-------------------------------------------
## Array.isArray()
The Array class has a method called Array.isArray() that checks if its argument is an array.
```js

Array.isArray([1, 2, 3])      // true
Array.isArray([])            // true

Array.isArray({})            // false
Array.isArray("hello")       // false
Array.isArray(123)           // false
Array.isArray(null)          // false
Array.isArray(undefined)     // false

```

# Comparison
Reference objects can be compared, but only by reference, not by value.
```js
[] == []   // false
{} === {} // false
```
Example: Implement the isNonEmptyArray function, that checks if a value is a `non-empty` array.
```js
export function isNonEmptyArray(value) {
    return Array.isArray(value) && value !== [] // this is wrong

}

// correct
export function isNonEmptyArray(value) {
    return Array.isArray(value) && value.length >= 1

}
```