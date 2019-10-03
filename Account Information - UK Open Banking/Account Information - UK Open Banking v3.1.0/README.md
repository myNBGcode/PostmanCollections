## **Account Information OAuth2 API v3.1.0** 
****
### **Introduction to the API**
This API helps you obtain a list of your accounts and their respective information such as balances, transactions, statements and beneficiaries.
The api conforms to the UK Open Banking PSD2 specification.

### **Real Life Use Case Scenario**
Imagine you want to create an application which handles all of your banks' accounts. What can you do about it? Just use this api to create a custom made Account Management Application, in any platform you prefer, in order to retrieve your accounts' information.

### **Create Sandbox**
Your first job is to create a sandbox and save your **sandbox-id** in order to be able to **"play"** with the api.

We will create our sandbox by making an **HTTP POST** request to the following URL:
> https://apis.nbg.gr/sandbox/uk.openbanking.accountinfo/oauth2/v3.1.1/sandbox

Request Body:
```json
 {
   "sandbox-id": "my-accounts-sandbox"
 }
``` 

**Note: Remember to store *sandbox-id* somewhere in your application, because you will need to provide it as a header
in each api call. Also remember to use the *Client-Id* provided when you create your application in the portal.**

When you create the sandbox application it has some default data.
## **Request Headers**
The following headers are required for every call. In postman they are in the appropriate environment variables.

**Request Headers**:
```
   'accept: application/json'
   'x-fapi-financial-id: {{financialId}}'
   'x-subject-bank-id: {{bankId}}'
   'x-fapi-interaction-id: {{$guid}}
   'sandbox-id: {{sandboxId}}'  
   'Client-Id: {{clientId}}'

``` 
## **Scenario Request**
You send **GET /accounts** request to get a list of the available accounts among with their details. The level of details depend on the permission that has been asigned to the Consent. For our testing purposes full permissions will be granted.
> https://apis.nbg.gr/sandbox/uk.openbanking.accountinfo/oauth2/v3.1.1/accounts


**Response** (Contains information about the available accounts (e.g. currency, type, description)):
```json
{
"Data": {
	"Account": [{
		"AccountId": "ACCOUNT_ID",
		"Currency": "EUR",
		"AccountType": "Personal",
		"AccountSubType": "Savings",
		"Description": "This is a personal savings account",
		"Nickname": "A Savings Account",
		"Account": [{
			"SchemeName": "UK.OBIE.IBAN",
			"Identification": "GR32011XXXXXXXXXXXXXXXXXXXX",
			"Name": "Ha****** Ab*****"
		}],
		"Servicer": {
			"SchemeName": "UK.OBIE.BICFI",
			"Identification": "ETHNGRAA"
		}
	}]
},
"Links": 
	"Self": "https://apis.nbg.gr/sandbox/uk.openbanking.accountinfo/oauth2/v3.1.1/accounts/accounts"
},
"Meta": {
	"TotalPages": 1
}

``` 


Created by **NBG**.\
See more at https://developer.nbg.gr/