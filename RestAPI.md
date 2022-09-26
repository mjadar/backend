# REST API

## What is API

- stands for Application Programming Interface
- a way for two computers to talk with each other

## Rest API

- is the common api standard used to talk to servers
- [REST] = Representational state transfer
- set of rules for building web apis:

  - uniform interface
  - client-server
  - stateless
  - cacheable
  - layered system
  - code on demand

- organise resources into unique URIS
- grouped by noun and not verbs
- retrieve all poducts : `/api/v1/products` and not `/api/v1/getAllProducts`

## HTTP requests

- POST = create a resource
- GET = read
- PUT = update
- DELETE

## Implementation

- the rest implementation should be stateless;
  - which means the two parties communicating should not store info about each other.
  - So the requests are independent from all others.
  - which makes an application easy to scale and well behaved.
- use pagination if a huge amount of data is returned
  - `/products?limit=25&offset=50`
- always take into account versioning of the REST API
