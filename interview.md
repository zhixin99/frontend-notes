# Interview

## Panic function 
Write a PANIC! function. The function should take in a sentence and return the same sentence in all caps with an exclamation point (!) at the end. 

If the string is a phrase or sentence, add a 😱 emoji in between each word. 

Example input: "Hello"
Example output: "HELLO!"

Example input: "I'm almost out of coffee"
Example output: "I'M 😱 ALMOST 😱 OUT 😱 OF 😱 COFFEE!"


```js
function panic(str){
    return str
        .split(' ')
        .join(' 😱 ')
        .toUpperCase() + "!";
}
```

## Alternating Caps 
 Write a function that takes in a string of letters
 and returns a sentence in which every other letter is capitalized.

Example input: "I'm so happy it's Monday"
Example output: "I'M So hApPy iT'S MoNdAy"


```js
function altCaps(str){
     // assemble each character back into a new string
     let newStr = '';
    // loop through the string
    for(let i = 0; i < str.length; i++){
        // uppercase every character with an even index
        if(i % 2 === 0){
            newStr += str[i].toUpperCase();
        } else {
            newStr +=
        }
    }
    
   
    return newStr;
}

console.log(altCaps("When you visit Portland you have to go to VooDoo Donuts"));
```

## Anagrams
Anagrams are groups of words that can be spelled with the same letters. 
For example, the letters in "pea" can be rearrange to spell "ape", and 
the letters in "allergy" can be rearranged to spell "gallery."

Write a function to check if two strings of lowercase letters are anagrams. 
Return true if the word is an anagram. Return false if it isn't. 

Example input: "allergy", "gallery"
Example output: true

Example input: "rainbow", "crossbow"
Example output: false


```jsx
function isAnagram(str1, str2){
    return str1.split("").sort().join("") === str2.split("").sort().join("")
    
}
```

## Flatten array
Write a function to flatten nested arrays of strings or
numbers into a single array. There's a method
for this, but pratice both doing it manually and using the method. 

Example input: [1, [4,5], [4,7,6,4], 3, 5]
Example output: [1, 4, 5, 4, 7, 6, 4, 3, 5]
*/

const kittyScores = [
    [39, 99, 76], 89, 98, [87, 56, 90], 
    [96, 95], 40, 78, 50, [63]
];

const kittyPrizes = [
    ["💰", "🐟", "🐟"], "🏆", "💐", "💵", ["💵", "🏆"],
    ["🐟","💐", "💐"], "💵", "💵", ["🐟"], "🐟"
];

```js
function flatten(arr){
    return arr.flat();
}

function flatten(arr){
    // initialize a new, empty array
    // loop through the passed in array and check - string or array? 
        // if the item is string, push into the new array
        // if the item is an array, loop through it, pushing each item into the array
    // return new array
    
    const newArr = [];
    
    arr.forEach(element => {
        if(Array.isArray(element)){
            element.forEach(item => newArr.push(item))
        } else {
            newArr.push(element);
        }
    });
    return newArr;
}
```

## Loop object
Your function should take in a food object and find the food
with the most votes. It should log the winner, along with 
how many votes it received.  

Example input: {"🐈 cats": 19, "🐕 dogs": 17} 
Example output: The winner is 🐈 cats with 19 votes!
*/ 
```js
const gameNightFood = {
    "🍕 pizza": 3, 
    "🌮 tacos": 10, 
    "🥗 salads": 7,
    "🍝 pasta": 5
}

function findTheWinner(obj){
    // initialize some new variable to: 
        // keep track of the current highest vote number
        let highestVotes = 0;
        // keep track of the current winning item
        let winningItem = "";
    // for each food option in the food object
    for(let food in obj){
          // is the current value higher than the value of highestVotes?
          if(obj[food] > highestVotes){
              // yes: the new value of highestVotes in the current value and
              highestVotes = obj[food];
              // winningItem = the current property
              winningItem = food;
          }   
    }
      
    // return string announcing the winner using winningItme and highestVote variables
    return `The winner is ${winningItem} with ${highestVotes} votes.`
}

console.log(findTheWinner(gameNightFood));
```

