# Vendor API
This document describes the usage of the anybill vendor REST API.

## Environments
There are currently two public environments:

### Production: `https://vendor-api.anybill.de`
This environment is for production use.

### Staging: `https://vendor-api-stg.anybill.de`
This environment is for integration testing.

## Bill API
<p>
  With this Endpoint you can add a Bill to the anybill API.
  For this, the respective store from which the receipt is to be issued must already have been added via the Store API.
</p>
<p>
Values for quantityType and tenderTypeId can be the integer value or the string equivalent.

### Possible quantityType values
- Count | 0
- Kilogram | 1
- Lbs | 2
- Meters | 3
- Inches | 4
- Liter | 5
- CubicMeters | 6

> Example:<br>
> qantityType: "Count"

> Example 2:<br>
> quantityType: 3


### Possible tenderTypeId values:
- CASH | 0
- VISA | 1
- MASTERCARD | 2
- AMERICAN_EXPRESS | 3
- DISCOVER | 4
- JCB | 5
- DEBITCARD | 6
- PAYPAL | 7
- APPLE_PAY | 8
- GOOGLE_PAY | 9
- AMAZON_PAY | 10

> Example:<br>
> tenderTypeId: "PAYPAL"

> Example 2:<br>
> tenderTypeId: 8

### Possible currencyCode values:
[Currency codes (ISO 4217)](https://www2.1010data.com/documentationcenter/prime/1010dataUsersGuide/DataTypesAndFormats/currencyUnitCodes.html)

> Example:<br>
> currencyCode: "EUR"

</p>
<p>
  Please check out the OpenAPI specifications for more information.
</p>

## Store API
<p>
  With these Endpoints the Stores of an Vendor can be managed.
  This can also be done on the anybill Partner Portal.
</p>
<p>
  Please check out the OpenAPI specifications for more information.
</p>

## Category API
<p>
  This endpoint lists all categories which are available to categorize the line items and the bill.
</p>
<p>
  Please check out the OpenAPI specifications for more information.
</p>

## OpenAPI Specification
<p>
  Here you can find the complete OpenAPI Specifications for the Vendor API.
</p>
<p>
  Click on your preferred OpenAPI tool to view the specifications:
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

### 2020-02-04
Bill endpoint:
- Quantity can now be of type double
- QuantityType added

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
