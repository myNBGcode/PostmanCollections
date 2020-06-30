## IBAN Beneficiary Validation Sandbox API V1
****

### **Introduction to the API**
The NBG IBAN Beneficiary Validator API aims to enable End Customers of the Bank's ecosystem to validate an IBAN for antifraud and security cases.

One using the API is able to (1) retrieve an NBG account's beneficiaries, (2) calculate the confidence of a third bank's IBAN where the most likely beneficiaries names are returned, and finally (3) validate an NBG Iban against certain criteria and calculate the results confidence level.

### **Real Life Use Case Scenario**
This API helps you validate an IBAN and calculate its "confidence".

### **Create Sandbox**
Your first job is to create a sandbox and save your **Sandbox-id** in order to be able to **"play"** with the api.

We will create our sandbox by making an **HTTP POST** request to the following URL:
>  https://apis.nbg.gr/sandbox/iban.beneficiary.validation/oauth2/v1

Request Body:
```json
 {
   "sandbox_id": "my-sandbox-value"
 }
``` 

**Note: Remember to store *sandbox_id* somewhere in your application, because you will need to provide it as a header
in each api call. Also remember to use the *Client-Id* provided when you create your application in the portal.**

When you create the sandbox application it has some default data.

## **Request Headers**
The following headers are required for every call. In postman they are in the appropriate environment variables.

**Request Headers**:
```
   'Accept: application/json'
   'Sandbox-Id: {{sandbox-id}}'  
   'Client-Id: {{client-id}}'  

``` 
## **Scenario Request**
You send **POST beneficiaryValidation/nbgIban** request to get a list of all available white list actions.
>  https://apis.nbg.gr/sandbox/iban.beneficiary.validation/oauth2/v1s/beneficiaryValidation/nbgIban

**Request**
```json
{
	"iban": "GR1601100400000004012345600"
}
``` 

**Response**:
```json

{
    "beneficiaries": [
        "Κ****ς Π*****π**λ*ς",
        "Γ**ρ**ς Κ****κ**"
    ]
}


``` 


Created by **NBG**.\
See more at https://developer.nbg.gr/