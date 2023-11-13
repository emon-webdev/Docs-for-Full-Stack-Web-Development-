# Redux Using Method And Example

### 🔭 What is Redux?
- step 1 = Setup Store.
- step 2 = Connect redux store with react in main.tsx / app.tsx (provider)
- step 3 = Setup the custome hook (only relatable for ts usage)
- step 4 = Create Slice (Name, initalState, reducer).
- step 5 = Connect you slice with the redux store.
- 
- For Consuming data
- useAppSelector => store
  
### 👯 Why use Redux?
- 
###  🤔 How to Use?

- [setupRedux](#setupRedux)
- [useCreateUserWithEmailAndPassword](#usecreateuserwithemailandpassword)
- [useSignInWithEmailAndPassword](#usesigninwithemailandpassword)
- [useSignInWithApple](#usesigninwithapple)
- [useSignInWithFacebook](#usesigninwithfacebook)
- [useSignInWithGithub](#usesigninwithgithub)
- [useSignInWithGoogle](#usesigninwithgoogle)
- [useSignInWithMicrosoft](#usesigninwithmicrosoft)
- [useSignInWithTwitter](#usesigninwithtwitter)
- [useSignInWithYahoo](#usesigninwithyahoo)
- [useUpdateEmail](#useupdateemail)
- [useUpdatePassword](#useupdatepassword)
- [useUpdateProfile](#useupdateprofile)
- [useSendPasswordResetEmail](#usesendpasswordresetemail)
- [useSendEmailVerification](#usesendemailverification)

### setupRedux

``` js

#step one
install redux ...

#step two
create folder "redux" in src

#step three
create "store.js" in  redux folder
import { configureStore } from '@reduxjs/toolkit'
import { api } from './api/apiSlice'
import cartSlice from './features/cart/cartSlice'

export const store = configureStore({
    reducer: {
        cart: cartSlice,
        [api.reducerPath]: api.reducer,
    },
    middleware: (getDefaultMiddleware) =>
        getDefaultMiddleware().concat(api.middleware),
    devTools: true
})


interrogate  store with provider

main.jsx -----------
import { store } from './redux/store.js';
import { Provider } from 'react-redux';

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <Provider store={store}>
      <AuthProvider>
        <ChakraProvider>
          <HelmetProvider>
            <QueryClientProvider client={queryClient}>
              <RouterProvider router={router} />
            </QueryClientProvider>
          </HelmetProvider>
        </ChakraProvider>
      </AuthProvider>
    </Provider>
  </React.StrictMode>
);


#step four
create a "features" folder in redux folder
#step six
create "cart, order, product, user, etc" folder in the features folder 

#step seaven
create a "cartSlice" folder in cart folder
create a "apiSlice" folder in api folder



cartSlice.js.................

import { createSlice } from '@reduxjs/toolkit';

const initialState = {
    products: [],
    totalPrice: 0,
}

export const cartSlice = createSlice({
    name: 'cart',
    initialState,
    reducers: {
        addToCart: (state, action) => {
            const existing = state.products.find(
                (product) => product._id === action.payload._id
            );
            console.log(existing?.quantity)
            if (existing) {
                existing.quantity = existing.quantity + 1;
            } else {
                state.products.push({ ...action.payload, quantity: 1 });
            }
            state.totalPrice += action.payload.price;
        },
        removeOneProduct: (state, action) => {
            const existing = state.products.find(
                product => product._id === action.payload._id
            )
            console.log('remove one product')
            if (existing && existing.quantity > 1) {
                existing.quantity = existing.quantity - 1
            } else {
                console.log('Delete product from cart minus btn')
                state.products = state.products.filter(
                    (product) => product._id !== action.payload._id
                )
            }
            state.totalPrice -= action.payload.price;
        },
        removeFromCart: (state, action) => {
            state.products = state.products.filter(
                (product) => product._id !== action.payload._id
            );
            state.totalPrice -= action.payload.price * action.payload.quantity;
        },
    },
})

export const {
    addToCart,
    removeFromCart,
    removeOneProduct
} = cartSlice.actions

export default cartSlice.reducer


use cartSlice.js ------------------

   const { products, totalPrice } = useSelector((state) => state.cart)
    const dispatch = useDispatch()


<ButtonGroup size='sm' isAttached variant='outline'>
    <IconButton
        onClick={() => dispatch(removeOneProduct(item))}
        aria-label='Add to friends'
        icon={<MinusIcon />}
    />
    <h1 className='px-3 text-2xl'>
        {item.quantity}
    </h1>
    <IconButton
        onClick={() => dispatch(addToCart(item))}
        aria-label='Add to friends'
        icon={<AddIcon />}
    />
</ButtonGroup>

apiSlice.js ----------------------
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react';


export const api = createApi({
    reducerPath: 'api',
    baseQuery: fetchBaseQuery({ baseUrl: `${import.meta.env.VITE_APP_API_URL}` }),
    tagTypes: ["reviews"],
    endpoints: (builder) => ({
        getProducts: builder.query({
            query: () => `/products`,
        }),
        getSingleProducts: builder.query({
            query: (id) => `/products/${id}`,
        }),
        getReviews: builder.query({
            query: () => `/review`,
        }),
        addProductComment: builder.mutation({
            query(data) {
                return {
                    url: `/product-review`,
                    method: 'POST',
                    body: data,
                }
            },
            invalidatesTags: ["reviews"]
        }),
        getProductReview: builder.query({
            query: (id) => `/product-review/${id}`,
            providesTags: ["reviews"]
        }),
    }),
})

export const {
    useGetProductsQuery,
    useGetSingleProductsQuery,
    useGetReviewsQuery,
    useGetProductReviewQuery,
    useAddProductCommentMutation,
} = api;



using apiSlice in component ----------------------

import { useAddProductCommentMutation, useGetProductReviewQuery, useGetSingleProductsQuery } from '../../redux/api/apiSlice';

   let image, price, recipe, name, _id, category
    const { id } = useParams()
    const { data: item, isLoading: loading } = useGetSingleProductsQuery(id)
    const {
        data: productReview,
        isLoading: reviewLoading,
        refetch: reviewRefetch
    } = useGetProductReviewQuery(id, {
        refetchOnMountOrArgChange: true,
        pollingInterval: 30000
    })
    // const item = useLoaderData()
    // const { image, price, recipe, category, name, _id } = item;

    if (!loading) {
        ({ image, price, recipe, category, name, _id } = item);
    }
    const [addProductComment, { isLoading, isError, isSuccess }] = useAddProductCommentMutation()

    const {
        register,
        handleSubmit,
        reset,
        formState: { errors },
    } = useForm();
    const { user } = useContext(AuthContext)
    const navigate = useNavigate()
    const location = useLocation()
    const [, refetch] = useCart()
    const currentDate = new Date();
    const formattedDate = format(currentDate, 'MMMM d, yyyy');


    const handleComment = (data) => {
        if (user && user?.email) {
            const review = {
                productId: item?._id,
                date: formattedDate,
                userName: user?.displayName,
                userEmail: user?.email,
                userPhoto: user?.photoURL,
                comment: data.comment
            }
            addProductComment(review)
            if (!isSuccess) {
                refetch()
                reset()
                reviewRefetch()
                Swal.fire({
                    title: 'Comment Done',
                })
            }
        } else {
            Swal.fire({
                title: 'Please login for the comment',
                icon: 'warning',
                showCancelButton: true,
                confirmButtonColor: '#3085d6',
                cancelButtonColor: '#d33',
                confirmButtonText: 'Login Now'
            }).then((result) => {
                if (result.isConfirmed) {
                    navigate('/login', { state: { from: location } })
                }
            })
        }
    }


    const handleAddToCart = item => {
        if (user && user?.email) {
            const cartItem = {
                menuItemId: item?._id,
                name,
                image,
                price,
                email: user?.email
            }
            fetch(`${import.meta.env.VITE_APP_API_URL}/carts`, {
                method: 'POST',
                headers: {
                    'content-type': 'application/json'
                },
                body: JSON.stringify(cartItem)
            }).then(res => res.json()).then(data => {
                if (data.insertedId) {
                    refetch() // refetch cart to update the cart number
                    Swal.fire({
                        icon: 'success',
                        title: 'Food added on the cart'
                    })
                }
            })
        } else {
            Swal.fire({
                title: 'Please login to order the food?',
                icon: 'warning',
                showCancelButton: true,
                confirmButtonColor: '#3085d6',
                cancelButtonColor: '#d33',
                confirmButtonText: 'Login Now'
            }).then((result) => {
                if (result.isConfirmed) {
                    navigate('/login', { state: { from: location } })
                }
            })
        }

    }





Split  api end pont from apiSlice.js ----------------------

create productApi.js------

import { api } from "../../api/apiSlice";

const productApi = api.injectEndpoints({
    endpoints: (builder) => ({
        getProducts: builder.query({
            query: () => `/products`,
        }),
        getSingleProducts: builder.query({
            query: (id) => `/products/${id}`,
        }),
    }),
})

export const {
    useGetProductsQuery,
    useGetSingleProductsQuery,
} = productApi;




```

#### Full Example

```js
import { getAuth, signInWithEmailAndPassword, signOut } from 'firebase/auth';
import { useAuthState } from 'react-firebase-hooks/auth';

const auth = getAuth(firebaseApp);

const login = () => {
  signInWithEmailAndPassword(auth, 'test@test.com', 'password');
};
const logout = () => {
  signOut(auth);
};

const CurrentUser = () => {
  const [user, loading, error] = useAuthState(auth);

  if (loading) {
    return (
      <div>
        <p>Initialising User...</p>
      </div>
    );
  }
  if (error) {
    return (
      <div>
        <p>Error: {error}</p>
      </div>
    );
  }
  if (user) {
    return (
      <div>
        <p>Current User: {user.email}</p>
        <button onClick={logout}>Log out</button>
      </div>
    );
  }
  return <button onClick={login}>Log in</button>;
};
```

### useCreateUserWithEmailAndPassword

```js
const [
  createUserWithEmailAndPassword,
  user,
  loading,
  error,
] = useCreateUserWithEmailAndPassword(auth);
```

Create a user with email and password. Wraps the underlying `firebase.auth().createUserWithEmailAndPassword` method and provides additional `loading` and `error` information.

The `useCreateUserWithEmailAndPassword` hook takes the following parameters:

- `auth`: `auth.Auth` instance for the app you would like to monitor
- `options`: (optional) `Object` with the following parameters:
  - `emailVerificationOptions`: (optional) `auth.ActionCodeSettings` to customise the email verification
  - `sendEmailVerification`: (optional) `boolean` to trigger sending of an email verification after the user has been created

Returns:

- `createUserWithEmailAndPassword(email: string, password: string)`: a function you can call to start the registration
- `user`: The `User` if the user was created or `undefined` if not
- `loading`: A `boolean` to indicate whether the the user creation is processing
- `error`: Any `Error` returned by Firebase when trying to create the user, or `undefined` if there is no error

#### Full Example

```jsx
import { useCreateUserWithEmailAndPassword } from 'react-firebase-hooks/auth';

const SignIn = () => {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [
    createUserWithEmailAndPassword,
    user,
    loading,
    error,
  ] = useCreateUserWithEmailAndPassword(auth);

  if (error) {
    return (
      <div>
        <p>Error: {error.message}</p>
      </div>
    );
  }
  if (loading) {
    return <p>Loading...</p>;
  }
  if (user) {
    return (
      <div>
        <p>Registered User: {user.email}</p>
      </div>
    );
  }
  return (
    <div className="App">
      <input
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      <input
        type="password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
      />
      <button onClick={() => createUserWithEmailAndPassword(email, password)}>
        Register
      </button>
    </div>
  );
};
```

### useSignInWithEmailAndPassword

```js
const [
  signInWithEmailAndPassword,
  user,
  loading,
  error,
] = useSignInWithEmailAndPassword(auth);
```

Login a user with email and password. Wraps the underlying `auth.signInWithEmailAndPassword` method and provides additional `loading` and `error` information.

The `useSignInWithEmailAndPassword` hook takes the following parameters:

- `auth`: `Auth` instance for the app you would like to monitor

Returns:

- `signInWithEmailAndPassword(email: string, password: string)`: a function you can call to start the login
- `user`: The `auth.User` if the user was logged in or `undefined` if not
- `loading`: A `boolean` to indicate whether the the user login is processing
- `error`: Any `Error` returned by Firebase when trying to login the user, or `undefined` if there is no error

#### Full Example

```jsx
import { useSignInWithEmailAndPassword } from 'react-firebase-hooks/auth';

const SignIn = () => {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [
    signInWithEmailAndPassword,
    user,
    loading,
    error,
  ] = useSignInWithEmailAndPassword(auth);

  if (error) {
    return (
      <div>
        <p>Error: {error.message}</p>
      </div>
    );
  }
  if (loading) {
    return <p>Loading...</p>;
  }
  if (user) {
    return (
      <div>
        <p>Signed In User: {user.email}</p>
      </div>
    );
  }
  return (
    <div className="App">
      <input
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      <input
        type="password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
      />
      <button onClick={() => signInWithEmailAndPassword(email, password)}>
        Sign In
      </button>
    </div>
  );
};
```

### useSignInWithApple

```js
const [signInWithApple, user, loading, error] = useSignInWithApple(auth);
```

Login a user with Apple Authenticatiton. Wraps the underlying `auth.signInWithPopup` method with the `auth.OAuthProvider` and provides additional `loading` and `error` information.

The `useSignInWithApple` hook takes the following parameters:

- `auth`: `Auth` instance for the app you would like to monitor

Returns:

- `signInWithApple(scopes: string[], customOAuthParameters: auth.CustomParameters)`: a function you can call to start the login
- `user`: The `auth.User` if the user was logged in or `undefined` if not
- `loading`: A `boolean` to indicate whether the the user login is processing
- `error`: Any `Error` returned by Firebase when trying to login the user, or `undefined` if there is no error

#### Full example

See [social login example](#social-login-example)

### useSignInWithFacebook

```js
const [signInWithFacebook, user, loading, error] = useSignInWithFacebook(auth);
```

Login a user with Facebook Authenticatiton. Wraps the underlying `auth.signInWithPopup` method with the `auth.OAuthProvider` and provides additional `loading` and `error` information.

The `useSignInWithApple` hook takes the following parameters:

- `auth`: `Auth` instance for the app you would like to monitor

Returns:

- `signInWithFacebook(scopes: string[], customOAuthParameters: auth.CustomParameters)`: a function you can call to start the login
- `user`: The `auth.User` if the user was logged in or `undefined` if not
- `loading`: A `boolean` to indicate whether the the user login is processing
- `error`: Any `Error` returned by Firebase when trying to login the user, or `undefined` if there is no error

#### Full example

See [social login example](#social-login-example)

### useSignInWithGithub

```js
const [signInWithGithub, user, loading, error] = useSignInWithGithub(auth);
```

Login a user with Github Authenticatiton. Wraps the underlying `auth.signInWithPopup` method with the `auth.OAuthProvider` and provides additional `loading` and `error` information.

The `useSignInWithGithub` hook takes the following parameters:

- `auth`: `Auth` instance for the app you would like to monitor

Returns:

- `signInWithGithub(scopes: string[], customOAuthParameters: auth.CustomParameters)`: a function you can call to start the login
- `user`: The `auth.User` if the user was logged in or `undefined` if not
- `loading`: A `boolean` to indicate whether the the user login is processing
- `error`: Any `Error` returned by Firebase when trying to login the user, or `undefined` if there is no error

#### Full example

See [social login example](#social-login-example)

### useSignInWithGoogle

```js
const [signInWithGoogle, user, loading, error] = useSignInWithGoogle(auth);
```

Login a user with Google Authenticatiton. Wraps the underlying `auth.signInWithPopup` method with the `auth.GoogleProvider` and provides additional `loading` and `error` information.

The `useSignInWithGoogle` hook takes the following parameters:

- `auth`: `Auth` instance for the app you would like to monitor

Returns:

- `signInWithGoogle(scopes: string[], customOAuthParameters: auth.CustomParameters)`: a function you can call to start the login
- `user`: The `auth.User` if the user was logged in or `undefined` if not
- `loading`: A `boolean` to indicate whether the the user login is processing
- `error`: Any `Error` returned by Firebase when trying to login the user, or `undefined` if there is no error

#### Full example

See [social login example](#social-login-example)

### useSignInWithMicrosoft

```js
const [signInWithMicrosoft, user, loading, error] = useSignInWithMicrosoft(
  auth
);
```

Login a user with Microsoftt Authenticatiton. Wraps the underlying `auth.signInWithPopup` method with the `auth.OAuthProvider` and provides additional `loading` and `error` information.

The `useSignInWithMicrosoft` hook takes the following parameters:

- `auth`: `Auth` instance for the app you would like to monitor

Returns:

- `signInWithMicrosoft(scopes: string[], customOAuthParameters: auth.CustomParameters)`: a function you can call to start the login
- `user`: The `auth.User` if the user was logged in or `undefined` if not
- `loading`: A `boolean` to indicate whether the the user login is processing
- `error`: Any `Error` returned by Firebase when trying to login the user, or `undefined` if there is no error

#### Full example

See [social login example](#social-login-example)

### useSignInWithTwittter

```js
const [signInWithTwitter, user, loading, error] = useSignInWithTwitter(auth);
```

Login a user with Twitter Authenticatiton. Wraps the underlying `auth.signInWithPopup` method with the `auth.OAuthProvider` and provides additional `loading` and `error` information.

The `useSignInWithTwitter` hook takes the following parameters:

- `auth`: `Auth` instance for the app you would like to monitor

Returns:

- `signInWithTwitter(scopes: string[], customOAuthParameters: auth.CustomParameters)`: a function you can call to start the login
- `user`: The `auth.User` if the user was logged in or `undefined` if not
- `loading`: A `boolean` to indicate whether the the user login is processing
- `error`: Any `Error` returned by Firebase when trying to login the user, or `undefined` if there is no error

#### Full example

See [social login example](#social-login-example)

### useSignInWithYahoo

```js
const [signInWithYahoo, user, loading, error] = useSignInWithYahoo(auth);
```

Login a user with Yahoo Authenticatiton. Wraps the underlying `auth.signInWithPopup` method with the `auth.OAuthProvider` and provides additional `loading` and `error` information.

The `useSignInWithYahoo` hook takes the following parameters:

- `auth`: `Auth` instance for the app you would like to monitor

Returns:

- `signInWithYahoo(scopes: string[], customOAuthParameters: auth.CustomParameters)`: a function you can call to start the login
- `user`: The `auth.User` if the user was logged in or `undefined` if not
- `loading`: A `boolean` to indicate whether the the user login is processing
- `error`: Any `Error` returned by Firebase when trying to login the user, or `undefined` if there is no error

#### Full example

See [social login example](#social-login-example)

### Social Login Example

```jsx
import { useSignInWithXXX } from 'react-firebase-hooks/auth';

const SignIn = () => {
  const [signInWithXXX, user, loading, error] = useSignInWithXXX(auth);

  if (error) {
    return (
      <div>
        <p>Error: {error.message}</p>
      </div>
    );
  }
  if (loading) {
    return <p>Loading...</p>;
  }
  if (user) {
    return (
      <div>
        <p>Signed In User: {user.email}</p>
      </div>
    );
  }
  return (
    <div className="App">
      <input
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      <input
        type="password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
      />
      <button onClick={() => signInWithXXX()}>Sign In</button>
    </div>
  );
};
```

### useUpdateEmail

```js
const [updateEmail, updating, error] = useUpdateEmail(auth);
```

Update the current user's email address. Wraps the underlying `auth.updateEmail` method and provides additional `updating` and `error` information.

The `useUpdateEmail` hook takes the following parameters:

- `auth`: `Auth` instance for the app you would like to monitor

Returns:

- `updateEmail(email: string)`: a function you can call to update the current user's email addres
- `updating`: A `boolean` to indicate whether the user update is processing
- `error`: Any `Error` returned by Firebase when trying to update the user, or `undefined` if there is no error

#### Full Example

```jsx
import { useUpdateEmail } from 'react-firebase-hooks/auth';

const UpdateEmail = () => {
  const [email, setEmail] = useState('');
  const [updateEmail, updating, error] = useUpdateEmail(auth);

  if (error) {
    return (
      <div>
        <p>Error: {error.message}</p>
      </div>
    );
  }
  if (updating) {
    return <p>Updating...</p>;
  }
  return (
    <div className="App">
      <input
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      <button
        onClick={async () => {
          await updateEmail(email);
          alert('Updated email address');
        }}
      >
        Update email
      </button>
    </div>
  );
};
```

### useUpdatePassword

```js
const [updatePassword, updating, error] = useUpdatePassword(auth);
```

Update the current user's password. Wraps the underlying `auth.updatePassword` method and provides additional `updating` and `error` information.

The `useUpdatePassword` hook takes the following parameters:

- `auth`: `Auth` instance for the app you would like to monitor

Returns:

- `updatePassword(password: string)`: a function you can call to update the current user's password
- `updating`: A `boolean` to indicate whether the user update is processing
- `error`: Any `Error` returned by Firebase when trying to update the user, or `undefined` if there is no error

#### Full Example

```jsx
import { useUpdatePassword } from 'react-firebase-hooks/auth';

const UpdatePassword = () => {
  const [password, setPassword] = useState('');
  const [updatePassword, updating, error] = useUpdatePassword(auth);

  if (error) {
    return (
      <div>
        <p>Error: {error.message}</p>
      </div>
    );
  }
  if (updating) {
    return <p>Updating...</p>;
  }
  return (
    <div className="App">
      <input
        type="password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
      />
      <button
        onClick={async () => {
          await updatePassword(email);
          alert('Updated password');
        }}
      >
        Update password
      </button>
    </div>
  );
};
```

### useUpdateProfile

```js
const [updateProfile, updating, error] = useUpdateProfile(auth);
```

Update the current user's profile. Wraps the underlying `auth.updateProfile` method and provides additional `updating` and `error` information.

The `useUpdateProfile` hook takes the following parameters:

- `auth`: `Auth` instance for the app you would like to monitor

Returns:

- `updateProfile({ displayName: string, photoURL: string })`: a function you can call to update the current user's profile
- `updating`: A `boolean` to indicate whether the user update is processing
- `error`: Any `Error` returned by Firebase when trying to update the user, or `undefined` if there is no error

#### Full Example

```jsx
import { useUpdateProfile } from 'react-firebase-hooks/auth';

const UpdateProfile = () => {
  const [displayName, setDisplayName] = useState('');
  const [photoURL, setPhotoURL] = useState('');
  const [updateProfile, updating, error] = useUpdateProfile(auth);

  if (error) {
    return (
      <div>
        <p>Error: {error.message}</p>
      </div>
    );
  }
  if (updating) {
    return <p>Updating...</p>;
  }
  return (
    <div className="App">
      <input
        type="displayName"
        value={displayName}
        onChange={(e) => setDisplayName(e.target.value)}
      />
      <input
        type="photoURL"
        value={photoURL}
        onChange={(e) => setPhotoURL(e.target.value)}
      />
      <button
        onClick={async () => {
          await updateProfile({ displayName, photoURL });
          alert('Updated profile');
        }}
      >
        Update profile
      </button>
    </div>
  );
};
```

### useSendPasswordResetEmail

```js
const [sendPasswordResetEmail, sending, error] = useSendPasswordResetEmail(
  auth
);
```

Send a password reset email to the specified email address. Wraps the underlying `auth.sendPasswordResetEmail` method and provides additional `sending` and `error` information.

The `useSendPasswordResetEmail` hook takes the following parameters:

- `auth`: `Auth` instance for the app you would like to monitor

Returns:

- `sendPasswordResetEmail(email: string)`: a function you can call to send a password reset emaail
- `sending`: A `boolean` to indicate whether the email is being sent
- `error`: Any `Error` returned by Firebase when trying to send the email, or `undefined` if there is no error

#### Full Example

```jsx
import { useSendPasswordResetEmail } from 'react-firebase-hooks/auth';

const SendPasswordReset = () => {
  const [email, setEmail] = useState('');
  const [sendPasswordResetEmail, sending, error] = useSendPasswordResetEmail(
    auth
  );

  if (error) {
    return (
      <div>
        <p>Error: {error.message}</p>
      </div>
    );
  }
  if (sending) {
    return <p>Sending...</p>;
  }
  return (
    <div className="App">
      <input
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      <button
        onClick={async () => {
          await sendPasswordResetEmail(email);
          alert('Sent email');
        }}
      >
        Reset password
      </button>
    </div>
  );
};
```

### useSendEmailVerification

```js
const [sendEmailVerification, sending, error] = useSendEmailVerification(auth);
```

Send a verification email to the current user. Wraps the underlying `auth.sendEmailVerification` method and provides additional `sending` and `error` information.

The `useSendEmailVerification` hook takes the following parameters:

- `auth`: `Auth` instance for the app you would like to monitor

Returns:

- `sendEmailVerification()`: a function you can call to send a password reset emaail
- `sending`: A `boolean` to indicate whether the email is being sent
- `error`: Any `Error` returned by Firebase when trying to send the email, or `undefined` if there is no error

#### Full Example

```jsx
import { useSendEmailVerification } from 'react-firebase-hooks/auth';

const SendEmailVerification = () => {
  const [email, setEmail] = useState('');
  const [sendEmailVerification, sending, error] = useSendEmailVerification(
    auth
  );

  if (error) {
    return (
      <div>
        <p>Error: {error.message}</p>
      </div>
    );
  }
  if (sending) {
    return <p>Sending...</p>;
  }
  return (
    <div className="App">
      <button
        onClick={async () => {
          await sendEmailVerification();
          alert('Sent email');
        }}
      >
        Verify email
      </button>
    </div>
  );
};
```
