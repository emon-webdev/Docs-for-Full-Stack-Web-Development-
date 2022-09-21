# React Using Method And Example

### 🔭 What is React?
- 
### 👯 Why use React?
- 
###  🤔 How to Use?

List of React:
- [useState](#useState)
- [useEffect](#useEffect)
- [searchItems](#searchItems)
- [conditionalRendering](#conditionalRendering)
- [contextApi](#contextApi)
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

### useState
<details>
<summary>
  <h3>What is useState? (Click Me)</h3>
</summary>
<br >
  
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
  
 ```
</details>


### useEffect
<details>
<summary>
  <h3>What is useEffect? (Click Me)</h3>
</summary>
<br >
  
 ```js
import React, { useState, useEffect } from 'react';

//Example: 1
  const [users, setUsers] = useState([]);
  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(res => res.json())
      .then(data => setUsers(data))
  }, [])

//Example: 2
const User = () => {
    const [users, setUsers] = useState([]);
    useEffect(() => fetchData, [])
    const fetchData = async () => {
        const url = 'https://jsonplaceholder.typicode.com/users';
        const res = await fetch(url);
        const data = await res.json();
        setUsers(data)
    }
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

### contextApi
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
  <h4>What is localStorage and SessionStorage? (Click Me)</h4>
</summary>
<br >

```js
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
    
    
    

 // <h3>Local Storage Fake Db</h3>

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

```
</details>

### Notes
<details>
<summary>
  <h3>Notes for javaScript (Click Me)</h3>
</summary>
<br >
 Notes

```js

************Reat Notes************
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
2. 


```
</details>
  
### ReactJsInterviewQuestions
<details>
<summary>
  <h3>React Js Interview Questions (Click Me)</h3>
</summary>
<br >
  
 ```js
************React Js Interview Questions************
	
//Milestone: 8 Simple React
//Module : 44
1. What are components in react?
Ans: i. Building blocks of the user interface.
ii. Each component exists in the same space but works independntly
iii. All of the components are being merged in a parcent component (the final UI)
iv. Splits UI into independt and reusable pieces.
v. Re-usable having their own structure and methods.
2. What are single page applications (SPA)?
Ans i. Only one webpage, and each time something happens, only part of the page in reloaded while the rest of HTml remains unchanged.
ii. All use interaction with this service is carried out, using one screen (page)
iii. Load all the necessary HTML, CSS and JavaScript in the initial page load.
and then dynamically update thir DOM and retrieve extra data based on user interactions.
iv. Give the user the illusion that they are accessing different pages of paths.
v. Enables to combine a complex functionality of an MPA with a convenient navigation (a hybrid approach)
3. Advantage of single page applications?
i. linear navigation ii. instant loading iii. offline mode iv. native UX v. Feature rich UI vi.cross platform adaptability
vii. Flexibility ix. Quicker & cheaper developement
4. Disavantage of single page applications?	
i. seo issues ii. longer initial iii. no work under high loads iv. security issues v. low sealability vi. no history of visits.
5. What is Props?
Ans: Props হল data send করে একটা component থেকে অন্য comomponent এ। Props সব সময় Parent Component থেকে child Component এ data 
send করে। child থেকে send করা যায় কিন্তু system করে।
6. What is differens between Props and State ?
Ans: i. State => টা manage হই component এর ভিতর।
ii. Props => বাইরে comomponent থেকে current comomponent a data আসে আবার current comomponent থেকে অন্য comomponent data send করে।
7. What is the best between SPA and MPS?
8. Examples of SPA and MPA?
Ans: SPA => i. Facebook nes feed ii. Twitter iii. Trello iv.Pinterest v. Gmail vi. google Maps vii. Airbnb
MPS => i. Amazon ii. eBay iii. ALiexpress iv. Forbes v. Thumbtack vi. Angi
9. What is JSX? (JavaScript XML)
Ans: JavaScript এর মধ্যে html এর মতো code type করার ability. JSX এর সাহায্যে HTML code JavaScript এর code সহজেই type করা যাই।
100% Html না but Html এর Flever পাওয়া যায়।

	
	
  
 ```
</details>


### Table
	
<div class="overflow-x-auto">
  <table class="table w-full">
    <!-- head -->
    <thead>
      <tr>
        <th></th>
        <th>Name</th>
        <th>Answer</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th>17</th>
        <td> String</td>
        <td>String হচ্ছে imutable. এর মান বা value change করা যাই না.  </td>
      </tr>
       <!-- row 18 -->
      <tr>
        <th>18</th>
        <td> String</td>
        <td>  Apply Search includes, indexOf, startswith, endswith </td>
      </tr>
       <!-- row 19 -->
        <!-- row 18 -->
      <tr>
        <th>18</th>
        <td> destructing two way (valriable value swap)</td>
        <td> Array to Array /* [first, second] = [second, first] */, Object to Object </td>
      </tr>
    </tbody>
  </table>
</div>



## 🌐 Socials: Connect with Emon Hossain!

[![Facebook Badge](https://img.shields.io/badge/Facebook-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://fb.com/emonhossain6) [![Linkedin Badge](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/emon007iu/) [![Twitter Badge](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/@emon_hossain7) [![Mail Badge](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:emon.hossain.wd@gmail.com)

<h4>❤️🤔 You can follow my Github and other social accounts 🤔❤️</h4>
<h2>❤️ Thank you very much! ❤️</h2>
