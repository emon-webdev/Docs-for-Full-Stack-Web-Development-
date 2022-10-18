# Firebase Using Method And Example

### 🔭 What is Firebase?
- 
### 👯 Why use Firebase?
- 
###  🤔 How to Use?

List of React:
- [InitialSetup](#InitialSetup)
- [GoogleSignIn](#GoogleSignIn)
- [EmailPasswordAuth](#EmailPasswordAuth)
- [PrivateRoute](#PrivateRoute)
- [useNavigate](#useNavigate)
- [AuthContext](#AuthContext)

- [FireBaseHosting](#FireBaseHosting)
- [Notes](#Notes)
- [FirebaseInterviewQuestions](#FirebaseInterviewQuestions)
- [Table](#Table)

### demo
<details>
<summary>
  <h3>AuthContext-(Click Me)</h3>
</summary>
<br >
	
```js

FireBaseHosting code

```
</details>

### InitialSetup
<details>
<summary>
  <h3> InitialSetup -(Click Me)</h3>
</summary>
<br >
	
```js
	
//Initial setup
1. visit: console.firebase.google.com
2. Create a new firebase
3. Google Analytics
i. একটি web analytics service
ii. website traffic কে track kore report তৈরি করে।
iii. website এর সাথে visitor এর interaction এর trend এবং pattern নির্ণয় করতে user কে সাহায্য করে।
iv. 
4. Visit doc (go to docs): Build > authentication > web > getting started
5. Register web app > firebase project home > click web > give name and register
6. Install firebase for your project: npm install firebase
7. Dangerous: get firebase config and put it in firebase.init.js
//Setup provider
8. export app from firebase.init.js
9. Create auth using getAuth from firebase by using app from firebase.init.js
10. Create a google auth provider 
11. go to firebase > Build > Authentication > Sing in method
11. Enable google sign in method
12. Create a button for google sign in method with a click handler
13. Inside the event handler, call signInWithPopup with auth, provider
14. After SingWithPopup .then result , error
// display data

//add a new sign in method
1. enable the sign in method
2. Create gitbub, twitter, fb, etc. app create
3. get clientId and Secret





```
</details>



### GoogleSignIn
<details>
<summary>
  <h3> Google Sign In-(Click Me)</h3>
</summary>
<br >

```js
import { getAuth, GoogleAuthProvider, signInWithPopup, signOut } from "firebase/auth";
import { useState } from "react";
import "./App.css";
import app from "./firebase.init";

const auth = getAuth(app);
function App() {
const [user, setUser] = useState({});
  const googleProvider = new GoogleAuthProvider();
  //handle GoogleS ingIn
  const handleGoogleSingIn = () => {
    signInWithPopup(auth, googleProvider)
      .then((result) => {
        const user = result.user;
        console.log(user)
        setUser(user)
      })
      .catch((error) => {
        console.error(error);
      });
  };
  //handle Google Sing Out
  const handleGoogleSingOut = () => {
    signOut(auth)
    .then(() => {
      setUser({})
    })
    .catch(() =>{
      setUser({})
    })
  };

  return (
    <div className="App">
      {
        user.uid? 
        <button onClick={handleGoogleSingOut}>Google Sing Out</button>
        :
        <button onClick={handleGoogleSingIn}>Google Sing In</button>
      }
      {
        user.uid && <div>
          <h3>Name: {user.displayName}</h3>
          <p>Email: {user.email}</p>
          <img src={user.photoURL} alt="" srcset="" />
        </div>
      }
    </div>
  );
}

export default App;


```
</details>



### EmailPasswordAuth
<details>
<summary>
  <h3> Email Password Authentication-(Click Me)</h3>
</summary>
<br >
	
```js

demo code

```
</details>

### PrivateRoute
<details>
<summary>
  <h3> Private Route-(Click Me)</h3>
</summary>
<br >
	
```js
//step 1
//Create 2 components
i. PrivateRoute ii. PrivateRoute Children component (যেইটা PrivateRoute হবে। login বাদে ঐ route lock থাকবে)

Example:
// App.js
{
  path: "/orders",
  element: (
    <PrivateRoute>
      <Orders />
    </PrivateRoute>
  ),
},

// PrivateRoute componets
import React, { useContext } from "react";
import { Navigate } from "react-router-dom";
import { AuthContext } from "../contexts/UserContext";

const PrivateRoute = ({ children }) => {
  const { user, loading } = useContext(AuthContext);
//loading যাতে page reload দেওয়ার পরে user ঐ page এ থাকে।
  if(loading){
    return <div>loading...</div>
  }

  if (user && user.uid) {
    return children;
  }
  return <Navigate to='/login'></Navigate>;
};

export default PrivateRoute;

//Orders componets
import React from 'react';
const Orders = () => {
    return (
        <div>
            <h2>Orders</h2>
        </div>
    );
};
export default Orders;

//  Another private Route (just set PrivateRoute inside)
{
  path: "/",
  element: <PrivateRoute><Home /></PrivateRoute>
},
{
  path: "/orders",
  element: (
    <PrivateRoute>
      <Orders />
    </PrivateRoute>
  ),
},


```
</details>


### useNavigate
<details>
<summary>
  <h3> useNavigate-(Click Me)</h3>
</summary>
<br >
	
```js
//step 1:
import { useNavigate } from "react-router-dom";
const navigate = useNavigate();
	
//step 2: 
// যখন user sign in করবে তখন user কে navigate করতে হবে
signIn(email, password)
.then((result) => {
const user = result.user;
console.log(user);
form.reset();
//step 3:
// navigate user home page
navigate("/home");
})
.catch((error) => console.error(error));


<--- Advace Example () --->
// step 1: (PrivateRoute)
//Private.js (component)
import React, { useContext } from "react";
import { Navigate, useLocation } from "react-router-dom";
import { AuthContext } from "../context/UserContext";

const PrivateRoute = ({ children }) => {
 const { user, loading } = useContext(AuthContext);
  const location = useLocation()
// loading state যাতে user page reload এর পরে same page এ থাকে।
  if(loading){
    return <div>loading</div>
  }
  if (user && user.uid) {
    return children;
  }
  return <Navigate to="/login" state={{from:location}} replace ></Navigate>;
};

export default PrivateRoute;

//step 2: 
//Login.js (component)
import { useLocation, useNavigate } from "react-router-dom";
const Login = () => {
  //navigate after login
  const navigate = useNavigate();
  // call location
  const location = useLocation();
  const from = location.state?.from?.pathname || "/";
    //sign in user in firebase
    signIn(email, password)
      .then((result) => {
        const user = result.user;
        console.log(user);
        form.reset();
        //navigate
        // navigate("/home");
        navigate(from, {replace:true})
      })
      .catch((error) => console.error(error));
  };
  
 return (
	<div></div>
 );
};


```
</details>

### AuthContext
<details>
<summary>
  <h3>AuthContext-(Click Me)</h3>
</summary>
<br >
	
```js

//step 1 create (UserContext) component
//UserContext.js (component)
import React, { createContext } from 'react';
export const AuthContext = createContext();
const UserContext = ({children}) => {
//check user where use context 
const user = {email: 'abc'};
const authInfo = {user};
    return (
        <AuthContext.Provider value={authInfo}>
            {children}
        </AuthContext.Provider>
    );
};
export default UserContext;

//step 2 (go index.js file then set UserContext)
import UserContext from "./context/UserContext";
<React.StrictMode>
    <UserContext>
      <App />
    </UserContext>
 </React.StrictMode>
	
//step 3 (access to UserContext in Header.js)
//Header.js (component)
import UserContext, { AuthContext } from "../../context/UserContext";
const Header = () => {
const user = useContext(AuthContext);
return (
	 <span>{user.email}</span>
    )
};

export default Header;
	
<!-- Full Example -->

	
	

```
</details>







### FireBaseHosting
<details>
<summary>
  <h3>FireBase Hosting-(Click Me)</h3>
</summary>
<br >
59-9 (bonus video) Host your react app to firebase
	
```js

//Firebase Hosting
// One time for each computer
1. npm install -g firebase-tools
2. firebase login

//for each project one time
3. firebase init
4. Hosting: Configure files for Firebase Hosting and (optionally) set up GitHub Action deploys
5. Use an existing project
6. Select you project (ema-john-fa6f4 must be match firebase.google.com your project name)
7.  (you just write build) What do you want to use as your public directory? (public) build 
8. (you select y) Configure as a single-page app (rewrite all urls to /index.html)? Yes
9. Configure as a single-page app (rewrite all urls to /index.html)? Yes

// for every deploy
10. npm run build
11. firebase deploy


```
</details>


### Notes
<details>
<summary>
  <h3>Notes for (Click Me)</h3>
</summary>
<br >
  - Notes must be know every single part for interview 

```js

************Firebase Notes************

2.
	
	
	
	

************End Firebase Notes************
```
</details>
  
### FirebaseInterviewQuestions
<details>
<summary>
  <h3>Firebase Interview Questions (Click Me)</h3>
</summary>
<br >
 must be know every single part for interview https://roadmap.sh/react
	
 ```js
************Firebase Interview Questions************
//Mileston 10: React Authentication
//Module: 57-1
1. What is Firebase?
2. Is firebase frontend or backend?
3. What is firebase architecture?
4. What are the features of firebase? / What are the tasks you can accomplish with firebase?
5. Differences between firebase and mongodb?
6. Have you ever used firebase database (real time database)?
7. Can you briefly explain the github authentication process with firebase?
8. Which method is used to Sign-in the user in Firebase Email/Password authentication?
9. Authentication vs Authorization?
Ans:i. Authentication: কাউকে , কোন কিছু, কারো কোন act (যা সঠিক বলে দাবি করা হচ্ছে) প্রকৃত তা সত্য কি না নির্ণয় করার প্রক্রিয়া।
i. Authorization: কাউকে কোন কাজ করার জন্য বা কোন resource ব্যবহার করতে পারার permision দেউয়ার প্রক্রিয়া।
2. What is Encryption
Ans: Encryption: কোন তথ্যকে (text , image, file, credentials etc) অনেক সুরক্ষিত করার জন্য (saving from hackers) 
সেই তথ্যর orginal representation কে different representation er মাধ্যমে প্রকাশ করা।
10. Can you tell me names of 3 authentication method?(hint: Sms/email code, voice, password, fingerprint, face verification)
11. Which authentication methods have you ever used for your project purpoose?
	
	
	
	
	
	
	
  ************End Firebase Interview Questions************
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
        <th>2</th>
        <td> </td>
        <td> </td>
      </tr>
      <!-- row 3 -->
      <tr>
        <th>3</th>
        <td> </td>
        <td> </td>
      </tr>
       <!-- row 1 -->
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

[![Facebook Badge](https://img.shields.io/badge/Facebook-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://fb.com/emonhossain6) [![Linkedin Badge](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/emon007iu/) [![Twitter Badge](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/@emon_webdev) [![Mail Badge](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:emon.hossain.wd@gmail.com)

<h4>❤️🤔 You can follow my Github and other social accounts 🤔❤️</h4>
<h2>❤️ Thank you very much! ❤️</h2>
