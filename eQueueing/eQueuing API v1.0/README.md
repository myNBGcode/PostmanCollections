 
# EQueueing API
------------------------------------------------------------------------------------------

### Introduction
The eQueueing API provides information about branches and ATMs. It also manages tickets for a branch, which means that someone can issue a ticket for a branch remotely from his way to the branch.

> The full API documentation: https://developer.nbg.gr/documentation/eQueuing-Sandbox-API-v1

### Use case scenario
In this scenario, we are going to use the API in order to provide data to the *WeFixDevices eServices* mobile application.

*WeFixDevices* is a company with many branches throughout the country that provides repairing services for electrical devices. Their main advantage is that someone can go to their store and have their device repaired in front of them! The company is proud about their service times and really appreciates their customer's feedback.

With this application, the company wants to allow their customers to issue tickets to their closest branch and, thus, save valuable waiting time.

##### Create Sandbox
In order to use this API for the first time you will need to create a Sandbox by making an **HTTP POST** request to the following URL
> https://apis.nbg.gr/public/sandbox/equeueing/v1/sandbox

With a request body:
```
 {
   "sandbox_id": "Your_sandbox_id"
 }
``` 

*Note: Remember to store **sandbox_id** somewhere in your application, because you will need to provide it in as a header
in each api call. Also for your ease remember to change your sandbox_id in the enviroment.json provided with this API and the *X-IBM-client-id header* with the Client ID provided from your subscription of your application in the Developers Portal site (https://developer.nbg.gr/product/social-network-platform-0)*

When a customer uses the application for the first time, a **deviceId** will be generated and stored for them. This is going to be used to identify them in all their tickets.

The application will ask the user to fill in the maximum range in kilometers that suits them and will store the user input multiplied by 1000 to [required_max_distance_meters].

Then it will make an **HTTP POST** request to
> https://apis.nbg.gr/public/sandbox/equeueing/v1/api/EQueueing/nearestBranches

with request body
```
{
  "payload": {
    "distance": [required_max_distance_meters]],
    "latitude": [device_lat],
    "longitude": [device_long],
    "userId": "1533"
  }
}
```

In order to fill in [device_lat] and [device_long] the application must have permission to access the device's location.

The response contains a list of brances that match the user's criteria.
```
{
    "payload": {
        "distance": 10000,
        "branches": [
            {
                "code": "080",
                "latitude": 37.9805317,
                "longitude": 23.7312227,
                "area": 24,
                "nameGR": "ΟΔ. ΣΤΑΔΙΟΥ  38",
                "nameEN": "STADIOU 38 ST.",
                "addressGR": "Σταδίου 38",
                "addressEN": "38,  Stadiou str.",
                "zipCodePart1": "105",
                "zipCodePart2": "64",
                "phoneAreaCode": "210",
                "phoneNumber": "3345512",
                "distance": null,
                "areaNameGR": "ΑΘΗΝΑ - ΚΕΝΤΡΟ",
                "areaNameEN": "ATHENS CENTER"
            }
        ]
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
```

The application will preview the branches and prompt the user to select one in order to view the queue details.

When the user selects one, an **HTTP POST** request will be made to
> https://apis.nbg.gr/public/sandbox/equeueing/v1/api/EQueueing/queueInfo

the response of which will contain the current queue information about the branch.
```
{
    "payload": {
        "code": "080",
        "canIssue": true,
        "isClosed": false,
        "canShowTimes": true,
        "meanWaitingTime": 1466,
        "meanWaitingTimeNew": 1466,
        "currentTicketNumber": "2",
        "waitingCustomers": 2,
        "opensAt": "2018-11-29T06:10:00.000Z",
        "closesAt": "2018-11-29T12:25:00.000Z",
        "timeNow": "2018-11-29T08:24:27.178Z",
        "openSaturday": true,
        "openSunday": true,
        "activeTellers": 2,
        "openTellers": 3,
        "longestWaitingTimes": 30000,
        "meanServiceTime": 58,
        "hasAppointments": false
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
```

According to the response, the application will show the data to the user to help him take his final decision.

When the user decides to issue a ticket to this branch, they will press the "Issue Ticket" button in the branch details screen. After filling in a description about their electronic device and its problem, they will press the "Submit" button.
This will trigger and **HTTP POST** request to
> https://apis.nbg.gr/public/sandbox/equeueing/v1/api/EQueueing/issueTicket

with request body:
```
{
  "payload": {
    "branchCode": "[selected_branch_code]",
    "reason": "General",
    "comments": "[customer_comments]",
    "deviceId": "[device_id]",
    "pushNotificationId": "string",
    "pushNotificationType": "Android",
    "lang": "en"
  }
}
```

The response contains details about the ticket:
```
{
    "payload": {
        "id": "e9f0ce8e-af23-46d0-bba3-629635eef4d6",
        "number": "3",
        "issueDate": "2018-09-15T13:06:28.711Z",
        "issueBranchCode": "080",
        "issueBranchNameGR": "ΟΔ. ΣΤΑΔΙΟΥ  38",
        "issueBranchNameEN": "STADIOU 38 ST.",
        "branchDetails": {...}
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
```

which the application must store.

Customer can now take their time, using all the provided data, to bring their device to their closest branch and receive the fastest service, with the smallest possible waiting time.

Created by **NBG**.
See more at https://developer.nbg.gr/
