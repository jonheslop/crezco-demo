# Crezco Demo App

A [Next.js](https://nextjs.org/) demo app which allows a user to:

- Onboard to Crezco
- Create an Invoice
- Create Crezco payment link and QR
- Recieve realtime notification of payment via websockets and a webhook

Learn more here — https://documentation.crezco.com/docs/partner/docs/Tutorials/F%20Full%20Onboarding.md
## Prerequisites

- A Crezco sandbox API key
- A webhook set up for all payment events - https://documentation.crezco.com/docs/partner/docs/Tutorials/Web-hooks.md#test-a-webhook

## How to use

`yarn dev`
Starts the development server.

`yarn build`
Builds the app for production.

`yarn start`
Runs the built app in production mode.

## User journey

1. User is passed to Crezco to create an account - [pages/index.js#L30-L32](https://github.com/Crezco-Limited/crezco-demo/blob/main/pages/index.js#L30-L32)
2. User is passed back to demo app with user UUID as query param
  - User info fetched before render - [lib/get-user-props.js](https://github.com/Crezco-Limited/crezco-demo/blob/main/lib/get-user-props.js)
3. User inputs invoice details - [pages/create-invoice.js](https://github.com/Crezco-Limited/crezco-demo/blob/main/pages/create-invoice.js)
  - This info is used to create a Pay Demand - [lib/create-pay-demand.js](https://github.com/Crezco-Limited/crezco-demo/blob/main/lib/create-pay-demand.js)
4. Pay demand details presented to user — [pages/invoice/\[id\].js](https://github.com/Crezco-Limited/crezco-demo/blob/main/pages/invoice/%5Bid%5D.js)
  - Pay demand details fetched from api — [lib/get-pay-demand.js](https://github.com/Crezco-Limited/crezco-demo/blob/main/lib/get-pay-demand.js)
  - Page uses [Pusher](https://www.pusher.com) to listen on websocket for payment event. - [pages/invoice/\[id\].js#L16-L31](https://github.com/Crezco-Limited/crezco-demo/blob/main/pages/invoice/%5Bid%5D.js#L16-L31)
  - A webhook has been configured to POST to an API endpoint when the payment is made which triggers a event - [pages/api/payment-webhooks.js](https://github.com/Crezco-Limited/crezco-demo/blob/main/pages/api/payment-webhooks.js)

## Further reading

- [Crezco developer docs](https://documentation.crezco.com)
- [Next.js docs](https://nextjs.org/docs/getting-started)
- [Tailwind CSS](https://tailwindcss.com/)

