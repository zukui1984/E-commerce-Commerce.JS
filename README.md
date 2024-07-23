# E-commerce website 

Build a responsive e-commerce website with help commerce infrastructure of commerce.js, React as framework and lastly Stripe as online payment

## [Demo](https://ecommerce-js-nicky.netlify.app/) 

## Screenshot
![short-clip](https://user-images.githubusercontent.com/71074389/113506708-b8772f00-9546-11eb-95cc-cb3644a75879.gif)

## Technical requirements
* React Hook / Router DOM
* commerce.js - headless e-commerce https://commercejs.com
* Stripe.js - online transaction payment https://stripe.com
* Material-UI Core & Icons
* API KEY (commerce.js & stripe.js)
* Heroku - Hosting

## Steps
1. Install node.js and verify after that
```
node -v
npm -v
```
2. Create React application
```jsx
npx create-react-app ecommerce
cd ecommerce
```
3. Install dependencies - Commerce.js & Stripe.js
```npm
npm install @chec/commerce.js
npm install @stripe/react-stripe-js @stripe/stripe-js
```
4. Set up Commerce.js
    - Create .env file and add your Commerce.js public key
    ```jsx
    REACT_APP_CHEC_PUBLIC_KEY=your_public_key_here
    ```  
    - Create a file named commerce.js in the src directory and add
   ```jsx
   import Commerce from '@chec/commerce.js';
   const commerce = new Commerce(process.env.REACT_APP_CHEC_PUBLIC_KEY, true);
   export default commerce;
   ```
  
5. Create Components (for complete code - [source](https://github.com/zukui1984/ecommerce/tree/master/src/components))
   - Cart
   - CheckoutForm
   - Navbar
   - Products
     
6. Set up Stripe js
- Add on "Create folder" and put into "PaymentForm folder"
   ```jsx
   import { loadStripe } from '@stripe/stripe-js';
   const stripePromise = loadStripe('your_public_key_here');
   export default stripePromise;;
   ```

7. Combine Components in App Folder (for complete code - [source](https://github.com/zukui1984/ecommerce/blob/master/src/App.js#L63))
  ```jsx
  import React, { useState, useEffect } from "react";
  import { commerce } from "./lib/commerce";
  import { Products, Navbar, Cart, Checkout } from "./components";
  import { BrowserRouter as Router, Switch, Route } from "react-router-dom";

  function App = () => {

  return (
    <Router>
      <div>
        <Navbar totalItems={cart.total_items} />
        <Switch>
          <Route exact path="/">
            <Products products={products} onAddToCart={handleAddToCart} />
          </Route>

          <Route exact path="/cart">
            <Cart
              cart={cart}
              handleUpdateCartQty={handleUpdateCartQty}
              handleRemoveFromCart={handleRemoveFromCart}
              handleEmptyCart={handleEmptyCart}
            />
          </Route>

          <Route exact path="/checkout">
            <Checkout 
            cart={cart}
            order={order}
            onCaptureCheckout={handleCaptureCheckout}
            error={errorMessage}
            />
          </Route>

        </Switch>
      </div>
      </Router>
    );
  };
  export default App; 
  ```

8. Run application
  ```npm
  npm start
  ```
9. Setup Heroku
    - Install & register heroku
    - Run "heroku login"
    - Run "create heroku ecommerce_2024"
    - Setup environment variables:
        - heroku config:set REACT_APP_CHEC_PUBLIC_KEY
        - heroku config:set REACT_APP_STRIPE_PUBLIC_KEY
    - Deploy code "git push heroku master"
    - Open app "heroku open"
