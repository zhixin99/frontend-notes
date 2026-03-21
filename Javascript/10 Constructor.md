# Constructors
* It is a machine that stores a template of object and can give you new instance of `object`.
* It should have `Uppercase first letter`.
* It is actually a kind of `function`, so we need bracket to invoke it. 

## Build Constructor functions
* We `uppercase the first letter` of the function name to show it is a constructor
```js
function Gamer(name, score){
    this.name = name
    this.score = score
    this.incrementScore = function(){
    	this.score++
    }
}

const dave = new Gamer('Dave', 0)
dave.incrementScore()
console.log(dave)
>>> Gamer {name: 'Dave', score: 1}
```

## Error() Constructor
* This constructor gives us an ability to custom error messages. 
* Put the custom message in the parenthesis of the new instance of Error. 
```js
function checkUsername(userName) {
    if (userName) {
        console.log(userName)
    } else {
        console.log(new Error('No username provided'))
    }
}

checkUsername()
>>> Error: No username provided    
// This is just a string
```

## throw the error
Different from just console.log, `throw` makes the whole codes stop immediately once there's an error
```js
function test() {
    throw new Error('Oops')
    console.log('B');     // never run
}

test()
console.log("C") // never run

// It means the whole codes is breaking down
>>> !Error: Oops    
```

## try/catch the error
```js
function addTouristSurcharge(payment) {
    if (typeof payment === 'number') {
        console.log(payment + 10)
    } else {
        throw new ReferenceError('payment is not a number')
    }
}

addTouristSurcharge('60')
console.log("haha")   // the whole program breaks down and it will never run

>>> !ReferenceError: payment is not a number
```
* If we want the `flow` continue to run after we throw an error (instead of the whole code break down), we should use try/catch.  
* It will jump out of try immediately after the error is thrown, find the nearest catch, and run the catch.  
```js
function addSurcharge(payment){
    try {
        if (typeof payment === 'number'){
            console.log(payment + 10)
        } else {
            throw new ReferenceError('Payment is not a number');
        }
    } catch (err) {
      console.error('Error: ' + err)
    }
}

addSurcharge('10')
console.log("haha")

>>>!Error: ReferenceError: payment is not a number
>>> haha
```

## try...catch...finally 
```js
fetch("/data")
	.then(result => {
		// fulfilled
	})
	.catch(error => {
		// rejected
	})
	.finally(() => {
		// always runs
	})
```

## Date() constructor   
* No arguments → current day, date and time (in your time zone). It is an `object`.
```js
const now = new Date()

// It is an object
console.log(now)
>>> 2025-12-19T07:22:54.426Z 

// Convert it to string
console.log(now.toString())
>>> Thu Jul 27 2023 13:54:08 GMT+0100 (British Summer Time)
```

### Accessing Date components
```js
getTime(); // returns the UNIX timestamp in milliseconds

getFullYear(); // Get the year (4 digits)
getMonth(); // Get the month, from 0 to 11.
getDate(); // Get the day of month, from 1 to 31.
getHours(); // Get the hour in a 24 clock, from 0 to 23
getMinutes(); // Get the minutes, from 0 to 59
getSeconds(); // Get the seconds, from 0 to 59
getMilliseconds(); // Get the milliseconds, from 0 and 999
getDay(); // Get the day of week, from 0 (Sunday) to 6 (Saturday).
```

### Format date and time
```js
var d = new Date();
d.toLocaleString();       // -> "2/1/2013 7:37:08 AM"
d.toLocaleDateString();   // -> "2/1/2013"
d.toLocaleTimeString();  // -> "7:38:05 AM"
```

## Update the time every second
```js
function doDate()
{
    const now = new Date()
    document.getElementById("todaysDate").innerHTML = now;
}

setInterval(doDate, 1000);
```

## Data type constructors
```js
String()
Number()
Array()
Object()
Boolean()
```











