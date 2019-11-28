# Introduction

Welcome to the File Sandbox API.

## Real life Use Case Scenario

### Create your Sandbox

You can create your Sandbox by making an HTTP POST request to the following by simply providing an “id” as your sandbox id and naming it almost anything you like. Moreover you should provide the name (userId) of the user that is going to be created in the default data. The 'userId' must be the same as the username of the logged in user in the NBG Technology Hub.

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/sandbox

With a request body:
```
{
    "sandboxId": "MyUniqueSandboxId",
    "userId": "123456"
}
```
**Note: Remember to store _sandboxId_ somewhere in your application, because you will need to provide it in as a header in each api call.**

### Upload a File

There are only 2 steps in order to upload a file.

1. Initiate an upload request in order to be informed of the size and the number of the chunks that the initial file should be seperated. Initiation could be invoked by making an HTTP POST request to the following URL

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/files/upload-initiation

With a request body:
```
 {
  "requester": {
    "id": 123456,
    "registry": "IBank"
  },
  "subject": {
    "id": 123456,
    "registry": "IBank"
  },
  "folderId": "F9C9E3B1-AC46-4851-AF34-60297EE9300E",
  "fileName": "MyFile.txt",
  "fileDescription": "MyFile",
  "userTags": [
    "MyFile"
  ],
  "fileSize": 8,
  "metadata": {
    "customProperty": "customerPropertyValue"
  },
  "fileIcon": null,
  "needsApproval": false
}
```
The response is a JSON object containing the file id, the number of file chunks and their size, as shown below. 
note: The Sandbox app always return 1 file chunk as a response and accepts 1 chunk to be uploaded by the following operation but the functionality is the same as the production. This is different to the production which can return maney chunks and expects those chunks as described in the step below.
```
{
  "fileId": "F9C9E3B1-AC46-4851-AF34-60297EE9300E",
  "fileChunks": 1,
  "fileChunkSize": 4
}
```

2. Upload the chunks one by one in a chronologically and incremental way as they seperated (Sandbox environment only accepts 1 chunk). Upload can be invoked by making an HTTP PUT request to the following URL. The File identifier is retrieved from the previous step. Let's say there are 2 chunks, the first chunk return an HTTP Status Code 308 Range and the final one returns HTTP Status Code 200 OK which indicates that the operation ended successfully.

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/files/{fileId}/upload

**Note: _{fileId}_ is the fileId returned from the previous step.**

With a request body:
```
{
  "requester": {
    "id": 123456,
    "registry": "IBank"
  },
  "subject": {
    "id": 123456,
    "registry": "IBank"
  },
  "fileContent": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAoHBwgHBgoICAgLCgoLDhgQDg0NDh0VFhEYIx8lJCIfIiEmKzcvJik0KSEiMEExNDk7Pj4+JS5ESUM8SDc9Pjv/2wBDAQoLCw4NDhwQEBw7KCIoOzs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozv/wAARCABpAGkDASIAAhEBAxEB/8QAGgABAQEBAQEBAAAAAAAAAAAAAAUGBAMHAf/EADUQAAEDAwIEBAIIBwAAAAAAAAABAgMEBRESIQYTFDFBUVNhM3EHIiM0gYKRkhUkMkJSscL/xAAaAQEAAgMBAAAAAAAAAAAAAAAAAgMBBAUG/8QALREAAgECAwUGBwAAAAAAAAAAAAECAxEEIWEFEhMxgRQVMnGR8DRBUVJjoeH/2gAMAwEAAhEDEQA/APswAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAOOvqnwNa2PZzvHyQn9ZU+s46br8SP5KRbhXrQdPikqKnnzNi+wZq0Z/ud5InmeU2hXrPFShGTy10N6lGO4m0UesqfWcOsqfWcReJL43hyxz3R8CzthVqctrtKrlyN749yjDIksLJETGtqOx5ZTJo8WuoqW87eZZaN7WOnrKn1nDrKn1nHjnfHio7JnwI9orfe/Vmd2P0PbrKn1nDrKn1nELiG/ssEFJK6nWfqqllOiI/Tp1ePYrknVrqKk5Oz1MWje1inQVckr1ikXVtlFO8kW373+VSuen2XUnUw95u+Zp1klPIAA6RSAAATLr8SP5KYH6QZ5oI7JyZpItdzja7Q5Uym+y48DfXX4kfyUhXSzUN4SnStidIlNMk0eHq3D07Lt3PJYqcYY6Upcv4b0E3SsjH8eVt1qeDrxHX2lKKGN8fJl6hsnN+1TwTttuc09vZw1euGK63XCqmmucrYalssyvSoY5Ey7Htn/Rsr1DaLrQ1FtuT0fD9VZY2uVFTCo5O2/kcNo4a4Yt9zjrbbSfzCszG7L3tjRU8M7Nzv5EaeIjGlutNc8ksndJfN9Q4Ny5mN4gWK7Ul5vlspKvFHM5EuMlwcxWPaqbRsTw7YTbuU4qV3EfHslLX1VT0rrTDNJBFKrGvcunuieGVyWarhLhN89bLLROVZlXnI1ZFZqcuFVqJtq38N0yUKSislJdVuNO7FStK2Hma3K1Y2oionlnGlfPC5JyxMVC0E+Ttpy1008jCg75nzaaeobwsyma59R0PEfJp2yPyulN0blfdTYcATPun8Qu1dVyyXJ87opqZyqjaVEXZiN/Dv7fMoN4c4ce7oWxuVz6rr9PMfvLlUzn5tXb2Uow2G3U98mvMMTo6ydmiVzXqjXp7t7Z2TcjXxNOcHFJpv3+zMYNO5ctv3v8AKpXJFt+9/lUrnY2R8N1ZRX8YAB1igAAA4blA+RGvYiu07KiE3lSem79qmgBycTsuFeo6m9a5fCs4q1jKy2ennkfJJTOV8mdTvrJnZqf8N/T3EVoghkjkjp5GrGmG7ux4p2/FTVAp7nytxH76kuPoZSSzU8sj3yUrn8z+prsq1d0Xt27oh+rZ4V1ZhlVHN0qiud/ijc9++ERM99jVAdz/AJH76jj6GYhtscEnMjp3a9CM1qiquEVV7r7uX9T35Unpu/apoARexYvnN+g7RoTbbTyNlWVzVamMJnxKQB1cNh44enuRdymc3N3YABskAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD/2Q==",
  "chunkPart": 1
}
```

