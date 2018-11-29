**Card API Use Case**
=

First create a sandbox by calling the Create Sandbox endpoint, providing a Sandbox ID of your choice. Save this ID as you will need it for each subsequent call.\
By calling import sandbox, you can get the contents of your sandbox. In the response you will find values for the url parameters for the rest of the API calls, such as bank ID, account ID, view_id etc.


This api provides a set of endpoints to implement financial data aggregation.\
A user can review their cards that are automatically created with the creation of the sandbox. The available endpoints to the user for querying their cards, are :

* Get cards for the current user
* Get cards for the specified bank

For example, by calling **Get cards for the specified bank**, a user will get a list of all their cards for a given bank along with details for each card such as :
* Card Number
* Connected Account
* Expiration date