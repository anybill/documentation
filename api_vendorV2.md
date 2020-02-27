# Vendor API V2 Preview
This document describes the usage of the anybill vendor REST API V2.

## Environments
There version 2 is currently in preview and is not yet deployed to our public environments. An open api specification can already be found [here](./specification_V2_Preview.json). There are currently two public environments:

### Production: `https://vendor-api.anybill.de`
This environment is for production use.  
[SwaggerUI](https://vendor-api.anybill.de/index.html)  
[OpenApi-Specification](https://vendor-api.anybill.de/swagger/v1/swagger.json)

### Staging: `https://vendor-api-stg.anybill.de`
This environment is for integration testing.  
[SwaggerUI](https://vendor-api-stg.anybill.de/index.html)  
[OpenApi-Specification](https://vendor-api-stg.anybill.de/swagger/v1/swagger.json)

# Bill
The bill controller offers two routes which can be used to add bills into the anybill system:
- POST `bill/user/{userId}`
- POST `bill`

The `bill/user/{userId}`-route can be used to add a bill for a registered user. This is the case if the QR-Code provided by the app gets scanned at POS. For a better description of the structure of the QR-Code have a look [here](./app_qr.md).

The `bill`-Route can be used to add an anonymous bill. This is the case if the customer does not scan his QR-Code at the POS. This route enables the vendor to issue a digital receipt to the customer. A JSON-Object which contains a url retrieve the receipt will be returned.
> Example:
>
>{ "url": "https://path-to-receipt.anybill.de/{receiptId}" }

As seen in the open api specification, the respective store from which the receipt is to be issued must have already been added via the Store API or the anybill Partner Portal.

## Description of possible values
For better understanding some values are descibed below.

Values for enumerations like QuantityType, PriceModifier or TenderType can be the integer value or the string equivalent, whereas integers are prefered. The descriptions always show the integer value and the string equivalent/meaning of the value.

### Possible QuantityType values:
The quantity type describes the type of quantity of the line item. For bananas, whose price is often measured by weight, you would choose 1 (kilogram) and for t-shirts that are sold per unit you would choose 0 (count).

- 0 - Count 
- 1 - Kilogram
- 2 - Lbs
- 3 - Meters
- 4 - Inches
- 5 - Liter
- 6 - CubicMeters
- 7 - SquareMeters

> **Example 1:**
>
> qantityType: "Count"

> **Example 2:**
>
> quantityType: 3

### Possible TenderType values:
The tender type describes the legal tender used in the tender object. The type used should be specified more with the detailedType-property. E.g. for a payment with visa the tender type should be 3 (credit card) and detailed type should be "Visa". The detailed type should be human readable and will be displayed for the user.

- 0 - Miscellaneous
- 1 - Cash
- 2 - DirectDebit
- 3 - CreditCard
- 4 - OnlinePayment
- 5 - GiftCard
- 6 - BankTransfer
- 7 - Check
- 8 - LoyaltyCard 

> **Example 1:**
>
> tenderType: "Cash"

> **Example 2:**
>
> tenderTypeId: 8

For every tender type, except for miscellaneous, additional details can be provided in the paymentDetails-property. For the cash tender type the CashPaymentDetails-object can be optionally used. Any details given, that do not match the correct tender type will be ignored.

### Possible CurrencyCode values:
To specify the currency, the 3-digit [ISO 4217](https://www2.1010data.com/documentationcenter/prime/1010dataUsersGuide/DataTypesAndFormats/currencyUnitCodes.html) standard is used. Any currency codes that do not match the standard will result in a invalid response.

> **Example:**
>
> currencyCode: "EUR"

### Display a discount:
A discount can be set to each line item individually. The optional properties discountValue, priceModifier and unitOriginalGrossPrice can be used to describe the discount.

Possible Values for priceModifier:

| Name                | Value | Description                                                                                                              |
|---------------------|:-----:|--------------------------------------------------------------------------------------------------------------------------|
| None (default)      |   0   | No discount gets applied.                                                                                                |
| Percentage          |   1   | A discount of a specific percentage gets applied. E.g. 20 %                                                              |
| Monetary            |   2   | The line item gross unit price is reduced by a certain amount. E.g. reduced by 2 € based on the original price per unit. |
| MonetaryReplacement |   3   | The line item price is reduced to a certain price. E.g. original price: 4 € price now: 3 €                               |

> **Example 1:**
>
> unitOriginalGrossPrice: 100.0<br>
> unitGrossPrice: 80.0<br>
> priceModifier: 1<br>
> discountValue: 20<br>
>
> => A 20 % discount was applied to this line item.

> **Example 2:**
>
> unitOriginalGrossPrice: 2.99<br>
> unitGrossPrice: 2.39<br>
> priceModifier: 2<br>
> discountValue: 0.60<br>
>
> => A 0.30 € discount was applied to this line item.

> **Example 3:**
>
> unitOriginalGrossPrice: 14.99<br>
> unitGrossPrice: 9.99<br>
> priceModifier: 3<br>
> discountValue: 5<br>
>
> => The price of this line item was reduced from 14.99 € to 9.99 €.

## Store
These endpoints are used to manage the stores of a vendor. This can also be done on the anybill Partner Portal.  
The most important usecase of these endpoints is to enable larger companies to automate the process of syncing store details. 

## Category
These endpoints list all categories which are available to categorize the line items and the bill.

# Postman
**The postman collection is not yet up to date for v2!** A Postman collection can be found [here](./Postman/Anybill%20Vendor%20Api.postman_collection.json).
There are also environments for [Staging](./Postman/Environments/Anybill%20VendorApi%20Staging.postman_environment.json) and [Production](./Postman/Environments/Anybill%20VendorApi%20Production.postman_environment.json)

To acquire an access_token first set your credentials for the following collection variables:
- username
- password
- client_id

After your credentials are set, send a request with the `GetToken` request. The acquired access token will automatically be set for all requests in the collection. Choose the environment and you are good to go. 

# Migration information from v1
Some general migration information:
- UserId is not part of the `AddBillDto` anymore. It is now part of the bill route if needed.
- Some properties of the `AddBillDto` moved to the `LegalInformationDto`.
- `LineItemDto` has alot more properties.
- `LineItemDto` some property names changed to better reflect the value.
- `TenderDto` has other `TenderTypeDto` and new detailed tender type to support more tender types and give some more flexibility. See description above.
- `StoreDto` shortName and longName changed to displayName and legalName

# Changelog
Changes to the V2 Api will be documented here.

### **2020-02-27** Initial Preview