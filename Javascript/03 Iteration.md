# Loop
## for loop
```js
const list = ['a', 'b', 'c'];
//   start      finish           step
for (let i = 0; i < list.length; i += 1) { 
	console.log(list[i])
}

//   start      finish           step
for (let i = 0; i < list.length; i++) { 
	console.log(list[i])
}
```

## for of 
For each item in an iterable object like `Array`, String. Not for `Object`.
```js
const characters = [
    {
        title: 'Ninja',
        emoji: '🥷',
        powers: ['agility', 'stealth', 'aggression'],
    },
    {
        title: 'Sorcerer',
        emoji: '🧙',
        powers: ['magic', 'invisibility', 'necromancy'],
    }
]

for (let character of characters){
    console.log(character)
}
```
Example: Implement a function birdsInWeek that accepts an   `array-like` object of bird counts per day and a week number. It returns the total number of birds that you counted in that specific week. You can assume weeks are always tracked completely. e.g.
```js
birdsPerDay = [2, 5, 0, 7, 4, 1, 3, 0, 2, 5, 0, 1, 3, 1];
birdsInWeek(birdsPerDay, 2);
// => 12
```
```js
export function birdsInWeek(birdsPerDay, week) {
	let sum = 0;
	let start = (week-1) * 7; // determine the start and end 
	let end = week * 7
	
	for (let i = start; i < end; i++){
		sum += birdsPerDay[i]
	};
	return sum;
}
```


## For loop Break and Continue
* There is no way to stop the iteration once the forEach loop was started. The statements break and continue do not exist in this context.
* Break: stop the iteration
* Continue: skip the current element and continue on the next iteration




## while loop
Multiple conditions - using && or ||
```js
let i = 0;
while (i < orders.length && timeLeft > 0>) {
	.....
	i += 1
}

// the condition is checked after the loop body was executed
do {
	// The code here will always be executed once and then
	// repeatedly while the condition is true.
} while (condition);
```

```js
let i = 0;

while (i < 100) {
	
	i = i + 2;

	if (i % 3 === 0) {
		continue;
	}

}
```


