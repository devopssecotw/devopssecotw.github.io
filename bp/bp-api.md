# dos
## bp
### API
#### RESTful web API design
##### What is REST?
##### Organize the API design around resource
    * Focus on the business entities that the web API exposes. 
    * A resource doesn't have to be based on a single physical data item
##### Define API operations in terms of HTTP methods
##### Conform to HTTP semantics
##### Filter and paginate data
##### Support partial responses for large binary resources
##### Use HATEOAS to enable navigation to related resources
##### Versioning a RESTful web API 
##### Open API Initiative


#### Web API implementation
##### Processing requests
###### GET, PUT, DELETE, HEAD, and PATCH actions should be idempotent
###### POST actions that create new resources should not have unrelated side-effects
###### Avoid implementing chatty POST, PUT, and DELETE operations
###### Follow the HTTP specification when sending a response
###### Support content negotiation
###### Provide links to support HATEOAS-style navigation and discovery of resources
##### Handling exceptions
###### Capture exceptions and return a meaningful response to clients
###### Handle exceptions consistently and log information about errors
###### Distinguish between client-side errors and server-side errors
##### Optimizing client-side data access
###### Support client-side caching
###### provide ETags to optimize query processing
###### Use ETags to Support Optimistic Concurrency
##### Handling large requests and responses
###### Optimize requests and responses that involve large objects
###### Implement partial responses for clients that don't support asynchronous operations
###### Avoid sending unnecessary 100-Continue status messages in client applications
###### Support pagination for requests that may return large numbers of objects
##### Maintaining responsiveness, scalability, and availability
###### Provide asynchronous support for long-running requests
###### Ensure that each request is stateless
###### Track clients and implement throttling to reduce the chances of DOS attacks
###### Manage persistent HTTP connections carefully
##### Publishing and managing a web API
###### Testing a web API
###### Using Azure API Management
##### Supporting client-side developers
###### Document the REST operations for a web API
###### Implement a client SDK
##### Monitoring a web API
###### Monitoring a web API directly
###### Monitoring a web API through the API Management Service






### references
#### links
- <https://learn.microsoft.com/en-us/azure/architecture/best-practices/api-design>
