# Getting User Data 

Getting user data into your application involves two things:

 - **Embedding a Javascript SDK for your web application client**. At the moment, Smile only provides a Javascript SDK, but native verions of the SDK for mobile applications such as iOS or Android are coming soon. The Javascript SDK launches a modal window called a "Wink" web widget where users can provide permission for Smile to access their data. Users will first find their employer or employment data provider, then submit their login credentials over a secure and encrypted connection. By using the SDK, you will not have to worry about the different authentication and verification implementations of the different employment platforms, making the integration simple for your developers, and the experience smooth for your users. 

 - **Obtaining a user token from the Smile Open API**. Your back-end server should obtain a "Link" token  from the /users endpoint. This is a single use, short-lived token which is used to initialize the Wink widget. Your server should generate a new Link token each time you wish to launch the widget.

---
<!-- focus: false -->
![Code](https://img.icons8.com/ios/50/000000/code.png)

## Example Code
Below is sample HTML code which embeds the Wink Javascript SDK:

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="icon" href="smileicon32.webp" sizes="32x32">
    <link rel="icon" href="smileicon192.webp" sizes="192x192">
    <title>Smile Wink Quickstart</title>
</head>

<body>
    <script src="https://web.smileapi.io/v1/smile.v1.js"></script>
    <script type="text/javascript">
        const smileLinkModal = new SmileLinkModal({
            /**
             * The Link API URI. Note: Sandbox and Production modes are using different API URIs.
             */
            apiHost: 'https://link-sandbox.smileapi.io/v1',
            /**
             * User token passed from your backend service which is obtained from the Smile API.
             */
            userToken: '<usertoken>',

            onAccountCreated: ({
                accountId,
                userId,
                providerId
            }) => {
                console.log('Account created: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            onAccountConnected: ({
                accountId,
                userId,
                providerId
            }) => {
                console.log('Account connected: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            onAccountRemoved: ({
                accountId,
                userId,
                providerId
            }) => {
                console.log('Account removed: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            onClose: () => {
                console.log('Link closed')
            },

            onTokenExpired: updateToken => {
                console.log('Token expired');
            }
        });
        smileLinkModal.open()
    </script>
</body>
</html>

```

### Configuration parameters

| Parameter |Value |
|----------|---------|
| apiHost | https://link-sandbox.smileapi.io/v1 for Sandbox |
|         | https://link.smileapi.io/v1 for Production |
| userToken | The user token returned from Smile using the /users endpoint (see documentation on Users endpoint) |

---
<!-- focus: false -->
![Example](https://img.icons8.com/material/50/000000/example.png)

## Quickstart Sample Implementation
> We provide sample code in [Github](https://github.com/SmileAPI/quickstart) which you can download and modify according to your own requirements. 

The example code installs a small server running on Node.js that automatically retrieves a token from our API, so you can instantiate the Wink widget. 

The example implementation is composed of two parts:
* Under /frontend, you will find example code in HTML that already has the Wink Javascript SDK embedded already.
* Under /node, you will find server-side Javascript code that will retrieve the token. You will need to download and run Node.js to run the code.


### Implementation steps
Below steps are also included in the README.md document included in the the Quickstart [repository] and [archive].
1. Download the Quickstart files onto your machine.

2. Go to /node directory of Quickstart.

3. Create a new file with called ".env" in that directory.

4. Make sure you have proper permissions in your machine to be able to create the file. 

> For example, in Mac or Linux machines open up the Terminal, you can use vi and enter the following commands as a Super User:

```bash
touch .env
```

> On Windows machines, Windows will not allow you to create a .env file directly from Windows Explorer since it will not allow file names starting with a ".". To get around this:

```
1. Open Notepad oand write the content of the file (see below).
2. Goto FILE-> SAVE AS Save as Screen in the notepad.
3. Select the All files() type in the selection window.
4. Save the file as ".env" 
```

5. Open up the ".env" file that you just created in your favorite editor, and enter the following:

```bash
# The port you want the example server to listen to
APP_PORT=<portnumber>

# Smile Link API keys (you can get this by requesting access from access@getsmileapi.com)
API_KEY_ID=<apikeyid>
API_KEY_SECRET=<apisecret>

# API Host (whether this will run in Sandbox or Production)
API_HOST=<apiURL>
```

> **You can use as reference ".env.example" included in the Quickstart repository or archive**


6. Save and close your file.

7. If you don't have Node.js installed in your machine, install Node.js. 

> For example on the Mac you can open up the Terminal and run:

```bash
curl "https://nodejs.org/dist/latest/node-${VERSION:-$(wget -qO- https://nodejs.org/dist/latest/ | sed -nE 's|.*>node-(.*)\.pkg</a>.*|\1|p')}.pkg" > "$HOME/Downloads/node-latest.pkg" && sudo installer -store -pkg "$HOME/Downloads/node-latest.pkg" -target "/"
```

> For Windows you can [download the installer](https://nodejs.org/en/#home-downloadhead).

> For other operating systems, [you can find the instructions](https://nodejs.org/en/download/package-manager/#macos) from the Node.js website.


8. Run Yarn with [npm package manager](https://www.npmjs.com/) which is included with Node.js and enter the following commands:

> In Mac or Linux, you will need to open up the Terminal. If you are using Windows, you can go to the command line. Make sure you are still in the /node directory of the Quickstart files you just downloaded onto your machine.

```bash
npm install --global yarn
yarn install
```

8. Run the server:
```bash
node index.js
```

9. Open up the your browser and open up the example Wink Widget. For example, if you specified port:8000 in your ".env" configuration file, open up http://127.0.0.1:8000 in your web browser.

10. Sit back, relax, and pat yourself on the back for a job well done!

---
<!-- focus: false -->
![Token](https://img.icons8.com/ios/50/000000/sms-token.png)

## Issuing a New Token
You can issue a new token for a user by calling the /tokens endpoint. Simply pass the userid as an argument in the Body of the request to give the user a new token. More information can be found in the Tokens endpoint documentation.

---
<!-- focus: false -->
![Event](https://img.icons8.com/ios/50/000000/important-event.png)

## Link events 
As the user moves through the Wink widget screen, any activities performed by the user are captured and are etiher used to update the messsages and presentation of the modal window, or are sent to Smile so that any account-related data can be updated. 

In the case of the latter, if the the user was able to successfully authenticate with an employment data provider, the Account status is changed to "CONNECTED". The account status of the user can be queried at any time via the /accounts endpoint. Examples of the events captured include:

| Event |Description |
|----------|---------|
| PENDING | The account was created but is pending successful authentication |
| AWAITING_MFA | The user was able to successfully authenticate however the data provider is waiting for the user to enter their verification code in a 2-factor authentication scenario. |
| ERROR | The data provider returned an error. The user may not have entered the wrong credentials or there was a problem on the side of the provider. |
| CONNECTED | The user was able to successfully authenticate with an employment data provider. |
