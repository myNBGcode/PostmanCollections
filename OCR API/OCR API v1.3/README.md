# **Introduction**
#### Welcome to OCR (Optical Character Recognition) Sandbox API.

------------------------------------------------------------------------------------------
### A few words about OCR
Optical character recognition (also optical character reader, OCR) is the mechanical or electronic conversion of images of typed, handwritten or printed text into machine-encoded text, whether from a scanned document, a photo of a document, a scene-photo (for example the text on signs and billboards in a landscape photo) or from subtitle text superimposed on an image (for example from a television broadcast).

> Read more at https://en.wikipedia.org/wiki/Optical_character_recognition

### The API
By using the OCR API, any user can get actionable information on various document types.
This API provides a standard RESTful interface that enables a user to:

* By using the endpoint _POST_ /ocr/getInfo, the fields of the following document types are extracted: 
-  Passport (issuing countries: Greece, Cyprus, Albania, USA)
-  Greek driving licence
-  Greek ID
-  Greek tax form
-  Greek energy bill (issued by DEH)
-  Greek water bill (issued by EYDAP),

* By using the endpoint _POST_ /ocr/uploadDocument in order to get the document's recognized data. 

> Visit https://developer.nbg.gr/documentation/OCR-API-for-Documents-Optical-Character-Recognition-v1.3
> for the full API documentation

### Real life Use Case Scenario
In this scenario we will be using the API to provide data to a *Customer Onboarding* application.

The main functionality of the application is to identify files or images and extract the basic information from them. For example, a user upload his identity, the application "understands" that it is a greek ID and extracts his name, surname and the other ID's details.

First of all, we will create our sandbox by making an **HTTP POST** request to the following URL
> https://apis.nbg.gr/sandbox/ocr/headers/v1.3/sandbox

With a request body:
```
 {
   "sandbox_id": "113E4C18-FA0D-49B7-992E-F90E7CC3922B"
 }
``` 


**Note: Remember to store *sandbox_id* somewhere in your application, because you will need to provide it in as a header
in each api call.**

Created by **NBG**. 
See more at https://www.nbg.gr/ 

