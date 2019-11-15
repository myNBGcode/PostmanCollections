# **Introduction**
#### Welcome to the Payments Sandbox API.

------------------------------------------------------------------------------------------

### The API
This API provides a standard RESTful interface that enables a user to
* Get the expenses related with a transaction
* Place a transaction request
* Get the details of a requested transaction

> Visit https://developer.nbg.gr/documentation/Payments-API-v1.3
> for the full API documentation

### Real life Use Case Scenario

The main functionality of the application is to execute payment requests from a user's account.

First of all, we will create our sandbox by making an **HTTP POST** request to the following URL
> https://apis.nbg.gr/sandbox/obppayment/headers/v1.3/sandbox

With a request body:
```json
 {
   "sandbox_id": "DE2A6935-9162-4076-B160-B5D3069DAE45"
 }
``` 

**Note: Remember to store *sandbox_id* somewhere in your application, because you will need to provide it in as a header
in each api call.**

There exists an application, "Switch", that users can stream online content and accept donations from their viewers. The application needs to give the viewer the ability to 
execute such donations using any of their accounts. For the receiver of the donation, only their iban needs to be known by the application.

To make such a donation, a viewer can create a transaction request by providing the bank id, account and view and executing a **HHTP POST** request to the following endpoint:
> https://apis.nbg.gr/sandbox/obppayment/headers/v1.3/obp/banks/{bank_id}/accounts/{account_id}/{view_id}/transaction-request-types/sepa/transaction-requests

along with a request body:
```json
{
	"to": {
		"iban": "GR4501101030000010348012377"
	},
	"charge_policy": "SHARED",
	"value": {
		"currency": "EUR",
		"amount": 1001
	},
	"description": "METAFORA"
}
```

getting the following response:


```json
{
    "extensions": null,
    "id": "fb753997-5873-4080-9ee3-4f48749cd6cc",
    "type": "SEPA",
    "from": {
        "bank_id": "DB173089-A8FE-43F1-8947-F1B2A8699829",
        "account_id": "cee1db2f-39e1-4918-b3fc-2d81d3439ccc"
    },
    "details": {
        "to": {
            "card_id": null,
            "account_id": "f64384b2-518c-4ab3-b4fb-7179d1fe0dc2",
            "bank_id": "DB173089-A8FE-43F1-8947-F1B2A8699829",
            "beneficiaryName": null
        },
        "value": {
            "currency": "EUR",
            "amount": 1001
        },
        "description": "METAFORA"
    },
    "transaction_ids": [],
    "status": "INITIATED",
    "start_date": "2018-11-29T10:44:27.3492016+02:00",
    "end_date": null,
    "challenge": {
        "id": "944c0b1d-67e7-4296-ae05-37a38d636ec3",
        "allowed_attempts": 3,
        "expiresOn": "0001-01-01T00:00:00",
        "confirmationCode": null,
        "challenge_type": "SMS"
    },
    "charge": {
        "summary": "SHARED",
        "value": {
            "currency": "EUR",
            "amount": 0
        },
        "chargeExtensions": null
    }
}
```

For the transaction to be completed, a user need only answer a challenge to verify the transaction request.

Created by **NBG**. 
See more at https://developer.nbg.gr/
