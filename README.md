# DomainDetectPublic
Public REST API Code And Documentation For DomainDetect.io

## API Documentation

DomainDetect.io's REST API is accessible at https://www.domaindetect.io/apiv1/ and is useable to any paid subscriber (including users with an acitved trial). The REST API can be used to view and manipulate your user, alerts and results.

By default we have left the Django-Rest client open to the pulic to assist you in understanding the API's functionality.

The RESTAPI uses a slightly different wording to the main interface, "Search Terms" are "Alerts" in the api and "Search Results" are just "Results". 

### Authentication

API authentication is controlled using Django Session ID's. 

Post your username and password to /apiv1/api-auth/login/

**__Sample Request Form Data__**
```
username:user
password:pass
```

The API will then assign you a sessionid in a cookie to send with each request:

**__Sample Response Cookie__**

```
sessionid=21ss25kc50y203sdf260e62llsbs87am40;
```

### Endpoint: /alerts

Alerts is gets all search queries for your user.

#### Method: GET

View a list of all alerts active for your user. The "results" feild for each alert is a resultid for viewing matches.

**__Sample Response__**
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
#### Method: POST

Create a new alert. (Just leave results blank, this is for importing old results)

**__Sample Request Body__**
```
{
    "query": "%yourtermhere%",
    "results": []
}
```

### Endpoint: /alerts/{alertid}

This endpoint is for viewing and manipulating individual alerts.

#### Method: GET

View a single alert.

**__Sample Response__**
```
  {
    "id": 17,
    "created": "2016-09-28T11:14:17Z",
    "query": "%vod%",
    "results": [
        "6"
    ],
    "owner": "root"
}
```
#### Method: PUT

Modify an existing alert

**__Sample Request Body__**
```
{
    "id": 21,
    "created": "2016-09-29T09:47:32Z",
    "query": "%234567%",
    "results": []
}
```

#### Method: DELETE

Delete an alert. (Just pull the body from /alerts/{id} and send it back with a DELETE request)


### Endpoint: /results

Results list all matches for your user.

#### Method: GET

Get all results for my user.

**__Sample Response__**
```
  {
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 6,
            "alert": 17,
            "created": "2016-09-28T12:23:18Z",
            "count": 25,
            "owner": "root",
            "result": "[\"evodl.com\", \"mozvod.com\", \"vodity.com\", \"vodyxl.com\", \"vodsjj.com\", \"vodlsx.com\", \"vodasjj.com\", \"vodayxl.com\", \"vodalsx.com\", \"evodbcc.com\", \"vodnaiba.com\", \"vodanaiba.com\", \"vodkafest.com\", \"vivodining.com\", \"kastelvodka.com\", \"lavodaliving.com\", \"volvodiyclub.com\", \"vodafonenews.com\", \"bez-provodov.com\", \"gaiolongvodao.com\", \"vodkashowroom.com\", \"treecityvodka.com\", \"texasvodkaclub.com\", \"vodlockerviooz.com\", \"digitalvideovisionvod.com\"]"
        }
    ]
}
```
### Endpoint: /results/{resultid}

Use for viewing a specific result.

#### Method: GET

Get a specific result.

**__Sample Response__**
```
  
  {
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 6,
            "alert": 17,
            "created": "2016-09-28T12:23:18Z",
            "count": 25,
            "owner": "root",
            "result": "[\"evodl.com\", \"mozvod.com\", \"vodity.com\", \"vodyxl.com\", \"vodsjj.com\", \"vodlsx.com\", \"vodasjj.com\", \"vodayxl.com\", \"vodalsx.com\", \"evodbcc.com\", \"vodnaiba.com\", \"vodanaiba.com\", \"vodkafest.com\", \"vivodining.com\", \"kastelvodka.com\", \"lavodaliving.com\", \"volvodiyclub.com\", \"vodafonenews.com\", \"bez-provodov.com\", \"gaiolongvodao.com\", \"vodkashowroom.com\", \"treecityvodka.com\", \"texasvodkaclub.com\", \"vodlockerviooz.com\", \"digitalvideovisionvod.com\"]"
        }
    ]
}
```
### Endpoint: /users/

For modifying, creating and updating users.

#### Method: GET

**__Sample Response__**

```
  {
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 1,
            "username": "myusername",
            "email": "user@site.com",
            "first_name": "John",
            "last_name": "Smith"
        }
    ]
}
```

#### Method: POST

Used to create a new user, remember that subscriptions must be activated through the interface. This can't be done from the API.

**__Sample Request Body__**
```
{
    "username": "NewUser",
    "password": "SuperSecurePassword",
    "email": "my@email.com",
    "first_name": "New",
    "last_name": "User"
}
```
### Endpoint: /users/{userid}

Used for viewing and updating just your user.

#### GET

Show your user details.

**__Sample Response__**

```
{
         "id": 1,
         "username": "myusername",
         "email": "user@site.com",
         "first_name": "Jonh",
         "last_name": "Smith"
}
```

#### PUT

Update your user details.

**__Sample Request Body__**
```
{
         "id": 1,
         "username": "myusername",
         "email": "user@site.com",
         "first_name": "John",
         "last_name": "Smith"
}
```

#### DELETE

Delete your user. Be careful.
