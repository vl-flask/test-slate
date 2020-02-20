# Check an Email Address for Breaches by SHA256 hash 

**Request method:** `POST`

**Request URL**: `{BASE_URL}/api/enterprise/v1/email-hash/check`

You can check an email address for breaches using a SHA256-encrypted email address value. This is  the recommended way to check email addresses for breaches using the Breach Report API.

Alternatively, you may check an email by using the [plaintext email address value](#plaintext-email-check). 

**Hashed email check** returns:
* Incidents count for **unverified** emails.
* Incidents count and further details for **verified** emails.

How to construct the request:
1. Calculate your email address hash using **SHA256**.
2. Include the API key in the request header.
3. Specify your hashed email address value in the request body.

### Hashing instruction
The Breach Report API only has access to encrypted email address values. The used encryption method is **Argond2d(SHA256(<email>))**.
Before sending a query, generate the email address hash.

How to produce an email address hash on Linux or Mac OS:
1. Convert your email to lowercase letters.
2. In the terminal, run the following command: `echo -n {email} | sha256sum`
Here, `{email}` is an email that you want to check. Don't use the brackets!
3. The command will produce a unique 64-character value that will look like: `8b063d4d3f323127ad8c13d42207269a747da2421db686144c5c982cc491e1ad`.

Alternatively, you may use an online hashing tool. For example, the [SHA256 tool on github.io](https://emn178.github.io/online-tools/sha256.html).

## Request and response examples

```shell
// Sample curl command

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
| hash | string | Hashed email address you want to check. |



> Verified email response

### Verified email response:
The output is the same as with checks by plaintext emails. 
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

> Response example: Unverified email

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