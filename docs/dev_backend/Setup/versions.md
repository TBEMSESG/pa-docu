# Supported Versions

The following versions are tested to run together. Do not try to create other combinations. 
:::note[]
From version 1.0.0 onwards, Backend and Frontend will always share the same version.
:::

## Versions Table
Date        |  Frontend | Backend    | DataBase   | Docs     | Note  |
------------|-----------|------------|------------|----------|:------|
05.05.2024  |   0.9.19   |  0.9.6    |    0.1.0   |          | -      |
10.05.2024  |0.9.20     |     0.9.7  |    0.1.0   |   0.9.1  |   Only Server side cookies are used, httpOnly   |
11.05.2024  |  0.9.21       |  0.9.8    | 0.1.0    |   0.9.2      |   Moved signup Logic to backend and other small updates |


## Release Note
----
### 11.05.2024
#### Backend 0.9.8
- Moved signup logic to backend (/signup endpoint)
- some small error correction due to removed react-auth-kit in 0.9.7 

#### Frontend 0.9.21
- Removed signup logic from frontend.

#### DataBase 0.1.0
- no changes

#### Docker Compose
- no changes
----
### 10.05.2024
#### Backend 0.9.7
- Modified Enpoints to get User Infos and API key either from the Request Header (for external API access) or from the Cookies 

#### Frontend 0.9.20
- Removed React-auth-kit
- Removed Client side created cookies
- Corrected Login and Logout issues (rerendering)
- Added Registration Page (Create new User and add new Family)

#### DataBase 0.1.0
- no changes

#### Docker Compose
- Mounted `backend` `Logs` locally to have them persistent 
- Added `docs`
--- 
