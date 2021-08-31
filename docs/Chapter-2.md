# Getting Started

---
<!-- focus: false -->
![Checklist](https://img.icons8.com/ios/50/000000/checklist--v1.png)

## Integration Steps
Its easy to get started with the Smile API! Implementing the Smile API involves simple client and server-side integration, which are outlined below in five key steps:

1. **Link token:** Your application server sends a request to our REST API to generate a short-lived "Link" token.

2. **Wink Widget:** Using the Link token, your application client initializes the client SDK to launch the Smile Wink widget. Your end-users interact with this widget to submit their login credentials to authenticate with their employment data provider over a secure and encrypted connection.

3. **User Creation:** Once the user successfully authenticates via the Smile Wink widget, a user account is created representing the user's authorized access to a specific employment data provider.

4. **Actions:** Our servers execute your application's requests. We read, transform, and temporarily store data from the user's employment data provider so that it can be sent to the client application.

5. **Webhooks (coming soon):** Webhooks can also be delivered to your server in cases where data will be processed asynchrounously. Messages via webhook will be sent whenever data becomes available or is updated. Your server can then fetch the data from our REST API.

---
<!-- focus: false -->
![Signup](https://img.icons8.com/ios-filled/50/000000/sign-up.png)

## Signing up for a Developer Account
To get started, register your application with us by emailing developers@getsmileapi.com.

After registration, your application will be assigned a client ID and a client secret. The client secret must be kept safe and used only in exchanges between your application's server and Smile API's server.

---
<!-- focus: false -->
![Modes](https://img.icons8.com/material-rounded/50/000000/switch-on.png)

## Modes of Operation
The API is available in two modes that can be accessed by sending requests to different base URLs. Each API client secret you are granted can only be used with a single mode. For example: an API client ID and secret granted to access the Sandbox can only be used in that mode.

| Mode        | Host                                        | Description |
|-------------|---------------------------------------------|-------------|
| Sandbox     | https://sandbox.smileapi.io     |       Use Sandbox mode to build and test your integration. In this mode, you must use test credentials to authenticate with the employment data providers. All API endpoints will return mock data and no actual user data is returned.  |
| Production  | https://open.smileapi.io  |       Production mode is used to go live with your integration. Your end-users will use their login credentials to authenticate with their employment data providers. API endpoints return real data and in this mode, all API calls are billable.  |

---
<!-- focus: false -->
![Versions](https://img.icons8.com/ios-glyphs/50/000000/versions.png)

## Versioning
The version is included in the URI Path. So for example it will look like: https://open.smileapi.io/v1/
- The versioning convention we use is the **1.2.3** format, where **1** is the major version, **2** is the minor version, and **3** is the patch update:
    - **Major version:** The version used in the URI and denotes breaking changes to the API. While we try to keep changes backward compatible, there may be occasions where we will need to introduce changes that might change existing behavior or functionality. These changes will be implemented in versions of the API accessible under a differnet URI (eg https://open.smileapi.io/v2/). You can continue to use the existing URI to avoid breaking existing integrations, but in order to take advantage of new features, you will have to update your application to point to the new version and URI. 
    - **Minor and Patch versions:** These are transparent to the client and we use this internally for backward-compatible updates. You do not need to update your integration when we release minor updates or patches. We will communicate these via via our change logs and email notifications, so you are updated with  any of these changes.
