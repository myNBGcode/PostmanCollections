# Use case scenario
# Social Network Platform
------------------------------------------------------------------------------------------

### Introduction
The Social Network Platform has been developed with a main functionality in mind, to support any client when connecting people. It enables the administrator to create multiple social networks with members, that can create posts and the members can interact with each other. More specifically, the members can communicate to each other through direct messages and react on the posts and direct messages of other members. All is done through the platform and bellow you will find a full documentation to guide you in detail.

### The API
The Social Network sandbox API provides a standard RESTful interface that enables a user to:
* Become part of a social network
* Get information about:
    * His/Her contacts
    * Posts created by his/her contacts
* Create a post
* Send a direct message to a contact
* React on a post/direct message

> Visit https://developer.nbg.gr/documentation/Social-Network-Application-v2.1
> for the full API documentation.

### Use case scenario

In this scenario we will be using the API to provide data to the *Lost & Found* application.
This application helps users to find items they have lost by asking a large community dedicated to this reason.

#####  Create Sandbox
Before start using the social network sandbox API, we will need to create a Sandbox by making an **HTTP POST** request to the following URL
> https://microsites.nbg.gr/api.gateway/sandbox/socialnetwork/headers/v2/sandbox

With a request body:
```json
 {
   "sandbox_id": "Your_sandbox_id"
 }
``` 

*Note: Remember to store **sandbox_id** somewhere in your application, because you will need to provide it in as a header
in each api call. Also for your ease remember to change your sandbox_id in the enviroment.json provided with this API and the *Client-Id header* with the Client ID provided from your subscription of your application in the Developers Portal site (https://developer.nbg.gr/apiProduct/Social-Network-Platform-v21-962)*

##### Use the Platform
The response contains - among others - a social network. You should store **SocialNetworkId** in your application as we will need it later to access our Social Network. From now on, we will refere to this id as **our_network_id**.

First of all, a user must register to the network in order to be able to interact with others. After asking the user to fill in their desired username, we must make an **HTTP POST** request to

> https://microsites.nbg.gr/api.gateway/sandbox/socialnetwork/headers/v2/[your_sandbox_id]/users

with request body:

```
{
  "username": "[input_username]",
  "isAdmin": false
}
```

with a response as shown below.
```json
{
    "payload": {
        "UserId": "aa75cd60-ef6e-48be-a4ca-881096c83d3c",
        "Username": "[input_username]",
        "ProviderId": "NBG.gr",
        "Provider": "NBG",
        "SocialNetworkId": null,
        "MemberId": null,
        "IsAdmin": false
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
```
Before proceeding, we will store the new UserId - [new_user_id] - and the username - [input_username]. We will need those for the registration process.

As you can see, our new user does not have neither *MemberId* nor *SocialNetworkId*. That's because they are not yet registered. 

The registration proccess continues by asking the user to fill in their personal details.
* First Name ([user_first_name])
* Last Name ([user_last_name])
* Gender ([user_gender])
* Alias ([user_alias])
* Phone Number ([user_phone_number])

After storing the user input, user must accept the terms and conditions of our network. In order to show the terms, we will make an **HTTP POST** request to 

> https://microsites.nbg.gr/api.gateway/sandbox/socialnetwork/headers/v2/UserManagement/declarations

providing our network id as shown below
```json
{
	"payload": {
	    "socialNetworkId": "[our_network_id]"
    }
}
```
The response contains a list of declarations. We will need the ids of all the declarations of type **Terms**.
```json
{
    "payload": {
        "declarations": [
            {
                "declarationId": "8ae414a9-065e-4a8b-beee-dd382a63634f",
                "declarationType": "Terms",
                "description": "Όροι αποδοχής",
                "timestamp": "2018-11-28T16:18:50.851Z",
                "order": 1
            },
            {
                "declarationId": "2405f2e6-5e98-4663-b067-87a9b9a67c3b",
                "declarationType": "Announcement",
                "description": "Ανακοίνωση",
                "timestamp": "2018-11-28T16:18:50.851Z",
                "order": 2
            }
        ]
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
```

In our case, the id of the declaration is **88ae414a9-065e-4a8b-beee-dd382a63634f** and the description which must be show to the user is **Όροι αποδοχής**. When the user accepts terms, we are ready to initiate the registration procces by making an **HTTP POST** request to

> https://microsites.nbg.gr/api.gateway/sandbox/socialnetwork/headers/v2/UserManagement/userRegistration

with request body
```json
{
	"payload": {
	    "socialNetworkId": "[our_network_id]",
	    "Identity": "[user_phone_number]",
	    "IdentityType": "Mobile",
	    "firstName": "[user_first_name]",
	    "lastName": "[user_last_name]",
	    "alias": "[user_alias]",
	    "gender": "[user-gender]",
	    "declarationAcceptance": [
	      {
	        "declarationId": "88ae414a9-065e-4a8b-beee-dd382a63634f",
	        "action": "Accepted"
	      }
    	]
    }
}
```
**Important!!** Do not forget to send the below HTTP Headers
```
user_id: [new_user_id]
username: [input_username]
```

The response of this request contains a verificationId as shown below.
```json
{
    "payload": {
        "verificationId": "5c1248e6-9f13-4c7e-84b7-e6a2a30c7c9b"
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
```

This verification id must be sent to the API along with a verification code in order to complete the registration process.
This is a sandbox API, thus, no sms is sent to the user containing a code. However, our application could prompt the user to fill in a code.

When they do fill in a code, we will make an **HTTP POST** request to 

> https://microsites.nbg.gr/api.gateway/sandbox/socialnetwork/headers/v2/UserManagement/userRegistrationVerification

with a request body
```json
{
	"payload": {
	    "socialNetworkId": "[our_network_id]",
	    "Identity": "[user_phone_number]",
	    "IdentityType": "Mobile",
	    "firstName": "[user_first_name]",
	    "lastName": "[user_last_name]",
	    "alias": "[user_alias]",
	    "gender": "[user-gender]",
	    "verificationId": "5c1248e6-9f13-4c7e-84b7-e6a2a30c7c9b",
	    "verificationCode": "[user_code]",
	    "declarationAcceptance": [
	      {
	        "declarationId": "88ae414a9-065e-4a8b-beee-dd382a63634f",
	        "action": "Accepted"
	      }
    	]
    }
}
```

If the registration process is successful, the reponse should contain the memberId of your newly registered user.
```json
{
    "payload": {
        "memberId": "701d5132-caba-485d-af9f-c675134a6112"
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
```

**Our user is now registered!**

Let's prompt them to create a new post about something they have lost!

Make an **HTTP POST** request to
> https://microsites.nbg.gr/api.gateway/sandbox/socialnetwork/headers/v2/SocialActivities/userPost

with request body:

```json
{
    "socialNetworkId": "[our_network]",
    "memberId": "[member_id]",
    "content": "[user_input]"
}
``` 

The response of a successful post looks like this:
```json
{
    "payload": {
        "success": true
    },
    "exception": null,
    "messages": null,
    "executionTime": 0
}
```

Other users that may know something about the lost item may respond to this post and connect with this user to provide them with additional details.


Created by **NBG**.
See more at https://developer.nbg.gr/
