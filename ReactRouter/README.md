# React Using Method And Example

### 🔭 What is React Router?
- 
### 👯 Why use React Router?

### 🤔 How to Use ?
<details>
<summary>
  <h3>Router setup step by step(Click Me)</h3>
</summary>
<br >
	
```js
1. Install react router: npm i react-router-dom
2. crate a router use createBrowserRouter
import { createBrowserRouter } from 'react-router-dom';
const router = createBrowserRouter([

]);
3. Add RouterProvider and pass router props
import { createBrowserRouter, RouterProvider } from 'react-router-dom';
  return (
    <div className="App">
      <RouterProvider router={router}></RouterProvider>
    </div>
  );
4. Create some route inside the router
function App() {
  const router = createBrowserRouter([
    // Create some route inside the router
    { path: '/', element: <div>Default Page</div> },
    //set component in router
     { path: '/home', element: <Home/> },
    { path: '/about', element: <About/> },
  ]);
  return (
    <div className="App">
      <RouterProvider router={router}></RouterProvider>
    </div>
  );
}
// Thinks you need to create a route
1. crate a Link: so that you can go to this route
2. Crate component: to add what you will show once you go to that route
3. Add roter so that react router know the component it needs
to display it needs to display while you are visiting to that route
 <Link to='/home'>Home</Link>
<Link to='/about'>About</Link>


// another setup react router
1. Install react router: npm i react-router-dom
2. crate a router use createBrowserRouter
3. Add RouterProvider and pass router props
4. Create some route inside the router
5. Create Main layout with some common part and one changing part based on the router
const Main = () => {
  return (
    <div>
      <Header />
      <Outlet />
    </div>
  );
};
6. set main layout at the root of the router
7. set children routes
8. set links on the header components
function App() {
  const router = createBrowserRouter([
    {
      path: "/",
      element: <Root />,
      errorElement: <ErrorPage />,
      children:[
	//index দিলে default index true এর পেজ ui show kore.
	{ index: true, element: <Home /> },
        { path: "/home", element: <Home /> },
        { path: "/about", element: <About /> },
      ]
    },
    {path:'*', element: <div>404 ! page Not Found</div>}
  ]);

  return (
    <div className="App">
      <RouterProvider router={router} />
    </div>
  );
}

```
</details>


