# API
* Application Programming Interface
* An API is a tool that can connect your program with someone else's program 
* The server holds the API (exposed endpoint), and we can access for getting data. 

## HTTP request component
- HTTP is a protocol(an agreed and standard way of doing something) for determinging how the hypertext should be transferred over the internet
- So all the data transferred between the client and server should be in the form of `strings`!!!
```
JSON.stringify(object)
```

### Path
It is the URL that the client is sending the request to. The server is living in the URL address. https://apis.scrimba.com/jsonplaceholder/posts. Once we click the link, the `browser` will send a `GET request` to the URL. 

```
Full URL = Base URL + Endpoint + Query String
```

- **Base URL / Domain / Host**: This will not change no matter what kind of resources you are getting from the API
- **Endpoint**: Specific resource that you want to get. 
    - `URL parameter`: /bike/:id
    - `Nested resources`: /bike/reviews; /posts/comments; /albums/photos
- **Query string**: How do I want to filter, sort, or modify the results coming back?

```
http://example.com /api/v1/users/ 42 /orders ?sort=desc&limit=5
─────────────────  ─────────────  ──  ──────  ──────────────────
    Domain             Path       │   Nested      Query String
                           URL Parameter
```

### Method
Method tells the server what is your intention with the request / what kind of request it is
* GET 
* POST - Add new data to the server
* PUT - Update existing data
* DELETE


### Header
* **Headers**: meta data about the request like what kind of browser is sending the request 
    * authentication tokens
    * body information
    * client information
- Content-Types(Mime Types): 
    - application/json
    - text/html
    - text/css
    - application.javascript
### Body
* **Body**: The data we want to send back to server. Only for POST and PUT. 




## API coding
### GET
```js
// default is GET request, we can ignore the {method: "GET"}
fetch("https://dog.ceo/api/breeds/image/random", {method: "GET"})
    // parse the response from JSON into Javascript
    // throw an error if the status is not ok, so the whole coding will not break down
    .then(response => {
        if (!res.ok) {  
            throw new Error("Failed to get the data from API") 
        } 
        return response.json()
    })
    .then(data => console.log(data))
    .catch(err => console.err(err))
```

### POST
```js
const options = {
    method: "POST",
    headers: {
        "Content-Type": "application/json"     // tell the server that we are sending data in a json format
    }
    body: JSON.stringify({
        title: "Buy Milk",
        completed: false      // use JSON.stringify to change js object to JSON
    })
}

fetch("https://apis.scrimba.com/jsonplaceholder/todos", options)
    .then(res => res.json())
    .then(data => console.log(data))
```


### Server response code
- 200: ok   
- 300: forbidden    
- 404: Server can not Found
- 500: Internal Server Error 
```js
fetch("https://api.coingecko.com/api/v3/coins/dogecoins32423")
    .then(res => {
        // check the 3 digits server response code
        console.log(res.status)  
        return res.json()
    })
```



















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


## GraphQl
* GraphQL stands for Graph Query Language.
    * The "QL" part: This is the actual language you use to write that "note" to the server (the part you saw in the Dirk POST body).
    * The "Runtime" part: It is also a server-side engine that executes those queries using a type system you define for your data.
* Most browsers and servers have a limit on how long a URL can be (usually around 2,000 characters). A complex query with nested products, prices, images, and brand details can easily exceed that limit. If they used GET, the URL would "break" or get cut off. 
* In GraphQL, this logic is a structured `JSON object`. It’s much "cleaner" to send that structure in a `POST body` than to try and cram it into a URL string.
* I am POSTing a question to the server, and the server is giving me the answer.

