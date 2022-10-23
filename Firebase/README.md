# Firebase Using Method And Example

### 🔭 What is Firebase?
- 
### 👯 Why use Firebase?
- 
###  🤔 How to Use?

List of React:
- [InitialSetup](#InitialSetup)
- [Firebasae.init.js](#FirebasaeInitJs)
- [GoogleSignIn](#GoogleSignIn)
- [EmailPasswordAuth](#EmailPasswordAuth)
- [ResetPassword](#ResetPassword)
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


### FirebasaeInitJs
<details>
<summary>
  <h3>Firebasae.init.js system -(Click Me)</h3>
</summary>
<br >
	
```js
//step 1
//Firebase.init.js

// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: "AIzaSyDf2qGcHt49oH-5_hG9euNs7yurgXaJvUU",
  authDomain: "authentech-b67c9.firebaseapp.com",
  projectId: "authentech-b67c9",
  storageBucket: "authentech-b67c9.appspot.com",
  messagingSenderId: "231829553918",
  appId: "1:231829553918:web:9716fcdfcf528781d01baf",
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);

export default app;


//step 2 (create file in your root folder (.env.local))
//.env.local
apiKey=AIzaSyDf2qGcHt49oH-5_hG9euNs7yurgXaJvUU
authDomain=authentech-b67c9.firebaseapp.com
projectId=authentech-b67c9
storageBucket=authentech-b67c9.appspot.com
messagingSenderId=231829553918
appId=1:231829553918:web:9716fcdfcf528781d01baf

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

//Registration or SignUp.js  (component)

import {
  createUserWithEmailAndPassword,
  getAuth,
  sendEmailVerification,
  updateProfile
} from "firebase/auth";
import React, { useState } from "react";
import { Link } from "react-router-dom";
import swal from 'sweetalert';
import app from "../../Hook/firebaseConfig";
const Registration = () => {
  const auth = getAuth(app);
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [error, setError] = useState("");
  const [isDisabled, setIsDisabled] = useState(true);

  const handleName = (event) => {
    console.log(event.target.value);
    setName(event.target.value);
  };

  const handleEmail = (event) => {
    const test = /^\S+@\S+\.\S+$/.test(event.target.value);
    if (!test) {
      setError("Please give a valid email");
      return;
    }
    setError("");
    setEmail(event.target.value);
  };

  const handlePassword = (event) => {
    if (!/(?=.{8,})/.test(event.target.value)) {
      setError("Password must be 8 character");
      return;
    }
    if (!/(?=.*[a-zA-Z])/.test(event.target.value)) {
      setError("Password Should have UpperCase!!");
      return;
    }

    if (!/(?=.*[!#$%&?@^"])/.test(event.target.value)) {
      setError("Password Must be use Special characters");
      return;
    }

    setError("");
    setPassword(event.target.value);
  };

  const handleRegister = (event) => {
    event.preventDefault();
    if ((name, email, password)) {
      createUserWithEmailAndPassword(auth, email, password)
        .then((userCredential) => {
          // Signed in
          const user = userCredential.user;
          verifyEmail();
          console.log(user);
          updateName();
          swal("Successfully Register");
          setError("");
        })
        .catch((error) => {
          const errorCode = error.code;
          const errorMessage = error.message;
          setError(errorMessage);
        });
    } else {
      setError("Please fil out all the input");
      return;
    }
  };

  const updateName = () => {
    updateProfile(auth.currentUser, {
      displayName: name,
    })
      .then(() => {
        // Profile updated!
        // ...
      })
      .catch((error) => {
        // An error occurred
        // ...
      });
  };

  const verifyEmail = () => {
    sendEmailVerification(auth.currentUser).then(() => {
      // Email verification sent!
      // ...
    });
  };

  return (
    <div className="mt-5">
      <div className="main-container d-flex container justify-content-between align-items-center">
        <div className="register-image image-fluid w-100  ">
          <img
            className="w-100 img-fluid image-fluid"
            src="https://i.ibb.co/hYJTmVX/undraw-Mobile-login-re-9ntv-1.png"
            alt=""
          />
        </div>
        <div className="register-form  w-100">
          <div className="input-box">
            <p className="text-danger">{error}</p>
            <form action="">
              <input
                onBlur={handleName}
                className="form-control p-3 m-2"
                type="text"
                placeholder="Enter your name"
                required
              />
              <input
                onBlur={handleEmail}
                className="form-control p-3 m-2"
                type="email"
                placeholder="Email"
                required
              />
              <input
                onBlur={handlePassword}
                className="form-control p-3 m-2"
                type="password"
                placeholder="password"
                required
              />
              <p className="link ">
                <Link to="/login" className="text-decoration-none">
                  <small className="text-danger link">
                    already have an account? please login
                  </small>
                </Link>
              </p>
              <input onClick={()=> setIsDisabled(!isDisabled)} className="p-2" type="checkbox" />{" "}
              <span className="mb-3">accept term & condition</span>
              <br />
              <button
                onClick={handleRegister}
                type="submit"
                disabled={isDisabled}
                className="btn btn-info p-3 w-50 mt-3 fw-bold text-white"
              >
                Register
              </button>
            </form>
          </div>
          <button className="btn mt-3 border d-flex align-items-center justify-content-evenly p-2 m-auto">
            <img
              className="w-25 image-fluid btn-image"
              src="https://img.icons8.com/color/344/google-logo.png"
              alt=""
            />
            <p className="fw-bold">Google SignIn</p>
          </button>
        </div>
      </div>
    </div>
  );
};

export default Registration;
	
//Login.js (component)
	
import { getAuth, signInWithEmailAndPassword } from "firebase/auth";
import React, { useState } from "react";
import { Link, useNavigate } from "react-router-dom";
import swal from "sweetalert";
import app from "../../Hook/firebaseConfig";
import ResetPassword from "../ResetPassword/ResetPassword";
const Login = () => {
  const auth = getAuth(app);
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [error, setError] = useState("");
  const navigate = useNavigate();
  const [modalShow, setModalShow] = useState(false);

  const handleEmail = (e) => {
    setEmail(e.target.value);
  };

  const handlePassword = (e) => {
    setPassword(e.target.value);
  };

  const handleLogin = () => {
    signInWithEmailAndPassword(auth, email, password)
      .then((userCredential) => {
        // Signed in
        const user = userCredential.user;
        console.log(user);
        swal("Successfully Login");
        navigate("/");
      })
      .catch((error) => {
        const errorCode = error.code;
        const errorMessage = error.message;
        setError(errorMessage);
      });
  };

  return (
    <div className="mt-5">
      <div className="main-container d-flex container justify-content-between align-items-center">
        <div className="register-image image-fluid w-100  ">
          <img
            className="w-100 img-fluid image-fluid"
            src="https://i.ibb.co/0hLvWvP/undraw-Login-re-4vu2.png"
            alt=""
          />
        </div>
        <div className="register-form  w-100">
          <p>{error}</p>
          <div className="input-box">
            <input
              onBlur={handleEmail}
              className="form-control p-3 m-2"
              type="email"
              placeholder="Email"
            />
            <input
              onBlur={handlePassword}
              className="form-control p-3 m-2"
              type="password"
              placeholder="password"
            />
            <p className="link ">
              <Link to="/registration" className="text-decoration-none">
                <small className="text-danger link">
                  are you new? please register
                </small>
              </Link>
              <span onClick={() => setModalShow(true)} role="button" className="ms-4 text-primary cursor-pointer">
                Forget Password?
              </span>
            </p>
            <input className="p-2" type="checkbox" />{" "}
            <span className="mb-3 ">remember me </span>
            <br />
            <button
              onClick={handleLogin}
              className="btn btn-info p-3 w-50 mt-3 fw-bold text-white"
            >
              Login
            </button>
          </div>
          <button className="btn mt-3 border d-flex align-items-center justify-content-evenly p-2 m-auto">
            <img
              className="w-25 image-fluid btn-image"
              src="https://img.icons8.com/color/344/google-logo.png"
              alt=""
            />
            <p className="fw-bold">Google SignIn</p>
          </button>
        </div>

        <ResetPassword show={modalShow} onHide={() => setModalShow(false)} />
      </div>
    </div>
  );
};

export default Login;

	
	

```
</details>


### ResetPassword
<details>
<summary>
  <h3>ResetPassword / Forget Password-(Click Me)</h3>
</summary>
<br >
	
```js
import { getAuth, sendPasswordResetEmail } from "firebase/auth";
import React, { useState } from "react";
import app from "../../Hook/firebaseConfig";

const ResetPassword = (props) => {
  const auth = getAuth(app);
  const [email, setEmail] = useState("");

  const handleResetPassword = () => {
    sendPasswordResetEmail(auth, email)
      .then(() => {
        props.onHide();
      })
      .catch((error) => {
        const errorCode = error.code;
        const errorMessage = error.message;
        // ..
      });
  };

  return (
    <div>
          <h4>Reset Your Password</h4>
          <input
            onBlur={(e) => setEmail(e.target.value)}
            type="text"
            placeholder="Email"
            className="form-control m-3"
          />
          <Button onClick={handleResetPassword}>Update</Button>
    </div>
  );
};

export default ResetPassword;


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
Before Use:
useNavigate er 2টা কাজ 
- Login / Sign Up এর পরে কোথায় যাবে।
- login না থাকা অবস্থাই কিছু route এ যেতে দেই না redirect করে Login Page আসে। 
আবার login করলে same page নিয়ে যেতে হবে।
- only allow authenticated user to visit the route
- 
- Redirect user to the route they wanted to go before login
	
```js	
	
// Simple Way (Login / Sign Up এর পরে কোথায় যাবে।)	
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


<--- Advance Example () --->
Before use: and loading use করতে হবে।
1. PrivateRoute Componet set 
 return <Navigate to="/signin" state={{ from: location }} replace />
2. Singin Componet set
  const navigate = useNavigate();
  const location = useLocation();
  const from = location.state?.from?.pathname || "/";

signInUser(email, password)
	.then((result) => {
	const user = result.user;
	console.log(user);
	navigate(from, {replace:true})
})
	
<!-- Full Example -->
	
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
	
//step 2 :
  return <Navigate to="/login" state={{from:location}} replace ></Navigate>;
};

export default PrivateRoute;


//Login.js (component)
import { useLocation, useNavigate } from "react-router-dom";
const Login = () => {
  //navigate after login
  const navigate = useNavigate();
	
//step 3: 
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
	
	//step 4:
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
import { AuthContext } from "../../context/UserContext";
const Header = () => {
const {user} = useContext(AuthContext);
return (
	 <span>{user.email}</span>
    )
};

export default Header;
	
<!-- End intial set up -->
	
	
<!-- Full Example -->
//step 1 (create UserCompnet and export AuthContext)
//UserCOntext.js (component)
import {
  createUserWithEmailAndPassword,
  getAuth,
  onAuthStateChanged,
  signInWithEmailAndPassword,
  signInWithPopup,
  signOut,
  updateProfile
} from "firebase/auth";
import React, { createContext, useEffect, useState } from "react";
import app from "../Firebase/Firebase.init";

//AuthContext export
export const AuthContext = createContext();
const auth = getAuth(app);

const UserContext = ({ children }) => {
  const [user, setUser] = useState({});
  // loading state যাতে user page reload এর পরে same page এ থাকে।
  const [loading, setLoading] = useState(true);
	
//google login
  const googleLogin = (provider) => {
    return signInWithPopup(auth, provider);
  };
  //create user for firebase
  const createUser = (email, password) => {
    setLoading(true)
    return createUserWithEmailAndPassword(auth, email, password);
  };

  //sign in user for firebase
  const signIn = (email, password) => {
    setLoading(true)
    return signInWithEmailAndPassword(auth, email, password);
  };
// verifyEmail
  const verifyEmail = () => {
    return sendEmailVerification(auth.currentUser)
  };
//set profile and name
  const updateUserProfile = (profile) => {
    return updateProfile(auth.currentUser, profile);
  };

  //sign out user from ui
  const logOut = () => {
    setLoading(true)
    return signOut(auth);
  };

  //current user
  useEffect(() => {
    const unSubscribe = onAuthStateChanged(auth, (currentUser) => {
      console.log(currentUser, "current User ");
      setUser(currentUser);
      setLoading(false)
    });

    return () => unSubscribe();
  }, []);

  //send Data any where
  const authInfo = {
    user,
    loading,
    updateUserProfile,
    googleLogin,
    createUser,
    logOut,
    verifyEmail,
    signIn,
  };
  return (
    <AuthContext.Provider value={authInfo}>{children}</AuthContext.Provider>
  );
};

export default UserContext;

//step 2 (use AuthContext in Login.js )
// Login.js (component)
import React, { useContext } from "react";
import { Link, useLocation, useNavigate } from "react-router-dom";
import { AuthContext } from "../../context/UserContext";
	
const Login = () => {
//receive data from UserContext
  const { signIn, googleLogin } = useContext(AuthContext);
//google provider
  const googleProvider = new GoogleAuthProvider();
  //navigate after login
  const navigate = useNavigate();
  // call location
  const location = useLocation();
  const from = location.state?.from?.pathname || "/";
	
  //handleSubmit
  const handleSubmit = (event) => {
    event.preventDefault();
    //catch input field
    const form = event.target;
    const email = form.email.value;
    const password = form.password.value;

    //sign in user in firebase
    signIn(email, password)
      .then((result) => {
        const user = result.user;
        console.log(user);
        form.reset();
        //navigate
        navigate(from, { replace: true });
      })
      .catch((error) => console.error(error));
  };
	
//google sign in
  const handleGoogleSignIn = () => {
    googleLogin(googleProvider)
      .then((result) => {
        const user = result.user;
        console.log(user);
      })
      .catch((error) => console.error(error));
  };
	
  return (
	
	<form onSubmit={handleSubmit}>
	<input
	  type="text"
	  required
	  name="email"
	  placeholder="Email"
	  className="input input-bordered border border-[#95A0A7] rounded-[5px] h-14"
	/>
	<input
	  type="text"
	  required
	  name="password"
	  placeholder="Password"
	  className="input input-bordered border border-[#95A0A7] rounded-[5px] h-14"
	/>
	<button> Login </button>
      </form>
	//google sign in
	<Button
          onClick={handleGoogleSignIn}
          className="mb-2"
          variant="outline-primary"
        >
          Login with google <FcGoogle />
        </Button>
	
  );
};

export default Login;
	
	
	
//step 3 (use AuthContext in register.js )
// register.js (component)
import React, { useContext, useState } from "react";
import Button from "react-bootstrap/Button";
import Form from "react-bootstrap/Form";
import { Link, useNavigate } from "react-router-dom";
import { AuthContext } from "../contexts/AuthProvider";
const Register = () => {
  const [error, setError] = useState("");
  const [accepted, setAccepted] = useState(false);
  const { createUser, updateUserProfile, verifyEmail } = useContext(AuthContext);
const navigate = useNavigate();
  const handleSubmit = (event) => {
    event.preventDefault();

    const form = event.target;
    const name = form.name.value;
    const photoURL = form.photoURL.value;
    const email = form.email.value;
    const password = form.password.value;

    createUser(email, password)
      .then((result) => {
        const user = result.user;
        setError("");
        form.reset();
        navigate('/')
	//update profile
        handleUpdateUserProfile(name, photoURL)
	// verification email
	handleEmailVerification()
      })
      .then((error) => {
        console.error(error);
        setError(error.message);
      });
  };
// update profile img
  const handleUpdateUserProfile = (name, photoURL) => {
    const profile = {
      displayName:name,
      photoURL:photoURL
    };
    updateUserProfile(profile)
    .then(() => {})
    .then(error=> console.error(error))
  };
	
// handle email veriyfication
const handleEmailVerification = () => {
  verifyEmail()
  .then(() => {})
  .catch(error=> console.error(error))
};

  const handleAccepted = (event) => {
    setAccepted(event.target.checked);
    // const  = ;
  };

  return (
    <div>
      <Form onSubmit={handleSubmit} className="w-75 mx-auto">
        <Form.Group className="mb-3" controlId="formBasicEmail">
          <Form.Label>Your Name</Form.Label>
          <Form.Control type="text" name="name" placeholder="Your Name" />
        </Form.Group>

        <Form.Group className="mb-3" controlId="formBasicEmail">
          <Form.Label>Photo URL</Form.Label>
          <Form.Control name="photoURL" type="text" placeholder="Photo URL" />
        </Form.Group>

        <Form.Group className="mb-3" controlId="formBasicEmail">
          <Form.Label>Email address</Form.Label>
          <Form.Control
            name="email"
            type="email"
            placeholder="Enter email"
            required
          />
        </Form.Group>

        <Form.Group className="mb-3" controlId="formBasicPassword">
          <Form.Label>Password</Form.Label>
          <Form.Control
            name="password"
            type="password"
            placeholder="Password"
            required
          />
        </Form.Group>

        <Form.Group className="mb-3" controlId="formBasicCheckbox">
          <Form.Check
            onClick={handleAccepted}
            type="checkbox"
            label={
              <>
                Accept <Link to="/terms">Terms and conditions</Link>
              </>
            }
          />
        </Form.Group>

        <Button variant="primary" type="submit" disabled={!accepted}>
          Register
        </Button>

        <Form.Text className="text-muted text-danger">
          We'll
          {error}
        </Form.Text>
      </Form>
    </div>
  );
};

export default Register;

	
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

1. disabled checked and  Submit button
//step 1
 const [accepted, setAccepted] = useState(false);
//step 2
 const handleAccepted = (event) => {
    setAccepted(event.target.checked);
    // const  = ;
  };
//step 3
<Form.Check
    onClick={handleAccepted}
    type="checkbox"
    label={
      <>
	Accept <Link to="/terms">Terms and conditions</Link>
      </>
    }
  />
// step 4
 <Button variant="primary" type="submit" disabled={!accepted}>
  Register
</Button>
	
	

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
12. Have you ever used custom hook? For which task you used it? 
13. Do you need private route in project? 
14. How will create a private route?
15. What is the necessity of useRef hook?
16. Can you give me an example of where and how you would use React Router?
17. What is nested routing?
18. What are the differences between react-router-dom and react-router-native?
19. What are some ways that you can share data among routes in React Router?
20. Explain strict mood in react.
21. Why will you use dynamic route? 

	
	
	
	
	
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
        <td> Reset Form After Submit Form</td>
        <td>form.reset()</td>
      </tr>
      <!-- row 2 -->
      <tr>
        <th>2</th>
        <td> email valid</td>
        <td>/^\S+@\S+\.\S+$/ ,  const test = /^\S+@\S+\.\S+$/.test(event.target.value); </td>
      </tr>
      <!-- row 3 -->
      <tr>
        <th>3</th>
        <td> email valid </td>
        <td> const handleEmail = (event) => {
    const test = /^\S+@\S+\.\S+$/.test(event.target.value);
    if(!test){
      setError('Please give a valid email')
      return
    }
    setEmail(event.target.value);
    setError('')
  };</td>
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
