# React Using Method And Example

### 🔭 What is React Router?
- 
### 👯 Why use React Router?

###  🤔 How to Use ?

 <h4>রাউটার সেটাপ করার জাস্ট পাঁচটা স্টেপ-</h4>

```js
১. প্রথমেই তোমাকে BrowserRouter ইউজ করতে হবে index.js এ। 
২. তারপর আমরা App.js এ গিয়ে Routes সেট করবো। 
৩. তার ভিতরে থাকবে এক একটা Route  
৪. সেইসব Route এর মধ্যে থাকবে path 
৫. আর Route এর মধ্যে element নামে আরেকটা prop সেট করে দিবো তাহলেই কাজ শেষ।  
  
```


List of React:

- [NestedRoute](#NestedRoute)
- [CustomLink](#CustomLink)
- [dynamicRoute](#dynamicRoute)
- [simpleNavbarwithResponsive](#simpleNavbarwithResponsive)

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
<details>
<summary>
  <h4>simpleNavbarwithResponsive</h4>
</summary>
<br >
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
        <td>Brice Swyre</td>
        <td>Tax Accountant</td>
      </tr>
    </tbody>
  </table>
</div>



## 🌐 Socials: Connect with Emon Hossain!

[![Facebook Badge](https://img.shields.io/badge/Facebook-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://fb.com/emonhossain6) [![Linkedin Badge](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/emon007iu/) [![Twitter Badge](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/@emon_hossain7) [![Mail Badge](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:emon.hossain.wd@gmail.com)

<h4>❤️🤔 You can follow my Github and other social accounts 🤔❤️</h4>
<h2>❤️ Thank you very much! ❤️</h2>
