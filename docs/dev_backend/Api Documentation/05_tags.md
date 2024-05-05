---
tags:
  - backend
  - famcal
  - api
---

# Tags

### Headers (Authentication)
The following Headers have to be provided by the API request: 
```JSON
{
Content-Type: "application/json",
api_key: "<Your API Token>",
family_uuid: "<The current Family UUID>"
}

```

### Add a Tag 

#### Endpoint
**`POST`** `/tags` 
 
#### Payload (JSON)
```JSON
{
  "tagName":"Home",
  "tagColor":"#e30b82"
}
```

> [!IMPORTANT]
> `tagName` is mandatory.

### Find all Tag entries

#### Endpoint
**`POST`**  `/tags/find` 

#### Payload (JSON)
`{}`

### Find one Tag entry

#### Endpoint
**`POST`**  `/tags/find` 

#### Payload (JSON)

`{"uuid":"<valuetofind>}`

(or any other valid key:value pairs)


### ~~Update one Tag's entry~~

#### Endpoint
**`PATCH`**  `/tags/<UUID>` 

#### Payload (JSON)
```
{
  "tagName":"School"
}
```
> [!NOTE]
> NO need to patch everything. Just add the changed Data into the JSON payload.

### ~~Delete one Tag's entry~~

#### Endpoint
**`DELETE`**  `/tags/<UUID>` 

#### Payload (JSON)
`none`


> [!WARNING]
> No Confirmation asked. This action cannot be undone.