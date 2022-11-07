# Express JS Using Method And Example

### 🔭 What is Express JS?
- Express JS is a fast, assertive, essential and moderate web framework of Node.js
- Express JS is a layer built on the top of the Node.js that helps manage a server and routes.
- Express JS It provides a robust set of features to develop web and mobile applications.
- Detail Explain: Special Session on Understanding The Server -[Milestone 10] {Gias Uddin Hasan}}

### 👯 Why use Express JS?
- i. Ultra fast I/o ii. Asynchronous and single threaded iii. MVC like structure iv. Robust API makes routing easy.
### 🤔 How/Where to Use Express JS ?
- 
- 
### 🤔 Who Uses  Node JS?
- 
- Every req in ExpressBoilerplate (Full Example)
List of Express JS:
- [serverStepByStep](#serverStepByStep)
- [ExpressBoilerplate](#ExpressBoilerplate)
- [RequestAndResponse](#RequestAndResponse)
- [Notes](#Notes)
- [ExpressJsInterviewQuestions](#ExpressJsInterviewQuestions)
- [Table](#Table)



### demo
<details>
<summary>
  <h3> Demo-(Click Me)</h3>
</summary>
<br >
	
```js

demo code

```
</details>

### serverStepByStep
<details>
<summary>
  <h3>server Step By Step-(Click Me)</h3>
</summary>
<br >
	
```js

/* 
=====Server step by step===
1. create folder (demo-server)
2. open cmd and type (npm init -y)
3. open folder and  create index.js (in your root folder যাতে server run করলে index.js দেখাতে পারে।)
4. install some package (npm i express cors nodemon dotenv jsonwebtoken mongodb)
5. open package.js 
 added ( "start": "nodemon index.js" ) in your scripts
 //Example:
  "scripts": {
    "start": "nodemon index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
6. then (npm start) in your terminal
	
// index.js
const express = require("express");
const cors = require("cors");
const { MongoClient, ServerApiVersion } = require("mongodb");
const app = express();
const Port = process.env.PORT || 5000;

app.use(cors());
app.use(express.json());

app.get("/", (req, res) => {
  res.send("Servant Network Server is Running");
});


app.listen(Port, () => {
  console.log(`Servant Network Server running on port ${Port}`);
});

//then go to mongodb and (create user and password)
// 
// check mongodb connected
const uri = `mongodb+srv://servantNetwork:jbTAlWrnJfp5NfFZ@cluster0.m1iwwru.mongodb.net/?retryWrites=true&w=majority`;
console.log(uri);
const client = new MongoClient(uri, {
  useNewUrlParser: true,
  useUnifiedTopology: true,
  serverApi: ServerApiVersion.v1,
});

async function run() {
  try {
    const servantCollection = client
      .db("servant-database")
      .collection("servants");

    const servants = {
      name: "text servant",
      email: "servant@gamil.com",
    };
    const result = await servantCollection.insertOne(servants);
    console.log(result);
  } finally {
  }
}
run().catch(console.dir);

```
</details>

### ExpressBoilerplate
<details>
<summary>
  <h3> Express Boilerplate-(Click Me)</h3>
</summary>
<br >
	
```js
//step 1 (express টা require করতে হবে)
const express = require("express");
//step 2 (express ta app এর ভিতর রাখতে হবে)
const app = express();
//step 3 (cors টা require করতে হবে)
const cors = require("cors");
app.use(cors());
//step 4:  middleware (post করার সময় autometic json এ convert করে দেই)
app.use(express.json())
// step 5: (port লাগবে কোন জায়গা server চলবে সেই জন্য)
const Port = process.env.Port || 5000;

//productsCollection দিয়ে data call করে আনা হল।
const productsCollection = require("./data/product.json");

//data get
app.get("/", (req, res, next) => {
  res.send("Now Server is Running.");
});

app.get("/allProducts", (req, res) => {
  res.send(productsCollection);
});

// get single data
app.get("/product/:id", (req, res) => {
  const id = req.params.id;
  const getSingleItem = productsCollection.find((p) => p.id == id);
  if (!getSingleItem) {
    res.send("item not found");
  }
  res.send(getSingleItem);
});

app.get("/category/:categoryName", (req, res) => {
  const name = req.params.categoryName;
  const getCategory = productsCollection.filter(p => p.category == name);
  console.log(getCategory)
  res.send(getCategory)
});

app.listen(Port, () => {
  console.log("Server is Running", Port);
});


```
</details>

### RequestAndResponse
<details>
<summary>
  <h3> Request And Response -(Click Me)</h3>
</summary>
<br >
	
```js

What is Request and Response?
Request: req(Method, Resoures, Headers, [content])
Response: res(Status Code, Headers, [content])

--Request(req) object?
The req object represents the HTTP request and has properties
i. request query string,
ii. parameters
iii. body
iv. HTTP headers, and so on
-----------
i. req.query
ii. params
console.log(req.params.name)
iii. body: Contains key value pairs of data submitted in the request body
app.post('/profile', function(req, res) => {
    console.log(req.body)
    res.json(req.body)
})

--Response (res) object?
The res object represents the HTTP response that an Express app
sends when it gets an HTTp request and has methods
i. res.send()
res.send({some: 'json'})
res.send('<p>some html</p>')

ii. res.json()
res.json(null)
res.json({user: 'tobi'})

iii. res.status(), res.sendStatus()
res.status(403).end()
res.status(400).send('Bad request')
res.status(404).sendFile('/absolute/path/to/404.png')

iv. res.set(), and so on
res.set('Content-type', 'text/plain')
res.set({
    'Content-type', 'text/plain',
    'Content-length', '123',
    Etag: '11234'
})

```
</details>







### Notes
<details>
<summary>
  <h3>Notes for Node js  (Click Me)</h3>
</summary>
<br >
  - Notes must be know every single part for interview 

```js

************Node js  Notes************
// free talk
১। JavaScript Backend(server site) এ use করা যাই। 
২। node.js er সাহায্যে node একটি runtime যেটা JavaScript Backend এ run করতে সাহায্যে করে।
৩। node js এর framework Express.js (node  এর code গুলো সহজে Express.js দিয়ে run করা হয়)
৪। এই Express.js  দিয়ে একটি server তৈরি করা যাই। 
যেইটা দিয়ে req আসবে res যাবে .
৫। cors একটা platform like: web, os and android এ কাজ করবে
	
	
	
	

************End Node Notes************
```
</details>
  
### ExpressJsInterviewQuestions
<details>
<summary>
  <h3>Express JS Interview Questions (Click Me)</h3>
</summary>
<br >
 must be know every single part for interview https://roadmap.sh/react
	
 ```js
************Express JS Interview Questions************
	
//Milestone: 9 React Router and States
//Module 55.5

	
	
	
	
	
	
	
	
	
  ************End Express JS Interview Questions************
 ```
</details>



### Table
<div class="overflow-x-auto">
  <table class="table w-full">
    <!-- head -->
    <thead>
      <tr>
        <th></th>
        <th>Questions</th>
        <th>Answer</th>
      </tr>
    </thead>
    <tbody>
      <!-- row 1 -->
      <tr>
        <th>1</th>
        <td> </td>
        <td> </td>
      </tr>
      <!-- row 2 -->
      <tr>
        <th>3</th>
        <td> </td>
        <td> </td>
      </tr>
       <!-- row 1 -->
      <tr>
        <th>4</th>
        <td> </td>
        <td> </td>
      </tr>
    </tbody>
  </table>
</div>



## 🌐 Socials: Connect with Emon Hossain!

[![Facebook Badge](https://img.shields.io/badge/Facebook-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://fb.com/emonhossain6) [![Linkedin Badge](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/emon007iu/) [![Twitter Badge](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/@emon_hossain7) [![Mail Badge](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:emon.hossain.wd@gmail.com)

<h4>❤️🤔 You can follow my Github and other social accounts 🤔❤️</h4>
<h2>❤️ Thank you very much! ❤️</h2>