List of React Router:
- [useRouteError](#useRouteError)
- [conditionRendering](#conditionRendering)
- [ActiveNavLink](#ActiveNavLink)
- [loader](#loader)
- [PrivateRoute](#PrivateRoute)
- [updateDynamicRoute](#updateDynamicRoute)
- [NestedRoute](#NestedRoute)
- [CustomLink](#CustomLink)
- [dynamicRoute](#dynamicRoute)
- [simpleNavbarwithResponsive](#simpleNavbarwithResponsive)
- [Notes](#Notes)
- [ReactRouterInterviewQuestions](#ReactRouterInterviewQuestions)
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

### useRouteError
<details>
<summary>
  <h3> useRouteError -(Click Me)</h3>
</summary>
<br >
	
```js

Step 1:
{
path: "/",
element: <Home />,
errorElement: <ErrorPage />,
},
Step 2:
const error = useRouteError();
Step 3:
//full example
//App.js
function App() {
  const router = createBrowserRouter([
    {
      path: "/",
      element: <Home />,
      errorElement: <ErrorPage />,
    }
  ]);
  return (
    <>
      <Header />
      <RouterProvider router={router} />
    </>
  );
}

//ErrorPage component
import { useRouteError } from 'react-router-dom';
const ErrorPage = () => {
  const error = useRouteError();
  return (
    <>
      <div className='flex flex-col min-h-[700px] justify-center items-center'>
        {error && (
          <div>
            <p className='text-red-500'>{error.statusText || error.message}</p>
            <p>{error.status}</p>
          </div>
        )}
      </div>
    </>
  )
}

```
</details>

### conditionRendering
<details>
<summary>
  <h3> conditionRendering-(Click Me)</h3>
</summary>
<br >
	
```js
/* 
//condition Rendering 4 way
1. use element in a variable and use if - else to set value
2. ternary operation condition ? true :  false
3. && operator (if condition is true, i want to display something)
4. || operator (if condition is false, i want to display something)
*/
//full Example
const Cart = ({ cart, handleRemoveItem }) => {
  let message;
  if (cart.length === 0) {
    message = <p>Please buy at least one item!!</p>;
  } else if (cart.length === 1) {
    message = (
      <div>
        <h3>Aamr jonno ekta</h3>
        <small>Tomar jonno ekta</small>
      </div>
    );
  } else {
    message = <p>Thanks for buy</p>;
  }

  return (
    <div className="text-center " style={{ padding: "10px" }}>
      <h2 className={cart.length === 2? `orange` : `purple` }>Order Summary</h2>
      <h4 className={`bold ${cart.length === 2 ? 'orange' : 'blue'}`}>Order Quantity {cart.length}</h4>
      {cart.map((tShirt) => (
        <div key={tShirt._id}>
          <h3>
            {tShirt.name}{" "}
            <button
              onClick={() => {
                handleRemoveItem(tShirt);
              }}
            >
              X
            </button>
          </h3>
        </div>
      ))}
      {message}
      {cart.length >3 ? <p>gift 3 person</p> : <p>gift dibo na</p>}
      <p>&& operator</p>
      {
        cart.length === 2 && <h2>Double Item</h2>
      }
      <p>Or Operator</p>
      {
        cart.length === 4 || <p>Selected item na</p>
      }
    </div>
  );
};

```
</details>

### ActiveNavLink
<details>
<summary>
  <h3> Active Nav Link-(Click Me)</h3>
</summary>
<br >
	
```js
//Example 1
import { NavLink } from 'react-router-dom';
<NavLink className={(isActive) => isActive ? 'active' : undefined} to='/home' className='p-3 mr-3 hover:text-blue-700'>Home</NavLink>


//Example 2
let activeClass = {
    color: "#FF3811",
    background: "none",
 };
  
<li>
<NavLink
  to="/home"
  style={({ isActive }) => (isActive ? activeClass : undefined)}
>
  Home
</NavLink>
</li>

```
</details>


### loader
<details>
<summary>
  <h3> loader / Nested Route (Click Me)</h3>
</summary>
<br >
	
```js
// step 1: 
 {
  path: '/friends',
  loader: async () => {
    return fetch('https://jsonplaceholder.typicode.com/users')
  },
  element: <Friends />
},

//step 2: open <Friends /> component
const friends = useLoaderData();

//Full Example
//App.js
import { createBrowserRouter, RouterProvider } from 'react-router-dom';
import Friends from './components/Friends/Friends';
function App() {
  const router = createBrowserRouter([
    {
      path: '/',
      element: <Main />,
      children: [
        {
          path: '/friends',

          loader: async () => {
            return fetch('https://jsonplaceholder.typicode.com/users')
          },
          element: <Friends />
        },
      ]
    },
  ]);

  return (
    <>
      <RouterProvider router={router} />
    </>
  );
}

export default App;

// Friends components
//Friends.js
import React from 'react';
import { useLoaderData } from 'react-router-dom';

const Friends = () => {
    const friends = useLoaderData();
    
    return (
        <div>
            <h2>Friends {friends.length}</h2>
	    {
                friends.map(friend => <Friend
                    key={friend.id}
                    friend={friend}
                />)
            }
        </div>
    );
};

export default Friends;
```
</details>


### updateDynamicRoute
<details>
<summary>
  <h3> update Dynamic Route-(Click Me)</h3>
</summary>
<br >

```js
Module: 52-5 React route parameter and load data based on dynamic route

//step 1: 
//distructure
const {id} = friend;
//route set
<div class="card-actions justify-end">
	<Link to={`/friend/${id}`} class="btn btn-primary">{username}</Link>
</div>

//step: 2
{
  path: '/friend/:friendId',
  loader: async ({ params }) => {
    return fetch(`https://jsonplaceholder.typicode.com/users/${params.friendId}`)
  },
  element: <FriendDetails />
}
//step:3
//open <FriendDetails /> components
const FriendDetails = () => {
    const friend = useLoaderData();
    return (
        <div>
            <h2>Friend Details {friend.name}</h2>
        </div>
    );
};

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



### NestedRoute

```js
//step 1
<Route path='/posts' element={<Posts/>}>
   <Route path=':postId' element={<PostDetails/>}/>
 </Route>
  
 //step 2
import React, { useEffect, useState } from 'react';
import { Link, Outlet } from 'react-router-dom';

const Posts = () => {
    const [posts, setPosts] = useState([]);
    useEffect(() => {
        const url = 'https://jsonplaceholder.typicode.com/posts';
        fetch(url)
            .then(res => res.json())
            .then(data => setPosts(data))


    }, [])
    return (
        <div>
            <h2>Every posts facebook ever had: {posts.length}</h2>
            {
                posts.map(post =>
                    <Link
                        key={post.id}
                        to={`/posts/${post.id}`}
                    >
                        {post.id} </Link>
                )
            }
            // use outlet
            <Outlet/>
        </div>
    );
};

export default Posts;

 //step 3
import React, { useEffect, useState } from 'react';
import { useParams } from 'react-router-dom';

const PostDetails = () => {
    const {postId} = useParams();
    const [post, setPost] = useState({});
    useEffect(() => {
        const url = `https://jsonplaceholder.typicode.com/posts/${postId}`;
        fetch(url)
            .then(res => res.json())
            .then(data => setPost(data))
    }, [postId])
    
    console.log(post)
    
    return (
        <div>
            <h2>PostDetails for: {postId}</h2>
            <h4>{post.title}</h4>
            <p>{post.body}</p>
        </div>
    );
};

export default PostDetails;
```

### CustomLink

```js
//step 1
 create CustomLink component
 //step 2
 import { Link, useMatch, useResolvedPath } from 'react-router-dom';
 // change the function
 function CustomLink({ children, to, ...props }) {
    let resolved = useResolvedPath(to);
    let match = useMatch({ path: resolved.pathname, end: true });

    return (
        <div>
            <Link
                style={{ color: match ? 'red' : 'black', textDecoration: match ? "underline" : "none" }}
                to={to}
                {...props}
            >
                {children}
            </Link>
        </div>
    );
}
// step 3
// use CustomLink component
import CustomLink from '../CustomLink/CustomLink';
<CustomLink to='/'>Home</CustomLink>

```

### dynamicRoute

```js
// <h4>Example 1 (useNavigate)</h4>

//step 1
// import
import { useNavigate } from 'react-router-dom';

const navigate = useNavigate();
//step 2
// add event handeler
const showFriendDetails = (friend) => {
      const path = `/friend/${friend.id}`;
      navigate(path)
  };
<button onClick= {() => showFriendDetails(friend)} class="btn btn-primary">{friend.username}</button>
//step 3
//detail component
import { useParams } from 'react-router-dom';

const {friendId} = useParams();
<h2>This is Detail of a Friend: {friendId}</h2>

//step 4
//dynamic id use করে dynamic data load করতে চাইলে
const [friend, setFriend] = useState({});
 useEffect(() => {
     const url = `https://jsonplaceholder.typicode.com/users/${friendId}`;
     fetch(url)
     .then(res => res.json())
     .then(data => setFriend(data))
 }, [])
 
 <h2  className='underline text-center '>
     Name: {friend.name}</h2>
 <h2  className='underline text-center '>
     Email: {friend.email}</h2>
 <h2  className='underline text-center '>
     Website: {friend.website}</h2>


//<h4>Example 2 (Link)</h4>

//step 1
// create Details component and set Route in App.js
<Route path='/friend/:friendId' element={<FriendDetail/>} />

//step 2
 <Link to={'/friend/' + friend.id} class="btn btn-primary">Show Details</Link>
 or
 <Link to={`/friend/${friend.id}`} class="btn btn-primary">Show Details</Link>
 
 //step 3
//detail component
import { useParams } from 'react-router-dom';

const {friendId} = useParams();
<h2>This is Detail of a Friend: {friendId}</h2>

//FUll Detail Component Example

import React, { useEffect, useState } from 'react';
import { useParams } from 'react-router-dom';

const FriendDetail = () => {
    const {friendId} = useParams();
    
    const [friend, setFriend] = useState({});
    useEffect(() => {
        const url = `https://jsonplaceholder.typicode.com/users/${friendId}`;
        fetch(url)
        .then(res => res.json())
        .then(data => setFriend(data))
    }, [])
    

    return (
        <div>
            <h2  className='underline text-center '>This is Detail of a Friend: {friendId}</h2>
            <h2  className='underline text-center '>
                Name: {friend.name}</h2>
            <h2  className='underline text-center '>
                Email: {friend.email}</h2>
            <h2  className='underline text-center '>
                Website: {friend.website}</h2>
        </div>
    );
};

export default FriendDetail;

  
```



### simpleNavbarwithResponsive

  <h4>simpleNavbarwithResponsive</h4>


```js
  import { MenuIcon, XIcon } from '@heroicons/react/solid';
import React, { useState } from 'react';


const Navbar = () => {
    const [open, setOpen] = useState(false);
    const routes = [
        { id: 1, name: "home", link: '/home' },
        { id: 2, name: "shop", link: '/shop' },
        { id: 3, name: "Deals", link: '/deals' },
        { id: 4, name: "Contact", link: '/contact' }
    ];


    return (
        <nav className=''>
            <div onClick={() => setOpen(!open)} className='w-6 h-6 md:hidden'>
                {open ? <XIcon /> : <MenuIcon />}
            </div>
            <ul className={`md:flex p-4 justify-center bg-indigo-200 w-full absolute md:static duration-500 ease-in ${open ? 'top-35' : 'top-[-150px]'}`}>
                {
                    routes.map((route, index) =>
                        <li key={index} className='mr-12 block'>
                            <a href={route.link}>{route.name}</a>
                        </li>
                    )
                }
            </ul>
        </nav>
    );
};

export default Navbar;
  
```

### Notes
<details>
<summary>
  <h3>Notes for React Router (Click Me)</h3>
</summary>
<br >
  - Notes must be know every single part for interview 

```js

************React Router Notes************
//Milestone: 9 React Router and States
1. // Handle add to cart
  const tShirts = useLoaderData();
  const [cart, setCart] = useState([]);

  const handleAddToCart = (tShirts) => {
    const exists = cart.find(tSrt => tSrt._id === tShirts._id);
    if (exists) {
      alert("t-shirt already added");
    } else {
      const newCart = [...cart, tShirts];
      setCart(newCart);
    }
  };
	
// handle Add To Cart
const handleAddToCart = (product) => {
	setCart((previous=> [...previous, product]))
}
	
// Handle remove to cart
  const handleRemoveItem = tShirts=> {
    const remaining = cart.filter(tShirt => tShirt._id !== tShirts._id);
    setCart(remaining)
  };
	
2.
	
	
	
	

************End React Router Notes************
```
</details>
  
### ReactRouterInterviewQuestions
<details>
<summary>
  <h3>React Router Interview Questions (Click Me)</h3>
</summary>
<br >
 must be know every single part for interview https://roadmap.sh/react
	
 ```js
************React Router Interview Questions************
	
//Milestone: 9 React Router and States
//Module 54
1. When to use context api?
Ans: Context provides a way to share values between components without having to explicitly pass a prop through every level of the tree
To aboid prop drilling, we can use context api.
2. How is React routing different from conventional routing?
3. How do you implement React routing?
4. Can you explain how the Provider works with the React Context API?
5. What is a custom hook?
6. How many ways can we implement conditional rendering in React?
//Module 55.5
7. What is a server?
Ans: Ususally, servers are powerful computers connected via a network to a group of less powerfull cliend devices.
i. Stores, sends andf receives data.
ii. Accepts and responds to requests made over a network.
iii. As the name pimples, serves information to the computers connected to it.
iv. A computer, software program or even storage device may act as a server.
8. How does server work?
Ans: i. When you type a url, lets say (facebook.com) on your device, your device or your browser is client.
ii. Your device requests web content for facebook to the web server of Facebook Located somewhere in the datacenter.
iii. Then server gets the request from your device and sends data to your device.
This is just an example of how web server and web client work.

	
	
	
	
	
	
	
	
	
  ************End React Js Interview Questions************
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
        <td>useParams()</td>
        <td>useParams provite you object</td>
      </tr>
      <!-- row 2 -->
      <tr>
        <th>2</th>
        <td>props</td>
        <td>React a uopr theke eventhandler k  props akare data pathano jai, down theke up pathano jai na. r jodi pathate hoi tahole jai jaiga jabe seijaiga evnthandler dita hobe</td>
      </tr>
      <!-- row 3 -->
      <tr>
        <th>3</th>
        <td>map key</td>
        <td>{ posts.map((post, index) => post key={index} post={post})}</td>
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

[![Facebook Badge](https://img.shields.io/badge/Facebook-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://fb.com/emonhossain6) [![Linkedin Badge](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/emon007iu/) [![Twitter Badge](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/@emon_hossain7) [![Mail Badge](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:emon.hossain.wd@gmail.com)

<h4>❤️🤔 You can follow my Github and other social accounts 🤔❤️</h4>
<h2>❤️ Thank you very much! ❤️</h2>
