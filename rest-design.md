# REST services APIs design
## Some tips on how to design good REST APIs that are: easy to use, stable to avoid clients inconsistency and has organized URIs under a logical pattern. 

#### - Use the http methods from the specification to provide operations over your data:
- POST -> To save a new resource
- GET -> To retrieve resources
- PUT -> Update an already saved resource
- DELETE -> Remove an already saved resource
- PATCH -> Perform a partial update of a resource

#### - Handle errors using http codes. Also, consider sending a body response with a more readable error (which parameter was wrong or missing, etc).

- 400 -> Bad request, wrong input for the requested resource.
- 404 -> Resource not found, the user sent an ID that does not have any resource associated with.

This is important because if we follow the http method specification will much easier for the user to comprehend how the API works.
Besides that, in a single endpoint we can provide several operations over the same data which simplify configurations and the logic on the client side.

#### - Build the URIs over the target resource (mainly will be the domain object which you will provide your operations):
For example consider that we are modeling REST services for a university:
- Students
- Courses
- Departments

#### - Use path params and use the resource name in plural form as convention:
For example, let us say that we have a CRL as the resource, this CRL(String id, File file) have a reference to an AuthorityKey(String authKey):

- GET on /crls -> Obtain all CRLs
- GET on /crls/{id} -> Obtain the CRL with {id}
- POST on /crls -> Save a new CRL
- PUT on /crls/{id} -> Update CRL with {id}
- DELETE on /crls/{id} -> Remove the CRL with {id}

#### - To obtain specific resources that are related to other resource use the path to inform the related resource:

- GET on /crls/{id}/authorities -> Return all authorities related to the specified CRL
- GET on /crls/{id}/file -> Return the file for CRL with {id} 
- GET on /authorities/{id}/crls -> Return all CRLs for the authority with {id}
- POST on /crls/{id}/file -> Save the file for CRL with {id}

#### - Allow fields filtering to avoid unecessary data transfer. The client might need only a few fields from the resource and that can be specified as a query parameter:

- GET on /crls?fields=id,creation_date -> Return the CRLs but only the ID and Creation Date for each register

#### - Filtering resources can be done with query parameters:
*Use + and - to inform ascend or descend ordering

- GET on /crls?sort_by={attribute}&order=-updated_on -> Retrieves all CRLs order by {attribute} in descendant order that they were updated
- GET on /authorities?sort_by{crl_size}&gt=2 -> Retrieves the Authorities that has more than 5 CRLs

#### - Work with pagination on query parameter specifying page number and filtering the results size:
*You can send the total registers to the user as a HEADER parameter: X-Total-Count or as additional field in the response.

- GET on /crls?page=1&size=10 -> Get 10 results in page 1


