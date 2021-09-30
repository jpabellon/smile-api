# API Reference

<!-- focus: false -->
![Authentication](https://img.icons8.com/ios-glyphs/50/000000/key--v1.png)

## Authentication

The Smile API uses HTTP Basic Auth. A set of credentials called API key and API secret, which is associated with your developer account can be used to access the Smile Network. To retrieve your credentials, contact access@getsmileapi.com

---
<!-- focus: false -->
![Modes](https://img.icons8.com/material-rounded/50/000000/switch-on.png)

## Modes of Operation
The API is available in two modes that can be accessed by sending requests to different base URLs. Each API client secret you are granted can only be used with a single mode. For example: an API client ID and secret granted to access the Sandbox can only be used in that mode.

| Mode        | Host                                        | Description |
|-------------|---------------------------------------------|-------------|
| Sandbox     | https://sandbox.smileapi.io/v1     |       Use Sandbox mode to build and test your integration. In this mode, you must use test credentials to authenticate with the employment data providers. All API endpoints will return mock data and no actual user data is returned.  |
| Production  | https://open.smileapi.io/v1  |       Production mode is used to go live with your integration. Your end-users will use their login credentials to authenticate with their employment data providers. API endpoints return real data and in this mode, all API calls are billable.  |

---
<!-- focus: false -->
![Versions](https://img.icons8.com/ios-glyphs/50/000000/versions.png)

## Versioning
The version is included in the URI Path. So for example it will look like: https://open.smileapi.io/v1/
- The versioning convention we use is the **1.2.3** format, where **1** is the major version, **2** is the minor version, and **3** is the patch update:
    - **Major version:** The version used in the URI and denotes breaking changes to the API. While we try to keep changes backward compatible, there may be occasions where we will need to introduce changes that might change existing behavior or functionality. These changes will be implemented in versions of the API accessible under a differnet URI (eg https://open.smileapi.io/v2/). You can continue to use the existing URI to avoid breaking existing integrations, but in order to take advantage of new features, you will have to update your application to point to the new version and URI. 
    - **Minor and Patch versions:** These are transparent to the client and we use this internally for backward-compatible updates. You do not need to update your integration when we release minor updates or patches. We will communicate these via via our change logs and email notifications, so you are updated with  any of these changes.


---
<!-- focus: false -->
![Alert](https://img.icons8.com/ios-glyphs/50/000000/error--v1.png)

## Error Messages

|HTTP Status Code|Status Description|Smile Code|Message|
|----------------------|----------------------|----------------------|----------------------|
|400 - Bad Request         |The request could not be understood by the server due to incorrect syntax. The client SHOULD NOT repeat the request without modifications.       |INVALID_CREDENTIALS   |The credentials you provided are incorrect.                                                                                       |
|400 - Bad Request         |The request could not be understood by the server due to incorrect syntax. The client SHOULD NOT repeat the request without modifications.       |INVALID_PARAMETERS    |Missing or invalid parameters were sent in your request.                                                                          |
|401 - Unauthorized        |Indicates that the request requires user authentication information. The client MAY repeat the request with a suitable Authorization header field|INVALID_TOKEN         |The token you provided is invalid or has expired.                                                                                 |
|403 - Forbidden           |Unauthorized request. The client does not have access rights to the content. Unlike 401, the client’s identity is known to the server.           |UNAUTHORIZED_ACCESS   |You do not have permission to access this resource.                                                                               |
|404 - Not Found           |The server can not find the requested resource.                                                                                                  |MISSING_RESOURCE      |The resource you provided cannot be found or is unavailable.                                                                      |
|415 - Unsupported Media Type           |The payload format is either not defined or is in an unsupported format.                                                                                                  |UNSUPPORTED_TYPE      |Please specify a valid content type for your request.                                                                      |
|429 - Too Many Requests   |Too many requests sent in a given amount of time                                                                                                 |REQUEST_LIMIT_EXCEEDED|You have exceeded your rate limit for this resource. Please try again later or contact support.                                   |
|500 - Internal Server Error |The server encountered an unexpected condition which prevented it from fulfilling the request.                                                   |SERVER_ERROR          |Our system is currently experiencing issues. Please try again later or contact support.                                           |
|501 - Not Implemented      |The HTTP method is not supported by the server and cannot be handled.                                                                            |UNSUPPORTED_METHOD    |The HTTP method you used is not supported for this resource.                                                                      |
|503 - Service Unavailable  |The server is not ready to handle the request.                                                                                                   |SERVER_UNAVAILABLE    |The server is not available to handle the request. It may be down or under maintenance. Please try again later or contact support.|
|504 - Gateway Timeout      |The server cannot give a response in time.                                                                                                       |TIME_LIMIT_EXCEEDED   |The server was not able to give a response in the allotted time. Please try again or contact support.  

---
<!-- focus: false -->
![Pagination](https://img.icons8.com/windows/50/000000/choose-page.png)

## List results and pagination

Resources or API endpoints, return a list or a collection of objects. By default we return 10, with a maximum of 100, at a time. You can limit the results by passing a parameter for size. For more information on filterig or limiting results, see below on query parameters.

When Smile returns a collection, we will also return a value called **nextCursor**. See below for an example:

```json
{
    "code": "OK",
    "message": "Success!",
    "requestId": "17bc5a84-2468-47f6-9d3c-05b5257befa5",
    "data": {
        "nextCursor": "20",
        "items": [...]
    }
}
```

To go to the next page in a collection, simply append the **cursor** parameter when you query an endpoint, using the **nextCursor** value returned from your previous query to go to the next page in the collection. See below for more information on cursor and other query parameters.

---
<!-- focus: false -->
![Parameters](https://img.icons8.com/ios-glyphs/50/000000/filled-filter.png)

## Query Parameters

API endpoints which return a list or collection of objects can be filtered or limited based on different query parameters. Below are some examples:

|Parameter |Description |
|----------------------|----------------------|
| size | The number of objects you want returned in a collection. See more information above on default values. |
| cursor | Uses the filter values of the previous page to determine the next set of items. See more information above on pagination. |
| userId | Filter the results by the associated userId |
| acccountId | For account-related data, filter the results based on the associated accountId |

Some resources however have unique query parameters associated with them. Check out the documentation in each of the endpoints to find out more.

---
<!-- focus: false -->
![Rate Limits](https://img.icons8.com/ios-filled/50/000000/traffic-light.png)


## Rate Limits

Smile limits the amount of API calls that can be made to each endpoint to ensure the stability and availability of the platform. At the moment we only allow clients a maximum of up to 5 requests per endpoint per second. Clients which make too many requests in succession will be given an error with HTTP Status Code 429 or too many requests. To request a higher limit, please contact access@getsmileapi.com.

