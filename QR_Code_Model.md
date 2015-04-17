FORMAT: 1A

# QR Code Model

This document describes the JSON model to use for Unitag's QR Code API.

## JSON model

Below is the global structure of a JSON object representing a QR Code:

```json
{
	"content":
	{
		...
	}, 
	"design":
	{
		...
	}, 
	"owner":"20"
}
```

+ `owner` is used to match an existing user in the PostgreSQL database.
+ `content` defines what is encoded in the QR Code.
+ `design` defines the graphical properties of the QR Code.

### Content object

The content object defines the data encoded in the QR Code and can only be one of the following types: TEXT, URL, CALL, GEOLOC, SMS, WIFI, VCARD, EMAIL, EMAIL, CALENDAR, CALL.

#### TEXT
```json
{
	"type":"TEXT",
	"text":"Hello World"
}
```
#### URL
```json
{
	"type":"URL",
	"url":"http://www.unitag.io"
}
```
#### GEOLOC
```json
{
	"type":"GEOLOC",
	"geoloc":
	{
		"latitude":"43-36-16.2N",
		"longitude":"1-26-38.4E"
	}
}
```
#### SMS
```json
{
	"type":"SMS",
	"sms":
	{
		"tel":"+33970805343",
		"message":"Hello World"
	}
}
```
#### WIFI
```json
{
	"type":"WIFI",
	"wifi":
	{
		"security":"WPA",
		"ssid":"unitag_WIFI",
		"password":"your_password_here"
	}
}
```
#### VCARD
```json
{
	"type":"VCARD",
	"vcard":
	{
		"firstname":"Romain",
		"lastname":"Kassel",
		"emailwork":"romain.kassel@unitag.io",
		"emailhome":"romain.kassel@gmail.com",
		"telcell":"+33970805341",
		"telwork":"+33970805342",
		"telhome":"+33970805343",
		"telfax":"+33970805344",
		"website":"http://www.unitag.io",
		"title":"CIO",
		"organization":"Unitag",
		"address":"67 allées Jean Jaurès",
		"postalcode":"31000",
		"city":"Toulouse",
		"country":"France"
	}
}
```
#### EMAIL
```json
{
	"type":"EMAIL",
	"email":
	{
		"to":"romain.kassel@unitag.io",
		"cc":"contact@unitag.io",
		"bcc":"other@my-company.com",
		"subject":"test",
		"body":"Hello World"
	}
}
```
#### CALENDAR
```json
{
	"type":"CALENDAR",
	"calendar":
	{
		"title":"AGM",
		"location":"Unitag - 67 allées Jean Jaurès 31000 Toulouse",
		"start":"10/02/2015 09:00",
		"end":"10/02/2015 12:00"
	}
}
```
#### CALL
```json
{
	"type":"CALL",
	"call":
	{
		"phone":"+33970805343"
	}
}
```

### Design object

The design object contains all the graphical properties and modifications that define and can be applied to a QR Code image. Its structure is the following:
```json
{
	"owner":20,
	"color":"007FB6",
	"modules":
	{
		...
	},
	"eyes":
	{
		...
	},
	"logo":
	{
		...
	},
	"background":
	{
		...
	},
	"quietZone":true
}
```
Fields `color`, `modules` and `eyes` are always mandatory, `owner` is only mandatory when persisting a design entity. By default there is no `logo`, no `background` and `quietZone` is set to true.

#### MODULES
This object defines the graphical properties of the modules of a QR Code.
```json
{
	"shape":"DRIFTED",
	"roundness":"5",
	"correctionLevel":"M",
	"image":
	{
		"url":"https://static-unitag.com/file/freeqr/671f9c9974bf42694ee4eca41be358b5.jpg",
		"enlightment":"60.7987",
		"contrast":"0.58"
	},
	"gradient":
	{
		"color":"c41200",
		"type":"RAD_CYC",
		"x1":"50",
		"y1":"50",
		"radius":"30"
	}
}
```
+ `shape` is mandatory and defines the shape applied to all the QR Code modules. Possible values are: NORMAL, ROUNDED, ROUNDED_LIGHT, ROUNDED_MEDIUM, ROUNDED_STRONG, SHAKED, DISTORTED, MELTED, DOTS, ARROWS, CURVED, DRIFTED, TICTACTOE, CIRCUIT_BOARD, CRYSTAL.
+ `roundness` can be used to specify the rounded effect strength of the ROUNDED shape. Use integer values between 0 and 10. No need to specify a roundness value for shapes ROUNDED_LIGHT, ROUNDED_MEDIUM and ROUNDED_STRONG since they come with a default value. 
+ `correctionLevel` is also mandatory and specifies the correction level to use when creating the QR Code. With a high correction level, more modules are needed to encode the same data. Possible values are: L (low), M (medium), Q (quartile), H (high).
+ `gradient` defines a color gradient that can be applied to the QR Code modules (see section below).
+ `image` indicates an image to be overlayed on the the QR Code modules (see section below).

