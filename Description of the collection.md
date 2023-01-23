## Methods:

## ```POST``` - **Add new place**

### Base URL: https://rahulshettyacademy.com

### Endpoint: /maps/api/place/add/json

### Params

<table>
  <tbody>
    <tr>
      <th>№</th>
      <th>KEY</th>
      <th>VALUE</th>
    </tr>
    <tr>
      <td>1</td>
      <td>key</td>
      <td>qaclick123</td>
    </tr>
  </tbody>
</table>

### Example HTTP-request

```HTTP 
POST /maps/api/place/add/json?key=qaclick123 HTTP/1.1
Host: rahulshettyacademy.com
Content-Type: application/json
Content-Length: 308
```
###### Body raw (JSON)

```json
{
  "location": {
      "lat": -38.383494,
      "lng": 33.427362
  },
  "accuracy": 51,
  "name": "Frontline house",
  "phone_number": "(+91) 983 893 3937",
  "address": "Nemtsov street, 250215",
  "types": [
      "flat",
      "park"
  ],
  "website": "https://www.google.com",
  "language": "English"
}
```

### Example HTTP-response 

```json
{
    "status": "OK",
    "place_id": "d965a5c91d7499b8b5e3620c392de4e2",
    "scope": "APP",
    "reference": "63bf79956bbe23e03cb97ea40cef3fed63bf79956bbe23e03cb97ea40cef3fed",
    "id": "63bf79956bbe23e03cb97ea40cef3fed"
}
```

### Tests tab

```JS
let jData = pm.response.json(); // assign the http-response as the 'jData' variable

let placeID = jData.place_id; // assign the place_id value from the http-response as the 'placeID' variable (e.g. d965a5c91d7499b8b5e3620c392de4e2)

pm.collectionVariables.set("place_id", placeID); // set a collection variable with a value from the 'placeID' variable
```
---

## ```GET``` - **Check place**

### Base URL: https://rahulshettyacademy.com

### Endpoint: /maps/api/place/get/json

### Params

<table>
  <tbody>
    <tr>
      <th>№</th>
      <th>KEY</th>
      <th>VALUE</th>
      <th>Commentary</th>
    </tr>
    <tr>
      <td>1</td>
      <td>key</td>
      <td>qaclick123</td>
      <td></td>
    </tr>
    <tr>
      <td>2</td>
      <td>place_id</td>
      <td>{{place_id}}</td>
      <td>It's taken from the collection variable, which was set after POST-response (e.g. d965a5c91d7499b8b5e3620c392de4e2) </td>
    </tr>
  </tbody>
</table>

### Example HTTP-request

```HTTP 
GET /maps/api/place/get/json?key=qaclick123&place_id=d965a5c91d7499b8b5e3620c392de4e2 HTTP/1.1
Host: rahulshettyacademy.com
```

### Example HTTP-responses 

###### if everything's OK:

```json
{
    "location": {
        "latitude": "-38.383494",
        "longitude": "33.427362"
    },
    "accuracy": "51",
    "name": "Frontline house",
    "phone_number": "(+91) 983 893 3937",
    "address": "Nemtsov street, 250215",
    "types": "flat,park",
    "website": "http://google.com",
    "language": "English"
}
```
###### if not:

```json
{
    "msg": "Get operation failed, looks like place_id  doesn't exists"
}
```

### Tests tab

```javascript
let jData = pm.response.json(); // assign the http-response as the 'jData' variable
let address = jData.address; // assign the address value from the http-response as the 'address' variable
let exp_address = pm.collectionVariables.get("place_address"); // assign the coolection variable place_address as a 'exp_address'
let placeID = pm.collectionVariables.get("place_id"); // assign the coolection variable place_id as a 'placeID'

pm.test("Check adress", function () {
  if (placeID != null){ // If the place_id exists
      if (address === exp_address){ // and the current address matches the address, which was set as a collection variable
      postman.setNextRequest('Update place'); // then next request should be 'Update place'
      } else postman.setNextRequest('Delete place'); // if the addresses doesn't match then next request should be 'Delete place' 
  } else postman.setNextRequest(null); // If the place_id doesn't exist at all then the collection running must be stopped 
}); 
```

---

## ```PUT``` - **Update place**

### Base URL: https://rahulshettyacademy.com

### Endpoint: /maps/api/place/update/json

### Example HTTP-request

```HTTP 
PUT /maps/api/place/update/json HTTP/1.1
Host: rahulshettyacademy.com
Content-Type: application/json
Content-Length: 94
```
###### Body raw (JSON)

```json
{
    "key":"qaclick123",
    "place_id":"d965a5c91d7499b8b5e3620c392de4e2", 
    "address":"Politkovskaya street, 071006"
}
```

### Example HTTP-response 

###### if everything's OK:

```json
{
    "msg": "Address successfully updated"
}
```

###### if not:

```json
{
    "msg": "Update address operation failed, looks like the data doesn't exists"
}
```

### Tests tab

```javascript 
let jData = pm.response.json(); // assign the http-response as the 'jData' variable
let msg = jData.msg; // assign the msg value from the http-response as the 'msg' variable

pm.test("Check address", function () {
  if (msg === "Address successfully updated"){ // if the updating is successful 
      postman.setNextRequest('Check place')} // then the collection running jump to the 'Check place' request 
  else postman.setNextRequest(null); // if something's wrong then the collection running must be stopped
});
```
---