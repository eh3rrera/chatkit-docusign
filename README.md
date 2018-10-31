# E-signatures in chats with ChatKit and Docusign

Chat build with React and [Chatkit](https://pusher.com/chatkit) that uses a Node.js server to post messages. However, users can only post messages after signing a document using [Docusign API](https://www.docusign.com/). Follow the tutorial [here](https://pusher.com/tutorials/esignatures-chatkit-docusign).

## Getting Started

1. Clone this repository.
2. Create a [Chatkit instance](https://dash.pusher.com/chatkit) if you haven't already.
3. In the Chatkit dashboard of your instance, in the *Instance Inspector* section, create one or two users and one chat room.
4. Follow [this guide](https://developers.docusign.com/esign-rest-api/guides) to:
  - Sign up for a [Docusign developer sandbox](https://go.docusign.com/o/sandbox/).
  - Create an integrator key with a Redirect URI and RSA keypair (this will be your only chance to save these keys)
  - Add a template using the document you find in this repo (`nda.pdf`) or your own.
5. Grant access to your integration key by visiting this URL (replace your integration key and redirect URI): `https://account-d.docusign.com/oauth/auth?
response_type=code&scope=signature%20impersonation&client_id=INTEGRATION_KEY&redirect_uri=REDIRECT_URI`.
6. In the file `src/App.js` enter:
  - Your Chatkit instance locator, something like `v1:us1:xxxxxxxxxxxxxxxx`
7. In the file `src/ChatScreen.js` enter:
  - Your Chatkit room ID
8. In the file `server.js` enter:
  - From Docusign:
    - Your Integrator Key
    - Your username API
    - Your template ID and role
    - A subdomain for the public URL of your server (that will be configured using [localtunnel](https://github.com/localtunnel/localtunnel))
  - From Chatkit:
    - Your Chatkit instance locator, something like `v1:us1:xxxxxxxxxxxxxxxx`
    - Your Chatkit secret key, something like `0710e105-5f59-20765:rPejy0yUx3VzI=`
  - One or two users's IDs and emails. The ID must match the one registered in Chatkit. In that email the user will receive the document from Docusign.
9. Create a directory `keys` and inside of it, the file `docusign_private_key.txt` and paste the RSA private key from your integrator key. 
10. In a terminal window, execute `npm install` to install the dependencies of the app.
11. Execute the server and the chat app with `npm start`.
12. In another terminal window, install [localtunnel](https://github.com/localtunnel/localtunnel) with `npm install -g localtunnel` and execute `lt --subdomain YOUR_SUBDOMAIN --port 3001` to expose your local server to the world so Docusign can call your webhook (the subdomain must match the one entered in `server.js`).
13. Enter the username in the first screen of the app to enter the chat.
14. Try sending a message. You won't be able to do it.
15. Click on the button `Send NDA` to receive the document in the user's email and sign it.
16. Monitor the server console to know when the webhook was called with the completion event.
17. From that moment, the user will be able to send messages.
18. Optionally, open the app in another browser to log in as another user, sign the document, and start chatting.

### Prerequisites

- [Chatkit account](https://dash.pusher.com)
- [Node.js](https://nodejs.org/en/download/)

## Built With

* [Pusher Chatkit](https://pusher.com/chatkit) - Developer-driven chat done simply
* [Docusign](https://www.docusign.com/) - eSignature solutions
* [React.js](https://reactjs.org/) - A JavaScript library for building interfaces
* [Node.js](https://nodejs.org/) - A JavaScript runtime built on Chrome's V8 JavaScript engine

## Acknowledgments
* Thanks to [Pusher](https://pusher.com/) for sponsoring this tutorial.

## LICENSE
MIT