# Async
`Promise` and `callback` functions are 2 methods of doing asynchronous codes. 

## Callback functions
A callback function is a function that is passed into another function as a parameter and executed later.

* If we add a parenthesis to the handleClick() here, this function will run immediately. 
* We pass the content of the function by its name, so `at sometime in the future` when it is appropriate (when it is clicked), addEventListener is able to call the function handleClick
```js
function handleClick() {
    fetch("https://apis.scrimba.com/deckofcards/api/deck/new/shuffle/")
        .then(res => res.json())
        .then(data => console.log(data))
}

document.getElementById("new-deck").addEventListener("click", handleClick)
```

We have used lots of callback functions already, including:
* .filter()
* setTimeout()
* addEventListener()

## Promise
* A Promise is an `object` that take a bit of time to finish but will eventually finish running. It stands for a future result of an async operation.
* The `object` that we return from the `fetch` is a `promise`
* Pending => Resolved or Rejected
* We can't directly log out the promise
```js
const data = fetch("https://apis.scrimba.com/deckofcards/api/deck/new/shuffle/")

console.log(data)
>>> Promise
```
* It has a method called `.then()`

### promise chaining
* .then() works on a promise and it also returns a promise
* promise is passed as a `parameter` (res) to the `callback function` of the .then()

```js
const promise = fetch("https://apis.scrimba.com/deckofcards/api/deck/new/shuffle/")

const promise2 = promise.then(res => res.json())

console.log(promise2)
>>> Promise
```
* In a promise chaining, we can simplify it into 
```js
fetch("https://apis.scrimba.com/deckofcards/api/deck/new/shuffle/").then(res => res.json())
```
* Whatever the first callback function `returns`, is what the next .then() will `receives` to its callback function  as the parameter. 
* Console.log() will not pass anything; Only the thing that is `returned` will be passed down. 
```js
fetch("https://apis.scrimba.com/bored/api/activity")
    .then(function(res) {
        return "Hello"
    })
    .then(function(whatever) {
        console.log(whatever)
        return "World"
    })
    .then(function(another) {
        console.log(another)
    })

>>> "World"
```

### Fulfilled => .then()
* It lets the `other codes run first` before the response from the fetch request come back from the server
* .then() is the part that will run if the promise is `fulfilled`
```js
console.log("The first console log")

fetch("https://dog.ceo/api/breeds/image/random")
    .then(response => response.json())
    .then(data => console.log(data))

console.log("The second console log")

>>> 
The first console log
The second console log
{message: 'https://images.dog.ceo/breeds/affenpinscher/n02110627_12003.jpg', status: 'success'}
```

### Rejected => .catch()
* It runs only if the Promise is rejected
* It receives an error as the **parameter**, it can be `error` or `err` or whatever we want to call it. 
```js
fetch("/data").catch(error => {console.log("something wenr wrong!")});
```

If there's an error and the .catch() is not set up, js will give us a warning like this
```js
unhandledrejection PromiseRejectionEvent
```

We can directly console log the `error itself`
```js
fetch("/data")
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err))
```

## `async` & `await`  
* await does not change how Promises work — it only makes the code look synchronous.  
* `async` goes before the function
* `await` goes before a method / a function that `returns a promise`
```js
async function getWeather() {
	const res = await fetech("")
	const data = await res.json()
	console.log(data)
}
```
* Use async in the `callback function`
```js
navigator.geolocation.getCurrentPosition(async position => {
    const res = await fetch(`https://apis.scrimba.com/openweathermap/data/2.5/weather?lat=${position.coords.latitude}&lon=${position.coords.longitude}&units=imperial`)
    if (!res.ok) {
        throw Error("Weather data not available")
    }
    const data = await res.json()
    const iconUrl = `http://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`
    document.getElementById("weather").innerHTML = `
        <img src=${iconUrl} />
    `
});
```
* Await can also be used at the `top level of a module`, without the need of a function
```html
<script src="index.js" type="module"></script>
```
```js
const res = await fetch("https://apis.scrimba.com/unsplash/photos/random?orientation=landscape&query=nature")
const data = await res.json()
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
Change it into `async` ... `await`
```jsx
try {
	res = await fetch("/data")
	if (!res.ok) {
		throw New Error("Something went wrong")
	}
	data = await res.json()
} catch (err) {
	console.error(err)
} finally {

}
```
