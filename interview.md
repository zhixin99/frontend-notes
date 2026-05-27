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