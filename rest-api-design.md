# REST API Design

<!-- toc -->

- [URI Format](#URI-Format)
  * [A TRAILING FORWARD SLASH (/) SHOULD NOT BE INCLUDED IN URIS](#A-TRAILING-FORWARD-SLASH-SHOULD-NOT-BE-INCLUDED-IN-URIS)
  * [HYPHENS (-) SHOULD BE USED TO IMPROVE THE READABILITY OF URIS](#HYPHENS---SHOULD-BE-USED-TO-IMPROVE-THE-READABILITY-OF-URIS)
  * [UNDERSCORES (_) SHOULD NOT BE USED IN URIS](#UNDERSCORES-_-SHOULD-NOT-BE-USED-IN-URIS)
  * [LOWERCASE LETTERS SHOULD BE PREFERRED IN URI PATHS](#LOWERCASE-LETTERS-SHOULD-BE-PREFERRED-IN-URI-PATHS)
  * [FILE EXTENSIONS SHOULD NOT BE INCLUDED IN URIS](#FILE-EXTENSIONS-SHOULD-NOT-BE-INCLUDED-IN-URIS)
- [Resource Archetypes](#Resource-Archetypes)
  * [DOCUMENT](#DOCUMENT)
  * [COLLECTION](#COLLECTION)
  * [STORE](#STORE)
  * [CONTROLLER](#CONTROLLER)
- [URI Path Design](#URI-Path-Design)
  * [A SINGULAR NOUN SHOULD BE USED FOR DOCUMENT NAMES](#A-SINGULAR-NOUN-SHOULD-BE-USED-FOR-DOCUMENT-NAMES)
  * [A PLURAL NOUN SHOULD BE USED FOR COLLECTION NAMES](#A-PLURAL-NOUN-SHOULD-BE-USED-FOR-COLLECTION-NAMES)
  * [A PLURAL NOUN SHOULD BE USED FOR STORE NAMES](#A-PLURAL-NOUN-SHOULD-BE-USED-FOR-STORE-NAMES)
  * [A VERB OR VERB PHRASE SHOULD BE USED FOR CONTROLLER NAMES](#A-VERB-OR-VERB-PHRASE-SHOULD-BE-USED-FOR-CONTROLLER-NAMES)
  * [VARIABLE PATH SEGMENTS MAY BE SUBSTITUTED WITH IDENTITY-BASED VALUES](#VARIABLE-PATH-SEGMENTS-MAY-BE-SUBSTITUTED-WITH-IDENTITY-BASED-VALUES)
  * [CRUD FUNCTION NAMES SHOULD NOT BE USED IN URIS](#CRUD-FUNCTION-NAMES-SHOULD-NOT-BE-USED-IN-URIS)
- [URI Query Design](#URI-Query-Design)
  * [THE QUERY COMPONENT OF A URI MAY BE USED TO FILTER COLLECTIONS OR STORES](#THE-QUERY-COMPONENT-OF-A-URI-MAY-BE-USED-TO-FILTER-COLLECTIONS-OR-STORES)
  * [THE QUERY COMPONENT OF A URI SHOULD BE USED TO PAGINATE COLLECTION OR STORE RESULTS](#THE-QUERY-COMPONENT-OF-A-URI-SHOULD-BE-USED-TO-PAGINATE-COLLECTION-OR-STORE-RESULTS)
- [Request Methods](#Request-Methods)

<!-- tocstop -->

### URI Format

#### A TRAILING FORWARD SLASH (/) SHOULD NOT BE INCLUDED IN URIS
As the last character within a URI’s path, a forward slash (/) adds no semantic value and may cause confusion. REST APIs should not expect a trailing slash and should not include them in the links that they provide to clients.
> INCORRECT http://api.canvas.restapi.org/shapes/
> CORRECT   http://api.canvas.restapi.org/shapes

#### HYPHENS (-) SHOULD BE USED TO IMPROVE THE READABILITY OF URIS
To make your URIs easy for people to scan and interpret, use the hyphen (-) character to improve the readability of names in long path segments. Anywhere you would use a space or hyphen in English, you should use a hyphen in a URI. For example:
>http://api.example.restapi.org/blogs/mark-masse/entries/this-is-my-first-post


#### UNDERSCORES (_) SHOULD NOT BE USED IN URIS
Text viewer applications (browsers, editors, etc.) often underline URIs to provide a visual cue that they are clickable. Depending on the application’s font, the underscore (_) character can either get partially obscured or completely hidden by this underlining. To avoid this confusion, use hyphens (-) instead of underscores

#### LOWERCASE LETTERS SHOULD BE PREFERRED IN URI PATHS
When convenient, lowercase letters are preferred in URI paths since capital letters can sometimes cause problems. 
> CORECT http://api.example.restapi.org/my-folder/my-doc
> INCORRECT http://api.example.restapi.org/My-Folder/my-doc
> This URI is not the same as first URI, which may cause unnecessary confusion.

#### FILE EXTENSIONS SHOULD NOT BE INCLUDED IN URIS
A REST API should not include artificial file extensions in URIs to indicate the format of a message’s entity body. Instead, they should rely on the media type, as communicated through the Content-Type header, to determine how to process the body’s content. 
> http://api.college.restapi.org/students/3248234/transcripts/2005/fall.json
> http://api.college.restapi.org/students/3248234/transcripts/2005/fall

### Resource Archetypes
A REST API is composed of four distinct resource archetypes: document, collection, store, and controller.

#### DOCUMENT
A document resource is a singular concept that is akin to an object instance or database record. A document’s state representation typically includes both fields with values and links to other related resources. 
A document may have child resources that represent its specific subordinate concepts.

Each URI below identifies a document resource:
> http://api.soccer.restapi.org/leagues/seattle
> http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet
> http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players/mike

#### COLLECTION
A collection resource is a server-managed directory of resources. Clients may propose new resources to be added to a collection. However, it is up to the collection to choose to create a new resource, or not. A collection resource chooses what it wants to contain and also decides the URIs of each contained resource.

Each URI below identifies a collection resource:
> http://api.soccer.restapi.org/leagues
> http://api.soccer.restapi.org/leagues/seattle/teams
> http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players

#### STORE
A store is a client-managed resource repository. A store resource lets an API client put resources in, get them back out, and decide when to delete them. On their own, stores do not create new resources; therefore a store never generates new URIs. Instead, each stored resource has a URI that was chosen by a client when it was initially put into the store.

The example interaction below shows a user (with ID 1234) of a client program using a fictional Soccer REST API to insert a document resource named alonso in his or her store of favorites:

> PUT /users/1234/favorites/alonso

#### CONTROLLER
A controller resource models a procedural concept. Controller resources are like executable functions, with parameters and return values; inputs and outputs.
REST API relies on controller resources to perform application-specific actions that cannot be logically mapped to one of the standard methods (create, retrieve, update, and delete, also known as CRUD).
Controller names typically appear as the last segment in a URI path, with no child resources to follow them in the hierarchy. The example below shows a controller resource that allows a client to resend an alert to a user:

> POST /alerts/245743/resend
 
### URI Path Design
Each URI path segment, separated by forward slashes (/), represents a design opportunity. Assigning meaningful values to each path segment helps to clearly communicate the hierarchical structure of a REST API’s resource model design

![f3d06e1b.png](:storage/28285b1e-9a50-4dd5-b2c3-461382652585/f3d06e1b.png)

This section provides rules relating to the design of meaningful URI paths.

#### A SINGULAR NOUN SHOULD BE USED FOR DOCUMENT NAMES
A URI representing a document resource should be named with a singular noun or noun phrase path segment.

For example, the URI for a single player document would have the singular form:
> http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players/claudio

#### A PLURAL NOUN SHOULD BE USED FOR COLLECTION NAMES
A URI identifying a collection should be named with a plural noun, or noun phrase, path segment. A collection’s name should be chosen to reflect what it uniformly contains.

For example, the URI for a collection of player documents uses the plural noun form of its contained resources:

> http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players

#### A PLURAL NOUN SHOULD BE USED FOR STORE NAMES
A URI identifying a store of resources should be named with a plural noun, or noun phrase, as its path segment. The URI for a store of music playlists may use the plural noun form as follows:

> http://api.music.restapi.org/artists/mikemassedotcom/playlists

#### A VERB OR VERB PHRASE SHOULD BE USED FOR CONTROLLER NAMES
Like a computer program’s function, a URI identifying a controller resource should be named to indicate its action. For example:

> http://api.college.restapi.org/students/morgan/register
> http://api.example.restapi.org/lists/4324/dedupe
> http://api.ognom.restapi.org/dbs/reindex
> http://api.build.restapi.org/qa/nightly/runTestSuite

#### VARIABLE PATH SEGMENTS MAY BE SUBSTITUTED WITH IDENTITY-BASED VALUES
A URI template includes variables that must be substituted before resolution. The URI template example below has three variables (leagueId, teamId, and playerId):

http://api.soccer.restapi.org/leagues/{leagueId}/teams/{teamId}/players/{playerId}

#### CRUD FUNCTION NAMES SHOULD NOT BE USED IN URIS
URIs should not be used to indicate that a CRUD function is performed. URIs should be used to uniquely identify resources, and they should be named as described in the rules above.

> CORRECT DELETE /users/1234
> INCORRECT GET /deleteUser?id=1234
> INCORRECT GET /deleteUser/1234
> INCORRECT DELETE /deleteUser/1234
> INCORRECT POST /users/1234/delete

### URI Query Design

#### THE QUERY COMPONENT OF A URI MAY BE USED TO FILTER COLLECTIONS OR STORES
A URI’s query component is a natural fit for supplying search criteria to a collection or store. Let’s take a look at an example:

> 1. GET /users
> 2. GET /users?role=admin
1. The response message’s state representation contains a listing of all the users in the collection.
2. The response message’s state representation contains a filtered list of all the users in the collection with a “role” value of admin.

#### THE QUERY COMPONENT OF A URI SHOULD BE USED TO PAGINATE COLLECTION OR STORE RESULTS
This section provides rules relating to the design of URI queries. 

A REST API client should use the query component to paginate collection and store results with the pageSize and pageStartIndex parameters. The pageSize parameter specifies the maximum number of contained elements to return in the response. The pageStartIndex parameter specifies the zero-based index of the first element to return in the response. For example:

> GET /users?pageSize=25&pageStartIndex=50

When the complexity of a client’s pagination (or filtering) requirements exceeds the simple formatting capabilities of the query part, consider designing a special controller resource that partners with a collection or store. For example, the following controller may accept more complex inputs via a request’s entity body instead of the URI’s query part:

> POST /users/search

This design allows for custom range types and special sort orders to be easily specified in the client request message body. 

### Request Methods

#### RULE: GET AND POST MUST NOT BE USED TO TUNNEL OTHER REQUEST METHODS
Tunneling refers to any abuse of HTTP that masks or misrepresents a message’s intent and undermines the protocol’s transparency. A REST API must not compromise its design by misusing HTTP’s request methods in an effort to accommodate clients with limited HTTP vocabulary. Always make proper use of the HTTP methods as specified by the rules in this section.

#### RULE: GET MUST BE USED TO RETRIEVE A REPRESENTATION OF A RESOURCE
A REST API client uses the GET method in a request message to retrieve the state of a resource, in some representational form. **A client’s GET request message may contain headers but no body**.

The architecture of the Web relies heavily on the nature of the GET method. Clients count on being **able to repeat GET requests without causing side effects**. Caches depend on the ability to serve cached representations without contacting the origin server.

#### RULE: PUT MUST BE USED TO BOTH INSERT AND UPDATE A STORED RESOURCE
PUT must be used to add a new resource to a store, with a URI specified by the client. PUT must also be used to update or replace an already stored resource.

The example below demonstrates how a service-oriented REST API can provide a store resource that allows its client application’s to persist their data as objects:

> PUT /accounts/4ef2d5d0-cb7e-11e0-9572-0800200c9a66/buckets/objects/4321

The PUT request message must include a representation of a resource that the client wants to store. However, the body of the request may or may not be exactly the same as a client would receive from a subsequent GET request. For example, a REST API’s store resource may allow clients to include only the mutable portions of the resource state in the request message’s representation.

#### RULE: PUT MUST BE USED TO UPDATE MUTABLE RESOURCES
Clients must use the PUT request method to make changes to resources. The PUT request message may include a body that reflects the desired changes.

#### RULE: POST MUST BE USED TO CREATE A NEW RESOURCE IN A COLLECTION
Clients use POST when attempting to create a new resource within a collection. The POST request’s body contains the suggested state representation of the new resource to be added to the server-owned collection.

The example below demonstrates how a client uses POST to request a new addition to a collection:

> POST /leagues/seattle/teams/trebuchet/players
> Note the request message may contain a representation that suggests the initial state of the player to be created.

#### RULE: POST MUST BE USED TO EXECUTE CONTROLLERS
Clients use the POST method to invoke the function-oriented controller resources. A POST request message may include both headers and a body as inputs to a controller resource’s function.

HTTP calls the POST request method *unsafe* and *non-idempotent*, which means that its outcome is unpredictable and not guaranteed to be repeatable without potentially undesirable side effects. For example, a resubmitted web form that uses POST might run the risk of double billing a user’s credit card. Controller resources trade a degree of transparency and robustness for the sake of flexibility.

The example below demonstrates how a controller can be executed using the POST request method:

> POST /alerts/245743/resend

#### RULE: DELETE MUST BE USED TO REMOVE A RESOURCE FROM ITS PARENT
A client uses DELETE to request that a resource be completely removed from its parent, which is often a collection or store. Once a DELETE request has been processed for a given resource, the resource can no longer be found by clients. Therefore, any future attempt to retrieve the resource’s state representation, using either GET or HEAD, must result in a 404 (“Not Found”) status returned by the API.

The example below shows how a client might remove a document from a store:

> DELETE /accounts/4ef2d5d0-cb7e-11e0-9572-0800200c9a66/buckets/objects/4321

#### RULE: OPTIONS SHOULD BE USED TO RETRIEVE METADATA THAT DESCRIBES A RESOURCE’S AVAILABLE INTERACTIONS
Clients may use the OPTIONS request method to retrieve resource metadata that includes an Allow header value. For example:

> Allow: GET, PUT, DELETE

In response to an OPTIONS request, a REST API may include a body that includes further details about each interaction option.

### Response Status Codes

#### RULE: 200 (“OK”) SHOULD BE USED TO INDICATE NONSPECIFIC SUCCESS

#### RULE: 200 (“OK”) MUST NOT BE USED TO COMMUNICATE ERRORS IN THE RESPONSE BODY

#### RULE: 201 (“CREATED”) MUST BE USED TO INDICATE SUCCESSFUL RESOURCE CREATION

#### RULE: 202 (“ACCEPTED”) MUST BE USED TO INDICATE SUCCESSFUL START OF AN ASYNCHRONOUS ACTION

#### RULE: 204 (“NO CONTENT”) SHOULD BE USED WHEN THE RESPONSE BODY IS INTENTIONALLY EMPTY

#### RULE: 301 (“MOVED PERMANENTLY”) SHOULD BE USED TO RELOCATE RESOURCES

#### RULE: 302 (“FOUND”) SHOULD NOT BE USED
The intent of 302 is that this automatic redirect behavior only applies if the client’s original request used either the GET or HEAD method.

#### RULE: 303 (“SEE OTHER”) SHOULD BE USED TO REFER THE CLIENT TO A DIFFERENT URI
A 303 response indicates that a controller resource has finished its work, but instead of sending a potentially unwanted response body, it sends the client the URI of a response resource. 

#### RULE: 304 (“NOT MODIFIED”) SHOULD BE USED TO PRESERVE BANDWIDTH
This status code is similar to 204 (“No Content”) in that the response body must be empty. The key distinction is that 204 is used when there is nothing to send in the body, whereas 304 is used when there is state information associated with a resource but the client already has the most recent version of the representation.

#### RULE: 307 (“TEMPORARY REDIRECT”) SHOULD BE USED TO TELL CLIENTS TO RESUBMIT THE REQUEST TO ANOTHER URI

#### RULE: 400 (“BAD REQUEST”) MAY BE USED TO INDICATE NONSPECIFIC FAILURE
400 is the generic client-side error status, used when no other 4xx error code is appropriate.

#### RULE: 401 (“UNAUTHORIZED”) MUST BE USED WHEN THERE IS A PROBLEM WITH THE CLIENT’S CREDENTIALS
A 401 error response indicates that the client tried to operate on a protected resource without providing the proper authorization. It may have provided the wrong credentials or none at all.

#### RULE: 403 (“FORBIDDEN”) SHOULD BE USED TO FORBID ACCESS REGARDLESS OF AUTHORIZATION STATE
A 403 error response indicates that the client’s request is formed correctly, but the REST API refuses to honor it. A 403 response is not a case of insufficient client credentials; that would be 401 (“Unauthorized”).

REST APIs use 403 to enforce application-level permissions. For example, a client may be authorized to interact with some, but not all of a REST API’s resources. If the client attempts a resource interaction that is outside of its permitted scope, the REST API should respond with 403.

#### RULE: 404 (“NOT FOUND”) MUST BE USED WHEN A CLIENT’S URI CANNOT BE MAPPED TO A RESOURCE
The 404 error status code indicates that the REST API can’t map the client’s URI to a resource.

#### RULE: 405 (“METHOD NOT ALLOWED”) MUST BE USED WHEN THE HTTP METHOD IS NOT SUPPORTED
The API responds with a 405 error to indicate that the client tried to use an HTTP method that the resource does not allow. For instance, a read-only resource could support only GET and HEAD, while a controller resource might allow GET and POST, but not PUT or DELETE.

A 405 response must include the Allow header, which lists the HTTP methods that the resource supports. For example:

> Allow: GET, POST

#### RULE: 406 (“NOT ACCEPTABLE”) MUST BE USED WHEN THE REQUESTED MEDIA TYPE CANNOT BE SERVED
The 406 error response indicates that the API is not able to generate any of the client’s preferred media types, as indicated by the Accept request header. For example, a client request for data formatted as application/xml will receive a 406 response if the API is only willing to format data as application/json.

#### RULE: 409 (“CONFLICT”) SHOULD BE USED TO INDICATE A VIOLATION OF RESOURCE STATE
The 409 error response tells the client that they tried to put the REST API’s resources into an impossible or inconsistent state. For example, a REST API may return this response code when a client tries to delete a non-empty store resource.

#### RULE: 412 (“PRECONDITION FAILED”) SHOULD BE USED TO SUPPORT CONDITIONAL OPERATIONS
The 412 error response indicates that the client specified one or more preconditions in its request headers, effectively telling the REST API to carry out its request only if certain conditions were met. A 412 response indicates that those conditions were not met, so instead of carrying out the request, the API sends this status code.

#### RULE: 415 (“UNSUPPORTED MEDIA TYPE”) MUST BE USED WHEN THE MEDIA TYPE OF A REQUEST’S PAYLOAD CANNOT BE PROCESSED
The 415 error response indicates that the API is not able to process the client’s supplied media type, as indicated by the Content-Type request header. For example, a client request including data formatted as application/xml will receive a 415 response if the API is only willing to process data formatted as application/json.

#### RULE: 500 (“INTERNAL SERVER ERROR”) SHOULD BE USED TO INDICATE API MALFUNCTION
500 is the generic REST API error response. Most web frameworks automatically respond with this response status code whenever they execute some request handler code that raises an exception.

A 500 error is never the client’s fault and therefore it is reasonable for the client to retry the exact same request that triggered this response, and hope to get a different response.

### HTTP Headers

#### RULE: CONTENT-TYPE MUST BE USED
The Content-Type header names the type of data found within a request or response message’s body. The value of this header is a specially formatted text string known as a media type, which is the subject of Media Types. Clients and servers rely on this header’s value to tell them how to process the sequence of bytes in a message’s body.

#### RULE: CONTENT-LENGTH SHOULD BE USED
The Content-Length header gives the size of the entity-body in bytes. In responses, this header is important for two reasons. First, a client can know whether it has read the correct number of bytes from the connection. Second, a client can make a HEAD request to find out how large the entity-body is, without downloading it.

#### RULE: LAST-MODIFIED SHOULD BE USED IN RESPONSES
The Last-Modified header applies to response messages only. The value of this response header is a timestamp that indicates the last time that something happened to alter the representational state of the resource. Clients and cache intermediaries may rely on this header to determine the freshness of their local copies of a resource’s state representation. This header should always be supplied in response to GET requests.

#### RULE: ETAG SHOULD BE USED IN RESPONSES
The value of ETag is an opaque string that identifies a specific “version” of the representational state contained in the response’s entity. The entity is the HTTP message’s payload, which is composed of a message’s headers and body. The entity tag may be any string value, so long as it changes along with the resource’s representation. This header should always be sent in response to GET requests.

Clients may choose to save an ETag header’s value for use in future GET requests, as the value of the conditional If-None-Match request header. If the REST API concludes that the entity tag hasn’t changed, then it can save time and bandwidth by not sending the representation again.

#### RULE: STORES MUST SUPPORT CONDITIONAL PUT REQUESTS
[HTTP conditional requests](https://developer.mozilla.org/en-US/docs/Web/HTTP/Conditional_requests#Conditional_headers)

#### RULE: LOCATION MUST BE USED TO SPECIFY THE URI OF A NEWLY CREATED RESOURCE
The Location response header’s value is a URI that identifies a resource that may be of interest to the client. In response to the successful creation of a resource within a collection or store, a REST API must include the Location header to designate the URI of the newly created resource.

In a 202 (“Accepted”) response, this header may be used to direct clients to the operational status of an asynchronous controller resource.

