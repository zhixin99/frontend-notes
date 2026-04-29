# API
* Application Programming Interface
* An API is a tool that can connect your program with someone else's program 
* The server holds the API (exposed endpoint), and we can access for getting data. 

## HTTP request component
HTTP is a protocol(an agreed and standard way of doing something) for determinging how the hypertext should be transferred over the internet

* **Path(URL)**: It is the URL that the client is sending the request to. / The server is living in the URL address. 
    * Base URL: This will not change no matter what kind of resources you are getting from the API - `https://apis.scrimba.com/jsonplaceholder`
    * Endpoint: Specific resource that you want to get. We should only use `noun`, for exmaple **/posts**
    * Full URL: https://apis.scrimba.com/jsonplaceholder/posts. Once we click the link, the `browser` will send a `GET request` to the URL. 

* **Method**: tell the server what is your intention with the request / what kind of request it is
    * GET 
    * POST - Add new data to the server
    * PUT - Update existing data
    * DELETE
* **Body**: The data we want to send back to server. Only for POST and PUT. 
* **Headers**: meta data about the request like what kind of browser is sending the request 
    * authentication tokens
    * body information
    * client information


## Client and server
* Client: Any device that makes a `request` of to get data **(resource)** from somewhere
    * HTML page
    * JSON 
    * Image file
* Server: A computer. It accepts requests from clients, and `response` to that request

## Server response code
200: ok   
300: forbidden    
404: Server can not Found
500: Internal Server Error 
```js
fetch("https://api.coingecko.com/api/v3/coins/dogecoins32423")
    .then(res => {
        // check the 3 digits server response code
        console.log(res.status)  
        // check if the status is ok
        console.log(res.ok)  
        return res.json()
    })
```

## GET
```js
// default is GET request
fetch("https://dog.ceo/api/breeds/image/random")
    // parse the response from JSON into Javascript
    .then(response => response.json())
    .then(data => console.log(data))
```
Specify the method of the request
```js
fetch("https://apis.scrimba.com/jsonplaceholder/todos", {method: "GET"})
```
## POST
```js
const options = {
    method: "POST",

    // tell the server that we are sending data in a json format
    headers: {
        "Content-Type": "application/json"
    }

    // use JSON.stringify to change js object to JSON
    body: JSON.stringify({
        title: "Buy Milk",
        completed: false
    })
}

fetch("https://apis.scrimba.com/jsonplaceholder/todos", options)
    .then(res => res.json())
    .then(data => console.log(data))

// it means the id of the new data is 201
>>> {title: 'Buy Milk', completed: false, id: 201}
```

## Error handling
```js
fetch("https://api.coingecko.com/api/v3/coins/dogecoins32423")
    .then(res => {
        console.log(res.status)  // check the 3 digits server response code
        console.log(res.ok)  // check if the status is ok
        return res.json()
    })
    .then(data => {
        console.log(data)
    })
    .catch(err => console.error(err)) 
  
>>> 404
>>> false
>>> {error: 'Could not find coin with the given id'}   // This is not an error and our .catch() never runs
```
* To catch the error, we can improve it 
```js
fetch("https://api.coingecko.com/api/v3/coins/dogecoins32423")
    .then(res => {
        if (!res.ok) {
            throw new Error("Failed to get the data from API")
        } 
		return res.json()
      })
    .then(data => {
        console.log(data)
    })
    .catch(err => console.error(err)) 
```
Do something when there's an error: 
* Have a default solution even if the .then() throws an error: For example, we can set up a default background image if we can't get access to the image from the API. 
* Report the error to some kind of service 

## API lists
### <a href="https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API/Using_the_Geolocation_API#getting_the_current_position" >Geolocation API</a>

```js
// A callback function that takes a GeolocationPosition object as its sole input parameter.
navigator.geolocation.getCurrentPosition((position) => {
  doSomething(position.coords.latitude, position.coords.longitude);
});
```
### <a href="https://openweathermap.org/current?collection=current_forecast#geo" >OpenWeather API</a>
### <a href="https://imgflip.com/api" >Meme Generator API</a>

## Architectures
`GraphQL` and `REST` are two completely different architectures for how a client talks to a server.


| Feature | REST | GraphQL |
| :--- | :--- | :--- |
| **Endpoints** | Multiple (e.g., `/products`, `/categories`, `/prices`) | **Single** (usually just `/graphql`) |
| **Data Control** | The **Server** decides what data you get. | The **Client** (you) decides what data to return. |
| **Payload Size** | Often "heavy" (returns every field in the database). | **"Lean"** (you only request the specific fields you need). |
| **Versioning** | Hard (requires new URLs like `/v1/` or `/v2/`). | **Easy** (just add new fields to the existing schema). |

## REST
* REST (REpresentational State Transfer) is a set of architectural guidelines.
* REST is a `design pattern` to provide a standard way for clients and servers to communicate with each other. 
### Princile of REST
1. Client & Server seperation
* A RESTful API is a `client side fetching`. The server isn't responsible to figure out how to display the data; It just send data (JSON in most cases) to the client and let the client itself to render the data. 
    * Client: Request JSON data. 
    * Server: Send JSON data to client.
* If we are not adhering to the REST
    * Client: Navigate to a website in a browser.
    * Server: `Build HTML page with data` and send them back. It's **server side rendering.** 
    
2. Statelessness: It forgets the interaction after the response is sent.

3. Accessing resources: There's a standard way of setting the endpoints.

### Resourses
* /bike
* `URL parameter`: 
    * /bike/:id
* `Nested resources`: 
    * /bike/1/reviews
    * /posts/1/comments
    * /albums/1/photos
    * /users/1/albums
    * /users/1/todos
    * /users/1/posts
* `Query string`: /bikes/?type=mountain&brand=nike

![alt text](../Images/Nested-resources.png)

## GraphQl
* GraphQL stands for Graph Query Language.
    * The "QL" part: This is the actual language you use to write that "note" to the server (the part you saw in the Dirk POST body).
    * The "Runtime" part: It is also a server-side engine that executes those queries using a type system you define for your data.
* Most browsers and servers have a limit on how long a URL can be (usually around 2,000 characters). A complex query with nested products, prices, images, and brand details can easily exceed that limit. If they used GET, the URL would "break" or get cut off. 
* In GraphQL, this logic is a structured `JSON object`. It’s much "cleaner" to send that structure in a `POST body` than to try and cram it into a URL string.
* I am POSTing a question to the server, and the server is giving me the answer.

