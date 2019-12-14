# Anybill App QR-Code
The QR-Code in the anybill app has the following json structure:

Example of the json-object:
```json
{
  "Actions" : 
  [
      "anybill_add_bill"
  ],
  "UserId" : "CB8B722D-D00C-46BF-9F55-47E91CF4B8C5"
}
```

The UserId-property will be in the form of a global unique identifier (GUID).

The Actions-property can have multiple actions. Currently there can be the following actions:
- `anybill_add_bill` instructs to add the bill to the user  