Between and after the above steps you can be informed about the status of the operation by making an HTTP GET request to the following URL:

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/files/{fileId}

The response is a JSON object containing the file metadata, as shown below.
```
{
  "fileId": "F9C9E3B1-AC46-4851-AF34-60297EE9300E",
  "fileName": "MyFile.txt",
  "createdOn": "2018-02-08",
  "updatedOn": "2018-02-08",
  "createdByUserId": 123456,
  "createdByUserRegistry": "IBank",
  "updatedByUserId": 123456,
  "updatedByUserRegistry": "IBank",
  "fileSize": 8,
  "chunksUploaded": 2,
  "totalChunks": 2,
  "fileDescription": "MyFile",
  "userTags": [
    "MyFile"
  ],
  "systemTags": [
    "EthnofileSystemResponse"
  ],
  "status": "Completed",
  "statusReason": null,
  "metadata": {
    "customProperty": "customerPropertyValue"
  },
  "fileIcon": null
}
```

### Download a File

A file can be downloaded by providing the file identifier and the chunk number one by one. The total chunks of a file can be retrieved by making an HTTP GET request as shown in the previous step. Let's say a file is seperated in 2 chunks, make an HTTP GET request to the following URL, 2 times by specifying the same fileId and chunk parts one by one (first 1 and then 2). 

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/files/{fileId}/{chunkPart}

