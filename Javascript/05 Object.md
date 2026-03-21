# Object
Only the type of the key is restricted: it has to be a `string`.  
It is mutable.

## Creating an Object
You create an object using curly brackets. State the key first, followed by a colon and the value.
```js
const obj = {
  //key           // value
  favoriteNumber: 42,
  greeting: 'Hello World',
  useGreeting: true,
  address: {
    street: 'Trincomalee Highway',
    city: 'Batticaloa',
  },
  fruits: ['melon', 'papaya'],
  addNumbers: function (a, b) {
    return a + b;
  }, // The trailing comma after the last entry is optional in JavaScript.
};
```

## Retrieving a Value - dot notaion 
There are two ways to retrieve the value for a given key, dot notation and bracket notation.  
```js
const obj = { greeting: 'hello world' };

obj["greeting"];
// => hello world

obj.greeting;
// => hello world
```

Bracket notation also works with variables, but dot notation doesn't. 
```js
const key = 'greeting';
obj[key];
// => hello world

obj.key // ❌ It is same as obj["key"]
```

## Adding or Changing a Value
You can add or change a value using the assignment operator =. Again, there are dot and bracket notations available.
```js
const obj = { greeting: 'hello world' };

obj.greeting = 'Hi there!';
obj['greeting'] = 'Welcome.';

obj.newKey1 = 'new value 1';
obj['new key 2'] = 'new value 2';

const key = 'new key 3';
obj[key] = 'new value 3';
```

## Deleting a pair
You can delete a key-value pair from an object using the delete keyword.
```js
const obj = {
	key1: 'value1',
	key2: 'value2',
};

delete obj.key1;
delete obj['key2'];
```

## Spread operator
It expands an object into a list of elements
```js
let address = {
	postalCode: '11011',
	city: 'Berlin',
}

address = { ...address, country: 'Germany' }

console.log(address)
>>>
{  postalCode: '11011',
  city: 'Berlin',
  country: 'Germany'
}
```

## Object destructure
```js
const weather = {
  sun: '☀️',
  sun_behind_small_cloud: '🌤️',
  sun_behind_cloud: '⛅',
  cloud: '☁️',
  cloud_with_lightning: '🌩️',
};

// the variable name must match the property name
// we can also rename it 
const { sun, cloud,  cloud_with_lightning: thunder} = weather;

// equals to
const sun = weather.sun
const cloud = weather.cloud
const thunder = weather.cloud_with_lightning
```
### Rest operator
rest operator can be used to collect more than one properties and store them in a single `object`.
```js
const { street, ...address } = {
  postalCode: '11011',
  street: 'Platz der Republik 1',
  city: 'Berlin',
};

console.log(street)
>>> 'Platz der Republik 1'

console.log(address)
>>> {postalCode: '11011', city: 'Berlin'}
```

## Objects with Method and this
* `this` in an object method represent the `object` itself
* **Avoid using arrow function** in object method.
```js
const gamer = {
    name: 'Dave',
    score: 0,
    incrementScore: function(){
		// "this" is same as "gamer"
        this.score++   
    }
}
```



## .hasOwnProperty() - Checking Whether a Key Exists
You can check whether a certain key exists in an object with the hasOwnProperty method.
```js
const obj = { greeting: 'hello world' };

obj.hasOwnProperty('greeting');
// => true

obj.hasOwnProperty('age');
// => false
```

## Looping Through an Object
* Objects are `not` designed to be ordered collections. 
* To avoid subtle errors, you should always assume the for...in loop visits the keys in an `arbitrary` order. 
* When iterating over a plain object, JavaScript follows this order:
- Integer keys: Iterated in `ascending` numeric order
- String keys: Iterated in the order they were inserted
- Symbol keys: Iterated in insertion order

```js
const obj = {
	b: 1, 
	1: 'one', 
	a: 2, 
	0: 'zero'
};

for (let key in obj) {
	console.log(key, obj[key]);
}
// 0
// 1
// b
// a
```


