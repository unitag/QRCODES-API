#QR Code API#

##Request##

The API base URL is: `http://api.qrcode.unitag.fr/api`

A QR Code API request is based on these following primary parameters:

##Parameters##

###t_pwd (required)
Provide the authentication for your account.

Values:
- To obtain a token please create an account on Unitag's platform and contact the Unitag Team.
- You can set `degraded` as value for tests (the answer received will be limited to a PNG format image of 200px size).

###T (optional)
Change the image format received.

Values: `SVG`, `PDF`, `PNG`, `JPEG`.

###stored (optional)
Store the QR Code in your Unitag Dashboard.

Values: If needed, set value to `true`.

###SIZE (optional)
Change the image size in pixels.

Values : integer between 0 and 3,000

###setting (required)
Send custom parameters to your QR Code design.

The setting parameter value is JSON formated and contains all QR Code customizations parameters. See description and examples below

Can be replaced by the templateId parameter.

###data (required)
Send QR Code data.

The data parameter value is JSON formated and contains all QR Code encoded data. See description and examples below.

###templateId (optional)
The parameter templateId can replace the parameter setting in order to indicate a Unitag Template to use as a design.

Values : If needed, set value to the targeted template id Integer.


##Data object##

	data = {
		"TYPE" : "",
		"DATA" : {}
	}

###"Type" - STRING###

* url
* text
* geoloc
* smsto
* wifi
* vcard
* email
* calendar
* call

###"data" - OBJECT###

**Type : url**

	data = {
		"TYPE" : "url",
		"DATA" : {
			"URL" : ""
		}
	}

**Type : text**

	data = {
		"TYPE" : "text",
		"DATA" : {
			"TEXT" : ""
		}
	}

**Type : geoloc**

	data : {
		"TYPE" : "geoloc",
		"DATA" : {
			"LAT" : "",
			"LONG" : ""
		}
	}

**Type : smsto**

	data = {
		"TYPE" : "smsto",
		"DATA" : {
			"TEL" : "",
			"MESSAGE" : ""
		}
	}

**Type : wifi**

	data = {
		"TYPE" : "wifi",
		"DATA" : {
			"TYPE" : "WEP"/"WPA"/"nopass",
			"SSID" : "",
			"PASSWORD" : ""
		}
	}
	
**Type : vcard**

	data = {
		"TYPE" : "vcard",
		"DATA" : {
			"FIRSTNAME" : "",
			"NAME" : "",
			"EMAIL;INTERNET" : "",
			"EMAIL;HOME;INTERNET" : "",
			"TEL;CELL" : "",
			"TEL;WORK" : "",
			"TEL;HOME" : "",
			"URL" : "",
			"TITLE" : "",
			"ORG" : "",
			"ADR" : "",
			"PC" : "",
			"CITY" : "",
			"COUNTRY" : ""
		}
	}
	

**Type : email**

	data = {
		"TYPE" : "email",
		"DATA" : {
			"EMAIL" : "",
			"EMAIL_OBJ" : "",
			"EMAIL_CORPS" : ""
		}
	}

**Type : calendar**

	data = {
		"TYPE" : "calendar",
		"DATA" : {
			"TITLE" : "",
			"LIEU" : "",
			"DATE_DEBUT" : "",
			"DATE_FIN" : ""
		}
	}
*LIEU : Place ; DATE_DEBUT : Start date ; DATE_FIN ; End date*
	
**Type : call**

	data = {
		"TYPE" : "call",
		"DATA" : {
			"PHONE" : ""
		}
	}


##Setting object##

	setting = {
		"LAYOUT" : {},
		"EYES" : {},
		"LOGO" : {},
		"BACKGROUND" : {},
		"E" : "",
		"BODY_TYPE" : INT,
		"ARRONDI" : INT,
		"QUIET_ZONE" : BOOLEAN
	}

*ARRONDI : Radius*
	
###LAYOUT - OBJECT###

	LAYOUT : {
		"GRADIENT_TYPE" : "",
		"COLOR1" : "",
		"COLOR2" : "",
		"RAYON" : INT,
		"X1" : INT,
		"Y1" : INT,
		"X2" : INT,
		"Y2" : INT,
		"COLORBG" : "",
		"COLOR_SHADOW" : "",
		"X_SHADOW" : INT,
		"Y_SHADOW" : INT,
		"FORCE_SHADOW" : ""
	}
	