Warning: do not specify a gradient and an image at the same time.

##### GRADIENT
Available fields to define a gradient are:
```json
{
	"color":"C41200",
	"type":"LIN_ACY",
	"x1":"0",
	"y1":"0",
	"x2":"250",
	"y2":"250"
	"radius":"20"
}
```
+ `color` is the second color used to create the color gradient (the first one being the main design color). This field is mandatory
+ `type` defines the color gradient type. This field is mandatory and all possible values are listed below.
+ `x1` and `y1` are coordinates (from the top left corner) used to specify a starting point when needed for some of the gradients
+ `x2` and `y2` are coordinates (from the top left corner) used to specify a second point when needed for some of the gradients
+ `radius` is needed for some of the gradients

Different `type` values are available:
+ HORI defines a horizontal gradient
+ VERT defines a vertical gradient
+ DIAG1 defines a gradient along the first QR Code diagonal
+ DIAG2 defines a gradient along the second QR Code diagonal
+ RAD defines a radial gradient from the center of the QR Code
+ LIN_ACY defines a linear gradient (needs 2 points)
+ LIN_CYC defines a cyclic linear gradient (needs 2 points)
+ RAD_ACY defines a radial gradient (needs a center point and a radius)
+ RAD_CYC defines a cyclic radial gradient (needs a center point and a radius)

##### IMAGE
Available fields to define an image are:
```json
{
	"url":"https://static-unitag.com/file/freeqr/671f9c9974bf42694ee4eca41be358b5.jpg",
	"brightness":"60.7987",
	"contrast":"0.58"
}
```
+ `url` is the only mandatory field. It should contain a URL where the image can be found. If the URL is invalid or if the image can't be read, the default background color will be used instead.
+ `brightness` defines the image brightness (use positive values to brighten the image and negative values to darken it, we recommend using values between -100.0 and 100.0 where the changes are most visible)
+ `contrast` defines the image contrast (positive values expected, we recommend using values between 0.0 and 2.0 where the changes are most visible)

#### EYES
This object defines the graphical properties of the 3 eyes of a QR Code.
```json
{
	"shape":"SPIKE",
	"innerColor":"007FB6",
	"outerColor":"CC0099",
	"topRight":
	{
		"innerColor":"8A9935"
	},
	"topLeft":
	{
		"innerColor":"8A9935",
		"outerColor":"C41200"
	},
	"bottom":
	{
		"outerColor":"C41200"
	}
}
```
+ `shape` is the only mandatory field and defines the shape of the eyes. Possible values are: DIAMOND, CIRCLE, CIRCLE_ROUNDED, ROUNDED, CURVED, CIRCLE_SQUARE, LEAVES_TL, LEAVES_TR, SPIKE_TL, SPIKE_TR, SPIKE_BL, SPIKE_BR, SPIKE, SHIELD, STAR, ROUNDEDSTAR, CURVEDSTAR, NORMAL, SHAKED, DOTS, DISTORTED, WAVE, TICTACTOE, OCTOGON, ALIEN and GRID.
+ `innerColor` defines the color to use for the inner part of an eye (defaulted to the design's global color).
+ `outerColor` defines the color to use for the outer part of an eye (defaulted to the design's global color).
+ `topRight` is used to overwrite the color values for the top right eye.
+ `topLeft` is used to overwrite the color values for the top left eye.
+ `bottom` is used to overwrite the color values for the bottom eye.

#### LOGO
Use the `logo` object to add an image on the QR Code.

Structure:
```json
{
	"url":"https://static-unitag.com/file/freeqr/671f9c9974bf42694ee4eca41be358b5.jpg",
	"width":"0.2",
	"height":"0.2",
	"leftOffset":"0.4",
	"topOffset":"0.6",
	"excavate":"true"
}
```

+ `url` is the only mandatory field. It should contain a URL where the logo image can be found. By default the logo is placed at the center of the image and `excavate` is set to true.
+  `width` is used to specify the width of a logo when not using the default positioning. It works like a percentage of the QR Code image width.
+  `height` is used to specify the height of a logo when not using the default positioning. It works like a percentage of the QR Code image height.
+  `leftOffset` is used to specify where to place the logo from the left edge when not using the default positioning. It works like a percentage of the QR Code image width.
+  `topOffset` is used to specify where to place the logo from the top edge when not using the default positioning. It works like a percentage of the QR Code image height.
+  `excavate` tells the generator whether to remove the QR Code modules behind the logo. If set to true (by default), the modules behind the logo are removed and this makes the QR Code look better. If set to false, the logo is simply placed on the QR Code but can partially hide some of the modules.

#### BACKGROUND
`background` can be set to either define a background color or a shadow.

Background color:
```json
{
	"color":"FFCC00"
}
```
QR Code shadow:
```json
{
	"shadow":
	{
		"color":"BDBDBD",
		"strength":"M"
	}
}
```
There are 3 different values for the field `strength` field which defines the strength of the shadow: `L` (light), `M` (medium), `S` (strong).
