# Check an Email Address for Breaches

**Request method:** `POST`

**Request URL**: `https://megatron.com/api/enterprise/v1/email/check`

*You can avoid sending unencrypted email addresses by using the hashed email address values, as described [below](#hashed-email-check).*


**Email check** returns:

* Incidents count for **unverified** emails.
* Incidents count and details for **verified** emails.

How to construct the request:
1. Include the API key in the request header.
2. Specify your hashed email in the request body.

## Request and response examples

```shell
curl --location --request POST 'https://megatron.com/portal/api/v1/email/check' \
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
| email | string | Email you want to check. |



> Response for verified email

### Verified email response:

```
{
    "email": "test@test.com",
    "records": 21,
    "isAssigned": true,
    "incidents": [
        {
            "incidentId": 865,
            "title": "Collection #2 ",
            "createdAt": "2019-03-06T14:21:14.374Z",
            "compromisedAccounts": 866851442,
            "yearIncident": 2019,
            "monthIncident": 0,
            "url": "",
            "logo": "https://crm.megatron.com/images/uploads/gbWusP5Upun2DLam.svg",
            "description": "As a part of the January 7th 2019 BigDB database leak, Collection #2 exposed more than 800M unique emails and passwords. The BigDB database does not feature new incidents, it is an aggregate file old incidents with newly decrypted passwords which the infosec community couldn't crack before. The file consists of the incidented site data of the most famous services such as quifax, Marriot, Yahoo, LinkedIn, and eBay.",
            "incidentDataTypes": [
                "email",
                "plaintext password"
            ]
        }
    ]
}
 
```
| Name | Type | Description |
| ------ | ------ | ------ |
| email | string | Email that is checked. |
| records | integer | Email incidents count. |
| isAssigned | boolean | Email is verified the user: True/False. |
| incidents | [] | The  list of detailed incidents description. |
| incidentId | integer | The ID of the incident within MegaTron. |
| title | string | The title of the incident. |
| createdAt| string | The date the incident was added to our BR database. |
| compromisedAccounts | integer | The total number of compromised accounts. |
| yearIncident | integer | The year the incident occured. |
| monthIncident | integer | The month of the incident. |
| url | string | The URL to the sources of the incident. |
| logo | string | The logo of the incident. |
| description | string | Text description of the incident. |
| incidentDataTypes| [string] | The list of leaked data types within the incident. |

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