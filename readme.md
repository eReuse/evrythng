A walkthrough over the Evrything API

Regarding the EVRYTHNG environment, what follows describes a walkthrough over the API mainly using the command line interface (CLI) and ‘curl’ commands, exploring the relationship with the eReuse platform.
Using the web interface we created different keys (removed some characters for security reasons) that were used below:
$ apiKey=W4ET08RCmgdjR5V28UutOuehVyxtr...
$ name=ereuse
$ region=eu
$ evrythng operators add $name $region $apiKey

Welcome to the EVRYTHNG CLI!

To get started, please provide the following to set up your first account Operator:

Short Operator name (e.g: 'personal'): test
Account region ('us' or 'eu'): eu
Operator API Key (from 'Account Settings' in the EVRYTHNG Dashboard'): W4ET08RCmgdjR5V28UutOuehVyxtrLIzBLgGQ6dCzoI...

$ OPERATOR_API_KEY=W4ET08RCmgdjR5V28UutOuehVyxtrLIzBLgGQ6dCzoI...

And register an application and obtain an application API key:

$ APPLICATION_API_KEY=1Wek8nKyPOQtbcH0YhCRGHQdtlOsso8Hr...

And create a (my) user account:

$ curl -H "Content-Type: application/json"   -H "Authorization: $APPLICATION_API_KEY"   -X POST 'https://api.evrythng.com/auth/evrythng/users'   -d '{  "firstName": "Leandro", "lastName": "Navarro", "email": "leandro@ereuse.org", "password": "upcD6105" }'

{"evrythngUser":"UKp9ffAnmwxD9xRRamKny...","activationCode":"LtYD8hHk","status":"inactive","email":"leandro@ereuse.org"}

And validate that user:

$ curl -H "Content-Type: application/json" -H "Authorization: $APPLICATION_API_KEY" -X POST 'https://api.evrythng.com/auth/evrythng/users/UKp9ffAnmwxD9xRRamKnybdt/validate' -d '{ "activationCode": "LtYD8hHk" }'
{"status":"active","evrythngUser":"UKp9ffAnmwxD9xRRamKny...","evrythngApiKey":"6c2Ok0lwFtxvrfIPMqkbzghi5NpNAF5PsZMLwKi..."}

We obtain an API key that we save in the local environment:

$ evrythngApiKey=6c2Ok0lwFtxvrfIPMqkbzghi5NpNAF5PsZMLwKiIIKFff0z5...

For instance we can create a product (a model or class of objects):

$ evrythng products create '{"name":"Computer_Desktop_LENOVO_7220W3T","id":3155,"description":"Computer Desktop LENOVO 7220W3T devices:Ready","categories":["Computer","Desktop","LENOVO","7220W3T"],"identifiers":{"serial":"S4WV089","model":"7220W3T","price":84.4},"brand":"LENOVO","fn":"Computer Desktop LENOVO 7220W3T"}' --project UH2TsYwhegPw9pRwaX...

Products follow the h-product microformat http://microformats.org/wiki/h-product
According to the definition, h-product is a simple, open format for publishing product data on the web. h-product is one of several open microformat draft standards suitable for embedding data in HTML.

#One of the possible computer types:

Computer_ProductID=Up5pcpVk3MNrHUaawpBsBqVm

One instance of the previous product:
curl -H "Content-Type: project=UH2TsYwhegPw9pRwaXndssXb' -d '{ "name": "Computer HZBA #43879", "description": "A single board desktop computer", "product": "Up5pcpVk3MNrHUaawpBsBqVm" }'
{"id":"UKp9CG4gXHmExnawR2FM2rfc","createdAt":1539266982239,"updatedAt":1539266982239,"name":"Computer HZBA #43879","description":"A single board desktop computer","product":"Up5pcpVk3MNrHUaawpBsBqVm"}

Now we add more product (types):
curl -H "Content-Type: appoject=UH2TsYwhegPw9pRwaXndssXb' -d '{ "name": "Computer HZBA #43879", "description": "A single board desktop computer", "product": "Up5pcpVk3MNrHUaawpBsBqVm" }'
{"id":"UKp9CG4gXHmExnawR2FM2rfc","createdAt":1539266982239,"updatedAt":1539266982239,"name":"Computer HZBA #43879","description":"A single board desktop computer","product":"Up5pcpVk3MNrHUaawpBsBqVm"}

curl -H "Content-Type: application/json" -H "Authorization: $APPLICATION_USER_API_KEY … project=UH2TsYwhegPw9pRwaXndssXb' -d '{ "name": "Computer HZBA #43878", "description": "A single board desktop computer", "product": "Up5pcpVk3MNrHUaawpBsBqVm" }'
{"id":"Up59C3tppXHbddwRaFhRGg2s","createdAt":1539267067157,"updatedAt":1539267067157,"name":"Computer HZBA #43878","description":"A single board desktop computer","product":"Up5pcpVk3MNrHUaawpBsBqVm"}

Creating an item (thng as an instance of a product class):

curl -H "Content-Type: application/json" -H "Authorization: $APPLICATION_USER_API_KEY" -X POST 'https://api.evrythng.com/thngs?project=UH2TsYwhegPw9pRwaXndssXb' -d '{ "name": "Computer HZBA #43877", "description": "A single board desktop computer", "product": "Up5pcpVk3MNrHUaawpBsBqVm" }'
{"id":"U5KtC4a9CTHC9TwRwk5bkfgs","createdAt":1539267087859,"updatedAt":1539267087859,"name":"Computer HZBA #43877","description":"A single board desktop computer","product":"Up5pcpVk3MNrHUaawpBsBqVm"}

$ curl -H "Content-Type: application/json" -H "Authorization: $APPLICATION_USER_API_KEYoject=UH2TsYwhegPw9pRwaXndssXb' -d '{ "name": "Computer HZBA #43877", "description": "A single board desktop computer", "product": "Up5pcpVk3MNrHUaawpBsBqVm" }'
{"id":"U5ptCHbThMbrYKRawGtkYFng","createdAt":1539267090467,"updatedAt":1539267090467,"name":"Computer HZBA #43877","description":"A single board desktop computer","product":"Up5pcpVk3MNrHUaawpBsBqVm"}

curl -H "Content-Type: application/json" -H "Authorization: $APPLICATION_USER_API_KEYoject=UH2TsYwhegPw9pRwaXndssXb' -d '{ "name": "Computer HZBA #43876", "description": "A single board desktop computer", "product": "Up5pcpVk3MNrHUaawpBsBqVm" }'
{"id":"Up5QWnTB3EwVQDRwR2hMkmpf","createdAt":1539267108998,"updatedAt":1539267108998,"name":"Computer HZBA #43876","description":"A single board desktop computer","product":"Up5pcpVk3MNrHUaawpBsBqVm"}

In a particular project:

$ PROJECT=UH2TsYwhegPw9pRwaXndssXb

We create a collection of devices:

$ curl -H "Content-Type: application/json" -H "Authorization: $APPLICATION_USER_API_ons?project=UH2TsYwhegPw9pRwaXndssXb' -d '{ "name": "pangea circuit lot #1223", "description": "A lot of several laptops" }'

{"id":"U5KQCqQMQbVgrBRaakkFUbqn","createdAt":1539267836010,"updatedAt":1539267836010,"name":"pangea circuit lot #1223","description":"A lot of several laptops"}

$ COLLECTION_ID=U5KQCqQMQbVgrBRaakkFUbqn

We create a list of items (thngs) in that collection:

$ curl -H "Content-Type: application/json" -H "Authorization: $APPLICATION_USER_API_KEY" -X PUT 'https://api.evrythng.com/collections/U5KQCqQMQbVgrBRaakkFUbqn/thngs' -d '[ "UKp9CG4gXHmExnawR2FM2rfc", "Up59C3tppXHbddwRaFhRGg2s", "U5KtC4a9CTHC9TwRwk5bkfgs", "U5ptCHbThMbrYKRawGtkYFng", "Up5QWnTB3EwVQDRwR2hMkmpf" ]'
{"id":"U5KQCqQMQbVgrBRaakkFUbqn","createdAt":1539267836010,"scopes":{"users":["UKp9ffAnmwxD9xRRamKnybdt"],"projects":["UH2TsYwhegPw9pRwaXndssXb"]},"updatedAt":1539267836010,"name":"pangea circuit lot #1223","description":"A lot of several laptops"}

And we list the items (thngs) in that collection:

$ curl -H "Authorization: $APPLICATION_USER_API_KEY" -X GET 'https://api.evrythng.com/collections/U5KQCqQMQbVgrBRaakkFUbqn/thngs'

[{"id":"Up5QWnTB3EwVQDRwR2hMkmpf","createdAt":1539267108998,"updatedAt":1539268176443,"name":"Computer HZBA #43876","description":"A single board desktop computer","product":"Up5pcpVk3MNrHUaawpBsBqVm","properties":{},"collections":["U5KQCqQMQbVgrBRaakkFUbqn"]},{"id":"U5ptCHbThMbrYKRawGtkYFng","createdAt":1539267090467,"updatedAt":1539268176443,"name":"Computer HZBA #43877","description":"A single board desktop computer","product":"Up5pcpVk3MNrHUaawpBsBqVm","properties":{},"collections":["U5KQCqQMQbVgrBRaakkFUbqn"]},{"id":"U5KtC4a9CTHC9TwRwk5bkfgs","createdAt":1539267087859,"updatedAt":1539268176443,"name":"Computer HZBA #43877","description":"A single board desktop computer","product":"Up5pcpVk3MNrHUaawpBsBqVm","properties":{},"collections":["U5KQCqQMQbVgrBRaakkFUbqn"]},{"id":"Up59C3tppXHbddwRaFhRGg2s","createdAt":1539267067157,"updatedAt":1539268176443,"name":"Computer HZBA #43878","description":"A single board desktop computer","product":"Up5pcpVk3MNrHUaawpBsBqVm","properties":{},"collections":["U5KQCqQMQbVgrBRaakkFUbqn"]},{"id":"UKp9CG4gXHmExnawR2FM2rfc","createdAt":1539266982239,"updatedAt":1539268176443,"name":"Computer HZBA #43879","description":"A single board desktop computer","product":"Up5pcpVk3MNrHUaawpBsBqVm","properties":{},"collections":["U5KQCqQMQbVgrBRaakkFUbqn"]}]

Products (classes) and thngs (instances) have identifiers, and these identifiers can be read (scanned)
 

EPCIS and Core Business Vocabulary (CBV)

https://www.gs1.org/standards/epcis

EPCIS is a GS1 standard that enables trading partners to share information about the physical movement and status of products as they travel throughout the supply chain – from business to business and ultimately to consumers. It helps answer the “what, where, when and why” questions to meet consumer and regulatory demands for accurate and detailed product information.

GS1 standards for traceability
What, when, where, how? In fact GS1 covers aspects to achieve interoperability, visibility and automation, through standards about identification (codes: global trade item number, container GTIN, locations: GLN), capture and sharing (keys, GDSN, eCom, EPCIS).

In fact, GS1 covers multiple aspects as the figure (from GS1) shows:



Places:

Places and locations are relevant to eReuse, as events may have a context related to places (a real-world location where a product or thing may be interacted with) and locations (the point where an item is or an action happened). Evrythng uses the GeoJSON Point specification (RFC 7946) and the address data type. 
However, eReuse uses a GeoJSON Polygon to represent a valid area of the perimeter of a recycling center.

We can create some relevant places:

$ evrythng places create --build

Provide values for each field (or leave blank to skip):

1/10: name (string): USE1_PLACE
2/10: description (string): Place of user 1
3/10: customFields (object, leave 'key' blank to finish)
  key: 
4/10: tags (comma-separated list of string): 
5/10: identifiers (object, leave 'key' blank to finish)
  key: 

Provide values for each field of [object Object] (or leave blank to skip):

7/10: icon (string): 

Provide values for each field of [object Object] (or leave blank to skip):


9/10: longitude (number): 1.2
10/10: latitude (number): 3.2

{
  "id": "UK6AYSwmmEaVtXwww2kaxk9k",
  "createdAt": 1539535113775,
  "customFields": {},
  "updatedAt": 1539535113775,
  "name": "USE1_PLACE",
  "description": "Place of user 1",
  "position": {
    "type": "Point",
    "coordinates": [
      1.2,
      3.2
    ]
  },
  "address": {},
  "identifiers": {},
  "latitude": 3.2,
  "longitude": 1.2
}

$ evrythng places create --build

Provide values for each field (or leave blank to skip):

1/10: name (string): USE2_PLACE
2/10: description (string): Place of user 2
3/10: customFields (object, leave 'key' blank to finish)
  key: 
4/10: tags (comma-separated list of string): 
5/10: identifiers (object, leave 'key' blank to finish)
  key: 

Provide values for each field of [object Object] (or leave blank to skip):


7/10: icon (string): 

Provide values for each field of [object Object] (or leave blank to skip):


9/10: longitude (number): 1.23
10/10: latitude (number): 4.23

{
  "id": "UK6dYbTFH9Ns7pwaRFNC2sAq",
  "createdAt": 1539535144923,
  "customFields": {},
  "updatedAt": 1539535144923,
  "name": "USE2_PLACE",
  "description": "Place of user 2",
  "position": {
    "type": "Point",
    "coordinates": [
      1.23,
      4.23
    ]
  },
  "address": {},
  "identifiers": {},
  "latitude": 4.23,
  "longitude": 1.23
}

Summary
The different elements of the Evrythng API and service is a good infrastructure for eReuse. 

eReuse has:
    • Methods and software tools to extract data from computer-based electronic devices (computers such as desktops and laptops, bootable with our Linux-based tools) that can extract detailed component data (characteristics, serial numbers) and perform related actions (erasure, health or stress checks) [workbench in eReuse].
    • Methods, software tools and services to link/map extracted data about devices to unique identifiers (for product items: products and thngs in Evrythng terminology) that can be represented as RFID tags, eTags, or QR codes. [Box in eReuse]
    • Methods, software tools and services to keep track of an inventory of devices, and related events [DeviceTag/Hub] implemented as a repository (here is where the Evrythng API and service can be used as a basis of a store for this information. 

Furthermore, the Evrythng API and service supports additional features like actions, interaction with web applications (such as external mobile or web apps that interact with the API/service), auth (OAuth, etc). 


