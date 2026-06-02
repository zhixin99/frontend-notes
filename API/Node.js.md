## Node.js
- Before Node.js came along in 2009, JavaScript was basically trapped inside the web browser (like Chrome, Safari, or Firefox), acting as the engine that made websites interactive.
- Node.js took that same JavaScript engine (specifically Google Chrome's V8 engine) and packed it into a standalone program.
- Node.js is an environment that allows us to write javascript in other places besides the browser. Because of Node.js, you can write JavaScript to run directly on your computer's operating system.

### Scenario A: Pure Frontend (No Node.js involved)
If your index.js file is hooked up to an index.html file like this:
```html
<script src="index.js"></script>
```
And you view it by double-clicking the HTML file to open it in Chrome, or by using the Live Server extension in VS Code...  

Is Node running it? **No**.   

Your computer is just using the **browser's built-in JavaScript engine** to read and execute the code. Node isn't doing any work here. This is traditional, old-school frontend development.

### Scenario B: Modern Development Tools (Node.js is running the show)
If you are working on a project where you have to open your terminal in VS Code and type a command like:
```
npm run dev

npm start

vite
```

And it gives you a local link like http://localhost:5173 to open in your browser...

Is Node running it? Yes, absolutely.

Even though you are looking at the final result in a web browser, Node.js is running a **mini web server** on your computer behind the scenes. Node is sitting in the background, watching your files in VS Code. 

While you are developing your **React app**, Node and Vite work together in the background to translate, bundle, and compile all your modern React code into standard HTML, CSS, and JS that any browser can easily read.


## Ceate a new Node.js API from scratch
1. Open the Directory in VS Code
2. Generate a package.json file
    - Open the built-in terminal in VS Code (Terminal > New Terminal).
    - Typing `npm init` in the terminal. The utility is running. Answer the questions and input the information.
    - Or we can type `npm init -y`, which tells npm to automatically answer "yes" to every single configuration question and build a default package.json file
    - We will get a package.json file like this
```json
{
  "name": "wild-horizons",
  "version": "1.0.0",
  "description": "a dataset of the planet’s most interesting places",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "author": "Tom Chant",
  "license": "ISC"
}
```
3. Enable ES Module Syntax
    - By default, Node.js expects the older CommonJS (require) syntax. To tell Node that you want to use modern import/export statements, you can open the package.json file in VS Code and add `"type": "module"` right under the "main" property.
    - The **ES Module approach** is the official, standardized way to split your JavaScript code into separate, reusable files and share code between them using the import and export keywords.
    - HTTP module allows data to be transferred over the HTTP protocol, so we can create servers, handle requests from clients, and provide responses to those requests. 
```json
{
  "name": "web-mini-projects",
  "version": "1.0.0",
  "main": "index.js",
  "type": "module",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  }
}
```

4. Create Your API File
    - In the VS Code file explorer, create a new file named server.js (or index.js).
    - import http from "node:http". `node:http` indicates that we are looking for a `node` module, not a javascript module that we created ourselves. 
```js
import http from 'node:http'
import { getDataFromDB } from "./database/db.js"

PORT = 8000

const server = http.createServer(async (req, res) => {
    
    const destination = await getDataFromDB()

    if (req.url === '/api' && req.method === 'GET') {
        res.setHeader("Content-Type", "application/json")
        res.statusCode = 200

        res.write("This is some data \n")
        // destination is a json, and we use JSON.stringify to convert it into json
        res.write(JSON.stringify(destination))  
        res.end("This is from the server", "utf8", () => {console.log("response end")})
    } else {
        res.setHeader("Content-Type", "application/json")
        res.statusCode = 404
        res.end(JSON.stringify({error: "not found", message: "The requested route does not exist"}))
    }

})

// Keep an eye on port 8000. The moment a request hits that doorway, fire off this exact response
server.listen(PORT, () => console.log("Connected on port."))
```
<img src="../Images/HTTPAPI.png" width="400">

5. Start Your API Server
     - Go back to your VS Code terminal and Run your file using Node, You should instantly see your terminal log:
🚀 API Server is running locally at http://localhost:8000
```bash
node server.js
```

6. Test Your New API!
    - Now that Node is running a mini web server on your machine, open your web browser or an API client and navigate to: http://localhost:8000/api/destinations
    - You will see your array of destinations printed cleanly on the screen as a true JSON `payload`. Whenever you want to turn the server off, just hit Ctrl + C in your VS Code terminal.

## port
- There are 65,535 available **ports** on a computer. A port is a virtual, numbered `doorway` inside your computer’s operating system that allows specific programs to send and receive data without bumping into each other. 
- When you see an address like http://localhost:3000  while developing, you are looking at two pieces of information:
    - localhost: This is the IP address. It tells the computer to look at itself (IP address 127.0.0.1).
    - 3000: Tells the computer to hand this specific web traffic over to the exact Node.js or Vite process running in your terminal.
- port 8000 is one of the most popular "alternative" ports used by developers to `run and test web` applications locally on their computers. Just like ports 3000 or 5173, port 8000 is a safe, `unassigned` virtual doorway that developers use so they don't interfere with standard internet traffic (like your normal web browsing, which uses ports 80 and 443).

## response object method & property
- res.write(): it allows us to send something to the client
- res.end(): always end the stream with res.end. 
    - We can ignore the utf8 because it is the default format of data.
    - We can also put a call back function inside.
    - We can also just `leave it empty`, make it simply the end of the stream. 
- res.setHeader(): pass in two strings to set the Content-Type. When you call res.setHeader('Content-Type', 'application/json'), you are telling the recipient's browser or API client exactly **what kind of file** you are sending back before you actually deliver the data.
- res.statusCode: this is a `property` not method!

## request object method 
- req.url: it gives us the endpoints and query string, excluding the basic URL. 
- req.headers: it returns an object of all the request header information
    - We can get the host url by  `req.headers.host`
```
{
  accept: '*/*',
  'accept-encoding': 'gzip, deflate',
  'accept-language': '*',
  connection: 'keep-alive',
  host: 'localhost:8000',
  'sec-fetch-mode': 'cors',
  'user-agent': 'node'
}
```
- req.method: it returns GET / POST / PUT .....

## query parameter
- We can call the URL constructor to create a new instance of URL. It has 2 parameters: the `Relative URL`, and `basic URL`.
    - Don't forget to add the http protocal to the basic URL.
    - This URL object has a property called `searchParams`, and this is what we need.
- Then we can get the **query string object** using the `Object.fromEntries` method. 
- Pay attention to the type of the value we got from the query parameter. The true / false can be in the `string` format. The number can also be in the `string` format. 
```js
import http from 'node:http'

const server = http.createServer((req, res) => {

    const urlObj = new URL(req.url, `http://${req.headers.host}`)

    const queryObj = Object.fromEntries(urlObj.searchParams)

    console.log(urlObj)

    console.log(queryObj)

})

