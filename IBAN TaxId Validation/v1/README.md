# **IBAN Tax Id Validation OAuth2 API v1.0**

----------

## **Introduction to the API**

This API helps user check if IBAN belongs to a certain AFM.

**Real Life Use Case Scenario**

Imagine you want to check if IBAN belongs to certain AFM? Just use this api to create a custom made IBAN Tax Id Validation Application.

**Create Sandbox**

Your first job is to create a sandbox and save your  **sandbox-id**  in order to be able to  **"play"**  with the api.

We will create our sandbox by making an  **HTTP POST**  request to the following URL:

> [https://apis.nbg.gr/sandbox/ibantaxid.validation/oauth2/v1.0/sandbox](https://apis.nbg.gr/sandbox/ibantaxid.validation/oauth2/v1.0/sandbox)

Request Body:

 {
   "sandbox-id": "my-validation-sandbox"
 }

**Note: Remember to store  _sandbox-id_  somewhere in your application, because you will need to provide it as a header in each api call. Also remember to use the  _Client-Id_  provided when you create your application in the portal.**

When you create the sandbox application it has some default data.

### **Request Headers**

The following headers are required for every call. In postman they are in the appropriate environment variables.

**Request Headers**:

```
   'accept: application/json'
   'sandbox_id: {{sandboxId}}'  
   'Client-Id: {{clientId}}'
```

### **Scenario Request**
You send  **POST /validation/Match**  request to validate your iban and taxId
> [https://apis.nbg.gr/sandbox/ibantaxid.validation/oauth2/v1.0/sandbox/validation/Match](https://apis.nbg.gr/ibantaxid.validation/oauth2/v1.0/sandbox/validation/Match)

---
Created by  **NBG**.  
See more at  [https://developer.nbg.gr/](https://developer.nbg.gr/)