# Vendor API V1
This document describes the usage of the anybill vendor REST API.

## Environments
There are currently two public environments:

### Production: `https://vendor-api.anybill.de`
This environment is for production use.<br>
<b>OpenAPI Specifications:</b><br>
[SwaggerUI](https://vendor-api.anybill.de/index.html)


### Staging: `https://vendor-api-stg.anybill.de`
This environment is for integration testing.<br>
<b>OpenAPI Specifications:</b><br>
[SwaggerUI](https://vendor-api.anybill.de/index.html)


# Bill API
<p>
  With this endpoint you can add a bill to the anybill API.
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
- SquareMeters | 7

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

### Display a discount:
A Discount can be set to each LineItem Individually with the Properties originalPrice, pricePaid and priceModifier.<br>
By providing these Parameters the applied Discount gets calculated automatically.

Possible Values for priceModifier:
<table>
  <tr>
    <th>Name</th>
    <th>Value</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>None (default)</td>  
    <td>0</td>
    <td>
      No Discount gets applied
    </td>
  </tr>
  <tr>
    <td>Percentage</td>  
    <td>1</td>
    <td>
      A Discount of a specific percentage gets applied
    </td>
  </tr>
  <tr>
    <td>Monetary</td>  
    <td>2</td>
    <td>
      The Line Item price is reduced by a certain Amount e.g. -2€
    </td>
  </tr>
  <tr>
    <td>Monetary Replacement</td>  
    <td>3</td>
    <td>
      The Line Item price is reduced to a certain Price e.g. costs 3€ instead of 4€
    </td>
  </tr>
</table>

> Example:<br>
> originalPrice: 100.0<br>
> pricePaid: 80.0<br>
> priceModifier: 1<br>
>
> => a discount of 20% is applied to this line item


> Example 2:<br>
> originalPrice: 2.99<br>
> pricePaid: 2.39<br>
> priceModifier: 2<br>
>
> => a discount of 0.30 is applied to this line item

> Example 3:<br>
> originalPrice: 14.99<br>
> pricePaid: 9.99<br>
> priceModifier: 3<br>
>
> => the price of this line item is reduced from 14.99 to 9.99
</p>

### OpenAPI Specifications:

<b>Production API:</b><br>
[SwaggerUI](https://vendor-api.anybill.de/index.html)

<b>Staging API:</b><br>
[SwaggerUI](https://vendor-api-stg.anybill.de/index.html)


## Store API
<p>
  With these Endpoints the stores of an Vendor can be managed.
  This can also be done on the anybill Partner Portal.
</p>

### OpenAPI Specifications:

<b>Production API:</b><br>
[SwaggerUI](https://vendor-api.anybill.de/index.html)

<b>Staging API:</b><br>
[SwaggerUI](https://vendor-api-stg.anybill.de/index.html)


## Category API
<p>
  This endpoint lists all categories which are available to categorize the line items and the bill.
</p>

### OpenAPI Specifications:

<b>Production API:</b><br>
[SwaggerUI](https://vendor-api.anybill.de/index.html)

<b>Staging API:</b><br>
[SwaggerUI](https://vendor-api-stg.anybill.de/index.html)


# Postman
A Postman collection can be found [here](./Postman/Anybill%20Vendor%20Api.postman_collection.json).
There are also Environments for [Staging](./Postman/Environments/Anybill%20VendorApi%20Staging.postman_environment.json) and [Production](./Postman/Environments/Anybill%20VendorApi%20Production.postman_environment.json)

To acquire an access_token first set your credentials for the following collection variables:
- username
- password
- client_id

After your credentials are set, send a request with the `GetToken` request. The acquired access token will automatically be set for all requests in the collection. Choose the environment and you are good to go. 

# Changelog
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
