## **Funds Confirmation v3.1 Sandbox API** 
****
### **Introduction to the API**
This API helps you get informed about Funds Availability before initiating a Payment.
The api conforms to the UK Open Banking PSD2 specification.

### **Real Life Use Case Scenario**
Imagine you want to get informed about funds availability before initiating a payment in ac card. What can you do about it? Just use this api to get informed.

### **Create Sandbox**
Your first job is to create a sandbox and save your **sandbox-id** in order to be able to **"play"** with the api.

We will create our sandbox by making an **HTTP POST** request to the following URL:
> https://apis.nbg.gr/sandbox/uk.openbanking.fundsconfirmation/oauth2/v3.1.1/sandbox

Request Body:
```json
 {
   "sandbox-id": "my-fundsconfirmations-sandbox"
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
   'x-fapi-interaction-id: {{$guid}}
   'sandbox-id: {{sandboxId}}'  
   'Client-Id: {{clientId}}'

``` 
## **Scenario Request**
You send **POST /domestic-payments** request to make an immediate domestic payment.
> https://apis.nbg.gr/sandbox/uk.openbanking.fundsconfirmation/oauth2/v3.1.1/funds-confirmation-consents

**Request**
```json
{
	"Data":{
		"DebtorAccount":{
			"SchemeName":"UK.OBIE.IBAN",
			"Identification":"GR3201155421998531020486502",
			"Name":"ACCOUNT_1"
			
		},
		"ExpirationDateTime":"2019-05-01T12:15:00"
		
	}
}
``` 

**Response** (Contains information about the available accounts (e.g. currency, type, description)):
```json
{
    "Data": {
        "ConsentId": "126fc7dd-4a56-4ff8-a58d-18d2044cf82c",
        "CreationDateTime": "2019-06-28T12:22:29.4219493+03:00",
        "Status": "Authorised",
        "StatusUpdateDateTime": "2019-06-28T12:22:29.4219507+03:00",
        "ExpirationDateTime": "2019-05-01T12:15:00",
        "DebtorAccount": {
            "SchemeName": "UK.OBIE.IBAN",
            "Identification": "GR3201155421998531020486502",
            "Name": "ACCOUNT_1"
        }
    },
    "Links": {
        "Self": "https://microsites.nbg.gr/api.gateway/sandbox/uk.openbanking.payments/oauth2/v3.1/funds-confirmation-consents"
    },
    "Meta": {
        "TotalPages": 1
    }
}

``` 


Created by **NBG**.\
See more at https://developer.nbg.gr/