# Use case scenario
#### Welcome to the Payments Initiation Sandbox API.

------------------------------------------------------------------------------------------
### The API
This API provides a standard RESTful interface that enables a user to send money to any account.

Moreover an expenses calculation mechanism is provided in order to be aware of the expenses of an transfer. Use it by invoking the POST /payments/transfer-charges API call.

There are 3 types of payments:
* NBG Transfer (Transfer between NBG accounts using the 11 digit account number format)
* Sepa Transfer (Transfer using account’s IBAN format, receiver account can be either a NBG account or any other bank account e.g Eurobank)
* Non Sepa Transfer (In case the receiver account bank does not support IBAN format and a different account number format is needed, which format depends on the bank that is used)

> Visit https://developer.nbg.gr/documentation/Payments-Initiation-API-OAuth2-v1.3 for the full API documentation

### Authentication & Authorization (OAuth2) ##
This API version uses the OAuth2.0 protocol for authentication and authorization, which means that a Bearer (access token) should be acquired. An access token can be retrieved using the client_id and client_secret of the APP that you created and subscribed in this API, and your own credentials (username, password) that you use to sign in the NBG Technology HUB. The scopes are defined below:
    
    
**Sandbox Scopes** : openid profile role sandbox-payment-initiation-api-v1-3
    
    
**Production Scopes** : openid profile ibank_profile role payment-initiation-api-v1-1


**Authorization Endpoint**: https://my.nbg.gr/identity/connect/authorize
    
    
**Token  Endpoint**: https://my.nbg.gr/identity/connect/token


See more [here](https://developer.nbg.gr/content/authorization-oauth-20#8an-authorization-code-flow-example)

### Use Case Scenario 
"Payments" Inc. has a mobile app, which offers an service in order to transfer money between accounts. As an additional feature "Payments" Inc provides a mechanism which calculates the transfer charges of a provided payment so that the user is always informed of the current expense system. Use the header "x-consent-check: false" in order to enable/disable the consent_id parameter validation to help you get up to speed with consuming the core API functionality before dealing with the user consent flow (See more [here](https://developer.nbg.gr/documentation/Payments-Initiation-API-OAuth2-v13-5680#section/Quick-Getting-Started)).

First of all, we will create our sandbox by making an **HTTP POST** request to the following URL
> https://apis.nbg.gr/sandbox/payment.initiation/oauth2/v1.3/sandbox

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

The calculation expense mechanism can be invoked from the following url:
> https://microsites.nbg.gr/api.gateway/sandbox/payment.initiation/oauth2/v1.3/payments/transfer-charges

With a request body:
```json
{
  "header": {
    "ID": "9aab6381-e11d-4748-8efa-ada57210b27d",
    "application": "598A4414-395A-43D6-A9C3-D53A15E6E9F6"
  },
  "payload": {
    "from": "67890123456",
    "to": {
      "accountIban": "GR9601106780000067890123458",
      "beneficiaryBic": "ETHNGRAA"
    },
    "amount": 1,
    "currency": "EUR",
    "userId": "User1",
    "type": "NBG",
    "chargePolicy": "SHA"
  }
}
```

Second the user can transfer money between NBG accounts. The endpoint can be invoked from the following url:
> https://microsites.nbg.gr/api.gateway/sandbox/payment.initiation/oauth2/v1.3/payments/nbg-transfer

With a request body:
```json
{
  "header": {
    "ID": "9aab6381-e11d-4748-8efa-ada57210b27d",
    "application": "598A4414-395A-43D6-A9C3-D53A15E6E9F6"
  },
  "payload": {
    "from": "67890123456",
    "to": "67890123458",
    "amount": 1,
    "description": "PAYMENT TEST 1",
    "tanNumber": "smsotp",
    "userId": "User1"
  }
}
```

**Remember** the above endpoint uses an SMS One Time Password mechanism. You have to invoke the endpoint two times. First with the "smsotp" value in the tanNumber field. Second with the actual value that is sended as an sms. (6 digits number)

Third the user can send money not only to an NBG account but to another bank as well. The following endpoint serves this purpose:

> https://microsites.nbg.gr/api.gateway/sandbox/payment.initiation/oauth2/v1.3/payments/sepa-transfer

With a request body:
```json
{
  "header": {
    "ID": "9aab6381-e11d-4748-8efa-ada57210b27d",
    "application": "598A4414-395A-43D6-A9C3-D53A15E6E9F6"
  },
  "payload": {
    "payerIban": "GR5301106780000067890123456",
    "to": "GR9601106780000067890123458",
    "amount": 1,
    "chargePolicy": "SHA",
    "beneficiary": "GEORGE",
    "description": "PAYMENT TEST 1",
    "tanNumber": "smsotp",
    "currency": "EUR",
    "userId": "User1"
  }
}
```

**Remember** the above endpoint uses an SMS One Time Password mechanism. You have to invoke the endpoint two times. First with the "smsotp" value in the tanNumber field. Second with the actual value that is sended as an sms. (6 digits number)

Created by **NBG**. 
See more at https://developer.nbg.gr/
