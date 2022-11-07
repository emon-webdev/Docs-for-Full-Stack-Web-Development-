# MongoDB Using Method And Example

### 🔭 What is MongoDB?
- 
### 👯 Why use MongoDB?
- 
###  🤔 How to Use?
- 

- Every req in MongoDBBoilerplate (Full Example)
List of Express JS:
- [initialSetUp](#initialSetUp)
- [ExpressBoilerplate](#ExpressBoilerplate)
- [MongoDBBoilerplate](#MongoDBBoilerplate)
- [CrudOparetion](#CrudOparetion)
- [DotEnv](#DotEnv)
- [Notes](#Notes)
- [MongoDBInterviewQuestions](#MongoDBInterviewQuestions)
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


### initialSetUp
<details>
<summary>
  <h3> initialSetUp -(Click Me)</h3>
</summary>
<br >
	
```js


১। mongodb atlas data host korte dai pore data niya kaj korte pari
2.mongodb connect korar jonno (URI) thakbe 
=>const uri = ;
3. mongodb oi URI er jonno ekta Client dei jaite oi URI (update, post, get, delete) korte pari and URI pass korte hobe
=> const client = new MongoClient(uri);
4. Sei client ke Connect kora and Database er kaj async kaj
async function run() {
  await client.connect();
}
5. app.use(express.json())
6. 

0. npm install mongodb
1. create New Project (copy user and password)
2. Database > Connect > connect your application copy (include full drive) paste index.js 
//
const { MongoClient, ServerApiVersion } = require('mongodb');
const uri = "mongodb+srv://GeniusCar:<password>@cluster0.nftlnia.mongodb.net/?retryWrites=true&w=majority";
const client = new MongoClient(uri, { useNewUrlParser: true, useUnifiedTopology: true, serverApi: ServerApiVersion.v1 });
client.connect(err => {
  const collection = client.db("test").collection("devices");
  // perform actions on the collection object
  client.close();
});
3. Remove this and create async function
client.connect(err => {
  const collection = client.db("test").collection("devices");
  // perform actions on the collection object
  client.close();
}); 
4. create async function (follow mongodb crud find many)
async function run(){
    try{
        //4.1 create collection 
const serviceCollection = client.db("geniusCar").collection(services);
    }
    finally{

    }
}
run().catch(error => console.error(error))
5. Database > collections > create database same name 
client.db("geniusCar").collection("services");
database name (geniusCar)
collection(services)
6. Backend data load করতে api lagbe
app.get('/services', async(req, res) => {

    })
7. query কারে কারে find করতে চাই ( )
 const query = { runtime: { $lt: 15 } };

৮। সব গুলাকে find করতে চাইলে empty object দিতে হবে।

const query = { };
৯। data sort করতে options use করে। 
  const options = {
      // sort returned documents in ascending order by title (A->Z)
      sort: { title: 1 },
      // Include only the `title` and `imdb` fields in each returned document
      projection: { _id: 0, title: 1, imdb: 1 },
    };
10. অথবা find use করতে cursor নিবো।
    const query = { };
    const cursor = serviceCollection.find(query);





```
</details>
	
### ExpressBoilerplate
<details>
<summary>
  <h3> ExpressBoilerplate-(Click Me)</h3>
</summary>
<br >
	
```js
//Must be install
"scripts": {
    "start": "nodemon index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
"dependencies": {
    "cors": "^2.8.5",
    "dotenv": "^16.0.3",
    "express": "^4.18.2",
    "mongodb": "^4.11.0",
    "nodemon": "^2.0.20"
  }
	
//index.js
const express = require("express");
const cors = require("cors");
require("dotenv").config();
const app = express();
const port = process.env.PORT || 5000;
//middleware
app.use(cors());
app.use(express.json());

app.get("/", (req, res) => {
  res.send("Ema John server is running");
});

app.listen(port, () => {
  console.log(`Ema John Server is Running: ${port}`);
});


```
</details>
	

### MongoDBBoilerplate
<details>
<summary>
  <h3> MongoDB Boilerplate-(Click Me)</h3>
</summary>
<br >
	
```js

const express = require("express");
const cors = require("cors");
const { MongoClient, ServerApiVersion } = require("mongodb");
require("dotenv").config();

const app = express();
const PORT = process.env.PORT || 5000;

//middleware
app.use(cors());
app.use(express.json());


const uri = `mongodb+srv://${process.env.DB_USER}:${process.env.DB_PASSWORD}@cluster0.nftlnia.mongodb.net/?retryWrites=true&w=majority`;
const client = new MongoClient(uri, {
  useNewUrlParser: true,
  useUnifiedTopology: true,
  serverApi: ServerApiVersion.v1,
});

async function run() {
  try {
    const serviceCollection = client.db("geniusCar").collection(services);
    //Backend data load করতে api lagbe
    app.get("/services", async (req, res) => {
      //সব গুলাকে find করতে চাইলে empty object দিতে হবে।
      const query = {};
      //data sort করতে options use করে। অথবা find use করতে cursor নিবো।
      const cursor = serviceCollection.find(query);
      // async/ promise call হচ্ছে তাই await use করতে হবে
      //toArray দিয়ে cursor টাকে array তে convert করতে হবে  যাতে client site use  করতে হবে
      const services = await cursor.toArray();
      res.send(services);
    });
  } finally {
  }
}
run().catch((error) => console.error(error));

app.get("/", (req, res) => {
  res.send("Hello Genius Car Server");
});
app.listen(PORT, () => {
  console.log("genius car server is running", PORT);
});


// Advance BoilerPlate
const express = require("express");
const cors = require("cors");
const { MongoClient, ServerApiVersion, ObjectId } = require("mongodb");
require("dotenv").config();

const app = express();
const PORT = process.env.PORT || 5000;

//middleware
app.use(cors());
app.use(express.json());

const uri = `mongodb+srv://${process.env.DB_USER}:${process.env.DB_PASSWORD}@cluster0.nftlnia.mongodb.net/?retryWrites=true&w=majority`;
const client = new MongoClient(uri, {
  useNewUrlParser: true,
  useUnifiedTopology: true,
  serverApi: ServerApiVersion.v1,
});

async function run() {
  try {
    //serviceCOllection
    const serviceCollection = client.db("geniusCar").collection("services");
    //order collection
    const orderCollection = client.db("geniusCar").collection("orders");
    // all services api call
    app.get("/services", async (req, res) => {
      const query = {};
      const cursor = serviceCollection.find(query);
      const services = await cursor.toArray();
      res.send(services);
      console.log();
    });

    //single services api call
    app.get("/services/:id", async (req, res) => {
      const id = req.params.id;
      const query = { _id: ObjectId(id) };
      const service = await serviceCollection.findOne(query);
      res.send(service);
    });

    //orders api call
    app.get("/orders", async (req, res) => {
      console.log(req.query.email);
      let query = {};
      if (req.query.email) {
        query = {
          email: req.query.email,
        };
      }
      const cursor = orderCollection.find(query);
      const orders = await cursor.toArray();
      res.send(orders);
    });

    app.post("/orders", async (req, res) => {
      const order = req.body;
      const result = orderCollection.insertOne(order);
      res.send(result);
    });

    //patch
    app.patch('/orders/:id', async(req, res) => {
      const id = req.params.id;
      const status = req.body.status;
      const query = {_id:ObjectId(id)};
      const updateDoc = {
        $set:{
          status: status
        }
      }
      const result = await orderCollection.updateOne(query, updateDoc);
      res.send(result)
    })

    // delete method
    app.delete("/orders/:id", async (req, res) => {
      const id = req.params.id;
      const query = { _id: ObjectId(id) };
      const result = await orderCollection.deleteOne(query);
      res.send(result);
    });
  } finally {
  }
}
run().catch((error) => console.error(error));

app.get("/", (req, res) => {
  res.send("Hello Genius Car Server");
});
app.listen(PORT, () => {
  console.log("genius car server is running", PORT);
});

/*
//mongodb 
0. npm install mongodb
1. create New Project (copy user and password)
2. Database > Connect > connect your application copy (include full drive) paste index.js 
//
const { MongoClient, ServerApiVersion } = require('mongodb');
const uri = "mongodb+srv://GeniusCar:<password>@cluster0.nftlnia.mongodb.net/?retryWrites=true&w=majority";
const client = new MongoClient(uri, { useNewUrlParser: true, useUnifiedTopology: true, serverApi: ServerApiVersion.v1 });
client.connect(err => {
  const collection = client.db("test").collection("devices");
  // perform actions on the collection object
  client.close();
});
3. Remove this and create async function
client.connect(err => {
  const collection = client.db("test").collection("devices");
  // perform actions on the collection object
  client.close();
}); 
4. create async function (follow mongodb crud find many)
async function run(){
    try{
        //4.1 create collection 
const serviceCollection = client.db("geniusCar").collection('services');
    }
    finally{

    }
}
run().catch(error => console.error(error))
5. Database > collections > create database same name 
client.db("geniusCar").collection(services);
database name (geniusCar)
collection(services)
6. Backend data load করতে api lagbe
app.get('/services', async(req, res) => {

    })
7. query কারে কারে find করতে চাই ( )
 const query = { runtime: { $lt: 15 } };

৮। সব গুলাকে find করতে চাইলে empty object দিতে হবে।

const query = { };
৯। data sort করতে options use করে। 
  const options = {
      // sort returned documents in ascending order by title (A->Z)
      sort: { title: 1 },
      // Include only the `title` and `imdb` fields in each returned document
      projection: { _id: 0, title: 1, imdb: 1 },
    };
10. অথবা find use করতে cursor নিবো।
    const query = { };
    const cursor = serviceCollection.find(query);

11. data create করার জন্য Express er post method use করতে হয়
 //orders api call
    app.post("/orders", async (req, res) => {
      const order = req.body;
      const result = orderCollection.insertOne(order);
      res.send(result);
    });
12. //  call post method
    fetch("http://localhost:5000/orders", {
      method: "POST",
      headers: {
        "content-type": "application/json",
      },
      body:JSON.stringify(order)
    })
    .then(res=> res.json)
    .then(data=> console.log(data))
    .then(error => console.error(error))
13, //api get korte hole
  app.get("/orders", async (req, res) => {
      const query = {};
      const cursor = orderCollection.find(query);
      const orders = await cursor.toArray();
      res.send(orders);
    });
  14, delete server site
  // delete method
    app.delete("/orders/:id", async (req, res) => {
      const id = req.params.id;
      const query = { _id: ObjectId(id) };
      const result = await orderCollection.deleteOne(query);
      res.send(result);
    });
    15. delete client site code
      const handleDelete = (id) => {
    const proceed = window.confirm("Are you sure, you want ");
    if (proceed) {
      fetch(`http://localhost:5000/orders/${id}`, {
        method: "DELETE",
      })
        .then((res) => res.json())
        .then((data) => {
          console.log(data);
          if (data.deletedCount > 0) {
            alert("deleted successfully");
            const remaining = orders.filter(odr=> odr._id !== id);
            setOrders(remaining)
          }
        });
    }
  };

14. patch server code
 //patch
    app.patch('/orders/:id', async(req, res) => {
      const id = req.params.id;
      const status = req.body.status;
      const query = {_id:ObjectId(id)};
      const updateDoc = {
        $set:{
          status: status
        }
      }
      const result = await orderCollection.updateOne(query, updateDoc);
      res.send(result)
    })
    14. patch client site code
    //patch
  const handleStatusUpdate = (id) => {
    fetch(`http://localhost:5000/orders/${id}`, {
      method: "PATCH",
      Headers: {
        "content-type": "application/json",
      },
      body: JSON.stringify({ status: "Approved" }),
    })
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
        if (data.modifiedCOunt > 0) {
          const remaining = orders.filter((odr) => odr._id !== id);
          const approving = orders.find(odr => odr._id === id);
          approving.status = 'Approved'
          const newOrders = [...remaining, approving];
          setOrders(newOrders);
        }
      });
  };


*/


```
</details>


### CrudOparetion
<details>
<summary>
  <h3> Crud Oparetion (Click Me)</h3>
</summary>
<br >
	
```js

// POST

//Step 1 : (send data client to server)
 const handleAddServant = (event) => {
    event.preventDefault();
    console.log(servant);
    
//(send data client to server)
    fetch('http://localhost:5000/servants', {
        method: 'POST',
        headers: {
            'content-type': 'application/json'
        },
        body: JSON.stringify(servant)
    })
    .then(res => res.json())
    .then(data => {
        if(data.acknowledged){
            alert('User added successfully');
            event.target.reset();
        }
    })
  };
  
  //Step 2 : (receive data in server)
async function run() {
  try {
    const servantCollection = client
      .db("servant-database")
      .collection("servants");
      
//(receive data in server)
      app.post('/servants', async (req, res) => {
        const servant = req.body;
        console.log(servant);
        const result = await servantCollection.insertOne(servant)
        res.send(result);
    });
  } finally {
  }
}
run().catch(console.dir);
  

```
</details>


### DotEnv
<details>
<summary>
  <h3> DotEnv -(Click Me)</h3>
</summary>
<br >
	
```js

/* 
১। npm install dotenv --save
2 create .env file in your root folder
DB_USER=Genius
DB_PASSWORD=ylqSoHGMEeM8
3. inde.js file (change username and password)
require('dotenv').config()
const uri = `mongodb+srv://${process.env.DB_USER}:${process.env.DB_PASSWORD}@cluster0.nftlnia.mongodb.net/?retryWrites=true&w=majority`;




*/

```
</details>



### Notes
<details>
<summary>
  <h3>Notes for MongoDb  (Click Me)</h3>
</summary>
<br >
  - Notes must be know every single part for interview 

```js

************Mongo DB  Notes************
//Module 65-8
 1.What are MongoDb operators?
MongoDb offers the following query operator types:
i. Comparison
ii. Logical
iii. Element
iv. Evalution
v. Geospatial
vi. Array
vii. Bitwise
viii. Comments
	
	
	
	

************End Node Notes************
```
</details>
  
### MongoDBInterviewQuestions
<details>
<summary>
  <h3>Mongo DB Interview Questions (Click Me)</h3>
</summary>
<br >
 must be know every single part for interview https://roadmap.sh/react
	
 ```js
************Mongo DB Interview Questions************
	
//Milestone: 11 Backend and Database integrate
//Node.js Interview Questions
//Module 65.9
1. What is Node.js and how it works?
2. What are the key features of Node.js?
3. What in npm? What is the main functionality of npm?
4. What is the difference between JavaScript and Node.js?
5. What is event-driven programming in Node.js?
6. How single threaded handles concurrency when multiple I/O operations happing in Node.js?
7. What is package.json?
8. What is Event loop in Node.js and how does it work?
9. What do you understand by callback hell?

//MongoDb Interview Questions	
1. What is a Document in MongoDb?
2. What is Collection in MongoDb?
3. What are some fetures of MongoDb?
4. When to use MongoDb?
5. What are some of the advantages of MongoDB?
6. What type of DBMS is MongoDB?
7. What is the difference between MongoDB and MYSql?
8. Explain the Structure of ObjectID in MongoDB?
9. What is CRUD in MongoDB?
	
	
	
	
	
	
	
  ************Mongo DB Interview Questions************
 ```
</details>

### Comparison Operators
<div class="overflow-x-auto">
  <table class="table w-full">
    <!-- head -->
    <thead>
      <tr>
        <th></th>
        <th>Operator</th>
        <th>Description</th>
	<th>Operator</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <!-- row 1 -->
      <tr>
        <th>1</th>
        <td>$eq </td>
        <td>Matches values that are equal to the given value </td>
	<td> $gt </td>
        <td> Matches if values are greater than the given value </td>
      </tr>
      <!-- row 2 -->
      <tr>
        <th>4</th>
        <td>$lt </td>
        <td>Matches if values are less than the given value </td>
	<td>$gte </td>
        <td> Matches if values are greater or equal to the given value</td>
      </tr>
       <!-- row 1 -->
      <tr>
        <th>4</th>
        <td>$lte </td>
        <td>Matches if values are less or equal to the given value.</td>
	<td> $in</td>
        <td>Matches any of the values in an array </td>
      </tr> <!-- row 1 -->
      <tr>
      <tr>
        <th>4</th>
        <td> $ne</td>
        <td>Matches values that are not equal to the given value. </td>
	<td>$nin </td>
        <td> Matches none of the values specified in an arrray </td>
      </tr> <!-- row 1 -->
      <tr>
        <th>4</th>
        <td>$and </td>
        <td> </td>
	  <td>$not </td>
        <td> </td>
      </tr>
      </tr> <!-- row 1 -->
      <tr>
        <th>4</th>
        <td>$nor </td>
        <td> </td>
	<td>$or </td>
        <td> </td>
      </tr>
    </tbody>
  </table>
</div>

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
