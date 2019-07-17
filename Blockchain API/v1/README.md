# Blockchain Registry Service API

Welcome to Blockchain Registry Service sandbox API, an API that allows the interaction with NBG's Blockchain Registry Service. 

## Introduction

### About Blockchain Registry Service

NBG is implementing a blockchain solution for storing and retrieving API data. The Blockchain Registry Service will offer the opportunity to any third-party, customer or organization, that uses the Bank's APIs, to store and retrieve their transactions on a private blockchain using smart contracts. For protecting the data and maintain the customer's privacy every transaction that is about to be stored on the blockchain will be transformed, in a one-way manner, to a digest.  A digest is a string of alpharithmetic characters impossible to reverse engineer. These digests will then be stored on the blockchain and can be identifiable by a specific UUID. So, no actual data will be stored on the blockchain, only digests that represent the fingerprints of the API data.

### Business Transaction Definition 

A business transaction is considered an API transaction that contains one or more documents. A document can be any information of the API transaction, from the whole request body to a specific entry. As stated above, to protect the customer's privacy, the transactions that are about to be stored on the blockchain will be transformed in a one-way manner to a digest. To ensure the one-way transformation, salts will be used. Salts are randomly generated strings that go along with each document and each transaction to make the pre-transformed information unique. Afterward, these salts will be used for the verification process.

### Business Logic 
The Blockchain API Registry Service will be built on top of NBG's Open Banking platform. The main goal is to give the capability to NBG's API users, to store their API transactions securely on the blockchain. As seen in the picture below, when a third-party use our APIs, if they want, they can store information from their request and response, either the complete transaction or specific information as documents. By the time the transaction is stored on the blockchain, anyone (API user or not) can serve as a validator and verify a transaction. By using this service, the users are confident that their stored transaction cannot be changed due to the blockchain. Also, it is in the users' hands to decide which part of the information will be stored and under which policies, which information, will be retrieved.

![Blockchain API Registry Service](pictures/blockchain_simple_architecture.PNG)


## Transformation Mechanism 
The transaction that is about to be stored on the blockchain may contain sensitive information. As a result, the information must be transformed in a one-way manner, impossible to reverse engineer. For this reason, every transaction and each sub-document of the transaction will be transformed to a digest (cryptographic hash). Of course, different transactions should have different digests, even if they contain the same data. To ensure the uniqueness of these digests, in every transaction and every document, randomly generated salts will be attached. Afterward, the documents and the transactions will be transformed into digests.

![Transformation Mechanism](pictures/transformation.PNG)


## The Api

This sandbox API will allow its users to perform the following interactions:

1. Query the blockchain-state of a given transaction by using its UUID. A "blockchain-state" can be "received" meaning that the registry service has received the transaction, "submitted" when it has been submitted to the blockchain network, "confirmed" if it has been confirmed on the blockchain network (which is the last step) or "failed" for a failed attempt.

2. Retrieve and then verify a specific business transaction. "Retrieve" means to get the pre-transformed data, while the "Verify" means to get the salts that used to transform the documents to its matching digests along with these digests. So given the salts, you can transform the data yourself, produce a new matching digest and compare it with the digest stored on the blockchain as a proof of existence for the corresponding business transaction.

3. Verify a specific business transaction knowing the data and salt of the transaction. You should parse the UUID of the transaction, all the API data, the salt of the transaction that was used for the transformation and the Smart Contract's name and address.

4. Retrieve and then verify specific documents of a business transaction. You should only ask for particular document names; the rest of the process is similar to operation 2.

5. Verify specific documents of a business transaction by providing the document names, data and corresponding salts. Similarly to operation 3, you should provide the specific documents (names and data) and their corresponding salts. 

### Real Life Use Case Scenario

Suppose that Company A uses checks to pay its partner Company B. In order for A to be consistent with its liabilities, A’s engineers have delegated the task to a software company C which provides an autonomous bot that checks every day, using the Accounts API provided by NBG, the Company’s A balance. If the balance is above 5000 euros the bot ignores the information. However, if the balance is below 5000 euros then the bot raises an alarm and A will transfer money from another account to reach 5000 or more. In that way, A’s partners are confident that will be paid on time using checks. Let’s now examine the case that: at some point in time A’s balance was below 1000. Company C’s bot had checked the balance using the API and for unknown reasons no alarm was raised. At the same day Company B could not liquidate its 2000 euro check and sued A. Using the blockchain solution for APIs, C proved that they had already checked their balance the day of the incident showing that the API call was recorded on the blockchain and no alarm was raised, indicating a remaining balance above 5000. Therefore they could not be aware of the above incident and the court acquitted the charge.

## Getting Started

### Create Sandbox 

Your first job is to create a sandbox and save your sandbox_id in order to be able to interact with the API.

We will create our sandbox by making an HTTP POST request to the following URL:
[https://apis.nbg.gr/sandbox/blockchain/headers/v1/sandbox](https://apis.nbg.gr/sandbox/blockchain/headers/v1/sandbox)

Request Body:
```
 {
   "sandbox_id": "test_blockchain_sandbox"
 }
 ```

**Note: Remember to store sandbox_id somewhere in your application, because you will need to provide it as a header in each api call. Also remember to use the Client-Id provided when you create your application in the portal.**

When you create the sandbox application it has some default data, for our use case example we will use **User1**.

### Request Headers

They are the same in each call so we mention them first, in postman they are stored in each environment variables.

Request Headers:
```
'accept: text/json'
'application_id: {{$guid}}'
'content-type: text/json'  
'Authorization: Bearer your_token'
'sandbox_id: your_sandbox_id'
'Client-Id: your_Client-Id'
```
## Current State of Sandbox Blockchain

In this sandbox environment, we are simulating a blockchain. In this specific blockchain, we have stored many transactions with unique UUIDs. Three of them are transactions that have been confirmed in the blockchain network, one has been submitted but not confirmed and one has been received but not submitted and not confirmed

The UUIDs of the confirmed transactions are:
* ba534cc4-359f-4945-bcb8-1dc2997cb194
* b41ecaa0-009a-44d9-beed-4e533a8f1a5f
* b4143ef3-7dfe-414e-a017-fe9a5f88e672

The UUID of the submitted transaction is:
* 1fcdcedf-fc22-4e14-8be3-ff9a07bc75a8

The UUID of the received transaction is:
* f98a50d3-2ed2-440d-9612-cf7f11bd1c50