### 2. Unix timestamp(number) → interpreted time
If a number is passed in, this will be interpreted as a timestamp. A timestamp is an `integer number` representing the number of milliseconds that has passed since **1 January 1970 UTC+0**.
```js
const epoch = new Date(0);
// Thu Jan 01 1970 01:00:00 GMT+0100 (Central European Standard Time)

const another = new Date(1749508766627);
// Tue Jun 10 2025 00:39:26 GMT+0200 (Central European Summer Time)
```
#### supplying individual date and time components
```js
// month starts from 0;  0 or 12 both represent Jan
const date1 = new Date(95, 11, 17);
// Creates Date for Dec 17 1995 00:00 if your local timezone is equivalent to UTC.

const date2 = new Date(2013, 12, 5, 13, 24, 0);
// Creates Date for Jan 5 2014 13:24 if your local timezone is equivalent to UTC.
// Equals to this
const date2 = new Date(2014, 0, 5, 13, 24, 0);
```

### 3. ISO 8601 timestamp (string) → interpreted time
```js
const dateFromString = new Date("2025-12-19T08:30:00Z");

console.log(dateFromString.toISOString());
// "2025-12-19T08:30:00.000Z"
```

Format:
```
YYYY-MM-DDTHH:mm:ssZ
```

Example:  
```
2025-12-19T10:00:00+02:00
2025-12-19T08:30:00Z
```
- +02:00 is the timezone offset. means 2 hours ahead of greenwich mean time(UTC)
- T is a literal letter, separating date from time
- Z is a literal letter, representing UTC time
- +/-HH:mm is an offset 

Change from `Date object` to ISO format: When working with Dates in JavaScript, always use an ISO 8601 timestamp when converting from a string to a Date.  
```js
new Date().toISOString()
```

### 4. Date object → copy time value
An existing date object can also be used as a `constructor argument`. This makes a copy of the existing Date object with the same date and time.
```js
const t1 = new Date();
const t2 = new Date(t1);
// Values of t1 and t2 will be the same.
// t1 and t2 are different objects
```


## Comparing Dates
Greater than (>) and greater than or equals (>=) as well as less than (<) and less than or equals (<=) can be used directly between two dates or a date and a number.   
Dates cannot be compared using equality (==, and ===), but the result of `.getTime()` can.

## Change Dates
```js
const date = now Date();
date.setDate(29);
// there was no February 29th in 2025.

d.setDate(d.getDate + 4)
// 4 days from now
```

Example: The function will receive first argument as appointment time and second argument of object of some options. You have to update the appointment according to the options in the object and return the new appointment date. The options object could have multiple options.

```js
export function updateAppointment(timestamp, options) {
  const date = new Date(timestamp);
  if (options.year !== undefined) {
    date.setFullYear(options.year);
  }
  if (options.month !== undefined) {
    date.setMonth(options.month); 
  }
  if (options.date !== undefined) {
    date.setDate(options.date);
  }
  if (options.hour !== undefined) {
    date.setHours(options.hour);
  }
  if (options.minute !== undefined) {
    date.setMinutes(options.minute);
  }

  return {
    year: date.getFullYear(),
    month: date.getMonth(), 
    date: date.getDate(),
    hour: date.getHours(),
    minute: date.getMinutes(),
  };
}
```
## Difference
```js
const dateA = new Date('2022-12-12T09:20:00.000');
const dateB = new Date('2022-12-18T08:30:00.000');

console.log(dateA - dateB)

>>> -515400000 // millisecond format
```


## Inheritance
Inheritance is a way to create parent-child relationships between classes. The child class (sometimes referred to as a subclass) has access to the behavior and data defined by the parent class (sometimes referred to as a superclass).
```js
class Pet {
  constructor(name) {
    this.name = name;
  }

  introduce() {
    console.log(`This is my pet, ${this.name}.`);
  }
}

// Dog is the child class.
// The extends keyword in the child class declaration establishes a relationship with the parent class through the prototype chain.
class Dog extends Pet {}  

const dog = new Dog('Otis');
dog.introduce();
// => This is my pet, Otis.
```
prototype chain
```
dog → Dog.prototype → Pet.prototype → Object.prototype → null
```
```js

// objA.isPrototypeOf(objB): is objA on the prototype chain of objB
Dog.prototype.isPrototypeOf(dog); // => true
Pet.prototype.isPrototypeOf(dog); // => true
Pet.prototype.isPrototypeOf(Dog.prototype); // => true

Pet.prototype.hasOwnProperty('introduce'); // => true
Dog.prototype.hasOwnProperty('introduce'); // => false
dog.hasOwnProperty('introduce'); // => false
```


