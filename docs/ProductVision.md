# Example Data Owner Journey

Smile Network allows end users or data owners to give access to their data stored in a variety of providers (eg payroll, HRIS, gig platforms) to applications that require it like banking apps or lending apps. This can be done through a Smile Network "bridge" mechanism that links a user's profile to their employer and employment detail. Users will authenticate via a frontend mechanism (a web modal or redirect called "Greet") that developers will use to allow the data owner to authenticate and share their data

## Data Owner Personas

[Role + Tasks + Goals 🛠️](https://www.notion.so/a726339271e94a989f87e953e66de394)

## Example Steps

[https://www.figma.com/embed?embed_host=notion&url=https%3A%2F%2Fwww.figma.com%2Ffile%2FOfpncUGSJz4eUBDOPPuC71%2FAuthorization-Flow%3Fnode-id%3D0%253A1](https://www.figma.com/embed?embed_host=notion&url=https%3A%2F%2Fwww.figma.com%2Ffile%2FOfpncUGSJz4eUBDOPPuC71%2FAuthorization-Flow%3Fnode-id%3D0%253A1)

1. User will open a lending or banking app to sign up
2. Lending or banking app will ask them to pull their data from their employer / work system (whether its a payroll, HR or gig platform)
3. User will click on a button, and then will be shown a "Greet" modal window. Greet will ask them for:
    - their government ID, which will automatically associate their user account to an identity object with value aggregated from provider parters

        [Envisioned%20Feature%20Set%20and%20User%20Journeys%20f3b7ba91cfac489f921b9a31305494c9/Screen_Recording_2021-04-14_at_4.13.36_PM.mov](Envisioned%20Feature%20Set%20and%20User%20Journeys%20f3b7ba91cfac489f921b9a31305494c9/Screen_Recording_2021-04-14_at_4.13.36_PM.mov)

        - passport
        - drivers license
        - Universal ID
        - health insurance ID
        - social security ID
        - tax ID
        - postal ID
        - Voters ID
        - Professional License ID
        - Senior Citizen ID
        - OFW ID
    - ***if this fails,*** they can select either their employer or platform they want to use, and ask them to login

    [Envisioned%20Feature%20Set%20and%20User%20Journeys%20f3b7ba91cfac489f921b9a31305494c9/Screen_Recording_2021-04-14_at_4.19.26_PM.mov](Envisioned%20Feature%20Set%20and%20User%20Journeys%20f3b7ba91cfac489f921b9a31305494c9/Screen_Recording_2021-04-14_at_4.19.26_PM.mov)

4. Behind the scenes, we can probably create a user account (eg Accounts) for them, create an object (eg "Bridge") that specifies what data sources they have access to, which also creates and stores token for connection
5. Data (as designed by our client's developer) then pulls in the data the app needs to show to the user such as Identity details and Employment history, with the user Account token 
6. Behind the scenes, we can probably create an object called "Actions" that pull data from the data source,  translate it then serve it up via our unified API. These Actions in some cases work instantaneously and can send data via HTTP Response, or asynchronously, and can send data via Webhook to send the data payload or update client app of the status of the job

![Envisioned%20Feature%20Set%20and%20User%20Journeys%20f3b7ba91cfac489f921b9a31305494c9/Untitled.png](Envisioned%20Feature%20Set%20and%20User%20Journeys%20f3b7ba91cfac489f921b9a31305494c9/Untitled.png)

# Example Implementer Journey

Smile Network will make it easy for developers to read employee and employer data across various providers (eg payroll, HRIS, gig platforms) and in some cases, push changes across providers using Secure HTTP requests. We use built-in HTTP features like HTTP verbs (GET, POST, PUT, PATCH, DELETE) and HTTP authentication so developers can use any HTTP client. All responses are returned in standard JSON (maybe XML?).

## Implementer Personas

[Role + Tasks + Goals 🛠️](https://www.notion.so/48ebd61a117e43d9a5b2458a457214b5)

## Steps

1. First, a [developer](https://www.notion.so/Mobile-App-Developer-6168084d55b943159ba6db9def676c0f) or [tester](https://www.notion.so/API-Tester-ee6beca4e2614fc6a871f4873422001a) will visit Smile Network website to register for an account (eg https://www.smilenetwork.io)
2. Once registered, he/she will get a dashboard where he/she can get an API key. 
3. This key will be sent to get a secure, expiring token, which will be used to access data from the Smile Network. Requests made to the Smile Network API will require this token. 
4. This API token should be sent in the header of all API requests. 
5. API request allows a developer to trigger "Actions" that can probably leverage permission stored in a "Bridge" that has the associated Data Owner account and credentials. These jobs can return data instantanously via HTTP Response, or run asynchronously in the background and return data via Webhook
6. Developer/tester will visit a documentation site (eg https://docs.smilenetwork.io) to be able to  understand and test (in a mockup) how the APIs behave
7. Developer/tester can have access to different environments provided by Smile Network
    - Production URL (eg https://prod.getsmileapi.com/{version})
    - Sandbox URL (eg https://sandbox.smilenetwork.io/{version})
8. Developer/tester can start implementing APIs

For reference, read up on the API implementation of similar companies:

[Similar Companies](https://www.notion.so/a3a997da158d4cafbaab8c76af382309)

# Example "Marketing" Naming for the Products

Detailed API design to follow

## Blink (Data Integration for Verification)

- General
    - Authorization mechanism - allows applications to authorize with payroll and HRIS providers
    - GET list of supported platforms/data sources
    - GET list of employers/companies
    - Webhooks - push data to 3rd party endpoint
- Employer
    - GET employer: company info detail (eg company name, address)
- Employee
    - GET employee: employment detail (eg name, title, start date)

## Wink (Data Integration for Verification+Data Enrichment)

- General
    - Authorization mechanism - allows applications to authorize with payroll and HRIS providers
    - GET list of supported platforms/data sources
    - GET list of employers/companies
    - Webhooks - push data to 3rd party endpoint
- Employer
    - GET employer: company info detail (eg company name, address)
    - GET employer: company health detail (income, expense, financial ratios, credit rating)
- Employee
    - GET employee: identity detail (eg address/number/ID/social media profile veritfication)
    - GET employee: employment detail (eg name, title, start date)
    - GET employee: income detail (eg gross pay, net pay, deductions, past payslips)

## Greet  (employee authorization)

- Authorization mechanism - allows applications to authorize with payroll and HRIS providers
- Embeddable/linkable page - Creates a frontend modal which allows employees access to search for their employer or payroll provider and authorize access
- SDK - provides a turnley framework to allow mobile developers to include the service in their native apps (iOS andAndroid)

## Beam (Self-service Data Portal and Data Visualization)

- User login/authentication
- GUI/Data entry form-frontend for data consumer/auditor to enter company and employee information
- Evaluation Report-summarized/aggregated/normalized data showing employer and employee information
- Notifications/integrations - ability to access portal data via API, and to get email or push notifications of completed evaluation reports
- Webhooks - push data to 3rd party endpoint

## Grin (Direct Deposit Switching)

- General
    - Authorization mechanism - allows applications to authorize with payroll and HRIS providers AS WELL as banking accounts
- Banking Information
    - GET employee: bank deposit information from banking system
    - CREATE/UPDATE employee bank deposit information in banking system
- Employee Information
    - GET employee: employment detail (eg name, title, start date)
    - GET employee: income detail (eg gross pay, net pay, deductions, past payslips)
    - GET employee: direct deposit information in payroll system
    - CREATE/UPDATE employee bank deposit information in payroll system