FORMAT: 1A

# QR Code Model

This document describes the JSON model to use for Unitag's QR Code API.

## JSON model

Below is the global structure of a JSON object representing a QR Code:

```json
{
	"content":
	{
		"type":"URL",
		"url":"http://www.unitag.io"
	}, 
	"design":
	{
		"owner":"20",
		"creation":"1426621510629",
		"color":"8a9935",
		"eyes":{"shape":"DIAMOND","innerColor":"8a9935", "outerColor":"8a9935"},
		"modules":{"shape":"ROUNDED","correctionLevel":"M"}
	}, 
	"owner":"20"
}
```

The owner field is used to match an existing user in the PostgreSQL database.
The content object defines what is encoded in the QR Code.
The design object defines the graphical properties of the QR Code.

### Content object

Blahblahblah.

```json
	{
		"type":"URL",
		"url":"http://www.unitag.io"
	}, 
```

For any other errors not directly related to the structure of QR Codes, the response will contain a JSON body. This JSON document is always an object with the following keys:
+ `code`: a string identifying the error
+ `message`: a more verbose error description
+ `details`: if present, additional data which could help to figure out the cause of the error

### Design object

Blahblahblah

    ```json
	{
		"id":15448332,
		"creation":1425217249837,
		"color":"8a9935",
		"modules":{"shape":"rounded",...},
		"logo":null,
		...
	}
    ```
