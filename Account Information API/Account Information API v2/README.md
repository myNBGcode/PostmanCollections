# Use case scenario
#### Welcome to the Accounts Information Sandbox API.

------------------------------------------------------------------------------------------
### The API
This API provides a standard RESTful interface that enables a user to:
* Set consents for accounts
* View their account list
* View their account details
* View their account balances
* View their account transactions

> Visit https://developer.nbg.gr/documentation/Accounts-Information-API-OAuth2-v2 for the full API documentation

### Authentication & Authorization (OAuth2)
This API version uses the OAuth2.0 protocol for authentication and authorization, which means that a Bearer (access token) should be acquired. An access token can be retrieved using the client_id and client_secret of the APP that you created and subscribed in this API, and your own credentials (username, password) that you use to sign in the NBG Technology HUB. The scopes are defined below:


**Sandbox Scopes**: openid profile role sandbox-account-info-api-v2


**Production Scopes**: openid profile ibank_profile role account-info-api-v2


**Authorization Endpoint**: https://my.nbg.gr/identity/connect/authorize
    
    
**Token  Endpoint**: https://my.nbg.gr/identity/connect/token


See more [here](https://developer.nbg.gr/oauth-document)

### Use Case Scenario 
"User Accounts" Inc. has a mobile app, showing the user domestic and foreign currency accounts. The main functionality of the application is to retrieve some user basic informations e.g.  his/her name and to retrieve his/her accounts so that the user is 24/7 informed about his/her accounts status e.g balances, transactions etc. Use the header "x-consent-check: false" in order to enable/disable the consent_id parameter validation to help you get up to speed with consuming the core API functionality before dealing with the user consent flow (See more [here](https://developer.nbg.gr/documentation/Accounts-Information-API-OAuth2-v2#section/How-To-Get-Started)).

First of all, we will create our sandbox by making an **HTTP POST** request to the following URL
> https://apis.nbg.gr/sandbox/account.info/oauth2/v2/sandbox

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


The available domestic accounts can be retrieved from the following API Call:

> https://apis.nbg.gr/sandbox/account.info/oauth2/v2/account/list

With a request body:
```json
{
  "header": {
	"ID": "bf80bcea-7a8b-4a4a-aac3-0ea52f0494e2",
	"application": "598A4414-395A-43D6-A9C3-D53A15E6E9F6"
  },
  "payload": {
	"userId": "User1"
  }
}
``` 

**Domestic Account Details**

Based on the account list returned the user can choose one of their accounts and see the account details or account transactions. The endpoint is available in the following url:

> https://apis.nbg.gr/sandbox/account.info/oauth2/v2/account/details

With a request body:
```json
{
  "header": {
    "ID": "bf80bcea-7a8b-4a4a-aac3-0ea52f0494e2",
    "application": "598A4414-395A-43D6-A9C3-D53A15E6E9F6"
  },
  "payload": {
    "account": "67890123456",
    "userId": "User1"
  }
}
``` 

**Domestic Account Transactions**

The endpoint is available in the following url:
> https://apis.nbg.gr/sandbox/account.info/oauth2/v2/account/transactions


With a request body:
```json
{
  "header": {
    "ID": "bf80bcea-7a8b-4a4a-aac3-0ea52f0494e2",
    "application": "598A4414-395A-43D6-A9C3-D53A15E6E9F6"
  },
  "payload": {
    "account": "67890123456",
    "dateFrom": "2018-01-25",
    "dateTo": "2019-12-31",
    "userId": "User1"
  }
}
``` 

The available foreign accounts can be retrieved from the following API Call

> https://apis.nbg.gr/sandbox/account.info/oauth2/v2/foreign-currency-account/list

With a request body:
```json
{
  "header": {
	"ID": "bf80bcea-7a8b-4a4a-aac3-0ea52f0494e2",
	"application": "598A4414-395A-43D6-A9C3-D53A15E6E9F6"
  },
  "payload": {
	"userId": "User1"
  }
}
``` 

Similarly to the domestic accounts, the user can see their account transactions or account details of a chosen foreign currency account.

**Foreign Account Details**

The endpoint is available in the following url:
> https://apis.nbg.gr/sandbox/account.info/oauth2/v2/foreign-currency-account/details

With a request body:
```json
{
  "header": {
    "ID": "bf80bcea-7a8b-4a4a-aac3-0ea52f0494e2",
    "application": "598A4414-395A-43D6-A9C3-D53A15E6E9F6"
  },
  "payload": {
    "account": "67890123456",
    "userId": "User1"
  }
}
``` 

**Foreign Account Transactions**

The endpoint is available in the following url:
> https://apis.nbg.gr/sandbox/account.info/oauth2/v2/foreign-currency-account/transactions

With a request body:
```json
{
  "header": {
    "ID": "bf80bcea-7a8b-4a4a-aac3-0ea52f0494e2",
    "application": "598A4414-395A-43D6-A9C3-D53A15E6E9F6"
  },
  "payload": {
    "account": "67890123456",
    "dateFrom": "2019-01-25",
    "dateTo": "2019-12-31",
    "userId": "User1"
  }
}
``` 

Created by **NBG**. 
See more at https://developer.nbg.gr/
