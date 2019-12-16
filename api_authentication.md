# Authentication

###	Basics
Communication with the anybill cloud is only possible after prior authentication. 
anybill uses OAuth 2.0 or OpenId Access Tokens for authentication. The identities
are managed in an Azure Active Directory B2C.
To get an access token you need a client id and a service account with username and password.

- The client ID is assigned by anybill once per POS system manufacturer.
- Username and password of the service account are assigned by anybill to the merchant.

### Scopes
The functional areas of the API are secured by scopes. An access token with the
requested scopes must be used for the respective functional area. The following
scopes currently exist:
- https://ad.anybill.de/vendor/category 
- https://ad.anybill.de/vendor/bill
- https://ad.anybill.de/vendor/store

### Retrieving an Access Token
To retrieve an access token, an HTTP POST request with the following data must be
sent to our OAuth 2.0 endpoint.
<br><br>
**URL**<br>
https://adanybill.b2clogin.com/ad.anybill.de/oauth2/v2.0/token?p=b2c_1_ropc_vendor

**Header**<br>
Content-Type: application/x-www-form-urlencoded

**Query Parameters**<br>
{“p” : “b2c_1_ropc_vendor”}

**Body**
```
{
    grant_type: password
    username: <service account username>
    password: <service account password>
    client_id: <client id of the POS system manufacturer>
    scope: https://ad.anybill.de/vendor/bill offline_access
    response_type: token
}
```
 
If authentication is successful, the server outputs the access token as a response
in the following format:
```
{
    "access_token": "*****",
    "token_type": "Bearer",
    "expires_in": "86400",
    "refresh_token": "*****"
}
```

For every communication with endpoints of the anybill API the access token must be
specified in the header:

Authorization: Bearer <access_token>

### Retrieving a Refresh Token
The access token can be updated as follows.
<br><br>
**URL**<br>
https://adanybill.b2clogin.com/ad.anybill.de/oauth2/v2.0/token?p=b2c_1_ropc_vendor

**Header**<br>
Content-Type: application/x-www-form-urlencoded

**Query Parameters**<br>
{“p” : “b2c_1_ropc_vendor”}

**Body**
 ```
 {
     refresh_token: <refresh token>
     grant_type: refresh_token
     client_id: <client id of the POS system manufacturer>
     scope: https://ad.anybill.de/vendor/bill offline_access
     response_type: token 
 }
 ```

If the update is successful, the server outputs the access token as a response in the
following format:
 ```
{
    "access_token": "*****",
    "token_type": "Bearer",
    "expires_in": "86400",
    "refresh_token": "*****",
    “refresh_token_expires_in”: “*****”,
}
 ```
