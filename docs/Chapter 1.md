# Welcome


<img src="https://img.icons8.com/material-outlined/48/000000/smiling.png"/>

##  Overview
Smile provides user-authorized access to valuable employment and income data from HR, payroll, commerce, and marketplace platforms through a single API. Banks, fintechs, recruitment agencies, and other service providers can leverage employment and income data to increase adoption and conversion, reduce cost, and reduce risk, through a single API. Access is given by the users themselves, so they can seamlessly share their data to the providers they trust.

---

<img src="https://img.icons8.com/ios/50/000000/checklist--v1.png"/>

## Implementation Overview
The Smile API is easy to integrate and highly customizable. Implementing Smile involves a simple client and server side integration, which be are outlined in five key steps:

1. Blink token: Your application server sends a request to our REST API to generate a short-lived token called a 'Blink'.

2. Wink login modal: Using the Blink token, your application client initializes the client SDK to launch the Smile Wink modal. Your end-users interact with Wink to submit their login credentials to authenticate with their employment data provider over a secure and encrypted connection.

3. User Creation: Once the user successfully authenticates via Smile Wink, a User account is created representing the user's authorized access to a specific employment data provider.

4. Actions: Our servers execute the requested actions. We read, transform, and temporarily store data from the user's employment data provider so that it can be sent to the client application.

5. Webhooks: Webhooks can also be delivered to your server in cases where data will be processed asynchrounously. Messages via webhook will be sent whenever data becomes available or is updated. Your server can then fetch the async data from our REST API.
----

<img src="https://img.icons8.com/ios-filled/50/000000/sign-up.png"/>

## Signing up for a Developer Account
To get started, register your application with us by emailing developers@getsmileapi.com.

After registration, your application will be assigned a client ID and a client secret. The client secret must be kept safe and used only in exchanges between your application's server and Smile API's server.

---
<img src="https://img.icons8.com/ios-filled/50/000000/find-matching-job.png"/>

## Available employment data
After a user authorizes access to their employment data, several 'actions' can be executed. For example, employment history and past income can be retrieved. The user can authorize which particular data of theirs can be retrieved, which as a developer you can then translate into specific instructions via parameters in the requests you will send to Smile to perform.

The available data includes:

| Action   | Type    | Description |
|----------|---------|-------------|
| Identity | Profile | Get vetted identity information from current and previous employers such as name, contacts, address, and document verification status.|
| Jobs     | Profile | Get previous employment history, including job title, status, tenure, employer names, employer contact information, and others.|
| Income   | Profile | Get previous earnings information such as gross pay, net pay, taxes, deductions, and other components that make up income.|  

