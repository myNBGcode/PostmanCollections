## **Payment Initiation v3.1 Sandbox API** 
****
### **Introduction to the API**
This API helps you perform a Domestic or International Payment. You may perform an immediate payment, schedule a future payment or even schedule a Standing Order.
The api conforms to the UK Open Banking PSD2 specification.

### **Real Life Use Case Scenario**
Imagine you want to perform a Payment using your own application. What can you do about it? Just use this api to make a payment, in any platform you prefer.

### **Create Sandbox**
Your first job is to create a sandbox and save your **sandbox-id** in order to be able to **"play"** with the api.

We will create our sandbox by making an **HTTP POST** request to the following URL:
> https://apis.nbg.gr/sandbox/uk.openbanking.paymentinitiation/oauth2/v3.1.1/sandbox

Request Body:
```json
 {
   "sandbox-id": "my-payments-sandbox"
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
   'x-idempotency-key: {{idempotencyKey}}'
   'x-fapi-interaction-id: {{$guid}}
   'sandbox-id: {{sandboxId}}'  
   'Client-Id: {{clientId}}'

``` 
## **Scenario Request**
You send **POST /domestic-payments** request to make an immediate domestic payment.
> https://apis.nbg.gr/sandbox/uk.openbanking.paymentinitiation/oauth2/v3.1.1/domestic-payments

**Request**
```json
{
	"Data":{
		"ConsentId":"108dbd9c-09c9-4ff7-a6c4-c81f0a7e8b2f",
		"Initiation":{
			"debtorAccount":{
				"name":"My Debtor Account",
				"schemeName":"UK.OBIE.IBAN",
				"Identification":"GR3201155421998531020486502"
			},
			"creditorAccount":{
				"name":"The Creditor Account",
				"schemeName":"UK.OBIE.IBAN",
				"Identification":"GR3201155421998531020486501"
			},
			"instructedAmount":{
				"amount":"40",
				"currency":"EUR"
			},
			"EndToEndIdentification":"108dbd9c-09c9-4ff7-a6c4-c81f0a7e8b2f",
			"InstructionIdentification":"108dbd9c-09c9-4ff7-a6c4-c81f0a7e8b2f"
		}
	},
	"Risk":{}
}
``` 

**Response** (Contains information about the available accounts (e.g. currency, type, description)):
```json
{
    "Data": {
        "DomesticPaymentId": "108dbd9c-09c9-4ff7-a6c4-c81f0a7e8b2f",
        "ConsentId": "346c9cf9-9204-4604-954a-1ab2e0c45191",
        "CreationDateTime": "2019-06-27T16:33:50.1437327+03:00",
        "Status": "AcceptedSettlementCompleted",
        "Charges": [
            {
                "ChargeBearer": "Shared",
                "Amount": {
                    "Amount": 1,
                    "Currency": "EUR"
                }
            }
        ],
        "Initiation": {
            "InstructionIdentification": "108dbd9c-09c9-4ff7-a6c4-c81f0a7e8b2f",
            "EndToEndIdentification": "108dbd9c-09c9-4ff7-a6c4-c81f0a7e8b2f",
            "InstructedAmount": {
                "Amount": 40,
                "Currency": "EUR"
            },
            "DebtorAccount": {
                "SchemeName": "UK.OBIE.IBAN",
                "Identification": "GR3201155421998531020486502",
                "Name": "My Debtor Account"
            },
            "CreditorAccount": {
                "SchemeName": "UK.OBIE.IBAN",
                "Identification": "GR3201155421998531020486501",
                "Name": "The Creditor Account"
            }
        }
    },
    "Links": {
        "Self": "https://microsites.nbg.gr/api.gateway/sandbox/uk.openbanking.payments/oauth2/v3.1/domestic-payments"
    },
    "Meta": {
        "TotalPages": 1
    }
}

``` 


Created by **NBG**.\
See more at https://developer.nbg.gr/