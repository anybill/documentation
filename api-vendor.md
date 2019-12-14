# Vendor API
This document describes the usage of the anybill vendor REST API.

## Environments
There are currently two public environments:

### Production: `https://vendor-api.anybill.de`
This environment is for production use.

### Staging: `https://vendor-api-stg.anybill.de`
This environment is for integration testing.

## OpenAPI Specification
The current OpenAPI specification can be found [here](./specification.json).

To visualize this file either use your tool of choice or try:
- [SwaggerUI](https://editor.swagger.io/?url=https://raw.githubusercontent.com/anybill/documentation/master/specification.json) or
- [ReDoc](https://redocly.github.io/redoc/?url=https://raw.githubusercontent.com/anybill/documentation/master/specification.json)

The always up-to-date Swagger documentation of the specific environment can also be found by navigating to the environments root url.

## Postman
A Postman collection can be found [here](./Postman/Anybill%20Vendor%20Api.postman_collection.json).
There are also Environments for [Staging](./Postman/Environments/Anybill%20VendorApi%20Staging.postman_environment.json) and [Production](./Postman/Environments/Anybill%20VendorApi%20Production.postman_environment.json)

To acquire an access_token first set your credentials for the following collection variables:
- username
- password
- client_id

After your credentials are set, send a request with the `GetToken` request. The acquired access token will automatically be set for all requests in the collection. Choose the environment and you are good to go. 

## Changelog
Changes to the anybill API will be documented here.

### 2019-12-14
Initial documented pre release.

Bill endpoint:
- AddBill

Category endpoint:
- GetCategories
- GetCategory

Stores:
- GetStores
- GetStore
- GetStoreHistory
- DeleteStore
- UpsertStore