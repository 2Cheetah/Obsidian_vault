# REST API
#api #restapi 

## Definition

REST stands for **re**presentational **s**tate **t**ransfer and is a software architecture style that defines a pattern for client and server communications over a network. REST provides a set of constraints for software architecture to promote performance, scalability, simplicity, and reliability in the system.

REST defines the following architectural constraints:
- Stateless: The server won’t maintain any state between requests from the client.
- Client-server: The client and server must be decoupled from each other, allowing each to develop independently.
- Cacheable: The data retrieved from the server should be cacheable either by the client or by the server.
- Uniform interface: The server will provide a uniform interface for accessing resources without defining their representation.
- Layered system: The client may access the resources on the server indirectly through other layers such as a proxy or load balancer.
- Code on demand (optional): The server may transfer code to the client that it can run, such as JavaScript for a single-page application.
Note, REST is not a specification but a set of guidelines on how to architect a network-connected software system.

## HTTP Methods

Main five HTTP methods:
1. GET - retrieve an existing resource
2. POST - create new resource
3. PUT - update existing resource
4. PATCH - partially update existing resource
5. DELETE - remove a resource

## HTTP status codes

|Code|Meaning|Description|
|-----:|:--------|:------------|
|200|OK|The required action was sucsessful|
|201|Created|A new resource was created|
|400|Bad Request|The request was malformed|
|401|Unauthorized|The client is not authorized to perform the request action|
|404|Not Found|The requested source was not found|
|500|Internal Server Error|The server threw an error when processing the request|

|Code range|Category|
|------:|:----------|
|2xx|Successful operation|
|3xx|Redirection|
|4xx|Client error|
|5xx|Server error|

## API Endpoints

|HTTP method|API endpoint|Description|
|-------:|:----------|:------------|
|`GET`|`/customers`|Get a list of customers.|
|`GET`|`/customers/<customer_id>`|Get a single customer.|
|`POST`|`/customers`|Create a new customer.|
|`PUT`|`/customers/<customer_id>`|Update a customer.|
|`PATCH`|`/customers/<customer_id>`|Partially update a customer.|
|`DELETE`|`/customers/<customer_id>`|Delete a customer.|

