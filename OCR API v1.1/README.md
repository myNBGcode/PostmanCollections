# Use case scenario
# Welcome to OCR (Optical Character Recognition) Sandbox

### What can I do?

By using the OCR API, any user can get actionable information on various document types.


### How do I get information on the documents the OCR API can recognize?

By using the endpoint _POST_ /ocr/getInfo, the fields of the following document types are extracted: 
-  Passport (issuing countries: Greece, Cyprus, Albania, USA)
-  Greek driving licence
-  Greek ID
-  Greek tax form
-  Greek energy bill (issued by DEH)
-  Greek water bill (issued by EYDAP),


### How do I get the extracted information for a documtn?

Invoke the  _POST_ /ocr/uploadDocument and get the document's recognized data. 


