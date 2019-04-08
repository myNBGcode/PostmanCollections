## **Bill Payments v2 Sandbox API** 
****
### **Introduction to the API**
This API helps you to pay bills such as car taxes, taxes, electricity, water, and payback fees, it provides you full control of your bill payment lifecycle.
### **Real Life Use Case Scenario**
Everyone has bills and bills must be paid, so imagine you are somewhere that has no bank branches either places that you can pay your bills, taxes or car taxes.
What can you do about it?  The answer is simple, you can use this api to create a custom bill payments web application in order to help users pay their bills using their bank account.

**Idea**: You can use this API together with **Rewards Platform ( i-bank Loyalty API Sandbox - v1 )** in order to increase your customer’s loyalty by applying your own rewarding platform.

### **Create Sandbox**
Your first job is to create a sandbox and save your **sandbox_id** in order to be able to **"play"** with the api.

We will create our sandbox by making an **HTTP POST** request to the following URL:
> https://apis.nbg.gr/public/sandbox/billpayments/v2/sandbox

Request Body:
```json
 {
   "sandbox_id": "payforme"
 }
``` 

**Note: Remember to store *sandbox_id* somewhere in your application, because you will need to provide it as a header
in each api call. Also remember to use the *Client-Id* provided when you create your application in the portal.**

When you create the sandbox application it has some default data, for our use case example we will use **User1**.
## **Request Headers**
They are the same in each call so we mention them first, in postman they are stored in each environment variables.

**Request Headers**:
```

   'accept: text/json'
   'application_id: {{$guid}}'
   'content-type: text/json'
   'phone_number: null'
   'provider: NBG'
   'provider_id: NBG.gr'
   'sandbox_id: your_sandbox_id'  !!!payforme is the one that we used to create the use case sandbox, you can also use it to see the results!!!
   'user_id: e6da8f9c-ee8b-488c-9179-0a566e9d8aed'
   'username: User1'
   'Client-Id: your_Client-Id' !!!c33f6acf-5ef1-4d00-b801-058eaa4ad0ed is the one that we got from creating a test app at the portal, you can also use it to see the results!!!

``` 
## **Scenario Requests**

**Step1**: You send **POST /Payments/paymentsList** request to see if you support the payment that the customer wants to make.
So now you found that you support payments of water bills to **ΔΗΜΟΣ ΜΑΚΡΑΚΩΜΗΣ**.
> https://apis.nbg.gr/public/sandbox/billpayments/v2/Payments/paymentsList