The response is a JSON object containing the file chunk part content, as shown below.
```
{
  "fileContent": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAoHBwgHBgoICAgLCgoLDhgQDg0NDh0VFhEYIx8lJCIfIiEmKzcvJik0KSEiMEExNDk7Pj4+JS5ESUM8SDc9Pjv/2wBDAQoLCw4NDhwQEBw7KCIoOzs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozv/wAARCABpAGkDASIAAhEBAxEB/8QAGgABAQEBAQEBAAAAAAAAAAAAAAUGBAMHAf/EADUQAAEDAwIEBAIIBwAAAAAAAAABAgMEBRESIQYTFDFBUVNhM3EHIiM0gYKRkhUkMkJSscL/xAAaAQEAAgMBAAAAAAAAAAAAAAAAAgMBBAUG/8QALREAAgECAwUGBwAAAAAAAAAAAAECAxEEIWEFEhMxgRQVMnGR8DRBUVJjoeH/2gAMAwEAAhEDEQA/APswAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAOOvqnwNa2PZzvHyQn9ZU+s46br8SP5KRbhXrQdPikqKnnzNi+wZq0Z/ud5InmeU2hXrPFShGTy10N6lGO4m0UesqfWcOsqfWcReJL43hyxz3R8CzthVqctrtKrlyN749yjDIksLJETGtqOx5ZTJo8WuoqW87eZZaN7WOnrKn1nDrKn1nHjnfHio7JnwI9orfe/Vmd2P0PbrKn1nDrKn1nELiG/ssEFJK6nWfqqllOiI/Tp1ePYrknVrqKk5Oz1MWje1inQVckr1ikXVtlFO8kW373+VSuen2XUnUw95u+Zp1klPIAA6RSAAATLr8SP5KYH6QZ5oI7JyZpItdzja7Q5Uym+y48DfXX4kfyUhXSzUN4SnStidIlNMk0eHq3D07Lt3PJYqcYY6Upcv4b0E3SsjH8eVt1qeDrxHX2lKKGN8fJl6hsnN+1TwTttuc09vZw1euGK63XCqmmucrYalssyvSoY5Ey7Htn/Rsr1DaLrQ1FtuT0fD9VZY2uVFTCo5O2/kcNo4a4Yt9zjrbbSfzCszG7L3tjRU8M7Nzv5EaeIjGlutNc8ksndJfN9Q4Ny5mN4gWK7Ul5vlspKvFHM5EuMlwcxWPaqbRsTw7YTbuU4qV3EfHslLX1VT0rrTDNJBFKrGvcunuieGVyWarhLhN89bLLROVZlXnI1ZFZqcuFVqJtq38N0yUKSislJdVuNO7FStK2Hma3K1Y2oionlnGlfPC5JyxMVC0E+Ttpy1008jCg75nzaaeobwsyma59R0PEfJp2yPyulN0blfdTYcATPun8Qu1dVyyXJ87opqZyqjaVEXZiN/Dv7fMoN4c4ce7oWxuVz6rr9PMfvLlUzn5tXb2Uow2G3U98mvMMTo6ydmiVzXqjXp7t7Z2TcjXxNOcHFJpv3+zMYNO5ctv3v8AKpXJFt+9/lUrnY2R8N1ZRX8YAB1igAAA4blA+RGvYiu07KiE3lSem79qmgBycTsuFeo6m9a5fCs4q1jKy2ennkfJJTOV8mdTvrJnZqf8N/T3EVoghkjkjp5GrGmG7ux4p2/FTVAp7nytxH76kuPoZSSzU8sj3yUrn8z+prsq1d0Xt27oh+rZ4V1ZhlVHN0qiud/ijc9++ERM99jVAdz/AJH76jj6GYhtscEnMjp3a9CM1qiquEVV7r7uX9T35Unpu/apoARexYvnN+g7RoTbbTyNlWVzVamMJnxKQB1cNh44enuRdymc3N3YABskAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD/2Q=="
}
```

### Update File Metadata

Update file metadata by making an HTTP PUT request to the following url. Only the values that are not null in the request body are used to update the metadata of the file. A null value indicates that the particular metadata key should remain unchanged.

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/files/{fileId}/upload

With a request body:
```
{
  "requester": {
    "id": 123456,
    "registry": "IBank"
  },
  "subject": {
    "id": 123456,
    "registry": "IBank"
  },
  "fileName": "File.txt",
  "userTags": [
    "PersonalFile"
  ],
  "fileDescription": "My File Updated",
  "fileIcon": null,
  "folderId": null,
  "useFolderId" : false
}
```
### Delete a File

Delete a file by making an HTTP DELETE request to the following URL:

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/files/{fileId}

### Share a File

Share a file with another user,specifying his permissions on the file, by making an HTTP PUT request to the following URL:

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/files/{fileId}/share/{sharedUserRegistry}/{sharedUserId}

**Note: _{sharedUserRegistry}_ and _{sharedUserId}_ are the values of the shared user registry and id.**

With a request body: 
```
{
  "requester": {
    "id": 123456,
    "registry": "IBank"
  },
  "subject": {
    "id": 123456,
    "registry": "IBank"
  },
  "permissions": {
    "canView": true,
    "canEditMetadata": true,
    "canMove": true,
    "canDelete": true,
    "canShare": true
  }
}
```

### Revoke Share of File
A file share is revoked from an external user by making an HTTP DELETE request to the following url. The access cannot be revoked to the user that created it.

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/files/{fileId}/share/{sharedUserRegistry}/{sharedUserId}

### Get File List

The user file list is returned alongside the files that are shared, by making an HTTP GET request to the following URL:

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/files

The user and filtering values are specified in the header values :
```
Requester, with format 'registry:id'
Subject, with format 'registry:id'
Offset, used for pagination, indicates response items start from position x, default 0
Limit, limit the number of response items, default 20
FolderId, Folder identifier
DateFrom, File Date criteria (Format yyyy-MM-ddTHH:mm:ss.fffZ)
DateTo, File Date criteria (Format yyyy-MM-ddTHH:mm:ss.fffZ)
UserTags, User custom tag, used like a hashtag
SystemTags, System tag e.g. EthnofileSystemResponse
```

