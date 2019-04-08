# **Introduction**
#### Welcome to Digital Payments Wallet Sandbox
------------------------------------------------------------------------------------------

### A few words about Digital Payments Wallet 
Digital Payments Wallet is the multi-award winning wallet by National Bank of Greece that is used to:
- send money to your friends and make payments and purchases with your phone
- make money transfers between your friends
- pay businesses and professionals

### The API
This API provides a standard RESTful interface that enables a user to
- Perform money transfers to another member or merchant or even make donations by just  **registering as a Member**  to our service and verifying your mobile device as a trusted one. 
- Once the registration step is completed simply  **select the other member**  you wish to  **send money to or request money from or pay**  and pretty much that's it.
> Visit https://developer.nbg.gr/documentation/ibank-Pay-Sandbox-v13-5326
> for the full API documentation
> 
### Real life Use Case Scenario
Given that you want to buy something from a store, but you don't carry your wallet. 
All you have to do is download myWallet App, make a registration and accept the request for payment that the merchant has started via POS.
In this scenario we will be using the API to register as a member and perform a P2B payment.

#### How do I make a registration?
First of all, we will create our sandbox by making an **HTTP POST** request to the following URL
>https://microsites.nbg.gr/api.gateway/sandbox/ibankpay/headers/v1.3/sandbox

With a request body:
```json
 {
   "sandbox_id": "5DE11422-D7D5-4727-82FA-0C26F195C66C"
 }
``` 

**Note: Remember to store *sandbox_id* somewhere in your application, because you will need to provide it in as a header in each api call.**

Then, you have to create a sandbox user by making an **HTTP POST** request to the following URL
>https://microsites.nbg.gr/api.gateway/sandbox/ibankpay/headers/v1.3/sandbox/{sandbox_id}/users

In order to register a member you have to make an **HTTP POST** request to the following URL
>https://microsites.nbg.gr/api.gateway/sandbox/ibankpay/headers/v1.3/P2P/registerMember

To complete the registration you have to verify the device by making an **HTTP POST** request to the following URL
>https://microsites.nbg.gr/api.gateway/sandbox/ibankpay/headers/v1.3/P2P/verifyDeviceRegistration
  
#### How do I pay a merchant?

First, the merchant has to create a payment request with an **HTTP POST** request to the following URL
>https://microsites.nbg.gr/api.gateway/sandbox/ibankpay/headers/v1.3/P2B/machinePaymentRequestRegistration

Then invoke an **HTTP POST** request to the following URL to see the pending payment request
>https://microsites.nbg.gr/api.gateway/sandbox/ibankpay/headers/v1.3/P2B/machinePaymentRequestInfoV2

Then invoke an **HTTP POST** request to the following URL to accept the payment
>https://microsites.nbg.gr/api.gateway/sandbox/ibankpay/headers/v1.3/P2P/acceptCreditV2 

Finally invoke an **HTTP POST** request to the following URL to see the payment result
>https://microsites.nbg.gr/api.gateway/sandbox/ibankpay/headers/v1.3/P2B/machinePaymentRequestInfoV2

Created by **NBG**. 
See more at https://developer.nbg.gr/
