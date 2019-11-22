# Use case scenario
#### Welcome to the Crowdfunding Sandbox API.
------------------------------------------------------------------------------------------

### What is Crowdfunding
Crowdfunding is a method of raising capital through the collective effort of friends, family, customers, and individual investors. This approach taps into the collective efforts of a large pool of individuals—primarily online via social media and crowdfunding platforms—and leverages their networks for greater reach and exposure.
> Read more at https://en.wikipedia.org/wiki/Crowdfunding

### The API
This API provides an interface that enables a user to create a fully functional crowdfunding application. The main entities of the API are the following:

#####  Thematic areas
Thematic areas are categories of actions. Each thematic area has one or more actions.

#####  Actions
Action is the main entity of the crowdfunding platform. It belongs to a thematic area and it has properties like 
* Name
* Starting date
* Ending date
* Amount from donations

##### Donation promises
Is the promise that a registered user will pay the amount he promised for a specific action. Donation promise can be paid either by credit/debit card or by deposit.

##### Content for actions
Each action has one or more contents to display. For example the description of an action is content.

> Visit https://developer.nbg.gr/documentation/Crowdfunding-API-v1 for the full API documentation

### Real life Use Case Scenario
Let's say that we want to create an application in which end users will make donations to two actions. The first action named 'Therapy dogs' has the purpose to raise €8000 in order to provide animal assisted therapy. The second action is the 'Help me go to school' and has the purpose to raise €30000 in order to purchase a specialy modified school bus for people with cerebral palcy.

Before starting developing our application, we should create our sandbox. Replace the **sandbox_id** with your desired value. 
> POST https://apis.nbg.gr/public/sandbox/crowdfunding/v1/sandbox
With a request body:
```
 {
    "sandbox_id": "crowdfunding-app"
 }
``` 
**Note: Remember to store *sandbox_id* somewhere in your application, because you will need to provide it in as a header
in each api call.**

When you create the sandbox application it has some default data.
#### **Request Headers**
They are the same in each call so we mention them first, in postman they are stored in each environment variables.

**Request Headers**:
```
 'accept: text/json'
 'content-type: text/json'
 'provider: NBG'
 'provider_id: NBG.gr'
 'sandbox_id: your_sandbox_id' !!!payforme is the one that we used to create the use case sandbox, you can also use it to see the results!!!
 'user_id: e6da8f9c-ee8b-488c-9179-0a566e9d8aed'
 'username: User1'
 'x-ibm-client-id: your_x-ibm-client-id' !!!c33f6acf-5ef1-4d00-b801-058eaa4ad0ed is the one that we got from creating a test app at the portal, you can also use it to see the results!!!
```

#### **Scenario Requests**
The first action named '**Therapy dogs**' is autocreated together with the creation of the sandbox. This means that they have been created for the specific action: thematic area, donations, content and everything else a developer needs to create an application.

In order a user to create the second action named '**Help me go to school**' has to do the following steps:

**Step1**: Create action by calling the **POST /backoffice/actions** request.
>https://apis.nbg.gr/public/sandbox/crowdfunding/v1/backoffice/actions

**Body Request**:
```json
{
  "actionName": "Help me go to school",
  "accountKey": "ece26104-ce1b-4c2d-829b-5d01dd921f48",
  "cardsAccountKey": "e2554977-c1d1-47c0-8c9b-f493a2a88263",
  "dateStart": "2018-12-01T10:10:00.042Z",
  "dateEnd": "2019-12-31T16:10:00.042Z",
  "offsetAmount": 0,
  "targetAmount": 30000,
  "merchantDataId":"",
  "publicAmount": 0
}
```
**Response** (Returns the created action):
```json
{
    "payload": {
        "actionData": {
            "accountKey": "ece26104-ce1b-4c2d-829b-5d01dd921f48",
            "cardsAccountKey": "e2554977-c1d1-47c0-8c9b-f493a2a88263",
            "offsetAmount": 0,
            "merchantDataId": "",
            "actionDataId": "2a76d3a7-7fb8-4642-ae52-e8c9f90cbb4e",
            "actionShortName": "Action_helpmegotoschool",
            "actionName": "Help me go to school",
            "dateStart": "2018-12-01T10:10:00.042Z",
            "dateEnd": "2019-12-31T16:10:00.042Z",
            "targetAmount": 30000,
            "status": "Active",
            "publicAmount": 0
        }
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
```
**Step2**: Create a donation for the action by calling the **POST /action/actions/{actionId}/donations** request. The **actionId** parameter must be replaced by the actionDataId from the previous endpoint response.
>https://apis.nbg.gr/public/sandbox/crowdfunding/v1/action/actions/2a76d3a7-7fb8-4642-ae52-e8c9f90cbb4e/donations

