# Introduction
The Smile API is built on RESTful principles. All request and response payloads are encoded in JSON. For security purposes, all requests must be sent through HTTPS. To get access to the Developer Dashboard and interface with the API, please contact sales@getsmileapi.com.

---

<img src="https://img.icons8.com/small/64/000000/process.png"/>

## Modes
The API is available in three environments that can be accessed by sending requests to different base URLs. Each API Key you are granted can only be used with a single environment. For example: an API Key granted to access the Sandbox environment can only be used in that environment.

| Mode        | Host                                        | Description |
|-------------|---------------------------------------------|-------------|
| Sandbox     | https://access.getsmileapi.com/sandbox/     |       Use Sandbox mode to build and test your integration. In this mode, you must use test credentials to authenticate with the employment data providers. All API endpoints will return mock data and no actual updates are made to any payroll account.  |
| Development | https://access.getsmileapi.com/development/ |       Development mode can be used to test your integration before going live in Production. In this mode, you use real credentials to authenticate with the employment data providers. API endpoints will return real data.    |
| Production  | https://access.getsmileapi.com/production/  |       Production mode is used to go live with your integration. Your end-users will use their login credentials to authenticate with their employment data providers. API endpoints return real data and in this mode, all API calls are billable.  |

---

<img src="https://img.icons8.com/ios-glyphs/60/000000/api.png"/>

## Conventions