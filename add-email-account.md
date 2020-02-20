# Add an Email Address to the Account

**Request method:** `POST`

**Request URL**: `https://megatron.com/api/enterprise/v1/email/`

This API call adds an email address to a Breach Report account associated with the secret API key that needs to be included in the request header. 


**Email check** returns:

* Incidents count for **unverified** emails.
* Incidents count and details for **verified** emails.

How to construct the request:
1. Include the API key in the request header.
2. Specify the email address in the request body.

## Request and response examples

```shell
curl --location --request POST 'https://megatron.com/api/enterprise/v1/email/' \
--header 'api-key: 72427357-6a59-4e1b-87fb-71c12231aacd' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--form 'email=test@test.com'
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
| email | string | Email you want to add to the account for monitoring. |



<aside class="success">
If the email address has been successfully added to the account, the response will be `200 OK`. 
</aside>
