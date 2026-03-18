# Others

## Function setTimeout - set the delay
The time is in milliseconds 
```js
setTimeout(
    function(){
        console.log("Hello. world!")
    }, 
    3000
)
```

## Function setInterval - run the function every xxx milliseconds
```js
setInterval(getCurrentTime(), 1000)
```

## clearInterval()
The clearInterval() method of the Window interface **cancels** a timed, repeating action which was previously established by a call to setInterval().

## Local storage
```js
// store   key     value
localStorage.setItem("name", "Jean");

// get the item
const name = localStorage.getItem("name");
console.log(name)
>>> name

// clear the storage
localStorage.clear()
console.log(name)
>>> null
```
We can only store  `string` as the value
```js
myLeads = ["11","aa","bb"]
localStorage.setItem("myLeads", JSON.stringify("myLeads"))
```


## UUID
```js
import { v4 as uuidv4 } from 'https://jspm.dev/uuid';
console.log(uuidv4());
```