**Request**:
```json
 {
  "header": {
    "ID": "{{$guid}}",
    "application": "{{application_id}}",
    "bank": "{{bank}}",
    "hostSession": null,
    "channel": "{{channel}}",
    "customer": 1,
    "logitude": 1,
    "latitude": 1,
    "go4moreMember": "{{go4moreMember}}",
    "TAN": null
  },
  "payload": {
    "userId": "{{user_id}}",
    "requestMachineId": null,
    "machineId": null
  }
}
``` 
**Response** (Retrieves all the supported organizations and it's payment methods):

<details><summary>Response</summary>
 
 ```json
 {
  "payload": {
        "payments": [
            {
                "id": "5b60f1c8-243f-4180-8c6b-0130572ee4ba",
                "legacyCode": "90906",
                "legacyType": "NONNBG",
                "name": "ΔΗΜΟΣ ΜΑΚΡΑΚΩΜΗΣ",
                "categoryName": "Δήμοι/Ύδρευση",
                "supportedPaymentMethods": [
                    {
                        "name": "ACCT",
                        "otp": false
                    }
                ],
                "isOnline": false,
                "supportsBarcode": false,
                "validationAlgorithm": "RI2",
                "sortOrder": 1,
                "objects": [
                    {
                        "name": "debtor",
                        "description": "Οφειλέτης",
                        "fields": [
                            {
                                "id": "42b2e00c-283f-4ee9-ae9a-90a54ceadea5",
                                "name": "name",
                                "description": "Επωνυμία Πελάτη",
                                "dataType": "string",
                                "dataTypeName": "Αλφαριθμητικό",
                                "length": 70,
                                "precision": 0,
                                "isMandatory": true,
                                "isVisible": true,
                                "isPartOfPaymentRef": false,
                                "partOrder": 0,
                                "fillMethod": null,
                                "fillValue": null,
                                "formatting": null,
                                "formattingExample": null
                            },
                            {
                                "id": "9fe9b85d-dfa0-4735-be0d-97244dd08e49",
                                "name": "telephone",
                                "description": "Τηλέφωνο Πελάτη",
                                "dataType": "string",
                                "dataTypeName": "Αλφαριθμητικό",
                                "length": 20,
                                "precision": 0,
                                "isMandatory": true,
                                "isVisible": true,
                                "isPartOfPaymentRef": false,
                                "partOrder": 0,
                                "fillMethod": null,
                                "fillValue": null,
                                "formatting": null,
                                "formattingExample": null
                            }
                        ],
                        "object": null
                    },
                    {
                        "name": "ultimateDebtor",
                        "description": "Τελικός Οφειλέτης",
                        "fields": [
                            {
                                "id": "ce1507cc-428d-48c4-96ed-3953f1028485",
                                "name": "customerNumber",
                                "description": "Κωδικός Πελάτη",
                                "dataType": "string",
                                "dataTypeName": "Αλφαριθμητικό",
                                "length": 36,
                                "precision": 0,
                                "isMandatory": true,
                                "isVisible": false,
                                "isPartOfPaymentRef": false,
                                "partOrder": 0,
                                "fillMethod": null,
                                "fillValue": null,
                                "formatting": null,
                                "formattingExample": null
                            },
                            {
                                "id": "f22e6a44-f5f1-419c-bbbf-9c5595e91622",
                                "name": "name",
                                "description": "Επωνυμία Πελάτη",
                                "dataType": "string",
                                "dataTypeName": "Αλφαριθμητικό",
                                "length": 70,
                                "precision": 0,
                                "isMandatory": true,
                                "isVisible": false,
                                "isPartOfPaymentRef": false,
                                "partOrder": 0,
                                "fillMethod": null,
                                "fillValue": null,
                                "formatting": null,
                                "formattingExample": null
                            }
                        ],
                        "object": null
                    },
                    {
                        "name": "paymentIdentification",
                        "description": "Μοναδικοποίηση Πληρωμής",
                        "fields": [
                            {
                                "id": "2bb50e53-0159-47a0-9e62-520dd7374f62",
                                "name": "instrId",
                                "description": "Μοναδικός Κωδικός Αναφοράς",
                                "dataType": "string",
                                "dataTypeName": "Αλφαριθμητικό",
                                "length": 36,
                                "precision": 0,
                                "isMandatory": true,
                                "isVisible": false,
                                "isPartOfPaymentRef": false,
                                "partOrder": 0,
                                "fillMethod": null,
                                "fillValue": null,
                                "formatting": null,
                                "formattingExample": null
                            }
                        ],
                        "object": null
                    },
                    {
                        "name": "settlementInfo",
                        "description": "Διακανονισμός",
                        "fields": [
                            {
                                "id": "8f654396-161b-4e2c-bb09-33d9a4e61c51",
                                "name": "method",
                                "description": "Τρόπος Πληρωμής",
                                "dataType": "string",
                                "dataTypeName": "Αλφαριθμητικό",
                                "length": 10,
                                "precision": 0,
                                "isMandatory": true,
                                "isVisible": false,
                                "isPartOfPaymentRef": false,
                                "partOrder": 0,
                                "fillMethod": null,
                                "fillValue": null,
                                "formatting": null,
                                "formattingExample": null
                            },
                            {
                                "id": "323ea7f6-70b3-4e53-ac57-3b866c9ea0bb",
                                "name": "amount",
                                "description": "Ποσό",
                                "dataType": "decimal",
                                "dataTypeName": "Αριθμός",
                                "length": 15,
                                "precision": 2,
                                "isMandatory": true,
                                "isVisible": true,
                                "isPartOfPaymentRef": false,
                                "partOrder": 0,
                                "fillMethod": null,
                                "fillValue": null,
                                "formatting": null,
                                "formattingExample": null
                            },
                            {
                                "id": "515008df-c6ce-4ce4-8f97-835386db17bf",
                                "name": "ccy",
                                "description": "Νόμισμα",
                                "dataType": "string",
                                "dataTypeName": "Αλφαριθμητικό",
                                "length": 3,
                                "precision": 0,
                                "isMandatory": true,
                                "isVisible": false,
                                "isPartOfPaymentRef": false,
                                "partOrder": 0,
                                "fillMethod": null,
                                "fillValue": null,
                                "formatting": null,
                                "formattingExample": null
                            }
                        ],
                        "object": null
                    },
                    {
                        "name": "paymentOrgIdentification",
                        "description": "Μοναδικοποίηση Οργανισμού",
                        "fields": [
                            {
                                "id": "2fd29c48-048a-4976-abbe-c2d968948481",
                                "name": "PAYMENT_CODE",
                                "description": "Κωδικός Πληρωμής",
                                "dataType": "string",
                                "dataTypeName": "Αλφαριθμητικό",
                                "length": 20,
                                "precision": 0,
                                "isMandatory": true,
                                "isVisible": true,
                                "isPartOfPaymentRef": false,
                                "partOrder": 0,
                                "fillMethod": null,
                                "fillValue": null,
                                "formatting": null,
                                "formattingExample": null
                            }
                        ],
                        "object": null
                    },
                    {
                        "name": "remittanceInfo",
                        "description": "Λεπτομέρειες Πληρωμής",
                        "fields": null,
                        "object": {
                            "name": "unstructured",
                            "description": "Χωρίς Δομή",
                            "fields": [
                                {
                                    "id": "3b923ab0-c468-40ec-9299-085d58b6bc5d",
                                    "name": "line",
                                    "description": "Λεπτομέρειες Πληρωμής",
                                    "dataType": "string",
                                    "dataTypeName": "Αλφαριθμητικό",
                                    "length": 140,
                                    "precision": 0,
                                    "isMandatory": false,
                                    "isVisible": false,
                                    "isPartOfPaymentRef": false,
                                    "partOrder": 0,
                                    "fillMethod": null,
                                    "fillValue": null,
                                    "formatting": null,
                                    "formattingExample": null
                                }
                            ],
                            "object": null
                        }
                    }
                ],
                "preprocessSteps": null,
                "objectMappings": null
 }
		]
	}
}           
```
 </details>

 

**It supports much more organizations but for now we use only ΔΗΜΟΣ ΜΑΚΡΑΚΩΜΗΣ**.

**Step2**: Now that you know you support the requested payment, you send the **POST /Payments/commission** request in order to provide your customer with the information about the charging fees for this transaction with **ΔΗΜΟΣ ΜΑΚΡΑΚΩΜΗΣ**.
> https://apis.nbg.gr/public/sandbox/billpayments/v2/Payments/commission

**Request**:
```json
 {
  "header": {
    "ID": "{{$guid}}",
    "application": "{{application_id}}",
    "bank": "{{bank}}",
    "hostSession": null,
    "channel": "{{channel}}",
    "customer": 1,
    "logitude": 1,
    "latitude": 1,
    "go4moreMember": "{{go4moreMember}}",
    "TAN": null
  },
  "payload": {
    "userId": "{{user_id}}",
    "paymentOrgIdentification": {
      "id": "5b60f1c8-243f-4180-8c6b-0130572ee4ba",
      "barcode": null,
      "fields": {
            "PAYMENT_CODE" : "1234567890"
        },
      "extraData": {}
    },
    "settlementInfo": {
        "ccy": "EUR",
        "amount": 31.12,
        "method": "ACCT"
        },
    "requestMachineId": null,
    "machineId": null
  }
}
``` 
**Response** (Contains comission such as total, nbg, merchant's(who provides the app), thirdParty(creator of the app), subAgent(Accountant services) ):
```json
 {
 "payload": {
        "commissionInfo": {
            "total": 0.1,
            "nbg": 0.1,
            "merchant": 0,
            "thirdParty": 0,
            "subAgent": 0
        }
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
``` 
**Step3**: After accomplishing the first two steps, you can execute the payment by using **POST /Payments/pay** request.
> https://apis.nbg.gr/public/sandbox/billpayments/v2/Payments/pay

**Request**:
```json
 {
  "header": {
    "ID": "{{$guid}}",
    "application": "{{application_id}}",
    "bank": "{{bank}}",
    "hostSession": null,
    "channel": "{{channel}}",
    "customer": 1,
    "logitude": 1,
    "latitude": 1,
    "go4moreMember": "{{go4moreMember}}",
    "TAN": null
  },
  "payload": {
    "userId": "{{user_id}}",
    "paymentIdentification": {
      "instrId": "{{$guid}}",
      "endtoendId": null,
      "txId": "{{$guid}}",
      "clrSysRef": null
    },
    "paymentOrgIdentification": {
      "id": "5b60f1c8-243f-4180-8c6b-0130572ee4ba",
      "barcode": null,
      "fields": {
            "PAYMENT_CODE" : "1234567890"
        },
      "extraData": {}
    },
    "chargesInfo": null,
    "settlementInfo": {
      "ccy": "EUR",
      "amount": 31.12,
      "method": "ACCT"
    },
    "debtor": {
      "name": "{{User1Fullname}}",
      "ibUserId": "{{user_id}}",
      "debtorAccount": {
        "iban": "{{User1AccountIBAN}}",
        "pan": null
      },
      "telephone": "{{User1Telephone}}"
    },
    "ultimateDebtor":  null,
    "remittanceInfo": null,
    "requestMachineId": null,
    "acceptDuplicate": true,
    "machineId": null
  }
}
``` 
**Response** (Contains information about the payment the creditor, the creditor bank, the debtor, the settlementInfo and the commissionInfo):
```json
 {
    "payload": {
        "paymentIdentification": {
            "instrId": "b98799b0-3c04-413c-a8b2-2e9ee96ef785",
            "endtoendId": "725428646563",
            "txId": "b98799b0-3c04-413c-a8b2-2e9ee96ef785",
            "clrSysRef": "90906700112820185239",
            "paymentRef": null
        },
        "creditor": {
            "name": "ΔΗΜΟΣ ΜΑΚΡΑΚΩΜΗΣ",
            "creditorAccount": {
                "iban": "GR41654214447695876477",
                "pan": null
            },
            "creditorBank": {
                "bic": "ETHNGRAA",
                "branchId": "700",
                "name": "NATIONAL BANK OF GREECE"
            }
        },
        "debtor": {
            "name": "Antonis Vlamis",
            "debtorAccount": {
                "iban": "GR8979540708770489",
                "pan": null
            },
            "telephone": "6980157548",
            "ibUserId": "e6da8f9c-ee8b-488c-9179-0a566e9d8aed",
            "idType": null
        },
        "settlementInfo": {
            "ccy": "EUR",
            "amount": 31.12,
            "method": "ACCT"
        },
        "commissionInfo": {
            "total": 0.1,
            "nbg": 0.1,
            "merchant": 0,
            "thirdParty": 0,
            "subAgent": 0
        },
        "additional": {
            "ledgerBalance": 100000,
            "availableBalance": 100000,
            "sendCutOffTime": "2018-11-28 18:00:00"
        },
        "tanCheck": null
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
``` 

**Step4**: After payment step you can see the status of that transaction by **POST /Payments/status** or you can cancel it if you want by using 
**POST /Payments/cancelPayment**.

**Note: Remember to use the same payment identification data that pay request gave you as a response.**

**Check Payment Status**
> https://apis.nbg.gr/public/sandbox/billpayments/v2/Payments/status

**Request**:
```json
 {
  "header": {
    "ID": "{{$guid}}",
    "application": "{{application_id}}",
    "bank": "{{bank}}",
    "hostSession": null,
    "channel": "{{channel}}",
    "customer": 1,
    "logitude": 1,
    "latitude": 1,
    "go4moreMember": "{{go4moreMember}}",
    "TAN": null
  },
  "payload": {
    "userId": "{{user_id}}",
    "paymentIdentification": {
         "instrId": "{{instrId}}",
         "endtoendId": "{{endtoendId}}",
         "txId": "{{txId}}",
         "clrSysRef": "{{clrSysRef}}"
    },
    "UltimateDebtor": {
      "name": "string",
      "customerNumber": "string"
    },
    "acceptDuplicate": true,
    "requestMachineId": null,
    "machineId": null
  }
}
``` 
**Response** (Contains information about the payment status):
```json
{
    "payload": {
        "status": "COMPLETED",
        "outboundStatus": "PROCESSED",
        "paymentIdentification": {
            "instrId": "b98799b0-3c04-413c-a8b2-2e9ee96ef785",
            "endtoendId": "725428646563",
            "txId": "b98799b0-3c04-413c-a8b2-2e9ee96ef785",
            "clrSysRef": "90906700112820185239",
            "paymentRef": null
        },
        "sendCutOffTime": null
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
``` 

**Cancel Payment**
> https://apis.nbg.gr/public/sandbox/billpayments/v2/Payments/cancelPayment

**Request**:
```json
 {
  "header": {
    "ID": "{{$guid}}",
    "application": "{{application_id}}",
    "bank": "{{bank}}",
    "hostSession": null,
    "channel": "{{channel}}",
    "customer": 1,
    "logitude": 1,
    "latitude": 1,
    "go4moreMember": "{{go4moreMember}}",
    "TAN": null
  },
  "payload": {
    "userId": "{{user_id}}",
    "requestMachineId": null,
    "cancelPaymentIdentification": {
         "instrId": "{{instrId}}",
         "endtoendId": "{{endtoendId}}",
         "txId": "{{txId}}",
         "clrSysRef": "{{clrSysRef}}"
    },
    "paymentRequest": null,
    "machineId": null
  }
}
``` 
**Response** (Contains information about the payment cancelation):
```json
{
    "payload": {
        "cancellationLimits": [
            {
                "limitType": "REVERSAL",
                "limitTypeInterval": 5,
                "maxCountWithinInterval": 1000,
                "maxAmountWithinInterval": 1000000,
                "usedCountWithinInterval": 1,
                "usedAmountWithinInterval": 31.12,
                "restCountWithinInterval": 999,
                "restAmountWithinInterval": 999968.88
            }
        ],
        "cancelationSucceeded": true,
        "cancellationSucceeded": false,
        "paymentResponse": null,
        "additional": {
            "ledgerBalance": 100000,
            "availableBalance": 100000,
            "sendCutOffTime": ""
        },
        "tanCheck": null
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
``` 
**Note: If you check status again you will see that the transaction was cancelled.**

**Step5**: Also you have the ability to see daily transactions, prefered date transactions or last payment transaction details by using\
**POST /Payments/dailyTransactions** or **POST /Payments/lastPaymentTransactionDetails** respectivelly.

**Check Daily Transactions**
> https://apis.nbg.gr/public/sandbox/billpayments/v2/Payments/dailyTransactions

**Request**:
```json
{
  "header": {
    "ID": "{{$guid}}",
    "application": "{{application_id}}",
    "bank": "{{bank}}",
    "hostSession": null,
    "channel": "{{channel}}",
    "customer": 1,
    "logitude": 1,
    "latitude": 1,
    "go4moreMember": "{{go4moreMember}}",
    "TAN": null
  },
  "payload": {
    "userId": "{{user_id}}",
    "transactionDate": "{{transaction_date}}",
    "paymentRef": null,
    "requestMachineId": null,
    "machineId": null
  }
}
``` 
**Response** (Contains information about all the transactions in a preferred date):
<details><summary>Response</summary>
 
 ``` json
{
    "payload": {
        "transactions": [
            {
                "additional": {
                    "ledgerBalance": null,
                    "availableBalance": null,
                    "sendCutOffTime": "28/11/2018 6:00:00 μμ"
                },
                "paymentOrgIdentification": {
                    "postTransactionData": {},
                    "id": "69d6ffc8-cc65-4130-a172-d2fa16b6cbe8",
                    "barcode": null,
                    "fields": {
                        "PAYMENT_CODE": "90773"
                    },
                    "extraData": {}
                },
                "paymentIdentification": {
                    "instrId": "38450793-1d68-4a60-bed1-313538a1bb01",
                    "endtoendId": "90773001121420176229",
                    "txId": "a76b579d-ed50-4d2b-a053-628247140593",
                    "clrSysRef": "11773001121420176229",
                    "paymentRef": null
                },
                "creditor": {
                    "name": "ΔΕΗ",
                    "creditorAccount": {
                        "iban": "GR41498760953239760",
                        "pan": null
                    },
                    "creditorBank": {
                        "bic": "ETHNGRAA",
                        "branchId": null,
                        "name": "ΕΘΝΙΚΗ"
                    }
                },
                "debtor": {
                    "name": "ΠΑΠΑΔΟΠΟΥΛΟΣ ΓΙΩΡΓΟΣ",
                    "debtorAccount": {
                        "iban": "GR7816570557954408",
                        "pan": null
                    },
                    "telephone": "2101234567",
                    "ibUserId": "acd77e31-a637-48b6-a070-ffc5d1d68e63",
                    "idType": null
                },
                "settlementInfo": {
                    "ccy": "EUR",
                    "amount": 17,
                    "method": "ACCT"
                },
                "commissionInfo": {
                    "total": 0.7,
                    "nbg": 0.2,
                    "merchant": 0.1,
                    "thirdParty": 0.4,
                    "subAgent": 0
                },
                "status": "COMPLETED",
                "timestamp": "2018-11-28T13:39:24.956Z"
            },
            {
                "additional": {
                    "ledgerBalance": null,
                    "availableBalance": null,
                    "sendCutOffTime": "28/11/2018 6:00:00 μμ"
                },
                "paymentOrgIdentification": {
                    "postTransactionData": {},
                    "id": "5b60f1c8-243f-4180-8c6b-0130572ee4ba",
                    "barcode": null,
                    "fields": {
                        "PAYMENT_CODE": "1234567890"
                    },
                    "extraData": {}
                },
                "paymentIdentification": {
                    "instrId": "c97dba0b-02ee-4755-82d4-7b576cceb1bb",
                    "endtoendId": "474813749889",
                    "txId": "c97dba0b-02ee-4755-82d4-7b576cceb1bb",
                    "clrSysRef": "90906700112820185715",
                    "paymentRef": null
                },
                "creditor": {
                    "name": "ΔΗΜΟΣ ΜΑΚΡΑΚΩΜΗΣ",
                    "creditorAccount": {
                        "iban": null,
                        "pan": null
                    },
                    "creditorBank": {
                        "bic": "ETHNGRAA",
                        "branchId": null,
                        "name": "NATIONAL BANK OF GREECE"
                    }
                },
                "debtor": {
                    "name": "Antonis Vlamis",
                    "debtorAccount": {
                        "iban": "GR8979540708770489",
                        "pan": null
                    },
                    "telephone": "6980157548",
                    "ibUserId": "DemoTPP4UsersSpotMachine1",
                    "idType": null
                },
                "settlementInfo": {
                    "ccy": "EUR",
                    "amount": 31.12,
                    "method": "ACCT"
                },
                "commissionInfo": {
                    "total": 0.1,
                    "nbg": 0.1,
                    "merchant": 0,
                    "thirdParty": 0,
                    "subAgent": 0
                },
                "status": "COMPLETED",
                "timestamp": "2018-11-28T13:48:06.678Z"
            },
            {
                "additional": {
                    "ledgerBalance": null,
                    "availableBalance": null,
                    "sendCutOffTime": "28/11/2018 6:00:00 μμ"
                },
                "paymentOrgIdentification": {
                    "postTransactionData": {},
                    "id": "5b60f1c8-243f-4180-8c6b-0130572ee4ba",
                    "barcode": null,
                    "fields": {
                        "PAYMENT_CODE": "1234567890"
                    },
                    "extraData": {}
                },
                "paymentIdentification": {
                    "instrId": "b98799b0-3c04-413c-a8b2-2e9ee96ef785",
                    "endtoendId": "725428646563",
                    "txId": "b98799b0-3c04-413c-a8b2-2e9ee96ef785",
                    "clrSysRef": "90906700112820185239",
                    "paymentRef": null
                },
                "creditor": {
                    "name": "ΔΗΜΟΣ ΜΑΚΡΑΚΩΜΗΣ",
                    "creditorAccount": {
                        "iban": null,
                        "pan": null
                    },
                    "creditorBank": {
                        "bic": "ETHNGRAA",
                        "branchId": null,
                        "name": "NATIONAL BANK OF GREECE"
                    }
                },
                "debtor": {
                    "name": "Antonis Vlamis",
                    "debtorAccount": {
                        "iban": "GR8979540708770489",
                        "pan": null
                    },
                    "telephone": "6980157548",
                    "ibUserId": "DemoTPP4UsersSpotMachine1",
                    "idType": null
                },
                "settlementInfo": {
                    "ccy": "EUR",
                    "amount": 31.12,
                    "method": "ACCT"
                },
                "commissionInfo": {
                    "total": 0.1,
                    "nbg": 0.1,
                    "merchant": 0,
                    "thirdParty": 0,
                    "subAgent": 0
                },
                "status": "CANCELLED",
                "timestamp": "2018-11-28T14:21:30.355Z"
            }
        ]
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
</details>

**Check Last Payment Transaction Details**

> https://apis.nbg.gr/public/sandbox/billpayments/v2/Payments/lastPaymentTransactionDetails

**Request**:
```json
 {
  "header": {
    "ID": "{{$guid}}",
    "application": "{{application_id}}",
    "bank": "{{bank}}",
    "hostSession": null,
    "channel": "{{channel}}",
    "customer": 1,
    "logitude": 1,
    "latitude": 1,
    "go4moreMember": "{{go4moreMember}}",
    "TAN": null
  },
  "payload": {
    "userId": "{{user_id}}",
    "paymentIdentification": {
         "instrId": "{{instrId}}",
         "endtoendId": "{{endtoendId}}",
         "txId": "{{txId}}",
         "clrSysRef": "{{clrSysRef}}"
    },
    "requestMachineId": null,
  "machineId": null
  }
}
``` 
**Response** (Contains information about the transaction that you requested):
```json
{
    "payload": {
        "sendCutOffTime": "2018-11-28T18:00:00.000Z",
        "paymentOrgIdentification": {
            "postTransactionData": {},
            "id": "5b60f1c8-243f-4180-8c6b-0130572ee4ba",
            "barcode": null,
            "fields": {
                "PAYMENT_CODE": "1234567890"
            },
            "extraData": {}
        },
        "paymentIdentification": {
            "instrId": "b98799b0-3c04-413c-a8b2-2e9ee96ef785",
            "endtoendId": "725428646563",
            "txId": "b98799b0-3c04-413c-a8b2-2e9ee96ef785",
            "clrSysRef": "90906700112820185239",
            "paymentRef": null
        },
        "creditor": {
            "name": "ΔΗΜΟΣ ΜΑΚΡΑΚΩΜΗΣ",
            "creditorAccount": {
                "iban": null,
                "pan": null
            },
            "creditorBank": {
                "bic": "ETHNGRAA",
                "branchId": null,
                "name": "NATIONAL BANK OF GREECE"
            }
        },
        "debtor": {
            "name": "Antonis Vlamis",
            "debtorAccount": {
                "iban": "GR8979540708770489",
                "pan": null
            },
            "telephone": "6980157548",
            "ibUserId": "DemoTPP4UsersSpotMachine1",
            "idType": null
        },
        "settlementInfo": {
            "ccy": "EUR",
            "amount": 31.12,
            "method": "ACCT"
        },
        "commissionInfo": {
            "total": 0.1,
            "nbg": 0.1,
            "merchant": 0,
            "thirdParty": 0,
            "subAgent": 0
        },
        "status": "CANCELLED",
        "timestamp": "2018-11-28T14:21:30.355Z"
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
``` 

Created by **NBG**.\
See more at https://developer.nbg.gr/
