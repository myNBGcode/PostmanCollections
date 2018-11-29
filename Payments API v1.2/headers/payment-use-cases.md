**Payment API Use Case**
=

First create a sandbox by calling the Create Sandbox endpoint, providing a Sandbox ID of your choice. Save this ID as you will need it for each subsequent call.\
By calling import sandbox, you can get the contents of your sandbox. In the response you will find values for the url parameters for the rest of the API calls, such as bank ID, account ID, view_id etc.


_Payment API_
-

This api provides a set of endpoints to implement payments from a user's account.

* Prior to requesting a transaction, a user can get information about the commission of a transaction by calling the **Get Charge Information (SEPA)** endpoint
* Additionally a user can retrieve the transaction types available by calling the **Get the Transaction Request Types supported by the bank** endpoint
* By calling the **Create Transaction Request (SEPA)** endpoint, a user can place a transaction request for verification. As a response, the user gets the details of the requested transaction along with the challenge ID for verification.
* To verify the request transaction, the user has to call the **Answer Transaction Request Challenge** endpoint and provide the challenge ID (found in the response of the previous call)and the answer in order to verify the request.
* After the transaction is successfully verified, the user can see details about the transaction by calling the **Get Transaction Request Details**, providing the desired transaction request ID. By calling the **Get Transaction Requests** endpoint, the user can get a list of requested transactions from a specific account.

