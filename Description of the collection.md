## Methods:

## ```POST``` - **Add new place**

### URI
```https://rahulshettyacademy.com/maps/api/place/add/json?key=qaclick123```

### PARAMS
**KEY**: key <br> **VALUE**: qaclick123
### Example HTTP-request
```HTTP 
POST /maps/api/place/add/json?key=qaclick123 HTTP/1.1
Host: rahulshettyacademy.com
Content-Type: application/json
Content-Length: 308
```
#### Body raw (JSON)
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
  "website": "http://google.com",
  "language": "English"
}
```