# Intoduction

The Loan API is an interface for a merchant in order to integrate with the NBG service of online loan application.

The Online Flow services are used while the customer is still in the Web UI of the merchant, The online flow terminates when the Loan Application is ready for approval.

The Offline Flow services are used when the merchant has been informed at a later stage that the application has been approved and the customer needs to download the generated loan contract. The customer then using the Loan API is able to digitally sign and submit the generated loan contact.

Between the Online Flow and Offline Flow services, the developer must use the Update Sandbox service in order to change the application status to "Application Approved", emulating the action of the NBG responsible for approving the the loan application.

### Loan Application Statuses

Each service of the API advances the status of the application to the next one. The statuses of the application are:

1. Initialized
1. BindCustomerDataOk
1. VerifyCustomerDataOk
1. PrecontractualDocumentsOtpRequestedOk
1. PrecontractualDocumentsConfirmedOk
1. ApplicationApproved
1. LoanContractOtpRequestedOk
1. LoanContractConfirmedOk

For executing a service, the application must have a specific status indicating that all previous steps have been executed successfully.

### Steps

1. Application Initialization: A new application is created under the user's sandbox. (Initialized)
2. Customer Data retrieval: The customer data are copied under the application (BindCustomerDataOk)
3. Precontractual Document Generation: The customer data are submitted back to the application. If data are valid then in the  next step the user can download the precontractual documents (VerifyCustomerDataOk)
4. Precontractual Documents Download: The user receives the precontractual documents 
5. The User requests otp for confirmign the documents (PrecontractualDocumentsOtpRequestedOk)
5. Precontractual Documents Confirmation: The user confirms that has accepted the documents (PrecontractualDocumentsConfirmedOk)
6. The user updates the application in the sandbox with the status "ApplicationApproved" (ApplicationApproved)
7. The user now can download the Loan contract document 
8. The user requests signing of the loan contract document (LoanContractOtpRequestedOk)
9. The user signs and downloads the digitally signed loan contract document (LoanContractConfirmedOk)
