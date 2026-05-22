# Problem solving method
* Create a function that takes 2 card objects as parameters, `card1` and `card2`, and determine which one has higher score
* These card objects have a property called `value`, which can be any one of the following strings, in order of rising "score":
"2", "3", "4", "5", "6", "7", "8", "9", "10", "JACK", "QUEEN", "KING", "ACE"

1. Map the string with the value
```js
const cardValues = {
    2: 2,
    3: 3,
    ...,
    10: 10
    JACK: 11,
    QUEEN: 12,
    KING: 13,
    ACE: 14
}

xxx = cardValues[card1] 
xxx = cardValues[card2] 
```

2. Use an array and compare the index
```js
const valueOptions = ["2", "3", "4", "5", "6", "7", "8", "9", 
    "10", "JACK", "QUEEN", "KING", "ACE"]
const card1ValueIndex = valueOptions.indexOf(card1.value)
const card2ValueIndex = valueOptions.indexOf(card2.value)
```