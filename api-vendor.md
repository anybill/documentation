# Vendor API
This document describes the usage of the anybill vendor REST API.

## Environments
There are currently two public environments:

### Production: `vendor.anybill.de`
This environment is for production use.

### Staging: `vendor-stg.anybill.de`
This environment is for integration testing.

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