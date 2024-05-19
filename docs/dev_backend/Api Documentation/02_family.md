---
id: 02_family
tags:
  - backend
  - api
  - famcal
---
# Family
>To be checked - Not complete

### Add a Family 

#### Endpoint 
**`POST`** `/api/family` 
 
#### Payload (JSON)
```JSON
{
    "familyName": "Your Name",
    "familyColor": ""
}
```
#### Schema
```JSON
{
    familyName: Joi.string()
        .min(3)
        .max(15)
        .required(),
    familyColor: Joi.string()
        .pattern(/^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$/),
    createdBy : Joi.string()
}

```

> [!IMPORTANT]
> `familyName` is mandatory.

### Find all Family entries

#### Endpoint 
**`POST`**  `/api/family/find` 

#### Payload (JSON)

```JSON
{}
```

### Find one Family entry

#### Endpoint 
**`POST`**  `/api/family/find`

#### Payload (JSON)
```JSON
{"uuid":"<valuetofind>}
```

(or any other valid key:value pairs)

### Update one Family entry

#### Endpoint 
**`PATCH`**  `/api/family/<UUID>` 

#### Payload (JSON)
```JSON
{
  "subject":"Clean the car"
}
```
> [!NOTE]
> No need to patch everything. Just add the changed Data into the JSON payload.

### Delete one Family entry

#### Endpoint 
**`DELETE`**  `/api/family/<UUID>`

#### Payload (JSON)
```JSON
{}
```

> [!WARNING]
> No Confirmation asked. This is an irreversible action.

### Add an Invitation Code to join Family as signup

#### Endpoint
**`POST`**  `/api/family/code`

#### Payload (JSON)
```JSON
{
    "uuid" : "the desired FamilyID" ,
    "invitationCode": "a 6 digit code" # like "ABG4RT"
}
``` 


### Check for an Invitation Code to join Family as signup

#### Endpoint
**`GET`**  `/api/family/<uuid>/code/<code>`

#### Payload (JSON)
```JSON
{}
``` 