server.listen(8000, () => console.log('Server listening on port 8000'))


>>> URL {
    href: 'http://localhost:8000/api?name=tom&country=uk',
    origin: 'http://localhost:8000',
    protocol: 'http:',
    username: '',
    password: '',
    host: 'localhost:8000',
    hostname: 'localhost',
    port: '8000',
    pathname: '/api',
    search: '?name=tom&country=uk',
    searchParams: URLSearchParams { 'name' => 'tom', 'country' => 'uk' },
    hash: ''
}

>>> { name: 'marcel', country: 'fr', is_open_to_public: 'true' }
```


```js
import http from 'node:http'
import { getDataFromDB } from './database/db.js'
import { sendJSONResponse } from './utils/sendJSONResponse.js'
import { getDataByPathParams } from './utils/getDataByPathParams.js'
import { getDataByQueryParams } from './utils/getDataByQueryParams.js'

const PORT = 8000

const server = http.createServer(async (req, res) => {
  const destinations = await getDataFromDB()

  const urlObj = new URL(req.url, `http://${req.headers.host}`)

  const queryObj = Object.fromEntries(urlObj.searchParams)

  if (urlObj.pathname === '/api' && req.method === 'GET') {
    
    let filteredData = getDataByQueryParams(destinations, queryObj)
    sendJSONResponse(res, 200, filteredData)

  } else if (req.url.startsWith('/api/continent') && req.method === 'GET') {

    const continent = req.url.split('/').pop()
    const filteredData = getDataByPathParams(destinations, 'continent', continent)
    sendJSONResponse(res, 200, filteredData)

  } else if (req.url.startsWith('/api/country') && req.method === 'GET') {

    const country = req.url.split('/').pop()
    const filteredData = getDataByPathParams(destinations, 'country', country)
    sendJSONResponse(res, 200, filteredData)

  } 
  
  else {

    res.setHeader('Content-Type', 'application/json')
    sendJSONResponse(res, 404, ({
      error: "not found",
      message: "The requested route does not exist"
    }))   

  }
})

server.listen(PORT, () => console.log(`Connected on port: ${PORT}`))
```

```js
export const getDataByQueryParams = (data, queryObj) => {

  const { continent, country, is_open_to_public } = queryObj

  if (continent) {
    data = data.filter(destination =>
      destination.continent.toLowerCase() === continent.toLowerCase()
    )
  }

  if (country) {
    data = data.filter(destination =>
      destination.country.toLowerCase() === country.toLowerCase()
    )
  }

    // use JSON.parse to transfer the string into a boolean
    // make sure the string is lowercase
  if (is_open_to_public) {
    data = data.filter(destination =>
      destination.is_open_to_public === JSON.parse(is_open_to_public.toLowerCase())
    )
  }

  return data
} 
```

```js
export const sendJSONResponse = (res, statusCode, payload) => {
    res.setHeader('Content-Type', 'application/json')
    // CORS 
    res.setHeader('Access-Control-Allow-Origin', '*')
    res.setHeader('Access-Control-Allow-Methods', 'GET')

    res.statusCode = statusCode
    res.end(JSON.stringify(payload))
}
```


