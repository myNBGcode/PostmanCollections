
# Use case scenario 
# Biometrics API
------------------------------------------------------------------------------------------

### Introduction
The Biometrics Sandbox API has been developed with three main functionalities in mind. It enables us to  compare two images so as to verify if they are the same person and performs a liveness check control in order to check if the person in a recorded video is alive and its not a static photo or image moving, and finally a user frame check that checks and returns the first image(frame) of a person detected from the recorded video.

> The full API documentation: https://developer.nbg.gr/documentation/Biometrics-API-v1

### Use case scenarios
In order to use this API for the first time you will need to create a Sandbox by making an **HTTP POST** request to the following URL
> https://apis.nbg.gr/public/sandbox/biometrics/v1

With a request body:
```json
 {
   "sandbox_id": "Your_sandbox_id"
 }
``` 

*Note: Remember to store the **sandbox_id** somewhere in your application, because you will need to provide it in as a header in each api call. Also for your ease remember to change your sandbox_id in the enviroment.json provided with this API and the *X-IBM-client-id header* with the Client ID provided from your subscription of your application in the Developers Portal site (https://developer.nbg.gr/product/biometrics)*

Once the sandbox is created, proceed with the two scenarios presented below:
##### Airport Face Control Scenario
This use case will showcase a scenario where a passenger passes through flight check control and the security needs to check if the photo in the passenger's identity card is matching the passenger's face by taking a picture of the person.

So we call the *Face-Match* endpoint with **HTTP POST** with request body:
```json
 {
   "image1": "The_identity_card_image_base64",
   "image2": "The_image_of_the_passenger's_face_image_base64",
 }
``` 

Once the call is made the response will return the matching scores between the two images like below:
```json
{
    "matching-score": 90,
    "matching-level": "HighMatch",
    "face-num1": 1,
    "face-num2": 1
}
``` 
##### Remote Customer Onboarding Scenario
This use case will showcase a scenario where a new customer is onboarded in an Application without actually and physically visiting a store/branch to verify his/her identity. 

This procedure consists of two steps. First using the face-match call to check if the person and his identity are a match and as a second step using the liveness-check call in order to check if the person in the video is alive and not impersonating the person in the identity in any way. This procedure will happen in a client using these endpoints and providing the images as base64.

So we call the *Face-Match* endpoint with **HTTP POST** with request body:
```json
 {
   "image1": "The_identity_card_image_base64",
   "image2": "The_image_of_the_passenger's_face_image_base64",
 }
``` 

Then we call the *Liveness-Check* endpoint with **HTTP POST** and a request body with a list of frames ordered ascending by time. For example the 5th frame should not be sent first. All frames should be time-sequenced.

Also note that the specification of the API demands a minimum of 10 frames per second to be sent.
```
 {
   "frames": ["The_first_image_base64","The_second_image_base64",...,"The_nth_image_base64"]
 }
``` 
and as a response will return an object:
```json
{
    "liveness": "Passed",
    "blinked": true,
    "smiled": true,
    "eyebrow-moved": true
}
``` 

So this concludes the use cases for the Biometrics API.

Created by **NBG**.
See more at https://developer.nbg.gr/
