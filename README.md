# Clerk Next.js Infinite redirect repro in standalone mode

## To reproduce

1. Install dependencies: `npm install`
2. Build the app, substituting the publishable key with a production key: `NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=[PROD_PUBLISHABLE_KEY] npm run build`
3. Run the app in standalone mode, using a production secret key: `CLERK_SECRET_KEY=[PROD_SECRET_KEY] node .next/standalone/server.js`
4. Make a curl request to the root route, or to any non-existing route. E.g. `curl -v http://localhost:3000/`

## Expected behavior

You should be redirected to the sign-in page.

## Actual behavior

The app enters an infinite redirect loop, making middleware calls with requests to urls of the form `http://localhost:3000/clerk_1736122693051` where the last number is changing with each request.
