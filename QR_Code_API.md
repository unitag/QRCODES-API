FORMAT: 1A

# QR Code API

This document describes the HTTP interface for accessing Unitag's QR Code API.

## Base URL

The following API routes are relative to this base URL:

```no-highlight
https://admin.unitag.io
```

## API reference

The following HTTP methods allow to manipulate QR Codes as JSON documents.

## Examples

The following example can be used for testing purposes.

### Minimal QR Code example

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
		"creation":"2014",
		"color":"8a9935",
		"eyes":{"shape":"DIAMOND","innerColor":"8a9935", "outerColor":"8a9935"},
		"modules":{"shape":"ROUNDED","correctionLevel":"M"}
	}, 
	"owner":"20"
}
```

## Error handling

When the QR Code API encounters an error, it produces an HTTP response with an appropriate status code (**`4xx`** or **`5xx`**).

When constraints on QR Codes are violated, an automatic error message is generated.
For example:
```json
[PROPERTY]
[eyes.outerColor]
[may not be null]
[null]
```

For any other errors not directly related to the structure of QR Codes, the response will contain a JSON body. This JSON document is always an object with the following keys:
+ `code`: a string identifying the error
+ `message`: a more verbose error description
+ `details`: if present, additional data which could help to figure out the cause of the error

For example, when trying to update a QR Code with an id that doesn't match any QR Code in the database:

```json
{
    "code": "404",
    "message": "This resource cannot be found"
}
```

# QR Code API routes

## QR Code [/newqrcodes/{id}]
This resource represents one particular QR Code identified by its **id**.

+ Parameters
    + id (int) ... ID of the QR Code.

+ Model (application/json)

    ```json
    {
		"id":15448333,
		"content":{"type":"url","url":"http://www.unitag.io","text":null,...},
		"design":
			{
				"id":15448332,
				"creation":1425217249837,
				"color":"8a9935",
				"modules":{"shape":"rounded",...},
				"logo":null,
				...
			}
    }
    ```

### Retrieve a QR Code [GET]
Retrieve a QR Code by its **id**.

+ Response 200

    [QR Code][]

### Create a new QR Code [POST]
Create a new QR Code.

+ Request (application/json)

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
			"creation":"2015",
			"color":"8a9935",
			"eyes":
			{
				"shape":"DIAMOND",
				"innerColor":"8a9935", 
				"outerColor":"8a9935"
			},
			"modules":
			{
				"shape":"ROUNDED",
				"correctionLevel":"M"
			}
		}, 
		"owner":"20"
	}
    ```

+ Response 201

    [QR Code][]

### Update a QR Code [PUT]
Update a QR Code.

+ Request (application/json)

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
			"creation":"2015",
			"color":"8a9935",
			"eyes":
			{
				"shape":"DIAMOND",
				"innerColor":"8a9935", 
				"outerColor":"8a9935"
			},
			"modules":
			{
				"shape":"ROUNDED",
				"correctionLevel":"M"
			}
		}, 
		"owner":"20"
	}
    ```

+ Response 200

    [QR Code][]

### Delete a QR Code [DELETE]
Delete a QR Code. **Warning:** This action **permanently** removes the QR Code from the database.

+ Response 204


## QR Code design [/newqrcodes/design/{id}]
This resource represents a QR Code design identified by its **id**.

+ Parameters
    + id (int) ... ID of the QR Code design.

+ Model (application/json)

    ```json
	{
		"owner":"20",
		"creation":"2014",
		"color":"8a9937",
		"eyes":
		{
			"shape":"DIAMOND",
			"innerColor":"8a9937", 
			"outerColor":"8a9937"
		},
		"modules":
		{
			"shape":"ROUNDED",
			"correctionLevel":"M"
		}
	}
    ```

### Retrieve a QR Code design [GET]
Retrieve a QR Code design by its **id**.

+ Response 200

    [QR Code design][]

### Create a new QR Code design [POST]
Create a new QR Code design.

+ Request (application/json)

    ```json
	{
		"owner":"20",
		"creation":"2014",
		"color":"8a9937",
		"eyes":
		{
			"shape":"DIAMOND",
			"innerColor":"8a9937", 
			"outerColor":"8a9937"
		},
		"modules":
		{
			"shape":"ROUNDED",
			"correctionLevel":"M"
		}
	}
    ```

+ Response 201

    [QR Code design][]

### Update a QR Code design [PUT]
Update a QR Code design.

+ Request (application/json)

    ```json
	{
		"owner":"20",
		"creation":"2014",
		"color":"8a9937",
		"eyes":
		{
			"shape":"DIAMOND",
			"innerColor":"8a9937", 
			"outerColor":"8a9937"
		},
		"modules":
		{
			"shape":"ROUNDED",
			"correctionLevel":"M"
		}
	}
    ```

+ Response 200

    [QR Code design][]

### Delete a QR Code design [DELETE]
Delete a QR Code design. **Warning:** This action **permanently** removes the QR Code design from the database.

+ Response 204


## QR Code graphical PNG representation [/newqrcodes/{id}/png]
This resource is the graphical PNG representation of a QR Code identified by its **id**.

+ Parameters
    + id (int) ... ID of the QR Code.

### Retrieve a QR Code graphical PNG representation [GET]
Retrieve a QR Code graphical PNG representation by its **id**.

+ Response 200 (image/png)


## Zip file containing the graphical PNG representation of a QR Code [/newqrcodes/{id}/zip]
This resource is a zipped file containing a graphical PNG representation of a QR Code identified by its **id**.

+ Parameters
    + id (int) ... ID of the QR Code.

### Retrieve a Zip file containing the graphical PNG representation of a QR Code [GET]
Retrieve a Zip file containing the graphical PNG representation of a QR Code by its **id**.

+ Response 200 (application/zip)


## Zip file containing the graphical PNG representation of multiple QR Codes [/newqrcodes/globalzip{?ids}]
This resource is a zipped file containing a graphical PNG representation of multiple QR Codes identified by their ***ids***.

+ Parameters
    + ids (int) ... IDs of the QR Codes.

### Retrieve a Zip file containing the graphical PNG representation of multiple QR Codes [GET]
Retrieve a Zip file containing the graphical PNG representation of multiple QR Codes by their **ids**.

+ Response 200 (application/zip)

