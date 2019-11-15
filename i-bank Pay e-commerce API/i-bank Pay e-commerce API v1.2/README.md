 
# Use case scenario
# IBankPay eCommerce Sandbox API
------------------------------------------------------------------------------------------

### Introduction
The iBankPay eCommerce API, combined with the client's side Checkout process, enables us to finalize payments that have been created through the client. Specifically, the first part of the process is the one that happens in the client side (The customer's web browser) in order to create Payments with payment tokens returned and the final part takes place in your server's side for using our REST API to finalize the payments.


> The full API documentation: https://developer.nbg.gr/documentation/iBankPay-eCommerce-Sandbox-API-v1.2

### Use case scenario
This use case scenario will guide you from the checkout button of your website, to the sandbox calls in order to integrate the i-bank Pay payment method, which will trigger the below flow:

  - Make a Payment (This will be done by the Checkout button and the i-frame)
  - Authorize a Payment
  - Complete a Payment

In order to use this API for the first time you will need to create a Sandbox by making an **HTTP POST** request to the following URL
> https://apis.nbg.gr/sandbox/ecommercepay/headers/v1.2/

With a request body:
```json
 {
   "sandbox_id": "Your_custom_id"
 }
``` 

*Note: Remember to store the **sandbox_id** somewhere in your application, because you will need to provide it in as a header in each api call. Also for your ease remember to change your sandbox_id in the enviroment.json provided with this API and the *X-IBM-Client-Id* header with the Client ID provided from your subscription of your application in the Developers Portal site.*

Once the sandbox is created, proceed with the flow of **Create** a Payment, **Authorize** the Payment and then finally **Complete** the Payment.

In order to Create a Payment you will firstly implement the UI by importing into your html page the *script* provided and one of the 2 button choices provided from the API documentation. The buttons provided return a *token* after the Payment is Created and you will need that *token* in order to Complete the Payment on the final call.

So, click **Pay** and the i-frame will appear. At this point a Payment is **Created** with the amount that you provided.

The next step is to **Authorize** this Payment and in order to simulate the action of a user scanning the QR code of the i-frame, you will have to call with **HTTP GET** the Authorize Payment from your postman with the appropriate headers and a response is received like bellow:
```json
 {
   "OK"
 }
``` 

The last step is to create a button that will call the Complete Payment with **HTTP POST** passing as query parameters the Payment Amount, the Payment Token that you have received (with the buttons provided) and the merchant reference which is your sandbox_id.

With this procedure you have successfully completed a payment.

Created by **NBG**.
See more at https://developer.nbg.gr/
