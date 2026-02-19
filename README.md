# Krunker.io Movement Coaching Website

A professional landing page and checkout system for Krunker.io movement coaching services.

## Files

- `index.html` - Main landing page with features, testimonials, and call-to-action
- `checkout.html` - Checkout page ready for Stripe integration
- `README.md` - This file

## Features

- Modern, gaming-themed design with neon accents
- Fully responsive layout for mobile and desktop
- Professional landing page highlighting coaching benefits
- Secure checkout page with order summary
- Pre-configured for $5/week pricing
- Ready for Stripe payment integration

## Stripe Integration Setup

To connect the checkout page to Stripe:

### 1. Get Stripe API Keys
- Sign up at [stripe.com](https://stripe.com)
- Get your API keys from the Stripe Dashboard
- You'll need both the **Publishable Key** (for frontend) and **Secret Key** (for backend)

### 2. Add Stripe.js to checkout.html
Add this script tag in the `<head>` section:
```html
<script src="https://js.stripe.com/v3/"></script>
```

### 3. Initialize Stripe
Replace the placeholder JavaScript code in `checkout.html` with:
```javascript
const stripe = Stripe('your_publishable_key_here');
const elements = stripe.elements();
const cardElement = elements.create('card', {
    style: {
        base: {
            color: '#fff',
            fontSize: '16px',
        }
    }
});
cardElement.mount('#card-element');
```

### 4. Create Backend Payment Endpoint
You'll need a server endpoint to create payment intents. Example using Node.js:
```javascript
const stripe = require('stripe')('your_secret_key_here');

app.post('/create-payment-intent', async (req, res) => {
    const paymentIntent = await stripe.paymentIntents.create({
        amount: 500, // $5.00 in cents
        currency: 'usd',
        metadata: {
            email: req.body.email,
            discord: req.body.discord,
            krunker: req.body.krunker
        }
    });

    res.json({client_secret: paymentIntent.client_secret});
});
```

### 5. Handle Payment Submission
Uncomment and configure the Stripe integration code in the `checkout.html` file.

## Customization

- Update the Discord username collection to match your server
- Add your actual testimonials
- Customize the coaching features based on what you offer
- Add a success page (`success.html`) to redirect after payment
- Consider adding a terms of service and refund policy

## Deployment

Upload the HTML files to any web hosting service:
- GitHub Pages (free)
- Netlify (free)
- Vercel (free)
- Traditional web hosting

## Notes

- The checkout form currently shows a placeholder for Stripe
- Make sure to test in Stripe's test mode before going live
- Consider adding email confirmation after purchase
- You may want to add Google Analytics or similar tracking

## Legal

Remember to add:
- Terms of Service
- Privacy Policy
- Refund Policy
- Disclaimer (not affiliated with Krunker.io)
