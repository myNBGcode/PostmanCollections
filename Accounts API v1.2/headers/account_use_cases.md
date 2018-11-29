*Account API Use Case*
=

First create a sandbox by calling the Create Sandbox endpoint, providing a Sandbox ID of your choice. Save this ID as you will need it for each subsequent call.\
By calling import sandbox, you can get the contents of your sandbox. In the response you will find values for the url parameters for the rest of the API calls, such as bank ID, account ID, view_id etc.


This api provides a set of endpoints to implement financial data aggregation.\
A user can review their accounts that are automatically created with the creation of the sandbox. The available endpoints to the user for querying their accounts, are :


* Get Accounts at all Banks (Private)
* Get Public Accounts at all Banks
* Get Accounts at one Bank (Public and Private)
* Get Accounts at Bank (Public)
* Get private accounts at one bank
* Get Account by Id (Core)
* Get Account by Id (Full)
* Get Account Beneficiaries by Id

For example, by calling **Get Account by Id (Full)**, a user will get the full details of the requested account, such as:
* Account Number
* List of owners
* Account type
* Amount and Currency
* Bank that the account belongs to