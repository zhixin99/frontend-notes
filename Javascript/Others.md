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