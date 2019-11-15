# Use case scenario
#### Welcome to the IBAN Validation Sandbox API.

------------------------------------------------------------------------------------------
### A few words about IBAN
The International Bank Account Number (IBAN) is an internationally agreed system of identifying bank accounts across national borders to facilitate the communication and processing of cross border transactions with a reduced risk of transcription errors. It was originally adopted by the European Committee for Banking Standards (ECBS), and later as an international standard under ISO 13616:1997. The current standard is ISO 13616:2007, which indicates SWIFT as the formal registrar. Initially developed to facilitate payments within the European Union, it has been implemented by most European countries and numerous countries in the other parts of the world, mainly in the Middle East and in the Caribbean. As of February 2016, 69 countries were using the IBAN numbering system.[1]

The IBAN consists of up to 34 alphanumeric characters comprising: a country code; two check digits; and a number that includes the domestic bank account number, branch identifier, and potential routing information. The check digits enable a check of the bank account number to confirm its integrity before submitting a transaction.

> Read more at https://en.wikipedia.org/wiki/International_Bank_Account_Number

### The API
This API provides a standard RESTful interface that enables a user to
* Get the IBAN of a bank account number
* Check if an IBAN is valid

> Visit https://developer.nbg.gr/documentation/IBAN-Validation-API-v1.2 for the full API documentation

### Real life Use Case Scenario
In this scenario we will be using the API to provide data to the *IBAN Calculator* application.

The application lets you convert a national account number into an IBAN and validate an IBAN.

First of all, we will create our sandbox by making an **HTTP POST** request to the following URL
> https://apis.nbg.gr/sandbox/ibanvalidation/headers/v1.2/sandbox

With a request body:
```json
 {
   "sandbox_id": "26D4E02D-CCFB-4FA0-8867-0A1CD1D87B0E"
 }
``` 

**Note: Remember to store *sandbox_id* somewhere in your application, because you will need to provide it in as a header
in each api call.**

Let's start with the IBAN Validation part of the application.

The user is prompted by the application to fill in an IBAN they want to validate. The input is stored in the variable *{iban}* and it is going to be used in the following **HTTP GET** request:

> https://apis.nbg.gr/sandbox/ibanvalidation/headers/v1.2/iban/{iban}/check

The response is a JSON object containing information about IBAN validity as well as whether this IBAN belongs to the National Bank of Greece, as shown below.

```json
{
  "valid": true,
  "nbgIban": true
}
```

Secondly, lets proceed to the account to IBAN conversion part.

In this part, the user is asked to fill in an account number. The user input is stored in the *{account}* variable.
In order to get the related IBAN, the application makes an **HTTP GET** request to the following URL:

> https://apis.nbg.gr/sandbox/ibanvalidation/headers/v1.2/account/{account}/iban

The response contains a JSON object wih the result IBAN as shown below.
```json
{
  "iban": "GRXXXXXXXXXXXXXXXXXXX"
}
```


Created by **NBG**. 
See more at https://developer.nbg.gr/
