---
title: Incidentreport API
language_tabs:
  - shell : cURL
  - ruby
  - python
  - c
  - csharp : c#
  - go
  - http
  - java
  - javascript
  - php
  - swift

---
# Introduction

One morning, when Gregor Samsa woke from troubled dreams, he found himself transformed in his bed into a horrible vermin. 
Visit MegaTron [website](https://megatron.com) to see all the features.

> Request and response examples are presented at the right side with different programming languages and libreries tabs to be chosen from.

**Accessing the API**

The MegaTron API (v1) may be accessed by sending Secure HTTP GET/POST requests to URLs in the following format:
`https://megatron.com/api/v1/<resource>/<function>`, and passing the request payload.

For example, to check how many incidents we have for the email address test@test.com, you would send the following request:

`GET https://megatron.com/api/v1/email/check -d "email=test@test.com"`

	
**API interfaces:**

* Check an email for incidents.
* Check a domain for incidents.

*You will need to register at [MegaTron](https://megatron.com) prior to using our API.* 


# API-Key
All API calls require an `API Key` in the request header. To generate a key, do the following:
1. [Register](https://megatron.com/portal/signup) or [login](https://megatron.com/portal/login).
2. Open the [API section](https://megatron.com/portal/user-api). 
3. Click `Create key` to generate the key value. 
4. Include the generated key in each API call header.

*Note that you may need to upgrade your [Subscription](https://megatron.com/portal/subscriptions) to get more API calls.*

# Email check

**Request method:** `POST`

**Request URL**: `https://megatron.com/api/v1/email/check`


*To avoid passing plain email address over the network, we do recommend to use hashed email address search described [below](#hashed-email-check).*

**Email check** returns:

* Incidents count for **unverified** emails.
* Incidents count and details for **verified** emails.

The email check can be done in couple of steps:

1. Include API Key as an `API-Key` header.
2. Include your hashed email in body request.

## Request and response examples


```shell
curl --location --request POST 'https://megatron.com/portal/api/v1/email/check' \
--header 'api-key: 916f1847-6a59-4e1b-87fb-71c12231aacd' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--form 'email=test@test.com'
```

```c
CURL *curl;
CURLcode res;
curl = curl_easy_init();
if(curl) {
  curl_easy_setopt(curl, CURLOPT_CUSTOMREQUEST, "POST");
  curl_easy_setopt(curl, CURLOPT_URL, "https://megatron.com/portal/api/v1/email/check");
  curl_easy_setopt(curl, CURLOPT_FOLLOWLOCATION, 1L);
  curl_easy_setopt(curl, CURLOPT_DEFAULT_PROTOCOL, "https");
  struct curl_slist *headers = NULL;
  headers = curl_slist_append(headers, "api-key: 916f1847-6a59-4e1b-87fb-71c12231aacd");
  headers = curl_slist_append(headers, "Content-Type: application/x-www-form-urlencoded");
  curl_easy_setopt(curl, CURLOPT_HTTPHEADER, headers);
  curl_mime *mime;
  curl_mimepart *part;
  mime = curl_mime_init(curl);
  part = curl_mime_addpart(mime);
  curl_mime_name(part, "email");
  curl_mime_data(part, "test@test.com", CURL_ZERO_TERMINATED);
  curl_easy_setopt(curl, CURLOPT_MIMEPOST, mime);
  res = curl_easy_perform(curl);
  curl_mime_free(mime);
}
curl_easy_cleanup(curl);
```

```csharp

var client = new RestClient("https://megatron.com/portal/api/v1/email/check");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("api-key", "916f1847-6a59-4e1b-87fb-71c12231aacd");
request.AddHeader("Content-Type", "application/x-www-form-urlencoded");
request.AlwaysMultipartFormData = true;
request.AddParameter("email", "test@test.com");
IRestResponse response = client.Execute(request);
Console.WriteLine(response.Content);
```


```go

package main

import (
  "fmt"
  "bytes"
  "mime/multipart"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://megatron.com/portal/api/v1/email/check"
  method := "POST"

  payload := &bytes.Buffer{}
  writer := multipart.NewWriter(payload)
  _ = writer.WriteField("email", "test@test.com")
  err := writer.Close()
  if err != nil {
    fmt.Println(err)
  }


  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, payload)

  if err != nil {
    fmt.Println(err)
  }
  req.Header.Add("api-key", "916f1847-6a59-4e1b-87fb-71c12231aacd")
  req.Header.Add("Content-Type", "application/x-www-form-urlencoded")

  req.Header.Set("Content-Type", writer.FormDataContentType())
  res, err := client.Do(req)
  defer res.Body.Close()
  body, err := ioutil.ReadAll(res.Body)

  fmt.Println(string(body))
}
```

```http

POST /portal/api/v1/email/check HTTP/1.1
Host: megatron.com
api-key: 916f1847-6a59-4e1b-87fb-71c12231aacd
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW

----WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="email"

test@test.com
----WebKitFormBoundary7MA4YWxkTrZu0gW
```


```java

POST /portal/api/v1/email/check HTTP/1.1
Host: megatron.com
api-key: 916f1847-6a59-4e1b-87fb-71c12231aacd
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW

----WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="email"

test@test.com
----WebKitFormBoundary7MA4YWxkTrZu0gW
```


```javascript

---------
Fetch
---------

POST /portal/api/v1/email/check HTTP/1.1
Host: megatron.com
api-key: 916f1847-6a59-4e1b-87fb-71c12231aacd
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW

----WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="email"

test@test.com
----WebKitFormBoundary7MA4YWxkTrZu0gW
```


```javascript

============
NodeJS
============
POST /portal/api/v1/email/check HTTP/1.1
Host: megatron.com
api-key: 916f1847-6a59-4e1b-87fb-71c12231aacd
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW

----WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="email"

test@test.com
----WebKitFormBoundary7MA4YWxkTrZu0gW
```


```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://megatron.com/portal/api/v1/email/check",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => array('email' => 'test@test.com'),
  CURLOPT_HTTPHEADER => array(
    "api-key: 916f1847-6a59-4e1b-87fb-71c12231aacd",
    "Content-Type: application/x-www-form-urlencoded"
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```


```python

=======
http.client
=======

import http.client
import mimetypes
conn = http.client.HTTPSConnection("megatron.com")
dataList = []
boundary = 'wL36Yn8afVp8Ag7AmP8qZ0SA4n1v9T'
dataList.append('--' + boundary)
dataList.append('Content-Disposition: form-data; name=email;')

dataList.append('Content-Type: {}'.format('multipart/form-data'))
dataList.append('')

dataList.append("test@test.com")
dataList.append('--'+boundary+'--')
dataList.append('')
body = '\r\n'.join(dataList)
payload = body
headers = {
  'api-key': '916f1847-6a59-4e1b-87fb-71c12231aacd',
  'Content-Type': 'application/x-www-form-urlencoded',
  'Content-type': 'multipart/form-data; boundary={}'.format(boundary)
}
conn.request("POST", "/portal/api/v1/email/check", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))

=======
Requests
=======

import requests

url = "https://megatron.com/portal/api/v1/email/check"

payload = {'email': 'test@test.com'}
files = [

]
headers = {
  'api-key': '916f1847-6a59-4e1b-87fb-71c12231aacd',
  'Content-Type': 'application/x-www-form-urlencoded'
}

response = requests.request("POST", url, headers=headers, data = payload, files = files)

print(response.text.encode('utf8'))
```


```ruby
require "uri"
require "net/http"

url = URI("https://megatron.com/portal/api/v1/email/check")

https = Net::HTTP.new(url.host, url.port);
https.use_ssl = true

request = Net::HTTP::Post.new(url)
request["api-key"] = "916f1847-6a59-4e1b-87fb-71c12231aacd"
request["Content-Type"] = "application/x-www-form-urlencoded"
form_data = [['email', 'test@test.com']]
request.set_form form_data, 'multipart/form-data'
response = https.request(request)
puts response.read_body
```

```swift
import Foundation

var semaphore = DispatchSemaphore (value: 0)

let parameters = [
  [
    "key": "email",
    "value": "test@test.com",
    "type": "text"
  ]] as [[String : Any]]

let boundary = "Boundary-\(UUID().uuidString)"
var body = ""
var error: Error? = nil
for param in parameters {
  if param["disabled"] == nil {
    let paramName = param["key"]!
    body += "--\(boundary)\r\n"
    body += "Content-Disposition:form-data; name=\"\(paramName)\""
    let paramType = param["type"] as! String
    if paramType == "text" {
      let paramValue = param["value"] as! String
      body += "\r\n\r\n\(paramValue)\r\n"
    } else {
      let paramSrc = param["src"] as! String
      let fileData = try NSData(contentsOfFile:paramSrc, options:[]) as Data
      let fileContent = String(data: fileData, encoding: .utf8)!
      body += "; filename=\"\(paramSrc)\"\r\n"
        + "Content-Type: \"content-type header\"\r\n\r\n\(fileContent)\r\n"
    }
  }
}
body += "--\(boundary)--\r\n";
let postData = body.data(using: .utf8)

var request = URLRequest(url: URL(string: "https://megatron.com/portal/api/v1/email/check")!,timeoutInterval: Double.infinity)
request.addValue("916f1847-6a59-4e1b-87fb-71c12231aacd", forHTTPHeaderField: "api-key")
request.addValue("application/x-www-form-urlencoded", forHTTPHeaderField: "Content-Type")
request.addValue("multipart/form-data; boundary=\(boundary)", forHTTPHeaderField: "Content-Type")

request.httpMethod = "POST"
request.httpBody = postData

let task = URLSession.shared.dataTask(with: request) { data, response, error in 
  guard let data = data else {
    print(String(describing: error))
    return
  }
  print(String(data: data, encoding: .utf8)!)
  semaphore.signal()
}

task.resume()
semaphore.wait()
```


**Request parameters:**

| Name | Type | Description |
| ------ | ------ | ------ |
| api-key | string | An API Key retrieved from [Portal](https://megatron.com/portal/user-api). Should be included as `Header`. |
| email | string | Email you want to check. |



> Response example: Verified email

### Verified email response parameters:

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

> Reponse example: Unverified email

### Unverified email reponse:

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



# Hashed email check

**Request method:** `POST`

**Request URL:** `https://megatron.com/api/v1/email-hash/check`

**Hashed email check** returns:

* Incidents count for **unverified** emails.
* Incidents count and details for **verified** emails.

The email check can be done in couple of steps:

1. Hash your email with **SHA256**. 
2. Include API Key as an `API-Key` header.
3. Include your hashed email in body request.

### Hashing instructions

Information about emails stored in our DB is hashed with set of hashes **Argond2d(SHA256(<email>))**.

Before sending queries, make sure that you hashed your given email address with **SHA256**.

**Linux (Mac OS):**

1. Convert your email to lowercase letters.
2. Run the following command in shell terminal:

`echo -n {your email} | sha256sum`

Where `{your email}` is an email that you want to check. Note, that brackets should not be used. This command will hash email address with SHA256:


The SHA256 hash ourtput will look like: `8b063d4d3f323127ad8c13d42207269a747da2421db686144c5c982cc491e1ad`

**Online hashing tool:**

You can also use online tools for hashing. For example, [github.io](https://emn178.github.io/online-tools/sha256.html) source allows a wide variety for hashing.

## Request and response examples

```shell
curl --location --request POST 'https://megatron.com/api/v1/email-hash/check' \
--header 'authorization: 916f1847-6a59-4e1b-87fb-71c12231aacd' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--form 'hash=fbd845faf6845d53d1124e63b17844fd671eab996e5397bc6e1962ce3ca034t6'
```


```c
CURL *curl;
CURLcode res;
curl = curl_easy_init();
if(curl) {
  curl_easy_setopt(curl, CURLOPT_CUSTOMREQUEST, "POST");
  curl_easy_setopt(curl, CURLOPT_URL, "https://megatron.com/api/v1/email-hash/check");
  curl_easy_setopt(curl, CURLOPT_FOLLOWLOCATION, 1L);
  curl_easy_setopt(curl, CURLOPT_DEFAULT_PROTOCOL, "https");
  struct curl_slist *headers = NULL;
  headers = curl_slist_append(headers, "authorization: 916f1847-6a59-4e1b-87fb-71c12231aacd");
  headers = curl_slist_append(headers, "Content-Type: application/x-www-form-urlencoded");
  curl_easy_setopt(curl, CURLOPT_HTTPHEADER, headers);
  curl_mime *mime;
  curl_mimepart *part;
  mime = curl_mime_init(curl);
  part = curl_mime_addpart(mime);
  curl_mime_name(part, "hash");
  curl_mime_data(part, "fbd845faf6845d53d1124e63b17844fd671eab996e5397bc6e1962ce3ca034t6", CURL_ZERO_TERMINATED);
  curl_easy_setopt(curl, CURLOPT_MIMEPOST, mime);
  res = curl_easy_perform(curl);
  curl_mime_free(mime);
}
curl_easy_cleanup(curl);
```



```csharp
var client = new RestClient("https://megatron.com/api/v1/email-hash/check");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("authorization", "916f1847-6a59-4e1b-87fb-71c12231aacd");
request.AddHeader("Content-Type", "application/x-www-form-urlencoded");
request.AlwaysMultipartFormData = true;
request.AddParameter("hash", "fbd845faf6845d53d1124e63b17844fd671eab996e5397bc6e1962ce3ca034t6");
IRestResponse response = client.Execute(request);
Console.WriteLine(response.Content);
```

```go
package main

import (
  "fmt"
  "bytes"
  "mime/multipart"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://megatron.com/api/v1/email-hash/check"
  method := "POST"

  payload := &bytes.Buffer{}
  writer := multipart.NewWriter(payload)
  _ = writer.WriteField("hash", "fbd845faf6845d53d1124e63b17844fd671eab996e5397bc6e1962ce3ca034t6")
  err := writer.Close()
  if err != nil {
    fmt.Println(err)
  }


  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, payload)

  if err != nil {
    fmt.Println(err)
  }
  req.Header.Add("authorization", "916f1847-6a59-4e1b-87fb-71c12231aacd")
  req.Header.Add("Content-Type", "application/x-www-form-urlencoded")

  req.Header.Set("Content-Type", writer.FormDataContentType())
  res, err := client.Do(req)
  defer res.Body.Close()
  body, err := ioutil.ReadAll(res.Body)

  fmt.Println(string(body))
}
```

```http
POST /api/v1/email-hash/check HTTP/1.1
Host: megatron.com
authorization: 916f1847-6a59-4e1b-87fb-71c12231aacd
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW

----WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="hash"

fbd845faf6845d53d1124e63b17844fd671eab996e5397bc6e1962ce3ca034t6
----WebKitFormBoundary7MA4YWxkTrZu0gW
```



```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/x-www-form-urlencoded");
RequestBody body = new MultipartBody.Builder().setType(MultipartBody.FORM)
  .addFormDataPart("hash", "fbd845faf6845d53d1124e63b17844fd671eab996e5397bc6e1962ce3ca034t6")
  .build();
Request request = new Request.Builder()
  .url("https://megatron.com/api/v1/email-hash/check")
  .method("POST", body)
  .addHeader("authorization", "916f1847-6a59-4e1b-87fb-71c12231aacd")
  .addHeader("Content-Type", "application/x-www-form-urlencoded")
  .build();
Response response = client.newCall(request).execute();
```


```javascript
var myHeaders = new Headers();
myHeaders.append("authorization", "916f1847-6a59-4e1b-87fb-71c12231aacd");
myHeaders.append("Content-Type", "application/x-www-form-urlencoded");

var formdata = new FormData();
formdata.append("hash", "fbd845faf6845d53d1124e63b17844fd671eab996e5397bc6e1962ce3ca034t6");

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: formdata,
  redirect: 'follow'
};

fetch("https://megatron.com/api/v1/email-hash/check", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));```
```


```javascript

=======
NodeJS
=======

var https = require('follow-redirects').https;
var fs = require('fs');

var options = {
  'method': 'POST',
  'hostname': 'megatron.com',
  'path': '/api/v1/email-hash/check',
  'headers': {
    'authorization': '916f1847-6a59-4e1b-87fb-71c12231aacd',
    'Content-Type': 'application/x-www-form-urlencoded'
  },
  'maxRedirects': 20
};

var req = https.request(options, function (res) {
  var chunks = [];

  res.on("data", function (chunk) {
    chunks.push(chunk);
  });

  res.on("end", function (chunk) {
    var body = Buffer.concat(chunks);
    console.log(body.toString());
  });

  res.on("error", function (error) {
    console.error(error);
  });
});

var postData = "------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"hash\"\r\n\r\nfbd845faf6845d53d1124e63b17844fd671eab996e5397bc6e1962ce3ca034t6\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW--";

req.setHeader('content-type', 'multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW');

req.write(postData);

req.end();
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://megatron.com/api/v1/email-hash/check",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => array('hash' => 'fbd845faf6845d53d1124e63b17844fd671eab996e5397bc6e1962ce3ca034t6'),
  CURLOPT_HTTPHEADER => array(
    "authorization: 916f1847-6a59-4e1b-87fb-71c12231aacd",
    "Content-Type: application/x-www-form-urlencoded"
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```python
=======
http.client
=======

import http.client
import mimetypes
conn = http.client.HTTPSConnection("megatron.com")
dataList = []
boundary = 'wL36Yn8afVp8Ag7AmP8qZ0SA4n1v9T'
dataList.append('--' + boundary)
dataList.append('Content-Disposition: form-data; name=hash;')

dataList.append('Content-Type: {}'.format('multipart/form-data'))
dataList.append('')

dataList.append("fbd845faf6845d53d1124e63b17844fd671eab996e5397bc6e1962ce3ca034t6")
dataList.append('--'+boundary+'--')
dataList.append('')
body = '\r\n'.join(dataList)
payload = body
headers = {
  'authorization': '916f1847-6a59-4e1b-87fb-71c12231aacd',
  'Content-Type': 'application/x-www-form-urlencoded',
  'Content-type': 'multipart/form-data; boundary={}'.format(boundary)
}
conn.request("POST", "/api/v1/email-hash/check", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

```python
=======
Requests
=======

import requests

url = "https://megatron.com/api/v1/email-hash/check"

payload = {'hash': 'fbd845faf6845d53d1124e63b17844fd671eab996e5397bc6e1962ce3ca034t6'}
files = [

]
headers = {
  'authorization': '916f1847-6a59-4e1b-87fb-71c12231aacd',
  'Content-Type': 'application/x-www-form-urlencoded'
}

response = requests.request("POST", url, headers=headers, data = payload, files = files)

print(response.text.encode('utf8'))
```

```ruby
require "uri"
require "net/http"

url = URI("https://megatron.com/api/v1/email-hash/check")

https = Net::HTTP.new(url.host, url.port);
https.use_ssl = true

request = Net::HTTP::Post.new(url)
request["authorization"] = "916f1847-6a59-4e1b-87fb-71c12231aacd"
request["Content-Type"] = "application/x-www-form-urlencoded"
form_data = [['hash', 'fbd845faf6845d53d1124e63b17844fd671eab996e5397bc6e1962ce3ca034t6']]
request.set_form form_data, 'multipart/form-data'
response = https.request(request)
puts response.read_body
```

```swift
import Foundation

var semaphore = DispatchSemaphore (value: 0)

let parameters = [
  [
    "key": "hash",
    "value": "fbd845faf6845d53d1124e63b17844fd671eab996e5397bc6e1962ce3ca034t6",
    "type": "text"
  ]] as [[String : Any]]

let boundary = "Boundary-\(UUID().uuidString)"
var body = ""
var error: Error? = nil
for param in parameters {
  if param["disabled"] == nil {
    let paramName = param["key"]!
    body += "--\(boundary)\r\n"
    body += "Content-Disposition:form-data; name=\"\(paramName)\""
    let paramType = param["type"] as! String
    if paramType == "text" {
      let paramValue = param["value"] as! String
      body += "\r\n\r\n\(paramValue)\r\n"
    } else {
      let paramSrc = param["src"] as! String
      let fileData = try NSData(contentsOfFile:paramSrc, options:[]) as Data
      let fileContent = String(data: fileData, encoding: .utf8)!
      body += "; filename=\"\(paramSrc)\"\r\n"
        + "Content-Type: \"content-type header\"\r\n\r\n\(fileContent)\r\n"
    }
  }
}
body += "--\(boundary)--\r\n";
let postData = body.data(using: .utf8)

var request = URLRequest(url: URL(string: "https://megatron.com/api/v1/email-hash/check")!,timeoutInterval: Double.infinity)
request.addValue("916f1847-6a59-4e1b-87fb-71c12231aacd", forHTTPHeaderField: "authorization")
request.addValue("application/x-www-form-urlencoded", forHTTPHeaderField: "Content-Type")
request.addValue("multipart/form-data; boundary=\(boundary)", forHTTPHeaderField: "Content-Type")

request.httpMethod = "POST"
request.httpBody = postData

let task = URLSession.shared.dataTask(with: request) { data, response, error in 
  guard let data = data else {
    print(String(describing: error))
    return
  }
  print(String(data: data, encoding: .utf8)!)
  semaphore.signal()
}

task.resume()
semaphore.wait()
```


**Request parameters:**

| Name | Type | Description |
| ------ | ------ | ------ |
| API-Key | string | An API Key retrieved from [Portal](https://megatron.com/portal/user-api). Should be included as `Header`. |
| hash | string | SHA-256 hash of your email. |

> Response example: Verified example

### Verified email reponse
```json
{
    "hash": "fbd845faf6845d53d1124e63b17844fd671eab996e5397bc6e1962ce3ca034t6",
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
| hash | string | SHA256 of email that is checked. |
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

### Unverified email reposnse:

```
{
	“emailHash":"8b063d4d3f323127ad8c13d42207269a747da2421db686144c5c982cc491e1da",
	"records":27,
	"isAssigned":false,
	"incidents":null
} 
```


| Name | Type | Description |
| ------ | ------ | ------ |
| emailHash | string | SHA-256 hash of your email. |
| records | integer | Incidents count. |
| isAssigned | boolean | Email verified by a user: true/false. |
| incidents | null / {} | Detailed incident information. If `isAssigned = false`, then incidents will be null. |


