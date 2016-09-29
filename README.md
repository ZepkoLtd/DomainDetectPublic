# DomainDetectPublic
Public REST API Code And Documentation For DomainDetect.io

## API Documentation

DomainDetect.io's REST API is accessible at https://www.domaindetect.io/apiv1/ and is useable to any paid subscriber (including users with an acitved trial). The REST API can be used to view, modify, create and delete alerts.

By default we have left the Django-Rest client open to the pulic to assist you in understanding the API's functionality.

The RESTAPI uses a slightly different wording to the main interface, "Search Terms" are "Alerts" in the api and "Search Results" are just "Results". 

### Endpoint: /alerts

Alerts is gets all search queries for your user.

#### Method: GET

View a list of all alerts active for your user. The "results" feild for each alert is a resultid for viewing matches.

**_Sample Response_**
```
  {
    "count": 4,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 17,
            "created": "2016-09-28T11:14:17Z",
            "query": "%term1%",
            "results": [
                "6"
            ],
            "owner": "root"
        },
        {
            "id": 18,
            "created": "2016-09-28T11:28:51Z",
            "query": "%term2%",
            "results": [],
            "owner": "root"
        }
    ]
}
```


### Endpoint: /alerts/{alertid}

#### Method: GET

#### Method: POST

#### Method: DELETE

#### Method: PUT

### Endpoint: /results

#### Method: GET

### Endpoint: /results/{resultid}

#### Method: GET

#### Method: POST

#### Method: DELETE

#### Method: PUT

### Endpoint: /users/

#### Method: GET

#### Method: POST

### Endpoint: /users/id

#### GET

#### PUT
