# Module Project: Context API - Shopping Cart

In this module you will take your newfound knowledge of `Context API` and refactor a e-commerce store to use `Context API` as well as extend the functionality of the application making it more robust!

## Introduction

Read these instructions carefully. Understand exactly what is expected _before_ starting this project.

### Commits

Commit your code regularly and meaningfully. This helps both you and your team lead in case you ever need to return to old code for any number of reasons.

### Description

In this project you'll take take an almost completed e-commerce store and refactor the application to use the `Context API`.

### Instructions

### Task 1: Project Set up
- [X] Download project dependencies by running `npm install`.
- [X] Start up the app using `npm start`.

### Task 2: MVP

Before you get started, please take a few minutes and get acquainted with this application. Understand what's going on and how it's working.

- If you look in the `App.js` you'll notice there are currently two state properties - `products` to keep track of all available products, and `cart` that will keep track of all the items in our `cart`.

- You'll also notice inside of our `App.js` we have 3 components. A navigation component and two route based components. Each of those components are all being passed either our `cart` state or `product` state as props, when we start to scale our application and add more props our codebase is going to start to become very cumbersome and will make our application hard to work with.

- To combat this from happening we're going to refactor our application to use `Context API`, making it easier and more effiecent to access data across our application.

**Step 1 - Add item functionality**

- In `App.js` there is a function called `addItem`. Finish writing the logic in this function to be able to add the given item to the shopping cart

**STEP 2 - Creating ProductContext**

- In `src`, create a new folder named `contexts`, this folder is going to be used to hold all of `context objects` we create.

- Inside that folder create a new file named `ProductContext.js`

- In this file, import the `createContext` function from the react library and create our `ProductContext`.

**STEP 3 - Providing data with ProductContext**

- Now that we've created our `ProductContext` we can import into our `App.js`. Now we can start providing data across our application!

- Wrap all of your components/routes in `App.js` inside of `ProductContext.Provider` component.

- Next pass a value prop to your `Provider`.

- In the value prop we'll pass in the products state, and an addItem function that will allow us to add books to the cart.

```js
<ProductContext.Provider value={{ products, addItem }}>
```

- Now that we're providing our products state and addItem function we can simplify our products route a bit.

**Before**

```js
<Route exact path="/">
  <Products products={products} addItem={addItem} />
</Route>
```

**After**

```js
<Route exact path="/">
  <Products />
</Route>
```

- After refactoring you'll notice a few errors... Don't worry we'll clean those up shortly!

**STEP 4 - Consuming data with ProductContext**

- Now that our `ProductContext` is now providing data we can finally consume it! To do so let's head over to our `Products` component and import the `useContext` hook as well as our `ProductContext`.

- In the component, call the `useContext` hook and pass in the context object we want to use into it.

- When we do this, `useContext` is going to return value passed by our `ProductContext` Provider `value` prop. In our case we're getting back an object with two properties. A `products` property and a `addItem` property. We can go ahead and destructure those.

```js
const { products, addItem } = useContext(ProductContext);
```

- Now that we have all of the data we need we can refactor our `Products` component from using props.

- To do so we just need to remove every instance of `props`.

  - Remove it from the function parameters
  - Remove it from the products map
  - Remove it from addItem prop

- Now our `Products` component is getting it's data solely from `Context API` 😃.

**STEP 5 - Create the CartContext**

- Now that we have refactored our `Products` component to utilize `Context API` let's refactor our `Cart` and `Navigation` Component to use `Context API` as well.

- To start create a new file in our contexts folder named `CartContext.js`, this context is going to be utilized by our `ShoppingCart` and `Navigation` component.

- Inside of our new `CartContext` import `createContext` and create a new context named `CartContext`.

**STEP 6 - Providing data with CartContext**

- Let's go ahead and bring our newly created `CartContext` into our `App.js` and wrap all of our components inside of our `CartContext.Provider`. Make sure our `ProductContext.Provider` is still the root provider.

- Now pass a value prop to our `CartContext.Provider`, this value prop is going to contain our `cart` state.

- Now that we're providing our cart data, we can start to refactor our `Navigation` and `ShoppingCart` components.

- Let's start with our `ShoppingCart` component first. Go ahead and refactor the `ShoppingCart` route to no longer use render props. This will throw us an error, but we'll be able to resolve it quickly.

- While were at it let's go ahead and remove the props from our navigation as well.

**STEP 7 - The final stretch**

- Our cart data is now being provided to us from our `CartContext` time to consume it!

- First, let's head to our `ShoppingCart` component and import the `useContext` hook and our `CartContext`.

- Now in the component, pass `CartContext` to the `useContext` hook and assign it to a variable named cart.

- Inside of our component we now need to remove all instances of props.

  - Remove the `props` parameter
  - Remove the `props` portion in our `getCartTotal` function
  - Remove `props` when we're mapping over our cart

- Time to do the same thing for our `Navigation` component.
  - First import the `useContext` hook and our `CartContext`
  - Next, pass our `CartContext` to the `useContext` hook and assign it to a variable named cart.
  - Lastly we need to remove all instances of `props`
    - Remove `props` from our parameters
    - Remove `props` from our cart length

We have now successfully converted our application into using `Context API` 🔥

**MVP Requirements**

- Create a `ProductContext` and a `CartContext`
- Use the Provider Component from `ProductContext` and `CartContext` to provide data to child components
- Consume data using the `useContext` hook from `ProductContext` and `CartContext`

### Task 3: Stretch Problems

Do not attempt stretch problems until MVP has been reached and a final commit has been made.

- Create a `removeItem` function that allows you to remove an item from your cart with a click of a button. This `removeItem` function should be able to be consumed from your `ShoppingCartItem` component.
  Remember each item has an `id` this will help out a lot while creating your removeItem function!

- Persist Cart Items using `localStorage`. (If you try this one, it will be a bit tricky to get our items to populate the shopping cart on a refresh. You'll have to think about where the data actually lives, and how you can get data there from localStorage when the app is being mounted after a refresh. Good luck!)

### Submission Format
- [ ] If this is your first time connecting a submission, authorize your github account within the codegrade assignment.
- [ ] Connect your fork to Codegrade using the "Connect Git" button.
- [ ] Find your newly created fork from the list and push your work to main.
- [ ] Check this video for details: www.youtube.com/watch?v=fC2BO7dI6IQ
