# React Using Method And Example

### 🔭 What is React?
- React JS is a JavaScript library for building user interfaces.
- React JS is a declarative, efficient, and flexible.
- It is fast and component - based
- It Was initaially debeloped and maintained by Facebook.
##### must be know every single part for interview https://roadmap.sh/react

- React's Virtual DOM is a JavaScript representation of the actual DOM. 
When updates are made React compares the current DOM to the virtual DOM
and only updates the differences bettween the two.
React hot loaderis a plugin that allows React components to be live reloaded without the loss of state.

- History of React
i. 2021 - The first signs of React
ii. An early prototype of React
iii. Something new had started at Facebook.
iv. 2013 - The year of the Big Launch
- React Fundamentals (ReactJS)
- https://fahimahammed-cse.medium.com/react-fundamentals-reactjs-d4f0bd042bf8
### React কোর কনসেপ্ট:
https://fahimahammed-cse.medium.com/react-fundamentals-reactjs-d4f0bd042bf8
- কিভাবে create react app দিয়ে নতুন React app তৈরি করবে 
- কিভাবে কম্পোনেন্ট তৈরি করবে, এবং কম্পোনেন্ট ইউজ করবে
- props ইউজ করে কিভাবে কম্পোনেন্ট এ ডাটা সেন্ড করবে 
- destructuring ইউজ করে object এর প্রপার্টি ইউজ করবে 
- কিভাবে useState ইউজ করে স্টেট ডিক্লেয়ার করতে হয় 
- eventHandler দিয়ে কিভাবে স্টেট চেইঞ্জ করতে হয়।
- useEffect ইউজ করে কিভাবে API থেকে ডাটা লোড করতে হয়। লোড করা ডাটা কিভাবে দেখানো যায়
{
	"editor.fontFamily": "JetBrains Mono, Fira Code, Menlo, Monaco, 'Courier New', monospace",
	"editor.fontLigatures": true	
}

#### Compaines using React
- React
i. Instagram ii. Twitter iii. Facebook iv. yahoo v. abnhub
- Angular
i. Youtube ii. telegram iii. udemy iv. paypal
- Vue
i. gramarly ii. alibaba iii. mi
#### React JS popular features
i. Reusability ii. JSX iii. The props (easy data flow)
iv. The state v. virtual DOM vi. Boosts performance
vii. Simple to migrate viii.SEO friendly ix. Easier debugging x. Testing is fairty smooth

### 👯 When to use React JS?
Ans: i. React js has a simple design and uses JSX which makes it easy to learn and use, even for beginners.
ii. Owing to ites virtual DOM, ReacJS offers fast performance for applications.
iii. Being a view library, react does not force on the specific architecture of you application
iv. React alllows you to tailor your stack ass per your own project requerments by
giving you the freedom to chosse additional libraries.
v. React is backed and supported by Facebook, which makes it a top choice for many leading businesses.
So list of popular companies that use ReactJS below.

###  🤔 How to Use?
List of React:

