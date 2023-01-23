## Methods:

## ```POST``` - **Add new place**

### Base URL: https://rahulshettyacademy.com

### Endpoint: ```/maps/api/place/add/json```

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

let placeID = jData.place_id; // assign the place_id value as the 'placeID' variable (e.g. d965a5c91d7499b8b5e3620c392de4e2)

pm.collectionVariables.set("place_id", placeID); // set a collection variable with a value from the 'placeID' variable
```