**Body Request**:
```json
{
  "payType": "Card",
  "publish": true,
  "xpAmount": 1000,
  "displayName": "From NBG"
}
```
**Response** (Returns the created donation promise):
```json
{
    "payload": {
        "donationPromise": {
            "donationPromiseId": "6990e095-77a0-4455-9671-316b8027bf33",
            "actionKey": "69034932-ff37-4243-aa2c-3e7c05908d83",
            "categoryMoneyFound": "",
            "donationTime": "2018-11-28T16:29:37.2786183Z",
            "payType": "Card",
            "publish": true,
            "theChallenge": "20353630",
            "transactionKey": "",
            "transactionReceiptKey": "",
            "userKey": "4735c448-bf3c-4d54-a81b-f5a95f116165",
            "xpAmount": 1000,
            "status": "Pending",
            "displayName": "From NBG"
        }
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
```

**Step3**: Make the payment of the donation in order to change the donation status from pending to paid. To do that call the  **POST /action/actions/{actionId}/donations/{donationPromiseId}/datacash** request. The **donationPromiseId** parameter must be replaced by the response from the previous call.
>https://apis.nbg.gr/public/sandbox/crowdfunding/v1/action/actions/2a76d3a7-7fb8-4642-ae52-e8c9f90cbb4e/donations/6990e095-77a0-4455-9671-316b8027bf33/datacash

**Body Request**:
```json
{
    "amount": 1000,
    "cardProduct": {
        "type": "card",
        "number": "5278900020308586",
        "details": {
            "cvv": "843",
            "cardHolder": "Επωνυμία Επιχ.",
            "expiryDate": "01/20"
        }
    }
}
```
**Response** (If the status is '1' and the reason is 'ACCEPTED' then the payment was successful):
```json
{
    "payload": {
        "datacashReference": "3400900031089253",
        "status": 1,
        "reason": "ACCEPTED",
        "threeDSecure": null
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
```

**Step4a**: Content for the action. When you created the action it also created a content for the action. In order to get all contents for the specific action call the **GET /cmscontent/tags/en/{actionShortName}**. The value of the **actionShortName** in our case is 'Action_helpmegotoschool'.

>https://apis.nbg.gr/public/sandbox/crowdfunding/v1/cmscontent/tags/en/Action_helpmegotoschool

**Response** (Returns list of nodes that belongs to action):
```json
{
    "payload": [
        {
            "nid": "1013",
            "title": "Help me go to school"
        }
    ],
    "exception": null,
    "messages": null,
    "executionTime": 0
}
```

**Step4b**: Change the autogenerated content with yours. To do that call **PUT  sandbox/{sandbox_id}/cmscontent/article/{nodeId}**. The **sandbox_id** is the one you entered in the create sandbox call and the **nodeId** is the **nid** from the response of the previous call. In our case the nodeid is '1013'.

>https://apis.nbg.gr/public/sandbox/crowdfunding/v1/sandbox/crowdfunding-app/cmscontent/article/1013

**Body Request**:
```json
{
  "title": "HELP ME GO TO SCHOOL",
  "body": "Cerebral Palsy Greece/Open Door believes in the unique values of people with cerebral palsy (CP). Over the years, the company has supported people with CP so as to enable them to develop, as fully as possible, their experiences and physical skills.  Cerebral Palsy Greece/Open Door (CPG) is a recognized non-profit charity established in 1972 with a mission to provide welfare for people suffering from CP in Greece.",
  "summary": "Cerebral Palsy Greece/Open Door believes in the unique values of people with cerebral palsy (CP). Over the years, the company has supported people with CP so as to enable them to develop, as fully as possible, their experiences and physical skills.",
  "image" : {
  	"alt": "SCHOOL image",
  	"title": "Image title",
  	"url" : "https://www.nbg.gr/Style%20Library/images/logo.png"
  }
}
```

**Response** (Returns the result of the update):
```json
{
    "payload": {
        "result": true
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
```


**FINALLY**
* In order to get the details of the action you created call **GET /action/actions/{actionId}**
https://apis.nbg.gr/public/sandbox/crowdfunding/v1/action/actions/2a76d3a7-7fb8-4642-ae52-e8c9f90cbb4e

* In order to get the **content** of the action you created call **GET /cmscontent/content/en/{contentId}**
https://apis.nbg.gr/public/sandbox/crowdfunding/v1/cmscontent/content/en/1013

* In order to get the public donations for all actions call **GET /action/donations/wall**
https://apis.nbg.gr/public/sandbox/crowdfunding/v1/action/donations/wall

* In order to get the public donations for the action you created call **GET /action/actions/{actionId}/donations**
https://apis.nbg.gr/public/sandbox/crowdfunding/v1/action/actions/2a76d3a7-7fb8-4642-ae52-e8c9f90cbb4e/donations


Congratulations you have create a functional crowdfunding application



Created by **NBG**.
See more at https://developer.nbg.gr/




