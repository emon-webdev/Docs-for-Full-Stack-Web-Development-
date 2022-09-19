# React Using Method And Example

### 🔭 What is React?
- 
### 👯 Why use React?
- 
###  🤔 How to Use?

List of React:
- [PrerequisitesOfReact](#PrerequisitesOfReact)
- [searchItems](#searchItems)
- [conditionalRendering](#conditionalRendering)
- [contextApi](#contextApi)
- [handleAddtoCart](#handleAddtoCart)
- [handleRemoveFromCart](#handleRemoveFromCart)
- [customHooks](#customHooks)
- [ChildrenChange](#ChildrenChange)
- [useState](#useState)
- [useEffect](#useEffect)
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

### PrerequisitesOfReact
<details>
<summary>
  <h3>তুমি react এর জন্য রেডি কিনা, বোঝা যাবে আজকে (Click Me)</h3>
</summary>
<br >

```js

 জাভাস্ক্রিপ্ট এর একজন জুনিয়র ডেভেলপার হওয়ার জন্য যা যা লাগে সেগুলোর একটা লিষ্ট এর মতো করে দিয়েছি যাতে এই টপিকগুলো দেখে  তুমি নিজেও বুঝতে পারো।
আজকের জাভাস্ক্রিপ্ট এর কনসেপ্টগুলো React এ গেলে কাজে লাগবে।

১. কিভাবে let, const দিয়ে ভেরিয়েবল লিখতে হয়,কখন কোনটা ইউজ করে তুমি কি জানো ?var নামক একটা জিনিস আছে সেটাও জানতে হবে।
২.১ কিভাবে কন্ডিশন লিখতে হয়, ছয় রকমের কন্ডিশন (>, <, >=, <=,  ==, !=,  ===, !==) কোনটা কোন জিনিসের জন্য ইউজ করবে। এছাড়াও && বা ।। দিয়ে কিভাবে একাধিক কন্ডিশন এর মধ্যে দুইটাই ফুলফিল করতে হবে আবার দুইটার যেকোন একটা ফুলফিল করতে হবে, সেটা কিভাবে করবে।
২.২. এক বা একাধিক কন্ডিশন দিয়ে কিভাবে if-else লিখে আবার কখন if-else if - else লিখে। সেই রকম একটা উদারহণ চিন্তা করে তুমি লিখে ফেলো। else ছাড়া শুধু if দিয়েও কন্ডিশন লিখো। একটা if অনেকগুলা else if এবং লাস্টে একটা else এর কন্ডিশন লিখো। হতে পারে গ্রেডিং বের করার জন্য কন্ডিশন লিখবে তুমি।
৩. array কিভাবে ডিক্লেয়ার করে array এর মধ্যে length, index, push, pop, indexOf, includes এইগুলা কিভাবে কাজ করে। কোনটা দিয়ে কি করে? সেগুলা কি তুমি জানো? কোন একটা জিনিস array কিনা সেটা চেক করার সিস্টেম জানতে হবে। আরেকটু ভালো হয় slice এবং splice জানলে। আরো বোনাস কিছু জানতে চাইলে shift, unshift, join দেখতে পারো। এডভান্স হিসেবে reduce দেখতে পারো।
৪. দুইটা বেসিক লুপ ,এর মধ্যে for loop তোমাকে জানতেই হবে। while লুপটাও দেখে রাখতে পারো। যদিও আমরা এই দুইটা লুপই কম ইউজ করবো। তাও কখনো লাগলে যেন তুমি বুঝে ফেলতে পারো। এছাড়া কখন for of আর কখন for in ইউজ করবে সেটা তুমি জানো।
৫. function একটা অবশ্য জিনিস। বিশেষ করে সিম্পল একটা ফাংশন কখন ডিক্লেয়ার করতে হয়। কখন ফাংশন থেকে return করে। আর কখন করে না। আর কিভাবে ফাংশন এর মধ্যে parameter নিতে হয়। কিভাবে কল করে। ফাংশন এর রিটার্ন কোন ভেরিয়েবলে রেখে সেই ভেরিয়েবল নিয়ে কিভাবে কাজ করে।
৬. আখেরি রত্ন হচ্ছে Object তাই কোন একটা অবজেক্ট কিভাবে ডিক্লেয়ার করে। সেখান property কিভাবে কিভাবে একসেস করা যায়। এছাড়াও অবজেক্ট এর প্রপার্টি এর ভ্যালু হিসেবে কিভাবে array, object ইউজ করা যায়।
.
সিম্পল বেসিক কয়েকটা ডাটা টাইপ সম্পর্কে জানতে হবে।
১. string কি জিনিস। স্ট্রিং কেমনে ডিক্লেয়ার করে। স্ট্রিং থেকে কিভাবে কোন একটা ক্যারেক্টার খুঁজে বের করে। চাইলে স্ট্রিং এর উপরে কি লুপ চালানো যায়। এছাড়াও length, includes, indexOf, toUpperCase, toLowerCase, জানতেই হবে। subString, concat জানলে ভালো। বোনাস হিসেবে জানতে পারো string কি mutable নাকি immutable
২. number সম্পর্কে জানতে হবে। integer, float কোনগুলা। স্ট্রিং থেকে নাম্বারে রূপান্তর করার সিস্টেম। কোন একটা সংখ্যা integer কিনা সেটা চেক করার সিস্টেম জানতে হবে। NaN বলতে একটা জিনিস আছে। সেটা কি জিনিস।
৩. true false কখন ইউজ  করে। সেটা জানতে হবে। কি কি ধরনের জিনিস জাভাস্ক্রিপ্ট এর truthy আর কি কি জিনিস জাভাস্ক্রিপ্ট এ falsy সেটা জানতে হবে।
৪. null এবং undefined কি জিনিস। কখন কোনটা ইউজ করা হয়। বা কখন কোনটা কিভাবে চেক করতে হয়। সেটা জানতে হবে।
ES6 রিলেটেড সাতটা জিনিস তোমাকে জানতে হবে
১. একটা টেম্পলেট স্ট্রিং দিয়ে একটা স্ট্রিং ভেরিয়েবল ডিক্লেয়ার করো। সেটার মধ্যে অবজেক্ট এর প্রপার্টি এর মান কিভাবে বসায় সেটা জানতে হবে। বিশেষ করে নেস্টেড অবজেক্ট আছে সেটার প্রপার্টি থেকে। বা কোন একটা অবজেক্ট এর প্রপার্টি array সেই array থেকে ভ্যালু এনে কিভাবে টেমপ্লেট স্ট্রিং এর মধ্যে বসাতে পারবে ।
২. স্প্রেড অপারেটর (...) কিভাবে কাজ করে। বিশেষ করে একটা array কে কপি করে নতুন করে array বানাবে এবং সেখানে একটা উপাদান যোগ করবে। আবার একটা উপাদান কে বাদ দিয়ে বাকি সব উপাদানকে কিভাবে যোগ করবে (filter ইউজ করে)
৩.১. শূন্য প্যারামিটারওয়ালা একটা অ্যারো ফাংশন কিভাবে লিখে। উদাহরণ হিসাবে তুমি এখন একটা অ্যারো ফাংশন লিখবে যেটা ৯ রিটার্ন করবে।
৩.২. এক প্যারামিটার ওয়ালা একটা অ্যারো ফাংশন ডিক্লেয়ার করবে। এই ফাংশনের কাজ হবে যে প্যারামিটার নিবে সেটাকে ১২ দিয়ে গুণ করে গুণফল রিটার্ন করবে।
৩.৩ দুই, প্যারামিটার ওয়ালা একটা অ্যারো ফাংশন লিখবে। এই ফাংশনের কাজ হবে যে দুইটা প্যারামিটার ইনপুট নিবে। সেই দুইটা প্যারামিটারকে যোগ করে যোগফলকে চার দিয়ে ভাগ করে ভাগফল রিটার্ণ করে দাও।
৩.৪ একাধিক লাইনওয়ালা অ্যারো ফাংশন লিখো। সেটাতে দুইটা প্যারামিটার নিবে। ওই arrow ফাংশনটা হবে অনেকগুলা লাইনের। সেখানে প্রত্যেকটা ইনপুট প্যারামিটার এর সাথে ৫ যোগ করবে তারপর যোগফল দুইটাকে আবার গুণ করবে। ক্যামনে করবে সেটা চিন্তা করে বের করার চেষ্টা করো।
.
৪. সিম্পল একটা জাভাস্ক্রিপ্ট অবজেক্ট এর কোন একটা প্রোপার্টিকে ভেরিয়েবল হিসেবে ডিক্লেয়ার করার জন্য destructuring ইউজ করো। array এর destructuring করবে আর সেটা করার জন্য তুমি এরে এর সেকেন্ড পজিশন এর উপাদান কে destructuring করে 'balance' নামক একটা ভেরিয়েবল এ রাখবে।
৫. shorthand দিয়ে অবজেক্ট কিভাবে ডিক্লেয়ার করে, {a , b } স্টাইলে।
৬. ফাংশন এর মধ্যে ডিফল্ট প্যারামিটার কিভাবে ডিক্লেয়ার করে
৭. অপশনাল চেইনিং কি জিনিস, সেটা কখন কিভাবে ইউজ করে ?
.
স্ট্যান্ডার্ড ছোট ছোট কয়েকটা লাইব্রেরি আছে সেগুলা হালকা করে হলেও জানতে হবে।
১. Math দিয়ে min, max, ceil, floor, abs, round, random ইত্যাদি দেখে রাখতে হবে। যদি লাগে যেন বের করে ফেলতে পারো
২. Date কিভাবে ডিক্লেয়ার করে। সেখান থেকে সময় কিভাবে বের করে নেয় বা দরকার হলে সময় কিভাবে ফরম্যাট করে সেটা জানতে হবে
৩. আগে না হয় পরে রেগুলার এক্সপ্রেশন কি জিনিস এবং কিভাবে এপ্লাই করে। কি কারণে এপ্লাই করে সেটা জানতে হবে
৪. এটলিস্ট JSON কিভাবে parse করে বা stringify করে সেটা জানতে হবে
ব্রাউজার API সম্পর্কে চারটা জিনিস
১. লোকাল স্টোরেজ, সেশন স্টোরেজ কোনটা কখন ইউজ করবে। কিভাবে ইউজ করবে
২. location API কিভাবে ইউজ করবে ব্রাউজারে
৩. history API কিভাবে ইউজ করে
৪. একদম প্রাথমিক স্টেপ হিসেবে jsonplaceholder এর ওয়েবসাইট থেকে ডাটা fetch করে সেটাকে কনসোল এ দেখাতে হবে। ধরো তুমি তাদের ওয়েবসাইট এ photos এর API এর লিংক কোনটা সেটা জাভাস্ক্রিপ্ট দিয়ে কোড করে সেই ডাটা কনসোল এ দেখতে পারতেছো কিনা। তারপর কয়েকটা কার্ড বানাবে (হতে পারে বুটস্ট্রাপ এর কার্ড) সেগুলা আবার তুমি html দিয়ে ওয়েবসাইট এ ছবি এবং ছবির নিচে ছবির টাইটেল দেখাবে।
------------
আরো পাঁচটা জিনিস জানতে হবে।
১.১ অনেকগুলা সংখ্যার একটা array হবে। তারপর তোমার কাজ হবে array এর উপরে map ইউজ করে। প্রত্যেকটা ২ দিয়ে গুণ করে গুণফল আরেকটা array হিসেবে রাখবে। পুরা কাজটা এক লাইনে হবে।
১.২. জাভাস্ক্রিপ্ট এ array এর map, forEach, filter, find কোনটা দিয়ে কি হয় সেটার একটা সামারি লিখে ফেলো।
২. ternary অপারেটর কি ? এইটা দিয়ে শর্টকার্টে কিভাবে if-else লিখে
৩. লজিক্যাল এন্ড (&&) আর লজিক্যাল or (।।) এই দুইটা সম্পর্কে হালকা ধারণা
৪. JSON এর stringify এবং parse কখন কোনটা ইউজ করে
৫. ++, --, +, +'', +=, -= এইগুলা কি জিনিস। কোনটা দিয়া কি করে সেটা বুঝলেই হবে। তাছাড়া active = !active এইটা এর মানে কি।
৬. Object.keys, Object.values জিনিসগুলা জানা থাকলেও ভালো।
.
ডিবাগিং এবং dev tool সম্পর্কে জানতেই হবে।
১. console ট্যাব
২. source ট্যাব
৩. application
৪. Network
৫. Elements
.
জাভাস্ক্রিপ্ট দিয়ে কিছু বেসিক প্রব্লেম সলভিং করে নিবে
.
যদিও রিএক্ট এর জন্য সরাসরি লাগবে না। তারপরে DOM, DOM ম্যানিপুলেশন, কিভাবে DOM এ ইভেন্ট হ্যান্ডলার যোগ করে। কিভাবে input থেকে ডাটা নিয়ে সেটাকে ওয়েবসাইট এ দেখানো যেতে পারে। এমন ৩-৪ টা প্রজেক্ট করতে হবে।
.
কিছু কন্সেপচুয়াল জিনিস জানতে হবে। এগুলা সরাসরি কাজে না লাগলেও ভিতরে ভিতরে ফিল করার জন্য লাগবে। যেমন জাভাস্ক্রিপ্ট কিভাবে কাজ করে। event loop, closure, ইত্যাদি।
.
দেখো উপরের জিনিসগুলা এর মধ্যে ১০০% জিনিস তুমি ধরে ফেলতে পারো কিনা। আর তুমি যদি উপরের জিনিসগুলা এর ৭০% বা তার বেশি জানো তাহলে তুমি ভালো পজিশনে আছো। নেক্সট এসাইনমেন্ট এর পরে ২ দিন রিভিশন দেয়া হবে। সেদিন রিভিশন দিয়ে এইগুলা কভার করে ফেলবে। আর যদি তুমি ৫০% এর মতো বুঝো তাহলে সামনে এগিয়ে যেতে পারবে। তবে ভালো করে মনোযোগ দিয়ে কষ্ট করে এগুতে হবে। ফাইনালি তুমি যদি ৩০% বা তার নিচে বুঝো তাহলে নেক্সট পাঁচ-ছয়দিন ভালো করে জাভাস্ক্রিপ্ট এ সিরিয়াসলি সময় দাও। তাহলে React এ গেলে তোমার লাইফ অনেক ইজি হয়ে যাবে।
.
ডাইরেক্ট
রিএক্ট;
হবে না, না করলে জাভাস্ক্রিপ্টকে রেসপেক্ট
এইটাই বাস্তবতা, এইটাই ফ্যাক্ট।


```
</details>

### demo
<details>
<summary>
  <h3> (Click Me)</h3>
</summary>
<br >
 reduce


```js

```
</details>

### searchItems
<details>
<summary>
  <h4>What is searchItems?</h4>
</summary>
<br >
- searchItems is
</details>

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

### useState
<details>
<summary>
  <h4>What is useState?</h4>
</summary>
<br >
```js
- useState is

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
  <h4>What is useEffect?</h4>
</summary>
<br >
```js
- useEffect is

// import
import React, {useState, useEffect } from 'react';

const Example = () => {
const [count, setCount] = useState(0);
  // Example
  useEffect(() => {
  // Update the document title using the browser API
      document.title = `You clicked ${count} times`;
  // fetch
    fetch('')
      .then(res => res.json())
      .then(data => console.log(data))
  }, [])

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
************Imporatant start************
// array sort
Example: 
array = [3, -2, -1, 0]
Ans: Ex 1: const sorted = array.sort((a,b) => a-b)
Ex 2 : const result=array.sort(function(a, b){return a - b});	
	
************Imporatant End************
	
************Milestone 4:************
//module 21
1. string: স্ট্রিং বস্তু অপরিবর্তনীয়। অপরিবর্তনীয় মানে অপরিবর্তনীয় বা অপরিবর্তনীয়। একবার স্ট্রিং অবজেক্ট তৈরি হয়ে গেলে এর ডেটা বা স্টেট পরিবর্তন করা যায় না তবে একটি নতুন স্ট্রিং অবজেক্ট তৈরি করা হয়।
//
2. 21-3 How to split, slice, substr, substring, concat, join?
Ans: const lyrics = 'tumi bondhu kala pakhi ami jeno ki. bosonto kale tomai bolte pari nai.';
//i. splite()
const parts = lyrics.split(' ');
const sentences = lyrics.split('.');
const chars = lyrics.split('');
console.log(parts)
console.log(chars)
console.log(sentences)
//ii. slice()
const partial = lyrics.slice(5, 8);
console.log(partial)
//iii. substr() {almost same slice}
const lyricsSubStr = lyrics.substring(5, 10);
console.log(lyricsSubStr)
//iv. split, slice, substr, substring, concat, join, trim,  etc.
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
//21-4 class 
3. Math, abs, pow, round, ceil, floor, and random number ?
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/max
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
************8 ways to get undefine************
// 1. variable that is not initialized will give undefined

// 2. function with no return
function second(a, b) {
    const total = a + b;
}
const result = second(2, 4);
console.log(result)

//3. parameter that is not passed will be undefined
function third(a, b, c, d) {
    const total = a + b + c + d;
    // console.log(a, b, c, d)
}
const result2 = third(2, 4);
console.log(result2)

//4. if return has nothing on the right side will return undefined
function noNegative(a, b){
    if(a < 0 || b < 0){
        return;
    }
    return a + b;
}
const result3 = noNegative(2, -4);
console.log(result3)

// 5. property that doesn't exists on an object will give you undefined
const fifth = {id: 2, name: 'ponchom', age: 40};
console.log(fifth.age, fifth.salary)

//6. accessing array elements outside of the index range will give you undefined
const sixth = [4, 56, 43, 78, 23];
console.log(sixth[1], sixth[6], sixth[200])

//7. deleting an element inside an array
const sixth1 = [4, 56, 43, 78, 23];
delete sixth1[1]
console.log(sixth1[1], sixth1[6], sixth1[200])
console.log(sixth1)

// 8 . set a value directly
const eighth = undefined;
const night = null;
const data = {results: [], updated: null};
console.log(typeof undefined) ans: undefined
console.log(typeof null) ans: object
	
************39-3 Different Truthy and Falsy values in JavaScript************
// truthy
1. true
2. any number (+positive, -negative) will be  truthy other than 0
3. any string other than empty string
4. '0'
5. {} (empty object) truthy
6. [] (empty array) truthy
7. check truthy
const value = ' ' 
if(!!value){
    console.log('truthy value')
}

// Falsy
1. false 
2. 0 
3. '' (empty string)
4. undefined
5. null
6. chek falsey
const value = null 
if(!value){
  console.log('falsy value')
}

************Common types of errors************
1. Syntax Error ?
Ans : Syntax Error is triggered when you write code that is not syntactically correct
i. missing inverted commas
ii. Missing closing parentheses
iii. improper alignment of curly braces or other characters

2. Type Error ?
Ans: Type Error is created when some value doesn't turn out tot be of a particular expected type.
i.i.Uncaught TypeError: Cannot read Property
i.ii.Uncaught TypeError: Cannot set Property
i. Invoking objects that are not methods.
ii. Attempting to access properties of null or undefined objects
iii. Treating a string as a number or vice versa.

3. Reference Error?
Ans: Reference Errors occur we might have forgotten to define a value for the variable before using it,
or we might be trying to use an inaccessible variable in our code.
1. variable name is not define
2. funtion name is not define
#solved way
i. Making a type in a variable name.
ii. Trying to access block-scoped variables outside of their scopes.

4. Logical Error
# যখন সব ঠিক আছে তবে আমরা logic এ ভুল করেছি

************Module 41 ************
#Debug Steps: 
1. Error check (error reproduce)
2. Check others stuffs on the website
3. Check Console for error
4. click on the link of the error (it will take you to the code)
5. If needed add a breakpoint and try to stop the code over there and see the values
6. if needed console log output
7. search full code base (Ctrl + Shift + F) > don't forget about partial match
8. look around for typo

************Module 42 ************
#



```
</details>
  
### ReactJsInterviewQuestions
<details>
<summary>
  <h3>React Js Interview Questions (Click Me)</h3>
</summary>
<br >
  
 ```js

	
  
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
       <!-- row 12 -->
      <tr>
        <th>10</th>
        <td>Conditionals </td>
        <td> comparison: >, <, >=, <=, ===, !==, if-else  </td>
      </tr>
       <!-- row 13 -->
      <tr>
        <th>14</th>
        <td> Array</td>
        <td> Declare, index, get values, set values, indexOf, push, pop </td>
      </tr>
       <!-- row 14 -->
      <tr>
        <th>14</th>
        <td> Loop</td>
        <td> for loop, while loop, break, continue </td>
      </tr>
       <!-- row 15 -->
      <tr>
        <th>15</th>
        <td> Function</td>
        <td> declare, parameters, return, call, use the returned value from a function </td>
      </tr>
       <!-- row 16 -->
      <tr>
        <th>16</th>
        <td> Objeect</td>
        <td> declare, properties, keys , values, get prop value, set value, loop object. </td>
      </tr>
       <!-- row 17 -->
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
             <!-- row 18 -->
      <tr>
        <th>18</th>
               <td> Array Check</td>
        <td> //check array using Array.isArray | console.log(Array.isArray(friends)) </td>
      </tr>
             <!-- row 18 -->
      <tr>
        <th>18</th>
        <td> Array Name Check (ase ki na) </td>
        <td> const friends = [13, 14, 11, 17, 21, 16, 15, 20]; | console.log(friends.includes(19))</td>
      </tr>
             <!-- row 18 -->
      <tr>
        <th>18</th>
        <td> preventDefault</td>
        <td> e.preventDefault();</td>
      </tr>
      <tr>
        <th>17</th>
        <td> Math </td>
        <td> Math, abs, pow, round, ceil, floor, and random number </td>
      </tr>
         <!-- row 19 -->
      <tr>
        <th>19</th>
        <td>Math.random() </td>
        <td>Math.random((Math.random()*1000)) // output 0.7895253939768327</td>
      </tr>
        <!-- row 20 -->
      <tr>
        <th>20</th>
        <td>Math.round() </td>
        <td> Math.round((Math.random()*10000)) // output 4492</td>
      </tr>
        <!-- row 21 -->
      <tr>
        <th>19</th>
        <td><a href="#" onclick="selectedItem(this)" class="btn btn-primary">SELECT</a> </td>
        <td> function er vitor this diya mane oi tai select kora </td>
      </tr>
        <!-- row 22 -->
      <tr>
        <th>22</th>
        <td>Date</td>
        <td>const today = new Date()  </td>
      </tr>
       <!-- row 23 -->
      <tr>
        <th>23</th>
        <td>multiline</td>
        <td>const multiline = 'line 1 \n' + ' line 2 \n'</td>
      </tr>
           <!-- row 24-->
      <tr>
        <th>24</th>
        <td>Api GET</td>
        <td> Receive Information about an API resource ()</td>
      </tr>
           <!-- row 24-->
      <tr>
        <th>24</th>
        <td>Api POST</td>
        <td> Create an API resource (নতুন একটা কিছু add করা) </td>
      </tr>
           <!-- row 24-->
      <tr>
        <th>24</th>
        <td>Api PUT/PATCH</td>
        <td> Update an Api resource (put almost patch but put => যদি কোন কিছু আগে থেকেই থাকে সেইটা পরিবর্তন করে নিজে বসে পরে।  আর না থাকলে নিজে create করে ) (patch => কোন কিছু আগে থেকেই আছে সেই টা update করে) patch করতে হলে কিছু থাকতে হবে।</td>
      </tr>
          <!-- row 24-->
      <tr>
        <th>24</th>
        <td>Api DELETE </td>
        <td> Delete an API resource (Api থেকে কিছু delete করতে DELETE method করতে হবে)</td>
      </tr> <!-- row 24-->
      <tr>
        <th>24</th>
        <td>Api CRUD</td>
        <td>'</td>
      </tr>
          <!-- row 24-->
      <tr>
        <th>24</th>
        <td>HTTP STATUS CODE</td>
        <td>(200 - ok), (301 - Moved Permanently), (302- Moved Temporarily), (404 - Not Found), (500 - Intenal Server Error), (503 - Service Unabailable)</td>
      </tr> 
          <!-- row 24-->
      <tr>
        <th>24</th>
        <td>setTimeout()</td>
        <td>For clearing the timeout funtion, clearTimeout() is used</td>
      </tr>
           <!-- row 24-->
      <tr>
        <th>24</th>
        <td>setTimeout()</td>
        <td>For clearing the timeout funtion, clearInterval() is used</td>
      </tr>
		     <!-- row 24-->
      <tr>
        <th>24</th>
        <td>event loop</td>
        <td> JavaScript এর asynchronous items গুলা থাকে Queue-তে এবং synchronous items গুলা থাকে Stack-এ। Stack এর কাজগুলা সম্পাদন হয়ে গেলে তখন Queue-তে থাকা কাজগুলো Stack-এ এসে সম্পাদন হতে থাকে। আর এই পুরো কাজটা Event Loop-এর মাধ্যমে হয়ে থাকে। এটাই event loop এর কন্সেপ্ট</td>
      </tr>
			     <!-- row 24-->
      <tr>
        <th>24</th>
        <td>Call Stack </td>
        <td> Call Stack হচ্ছে Stack এর মধ্যে synchronous ভাবে যেই function এর কাজগুলো একটার পর একটা থাকে এবং সেই অনুসারে execute হয়, সেটাকেই call stack বলে</td>
      </tr>	     <!-- row 24-->
      <tr>
        <th>24</th>
        <td>Edit any ui page</td>
        <td> document.body.contentEditable = true</td>
      </tr>
	 <!-- row 24-->
      <tr>
        <th>24</th>
        <td> get cookie value from browser</td>
        <td>document.cookie </td>
      </tr>
	  <!-- row 24-->
      <tr>
        <th>24</th>
        <td>get cookie value as array </td>
        <td> document.cookie.split('; ')</td>
      </tr>
	<!-- row 24-->
      <tr>
        <th>24</th>
        <td>get cookie value in key-value pair </td>
        <td>  document.cookie.split('; ').map(c => console.log(c))</td>
      </tr>
	 <!-- row 24-->
      <tr>
        <th>24</th>
        <td>window.location.reload() </td>
        <td> page reload করে  </td>
      </tr>
	<!-- row 24-->
      <tr>
        <th>24</th>
        <td> </td>
        <td> </td>
      </tr>
<!-- row 24-->
      <tr>
        <th>24</th>
        <td> </td>
        <td> </td>
      </tr>
		<!-- row 24-->
      <tr>
        <th>24</th>
        <td> </td>
        <td> </td>
      </tr>
<!-- row 24-->
      <tr>
        <th>24</th>
        <td>shorthand-javascript-techniques </td>
        <td>https://www.sitepoint.com/shorthand-javascript-techniques/?fbclid=IwAR3ELG6nojp4FdQVgXt1sEtZDgIU7ImGEZKxuRBCQblWx1VG1rxGOdCrjE8 </td>
      </tr>
    </tbody>
  </table>
</div>



## 🌐 Socials: Connect with Emon Hossain!

[![Facebook Badge](https://img.shields.io/badge/Facebook-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://fb.com/emonhossain6) [![Linkedin Badge](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/emon007iu/) [![Twitter Badge](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/@emon_hossain7) [![Mail Badge](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:emon.hossain.wd@gmail.com)

<h4>❤️🤔 You can follow my Github and other social accounts 🤔❤️</h4>
<h2>❤️ Thank you very much! ❤️</h2>
