---
id: 05_versions
tags:
  - backend
  - docker
  - famcal
---

# Supported Versions

The following versions are tested to run together. Do not try to create other combinations. 

<!-- :::note[]
From version 1.0.0 onwards, Backend and Frontend will always share the same version.
::: -->

## Versions Table
Date        |  Frontend | Backend    | DataBase   | Docs     | Note  |
------------|-----------|------------|------------|----------|:------|
19.05.2024  |  0.9.26   |  0.9.13    |  0.1.0 (u) | 0.9.8    | InvitationCode Signup
17.05.2024  |   0.9.25   | 0.9.12 (u)|  0.1.0 (u) | 0.9.7   | Appointment Component modified
15.05.2024  |   0.9.24  |  0.9.12    |  0.1.0 (u) | 0.9.6   |  Family Settings and permission optimization 
13.05.2024  |   0.9.23 |  0.9.11    |   0.1.0 (u) | 0.9.5   | backend logging reworked
12.05.2024  |  0.9.22   |  0.9.9     |    0.1.0   |   0.9.3  | Optimized Cookie utilization
11.05.2024  |  0.9.21       |  0.9.8    | 0.1.0    |   0.9.2      |   Moved signup Logic to backend and other small updates |
10.05.2024  |0.9.20     |     0.9.7  |    0.1.0   |   0.9.1  |   Only Server side cookies are used, httpOnly   |
05.05.2024  |   0.9.19   |  0.9.6    |    0.1.0   |          | -      |

(u) = unchanged

## Release Notes

----
### 19.05.2024
#### Backend 0.9.13
- Added Endpoint to create an Invitation Code and to check for one
- Handling InvitationCode based signup. 

#### Frontend 0.9.26
- Added details about InvitationCodes and InvitationCodes Creation (Family Settings)
- 

#### DataBase 0.1.0
- no changes
  
#### Documentation 0.9.8
- small updates to the Fam API

#### Docker Compose
- no changes
----
### 17.05.2024
#### Backend 0.9.12
- no changes

#### Frontend 0.9.25
- modified Appointment Component
- updates Appointment Details view and header menu

#### DataBase 0.1.0
- no changes
  
#### Documentation 0.9.7
- small updates

#### Docker Compose
- no changes

----
### 15.05.2024
#### Backend 0.9.24
- reworked express middlewares to first identify the user based on jwt
- modified genericRoute to check permissions before searching, deleting or modifying an item. 
- modified familyRoute to check permissions before searching, deleting or modifying an item. 
- modified usersRoute to check permissions before searching, deleting or modifying an item. 

#### Frontend 0.9.12
- small correction in "family" requests to backend.
- added "Delete Appointement"-Button in Appointmentes page (... - Delete)
- modified Settings - Family to Show Family details (only Fam Admin or server Admin)
- Corrected Manual URL and API documentation URL and reordered menu items

#### DataBase 0.1.0
- no changes
  
#### Documentation 0.9.6
- small updates
- Separated setup Pages

#### Docker Compose
- no changes

----
### 13.05.2024
#### Backend 0.9.11
- logging has been completely revorked to be more clean and organized.
- added new env Variable for log level (debug, info, warn or error) if nothing is provided, then info is default.

#### Frontend 0.9.23
- small updates to debug page 
- small styling updates

#### DataBase 0.1.0
- no changes
  
#### Documentation 0.9.5
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
