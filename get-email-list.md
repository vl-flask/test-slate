# Get the Email List

**Request method:** `GET`

**Request URL**: `https://megatron.com/api/enterprise/v1/email

This call returns the list of Email Addresses attributed to the API key owner's account.  


To construct the request, include the API key in the request header.

## Request and response examples

```shell
# sample terminal command
```

```c
// Sample C code
```

```csharp
// Sample C# code
```


```go
// Sample Golang comments
```

```http
<!-- Sample HTTP code --> 
```


```java
// Sample Java code
```

```javascript
// Fetch
```

```javascript
// NodeJS
```

```php
// Sample PHP code
```

```python
# Sample Python code - http.client
# Sample Python code - requests
```

```ruby
# Sample Ruby code 
```

```swift
// Sample Swift Code
```


**Request parameters:**

| Name | Type | Description |
| ------ | ------ | ------ |
| api-key | string | An API key you can generate on the [Portal](https://megatron.com/portal/user-api). Include this key in the request header. |



> Response for verified email

### Verified email response:

```
{
  "status": "success",
  "data": [
    {
      "id": "5e4e9b0d11944f4cf3184eb7",
      "emailAddress": "me@vassily.pro",
      "inWatchlist": false,
      "isAssignToDomain": true,
      "domain": {
        "id": "5e4e978211944f4cf3184eb4",
        "domainName": "vassily.pro"
      }
    }
  ]
}
 
```
| Name | Type | Description |
| ------ | ------ | ------ |
| status | string | Operation status - success or error. |
| data | integer | THe list / array of email address data. |
| id | string | Email id. |
| emailAddress | integer | Email incidents count. |
| inWatchlist | boolean | Email is verified the user: True/False. |
| isAssignToDomain | boolean | The  list of detailed incidents description. |
| domain | nested object | Data for the related domain, if isAssignToDomain === true |


> Response for unverified email

### Unverified email response:

```
{
    "email": "test@test.com",
    "records": 34924,
    "isAssigned": false,
    "incidents": null
}
```
| Name | Type | Description |
| ------ | ------ | ------ |
| email | string | Email that is checked. |
| records | integer | Email incidents count. |
| isAssigned | boolean | Email verified by a user: true/false. |
| incidents | null / [] | Detailed incident information. If `isAssigned = false`, then `incidents` will be null. |