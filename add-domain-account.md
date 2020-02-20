# Add an Internet Domain to the Account

**Request method:** `POST`

**Request URL**: `{BASE_URL}/api/enterprise/v1/domain/`

This API request adds an internet domain to the Breach Report account associated with the secret API key from the request header. 

**Domain check** returns a response code and a status message. 

How to construct the request:
1. Include the API key in the request header.
2. Specify the email address in the request body.

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
| api-key | string | An API key you can generate on the [Portal](https://megatron.com/portal/user-api). Include the key in the request header. |
| domain | string | Domain you want to add to the account for monitoring. |


> Response example: Email address has been added.
### Email address has been added:

```
{
  "status": "success",
  "domain": {
    "id": "5e4e978211944f4cf3184eb4",
    "domainName": "vassily.pro"
  }
}
 
```
| Name | Type | Description |
| ------ | ------ | ------ |
| id | string | ID of the requested email address in the Breach Report database. |
| emailAddress | string | The requested email address. |


> Response example: Email address has not been added.

### Email address was added before:

```
{
  "status": "error",
  "message": "Email address already exists"
}
```
