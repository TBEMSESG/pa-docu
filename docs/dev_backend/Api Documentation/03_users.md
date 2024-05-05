---
id: 03_users
tags:
  - backend
  - api
  - famcal
---

# Users

### Headers (Authentication)
The following Headers have to be provided by the API request: 
```JSON
{
Content-Type: "application/json"
}

```

### Add user entry (Signup)

#### Endpoint 
**`POST`** `/api/users`

#### Payload (JSON)
```jSON
{
  "username": "thomas",
  "email": "tbe@pm.me",
  "password": "******",
  "repeat_password": "******",
  "remember": true,
  "isAdmin": true,
  "linkedPerson": "uuid",
  "linkedFamily": "uuid"
}
```
#### Schema
```JSON
    username: Joi.string()
        .alphanum()
        .min(3)
        .max(30)
        .required(),
    email: Joi.string()
        .email(),
    password: Joi.string()
        .required()
        .pattern(new RegExp('^[a-zA-Z0-9]{3,60}$')),
    repeat_password: Joi.ref('password'),
    remember: Joi.boolean(),
    linkedPerson: Joi.String(),
    linkedFamily: Joi.String(),
    isAdmin: Joi.boolean(),
    isFamilyAdmin : Joi.boolean()
})
    .with('password', 'repeat_password');
```
where `username` and `password` are mandatory, and `password` and `repeat_password` must be the same

### Find all user entries

#### Endpoint 
**`POST`**  `/users`

#### Payload (JSON)

`{}`

> [!NOTE]
> The requesting User must have `isAdmin = true` role

### Find one user

#### Endpoint 
**`GET`**  `/users/<UUID>`

#### Payload (JSON)
`none`

### Update one user entry

#### Endpoint 
**`PATCH`**  `/users/<UUID>`

#### Payload (JSON)
```JSON
{
  "attendees": [
    "Lionel",
    "Lu"
  ],
  "tags": ["schule", "Wald"]
}
```
No need to patch everything. Just add the changed data to the JSON payload.

### Delete one user entry

#### Endpoint 
**`DELETE`**  `/users/<UUID>`

#### Payload (JSON)
`none`

> [!WARNING]
> No Confirmation asked. Cannot be undone.