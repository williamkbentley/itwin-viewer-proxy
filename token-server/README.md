# Token Server

The goal of the this token server is to provide an example of how to implement a two-legged authentication workflow for interacting with the iTwin Platform and configure it for the iTwin Viewer.

This server holds the client secret created for your application and manages issuing the token to a client-side application that will allow access to the
the iTwin Platform. This will enforce a secure workflow when implementing the [client credentials workflow](https://developer.bentley.com/apis/overview/authorization/#clientcredentialflow).

> __Important__: It is strongly recommended that this server be placed behind a layer of authorization and/or authentication that fits your workflow and validates the user has access to get the token required. However to simplify the example, this server will not be setup with any additional checking and essentially provide an "unprotected" endpoint.

## Setup token server

Use the CLIENT_ID and CLIENT_SECRET created in the [client registration](../README.md#client-registration) to populate the values in the `.env`.

Run,

- `npm install`
- `npm run build`
- `npm start`
- Note the port the server starts on, that will be used when configuring the Viewer.
  - The PORT can be configured by setting the `PORT` in the `.env`

## Setup the iTwin Viewer to use the token server

To configure the viewer to use the token server, make the following change to the `Viewer` component in [App.tsx](../react-viewer/src/App.tsx):

```jsx
<Viewer
  // ... (iModel related information)
  authClient={myTokenServerAuthClient}
>
```

If a custom port is defined in setting up the token server, provide the new port using `TOKEN_URL`. The default value is, `http://localhost:3001/getToken`.
