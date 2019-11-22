# Use case scenario
#### Welcome to the Confirmation Funds Sandbox API.

------------------------------------------------------------------------------------------
### The API
This API provides a standard RESTful interface that enables a user to check the availability of their funds. The availability is determined by providing the account's details and the corresponding amount in question.

> Visit https://developer.nbg.gr/documentation/Confirmation-Funds-API-OAuth2-v1.3 for the full API documentation

### Authentication & Authorization (OAuth2)
This API version uses the OAuth2.0 protocol for authentication and authorization, which means that a Bearer (access token) should be acquired. An access token can be retrieved using the client_id and client_secret of the APP that you created and subscribed in this API, and your own credentials (username, password) that you use to sign in the NBG Technology HUB. The scopes are defined below:

    
**Sandbox Scopes** : openid profile role sandbox-funds-confirmation-api-v1-3
    
    
**Production Scopes** : openid profile ibank_profile role funds-confirmation-api-v1-1
    

**Authorization Endpoint**: https://my.nbg.gr/identity/connect/authorize
    
    
**Token  Endpoint**: https://my.nbg.gr/identity/connect/token


See more [here](https://developer.nbg.gr/oauth-document)

### Use Case Scenario 
"Wallet" Inc. has a mobile app, which offers an service in order to check if a transfer is possible based on your current funds. Use the header "x-consent-check: false" in order to enable/disable the consent_id parameter validation to help you get up to speed with consuming the core API functionality before dealing with the user consent flow (See more [here](https://developer.nbg.gr/documentation/Confirmation-Funds-API-OAuth2-v13-5674#section/Quick-Getting-Started)).

First of all, we will create our sandbox by making an **HTTP POST** request to the following URL
> https://apis.nbg.gr/sandbox/confirmation.funds/oauth2/v1.3/sandbox

With a request body:
```json
{
  "header": {
	"ID": "e635360e-f1b8-4deb-810c-b75b055f4ba5",
	"application": "598A4414-395A-43D6-A9C3-D53A15E6E9F6"
  },
  "payload": {
	"sanboxId": "MySandbox"
  }
}
``` 

**Note: Remember to store *sandbox_id* somewhere in your application, because you will need to provide it in as a header in each api call. Moreover userId should be the same as the logged in user username.**

The funds availability can be retrieved from the following API Call

> https://apis.nbg.gr/sandbox/confirmation.funds/oauth2/v1.3/funds-confirmations/check-availability

With a request body:
```json
{
  "header": {
    "ID": "9155cc0e-de98-4b75-8a5c-8a7b614ad7bb",
    "application": "598A4414-395A-43D6-A9C3-D53A15E6E9F6"
  },
  "payload": {
    "iban": "GR5301106780000067890123456",
    "payee": "User1",
    "amount": {
      "amount": 1,
      "currency": "EUR"
    },
    "userId": "User1"
  }
}
```

Created by **NBG**. 
See more at https://developer.nbg.gr/
