---
tags:
  - backend
  - famcal
  - api
---

# People

### Headers (Authentication)
The following Headers have to be provided by the API request: 
```JSON
{
Content-Type: "application/json",
api_key: "<Your API Token>",
family_uuid: "<The current Family UUID>"
}

```

### Add Person 

#### Endpoint
**`POST`** `/people` 
 
#### Payload (JSON)
```JSON
{
  "firstName":"Thomas",
  "lastName":"Beck",
  "nickName":"Tom",
  "dob":"17.04.1979",
  "email":"mymail@mail.me"
}
```
#### Schema 
```JSON
firstName: 
        .string()
        .alphanum()
        .min(3)
        .max(30)
        .required(),
    lastName: 
        .string()
        .alphanum()
        .min(3)
        .max(30),
    nickName: 
        .string()
        .alphanum()
        .min(3)
        .max(30),
    dob: 
        .date()
        .format('DD.MM.YYYY'),
    email: 
        .string()
        .email()

```


> [!IMPORTANT]
> `firstName` is mandatory.

### Find all Person entries

#### Endpoint
**`POST`**  `/people/find` 

#### Payload (JSON)

`{}`

### Find one Person's entry

#### Endpoint
**`POST`**  `/people/find` 

#### Payload (JSON)

`{"uuid":"<valuetofind>}`

(or any other key:value pairs)

### ~~Update one Person's entry~~

#### Endpoint
**`PATCH`**  `/people/<UUID>` 

#### Payload (JSON)
```
{
  "nickName":"Thomas"
}
```
> [!NOTE]
> NO need to patch everything. Just add the changed Data into the JSON payload.

### ~~Delete one Person's entry~~

#### Endpoint
**`DELETE`**  `/people/<UUID>` 

#### Payload (JSON)
`none`

> [!WARNING]
> No Confirmation asked. It cannot be undone.