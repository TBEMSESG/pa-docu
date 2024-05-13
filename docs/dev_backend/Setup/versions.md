---
id: 03_versions
tags:
  - backend
  - docker
  - famcal
---

# Supported Versions

The following versions are tested to run together. Do not try to create other combinations. 
:::note[]
From version 1.0.0 onwards, Backend and Frontend will always share the same version.
:::

## Versions Table
Date        |  Frontend | Backend    | DataBase   | Docs     | Note  |
------------|-----------|------------|------------|----------|:------|
13.05.2024  |   0.9.22(u) |  0.9.11    |   0.1.0 (u) | 0.9.4   | backend logging reworked
12.05.2024  |  0.9.22   |  0.9.9     |    0.1.0   |   0.9.3  | Optimized Cookie utilization
11.05.2024  |  0.9.21       |  0.9.8    | 0.1.0    |   0.9.2      |   Moved signup Logic to backend and other small updates |
10.05.2024  |0.9.20     |     0.9.7  |    0.1.0   |   0.9.1  |   Only Server side cookies are used, httpOnly   |
05.05.2024  |   0.9.19   |  0.9.6    |    0.1.0   |          | -      |

(u) = unchanged

## Release Notes

----
### NextRelease
#### Backend 0.9.10
- logging has been completely revorked to be more clean and organized.
- added new env Variable for log level (debug, info, warn or error) if nothing is provided, then info is default.

#### Frontend 0.9.x
- no changes

#### DataBase 0.1.x
- no changes
  
#### Documentation 0.9.4
- small updates

#### Docker Compose
- no changes

----
### 12.05.2024
#### Backend 0.9.9
- added new Cookie with backend version information
- recreated ME endpoint to only work with the signed tocken from the client

#### Frontend 0.9.22
- Modified /MePage to get the info from the /me endpoint instead of using the fc_user Cookie

#### DataBase 0.1.0
- no changes
  
#### Documentation 0.9.3
- reordered Versions Table

#### Docker Compose
- no changes
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
