# Use case scenario
#### Welcome to the Transactions Sandbox API.

------------------------------------------------------------------------------------------

### The API
This API provides a standard RESTful interface that enables a user to
* Get all the transactions specified by account and bank
* Get the details of a specific transaction

> Visit https://developer.nbg.gr/documentation/Transactions-API-OAuth2-v1.2
> for the full API documentation

### Real life Use Case Scenario

The main functionality of the application is to review transactions issued by a user.

First of all, we will create our sandbox by making an **HTTP POST** request to the following URL
> https://microsites.nbg.gr/api.gateway/sandbox/obptransaction/oauth2/v1.2/sandbox

With a request body:
```json
 {
   "sandbox_id": "DE2A6935-9162-4076-B160-B5D3069DAE45"
 }
``` 

**Note: Remember to store *sandbox_id* somewhere in your application, because you will need to provide it in as a header
in each api call.**


There exists an application, "MyAccountant", that offers the functionality of reviewing the details of a specific transaction that the user has issued. A user of the application wants to know if a requested transaction has been completed 
or it is still pending execution.

To do so, the user selects the bank to get their transactions from,the account and the view, and the application calls the api a **HTTP POST** request to the following endpoint:
> https://microsites.nbg.gr/api.gateway/sandbox/obptransaction/oauth2/v1.2/obp/banks/{bank_id}/accounts/{account_id}/{view_id}/transactions/details

along with a request body:
```json
{
  "tranId": "0b30f879-cd0b-49bc-b474-39e2bbb89395",
  "remTpe":"SEPA"
}
```
will return the results below:

```json
{
    "transactionId": "0b30f879-cd0b-49bc-b474-39e2bbb89395",
    "ordererBankBic": "ETHNGRAA",
    "ordererName": "sDoulfis",
    "ordererAccountNo": "97226400154",
    "ordererIban": "GR0901109720000097226400154",
    "benAccountNo": "10348012377",
    "benIban": "GR4501101030000010348012377",
    "benName": [
        "User2"
    ],
    "remAmount": -20,
    "commision": null,
    "chargesAmount": null,
    "chargesXt": null,
    "chargesMsg": null,
    "valeur": "2018-11-30T00:00:00+02:00",
    "issueDate": "2018-11-29T00:00:00+02:00",
    "description": "",
    "remStatus": "Pending",
    "remMsg": []
}
```

From the response, the field "remStatus" contains the state of the transaction, "Pending" in this case.


Created by **NBG**. 
See more at https://developer.nbg.gr/