As with any class in JavaScript, subclasses can inherit from Error to create Custom errors by using the extends keyword. The instanceof syntax will check if the error caught is an instance of a particular subclass of Error.
```js
class CustomError extends Error {}

try {
  // ... Code that may throw an error
} catch (error) {
  if (error instanceof CustomError) {
    console.log('The error thrown is an instance of the CustomError');
  }
}
```




## Class syntax
It is not hoisted
```js
class Gamer {
	constructor(name, score){
		this.name = name
		this.score = score
	}
	incrementScore(){
		this.score++
	}
}

const dave = new Gamer('Dave', 0)
dave.incrementScore()
```






array is also an object
```js
// array
const arr = [1, 2, 3];
arr.foo = 'hello';

console.log(arr.foo); // "hello"
```
function is also an object
```js
//function
function f() {}
f.x = 42;

console.log(f.x); // 42
```





```js
Car.prototype.startEngine = function () {
  this.engineRunning = true;
};
```
startEngine is a property name  
startEngine -> function () {this.engineRunning = true;} is the `method`

Example:   
```js
function Tiger(name, weight){
    // field
    this.name = name;
    this.weight = weight;
}

// prototype
Tiger.prototype.bark = function(){
    console.log(this.name + ": wahwahwah");
}

Tiger.prototype.eat = function(foodWeight){
    this.weight += 0.1 * foodWeight
};


const tigerA = new Tiger("tigerA", 100);
tigerA.bark()
tigerA.eat(10)

tigerA.bark()
tigerA.eat(50)

tigerA.bark()
tigerA.eat(20)

console.log(tigerA.weight)
```



## instanceof
Check whether the object come from the class 
```js
class Beverage {
  // ...
}

// The Coffee class is a child of the Beverage class.
class Coffee extends Beverage {
  // ...
}

const java = new Coffee();

java instanceof Coffee;
// => true

java instanceof Beverage;
// => true
```

## The in operator
The in operator returns whether the first operand is a property of the second operand. It does not check that the property has a defined value. A property set to undefined will still be detected by in.   

`in` will return true for `inherited` properties and methods.
```js
class Coffee {
  constructor() {
    this.temperature = 'hot';
    this.isDarkMatter = undefined;
  }

  coolDown() {
    this.temperature = 'warm';
  }
}

const espresso = new Coffee();

'temperature' in espresso;
// => true

'color' in espresso;
// => false

'isDarkMatter' in espresso;
// => true
```

## Object.hasOwn() 
The Object.hasOwn() method returns whether the specified object owns the given property (it is not inherited or a method).
```js
class Coffee {
  constructor() {
    this.temperature = 'hot';
  }

  coolDown() {
    this.temperature = 'warm';
  }
}
const cappuccino = new Coffee();

Object.hasOwn(cappucino, 'temperature');
// => true

Object.hasOwn(cappucino, 'constructor');
// => false

Object.hasOwn(cappucino, 'coolDown');
// => false
```

## Compare the error
we `throw` the error, not `return` the error, so we can't use error == xxx to compare.
the error should be an instance of a class of error. we can use `instanceof`.  

Example:   

Now that your machine can detect errors, you will implement a function `monitorTheMachine` that takes an argument actions. actions is an `object` that has 4 properties:
- check: a function. Checks the temperature of the machine. It may throw various errors.
- alertDeadSensor: a function. Alerts a technician that the temperature's sensor is dead.
- alertOverheating: a function. Will turn on a warning light on the machine.
- shutdown: a function. Will turn off the machine.

The monitorTheMachine(actions) function should internally call check(). If that passes, the function should not return anything. If that throws an error, different behaviour is expected:
- ArgumentError: all the alertDeadSensor function.
- OverheatingError: If the temperature is less than 600 °C, turn on the warning light by calling the alertOverheating function. If the temperature exceeds 600 °C, the situation is critical, so call the shutdown function.
- (anything else): rethrow the error
```js
export class ArgumentError extends Error {}

export class OverheatingError extends Error {
  constructor(temperature) {
    super(`The temperature is ${temperature} ! Overheating !`);
    this.temperature = temperature;
  }
}

export function monitorTheMachine(actions) {
  try{
    actions.check()
  } catch(error){
    if(error instanceof ArgumentError){
      actions.alertDeadSensor();
    }
      
    else if (error instanceof OverheatingError){
      if(error.temperature <= 600){
        actions.alertOverheating();
      }
      else{
        actions.shutdown();
      }
    }
      
    else{
      throw error;
    }
  }
}
```