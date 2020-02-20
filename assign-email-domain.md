# Add an Email Address to the Watchlist

**Request method:** `POST`

**Request URL**: `https://megatron.com/api/enterprise/v1/email/`

This API call assigns an email address to a domain. Both the email address and the domain must already exist in the Breach Report data for the operation to be successful. 
Email address assigning enables the data to be aggregated across the registered domains. 


**Email check** returns:

* Incidents count for **unverified** emails.
* Incidents count and details for **verified** emails.

How to construct the request:
1. Include the API key in the request header.
2. In the request body, specify:
2.1. Email address
2.2. Domain identifier in the Breach Report database


## Request and response examples

```shell
# Sample terminal command
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
| email | string | Email address in the Breach Report database. |
| domainId | string | Identifier of the domain in the Breach Report database. |



> Response: Email Successfully Assigned

### Verified email response:

```
{
  "status": "success",
  "email": {
    "id": "5e4e9b0d11944f4cf3184eb7",
    "emailAddress": "me@vassily.pro"
  }
}
 
```
| Name | Type | Description |
| ------ | ------ | ------ |
| id | string | ID of the requested email address in the Breach Report database. |
| emailAddress | string | The requested email address. |


> Response: Email address can't be assigned

### Unverified email response:

```
{
  "status": "error",
  "message": "Email address already exists"
}
```
