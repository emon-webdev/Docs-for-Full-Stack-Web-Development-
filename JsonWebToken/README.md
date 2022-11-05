# (jwt) JsonWebToken Using Method And Example 

### 🔭 What is JsonWebToken?
- 
### 👯 Why use JsonWebToken?
- 
### 🤔 How to Use?
- Every req in Boilerplate (Full Example)
List of Express JS:
- [initialSetUp](#initialSetUp)
- [Boilerplate](#Boilerplate)
- [JsonWebTokenInterviewQuestions](#JsonWebTokenInterviewQuestions)
- [Table](#Table)
CrudOparetion


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

/* 
1। npm install jsonwebtoken
2.const jwt = require('jsonwebtoken');
3. in your terminal

> require('crypto').randomBytes(64)
	
<Buffer ed 24 a7 0f 85 f1 a9 99 96 bf c0 fd 55 11 70 ce 2e 55 17 e5 eb 13 87 4b 87 e2 90 2d 27 ae f8 18 48 53 13 7c c0 53 61 14 23 9a c7 a9 61 21 a4 96 8a 33 ... 14 more bytes>
	
> require('crypto').randomBytes(64).toString()
'I�%�\x11�U��k��\x04����ϯ���`�T\b\f7\x19g���o�\x1Ft)tՎސ.\x06,\x1C��\n\x16\x04?�\x18"��\\���%h'
	
> require('crypto').randomBytes(64).toString('hex')
'ceb36bf116d2ef75dbd1df43a5e03b1c6fa29105201ba3e98c756534ad394904c724c4d9193cbfc51bf8f2a49dc4187bf63b49dea76e22aa585ce4e749eed619'
>

3.1 .env
ACCESS_TOKEN_SECRET=4766da99c10f0f4b8ba9c75f8ebe20fdd64c0a25115d91cd8f3d761029774b9e08d2bc7ff6c6cf16778aeca710abb1738ff3e71098040b85aa4e00200ab3e577
	
4. client site (login.js )
login(email, password)
      .then((result) => {
        const user = result.user;
        console.log(result.user.email);
        const currentUser = {
          email: user.email,
        };

        console.log(currentUser);

        // get jwt token
        fetch("http://localhost:5000/jwt", {
          method: "POST",
          headers: {
            "content-type": "application/json",
          },
          body: JSON.stringify(currentUser),
        })
          .then((res) => res.json())
          .then((data) => {
            console.log(data);
          });

        // form.reset();
        // navigate(from, {replace:true})
      })
      .catch((error) => console.log(error));


// server (index.js)
app.post('/jwt', async(req, res) => {
const user = req.body;
const token = jwt.sign(user, process.env.ACCESS_TOKEN_SECRET, {expiresIn: "1h"});
res.send(token)

})

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

