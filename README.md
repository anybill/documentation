# <img id="logo" src="./Assets/logo.svg" width="200" alt="anybill logo"/>

anybill is the solution, to transfer digital receipts directly at the checkout onto your customers´ smartphone.<br>

For technical questions, feel free to contact us:<br>

Tobias Gubo<br>
tobias.gubo@anybill.de<br>
+49 151 20457172<br>

Patrick Göttler<br>
patrick.goettler@anybill.de<br>
+49 157 50777325<br>

## Documentation
### HTTP API

[Vendor API](./api_vendor.md)

### App Documentation

[QR-Code](./app_qr.md)

## Workflow

1. User scanns the purchased items by cashier or self-scanning application at self chechout
2. Scanning of the [QR-Code](./app_qr.md) displayed in the app at the scanner of the cash register by customer for authentication
3. Recognition of the anybill ID by cash register and subsequent transfer of the receipt data to the [anybill Rest Api](./api_vendor.md)