**GRADIENT_TYPE - STRING - mandatory**

* From up to down : "HORI"
* From left to right: "VERT"
* Diagonal top left to bottom right: "DIAG1"
* Diagonal bottom left to top right: "DIAG2"
* Radial outward from the center: "RADI"
* Linear without repeating the pattern, setting requires two distinct points of start and end: "LIN_ACY"
* Linear with pattern repeat, requires setting two distinct points of start and end: "LIN_CYC"
* Without repetition of the pattern ,requires setting a starting point and a radius: "RAD_ACY"
* With repetition of the pattern, requires setting a starting point and a radius x1: "RAD_CYC"

**COLORBG**

Can be transparent

**FORCE_SHADOW**

Strength of the shadowing.

_Note: FORCE_SHADOW is a shortcut for X_SHADOW/Y_SHADOW_

* "L" : Low (value is 5)
* "M" : Medium (value is 7)
* "S" : Strong (value is 10)


###EYES###

	"EYES" : {
		"COLOR_EHG" : "",
		"COLOR_EHD" : "",
		"COLOR_EBG" : "",
		"COLOR_IHG" : "",
		"COLOR_IHD" : "",
		"COLOR_IB" : "",
		"EYE_TYPE" : ""
	}

**EYE_TYPE**

* Square: "Simple"
* Diamond: "Diamond"
* Roundness: "ER_IC"
* Roundess "ER_IR"
* True circle "ES_IC"
* Right circle "LLRight"
* Left eye: "LLLeft"
* Shield "Shield"
* Cushion "SFLeaves"
* Star "SFLeavesC"
* Leaf "Spike"
* Sieve: "Turned"
* Dots: "S_Circle"
* Wave "Wave"
* Sharp "Sharp"
* Curved "ECurve_ICurve"
	
###LOGO###
	
	"LOGO" : {
		"L_NAME" : "",
		"L_X_Norm" : FLOAT,
		"L_Y_Norm" : FLOAT,
		"L_WIDTH" : FLOAT,
		"L_LENGTH" : FLOAT,
		"EXCAVATE" : BOOLEAN
	}

**L_X_Norm & L_Y_Norm**

The upper corner of the logo in the QR Code as a percentage. Omit to have it centered.


###BACKGROUND###

	"BACKGROUND" : {
		"IMAGE_BACKGROUND" : "",
		"ENLIGHTMENT" : FLOAT,
		"CONTRAST" : FLOAT
	}

**ENLIGHTMENT & CONTRAST - float**

0 <= x <= 2	
		
###E - STRING###

QR Code redundancy : 

* Low : "L"
* Medium : "M"
* Quality : "Q"
* Strong : "H"

###BODY_TYPE - INT###

Modules look : 

* Square : 0
* Light roundness : 1 ("ARRONDI" required)
* Medium roundness : 1 ("ARRONDI" required)
* Strong roundness : 1 ("ARRONDI" required)
* Sieve : 2
* Angular : 3
* Painting : 4
* Dots : 5
* Arrow : 6
* Classy : 7
* Rectangular : 8


###ARRONDI - INT###

0 <= x <= 10

###TEXT###

Use this module to add text under the QR Code

	"TEXT" : {
		"LABEL" : String,
		"COLOR" : 000000,
		"SIZE" : int,
		"POSITION" : -,
		"STYLES" : -,
		"FAMILY" : -,
		"FAMILYLINK" : String,
		"QRMARGIN" : int,
		"SPACING" : int
	}
	
		
* LABEL : put \n for new lines		
* POSITION : CENTER, LEFT, RIGHT or AUTO ( ie resize to take maximum space beneath the QR Code )
* STYLES : PLAIN, BOLD, ITALIC, TOTAL ( BOLD+ITALIC )
* FAMILY : Have a look at our font catalog, or CUSTOM
* FAMILYLINK : only if FAMILY is CUSTOM, a link to a .TTF or .OTF file containing the family you wish to use
* QRMARGIN : space between the QR Code and the text
* SPACING : space in between two lines of text