- [Axios](#Axios)
- [useState](#useState)
- [useEffect](#useEffect)
- [ReactQueryTanStackQuery](#ReactQueryTanStackQuery)
- [dynamicTitle](#dynamicTitle)
- [searchItems](#searchItems)
- [conditionalRendering](#conditionalRendering)
- [useContext](#useContext)
- [handleAddtoCart](#handleAddtoCart)
- [handleRemoveFromCart](#handleRemoveFromCart)
- [customHooks](#customHooks)
- [ChildrenChange](#ChildrenChange)
- [Immutable](#Immutable)
- [searchItem](#searchItem)
- [localStorageSessionStorage](#localStorageSessionStorage)
- [Notes](#Notes)
- [ReactJsInterviewQuestions](#ReactJsInterviewQuestions)
- [Table](#Table)


### demo
<details>
<summary>
  <h3>Demo (Click Me)</h3>
</summary>
<br >
  
 ```js
Demo
	
  
 ```
</details>

### Axios
<details>
<summary>
  <h3>What is Axios? (Click Me)</h3>
</summary>
<br >
Axios and Fetch almost same. যখন অনেক api call করে তখন সহজেই api গুলো রোধ করে অন্য কাজ করতে পারে।
যেমন : i. api রোধ করে token collect করা।
More Details
https://axios-http.com/docs/intro
	
 ```js
Axios Features:
i.Make XMLHttpRequests from the browser
ii. Make http requests from node.js
iii. Supports the Promise API
iv. Intercept request and response
v. Transform request and response data
vi. Cancel requests
vii. Automatic transforms for JSON data
vii. Client side support for protecting against XSRF

//Example: Slag and split data 
//input
("slug": "apple_iphone_13_mini-11104",)
//output
{name: 'iPhone 13 mini', price: 11104}
	
"data": [
	{
	"brand": "Apple ",
	"phone_name": "iPhone 13 mini",
	"slug": "apple_iphone_13_mini-11104",
	"image": "https://fdn2.gsmarena.com/vv/bigpic/apple-iphone-13-mini.jpg"
	},
]
const [phones, setPhones] = useState([])
useEffect(() => {
axios.get('https://openapi.programming-hero.com/api/phones?search=iphone')
    .then(data => {
	const phonesLoaded = data.data.data;
	const phoneData = phonesLoaded.map(phone => {
	    const parts = phone.slug.split('-');
	    const price = parseInt(parts[1]);
	    const singlePhone = {
		name: phone.phone_name,
		price: price
	    };
	    return singlePhone;
	});
	console.log(phoneData)
	setPhones(phoneData)
    })
}, [])
console.log(phones)
	
  
 ```
</details>

### useState
<details>
<summary>
  <h3>What is useState? (Click Me)</h3>
</summary>
<br >
##### const [state, setState ] = useState( initialValue);
1. useState(0) কে dispatch বলে
2. [state, setState] এইটা refarence রাখে
3. setCount asynchronous
4. state asynchronous ভাবে update হয়।	
5. state variable er মতো কাজ করে
6. js এ data variable এর ভিতর রাখতে হয় but react এ useState এর ভিতর রাখতে হয়।
	
 ```js

// import
import React, { useState } from 'react';

const Example = () => {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
	
//Example 2 Toggole Flags (true / false)
const [mode, setMode] = useState(false)
const clickHandler = () => {
	setMode(!mode)	
}
const toggledClass = mode ? light : dark;
<button onClick={clickHandler} >Toggle Display</button>
  
 ```
</details>



### useEffect
<details>
<summary>
  <h3>What is useEffect? (Click Me)</h3>
</summary>

<br >
	
##### useEffect(() => {},[])
console.log('Hello World')
}, [dependancy])
1. dependancy injection এ যদি [] (empty array ) থাকে তাহলে এক বার call করে
2. যদি [products, cart] (array) এর ভিতর কিছু থাকলে সেইটার উপর useEffect টা depend করে ওইটার কোন change হলে 
useEffect আবার call করে। (যেমন products, cart ) এর উপর depend করছে
3. re-run effect when the values within the array change across re-renders
#### useEffect use cases
1. validating input field.
2. fetch API data
3. live filtering
4. trigger animation on new array value
5. Reading data from local storage
 ```js

import React, { useState, useEffect } from 'react';

//Example: 0
  const [control, setControl] = useState(false);

useEffect(() => {
	console.log('Hello World')
}, [control])
const handleEffect = () => {
setControl(!control)	
}
<button onClick={handleEffect}>Check Effect</button>

//Example: 1
useEffect(() => {
fetch('https://www.themealdb.com/api/json/v1/1/search.php?s=fish')
    .then(res => res.json())
    .then(data => {
	setMeals(data.meals)
    })
}, [])

//Example: 2
  const [users, setUsers] = useState([]);
  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(res => res.json())
      .then(data => setUsers(data))
  }, [])

//Example: 3
const User = () => {
    const [users, setUsers] = useState([]);
//Ex : 1
useEffect(() => fetchData, [])
//Ex: 2
  useEffect(() => {
  const loadCountries = async () => {
    const url = 'https://restcountries.com/v3.1/all';
    try {
      const res = await fetch(url);
      const data = await res.json();
      setCountries(data)
    } catch (error) {
      console.error(error)
    }
  }
  loadCountries ()
}, [])
	
  
	
return (
<>
    <h1>External User</h1>
    {
	users.map(user => {
	    const {name, email, id} = user;
	    return(
		<div key={user.id}>
		    <h1>Name: {name}</h1>
		    <h1>Email: {email}</h1>
		    <h1>Id: {id}</h1>
		</div>
	    )
	}
	)
    }
</>
)
}
  
 ```
</details>


### ReactQueryTanStackQuery
<details>
<summary>
  <h3>React Query or TanStack Query  (Click Me)</h3>
</summary>
<br >
  
 ```js

docs: https://tanstack.com/query/v4/docs/react/quick-start

//step 1: 
$ npm i @tanstack/react-query

//step 2: 

import {
  QueryClient,
  QueryClientProvider
} from "@tanstack/react-query";
const queryClient = new QueryClient();
//
<React.StrictMode>
    <QueryClientProvider client={queryClient}>
      <AuthProvider>
        <App />
      </AuthProvider>
    </QueryClientProvider>
  </React.StrictMode>
  
  
 const {
    data: appointmentOptions = [],
    refetch,
    isLoading,
  } = useQuery({
    queryKey: ["appointmentOptions", date],
    queryFn: async () => {
      const res = await fetch(
        `http://localhost:5000/v2/appointmentOptions?date=${date}`
      );
      const data = await res.json();
      return data;
    },
  });

  if (isLoading) {
    return <Loading />;
  }

	
{appointmentOptions.map((option) => (
  <AppointmentOption
    key={option._id}
    option={option}
    setTreatment={setTreatment}
  />
))}
	
  
 ```
</details>


### dynamicTitle
<details>
<summary>
  <h3>dynamic Title (Click Me)</h3>
</summary>
<br >
  
 ```js

// Step : 1
//Create useTitle.js hooks file
import { useEffect } from "react";

const useTitle = title => {
    useEffect(() => {
        document.title = `${title} - Website Name`
    }, [title])
};
export default useTitle;

//Step : 2 
// Import useTitle hooks in your components 
useTitle("Home");

<--Example --->

import { useEffect } from "react";

const useTitle = title => {
    useEffect(() => {
        document.title = `${title} - Website Name`
    }, [title])
};
export default useTitle;

import React from "react";
import useTitle from "../hooks/useTitle";
const Home = () => {
  useTitle("Home");
  return (
    <div>
      <h2>Dragon News: {allNews.length}</h2>
    </div>
  );
};

export default Home;
  
 ```
</details>



### searchItems
<details>
<summary>
  <h4>What is searchItems?</h4>
</summary>
<br >
- searchItems is


```js
//step 1 
//create input field and add event handeler
const handleSearchChange = (event) => {
    console.log(event.target.value)
};
<input onChange={handleSearchChange} type="search" placeholder="Search Mockups"/>
//step 2
//set useState
const [searchResult, setSearchResult] = useState([]);
 const handleSearchChange = (event) => {
      const searchText = (event.target.value);
      console.log(searchText)

      const match = tShirts.filter(tShirt => tShirt.name.includes(searchText))
      console.log(match)
      setSearchResult(match)
  };
  
  
  // full example
     const [searchText, setSearchText] = useState([]);
    const [searchResult, setSearchResult] = useState([]);
   
    useEffect(() => {
        console.log('inside the use effect')
        fetch('tShirts.json')
        .then(res => res.json())
        .then(data => {
            const match = data.filter(d => d.name.includes(searchText));
            setSearchResult(match)
        })
    }, [searchText])

    const handleSearchChange = (event) => {
        setSearchText(event.target.value);
    };

```
</details>

### conditionalRendering
<details>
<summary>
  <h4>What is conditionalRendering?</h4>
</summary>
<br >
- conditionalRendering is
</details>

```js
//step 1 
Conditional Rendering Options
1. Element Variable
let command;
if(cart.length === 0){
    command= <p>Please Add some items</p>
}else{
    command = <p>Thanks for adding item</p>
}
2. Ternary Operator (condition ? true : false)
3. true && condition (আগের condition true হইলে পরেরটা হবে)
4. false || condition (আগের condition false হইলে পরেরটা হবে)

```

### useContext
<details>
<summary>
  <h4>What is contextApi?</h4>
</summary>
<br >
- contextApi is . Context api using langguage changing, theme color changing.
</details>

```js
### Context Api
1. call createContext with a default getValue
2. set a variable of the context with uppercase
3. make sure you export the context to use it in other places
4. wrap you child context useing DemoContext.Provider
5. Provide a getValue
6. to consume the context from child Component
7. useContext hook and will you need to pass the contextName
====================
//step 1 
export const DemoContext = createContext('diamond');
// function er উপরে
const DemoContext = createContext('diamond');
//step 2
 const ornament = 'ring';
<DemoContext.Provider value={ornament}>
      <div>
          <h2>Grandpa</h2>
      </div>
  </DemoContext.Provider>
  // step 3 using
  import React, { useContext } from 'react';
  const ring = useContext(DemoContext);
  <p>{ring}</p>
  
  
<!-- Example -->
//step 1
//AuthContext.js (component)
import React, { createContext } from 'react';
export const AuthContext = createContext();
const AuthProvider = ({children}) => {
    const user = {name: 'Test Context'};
    const authInfo = {user};
    return (
        <AuthContext.Provider value={authInfo}>
            {children}
        </AuthContext.Provider>
    );
};
export default AuthProvider;

//step 2 
//index.js
import AuthProvider from "./contexts/AuthProvider";

  <React.StrictMode>
  //setup context
    <AuthProvider>
      <App />
    </AuthProvider>
  </React.StrictMode>
  

 //step 3 (use context)
 import React, { useContext } from "react";
 import AuthProvider from "../../contexts/AuthProvider";
 
 const {user} = useContext(AuthProvider);
console.log(user.name)

```

### handleAddtoCart
<details>
<summary>
  <h4>What is customHooks?</h4>
</summary>
<br >
- customHooks is
</details>

```js
//step 1 
const [cart, setCart] = useState([]);

    const handleAddtoCart = (selectedItem) => {
       const newCart = [...cart, selectedItem]
        setCart(newCart)
    };
    
    // যেই cart selet korso oi ta ase ki na check koro
    const handleAddtoCart = (selectedItem) => {
        const exists = cart.find(tShirt => tShirt._id === selectedItem._id);
        if (!exists) {
            const newCart = [...cart, selectedItem]
            setCart(newCart)
        }else{
            alert('item already added')
        }
    };
// step 2  
<Cart
  cart={cart}
/>
// step 3
// distucture
{ tShirt, handleAddtoCart }
<button onClick={() => handleAddtoCart(tShirt)}>Add to Cart</button>
```

### handleRemoveFromCart
<details>
<summary>
  <h4>What is handleRemoveFromCart?</h4>
</summary>
<br >
- handleRemoveFromCart is
</details>

```js
//step 1 
const [cart, setCart] = useState([]);
const handleRemoveFromCart = (selectedItem) => {
      const rest = cart.filter(tShirt => tShirt._id !== selectedItem._id);
      setCart(rest)
  };
// step 2  
<Cart
  cart={cart}
  handleRemoveFromCart={handleRemoveFromCart}
/>
// step 3
// distucture
{cart, handleRemoveFromCart}
 <button onClick={() => handleRemoveFromCart(tShirt)}>X</button>
```

### customHooks
<details>
<summary>
  <h4>What is customHooks?</h4>
</summary>
<br >
- customHooks is
</details>

```js
//step 1 create component and file
import { useEffect, useState } from "react";

const useProducts = () => {
    const [products, setProducts] = useState([]);

    useEffect(() => {
        fetch('products.json')
        .then(res => res.json())
        .then(data => setProducts(data))
        
    }, [])
    // step 2 return your need 
    return [products, setProducts];

};
// step 3 export function
export default useProducts;

```
### ChildrenChange
<details>
<summary>
  <h4>What is ChildrenChange?</h4>
</summary>
<br >
- ChildrenChange is
</details>

```js
//step 1 create component and file
// shop component
  <div className="cart-container">
      <Cart cart={cart}>
      //child route and button change 
          <Link to='/orders'>
              <button className='btn'>Review Order</button>
          </Link>
      </Cart>
  </div>
  //step 2 create component and file
  // order component
  <Cart cart={cart}>
   //child route and button change 
        <Link to='/inventory'>
            <button className='btn'>Proceed Checkout</button>
        </Link>
        // if do not use link then use just button then using
        import { Link, useNavigate } from 'react-router-dom';
        
        const navigate = useNavigate();
        
        <button onClick={() => navigate('/inventory')} className='btn'>Proceed Checkout</button>
    </Cart>
    
    //step 3 destructure
    const Cart = ({ children }) => {
          return (
              <div className="cart">
              //step 4 using
                  {children}
              </div>
          );
    };

```



### Immutable
<details>
<summary>
  <h4>What is Immutable?</h4>
</summary>
<br >
- useState is
</details>

```js
const [cart, setCart] = useState([]);

    const handleAddToCart = (product) => {
        //simple array push
        //cart.push(push)
        //array copy and new array create
        const newCart = [...cart, product];
        setCart(newCart)
    }
```
### searchItem
<details>
<summary>
  <h4>What is searchItem?</h4>
</summary>
<br >
- searchItem is
</details>

```js
  //step 1
    // create input filed and button
    <input onChange={searchFood} type="text" placeholder="Type here"/>
  //step 2
    // target input value
    const searchFood = (event) => {
        setSearchText(event.target.value)
  };
  //step 3
    //keep data
    const [searchText, setSearchText] = useState('');
    const [loadMeals, setLoadMeals] = useState([]);
  
  //step 4
  // call search api and daynamic
     //search api call
    useEffect(() => {
        const url = `https://www.themealdb.com/api/json/v1/1/search.php?s=${searchText}`;
        fetch(url)
            .then(res => res.json())
            .then(data => setLoadMeals(data.meals))
    }, [searchText])
  
  //step 5
    // map single items
      {
        loadMeals.map(loadMeal =>
                <div key={loadMeal.idMeal} className="single-meal card w-auto bg-base-100 shadow-xl">
                <figure className="">
                    <img src={loadMeal.strMealThumb} alt="Shoes" className="rounded-md" />
                </figure>
                <div className="card- p-4 items-center text-center">
                    <h2 className="card-title block  py-4 text-center">{loadMeal.strMeal}</h2>
                    <p>{loadMeal.strInstructions.slice(0, 100)}</p>
                    <div className="card-actions block py-3">
                        <button onClick={() => handleAddToOrder(loadMeal.meal)}>Order Now</button>
                    </div>
                </div>
            </div>
        )
      }
```


### localStorageSessionStorage

<details>
<summary>
  <h3>What is localStorage ? (Click Me)</h3>
</summary>
<br >
// clear Local storage 
1. Conceptual session:  Explore Sportsdb and Make your Own Sport Team -- Gias Uddin Hasan [26th September]]

i. Local storage Module: 47_5-5 Store multiple data in an Object with local storage
ii. 49-6 -> 49-8 (advanced) Add to the cart with quantity and explanation
iii. 
 ```js
************Local storage************
	
	
	
	
	
	
// Example 1 Full local storage
const Cosmetic = ({ cosmetic }) => {
    const { name, price, _id } = cosmetic;
    
    //use only one(advance, simple)
    //simple use localStorage
    const addToCart = (_id) => {
        // addToDb(_id)
        const quantity = localStorage.getItem(_id);
        if (quantity) {
            console.log('already exists')
            const newQuantity = parseInt(quantity) + 1;

            localStorage.setItem(_id, newQuantity)

        } else {
            console.log('new item')

            localStorage.setItem(_id, 1)
        }
    };
    
    // advance use LocalStorage
      const addToCart = (_id) => {
        // addToDb(_id)
        let shoppingCart;
        //get the shopping cart from local storage
        const storedCart = localStorage.getItem('shopping-cart');
        if (storedCart) {
            shoppingCart = JSON.parse(storedCart)

        } else {
            shoppingCart = {}
        }
        //add quantity
        const quantity = shoppingCart[_id];
        if (quantity) {

            const newQuantity = quantity + 1;
            shoppingCart[_id] = newQuantity;

        } else {
            shoppingCart[_id] = 1;
        }
        localStorage.setItem('shopping-cart', JSON.stringify(shoppingCart))
    };
    
      const removeFromCart = (_id) => {
        console.log('removing', _id)
        
    }

    return (
        <div className='product'>
            <h2>Buy this: {name}</h2>
            <h4>Only for: $ {price}</h4>
            <h5>Id : {_id}</h5>
            <button onClick={() => addToCart(_id)} >Add to Cart</button>
        </div>
    );
};

	
//Example 2

// localStorage connect to ui
useEffect(() => {
if (products.length) {
    const storedProductIds = getFromLocalStorage();
    const previousCart = [];

    for (const id in storedProductIds) {
	const foundProduct = products.find(product => product.id === id);
	if(foundProduct){
	    const quantity = storedProductIds[id];
	    foundProduct.quantity = quantity
	    previousCart.push(foundProduct)
	}
    }
    setCart(previousCart)
}

}, [products])

//Example 3
// Local Storage Fake Db
// use local storage to manage cart data
const addToDb = id =>{
// set localStorage
    let shoppingCart = {};

    //get the shopping cart
        // যেই নামে setItem করা হইছে সেই নামে পেতে হবে/
        const storedCart = localStorage.getItem('shopping-cart');
        if(storedCart){
            console.log(storedCart)
            // local store data save হই string হিসাবে  সেইটা getItem করার সময় normal javascript a conver korta hoi
            // সেই জন্য JSON.parse(storedCart) করা লাগে।
            shoppingCart = JSON.parse(storedCart)

        }

    // add quantity
   const quantity = shoppingCart[product.id];
        if (quantity) {
            // const newQuantity = quantity + 1;
            shoppingCart[product.id] = quantity + 1;

        } else {
            shoppingCart[product.id] = 1;
        }
        
    // local storage name set
        // step 1 key and value দুইটাই object হওয়া লাগবে;
        // step 2 object কে string convert korar jonno JSON.stringify(shoppingCart) করা লাগবে।
        localStorage.setItem('shopping-cart', JSON.stringify(shoppingCart))
}

const getStoredCart = () =>{
    let shoppingCart = {};

    //get the shopping cart from local storage
    const storedCart = localStorage.getItem('shopping-cart');
    if(storedCart){
        shoppingCart = JSON.parse(storedCart);
    }
    return shoppingCart;
}

const removeFromDb = id =>{
    const storedCart = localStorage.getItem('shopping-cart');
    if(storedCart){
        const shoppingCart = JSON.parse(storedCart);
        if(id in shoppingCart){
            delete shoppingCart[id];
            localStorage.setItem('shopping-cart', JSON.stringify(shoppingCart));
        }
    }
}

const deleteShoppingCart = () =>{
    localStorage.removeItem('shopping-cart');
}

export {
    addToDb,
    getStoredCart,
    removeFromDb,
    deleteShoppingCart
};- Find is used to conditionally find the first element in an array. If more than one element meets the condition, find returns the first element.	
	
	
  ************End Local storage************
 ```
</details>



### Notes
<details>
<summary>
  <h3>Notes for javaScript (Click Me)</h3>
</summary>
<br >
  - Notes must be know every single part for interview https://roadmap.sh/react

```js

************React Notes************
//Milestone: 8 Simple React
//Module : 44
1. Rypes of Component.
Ans: i. similar in look, differnt in data
ii. container component
iii. no common pattern but breakdown for working purpose
v. stand alone component
	
2. advantages of components.
i. code re-usability ii. Fast development iii. Design consistency iv. Maintainablility 
//Module : 45
1. React inline style
<div style={{border: '2px solid red', margin: '20px'}}>
	<p>Hello world</p>
</div>
	
3. //export import
Ans: i. //create utilites file
const add = (first, second) => {
    return first + second;
};
const multiply = (first, second) => {
    return first * second;
};
export { add, multiply, getTotalPrice as getTotal };
i. // import utilites file
import { add, multiply } from '../../utilities/calculator';
iii. //uses
const Shoes = () => {
    const first = 13;
    const second = 11;
    const result = multiply(first, second);
    const sum = add(first, second);
    return (
        <div>
            <p>result {result}</p>
            <p>sum {sum}</p>
        </div>
    );
};
	
4. //card total price sum (Module: 49-3 )
//Example 1
//import cart (array like obj)
let total = 0;
for (const product of cart) {
console.log(product.price)
total = total + product.price
}
//Example 2
//import cart (array like obj)
//total price
const totalReducer = (prv, curr) => prv + curr.price;
const total = cart.reduce(totalReducer, 0);
//total shipping
const shippingReducer = (prv, curr) => prv + curr.shipping;
const shipping = cart.reduce(shippingReducer, 0);
//Tax (string to number convert)
const tax = parseFloat((total * 10 / 100).toFixed(2));
// Grand price
const grandTotal = (total + shipping + tax).toFixed(2);
	
5. conceptual session expoloar sport db (gias vai)
//filter remove from cart list
    // delete from cart
    const handleDelete = (idMeal) => {
        const newCart = cart.filter(singleCart => singleCart.idMeal !== idMeal);
        setCart(newCart)
    };
	
6. React Hooks uses?
Ans: Hooks were first introuced in react 16.8 . They let us use more of react features like Managing our component state, 
or performing an after effect when certain changes occur in state without writing a class.
7. React togle Click
import { Bars3Icon, XMarkIcon } from '@heroicons/react/24/solid';
const [open, setOpen] = useState(false);		
{
open ?
<XMarkIcon onClick={() => { setOpen(!open) }} className="h-6 w-6 " />
:
<Bars3Icon onClick={() => { setOpen(!open) }} className="h-6 w-6 " />
}
	
	
	
	
	
	
	

************End React Notes************
```
</details>
  
### ReactJsInterviewQuestions
<details>
<summary>
  <h3>React Js Interview Questions (Click Me)</h3>
</summary>
<br >
 must be know every single part for interview https://roadmap.sh/react
	
 ```js
************React Js Interview Questions************
	
//Milestone: 8 Simple React
//Module : 44
0. What is React?
Ans:
1. What are components in react?
Ans: i. Building blocks of the user interface.
ii. Each component exists in the same space but works independntly
iii. All of the components are being merged in a parcent component (the final UI)
iv. Splits UI into independt and reusable pieces.
v. Re-usable having their own structure and methods.
vi. Markup language & logic কে আলাদা file এ না রেখে একই সাথে প্রয়োজনমত একই file এ রাখা যায়।
এর জন্য React component ব্যবহার করা হয়।
2. What are single page applications (SPA)?
Ans i. Only one webpage, and each time something happens, only part of the page in reloaded
while the rest of HTml remains unchanged.
ii. All use interaction with this service is carried out, using one screen (page)
iii. Load all the necessary HTML, CSS and JavaScript in the initial page load.
and then dynamically update thir DOM and retrieve extra data based on user interactions.
iv. Give the user the illusion that they are accessing different pages of paths.
v. Enables to combine a complex functionality of an MPA with a convenient navigation (a hybrid approach)
3. Advantage of single page applications?
i. linear navigation ii. instant loading iii. offline mode iv. native UX v. Feature rich UI vi.cross platform adaptability
vii. Flexibility ix. Quicker & cheaper developement
4. Disavantage of single page applications?	
i. seo issues ii. longer initial iii. no work under high loads iv. security issues v. low sealability vi.
no history of visits.
5. What is Props?
Ans: Props হল data send করে একটা component থেকে অন্য comomponent এ। Props সব সময় Parent Component থেকে 
child Component এ data  send করে। child থেকে send করা যায় কিন্তু system করে করা যায়।
Ans: We use props in React to pass data from one component to another (from a parent component to a child component)
6. What is differens between Props and State ?
Ans: i. State => টা manage হই component এর ভিতর।
ii. Props => বাইরে comomponent থেকে current comomponent a data আসে আবার current comomponent থেকে
অন্য comomponent data send করে।
7. What is the best between SPA and MPS?
8. Examples of SPA and MPA?
Ans: SPA => i. Facebook nes feed ii. Twitter iii. Trello iv.Pinterest v. Gmail vi. google Maps vii. Airbnb
MPS => i. Amazon ii. eBay iii. ALiexpress iv. Forbes v. Thumbtack vi. Angi
9. What is JSX? (JavaScript XML)
Ans:i. JSX JavaScript XML
ii. JavaScript এর মধ্যে html এর মতো code type করার ability. JSX এর সাহায্যে HTML code JavaScript এর code সহজেই type করা যাই।
100% Html না but Html এর Flever পাওয়া যায়। JSX এর ভিতর powerfull JS map, filter find সহজেই করা যায় {} এর মাধমে ।
propery এর ভিতর dynamic expresion লিখা যায়।
iii. Markup language & logic কে আলাদা file এ না রেখে একই সাথে প্রয়োজনমত একই file এ রাখা যায়।
এর জন্য React component ব্যবহার করা হয়।
iv. JSX is a syntax extension for React JS
v. Easier to read and write
vi. Gets transpiled to JavaScript with BABEL.

//Module : 47 (How React Works)
10. npm and npx diffrence?
Ans: npm: Node package manager
11. What is Babel Compiler?
Ans Babel হল free & open source javascript Transpiler যা EcmaScript এর newer version কে previous verions a convert করে .
12. what are the JSX Benifits?
Ans: One of the advantages of JSX is that React creates a virtual DOM 
(a virtual representation of the page) to track changes and updates.
13. how props works?
Ans: props works an Unidirectional data flow (one way binding). props এর  value set করা যাই না এটা readonly.
14. What is React JS?
Ans: i. React JS is a JavaScript library for building user interfaces.
ii. React JS is a declarative, efficient, and flexible.
iii. It is fast and component - based
iv. It Was initaially debeloped and maintained by Facebook.
15. More About React JS.
Ans: React's Virtual DOM is a JavaScript representation of the actual DOM. 
When updates are made React compares the current DOM to the virtual DOM and only updates the differences bettween the two.
16. React VS Angular VS Vue ? (important)
Ans: React VS Angular.....
 - Library VS Framework =>
i. React is a JavaScript library. Angular is a complate framework built on TypeScript - a superset of JavaScript.
ii. ReactJS is a smaller piece of the overall puzzle, whereas Angular is a collection of all different puzzle pieces.
- Architecture => 
i. React JS is responsible for the 'view' element of application development in a Model-View-Controller (MVC) framework.
ii. Angular is a complete MVC framework for front-end development.
- Components => 
i. React JS is a library for building and rendering components.
ii. Angular is not only about components, it offers more solutions that simply create components such as routing.
state management, form validations, and other tools that you need to develop large applications.
- Performance => 
i. The virtual DOM feature of ReactJS allows its application to virtually update
ii. the changes without rewriting the entire HTML document, this renders updates much quicker.
iii. The regular DOM feature of Angular makes the application slow in performance,
especially when comared to applications built using ReactJS.
- Data bunding =>
i. React js supports unidirectional data binding, or what is commonly known as one way data binding,
means that data flows one way while synchronising the model and view.
ii Angular data binding model is bi-directional, meaning that there is a two-way flow of data between the Model and the View.
- Scalability => 
i. React applications requires you to rely on third-party tools and supporting integrations external to React JS.
ii. Angular includes additional tools like routing, state management, HTTPS, ete. which help you build large-scale apps,
eans it comes packed with all the core features that you may require.
- Learning curve =>
i. React Js uses (JavaScript XML). which is fairly easy to learn if you have prior experience with writng code in JavaScript.
ii. A beginner need to familiarise with the TypeScript language that Angular uses.

17. When to use React JS?
Ans: i. React js has a simple design and uses JSX which makes it easy to learn and use, even for beginners.
ii. Owing to ites virtual DOM, ReacJS offers fast performance for applications.
iii. Being a view library, react does not force on the specific architecture of you application
iv. React alllows you to tailor your stack ass per your own project requerments by
giving you the freedom to chosse additional libraries.
v. React is backed and supported by Facebook, which makes it a top choice for many leading businesses.
So list of popular companies that use ReactJS below.

18. module=> 47-7 How react works, Render, virtual dom, diff algorithm, fiber	
19. React এ প্রতিটা component 3ta stage অতিক্রম করে।
i. Mounting
=> initial stage.যখন কোন component DOM এ প্রবেশ করে তখন আই stage শুরু হয়। আই stage এ ৪ টি method ঘটে।
- constructor() - getDerivedStateFromProps() - render() - componentDidMount()
ii. Update
যখন কোন props and state এর পরিবর্তন ঘটাই 
iii. Unmounting
যখন DOM থেকে কোন component  সরানোর প্রয়োজন হয়।
20. Props driling?
Ans: Prop drilling is a method where we pass a props with another componet with the help of 
all the components that come between them.
21. state vs props?
Ans:
22. React Hooks?
i. Hooks were added to React in version 16.8
ii. hooks allow function components to have access to state and other React features.
iii. Hooks allow us to "hook" into React features such as state and lifecycle methods.
- useState hook
iv. The useState hook allows us to track state in a function component.
22.1 What is useState?
Ans: i. Allows to have state variables in functional components.
ii. Takes the inital state to this function.
iii. Returns a variable with the current state value and another function to update this value.
// use cases of useState()
i. State management
ii. conditional rendering
iii. Toggle flages (true/ false)
iv. Counter
v. Store API data in sate.

23. useEffect Hook?
Ans: The useEffect Hook allows you to perform side effects in your components.  Preforms asynchronuous tasks.
Some examples of side effets area: 
i. fetching data.
ii. directly updating the DOM and timers.
24. What is Virtual DOM?
Ans: i. Lightweight copy of a DOM object
ii. Has propeties the same as real DOM object
iii. Make changes in the Dom with the help of the Diff Algorithm
iv. It's like: instead of moving actual rooms in a house, you edit the blueprint.
25. How does work virtual dom?
Ans: dom a কোন কিছু change হলে virtual dom বুজে যাই virtual dom এর ভিতর কোথাই change হইছে। 
then virtual dom Real dom er সাথে compatre করে শুধু change হওয়াটা update করে।
26. what is the difference between class component and functional component?
Ans: 
27. What are react lifecycle methods?
Ans: 
28. What are hooks? Tell us the role of useState and useEffet?
Ans: 
29. What is diff algorithm?
Ans: 
30. What is the difference between attribute and property?
Ans: 

//Module 50.5
31. What is state in react? (M- 50_5-1)
Ans: i. A built in react object
ii. Used to contain data about the component
iii. Cangeable over time
iv. React Component rendering and states are dependent
32. What is the useEffect cleanup function? and why uses ?
Ans:
//Example 1
useEffect(() => {
effect();
return() => {
	cleanup();
}
}, [])
33. What is Render in React?
Ans: Reader technically means to provide serviced. React schedules a render every time the sate of a component changes.
35. defference of SSR and CSR? // MOdule 50_5-3 (important)
1. SSR (Server Side Rendering)
Ans: 
2. CSR (Client Side Rendering)
CRS is a technique where all the pagte resoures are rendered on the client brower rather than the server.
	
	
	

	
	
  ************End React Js Interview Questions************
 ```
</details>

## Virtual DOM vs Real DOM

<div class="overflow-x-auto">
  <table class="table w-full">
    <!-- head -->
    <thead>
      <tr>
        <th>1</th>
        <th>Virtual DOM</th>
        <th>Real DOM</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th>2</th>
        <td>Dom mainipulation is very easy</td>
        <td>Dom mainipulation is very expensive </td>
      </tr>
       <!-- row 18 -->
      <tr>
        <th>3</th>
        <td>No memory wastage </td>
        <td> There is too much memory wastage </td>
      </tr>
       <!-- row 19 -->
        <!-- row 18 -->
      <tr>
        <th>4</th>
        <td> It updates fast</td>
        <td>  It updates Slow</td>
      </tr>
	       <!-- row 18 -->
	<tr>
        <th>5</th>
        <td>It can't update HTML directly </td>
        <td> It can update HTML directly </td>
      </tr>
	       <!-- row 18 -->
	<tr>
        <th> 6</th>
        <td> It is only a virtual representation of the DOM </td>
        <td> It represents the UI of you application </td>
      </tr>
	         <!-- row 8 -->
	<tr>
        <th> 7</th>
        <td>Update the JSX if the element update </td>
        <td> Create a new DOM if the element updates </td>
      </tr>
	         <!-- row 9 -->
	<tr>
        <th> 8</th>
        <td>It can produce about 200,000 virtual DOM Nodes/ Second </td>
        <td> It allows us to directly target any specific node  </td>
      </tr>
	    
    </tbody>
  </table>
</div>


### Angular vs React vs Vue
	
<div class="overflow-x-auto">
  <table class="table w-full">
    <!-- head -->
    <thead>
      <tr>
        <th>Attributes</th>
        <th>Angular</th>
        <th>React</th>
	<th>Vue</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th>Type</th>
        <td>JavaScript framework </td>
        <td>Open Source Js Library </td>
	<td> Progressive JavaScript Framework</td>
      </tr>
       <!-- row 18 -->
      <tr>
        <th>Coding speed</th>
        <td>SLow </td>
        <td> Normal </td>
	 <td>Fast </td>
      </tr>
       <!-- row 19 -->
        <!-- row 18 -->
      <tr>
        <th>Performance</th>
        <td> OK</td>
        <td> OK</td>
	<td> OK</td>
      </tr>
	       <!-- row 18 -->
	<tr>
        <th>Startup Time</th>
        <td>Longer due to its large codebase </td>
        <td> Quick</td>
	<td>Quick </td>
      </tr>
	       <!-- row 18 -->
	<tr>
        <th>Complete web apps</th>
        <td> Can be used on standalone basis</td>
        <td>Needs to be integrated with many other tools </td>
	<td> Requires third party tools</td>
      </tr>
	       <!-- row 18 -->
	<tr>
        <th>Data binding</th>
        <td> Bi-directional </td>
        <td> uni-derectional </td>
	<td>  Bi-directional</td>
      </tr></td>
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
        <th>1</th>
        <th>Problem</th>
        <th>Answer</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th>1</th>
        <td>export () </td>
        <td>export { add, multiply, getTotalPrice as getTotal };</td>
      </tr>
       <!-- row 18 -->
      <tr>
        <th>2</th>
        <td>React Toggle Click (true/false) </td>
        <td> const [open, setOpen] = useState(false); <Bars3Icon onClick={() => { setOpen(!open) }} className="h-6 w-6 " /> </td>
      </tr>
       <!-- row 19 -->
        <!-- row 18 -->
      <tr>
        <th>3</th>
        <td> Condition </td>
        <td>
	{details.length > 200 ? (
              <p>
                {details.slice(0, 250) + "..."}{" "}
                <Link to={`'/news/${_id}`}>Read More</Link>
              </p>
            ) : (
              <p>{details}</p>
           )}
	    </td>
      </tr>
	       <!-- row 18 -->
	<tr>
        <th>4</th>
        <td>Longer due to its large codebase </td>
        <td> Quick</td>
      </tr>
    </tbody>
  </table>
</div>


## 🌐 Socials: Connect with Emon Hossain!

[![Facebook Badge](https://img.shields.io/badge/Facebook-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://fb.com/emonhossain6) [![Linkedin Badge](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/emon007iu/) [![Twitter Badge](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/@emon_hossain7) [![Mail Badge](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:emon.hossain.wd@gmail.com)

<h4>❤️🤔 You can follow my Github and other social accounts 🤔❤️</h4>
<h2>❤️ Thank you very much! ❤️</h2>