The response is a JSON object containing the file list, as shown below.
```
[
  {
    "fileId": "260401BD-F941-405E-9096-7D23CE696DB5",
    "fileName": "file.txt",
    "createdOn": "2018-02-08",
    "updatedOn": "2018-02-08",
    "createdByUserId": 123456,
    "createdByUserRegistry": "IBank",
    "updatedByUserId": 123456,
    "updatedByUserRegistry": "IBank",
    "fileSize": 10,
    "chunksUploaded": 3,
    "totalChunks": 3,
    "fileDescription": "My uploaded file description",
    "userTags": [
      "PersonalFile"
    ],
    "systemTags": [
      "EthnofileSystemResponse"
    ],
    "status": "Completed",
    "statusReason": null,
    "metadata": {
      "customProperty": "customerPropertyValue"
    },
    "fileIcon":null
  }
]
```

### Create a Folder

Create a folder by making an HTTP POST request to the following URL:

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/folders

With a request body :
```
{
  "requester": {
    "id": 123456,
    "registry": "IBank"
  },
  "subject": {
    "id": 123456,
    "registry": "IBank"
  },
  "folderName": "Folder A",
  "folderDescription": "Folder for my files",
  "folderIcon": null,
  "parentFolderId": null
}
```

The response is a JSON object containing the folder id, as shown below.
```
{
  "folderId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

### Update a Folder

Update a folder by making an HTTP PUT request to the following url. Only the filled values are used.

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/folders/{folderId}

With a request body :
```
{
  "requester": {
    "id": 123456,
    "registry": "IBank"
  },
  "subject": {
    "id": 123456,
    "registry": "IBank"
  },
  "folderName": "Folder A",
  "folderDescription": "Folder for my files updated",
  "folderIcon": null,
  "parentFolderId": null
}
```

### Delete a Folder

Delete a folder by making an HTTP DELETE request to the following URL. Be careful the containing files are deleted also!

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/folders/{folderId}

### Share a Folder

Share a folder with another user,specifying his permissions on the folder, by making an HTTP PUT request to the following URL:

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/folders/{folderId}/share/{sharedUserRegistry}/{sharedUserId}

**Note: _{sharedUserRegistry}_ and _{sharedUserId}_ are the values of the shared user registry and id.**

With a request body :
```
{
  "requester": {
    "id": 123456,
    "registry": "IBank"
  },
  "subject": {
    "id": 123456,
    "registry": "IBank"
  },
  "permissions": {
    "canAdd": true,
    "canView": true,
    "canEditMetadata": true,
    "canMove": true,
    "canDelete": true,
    "canShare": true
  }
}
```

### Revoke Share of Folder
A folder share is revoked from an external user by making an HTTP DELETE request to the following url. The access cannot be revoked to the user that created it.

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/folders/{folderId}/share/{sharedUserRegistry}/{sharedUserId}

### Get Folder List
Get the The created/shared folder list for a user by making an HTTP GET request to the following URL:

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/folders

The user is specified in the header values :
```
Requester, with format 'registry:id'
Subject, with format 'registry:id'
```

The response is a JSON object containing the folder list, as shown below.
```
[
  {
    "folderId": "848EEC71-D283-4B55-97E4-7ED33FB3315E",
    "folderName": "Folder A",
    "folderDescription": "Folder for my files",
    "createdOn": "2018-02-02",
    "updatedOn": "2018-02-02",
    "createdByUserId": 123456,
    "createdByUserRegistry": "IBank",
    "updatedByUserId": 123456,
    "updatedByUserRegistry": "IBank",
    "folderIcon": null,
    "subFolders": {
      "folderId": "4ACEC3F1-5064-463D-BC80-48F15677B83C",
      "folderName": "Folder B",
      "folderDescription": "Subfolder for my files",
      "createdOn": "2018-02-02",
      "updatedOn": "2018-02-02",
      "createdByUserId": 123456,
      "createdByUserRegistry": "IBank",
      "updatedByUserId": 123456,
      "updatedByUserRegistry": "IBank",
      "folderIcon": null,
      "subFolders": null
    }
  }
]
```
### Send a File from File API to Ethnofiles System

Send a file stored in the File API to Ethnofiles by making an HTTP POST request to the following url.

> https://apis.nbg.gr/sandbox/file/oauth2/v2.1/files/SendFileToEthnofiles

With a request body:
```
{
    "header":{
		"id":"guid",
		"application":"client_id"
	},
    "payload": {
        "fileApiFileId": "80000006-0000-fc00-b63f-84710c7967bb",
        "userId": "",
        "fileTypeId": "",
        "rowCount": "",
        "totalSum": "",
        "tanNumber": "",
        "locale": "",
        "inboxId": "",
        "xactionId": "",
        "isSmsOtp": "",
        "convId": "",
        "xmlFileField": "",
        "debtorName": "",
        "debtorIBAN": "",
        "fileId": "",
        "acceptTerms": "",
        "acceptTrnTerms": ""
}
```

Created by **NBG**. See more at https://developer.nbg.gr/
