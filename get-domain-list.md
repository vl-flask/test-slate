# Get the Domain List

**Request method:** `GET`

**Request URL**: `https://megatron.com/api/enterprise/v1/domain

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



> Response example

### Domain list example:

```
{
  "status": "success",
  "data": [
    {
      "id": "5e4e978211944f4cf3184eb4",
      "domainName": "vassily.pro",
      "inWatchlist": false,
      "emailList": [
        {
          "id": "5e4e9b0d11944f4cf3184eb7",
          "emailAddress": "me@vassily.pro"
        }
      ]
    }
  ]
}
 
```
| Name | Type | Description |
| ------ | ------ | ------ |
| status | string | Operation status - success or error. |
| data | integer | THe list / array of email address data. |
| id | string | Domain identifier in the Breach Report database. |
| inWatchlist | boolean | The email is in the watchlist (in other words, is currently monitored). |
| emailList | nested object | Data for the related email(s), if any. |


