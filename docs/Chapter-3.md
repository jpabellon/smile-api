# API Reference

---
<!-- focus: false -->
![Authentication](https://img.icons8.com/ios-glyphs/50/000000/key--v1.png)

## Authentication

The Smile API uses HTTP Basic Auth. A set of credentials called client_id and client_secret, which is associated with your developer account can be used to access the Smile Network. To retrieve your credentials, contact access@getsmileapi.com

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
|429 - Too Many Requests   |Too many requests sent in a given amount of time                                                                                                 |REQUEST_LIMIT_EXCEEDED|You have exceeded your rate limit for this resource. Please try again later or contact support.                                   |
|500 - Internal Server Error |The server encountered an unexpected condition which prevented it from fulfilling the request.                                                   |SERVER_ERROR          |Our system is currently experiencing issues. Please try again later or contact support.                                           |
|501 - Not Implemented      |The HTTP method is not supported by the server and cannot be handled.                                                                            |UNSUPPORTED_METHOD    |The HTTP method you used is not supported for this resource.                                                                      |
|503 - Service Unavailable  |The server is not ready to handle the request.                                                                                                   |SERVER_UNAVAILABLE    |The server is not available to handle the request. It may be down or under maintenance. Please try again later or contact support.|
|504 - Gateway Timeout      |The server cannot give a response in time.                                                                                                       |TIME_LIMIT_EXCEEDED   |The server was not able to give a response in the allotted time. Please try again or contact support.         

---
<!-- focus: false -->
![Parameters](https://img.icons8.com/ios-glyphs/50/000000/filled-filter.png)

## Query Parameters

API endpoints which return a collection of objects can be filtered or limited based on different query parameters:

|Parameter |Description |
|----------------------|----------------------|
|size |The number of objects you want returned in a collection |
|cursor |Uses the filter values of the previous page to determine the next set of items |

Some resources however have unique query parameters associated with them. Check out the documentation in each of the endpoints to find out more.

---
<!-- focus: false -->
![Rates](https://img.icons8.com/ios-filled/50/000000/traffic-light.png)

## Rate Limits

Smile limits the amount of API calls that can be made to each endpoint to ensure the stability and availability of the platform. At the moment we only allow clients a maximum of up to 50 requests per endpoint per second. Clients which make too many requests in succession will be given an error with HTTP Status Code 429 or too many requests. To request a higher limit, please contact access@getsmileapi.com.

