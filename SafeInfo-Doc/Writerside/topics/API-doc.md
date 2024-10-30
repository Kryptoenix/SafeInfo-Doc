# API documentation


- [Login](#login)
- [Registration](#registration)
- [Forgot Password](#forgot-password)
- [Verify Phone Number](#verify-phone-number)
- [Verify OTP](#verify-otp)
- [New Chat IDs](#new-chat-ids)
- [Get Public Key](#get-public-key)
- [Send Public Key](#send-public-key)
- [Get Session](#get-session)
- [Get Chat ID](#get-chat-id)
- [Change Phone](#change-phone)
- [Change Password](#change-password)

---

### Login
##### **Endpoint**: `/api/login`
 * **Method**: POST
 * **Description**: Authenticates a user with their username and password.

##### **Parameters**

   | Field          | Type    | Required | Description                        |
   |----------------|---------|----------|------------------------------------|
   | `username`     | String  | Yes      | The username of the user.          |
   | `passwordHash` | String  | Yes      | The password hash for the account. |
### **Example Requests and Responses** {id="example0"}
#### **Request Example** {id="request0"}
```http
POST /api/login
Content-Type: application/json

{
    "username": "exampleUser",
    "passwordHash": "examplePasswordHash"
}
```
**Response** 

| Field	        | Type      | 	Description                              |
|---------------|-----------|-------------------------------------------|
| `status`      | String    | 	"success" or "error".                    |
| `message`     | String	   | Error details, if the status is "error".  |
| `phoneNumber` | String    | Phone number associated with the account. |
**Response Example**
**Successful Login:**

```json
{
    "status": "success",
    "phoneNumber": "+0123456789101"
}
```
##### **Failed Login:**

```json
{
    "status": "error",
    "message": "Invalid username or password."
}
```


### Registration
##### **Endpoint**: `/api/registration`
* **Method**: POST
* **Description**: Registers a new user with username, password and phone number.

##### **Parameters** {id="param1"}

| Field          | Type   | Required | Description                        |
|----------------|--------|----------|------------------------------------|
| `username`     | String | Yes      | The username of the user.          |
| `passwordHash` | String | Yes      | The password hash for the account. |
| `phone`        | String | Yes      | The phone number for the account.  |
### **Example Requests and Responses** {id="example2"}
#### **Request Example** {id="request2"}
```http
POST /api/registration
Content-Type: application/json

{
    "username": "exampleUser",
    "password": "examplePasswordHash",
    "phone":"examplePhoneNumber"
}
```
##### **Response**

| Field	    | Type   | 	Description                             |
|-----------|--------|------------------------------------------|
| `status`  | String | 	"success" or "error".                   |
| `message` | String | Error details, if the status is "error". |
##### **Response Example**
##### **Successful Login:**

```json
{
    "status": "success"
}
```
**Failed Login:**

```json
{
    "status": "error",
    "message": "Invalid username or password."
}
```


### Forgot-Password
##### **Endpoint**: `/api/forgotPassword`
* **Method**: POST
* **Description**: Authenticates a user by sending a verification code to the associated phone number account.

**Parameters**

| Field          | Type    | Required | Description                   |
   |----------------|---------|----------|-------------------------------|
| `username`     | String  | Yes      | The username of the user.     |
### **Example Requests and Responses** {id="example3"}
#### **Request Example** {id="request3"}
```http
POST /api/forgotPassword
Content-Type: application/json

{
    "username": "exampleUser"
}
```
**Response**

| Field	    | Type    | 	Description                             |
|-----------|---------|------------------------------------------|
| `status`  | String  | 	"success" or "error".                   |
| `message` | String  | Error details, if the status is "error". |
**Response Example**
**Successful Login:**

```json
{
    "status": "success"
}
```
**Failed Login:**

```json
{
    "status": "error",
    "message": "Invalid username."
}
```


### Verify-Phone-Number
##### **Endpoint**: `/api/verifyPhoneNumber`
* **Method**: POST
* **Description**: Sends a verification code to user's phone number.

**Parameters**

| Field            | Type    | Required | Description                        |
   |------------------|---------|----------|------------------------------------|
| `username`       | String  | Yes      | The username of the user.          |
| `hashedPassword` | String  | Yes      | The password hash for the account. |
### **Example Requests and Responses** {id="example4"}
#### **Request Example** {id="request4"}
```http
POST /api/verifyPhoneNumber
Content-Type: application/json

{
    "username": "exampleUser",
    "hashedPassword": "examplePasswordHash"
}
```
**Response**

| Field	        | Type    | 	Description                                |
|---------------|---------|---------------------------------------------|
| `status`      | String  | 	"success" or "error".                      |
| `message`     | String	 | Error details, if the status is "error".    |
| `phoneNumber` | String  | Phone Number associated with user's account |
**Response Example**
**Successful Login:**

```json
{
    "status": "success",
    "phoneNumber": "+123456789101"
}
```
**Failed Login:**

```json
{
    "status": "error",
    "message": "Invalid username or password."
}
```

### Verify-OTP
##### **Endpoint**: `/api/verifyOTP`
* **Method**: POST
* **Description**: Validates the OTP code, returning "success" upon successful login.

**Parameters**

| Field      | Type    | Required | Description                        |
   |------------|---------|----------|------------------------------------|
| `username` | String  | Yes      | The username of the user.          |
| `otp`      | String  | Yes      | The OTP code receives through SMS. |
### **Example Requests and Responses** {id="example5"}
#### **Request Example** {id="request5"}
```http
POST /api/verifyOTP
Content-Type: application/json

{
    "username": "exampleUser",
    "otp": "123456"
}
```
**Response**

| Field	         | Type    | 	Description                             |
|----------------|---------|------------------------------------------|
| `status`       | String  | 	"success" or "error".                   |
| `message`      | String	 | Error details, if the status is "error". |
| `passwordHash` | String  | The password hash of the user.           |
**Response Example**
**Successful Login:**

```json
{
    "status": "success",
    "passwordHash": "992feb10b..."
}
```
**Failed Login:**

```json
{
    "status": "error",
    "message": "Failed to get password hash from database"
}
```


### New-Chat-Ids
##### **Endpoint**: `/api/newChatIds`
* **Method**: POST
* **Description**: Returns a list of new chat ids.

**Parameters**

| Field   | Type    | Required | Description                           |
|---------|---------|----------|---------------------------------------|
| `token` | String	 | Yes      | JWT token for session authentication. |
### **Example Requests and Responses** {id="example6"}
#### **Request Example** {id="request6"}
```http
POST /api/newChatIds
Content-Type: application/json

{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```
**Response**

| Field	    | Type    | 	Description                             |
|-----------|---------|------------------------------------------|
| `status`  | String  | 	"success" or "error".                   |
| `token`   | String	 | JWT token for session authentication.    |
| `message` | String  | Error details, if the status is "error". |
**Response Example**
**Successful Login:**

```json
{
    "status": "success",
    "newChatIds" : ["<chat-id1>","<chat-id2>",...]
}
```
```json
{
    "status": "success",
    "message": "No new chat ids found"
}
```
**Failed Login:**

```json
{
    "status": "error",
    "message": "Failed to find new chat ids in database"
}
```


### Get-Public-Key
##### **Endpoint**: `/api/getPubKey`
* **Method**: POST
* **Description**: Requests the RSA public key of another user.

**Parameters**

| Field       | Type    | Required | Description                           |
   |-------------|---------|----------|---------------------------------------|
| `token`     | String  | Yes      | JWT token for session authentication. |
| `otherUser` | String  | Yes      | The username of the other user.       |
### **Example Requests and Responses** {id="example7"}
#### **Request Example** {id="request7"}
```http
POST /api/getPubKey
Content-Type: application/json

{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
    "otherUser": "exampleOtherUser"
}
```
**Response**

| Field	    | Type    | 	Description                                  |
|-----------|---------|-----------------------------------------------|
| `status`  | String  | 	"success" or "error".                        |
| `message` | String	 | Error details, if the status is "error".      |
| `pubKey`  | String  | Base64 encoded public key for the other user. |
**Response Example**
**Successful Login:**

```json
{
    "status": "success",
    "pubKey": "MIIBIjANBgkqhkiG9w0BAQEFAAO..."
}
```
**Failed Login:**

```json
{
    "status": "error",
    "message": "Failed to get pubKey from database"
}
```


### Send-Public-Key
##### **Endpoint**: `/api/sendPubKey`
* **Method**: POST
* **Description**: Sends the base64 encoded public key of current user to server.

**Parameters**

| Field    | Type   | Required | Description                           |
   |----------|--------|----------|---------------------------------------|
| `token`  | String | Yes      | JWT token for session authentication. |
| `pubKey` | String | Yes      | The public key for the current user.  |
### **Example Requests and Responses** {id="example8"}
#### **Request Example** {id="request8"}
```http
POST /api/sendPubKey
Content-Type: application/json

{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "pubKey": "MIIBIjANBgkqhkiG9w0BAQEFAAO..."
}
```
**Response**

| Field	    | Type    | 	Description                             |
|-----------|---------|------------------------------------------|
| `status`  | String  | 	"success" or "error".                   |
| `message` | String  | Error details, if the status is "error". |
**Response Example**
**Successful Login:**

```json
{
    "status": "success"
}
```
**Failed Login:**

```json
{
    "status": "error",
    "message": "Failed to update pubKey field"
}
```


### Get-Session
##### **Endpoint**: `/api/getSession`
* **Method**: POST
* **Description**: Retrieves a session token with the provided credentials.

**Parameters**

| Field          | Type    | Required | Description                        |
   |----------------|---------|----------|------------------------------------|
| `username`     | String  | Yes      | The username of the user.          |
| `passwordHash` | String  | Yes      | The password hash for the account. |
### **Example Requests and Responses** {id="example9"}
#### **Request Example** {id="request9"}
```http
POST /api/getSession
Content-Type: application/json

{
    "username": "exampleUser",
    "passwordHash": "examplePasswordHash"
}
```
**Response**

| Field	    | Type    | 	Description                             |
|-----------|---------|------------------------------------------|
| `status`  | String  | 	"success" or "error".                   |
| `message` | String	 | Error details, if the status is "error". |
| `token`   | String  | JWT token for session authentication.    |
**Response Example**
**Successful Login:**

```json
{
    "status": "success",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```
**Failed Login:**

```json
{
    "status": "error",
    "message": "Wrong username or password"
}
```


### Get-Chat-Id
##### **Endpoint**: `/api/getChatId`
* **Method**: POST
* **Description**: Retrieves an existing chat id for a specified user.

**Parameters**

| Field       | Type   | Required | Description                           |
   |-------------|--------|----------|---------------------------------------|
| `token`     | String | Yes      | JWT token for session authentication. |
| `otherUser` | String | Yes      | The username of the other user.       |
### **Example Requests and Responses** {id="example10"}
#### **Request Example** {id="request10"}
```http
POST /api/getChatId
Content-Type: application/json

{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "otherUser": "exampleOtherUser"
}
```
**Response**

| Field	    | Type    | 	Description                             |
|-----------|---------|------------------------------------------|
| `status`  | String  | 	"success" or "error".                   |
| `token`   | String	 | JWT token for session authentication.    |
| `message` | String  | Error details, if the status is "error". |
**Response Example**
**Successful Login:**

```json
{
    "status": "success",
    "chatId": "84c10f60-f1cf-4045-b018-113e9dd40a49"
}
```
**Failed Login:**

```json
{
    "status": "error",
    "message": "Failed to get chat id from database"
}
```


### Change-Phone
##### **Endpoint**: `/api/changePhone`
* **Method**: POST
* **Description**: Requests a new phone number.

**Parameters**

| Field   | Type   | Required | Description                           |
|---------|--------|----------|---------------------------------------|
| `token` | String | Yes      | JWT token for session authentication. |
| `phone` | String | Yes      | The new phone number for the account. |
### **Example Requests and Responses** {id="example11"}
#### **Request Example** {id="request11"}
```http
POST /api/changePhone
Content-Type: application/json

{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "phone": "+0123456789101"
}
```
**Response**

| Field	    | Type    | 	Description                             |
|-----------|---------|------------------------------------------|
| `status`  | String  | 	"success" or "error".                   |
| `message` | String  | Error details, if the status is "error". |
**Response Example**
**Successful Login:**

```json
{
    "status": "success"
}
```
**Failed Login:**

```json
{
    "status": "error",
    "message": "Failed to change phone number; user may not exist"
}
```


### Change-Password
##### **Endpoint**: `/api/changePassword`
* **Method**: POST
* **Description**: Requests a new password.

**Parameters**

| Field         | Type   | Required | Description                           |
   |---------------|--------|----------|---------------------------------------|
| `token`       | String | Yes      | JWT token for session authentication. |
| `newPassword` | String | Yes      | The new password for the account.     |
### **Example Requests and Responses** {id="example12"}
#### **Request Example** {id="request12"}
```http
POST /api/changePassword
Content-Type: application/json

{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "newPassword": "examplePassword"
}
```
**Response**

| Field	    | Type    | 	Description                             |
|-----------|---------|------------------------------------------|
| `status`  | String  | 	"success" or "error".                   |
| `message` | String  | Error details, if the status is "error". |
**Response Example**
**Successful Login:**

```json
{
    "status": "success"
}
```
**Failed Login:**

```json
{
    "status": "error",
    "message": "Failed to change password; user may not exist"
}
```
