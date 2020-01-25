[![npm version](https://badge.fury.io/js/react-stripe-checkout.svg)](http://badge.fury.io/js/react-stripe-checkout)
[![Dependencies Status](https://david-dm.org/azmenak/react-stripe-checkout.svg)](https://david-dm.org/react-stripe-checkout)
[![Gitter](https://img.shields.io/gitter/room/nwjs/nw.js.svg)](https://gitter.im/azmenak/react-stripe-checkout)

# React Stripe Checkout Component
Stripe's Checkout makes it almost too easy to take people's money.
This should make it even easier if you're building a react
application.

### Installation

Get started by installing with npm

    npm install stripe-react-sdk-prodio


### Requirements

`token` and `stripeKey` are the only *required* props,
everything else is optional as per the stripe docs. See [Checkout
Docs](https://stripe.com/docs/checkout#integration-custom). All props
go through simple validation and are passed to stripe checkout, they're
also documented in `StripeCheckout.js`.

```jsx
import React from 'react'
import StripeCheckout from 'stripe-react-sdk-prodio';

export default class PaymentClass extends React.Component {
  onToken = (token) => {
    fetch('/savePaymentTransaction', {
      method: 'POST',
      body: JSON.stringify(token),
    }).then(response => {
      response.json().then(data => {
        console.log('Payment completed successfully.');
      });
    });
  }

  // ...

  render() {
    return (
      // ...
      <StripeCheckout
        token={this.onToken}
        stripeKey="my_PUBLISHABLE_stripekey"
      />
    )
  }
}
```

This will give you a default *Stripe-style* button which looks like this:

![stripe checkout button](example.png)

### Send all the props!

```jsx
<StripeCheckout
  name="Payment Transaction" // the pop-in header title
  description="Here you can write the description" // the pop-in header subtitle
  image="{REMOTE_URL_FOR_THE_IMAGE}" // the pop-in header image (default none)
  label="Let's Pay" // text inside the Stripe button
  panelLabel="Give Money" // prepended to the amount in the bottom pay button
  amount={1000000} // cents
  containerStyle={{}} //container style
  buttonStyle={{}} //payment button style object
  currency="USD"
  stripeKey="..."
  locale="en"
  email=""
  // Note: Enabling either address option will give the user the ability to
  // fill out both. Addresses are sent as a second parameter in the token callback.
  shippingAddress
  billingAddress={false}
  // Note: enabling both zipCode checks and billing or shipping address will
  // cause zipCheck to be pulled from billing address (set to shipping if none provided).
  zipCode={false}
  allowRememberMe // "Remember Me" option (default true)
  token={this.onToken} // submit callback
  opened={this.onOpened} // called when the checkout popin is opened (no IE6/7)
  closed={this.onClosed} // called when the checkout popin is closed (no IE6/7)
  >
  <button className="btn btn-primary">
    Use your own child component, which gets wrapped in whatever
    component you pass into as "ComponentClass" (defaults to span)
  </button>
</StripeCheckout>
```
