*Transaction API Use Case*
=

First create a sandbox by calling the Create Sandbox endpoint, providing a Sandbox ID of your choice. Save this ID as you will need it for each subsequent call.\
By calling import sandbox, you can get the contents of your sandbox. In the response you will find values for the url parameters for the rest of the API calls, such as bank ID, account ID, view_id etc.

This api provides a set of endpoints to implement reviewing and reconciliation of transactions for a user's account

Once a transaction is completed , a user can query about them using the endpoints provided in the Transaction API :

* The user can get a list of completed transactions along with core/full details, calling **Get Transactions for Account (Core)** , **Get Transactions for Account (Full)** endpoints respectively. 
* The user can get details about a specific transaction by calling **Get Transaction details by reference number** endpoint.
Such details include among others : 
* Orderer Bank, 
* Orderer IBAN,
* Beneficiary IBAN,
* Beneficiary Name,
* Remittance Amount,
* Commission,
* Issue Date 
* Remittance Status