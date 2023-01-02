# MongoDB Using Method And Example

### 🔭 What is MongoDB?
- 
### 👯 Why use MongoDB?
- 
###  🤔 How to Use?
- 

- Every req in MongoDBBoilerplate (Full Example)
List of Express JS:
- [AllOparetion](#AllOparetion)
- [initialSetUp](#initialSetUp)
- [Boilerplate](#Boilerplate)
- [MongoDBBoilerplate](#MongoDBBoilerplate)
- [CrudOparetion](#CrudOparetion)
- [DotEnv](#DotEnv)
- [imageStore](#imageStore)
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

Demo Content

```
</details>


### AllOparetion
<details>
<summary>
  <h3> AllOparetion -(Click Me)</h3>
</summary>
<br >
	
```js

All Opareation Client > Database > Mongodb
========================================
========  Get Method  (Email waise data fetch in MongoDb) =================
<---Client Code--->
const { user } = useContext(AuthContext);
  const [orders, setOrders] = useState([]);
    fetch(`http://localhost:5000/orders?email=${user?.email}`)
      .then((res) => {
        // if (res.status === 401 || res.status === 403) {
        //   return logout();
        // }
        return res.json();
      })
      .then((data) => {
        setOrders(data);
      });
  }, [user?.email]);
	
<---Database Code--->
//orders api
    app.get("/orders", async (req, res) => {
      let query = {};
      if (req.query.email) {
        query = {
          email: req.query.email,
        };
      }
      const result = await orderCollection.find(query).toArray();
      res.send(result);
    });
	
========================================	

========   Method ( MongoDB ObjectId  বাদে অন্য id ধরে data load ) =======
<---Client Code--->
 const { serviceName, phone, price, service, _id, customer, status } = order;
  const [orderService, setOrderService] = useState([]);
  useEffect(() => {
    fetch(`http://localhost:5000/services/${service}`)
      .then((res) => res.json())
      .then((data) => setOrderService(data));
  }, [service]);

<---Database Code--->


========================================
	
<--- Delete  Method (_id waise) --->
<---Client Code--->
	
 const handleDelete = (id) => {
    const proceed = window.confirm(
      "Are you sure you want to cancel this order"
    );
    if (proceed) {
      fetch(`http://localhost:5000/orders/${id}`, {
        method: "DELETE",
      })
        .then((res) => res.json())
        .then((data) => {
          console.log(data);
          if(data.deletedCount > 0){
            alert('deleted successfully')
            const remaining = orders.filter(odr => odr._id !== id);
            setOrders(remaining)
          }
        });
    }
  };
	
//
 <button onClick={() => handleDelete(_id)} className="btn btn-circle">

<---Database Code--->
 //delete method
    app.delete("/orders/:id", async (req, res) => {
      const id = req.params.id;
      const query = { _id: ObjectId(id) };
      const result = await orderCollection.deleteOne(query);
      res.send(result);
    });

========================================
	
<---  Update Method ( add admin, pending/ approved, req/submited work in this way ) --->
<---Client Code--->
 <button
  onClick={() => handleStatusUpdate(_id)}
  className="btn btn-ghost btn-xs"
>
  {status ? status : "pending"}
</button>
//

  const handleStatusUpdate = (id) => {
    fetch(`http://localhost:5000/orders/${id}`, {
      method: "PATCH",
      headers: {
        "content-type": "application/json",
      },
      body: JSON.stringify({ status: "Approved" }),
    })
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
        if (data.modifiedCount > 0) {
          console.log(data);
          const remaining = orders.filter((odr) => odr._id !== id);
          const approving = orders.find((odr) => odr._id === id);
          approving.status = "Approved";
          const newOrders = [approving, ...remaining];
          setOrders(newOrders);
        }
      });
  };
	
<---Database Code--->
app.patch("/orders/:id", async (req, res) => {
      const id = req.params.id;
      const status = req.body.status;
      console.log(id, status);
      const query = { _id: ObjectId(id) };
      const updatedDoc = {
        $set: {
          status: status,
        },
      };
      const result = await orderCollection.updateOne(query, updatedDoc);
      res.send(result);
    });
	
	
========================================	
	
<---  Get Method (double query করে data load MOdule : 68) --->

<---Client Code--->
  const [products, setProducts] = useState([]);
  const [size, setSize] = useState(10);

  useEffect(() => {
    const url = `http://localhost:5000/products?page=${page}&size=${size}`;
    fetch(url)
      .then((res) => res.json())
      .then((data) => {
        setProducts(data.products);
        setCount(data.count);
      });
  }, [page, size]);
  
<---Database Code--->
app.get("/products", async (req, res) => {
      const page = parseInt(req.query.page);
      const size = parseInt(req.query.size);
      console.log(page, size);
      const query = {};
      const cursor = productCollection.find(query);
      const products = await cursor
        .skip(page * size)
        .limit(size)
        .toArray();
      //pagination er jonno count send kora client site
      const count = await productCollection.estimatedDocumentCount();
      res.send({ products, count });
    });
	
========================================
	
<---  post  Method ( map body to db id) --->
<---Client Code--->
  //get data from localStorage
  useEffect(() => {
    const storedCart = getStoredCart();
    const savedCart = [];
    const ids = Object.keys(storedCart);
    console.log(storedCart, ids);

    fetch("http://localhost:5000/productsByIds", {
      method: "POST",
      headers: {
        "content-type": "application/json",
      },
      body: JSON.stringify(ids),
    })
      .then((res) => res.json())
      .then((data) => {
        for (const id in storedCart) {
          const addedProduct = data.find((product) => product._id === id);
          if (addedProduct) {
            const quantity = storedCart[id];
            addedProduct.quantity = quantity;
            savedCart.push(addedProduct);
          }
        }
        setCart(savedCart);
      });
  }, [products]);

<---Database Code--->
app.post("/productsByIds", async (req, res) => {
      const ids = req.body;
      const objectIds = ids.map(id => ObjectId(id));
      const query = {_id: {$in: objectIds}};
      console.log(ids, query) ;
      const cursor = productCollection.find(query);
      const products = await cursor.toArray();
      res.send(products);
    });

========================================
	
<---   Method () --->
<---Client Code--->

<---Database Code--->
========================================
	
<---   Method () --->
<---Client Code--->

<---Database Code--->

========================================
	
<---   Method () --->
<---Client Code--->

<---Database Code--->
	
========================================	
	
<---   Method () --->
<---Client Code--->

<---Database Code--->
	
========================================
	
<---   Method () --->
<---Client Code--->

<---Database Code--->
	

========================================

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

============================================



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





```
</details>


### CrudOparetion
<details>
<summary>
  <h3> Crud Oparetion (Click Me)</h3>
</summary>
<br >
	
```js

MongoDB  CRUD operation নিয়ে simple talk ? 

C ---- Create বা insert  Data => 
Server থেকে  নতুন  Data কে   .insertOne() , .insertMany() দিয়ে  MongoDB র Collection এ  সেই নতুন Data পাঠিয়ে দেয়া ।
R ----- Read  Data  =>   
MongoDB র   Collection  থেকে কোনো  Data  কে  ব্যাবহার করার জন্য  .find()  দিয়ে     Data  কে  Server কিংবা  Client Side  এ ফিরিয়ে আনা । 
U ----- Update Data =>
MongoDB র   Collection  এ থাকা  কোনো Data কে পরিবর্তন করার জন্য .updateOne()  ,  .updateMany() , replaceOne()   ব্যাবহার করে  Server Side থেকে MongoDB  তে  Data  পাঠানো । 
D ---- Delete Data =>
MongoDB Collection এ থাকা কোনো Data কে  Delete করার জন্য .deleteOne()  ,  .deleteMany()   দিয়ে  Server  থেকে  MongoDB  তে কমান্ড  পাঠানো ।

//Number 1 of CRUD POST method
// POST (Crud er => C )

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

//Number 2 of CRUD GET/READ method
//Get api (Crud => R(get/read) )

async function run() {
  try {
    const servantCollection = client
      .db("servant-database")
      .collection("servants");

    //Get api (Crud => R(get/read) )
//you can access browser (http://localhost:5000/servants)
    app.get("/servants", async (req, res) => {
      const query = {};
      const cursor = servantCollection.find(query);
      const servants = await cursor.toArray();
      res.send(servants);
    });

  } finally {
  }
}
run().catch(console.dir);
	
//Number 3 of CRUD PUT/PATCH method
//Update (PUT/PATCH) api (Crud => u(PUT/PATCH) )
	
async function run() {
  try {
    const servantCollection = client
      .db("servant-database")
      .collection("servants");
	
//Update (PUT/PATCH) api (Crud => u(PUT/PATCH) )
    app.put("/servants/:id", async (req, res) => {
      const id = req.params.id;
      const query = { _id: ObjectId(id) };
      const servant = req.body;
      const option = { upsert: true };
      const updatedServant = {
        $set: {
          name: servant.name,
          address: servant.address,
          email: servant.email,
        },
      };
      const result = await servantCollection.updateOne(query, updatedServant, option);
      res.send(result);
    });
	
}
run().catch(console.dir);

app.listen(Port, () => {
  console.log(`Servant Network Server running on port ${Port}`);
});
	
//Update Component
import React, { useState } from "react";
import { useLoaderData } from "react-router-dom";

const Update = () => {
  const storedServant = useLoaderData();

  const [servant, setServant] = useState(storedServant);

  const handleUpdateServant = (event) => {
    event.preventDefault();
    console.log(servant);
    fetch(`http://localhost:5000/servants/${storedServant._id}`, {
      method: "PUT",
      headers: {
        "content-type": "application/json",
      },
      body: JSON.stringify(servant),
    })
      .then((res) => res.json())
      .then((data) => {
        if (data.modifiedCount > 0) {
          alert("user updated");
          console.log(data);
          event.target.reset()
        }
      });
  };

  const handleInputChange = (event) => {
    const field = event.target.name;
    const value = event.target.value;
    const newUser = { ...servant };
    newUser[field] = value;
    setServant(newUser);
  };

  return (
    <div className="text-center">
      <h2>Update Servant: {storedServant.name} </h2>
      <h2>Update Servant: {storedServant.email} </h2>
      <div className="">
        <form onSubmit={handleUpdateServant} className="mx-auto mb-14 max-w-md">
          <input
            type="text"
            name="name"
            defaultValue={storedServant.name}
            required
            onBlur={handleInputChange}
            placeholder="Type Name"
            className="input input-bordered input-secondary w-full max-w-xs"
          />
          <br />
          <input
            type="text"
            name="address"
            required
            onBlur={handleInputChange}
            defaultValue={storedServant.address}
            placeholder="Type address"
            className="input input-bordered input-secondary w-full max-w-xs"
          />
          <br />
          <input
            type="email"
            name="email"
            required
            defaultValue={storedServant.email}
            onBlur={handleInputChange}
            placeholder="Type Email"
            className="input input-bordered input-secondary w-full max-w-xs"
          />
          <br />
          <button className="btn btn-outline btn-success" type="submit">
            Update Servant
          </button>
        </form>
      </div>
    </div>
  );
};

export default Update;


	
//Number 4 of CRUD DELETE method
//DELETE  api (Crud => D(DELETE) )

async function run() {
  try {
    const servantCollection = client
      .db("servant-database")
      .collection("servants");

//Delete api (CRUD => D )
    app.delete("/servants/:id", async (req, res) => {
      const id = req.params.id;
      const query = { _id: ObjectId(id) };
      const result = await servantCollection.deleteOne(query);
      console.log(result);
      res.send(result);
    });

  } finally {
  }
}
run().catch(console.dir);

	
//delete component
const Blog = () => {
  const servants = useLoaderData();
  const [displayServants, setDisplayServants] = useState(servants);

  const handleDelete = (servant) => {
    const agree = window.confirm(
      `Are you sure you want to delete: ${servant.name}`
    );
    if (agree) {
      console.log(agree);
      fetch(`http://localhost:5000/servants/${servant._id}`, {
        method: "DELETE",
      })
        .then((res) => res.json())
        .then((data) => {
          if (data.deletedCount > 0) {
            alert("user deleted successfully");
            const remainingServant = displayServants.filter(
              (srvnt) => srvnt._id !== servant._id
            );
            setDisplayServants(remainingServant);
          }
        });
    }
  };
	
  return (
    <div className="text-center">
      <h2>Blog</h2>
      <h1>servant: {displayServants.length}</h1>
      <div>
        {displayServants.map((servant) => (
          <div className="p-4 mb-3 border" key={servant._id}>
            <p>{servant.name}</p>
            <p>{servant.email}</p>
            <button
              className="btn btn-tiny"
              onClick={() => handleDelete(servant)}
            >
              X
            </button>
          </div>
        ))}
      </div>
    </div>
  );
};

export default Blog;
	
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


### imageStore
<details>
<summary>
  <h3> image Store-(Click Me)</h3>
</summary>
<br >
	
```js

//Three places to setore images
1. Thirt party Image hosting server
2. File system of your server
3. mongodb (databasae)

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
        <td>Limit Data </td>
        <td> const products = await cursor.limit(10).toArray(); </td>
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
