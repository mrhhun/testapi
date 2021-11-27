# Hun Cross Country API #

This API allows you to track and record race times for Hun Cross Country runners

The API is available at `https://hunxcapi.hunschool.org`

## Endpoints ##

### Status ###

GET `/status`

Returns the status of the API.

### List of races ###

GET `/races`

Returns a list of races from the current cross-country season.

Optional query parameters:

- date: the date of the race (Format mm-dd)
- location: the location of the race


### Get a single race ###

GET `/races/:raceId`

Retrieve detailed information about a race.


### Submit a result ###

POST `/results`

Allows you to submit an individual result for a race. Requires authentication.

The request body needs to be in JSON format and include the following properties:

 - `resultId` - Integer - The unique ID of the result. Required
 - `runnerId` - Integer - The unique ID of a Hun runner. Required
 - `raceID` - Integer - The unique ID of the race. Required
 - `location` - String - The name of the location where the race was run. Required
 - `time` - Integer - The time (in seconds) of a runner for the race. Required
 - `name` - String - The name of the runner. Optional

Example
```
POST /results/
Authorization: Bearer <YOUR TOKEN>

{
  "resultID": 26,
  "runnerId": 1,
  "raceID": 5,
  "location": "Pennington",
  "time": 1101,
  "name": "Zach Huffman"
}
```

The response body will contain the access token.

### Update a result ###

PATCH `/results/:resultId`

Update an existing result. Requires authentication.

The request body needs to be in JSON format and allows you to update the following properties:

 - `location` - String
 - `time` - Integer
 - `name` - String

 Example
```
PATCH /results/PF6MflPDcuhWobZcgmJy5
Authorization: Bearer <YOUR TOKEN>

{
  "location": "Peddie",
  "time": 1,
  "name": "Barry Allen"
}
```

### Delete a result ###

DELETE `/results/:resultId`

Delete an existing result. Requires authentication.

The request body needs to be empty.

 Example
```
DELETE /results/PF6MflPDcuhWobZcgmJy5
Authorization: Bearer <YOUR TOKEN>

### Get all runners ###

GET `/runners`

Allows you to view all runners. Requires authentication.

### Get a runner ###

GET `/runners/:runnerId`

Allows you to view an existing runner. Requires authentication.
```

## API Authentication ##

To submit or view an order, you need to register your API client.

POST `/api-clients/`

The request body needs to be in JSON format and include the following properties:

 - `clientName` - String
 - `clientEmail` - String

 Example

 ```
 {
    "clientName": "Valentin",
    "clientEmail": "valentin@example.com"
}
 ```

The response body will contain the access token.

**Possible errors**

Status code 409 - "API client already registered." Try changing the values for `clientEmail` and `clientName` to something else.
