# Vendor API
This document describes the usage of the anybill vendor REST API.

## Environments
There are currently two public environments:

### Production: `https://vendor.anybill.de`
This environment is for production use.

### Staging: `https://vendor-api-stg.anybill.de`
This environment is for integration testing.

## Bill API
<p>
  To add a Bill to a anybill User <b>only</b> the post bill endpoint has to be implemented.
</p>
<p>
  For more information have a look at the OpenAPI Specifications.
</p>

## Store API
<p>
  With these Endpoints the Stores of an Vendor can be managed.
  This can also be done on the anybill Partner Portal so implementing these Endpoints is not required.
</p>
<p>
  For more information have a look at the OpenAPI Specifications.
</p>

## Category API
<p>
  This Endpoint lists all Categories which are available to categorize the LineItems and the Bill.
</p>
<p>
  For more information have a look at the OpenAPI Specifications.
</p>

## OpenAPI Specification
<p>
  Here you can find the complete OpenAPI Specifications for the Vendor API.
</p>
<p>
  Click on your Preferred OpenAPI tool to view the Specifications:
</p>

- #### [SwaggerUI](https://vendor-api-stg.anybill.de/index.html)
- #### [ReDoc](https://redocly.github.io/redoc/?url=https://vendor-api-stg.anybill.de/swagger/v1/swagger.json)
- #### [Raw OpenAPI Json File](https://vendor-api-stg.anybill.de/swagger/v1/swagger.json)

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
