---
title: CRO Software API
language_tabs:
  - shell: Shell
  - http: HTTP
  - javascript: JavaScript
  - javascript--nodejs: Node.JS
  - ruby: Ruby
  - python: Python
  - java: Java
  - go: Go
toc_footers: []
includes: []
search: true
highlight_theme: darkula
headingLevel: 2

---

<h1 id="cro-software-api">CRO Software API v0.0.1</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

Build on & integrate with CRO Software.

Base URLs:

* <a href="http://localhost:8003">http://localhost:8003</a>

Email: <a href="mailto:develop@crosoftware.net">Support</a> 
License: <a href="http://www.apache.org/licenses/LICENSE-2.0.html">Apache 2.0</a>

# Authentication

- HTTP Authentication, scheme: bearer 

<h1 id="cro-software-api-dispatch">Dispatch</h1>

For 3rd party integration with CRO

## Locations

<a id="opIdlist_locations"></a>

> Code samples

```shell
# You can also use wget
curl -X GET http://localhost:8003/location \
  -H 'Accept: application/json' \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
GET http://localhost:8003/location HTTP/1.1
Host: localhost:8003
Accept: application/json
X-TENANT-ID: 1

```

```javascript
var headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'http://localhost:8003/location',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('http://localhost:8003/location', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "http://localhost:8003/location", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### GET /location

List locations for tenant.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|

> Example responses

> 200 Response

```json
[
  {
    "id": 1,
    "is_active": true,
    "name": "Sequim",
    "test": "Q1JPIFNvZnR3YXJl"
  }
]
```

> 400 Response

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Inline|List of locations|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

<h3 id="undefined-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[LocationModel](#schemalocationmodel)]|false|none|none|
|» id|integer(int64)|false|none|none|
|» is_active|boolean|false|none|none|
|» name|string|false|none|none|
|» test|string(byte)|false|none|none|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdlist_locations_options"></a>

> Code samples

```shell
# You can also use wget
curl -X OPTIONS http://localhost:8003/location \
  -H 'Authorization: Bearer {access-token}'

```

```http
OPTIONS http://localhost:8003/location HTTP/1.1
Host: localhost:8003

```

```javascript
var headers = {
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location',
  method: 'options',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location',
{
  method: 'OPTIONS',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.options 'http://localhost:8003/location',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'Bearer {access-token}'
}

r = requests.options('http://localhost:8003/location', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("OPTIONS");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("OPTIONS", "http://localhost:8003/location", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### OPTIONS /location

List HTTP operations.

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Headers|string||Comma separated list of access control headers.|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdlist_locations_head"></a>

> Code samples

```shell
# You can also use wget
curl -X HEAD http://localhost:8003/location \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
HEAD http://localhost:8003/location HTTP/1.1
Host: localhost:8003

X-TENANT-ID: 1

```

```javascript
var headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location',
  method: 'head',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location',
{
  method: 'HEAD',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.head 'http://localhost:8003/location',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.head('http://localhost:8003/location', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("HEAD");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("HEAD", "http://localhost:8003/location", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### HEAD /location

HTTP head

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## Location

<a id="opIdget_location"></a>

> Code samples

```shell
# You can also use wget
curl -X GET http://localhost:8003/location/{location_id} \
  -H 'Accept: application/json' \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
GET http://localhost:8003/location/{location_id} HTTP/1.1
Host: localhost:8003
Accept: application/json
X-TENANT-ID: 1

```

```javascript
var headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'http://localhost:8003/location/{location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('http://localhost:8003/location/{location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "http://localhost:8003/location/{location_id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### GET /location/{location_id}

Get info for specified location.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|

> Example responses

> 200 Response

```json
{
  "id": 1,
  "is_active": true,
  "name": "Sequim",
  "test": "Q1JPIFNvZnR3YXJl"
}
```

> 400 Response

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[LocationModel](#schemalocationmodel)|Location info.|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdlocation_options"></a>

> Code samples

```shell
# You can also use wget
curl -X OPTIONS http://localhost:8003/location/{location_id} \
  -H 'Authorization: Bearer {access-token}'

```

```http
OPTIONS http://localhost:8003/location/{location_id} HTTP/1.1
Host: localhost:8003

```

```javascript
var headers = {
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}',
  method: 'options',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}',
{
  method: 'OPTIONS',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.options 'http://localhost:8003/location/{location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'Bearer {access-token}'
}

r = requests.options('http://localhost:8003/location/{location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("OPTIONS");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("OPTIONS", "http://localhost:8003/location/{location_id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### OPTIONS /location/{location_id}

List HTTP operations.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Headers|string||Comma separated list of access control headers.|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdlocation_head"></a>

> Code samples

```shell
# You can also use wget
curl -X HEAD http://localhost:8003/location/{location_id} \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
HEAD http://localhost:8003/location/{location_id} HTTP/1.1
Host: localhost:8003

X-TENANT-ID: 1

```

```javascript
var headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}',
  method: 'head',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}',
{
  method: 'HEAD',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.head 'http://localhost:8003/location/{location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.head('http://localhost:8003/location/{location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("HEAD");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("HEAD", "http://localhost:8003/location/{location_id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### HEAD /location/{location_id}

HTTP head

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## Jobs

<a id="opIdlist_jobs_for_location"></a>

> Code samples

```shell
# You can also use wget
curl -X GET http://localhost:8003/location/{location_id}/job \
  -H 'Accept: application/json' \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
GET http://localhost:8003/location/{location_id}/job HTTP/1.1
Host: localhost:8003
Accept: application/json
X-TENANT-ID: 1

```

```javascript
var headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/job',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/job',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'http://localhost:8003/location/{location_id}/job',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('http://localhost:8003/location/{location_id}/job', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/job");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "http://localhost:8003/location/{location_id}/job", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### GET /location/{location_id}/job

List jobs for location.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|
|page_limit|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 < PageLimit < 1000.|
|page_index|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

> Example responses

> 200 Response

```json
{
  "current_limit": 1,
  "current_page": 1,
  "results": [
    {
      "arrived_at_dest": "2018-11-18T19:54:55.327000",
      "arrived_on": "2018-11-18T19:54:55.327000",
      "asset_dropped": 1,
      "asset_id": 1,
      "asset_quantity": 1,
      "asset_type_id": 1,
      "completed_by": 1,
      "completed_by_driver": false,
      "completed_on": "2018-11-18T19:54:55.327000",
      "confirmed_on": "2018-11-18T19:54:55.327000",
      "created_by_id": 1,
      "created_with_portal": false,
      "customer_id": 9,
      "customer_notes": "Some customer notes",
      "departed_on": "2018-11-18T19:54:55.327000",
      "desired_asset_desc": "An asset description.",
      "dispatch_priority": "H",
      "dispatched_by_route": 1,
      "dispatched_on": "2018-11-18T19:54:55.327000",
      "dispatcher_notes": "Some dispatcher notes",
      "do_confirm": false,
      "driver_notes": "Some driver notes",
      "dropped_number": "Unused/deprecated field",
      "dump_location_id": 1,
      "dumped_on": "2018-11-18T19:54:55.327000",
      "end_time": "2018-11-18T19:54:55.327000",
      "fail_reason": "Failure reason",
      "final_location_id": 1,
      "flags": "Job notes",
      "id": 1,
      "invoice_notes": "Some invoice notes",
      "is_completed": false,
      "is_declined": false,
      "is_deleted": false,
      "is_failed": false,
      "is_paid": true,
      "job_group_id": 1,
      "location_id": 1,
      "merged_with_route": 1,
      "original_schedule_date": "2018-10-31T11:34:13.690000",
      "pickup_date": "2018-10-31T11:34:13.690000",
      "priority": -1,
      "reference_number": null,
      "removed_number": "string",
      "requested_on": "2018-10-31T11:33:52.920000",
      "require_image": false,
      "require_material": false,
      "require_signature": false,
      "require_weights": false,
      "schedule_date": "2018-10-31T00:00:00",
      "start_location_id": 1,
      "start_time": "2018-10-31T11:33:52.920000",
      "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "times_failed": 0,
      "times_rolled_over": 0,
      "truck_id": 1,
      "type": "D",
      "weighed_on": "2018-10-31T11:33:52.920000",
      "asset": {
        "asset_type": {
          "deleted": false,
          "id": 1,
          "is_default": false,
          "location_id": 1,
          "name": "10 yrd",
          "quantity": 2,
          "require_numbers": true,
          "weight": 3245
        },
        "asset_type_id": 1,
        "cluster": 1,
        "customer_id": 1,
        "description": "A description",
        "dispatched_on": "2019-01-04T20:56:01.857Z",
        "id": 1,
        "is_returned": false,
        "last_activity_on": "2019-01-04T20:56:01.857Z",
        "last_rental_invoice_on": "2019-01-04T20:56:01.857Z",
        "latitude": 54.235,
        "location": {
          "id": 1,
          "is_active": true,
          "name": "Sequim",
          "test": "Q1JPIFNvZnR3YXJl"
        },
        "location_id": 1,
        "longitude": 127.123,
        "number": "REF100",
        "quantity": 1,
        "returned_on": "2019-01-04T20:56:01.857Z"
      },
      "asset_type": {
        "deleted": false,
        "id": 1,
        "is_default": false,
        "location_id": 1,
        "name": "10 yrd",
        "quantity": 2,
        "require_numbers": true,
        "weight": 3245
      },
      "customer": {
        "addresses": [
          {
            "address": {
              "country": "usa",
              "id": 9,
              "latitude": 48.0854948,
              "line_1": "610 N 5th Ave",
              "line_2": "P.O. Box 123",
              "line_3": "Suite 1",
              "line_4": "1st Floor",
              "locality": "Sequim",
              "longitude": -123.11221510000001,
              "postcode": 98382,
              "region": "WA"
            },
            "address_id": 9,
            "customer_id": 9,
            "is_active": true,
            "is_billing": false,
            "is_physical": true,
            "is_shipping": true
          }
        ],
        "created_on": "2019-01-04T20:56:01.858Z",
        "id": 9,
        "locations": [
          {
            "created_on": "2019-01-04T20:56:01.858Z",
            "customer_id": 9,
            "is_active": true,
            "is_commercial": false,
            "last_edited": "2019-01-04T20:56:01.858Z",
            "location_id": 1,
            "note": "string",
            "reference_number": "string",
            "renewal_date": "string",
            "sales_rep": "string",
            "suspension_id": "string"
          }
        ],
        "name": "YMCA",
        "parent_id": 8
      },
      "dump_location": {
        "address": "123 Sequim Ave.",
        "city": "Sequim",
        "contact_email": "support@crosoftware.net",
        "contact_name": "John Doe",
        "contact_phone": "(706) 360-7109",
        "id": 1,
        "is_holding_yard": true,
        "latitude": 128.123,
        "location": {
          "id": 1,
          "is_active": true,
          "name": "Sequim",
          "test": "Q1JPIFNvZnR3YXJl"
        },
        "location_id": 1,
        "longitude": 54.234,
        "name": "A Destination",
        "state": "Washington",
        "zip": 98368
      },
      "final_location": {
        "address": "123 Sequim Ave.",
        "city": "Sequim",
        "contact_email": "support@crosoftware.net",
        "contact_name": "John Doe",
        "contact_phone": "(706) 360-7109",
        "id": 1,
        "is_holding_yard": true,
        "latitude": 128.123,
        "location": {
          "id": 1,
          "is_active": true,
          "name": "Sequim",
          "test": "Q1JPIFNvZnR3YXJl"
        },
        "location_id": 1,
        "longitude": 54.234,
        "name": "A Destination",
        "state": "Washington",
        "zip": 98368
      },
      "start_location": {
        "address": "123 Sequim Ave.",
        "city": "Sequim",
        "contact_email": "support@crosoftware.net",
        "contact_name": "John Doe",
        "contact_phone": "(706) 360-7109",
        "id": 1,
        "is_holding_yard": true,
        "latitude": 128.123,
        "location": {
          "id": 1,
          "is_active": true,
          "name": "Sequim",
          "test": "Q1JPIFNvZnR3YXJl"
        },
        "location_id": 1,
        "longitude": 54.234,
        "name": "A Destination",
        "state": "Washington",
        "zip": 98368
      }
    }
  ],
  "total_count": 1,
  "total_pages": 1
}
```

> 400 Response

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[JobListModel](#schemajoblistmodel)|List of jobs for location.|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdlocation_jobs_options"></a>

> Code samples

```shell
# You can also use wget
curl -X OPTIONS http://localhost:8003/location/{location_id}/job \
  -H 'Authorization: Bearer {access-token}'

```

```http
OPTIONS http://localhost:8003/location/{location_id}/job HTTP/1.1
Host: localhost:8003

```

```javascript
var headers = {
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/job',
  method: 'options',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/job',
{
  method: 'OPTIONS',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.options 'http://localhost:8003/location/{location_id}/job',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'Bearer {access-token}'
}

r = requests.options('http://localhost:8003/location/{location_id}/job', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/job");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("OPTIONS");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("OPTIONS", "http://localhost:8003/location/{location_id}/job", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### OPTIONS /location/{location_id}/job

List HTTP operations.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Headers|string||Comma separated list of access control headers.|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdlist_jobs_head"></a>

> Code samples

```shell
# You can also use wget
curl -X HEAD http://localhost:8003/location/{location_id}/job \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
HEAD http://localhost:8003/location/{location_id}/job HTTP/1.1
Host: localhost:8003

X-TENANT-ID: 1

```

```javascript
var headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/job',
  method: 'head',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/job',
{
  method: 'HEAD',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.head 'http://localhost:8003/location/{location_id}/job',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.head('http://localhost:8003/location/{location_id}/job', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/job");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("HEAD");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("HEAD", "http://localhost:8003/location/{location_id}/job", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### HEAD /location/{location_id}/job

HTTP head

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## Job

<a id="opIdget_job"></a>

> Code samples

```shell
# You can also use wget
curl -X GET http://localhost:8003/location/{location_id}/job/{job_id} \
  -H 'Accept: application/json' \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
GET http://localhost:8003/location/{location_id}/job/{job_id} HTTP/1.1
Host: localhost:8003
Accept: application/json
X-TENANT-ID: 1

```

```javascript
var headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/job/{job_id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/job/{job_id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'http://localhost:8003/location/{location_id}/job/{job_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('http://localhost:8003/location/{location_id}/job/{job_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/job/{job_id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "http://localhost:8003/location/{location_id}/job/{job_id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### GET /location/{location_id}/job/{job_id}

Get specified job.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|
|job_id|path|[RecordId](#schemarecordid)|true|Job identifier (internal).|

> Example responses

> 200 Response

```json
{
  "arrived_at_dest": "2018-11-18T19:54:55.327000",
  "arrived_on": "2018-11-18T19:54:55.327000",
  "asset_dropped": 1,
  "asset_id": 1,
  "asset_quantity": 1,
  "asset_type_id": 1,
  "completed_by": 1,
  "completed_by_driver": false,
  "completed_on": "2018-11-18T19:54:55.327000",
  "confirmed_on": "2018-11-18T19:54:55.327000",
  "created_by_id": 1,
  "created_with_portal": false,
  "customer_id": 9,
  "customer_notes": "Some customer notes",
  "departed_on": "2018-11-18T19:54:55.327000",
  "desired_asset_desc": "An asset description.",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2018-11-18T19:54:55.327000",
  "dispatcher_notes": "Some dispatcher notes",
  "do_confirm": false,
  "driver_notes": "Some driver notes",
  "dropped_number": "Unused/deprecated field",
  "dump_location_id": 1,
  "dumped_on": "2018-11-18T19:54:55.327000",
  "end_time": "2018-11-18T19:54:55.327000",
  "fail_reason": "Failure reason",
  "final_location_id": 1,
  "flags": "Job notes",
  "id": 1,
  "invoice_notes": "Some invoice notes",
  "is_completed": false,
  "is_declined": false,
  "is_deleted": false,
  "is_failed": false,
  "is_paid": true,
  "job_group_id": 1,
  "location_id": 1,
  "merged_with_route": 1,
  "original_schedule_date": "2018-10-31T11:34:13.690000",
  "pickup_date": "2018-10-31T11:34:13.690000",
  "priority": -1,
  "reference_number": null,
  "removed_number": "string",
  "requested_on": "2018-10-31T11:33:52.920000",
  "require_image": false,
  "require_material": false,
  "require_signature": false,
  "require_weights": false,
  "schedule_date": "2018-10-31T00:00:00",
  "start_location_id": 1,
  "start_time": "2018-10-31T11:33:52.920000",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "times_failed": 0,
  "times_rolled_over": 0,
  "truck_id": 1,
  "type": "D",
  "weighed_on": "2018-10-31T11:33:52.920000",
  "asset": {
    "asset_type": {
      "deleted": false,
      "id": 1,
      "is_default": false,
      "location_id": 1,
      "name": "10 yrd",
      "quantity": 2,
      "require_numbers": true,
      "weight": 3245
    },
    "asset_type_id": 1,
    "cluster": 1,
    "customer_id": 1,
    "description": "A description",
    "dispatched_on": "2019-01-04T20:56:01.862Z",
    "id": 1,
    "is_returned": false,
    "last_activity_on": "2019-01-04T20:56:01.862Z",
    "last_rental_invoice_on": "2019-01-04T20:56:01.862Z",
    "latitude": 54.235,
    "location": {
      "id": 1,
      "is_active": true,
      "name": "Sequim",
      "test": "Q1JPIFNvZnR3YXJl"
    },
    "location_id": 1,
    "longitude": 127.123,
    "number": "REF100",
    "quantity": 1,
    "returned_on": "2019-01-04T20:56:01.862Z"
  },
  "asset_type": {
    "deleted": false,
    "id": 1,
    "is_default": false,
    "location_id": 1,
    "name": "10 yrd",
    "quantity": 2,
    "require_numbers": true,
    "weight": 3245
  },
  "customer": {
    "addresses": [
      {
        "address": {
          "country": "usa",
          "id": 9,
          "latitude": 48.0854948,
          "line_1": "610 N 5th Ave",
          "line_2": "P.O. Box 123",
          "line_3": "Suite 1",
          "line_4": "1st Floor",
          "locality": "Sequim",
          "longitude": -123.11221510000001,
          "postcode": 98382,
          "region": "WA"
        },
        "address_id": 9,
        "customer_id": 9,
        "is_active": true,
        "is_billing": false,
        "is_physical": true,
        "is_shipping": true
      }
    ],
    "created_on": "2019-01-04T20:56:01.862Z",
    "id": 9,
    "locations": [
      {
        "created_on": "2019-01-04T20:56:01.862Z",
        "customer_id": 9,
        "is_active": true,
        "is_commercial": false,
        "last_edited": "2019-01-04T20:56:01.862Z",
        "location_id": 1,
        "note": "string",
        "reference_number": "string",
        "renewal_date": "string",
        "sales_rep": "string",
        "suspension_id": "string"
      }
    ],
    "name": "YMCA",
    "parent_id": 8
  },
  "dump_location": {
    "address": "123 Sequim Ave.",
    "city": "Sequim",
    "contact_email": "support@crosoftware.net",
    "contact_name": "John Doe",
    "contact_phone": "(706) 360-7109",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 128.123,
    "location": {
      "id": 1,
      "is_active": true,
      "name": "Sequim",
      "test": "Q1JPIFNvZnR3YXJl"
    },
    "location_id": 1,
    "longitude": 54.234,
    "name": "A Destination",
    "state": "Washington",
    "zip": 98368
  },
  "final_location": {
    "address": "123 Sequim Ave.",
    "city": "Sequim",
    "contact_email": "support@crosoftware.net",
    "contact_name": "John Doe",
    "contact_phone": "(706) 360-7109",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 128.123,
    "location": {
      "id": 1,
      "is_active": true,
      "name": "Sequim",
      "test": "Q1JPIFNvZnR3YXJl"
    },
    "location_id": 1,
    "longitude": 54.234,
    "name": "A Destination",
    "state": "Washington",
    "zip": 98368
  },
  "start_location": {
    "address": "123 Sequim Ave.",
    "city": "Sequim",
    "contact_email": "support@crosoftware.net",
    "contact_name": "John Doe",
    "contact_phone": "(706) 360-7109",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 128.123,
    "location": {
      "id": 1,
      "is_active": true,
      "name": "Sequim",
      "test": "Q1JPIFNvZnR3YXJl"
    },
    "location_id": 1,
    "longitude": 54.234,
    "name": "A Destination",
    "state": "Washington",
    "zip": 98368
  }
}
```

> 400 Response

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[JobModel](#schemajobmodel)|JobModel|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIddispatch_job"></a>

> Code samples

```shell
# You can also use wget
curl -X PATCH http://localhost:8003/location/{location_id}/job/{job_id}?truck_id=1 \
  -H 'Accept: application/json' \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
PATCH http://localhost:8003/location/{location_id}/job/{job_id}?truck_id=1 HTTP/1.1
Host: localhost:8003
Accept: application/json
X-TENANT-ID: 1

```

```javascript
var headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/job/{job_id}',
  method: 'patch',
  data: '?truck_id=1',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/job/{job_id}?truck_id=1',
{
  method: 'PATCH',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.patch 'http://localhost:8003/location/{location_id}/job/{job_id}',
  params: {
  'truck_id' => '[RecordId](#schemarecordid)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.patch('http://localhost:8003/location/{location_id}/job/{job_id}', params={
  'truck_id': '1'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/job/{job_id}?truck_id=1");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PATCH");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PATCH", "http://localhost:8003/location/{location_id}/job/{job_id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### PATCH /location/{location_id}/job/{job_id}

Dispatch job.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|
|job_id|path|[RecordId](#schemarecordid)|true|Job identifier (internal).|
|truck_id|query|[RecordId](#schemarecordid)|true|Truck identifier (internal).|
|future_job_schedule_date|query|[DateTime](#schemadatetime)|false|Future dispatch time for job.|

> Example responses

> 200 Response

```json
{
  "arrived_at_dest": "2018-11-18T19:54:55.327000",
  "arrived_on": "2018-11-18T19:54:55.327000",
  "asset_dropped": 1,
  "asset_id": 1,
  "asset_quantity": 1,
  "asset_type_id": 1,
  "completed_by": 1,
  "completed_by_driver": false,
  "completed_on": "2018-11-18T19:54:55.327000",
  "confirmed_on": "2018-11-18T19:54:55.327000",
  "created_by_id": 1,
  "created_with_portal": false,
  "customer_id": 9,
  "customer_notes": "Some customer notes",
  "departed_on": "2018-11-18T19:54:55.327000",
  "desired_asset_desc": "An asset description.",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2018-11-18T19:54:55.327000",
  "dispatcher_notes": "Some dispatcher notes",
  "do_confirm": false,
  "driver_notes": "Some driver notes",
  "dropped_number": "Unused/deprecated field",
  "dump_location_id": 1,
  "dumped_on": "2018-11-18T19:54:55.327000",
  "end_time": "2018-11-18T19:54:55.327000",
  "fail_reason": "Failure reason",
  "final_location_id": 1,
  "flags": "Job notes",
  "id": 1,
  "invoice_notes": "Some invoice notes",
  "is_completed": false,
  "is_declined": false,
  "is_deleted": false,
  "is_failed": false,
  "is_paid": true,
  "job_group_id": 1,
  "location_id": 1,
  "merged_with_route": 1,
  "original_schedule_date": "2018-10-31T11:34:13.690000",
  "pickup_date": "2018-10-31T11:34:13.690000",
  "priority": -1,
  "reference_number": null,
  "removed_number": "string",
  "requested_on": "2018-10-31T11:33:52.920000",
  "require_image": false,
  "require_material": false,
  "require_signature": false,
  "require_weights": false,
  "schedule_date": "2018-10-31T00:00:00",
  "start_location_id": 1,
  "start_time": "2018-10-31T11:33:52.920000",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "times_failed": 0,
  "times_rolled_over": 0,
  "truck_id": 1,
  "type": "D",
  "weighed_on": "2018-10-31T11:33:52.920000"
}
```

> 400 Response

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[UpdatedJobModel](#schemaupdatedjobmodel)|UpdatedJobModel|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdget_job_options"></a>

> Code samples

```shell
# You can also use wget
curl -X OPTIONS http://localhost:8003/location/{location_id}/job/{job_id} \
  -H 'Authorization: Bearer {access-token}'

```

```http
OPTIONS http://localhost:8003/location/{location_id}/job/{job_id} HTTP/1.1
Host: localhost:8003

```

```javascript
var headers = {
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/job/{job_id}',
  method: 'options',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/job/{job_id}',
{
  method: 'OPTIONS',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.options 'http://localhost:8003/location/{location_id}/job/{job_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'Bearer {access-token}'
}

r = requests.options('http://localhost:8003/location/{location_id}/job/{job_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/job/{job_id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("OPTIONS");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("OPTIONS", "http://localhost:8003/location/{location_id}/job/{job_id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### OPTIONS /location/{location_id}/job/{job_id}

List HTTP operations.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|
|job_id|path|[RecordId](#schemarecordid)|true|Job identifier (internal).|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Headers|string||Comma separated list of access control headers.|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdget_job_head"></a>

> Code samples

```shell
# You can also use wget
curl -X HEAD http://localhost:8003/location/{location_id}/job/{job_id} \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
HEAD http://localhost:8003/location/{location_id}/job/{job_id} HTTP/1.1
Host: localhost:8003

X-TENANT-ID: 1

```

```javascript
var headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/job/{job_id}',
  method: 'head',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/job/{job_id}',
{
  method: 'HEAD',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.head 'http://localhost:8003/location/{location_id}/job/{job_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.head('http://localhost:8003/location/{location_id}/job/{job_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/job/{job_id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("HEAD");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("HEAD", "http://localhost:8003/location/{location_id}/job/{job_id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### HEAD /location/{location_id}/job/{job_id}

HTTP head

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|
|job_id|path|[RecordId](#schemarecordid)|true|Job identifier (internal).|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## Trucks

<a id="opIdlist_trucks_for_location"></a>

> Code samples

```shell
# You can also use wget
curl -X GET http://localhost:8003/location/{location_id}/truck \
  -H 'Accept: application/json' \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
GET http://localhost:8003/location/{location_id}/truck HTTP/1.1
Host: localhost:8003
Accept: application/json
X-TENANT-ID: 1

```

```javascript
var headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/truck',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/truck',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'http://localhost:8003/location/{location_id}/truck',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('http://localhost:8003/location/{location_id}/truck', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/truck");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "http://localhost:8003/location/{location_id}/truck", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### GET /location/{location_id}/truck

List trucks for location.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "driver_id": 1,
      "id": 2,
      "location_id": 1,
      "name": "ZachTruck",
      "notes": "Sequim",
      "out_of_service": false,
      "require_odometer": false,
      "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "type": "AwesomeTRUCK Rolloff",
      "weight": 18678
    }
  ],
  "total_count": 1,
  "total_pages": 1
}
```

> 400 Response

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TruckListModel](#schematrucklistmodel)|List of trucks for location.|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdlist_trucks_options"></a>

> Code samples

```shell
# You can also use wget
curl -X OPTIONS http://localhost:8003/location/{location_id}/truck \
  -H 'Authorization: Bearer {access-token}'

```

```http
OPTIONS http://localhost:8003/location/{location_id}/truck HTTP/1.1
Host: localhost:8003

```

```javascript
var headers = {
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/truck',
  method: 'options',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/truck',
{
  method: 'OPTIONS',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.options 'http://localhost:8003/location/{location_id}/truck',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'Bearer {access-token}'
}

r = requests.options('http://localhost:8003/location/{location_id}/truck', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/truck");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("OPTIONS");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("OPTIONS", "http://localhost:8003/location/{location_id}/truck", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### OPTIONS /location/{location_id}/truck

List HTTP operations.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Headers|string||Comma separated list of access control headers.|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdlist_trucks_head"></a>

> Code samples

```shell
# You can also use wget
curl -X HEAD http://localhost:8003/location/{location_id}/truck \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
HEAD http://localhost:8003/location/{location_id}/truck HTTP/1.1
Host: localhost:8003

X-TENANT-ID: 1

```

```javascript
var headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/truck',
  method: 'head',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/truck',
{
  method: 'HEAD',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.head 'http://localhost:8003/location/{location_id}/truck',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.head('http://localhost:8003/location/{location_id}/truck', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/truck");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("HEAD");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("HEAD", "http://localhost:8003/location/{location_id}/truck", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### HEAD /location/{location_id}/truck

HTTP head

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## Truck

<a id="opIdget_truck"></a>

> Code samples

```shell
# You can also use wget
curl -X GET http://localhost:8003/location/{location_id}/truck/{truck_id} \
  -H 'Accept: application/json' \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
GET http://localhost:8003/location/{location_id}/truck/{truck_id} HTTP/1.1
Host: localhost:8003
Accept: application/json
X-TENANT-ID: 1

```

```javascript
var headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/truck/{truck_id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/truck/{truck_id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'http://localhost:8003/location/{location_id}/truck/{truck_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('http://localhost:8003/location/{location_id}/truck/{truck_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/truck/{truck_id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "http://localhost:8003/location/{location_id}/truck/{truck_id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### GET /location/{location_id}/truck/{truck_id}

Get truck info.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|
|truck_id|path|[RecordId](#schemarecordid)|true|Truck identifier (internal).|

> Example responses

> 200 Response

```json
{
  "driver_id": 1,
  "id": 2,
  "location_id": 1,
  "name": "ZachTruck",
  "notes": "Sequim",
  "out_of_service": false,
  "require_odometer": false,
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "type": "AwesomeTRUCK Rolloff",
  "weight": 18678
}
```

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|string|Truck info.|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdset_truck_driver"></a>

> Code samples

```shell
# You can also use wget
curl -X PATCH http://localhost:8003/location/{location_id}/truck/{truck_id}?driver_id=1 \
  -H 'Accept: application/json' \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
PATCH http://localhost:8003/location/{location_id}/truck/{truck_id}?driver_id=1 HTTP/1.1
Host: localhost:8003
Accept: application/json
X-TENANT-ID: 1

```

```javascript
var headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/truck/{truck_id}',
  method: 'patch',
  data: '?driver_id=1',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/truck/{truck_id}?driver_id=1',
{
  method: 'PATCH',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.patch 'http://localhost:8003/location/{location_id}/truck/{truck_id}',
  params: {
  'driver_id' => '[RecordId](#schemarecordid)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.patch('http://localhost:8003/location/{location_id}/truck/{truck_id}', params={
  'driver_id': '1'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/truck/{truck_id}?driver_id=1");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PATCH");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PATCH", "http://localhost:8003/location/{location_id}/truck/{truck_id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### PATCH /location/{location_id}/truck/{truck_id}

Set driver for truck.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|
|truck_id|path|[RecordId](#schemarecordid)|true|Truck identifier (internal).|
|driver_id|query|[RecordId](#schemarecordid)|true|Location identifier (internal).|

> Example responses

> 200 Response

```json
{
  "driver_id": 1,
  "id": 2,
  "location_id": 1,
  "name": "ZachTruck",
  "notes": "Sequim",
  "out_of_service": false,
  "require_odometer": false,
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "type": "AwesomeTRUCK Rolloff",
  "weight": 18678
}
```

> 400 Response

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TruckModel](#schematruckmodel)|Updated truck profile.|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdget_truck_options"></a>

> Code samples

```shell
# You can also use wget
curl -X OPTIONS http://localhost:8003/location/{location_id}/truck/{truck_id} \
  -H 'Authorization: Bearer {access-token}'

```

```http
OPTIONS http://localhost:8003/location/{location_id}/truck/{truck_id} HTTP/1.1
Host: localhost:8003

```

```javascript
var headers = {
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/truck/{truck_id}',
  method: 'options',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/truck/{truck_id}',
{
  method: 'OPTIONS',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.options 'http://localhost:8003/location/{location_id}/truck/{truck_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'Bearer {access-token}'
}

r = requests.options('http://localhost:8003/location/{location_id}/truck/{truck_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/truck/{truck_id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("OPTIONS");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("OPTIONS", "http://localhost:8003/location/{location_id}/truck/{truck_id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### OPTIONS /location/{location_id}/truck/{truck_id}

List HTTP operations.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|
|truck_id|path|[RecordId](#schemarecordid)|true|Truck identifier (internal).|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Headers|string||Comma separated list of access control headers.|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdget_truck_head"></a>

> Code samples

```shell
# You can also use wget
curl -X HEAD http://localhost:8003/location/{location_id}/truck/{truck_id} \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
HEAD http://localhost:8003/location/{location_id}/truck/{truck_id} HTTP/1.1
Host: localhost:8003

X-TENANT-ID: 1

```

```javascript
var headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/truck/{truck_id}',
  method: 'head',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/truck/{truck_id}',
{
  method: 'HEAD',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.head 'http://localhost:8003/location/{location_id}/truck/{truck_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.head('http://localhost:8003/location/{location_id}/truck/{truck_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/truck/{truck_id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("HEAD");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("HEAD", "http://localhost:8003/location/{location_id}/truck/{truck_id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### HEAD /location/{location_id}/truck/{truck_id}

HTTP head

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|
|truck_id|path|[RecordId](#schemarecordid)|true|Truck identifier (internal).|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## Drivers

<a id="opIdlist_drivers_for_location"></a>

> Code samples

```shell
# You can also use wget
curl -X GET http://localhost:8003/location/{location_id}/driver \
  -H 'Accept: application/json' \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
GET http://localhost:8003/location/{location_id}/driver HTTP/1.1
Host: localhost:8003
Accept: application/json
X-TENANT-ID: 1

```

```javascript
var headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/driver',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/driver',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'http://localhost:8003/location/{location_id}/driver',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('http://localhost:8003/location/{location_id}/driver', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/driver");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "http://localhost:8003/location/{location_id}/driver", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### GET /location/{location_id}/driver

List drivers for location.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "address": "1234 Cro St",
      "can_convert_to_group": false,
      "can_create_requests": false,
      "can_edit_requests": false,
      "can_reposition_asset": false,
      "city": "Sequim",
      "disable_shift_tracking": false,
      "email": "john@crosoftware.net",
      "id": 2,
      "license_number": "123ABC",
      "location_id": 1,
      "name": "John Denver",
      "phone_number": "(360) 718-1234",
      "state": "WA",
      "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "zip": 98368
    }
  ],
  "total_count": 1,
  "total_pages": 1
}
```

> 400 Response

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DriverListModel](#schemadriverlistmodel)|List of drivers for location.|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdlist_drivers_options"></a>

> Code samples

```shell
# You can also use wget
curl -X OPTIONS http://localhost:8003/location/{location_id}/driver \
  -H 'Authorization: Bearer {access-token}'

```

```http
OPTIONS http://localhost:8003/location/{location_id}/driver HTTP/1.1
Host: localhost:8003

```

```javascript
var headers = {
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/driver',
  method: 'options',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/driver',
{
  method: 'OPTIONS',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.options 'http://localhost:8003/location/{location_id}/driver',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'Bearer {access-token}'
}

r = requests.options('http://localhost:8003/location/{location_id}/driver', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/driver");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("OPTIONS");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("OPTIONS", "http://localhost:8003/location/{location_id}/driver", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### OPTIONS /location/{location_id}/driver

List HTTP operations.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Headers|string||Comma separated list of access control headers.|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdlist_drivers_head"></a>

> Code samples

```shell
# You can also use wget
curl -X HEAD http://localhost:8003/location/{location_id}/driver \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
HEAD http://localhost:8003/location/{location_id}/driver HTTP/1.1
Host: localhost:8003

X-TENANT-ID: 1

```

```javascript
var headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/driver',
  method: 'head',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/driver',
{
  method: 'HEAD',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.head 'http://localhost:8003/location/{location_id}/driver',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.head('http://localhost:8003/location/{location_id}/driver', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/driver");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("HEAD");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("HEAD", "http://localhost:8003/location/{location_id}/driver", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### HEAD /location/{location_id}/driver

HTTP head

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## Customers

<a id="opIdlist_customers_for_location"></a>

> Code samples

```shell
# You can also use wget
curl -X GET http://localhost:8003/location/{location_id}/customer \
  -H 'Accept: application/json' \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
GET http://localhost:8003/location/{location_id}/customer HTTP/1.1
Host: localhost:8003
Accept: application/json
X-TENANT-ID: 1

```

```javascript
var headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/customer',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/customer',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'http://localhost:8003/location/{location_id}/customer',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('http://localhost:8003/location/{location_id}/customer', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/customer");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "http://localhost:8003/location/{location_id}/customer", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### GET /location/{location_id}/customer

List customers for location.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "addresses": [
        {
          "country": "USA",
          "is_active": true,
          "is_billing": true,
          "is_physical": false,
          "is_shipping": false,
          "latitude": 48.076273,
          "line_1": "643 Summer Breeze",
          "line_2": "Suite 34",
          "line_3": "2nd Door on Left",
          "line_4": "Blue slot",
          "locality": "Sequim",
          "longitude": -123.117185,
          "postcode": 98382,
          "region": "WA"
        }
      ],
      "contacts": [
        {
          "email": "nathan@crosoftware.com",
          "fax": "(360) 716-1968",
          "name": "John Doe",
          "notify_on_acknowledged_request": false,
          "notify_on_completed_request": false,
          "notify_on_dispatched_request": false,
          "notify_on_failed_request": false,
          "notify_on_new_request": false,
          "number": "1-111-111-1111"
        }
      ],
      "created_on": "2018-10-31T11:31:30.237000",
      "customer_id": 1,
      "is_active": false,
      "is_commercial": false,
      "last_edited": "2018-10-31T11:54:12.430000",
      "location_id": 1,
      "name": "HOLINC001",
      "note": "Service Location of Holland Inc.",
      "parent_id": 1,
      "reference_number": "Ref#100",
      "renewal_date": "2019-10-02T00:00:00",
      "sales_rep": "John Doe",
      "suspension_id": 1
    }
  ],
  "total_count": 100,
  "total_pages": 1
}
```

> 400 Response

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ListCustomerResultModel](#schemalistcustomerresultmodel)|Paged result sef of customers for location.|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdlist_customers_options"></a>

> Code samples

```shell
# You can also use wget
curl -X OPTIONS http://localhost:8003/location/{location_id}/customer \
  -H 'Authorization: Bearer {access-token}'

```

```http
OPTIONS http://localhost:8003/location/{location_id}/customer HTTP/1.1
Host: localhost:8003

```

```javascript
var headers = {
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/customer',
  method: 'options',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/customer',
{
  method: 'OPTIONS',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.options 'http://localhost:8003/location/{location_id}/customer',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'Bearer {access-token}'
}

r = requests.options('http://localhost:8003/location/{location_id}/customer', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/customer");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("OPTIONS");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("OPTIONS", "http://localhost:8003/location/{location_id}/customer", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### OPTIONS /location/{location_id}/customer

List HTTP operations.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Headers|string||Comma separated list of access control headers.|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdlist_customers_head"></a>

> Code samples

```shell
# You can also use wget
curl -X HEAD http://localhost:8003/location/{location_id}/customer \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
HEAD http://localhost:8003/location/{location_id}/customer HTTP/1.1
Host: localhost:8003

X-TENANT-ID: 1

```

```javascript
var headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/location/{location_id}/customer',
  method: 'head',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/location/{location_id}/customer',
{
  method: 'HEAD',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.head 'http://localhost:8003/location/{location_id}/customer',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.head('http://localhost:8003/location/{location_id}/customer', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/location/{location_id}/customer");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("HEAD");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("HEAD", "http://localhost:8003/location/{location_id}/customer", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### HEAD /location/{location_id}/customer

HTTP head

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|location_id|path|[RecordId](#schemarecordid)|true|Location identifier.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## Haulers

<a id="opIdlist_haulers"></a>

> Code samples

```shell
# You can also use wget
curl -X GET http://localhost:8003/hauler \
  -H 'Accept: application/json' \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
GET http://localhost:8003/hauler HTTP/1.1
Host: localhost:8003
Accept: application/json
X-TENANT-ID: 1

```

```javascript
var headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/hauler',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/hauler',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'http://localhost:8003/hauler',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('http://localhost:8003/hauler', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/hauler");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "http://localhost:8003/hauler", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### GET /hauler

List third party haulers for tenant.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "name": "SMS594"
    }
  ],
  "total_count": 1,
  "total_pages": 1
}
```

> 400 Response

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[HaulerListModel](#schemahaulerlistmodel)|List of third party haulers for tenant.|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdcreate_third_party_hauler"></a>

> Code samples

```shell
# You can also use wget
curl -X POST http://localhost:8003/hauler?company_name=Cro%20Scrap&username=test_user%40crosoftware.net&password=AnExample%21Password1000&recaptcha=string \
  -H 'Accept: application/json' \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
POST http://localhost:8003/hauler?company_name=Cro%20Scrap&username=test_user%40crosoftware.net&password=AnExample%21Password1000&recaptcha=string HTTP/1.1
Host: localhost:8003
Accept: application/json
X-TENANT-ID: 1

```

```javascript
var headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/hauler',
  method: 'post',
  data: '?company_name=Cro%20Scrap&username=test_user%40crosoftware.net&password=AnExample%21Password1000&recaptcha=string',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/hauler?company_name=Cro%20Scrap&username=test_user%40crosoftware.net&password=AnExample%21Password1000&recaptcha=string',
{
  method: 'POST',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.post 'http://localhost:8003/hauler',
  params: {
  'company_name' => 'string(stringIdentifier)',
'username' => 'string(email)',
'password' => 'string(password)',
'recaptcha' => 'string(recaptcha)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.post('http://localhost:8003/hauler', params={
  'company_name': 'Cro Scrap',  'username': 'test_user@crosoftware.net',  'password': 'AnExample!Password1000',  'recaptcha': 'string'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/hauler?company_name=Cro%20Scrap&username=test_user%40crosoftware.net&password=AnExample%21Password1000&recaptcha=string");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "http://localhost:8003/hauler", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### POST /hauler

Create 3rd Party hauler profile.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|company_name|query|string(stringIdentifier)|true|The comapny identifier issued at account creation. All caps, no spaces, no special characters.|
|username|query|string(email)|true|The email address registered for an account. Access control is based on the username.|
|password|query|string(password)|true|ASCII string. Min length 6, max length 32. |
|recaptcha|query|string(recaptcha)|true|ReCaptcha string.|

> Example responses

> 200 Response

```json
{
  "arrived_at_dest": "2018-11-18T19:54:55.327000",
  "arrived_on": "2018-11-18T19:54:55.327000",
  "asset_dropped": 1,
  "asset_id": 1,
  "asset_quantity": 1,
  "asset_type_id": 1,
  "completed_by": 1,
  "completed_by_driver": false,
  "completed_on": "2018-11-18T19:54:55.327000",
  "confirmed_on": "2018-11-18T19:54:55.327000",
  "created_by_id": 1,
  "created_with_portal": false,
  "customer_id": 9,
  "customer_notes": "Some customer notes",
  "departed_on": "2018-11-18T19:54:55.327000",
  "desired_asset_desc": "An asset description.",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2018-11-18T19:54:55.327000",
  "dispatcher_notes": "Some dispatcher notes",
  "do_confirm": false,
  "driver_notes": "Some driver notes",
  "dropped_number": "Unused/deprecated field",
  "dump_location_id": 1,
  "dumped_on": "2018-11-18T19:54:55.327000",
  "end_time": "2018-11-18T19:54:55.327000",
  "fail_reason": "Failure reason",
  "final_location_id": 1,
  "flags": "Job notes",
  "id": 1,
  "invoice_notes": "Some invoice notes",
  "is_completed": false,
  "is_declined": false,
  "is_deleted": false,
  "is_failed": false,
  "is_paid": true,
  "job_group_id": 1,
  "location_id": 1,
  "merged_with_route": 1,
  "original_schedule_date": "2018-10-31T11:34:13.690000",
  "pickup_date": "2018-10-31T11:34:13.690000",
  "priority": -1,
  "reference_number": null,
  "removed_number": "string",
  "requested_on": "2018-10-31T11:33:52.920000",
  "require_image": false,
  "require_material": false,
  "require_signature": false,
  "require_weights": false,
  "schedule_date": "2018-10-31T00:00:00",
  "start_location_id": 1,
  "start_time": "2018-10-31T11:33:52.920000",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "times_failed": 0,
  "times_rolled_over": 0,
  "truck_id": 1,
  "type": "D",
  "weighed_on": "2018-10-31T11:33:52.920000",
  "asset": {
    "asset_type": {
      "deleted": false,
      "id": 1,
      "is_default": false,
      "location_id": 1,
      "name": "10 yrd",
      "quantity": 2,
      "require_numbers": true,
      "weight": 3245
    },
    "asset_type_id": 1,
    "cluster": 1,
    "customer_id": 1,
    "description": "A description",
    "dispatched_on": "2019-01-04T20:56:01.870Z",
    "id": 1,
    "is_returned": false,
    "last_activity_on": "2019-01-04T20:56:01.870Z",
    "last_rental_invoice_on": "2019-01-04T20:56:01.870Z",
    "latitude": 54.235,
    "location": {
      "id": 1,
      "is_active": true,
      "name": "Sequim",
      "test": "Q1JPIFNvZnR3YXJl"
    },
    "location_id": 1,
    "longitude": 127.123,
    "number": "REF100",
    "quantity": 1,
    "returned_on": "2019-01-04T20:56:01.870Z"
  },
  "asset_type": {
    "deleted": false,
    "id": 1,
    "is_default": false,
    "location_id": 1,
    "name": "10 yrd",
    "quantity": 2,
    "require_numbers": true,
    "weight": 3245
  },
  "customer": {
    "addresses": [
      {
        "address": {
          "country": "usa",
          "id": 9,
          "latitude": 48.0854948,
          "line_1": "610 N 5th Ave",
          "line_2": "P.O. Box 123",
          "line_3": "Suite 1",
          "line_4": "1st Floor",
          "locality": "Sequim",
          "longitude": -123.11221510000001,
          "postcode": 98382,
          "region": "WA"
        },
        "address_id": 9,
        "customer_id": 9,
        "is_active": true,
        "is_billing": false,
        "is_physical": true,
        "is_shipping": true
      }
    ],
    "created_on": "2019-01-04T20:56:01.870Z",
    "id": 9,
    "locations": [
      {
        "created_on": "2019-01-04T20:56:01.870Z",
        "customer_id": 9,
        "is_active": true,
        "is_commercial": false,
        "last_edited": "2019-01-04T20:56:01.870Z",
        "location_id": 1,
        "note": "string",
        "reference_number": "string",
        "renewal_date": "string",
        "sales_rep": "string",
        "suspension_id": "string"
      }
    ],
    "name": "YMCA",
    "parent_id": 8
  },
  "dump_location": {
    "address": "123 Sequim Ave.",
    "city": "Sequim",
    "contact_email": "support@crosoftware.net",
    "contact_name": "John Doe",
    "contact_phone": "(706) 360-7109",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 128.123,
    "location": {
      "id": 1,
      "is_active": true,
      "name": "Sequim",
      "test": "Q1JPIFNvZnR3YXJl"
    },
    "location_id": 1,
    "longitude": 54.234,
    "name": "A Destination",
    "state": "Washington",
    "zip": 98368
  },
  "final_location": {
    "address": "123 Sequim Ave.",
    "city": "Sequim",
    "contact_email": "support@crosoftware.net",
    "contact_name": "John Doe",
    "contact_phone": "(706) 360-7109",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 128.123,
    "location": {
      "id": 1,
      "is_active": true,
      "name": "Sequim",
      "test": "Q1JPIFNvZnR3YXJl"
    },
    "location_id": 1,
    "longitude": 54.234,
    "name": "A Destination",
    "state": "Washington",
    "zip": 98368
  },
  "start_location": {
    "address": "123 Sequim Ave.",
    "city": "Sequim",
    "contact_email": "support@crosoftware.net",
    "contact_name": "John Doe",
    "contact_phone": "(706) 360-7109",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 128.123,
    "location": {
      "id": 1,
      "is_active": true,
      "name": "Sequim",
      "test": "Q1JPIFNvZnR3YXJl"
    },
    "location_id": 1,
    "longitude": 54.234,
    "name": "A Destination",
    "state": "Washington",
    "zip": 98368
  }
}
```

> 400 Response

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[JobModel](#schemajobmodel)|Third party hauler profile.|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdlist_haulers_options"></a>

> Code samples

```shell
# You can also use wget
curl -X OPTIONS http://localhost:8003/hauler?company_name=Cro%20Scrap \
  -H 'Authorization: Bearer {access-token}'

```

```http
OPTIONS http://localhost:8003/hauler?company_name=Cro%20Scrap HTTP/1.1
Host: localhost:8003

```

```javascript
var headers = {
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/hauler',
  method: 'options',
  data: '?company_name=Cro%20Scrap',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/hauler?company_name=Cro%20Scrap',
{
  method: 'OPTIONS',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.options 'http://localhost:8003/hauler',
  params: {
  'company_name' => 'string(stringIdentifier)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'Bearer {access-token}'
}

r = requests.options('http://localhost:8003/hauler', params={
  'company_name': 'Cro Scrap'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/hauler?company_name=Cro%20Scrap");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("OPTIONS");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("OPTIONS", "http://localhost:8003/hauler", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### OPTIONS /hauler

List HTTP operations.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|company_name|query|string(stringIdentifier)|true|The comapny identifier issued at account creation. All caps, no spaces, no special characters.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Headers|string||Comma separated list of access control headers.|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdlist_haulers_head"></a>

> Code samples

```shell
# You can also use wget
curl -X HEAD http://localhost:8003/hauler?company_name=Cro%20Scrap \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
HEAD http://localhost:8003/hauler?company_name=Cro%20Scrap HTTP/1.1
Host: localhost:8003

X-TENANT-ID: 1

```

```javascript
var headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/hauler',
  method: 'head',
  data: '?company_name=Cro%20Scrap',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/hauler?company_name=Cro%20Scrap',
{
  method: 'HEAD',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.head 'http://localhost:8003/hauler',
  params: {
  'company_name' => 'string(stringIdentifier)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.head('http://localhost:8003/hauler', params={
  'company_name': 'Cro Scrap'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/hauler?company_name=Cro%20Scrap");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("HEAD");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("HEAD", "http://localhost:8003/hauler", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### HEAD /hauler

HTTP head

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|company_name|query|string(stringIdentifier)|true|The comapny identifier issued at account creation. All caps, no spaces, no special characters.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## Hauler

<a id="opIdget_hauler"></a>

> Code samples

```shell
# You can also use wget
curl -X GET http://localhost:8003/hauler/{hauler_id} \
  -H 'Accept: application/json' \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
GET http://localhost:8003/hauler/{hauler_id} HTTP/1.1
Host: localhost:8003
Accept: application/json
X-TENANT-ID: 1

```

```javascript
var headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/hauler/{hauler_id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/hauler/{hauler_id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'http://localhost:8003/hauler/{hauler_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('http://localhost:8003/hauler/{hauler_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/hauler/{hauler_id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "http://localhost:8003/hauler/{hauler_id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### GET /hauler/{hauler_id}

Hauler profile.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|hauler_id|path|[UUID](#schemauuid)|true|Hauler identifier.|

> Example responses

> 200 Response

```json
{
  "id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "name": "SMS594"
}
```

> 400 Response

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[HaulerModel](#schemahaulermodel)|Hauler profile.|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdget_hauler_options"></a>

> Code samples

```shell
# You can also use wget
curl -X OPTIONS http://localhost:8003/hauler/{hauler_id} \
  -H 'Authorization: Bearer {access-token}'

```

```http
OPTIONS http://localhost:8003/hauler/{hauler_id} HTTP/1.1
Host: localhost:8003

```

```javascript
var headers = {
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/hauler/{hauler_id}',
  method: 'options',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/hauler/{hauler_id}',
{
  method: 'OPTIONS',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.options 'http://localhost:8003/hauler/{hauler_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'Bearer {access-token}'
}

r = requests.options('http://localhost:8003/hauler/{hauler_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/hauler/{hauler_id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("OPTIONS");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("OPTIONS", "http://localhost:8003/hauler/{hauler_id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### OPTIONS /hauler/{hauler_id}

List HTTP operations.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|hauler_id|path|[UUID](#schemauuid)|true|Hauler identifier.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Headers|string||Comma separated list of access control headers.|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdget_hauler_head"></a>

> Code samples

```shell
# You can also use wget
curl -X HEAD http://localhost:8003/hauler/{hauler_id} \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
HEAD http://localhost:8003/hauler/{hauler_id} HTTP/1.1
Host: localhost:8003

X-TENANT-ID: 1

```

```javascript
var headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/hauler/{hauler_id}',
  method: 'head',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/hauler/{hauler_id}',
{
  method: 'HEAD',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.head 'http://localhost:8003/hauler/{hauler_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.head('http://localhost:8003/hauler/{hauler_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/hauler/{hauler_id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("HEAD");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("HEAD", "http://localhost:8003/hauler/{hauler_id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### HEAD /hauler/{hauler_id}

HTTP head

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|hauler_id|path|[UUID](#schemauuid)|true|Hauler identifier.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## Hauler Connections

<a id="opIdlist_hauler_connections"></a>

> Code samples

```shell
# You can also use wget
curl -X GET http://localhost:8003/hauler/{hauler_id}/connection \
  -H 'Accept: application/json' \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
GET http://localhost:8003/hauler/{hauler_id}/connection HTTP/1.1
Host: localhost:8003
Accept: application/json
X-TENANT-ID: 1

```

```javascript
var headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/hauler/{hauler_id}/connection',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/hauler/{hauler_id}/connection',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'http://localhost:8003/hauler/{hauler_id}/connection',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('http://localhost:8003/hauler/{hauler_id}/connection', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/hauler/{hauler_id}/connection");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "http://localhost:8003/hauler/{hauler_id}/connection", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### GET /hauler/{hauler_id}/connection

Hauler profile.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|hauler_id|path|[UUID](#schemauuid)|true|Hauler identifier.|

> Example responses

> 200 Response

```json
{
  "approved_by": 1,
  "approved_on": "2019-01-04T20:56:01.872Z",
  "denied_on": "string",
  "is_approved": true,
  "location_id": 1,
  "provider_email": "test_hauler@crosoftware.net",
  "provider_id": 2,
  "provider_name": "CRO Scrap - Sequim",
  "provider_phone": "na",
  "requested_on": "2019-01-04T20:56:01.872Z"
}
```

> 400 Response

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[HaulerConnectionModel](#schemahaulerconnectionmodel)|List|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdget_hauler"></a>

> Code samples

```shell
# You can also use wget
curl -X POST http://localhost:8003/hauler/{hauler_id}/connection?tenant_code=CROSCRAP%2B1 \
  -H 'Accept: application/json' \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
POST http://localhost:8003/hauler/{hauler_id}/connection?tenant_code=CROSCRAP%2B1 HTTP/1.1
Host: localhost:8003
Accept: application/json
X-TENANT-ID: 1

```

```javascript
var headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/hauler/{hauler_id}/connection',
  method: 'post',
  data: '?tenant_code=CROSCRAP%2B1',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/hauler/{hauler_id}/connection?tenant_code=CROSCRAP%2B1',
{
  method: 'POST',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.post 'http://localhost:8003/hauler/{hauler_id}/connection',
  params: {
  'tenant_code' => 'string(tenantCode)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.post('http://localhost:8003/hauler/{hauler_id}/connection', params={
  'tenant_code': 'CROSCRAP+1'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/hauler/{hauler_id}/connection?tenant_code=CROSCRAP%2B1");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "http://localhost:8003/hauler/{hauler_id}/connection", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### POST /hauler/{hauler_id}/connection

Create hauler connection.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|hauler_id|path|[UUID](#schemauuid)|true|Hauler identifier.|
|tenant_code|query|string(tenantCode)|true|<YardCode>+<LocationId>. The YardCode is an identifier assigned at account creation.|

> Example responses

> 200 Response

```json
{
  "approved_by": 1,
  "approved_on": "2019-01-04T20:56:01.873Z",
  "denied_on": "string",
  "is_approved": true,
  "location_id": 1,
  "provider_email": "test_hauler@crosoftware.net",
  "provider_id": 2,
  "provider_name": "CRO Scrap - Sequim",
  "provider_phone": "na",
  "requested_on": "2019-01-04T20:56:01.873Z"
}
```

> 400 Response

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[HaulerConnectionModel](#schemahaulerconnectionmodel)|Hauler with given UUID.|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdget_hauler_connection_options"></a>

> Code samples

```shell
# You can also use wget
curl -X OPTIONS http://localhost:8003/hauler/{hauler_id}/connection \
  -H 'Authorization: Bearer {access-token}'

```

```http
OPTIONS http://localhost:8003/hauler/{hauler_id}/connection HTTP/1.1
Host: localhost:8003

```

```javascript
var headers = {
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/hauler/{hauler_id}/connection',
  method: 'options',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/hauler/{hauler_id}/connection',
{
  method: 'OPTIONS',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.options 'http://localhost:8003/hauler/{hauler_id}/connection',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'Bearer {access-token}'
}

r = requests.options('http://localhost:8003/hauler/{hauler_id}/connection', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/hauler/{hauler_id}/connection");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("OPTIONS");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("OPTIONS", "http://localhost:8003/hauler/{hauler_id}/connection", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### OPTIONS /hauler/{hauler_id}/connection

List HTTP operations.

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|hauler_id|path|[UUID](#schemauuid)|true|Hauler identifier.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Headers|string||Comma separated list of access control headers.|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

<a id="opIdget_hauler_connection_head"></a>

> Code samples

```shell
# You can also use wget
curl -X HEAD http://localhost:8003/hauler/{hauler_id}/connection \
  -H 'X-TENANT-ID: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```http
HEAD http://localhost:8003/hauler/{hauler_id}/connection HTTP/1.1
Host: localhost:8003

X-TENANT-ID: 1

```

```javascript
var headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'http://localhost:8003/hauler/{hauler_id}/connection',
  method: 'head',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'X-TENANT-ID':'1',
  'Authorization':'Bearer {access-token}'

};

fetch('http://localhost:8003/hauler/{hauler_id}/connection',
{
  method: 'HEAD',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'X-TENANT-ID' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.head 'http://localhost:8003/hauler/{hauler_id}/connection',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'X-TENANT-ID': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.head('http://localhost:8003/hauler/{hauler_id}/connection', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("http://localhost:8003/hauler/{hauler_id}/connection");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("HEAD");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "X-TENANT-ID": []string{"1"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("HEAD", "http://localhost:8003/hauler/{hauler_id}/connection", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

### HEAD /hauler/{hauler_id}/connection

HTTP head

<h3 id="undefined-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-TENANT-ID|header|integer(int64)|true|Tenant identifier.|
|hauler_id|path|[UUID](#schemauuid)|true|Hauler identifier.|

<h3 id="undefined-responses">Responses</h3>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|None|Empty body.|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Access-Control-Allow-Methods|string||Comma separated list of allowed HTTP methods for this endpoint.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

# Schemas

<h2 id="tocSdatetime">DateTime</h2>

<a id="schemadatetime"></a>

```json
"2018-10-31T11:32:38.390000"

```

*YYYY-MM-DDThh:mm:ss.ssssss
ISO 8601 DateTime Format (GMT)
*

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|*anonymous*|string(datetime)|true|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT)|

<h2 id="tocSuuid">UUID</h2>

<a id="schemauuid"></a>

```json
"b8d78911-e1fa-4adc-9b22-3b48dda30522"

```

*UUID
*

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|*anonymous*|string(uuid)|true|UUID|

<h2 id="tocSrecordid">RecordId</h2>

<a id="schemarecordid"></a>

```json
1

```

*Record identifier.
*

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|*anonymous*|integer(int64)|true|Record identifier.|

<h2 id="tocSaddressmodel">AddressModel</h2>

<a id="schemaaddressmodel"></a>

```json
{
  "country": "usa",
  "id": 9,
  "latitude": 48.0854948,
  "line_1": "610 N 5th Ave",
  "line_2": "P.O. Box 123",
  "line_3": "Suite 1",
  "line_4": "1st Floor",
  "locality": "Sequim",
  "longitude": -123.11221510000001,
  "postcode": 98382,
  "region": "WA"
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|country|string|true|none|
|id|integer(int64)|true|none|
|latitude|number(float)|true|none|
|line_1|string|true|none|
|line_2|string|true|none|
|line_3|string|true|none|
|line_4|string|true|none|
|locality|string|true|none|
|longitude|number(float)|true|none|
|postcode|string|true|none|
|region|string|true|none|

<h2 id="tocSassettypemodel">AssetTypeModel</h2>

<a id="schemaassettypemodel"></a>

```json
{
  "deleted": false,
  "id": 1,
  "is_default": false,
  "location_id": 1,
  "name": "10 yrd",
  "quantity": 2,
  "require_numbers": true,
  "weight": 3245
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|deleted|boolean|true|none|
|id|integer(int64)|true|none|
|is_default|boolean|true|none|
|location_id|integer(int64)|true|none|
|name|string|true|none|
|quantity|integer(int64)|true|none|
|require_numbers|boolean|true|none|
|weight|integer(int64)|true|none|

<h2 id="tocSbasejobmodel">BaseJobModel</h2>

<a id="schemabasejobmodel"></a>

```json
{
  "arrived_at_dest": "2018-11-18T19:54:55.327000",
  "arrived_on": "2018-11-18T19:54:55.327000",
  "asset_dropped": 1,
  "asset_id": 1,
  "asset_quantity": 1,
  "asset_type_id": 1,
  "completed_by": 1,
  "completed_by_driver": false,
  "completed_on": "2018-11-18T19:54:55.327000",
  "confirmed_on": "2018-11-18T19:54:55.327000",
  "created_by_id": 1,
  "created_with_portal": false,
  "customer_id": 9,
  "customer_notes": "Some customer notes",
  "departed_on": "2018-11-18T19:54:55.327000",
  "desired_asset_desc": "An asset description.",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2018-11-18T19:54:55.327000",
  "dispatcher_notes": "Some dispatcher notes",
  "do_confirm": false,
  "driver_notes": "Some driver notes",
  "dropped_number": "Unused/deprecated field",
  "dump_location_id": 1,
  "dumped_on": "2018-11-18T19:54:55.327000",
  "end_time": "2018-11-18T19:54:55.327000",
  "fail_reason": "Failure reason",
  "final_location_id": 1,
  "flags": "Job notes",
  "id": 1,
  "invoice_notes": "Some invoice notes",
  "is_completed": false,
  "is_declined": false,
  "is_deleted": false,
  "is_failed": false,
  "is_paid": true,
  "job_group_id": 1,
  "location_id": 1,
  "merged_with_route": 1,
  "original_schedule_date": "2018-10-31T11:34:13.690000",
  "pickup_date": "2018-10-31T11:34:13.690000",
  "priority": -1,
  "reference_number": null,
  "removed_number": "string",
  "requested_on": "2018-10-31T11:33:52.920000",
  "require_image": false,
  "require_material": false,
  "require_signature": false,
  "require_weights": false,
  "schedule_date": "2018-10-31T00:00:00",
  "start_location_id": 1,
  "start_time": "2018-10-31T11:33:52.920000",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "times_failed": 0,
  "times_rolled_over": 0,
  "truck_id": 1,
  "type": "D",
  "weighed_on": "2018-10-31T11:33:52.920000"
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|arrived_at_dest|string(datetime)|true|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Entered by driver for dispatcher and customer. Asset arrival at destination time. Only applicable for jobs with a valid dump destination.|
|arrived_on|string(datetime)|true|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Drive start time entered by driver for dispatcher and customer (arrived at job slider).|
|asset_dropped|integer(int64)|true|Reference to deployed asset entered by driver for customer, dispatcher applicable to job types 'D', 'E'.|
|asset_id|integer(int64)|true|Applicable to job types 'E', 'P', 'R'.|
|asset_quantity|integer(int64)|true|How many assets are being serviced within a cluster (for jobs assigned to an asset cluster). For jobs dispatched by routes, or manually dispatched route stops, this value is 0 or 1.|
|asset_type_id|integer(int64)|false|Selected asset for the job (job types 'D', 'L', 'E').|
|completed_by|integer(int64)|false|Dispatcher or driver id.|
|completed_by_driver|boolean|false|If TRUE, completed by driver. If FALSE, completed by dispatcher.|
|completed_on|string(datetime)|true|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Job completion time (must be in the past).|
|confirmed_on|string(datetime)|true|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Must be in the past.|
|created_by_id|integer(int64)|true|Customer, dispatcher, or driver id.|
|created_with_portal|boolean|false|Unused field|
|customer_id|integer(int64)|false|Customer identifier.|
|customer_notes|string|true|Notes entered by customers to communicate with dispatchers.|
|departed_on|string(datetime)|true|Unused/deprecated|
|desired_asset_desc|string|true|Free-form text entered by dispatchers and drivers to be used as the future asset description.|
|dispatch_priority|string|true|Entered by dispatchers to determine dispatch order. Can be 'H', 'M', 'L' (High, Medium, Low).|
|dispatched_by_route|integer(int64)|true|Route id of dispatching route (or NULL if not dispatched by a route).|
|dispatched_on|string(datetime)|true|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Time the job is assigned to a truck.|
|dispatcher_notes|string|true|Entered by dispatchers, read by drivers and dispatchers.|
|do_confirm|boolean|false|Tell dispatcher that a customer should be contacted before job is dispatched.|
|driver_notes|string|true|Entered by drivers when completing or failing a job for dispatchers.|
|dropped_number|string|false|Unused/deprecated|
|dump_location_id|integer(int64)|true|Asset or asset cluster dump location identifier (e.g. trash bin needs  dumped before returning from customer).|
|dumped_on|string(datetime)|true|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Dump request completion date.|
|end_time|string(datetime)|true|Future estimated time of job completion.|
|fail_reason|string|true|Failure description selected by a driver for use by dispatchers.|
|final_location_id|integer(int64)|true|Final location identifier. Used by dispatchers for prioritizing jobs. Used by drivers to know where to leave the asset on job completion.|
|flags|string|true|Job notes.|
|id|integer(int64)|false|Job identifier.|
|invoice_notes|string|true|Invoice notes from the billing system.|
|is_completed|boolean|false|Job completion flag set by dispatchers and drivers.|
|is_declined|boolean|false|Job completion flag set by dispatchers and drivers.|
|is_deleted|boolean|false|Indicates whether job is still valid.|
|is_failed|boolean|false|Set by drivers and dispatchers to indicate a failed job.|
|is_paid|boolean|true|Unused/deprecated|
|job_group_id|integer(int64)|true|Job group identifier for group jobs (vs service, exchange, etc.).|
|location_id|integer(int64)|false|Owning location for the job.|
|merged_with_route|integer(int64)|true|Assigned by dispatchers for dispatchers and drivers.|
|original_schedule_date|string(datetime)|false|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Original scheduling date.|
|pickup_date|string(datetime)|true|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) A pickup job is scheduled for this date upon job completion. If the asset or cluster is assigned to a route stop, the route stop will be deleted. Must be in the future.|
|priority|integer(int64)|false|Assigned by dispatchers for job order completion determination for drivers.|
|reference_number|string|true|Provider-specific billing/reporting field.|
|removed_number|string|true|Unused/deprecated|
|requested_on|string(datetime)|false|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Job creation date.|
|require_image|boolean|false|Set by dispatchers and drivers, requires drivers to upload one or more job images before completion.|
|require_material|boolean|false|Set by dispatchers and drivers, requires drivers to set a material before completing a job.|
|require_signature|boolean|false|Set by dispatchers and drivers, requires drivers to get a customer signature before job completion.|
|require_weights|boolean|false|Set by disptachers and drivers, requires drivers to set material weights before job completion.|
|schedule_date|string(datetime)|false|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Scheduled job completion date.|
|start_location_id|integer(int64)|true|Pickup location for asset or asset cluster Set by dispatchers and drivers for drivers.|
|start_time|string(datetime)|true|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Time customer has requested job start, set by dispatchers for dispatchers and drivers.|
|third_party_hauler_id|[UUID](#schemauuid)|true|UUID|
|times_failed|integer(int64)|false|Number of times a job has been attempted and failed.|
|times_rolled_over|integer(int64)|false|Tracks job age in days for dispatchers.|
|truck_id|integer(int64)|true|Set by dispatchers to determine job visibility for drivers.|
|type|string|false|Set by dispatchers and customers. Represents physical actions to execute on job start. 'D', 'E', 'L', 'P', 'R'|
|weighed_on|string(datetime)|true|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Time of truck weight entry.|

<h2 id="tocScustomeraddressmodel">CustomerAddressModel</h2>

<a id="schemacustomeraddressmodel"></a>

```json
{
  "address": {
    "country": "usa",
    "id": 9,
    "latitude": 48.0854948,
    "line_1": "610 N 5th Ave",
    "line_2": "P.O. Box 123",
    "line_3": "Suite 1",
    "line_4": "1st Floor",
    "locality": "Sequim",
    "longitude": -123.11221510000001,
    "postcode": 98382,
    "region": "WA"
  },
  "address_id": 9,
  "customer_id": 9,
  "is_active": true,
  "is_billing": false,
  "is_physical": true,
  "is_shipping": true
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|address|[AddressModel](#schemaaddressmodel)|true|none|
|address_id|integer(int64)|true|none|
|customer_id|integer(int64)|true|none|
|is_active|boolean|true|none|
|is_billing|boolean|true|none|
|is_physical|boolean|true|none|
|is_shipping|boolean|true|none|

<h2 id="tocScustomermodel">CustomerModel</h2>

<a id="schemacustomermodel"></a>

```json
{
  "addresses": [
    {
      "address": {
        "country": "usa",
        "id": 9,
        "latitude": 48.0854948,
        "line_1": "610 N 5th Ave",
        "line_2": "P.O. Box 123",
        "line_3": "Suite 1",
        "line_4": "1st Floor",
        "locality": "Sequim",
        "longitude": -123.11221510000001,
        "postcode": 98382,
        "region": "WA"
      },
      "address_id": 9,
      "customer_id": 9,
      "is_active": true,
      "is_billing": false,
      "is_physical": true,
      "is_shipping": true
    }
  ],
  "created_on": "2019-01-04T20:56:01.876Z",
  "id": 9,
  "locations": [
    {
      "created_on": "2019-01-04T20:56:01.876Z",
      "customer_id": 9,
      "is_active": true,
      "is_commercial": false,
      "last_edited": "2019-01-04T20:56:01.876Z",
      "location_id": 1,
      "note": "string",
      "reference_number": "string",
      "renewal_date": "string",
      "sales_rep": "string",
      "suspension_id": "string"
    }
  ],
  "name": "YMCA",
  "parent_id": 8
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|addresses|[[CustomerAddressModel](#schemacustomeraddressmodel)]|true|none|
|created_on|string(datetime)|true|none|
|id|integer(int64)|true|none|
|locations|[[JobLocationModel](#schemajoblocationmodel)]|true|none|
|name|string(byte)|true|none|
|parent_id|integer(int64)|true|none|

<h2 id="tocSdriverlistmodel">DriverListModel</h2>

<a id="schemadriverlistmodel"></a>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "address": "1234 Cro St",
      "can_convert_to_group": false,
      "can_create_requests": false,
      "can_edit_requests": false,
      "can_reposition_asset": false,
      "city": "Sequim",
      "disable_shift_tracking": false,
      "email": "john@crosoftware.net",
      "id": 2,
      "license_number": "123ABC",
      "location_id": 1,
      "name": "John Denver",
      "phone_number": "(360) 718-1234",
      "state": "WA",
      "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "zip": 98368
    }
  ],
  "total_count": 1,
  "total_pages": 1
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|current_limit|integer(int64)|true|none|
|current_page|integer(int64)|true|none|
|results|[[DriverModel](#schemadrivermodel)]|true|none|
|total_count|integer(int64)|true|none|
|total_pages|integer(int64)|true|none|

<h2 id="tocSdrivermodel">DriverModel</h2>

<a id="schemadrivermodel"></a>

```json
{
  "address": "1234 Cro St",
  "can_convert_to_group": false,
  "can_create_requests": false,
  "can_edit_requests": false,
  "can_reposition_asset": false,
  "city": "Sequim",
  "disable_shift_tracking": false,
  "email": "john@crosoftware.net",
  "id": 2,
  "license_number": "123ABC",
  "location_id": 1,
  "name": "John Denver",
  "phone_number": "(360) 718-1234",
  "state": "WA",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "zip": 98368
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|address|string|true|none|
|can_convert_to_group|boolean|true|none|
|can_create_requests|boolean|true|none|
|can_edit_requests|boolean|true|none|
|can_reposition_asset|boolean|true|none|
|city|string|true|none|
|disable_shift_tracking|boolean|true|none|
|email|string|true|none|
|id|integer(int64)|true|none|
|license_number|string|true|none|
|location_id|integer(int64)|true|none|
|name|string|true|none|
|phone_number|string|true|none|
|state|string|true|none|
|third_party_hauler_id|[UUID](#schemauuid)|true|UUID|
|zip|string|true|none|

<h2 id="tocShaulerconnectionmodel">HaulerConnectionModel</h2>

<a id="schemahaulerconnectionmodel"></a>

```json
{
  "approved_by": 1,
  "approved_on": "2019-01-04T20:56:01.877Z",
  "denied_on": "string",
  "is_approved": true,
  "location_id": 1,
  "provider_email": "test_hauler@crosoftware.net",
  "provider_id": 2,
  "provider_name": "CRO Scrap - Sequim",
  "provider_phone": "na",
  "requested_on": "2019-01-04T20:56:01.877Z"
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|approved_by|integer(int64)|true|none|
|approved_on|string(datetime)|true|none|
|denied_on|string|true|none|
|is_approved|boolean|true|none|
|location_id|integer(int64)|true|none|
|provider_email|string|true|none|
|provider_id|integer(int64)|true|none|
|provider_name|string|true|none|
|provider_phone|string|true|none|
|requested_on|string(datetime)|true|none|

<h2 id="tocShaulerlistmodel">HaulerListModel</h2>

<a id="schemahaulerlistmodel"></a>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "name": "SMS594"
    }
  ],
  "total_count": 1,
  "total_pages": 1
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|current_limit|integer(int64)|true|none|
|current_page|integer(int64)|true|none|
|results|[[HaulerModel](#schemahaulermodel)]|true|none|
|total_count|integer(int64)|true|none|
|total_pages|integer(int64)|true|none|

<h2 id="tocShaulermodel">HaulerModel</h2>

<a id="schemahaulermodel"></a>

```json
{
  "id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "name": "SMS594"
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|id|[UUID](#schemauuid)|true|UUID|
|name|string|true|none|

<h2 id="tocSjoblistmodel">JobListModel</h2>

<a id="schemajoblistmodel"></a>

```json
{
  "current_limit": 1,
  "current_page": 1,
  "results": [
    {
      "arrived_at_dest": "2018-11-18T19:54:55.327000",
      "arrived_on": "2018-11-18T19:54:55.327000",
      "asset_dropped": 1,
      "asset_id": 1,
      "asset_quantity": 1,
      "asset_type_id": 1,
      "completed_by": 1,
      "completed_by_driver": false,
      "completed_on": "2018-11-18T19:54:55.327000",
      "confirmed_on": "2018-11-18T19:54:55.327000",
      "created_by_id": 1,
      "created_with_portal": false,
      "customer_id": 9,
      "customer_notes": "Some customer notes",
      "departed_on": "2018-11-18T19:54:55.327000",
      "desired_asset_desc": "An asset description.",
      "dispatch_priority": "H",
      "dispatched_by_route": 1,
      "dispatched_on": "2018-11-18T19:54:55.327000",
      "dispatcher_notes": "Some dispatcher notes",
      "do_confirm": false,
      "driver_notes": "Some driver notes",
      "dropped_number": "Unused/deprecated field",
      "dump_location_id": 1,
      "dumped_on": "2018-11-18T19:54:55.327000",
      "end_time": "2018-11-18T19:54:55.327000",
      "fail_reason": "Failure reason",
      "final_location_id": 1,
      "flags": "Job notes",
      "id": 1,
      "invoice_notes": "Some invoice notes",
      "is_completed": false,
      "is_declined": false,
      "is_deleted": false,
      "is_failed": false,
      "is_paid": true,
      "job_group_id": 1,
      "location_id": 1,
      "merged_with_route": 1,
      "original_schedule_date": "2018-10-31T11:34:13.690000",
      "pickup_date": "2018-10-31T11:34:13.690000",
      "priority": -1,
      "reference_number": null,
      "removed_number": "string",
      "requested_on": "2018-10-31T11:33:52.920000",
      "require_image": false,
      "require_material": false,
      "require_signature": false,
      "require_weights": false,
      "schedule_date": "2018-10-31T00:00:00",
      "start_location_id": 1,
      "start_time": "2018-10-31T11:33:52.920000",
      "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "times_failed": 0,
      "times_rolled_over": 0,
      "truck_id": 1,
      "type": "D",
      "weighed_on": "2018-10-31T11:33:52.920000",
      "asset": {
        "asset_type": {
          "deleted": false,
          "id": 1,
          "is_default": false,
          "location_id": 1,
          "name": "10 yrd",
          "quantity": 2,
          "require_numbers": true,
          "weight": 3245
        },
        "asset_type_id": 1,
        "cluster": 1,
        "customer_id": 1,
        "description": "A description",
        "dispatched_on": "2019-01-04T20:56:01.878Z",
        "id": 1,
        "is_returned": false,
        "last_activity_on": "2019-01-04T20:56:01.878Z",
        "last_rental_invoice_on": "2019-01-04T20:56:01.878Z",
        "latitude": 54.235,
        "location": {
          "id": 1,
          "is_active": true,
          "name": "Sequim",
          "test": "Q1JPIFNvZnR3YXJl"
        },
        "location_id": 1,
        "longitude": 127.123,
        "number": "REF100",
        "quantity": 1,
        "returned_on": "2019-01-04T20:56:01.878Z"
      },
      "asset_type": {
        "deleted": false,
        "id": 1,
        "is_default": false,
        "location_id": 1,
        "name": "10 yrd",
        "quantity": 2,
        "require_numbers": true,
        "weight": 3245
      },
      "customer": {
        "addresses": [
          {
            "address": {
              "country": "usa",
              "id": 9,
              "latitude": 48.0854948,
              "line_1": "610 N 5th Ave",
              "line_2": "P.O. Box 123",
              "line_3": "Suite 1",
              "line_4": "1st Floor",
              "locality": "Sequim",
              "longitude": -123.11221510000001,
              "postcode": 98382,
              "region": "WA"
            },
            "address_id": 9,
            "customer_id": 9,
            "is_active": true,
            "is_billing": false,
            "is_physical": true,
            "is_shipping": true
          }
        ],
        "created_on": "2019-01-04T20:56:01.878Z",
        "id": 9,
        "locations": [
          {
            "created_on": "2019-01-04T20:56:01.878Z",
            "customer_id": 9,
            "is_active": true,
            "is_commercial": false,
            "last_edited": "2019-01-04T20:56:01.878Z",
            "location_id": 1,
            "note": "string",
            "reference_number": "string",
            "renewal_date": "string",
            "sales_rep": "string",
            "suspension_id": "string"
          }
        ],
        "name": "YMCA",
        "parent_id": 8
      },
      "dump_location": {
        "address": "123 Sequim Ave.",
        "city": "Sequim",
        "contact_email": "support@crosoftware.net",
        "contact_name": "John Doe",
        "contact_phone": "(706) 360-7109",
        "id": 1,
        "is_holding_yard": true,
        "latitude": 128.123,
        "location": {
          "id": 1,
          "is_active": true,
          "name": "Sequim",
          "test": "Q1JPIFNvZnR3YXJl"
        },
        "location_id": 1,
        "longitude": 54.234,
        "name": "A Destination",
        "state": "Washington",
        "zip": 98368
      },
      "final_location": {
        "address": "123 Sequim Ave.",
        "city": "Sequim",
        "contact_email": "support@crosoftware.net",
        "contact_name": "John Doe",
        "contact_phone": "(706) 360-7109",
        "id": 1,
        "is_holding_yard": true,
        "latitude": 128.123,
        "location": {
          "id": 1,
          "is_active": true,
          "name": "Sequim",
          "test": "Q1JPIFNvZnR3YXJl"
        },
        "location_id": 1,
        "longitude": 54.234,
        "name": "A Destination",
        "state": "Washington",
        "zip": 98368
      },
      "start_location": {
        "address": "123 Sequim Ave.",
        "city": "Sequim",
        "contact_email": "support@crosoftware.net",
        "contact_name": "John Doe",
        "contact_phone": "(706) 360-7109",
        "id": 1,
        "is_holding_yard": true,
        "latitude": 128.123,
        "location": {
          "id": 1,
          "is_active": true,
          "name": "Sequim",
          "test": "Q1JPIFNvZnR3YXJl"
        },
        "location_id": 1,
        "longitude": 54.234,
        "name": "A Destination",
        "state": "Washington",
        "zip": 98368
      }
    }
  ],
  "total_count": 1,
  "total_pages": 1
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|current_limit|integer(int64)|true|none|
|current_page|integer(int64)|true|none|
|results|[[JobModel](#schemajobmodel)]|true|none|
|total_count|integer(int64)|true|none|
|total_pages|integer(int64)|true|none|

<h2 id="tocSjoblocationmodel">JobLocationModel</h2>

<a id="schemajoblocationmodel"></a>

```json
{
  "created_on": "2019-01-04T20:56:01.882Z",
  "customer_id": 9,
  "is_active": true,
  "is_commercial": false,
  "last_edited": "2019-01-04T20:56:01.883Z",
  "location_id": 1,
  "note": "string",
  "reference_number": "string",
  "renewal_date": "string",
  "sales_rep": "string",
  "suspension_id": "string"
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|created_on|string(datetime)|true|none|
|customer_id|integer(int64)|true|none|
|is_active|boolean|true|none|
|is_commercial|boolean|true|none|
|last_edited|string(datetime)|true|none|
|location_id|integer(int64)|true|none|
|note|string|true|none|
|reference_number|string|true|none|
|renewal_date|string|true|none|
|sales_rep|string|true|none|
|suspension_id|string|true|none|

<h2 id="tocSjobmodel">JobModel</h2>

<a id="schemajobmodel"></a>

```json
{
  "arrived_at_dest": "2018-11-18T19:54:55.327000",
  "arrived_on": "2018-11-18T19:54:55.327000",
  "asset_dropped": 1,
  "asset_id": 1,
  "asset_quantity": 1,
  "asset_type_id": 1,
  "completed_by": 1,
  "completed_by_driver": false,
  "completed_on": "2018-11-18T19:54:55.327000",
  "confirmed_on": "2018-11-18T19:54:55.327000",
  "created_by_id": 1,
  "created_with_portal": false,
  "customer_id": 9,
  "customer_notes": "Some customer notes",
  "departed_on": "2018-11-18T19:54:55.327000",
  "desired_asset_desc": "An asset description.",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2018-11-18T19:54:55.327000",
  "dispatcher_notes": "Some dispatcher notes",
  "do_confirm": false,
  "driver_notes": "Some driver notes",
  "dropped_number": "Unused/deprecated field",
  "dump_location_id": 1,
  "dumped_on": "2018-11-18T19:54:55.327000",
  "end_time": "2018-11-18T19:54:55.327000",
  "fail_reason": "Failure reason",
  "final_location_id": 1,
  "flags": "Job notes",
  "id": 1,
  "invoice_notes": "Some invoice notes",
  "is_completed": false,
  "is_declined": false,
  "is_deleted": false,
  "is_failed": false,
  "is_paid": true,
  "job_group_id": 1,
  "location_id": 1,
  "merged_with_route": 1,
  "original_schedule_date": "2018-10-31T11:34:13.690000",
  "pickup_date": "2018-10-31T11:34:13.690000",
  "priority": -1,
  "reference_number": null,
  "removed_number": "string",
  "requested_on": "2018-10-31T11:33:52.920000",
  "require_image": false,
  "require_material": false,
  "require_signature": false,
  "require_weights": false,
  "schedule_date": "2018-10-31T00:00:00",
  "start_location_id": 1,
  "start_time": "2018-10-31T11:33:52.920000",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "times_failed": 0,
  "times_rolled_over": 0,
  "truck_id": 1,
  "type": "D",
  "weighed_on": "2018-10-31T11:33:52.920000",
  "asset": {
    "asset_type": {
      "deleted": false,
      "id": 1,
      "is_default": false,
      "location_id": 1,
      "name": "10 yrd",
      "quantity": 2,
      "require_numbers": true,
      "weight": 3245
    },
    "asset_type_id": 1,
    "cluster": 1,
    "customer_id": 1,
    "description": "A description",
    "dispatched_on": "2019-01-04T20:56:01.883Z",
    "id": 1,
    "is_returned": false,
    "last_activity_on": "2019-01-04T20:56:01.883Z",
    "last_rental_invoice_on": "2019-01-04T20:56:01.883Z",
    "latitude": 54.235,
    "location": {
      "id": 1,
      "is_active": true,
      "name": "Sequim",
      "test": "Q1JPIFNvZnR3YXJl"
    },
    "location_id": 1,
    "longitude": 127.123,
    "number": "REF100",
    "quantity": 1,
    "returned_on": "2019-01-04T20:56:01.883Z"
  },
  "asset_type": {
    "deleted": false,
    "id": 1,
    "is_default": false,
    "location_id": 1,
    "name": "10 yrd",
    "quantity": 2,
    "require_numbers": true,
    "weight": 3245
  },
  "customer": {
    "addresses": [
      {
        "address": {
          "country": "usa",
          "id": 9,
          "latitude": 48.0854948,
          "line_1": "610 N 5th Ave",
          "line_2": "P.O. Box 123",
          "line_3": "Suite 1",
          "line_4": "1st Floor",
          "locality": "Sequim",
          "longitude": -123.11221510000001,
          "postcode": 98382,
          "region": "WA"
        },
        "address_id": 9,
        "customer_id": 9,
        "is_active": true,
        "is_billing": false,
        "is_physical": true,
        "is_shipping": true
      }
    ],
    "created_on": "2019-01-04T20:56:01.883Z",
    "id": 9,
    "locations": [
      {
        "created_on": "2019-01-04T20:56:01.883Z",
        "customer_id": 9,
        "is_active": true,
        "is_commercial": false,
        "last_edited": "2019-01-04T20:56:01.883Z",
        "location_id": 1,
        "note": "string",
        "reference_number": "string",
        "renewal_date": "string",
        "sales_rep": "string",
        "suspension_id": "string"
      }
    ],
    "name": "YMCA",
    "parent_id": 8
  },
  "dump_location": {
    "address": "123 Sequim Ave.",
    "city": "Sequim",
    "contact_email": "support@crosoftware.net",
    "contact_name": "John Doe",
    "contact_phone": "(706) 360-7109",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 128.123,
    "location": {
      "id": 1,
      "is_active": true,
      "name": "Sequim",
      "test": "Q1JPIFNvZnR3YXJl"
    },
    "location_id": 1,
    "longitude": 54.234,
    "name": "A Destination",
    "state": "Washington",
    "zip": 98368
  },
  "final_location": {
    "address": "123 Sequim Ave.",
    "city": "Sequim",
    "contact_email": "support@crosoftware.net",
    "contact_name": "John Doe",
    "contact_phone": "(706) 360-7109",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 128.123,
    "location": {
      "id": 1,
      "is_active": true,
      "name": "Sequim",
      "test": "Q1JPIFNvZnR3YXJl"
    },
    "location_id": 1,
    "longitude": 54.234,
    "name": "A Destination",
    "state": "Washington",
    "zip": 98368
  },
  "start_location": {
    "address": "123 Sequim Ave.",
    "city": "Sequim",
    "contact_email": "support@crosoftware.net",
    "contact_name": "John Doe",
    "contact_phone": "(706) 360-7109",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 128.123,
    "location": {
      "id": 1,
      "is_active": true,
      "name": "Sequim",
      "test": "Q1JPIFNvZnR3YXJl"
    },
    "location_id": 1,
    "longitude": 54.234,
    "name": "A Destination",
    "state": "Washington",
    "zip": 98368
  }
}

```

### Properties

*allOf*

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|*anonymous*|[BaseJobModel](#schemabasejobmodel)|true|none|

*and*

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|*anonymous*|object|true|none|
|» asset|[AssetModel](#schemaassetmodel)|true|none|
|» asset_type|[AssetTypeModel](#schemaassettypemodel)|true|none|
|» customer|[CustomerModel](#schemacustomermodel)|true|none|
|» dump_location|[DestinationModel](#schemadestinationmodel)|true|none|
|» final_location|[DestinationModel](#schemadestinationmodel)|true|none|
|» start_location|[DestinationModel](#schemadestinationmodel)|true|none|
|» third_party_hauler_id|[UUID](#schemauuid)|true|UUID|

<h2 id="tocSlocationmodel">LocationModel</h2>

<a id="schemalocationmodel"></a>

```json
{
  "id": 1,
  "is_active": true,
  "name": "Sequim",
  "test": "Q1JPIFNvZnR3YXJl"
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|id|integer(int64)|true|none|
|is_active|boolean|true|none|
|name|string|true|none|
|test|string(byte)|true|none|

<h2 id="tocStrucklistmodel">TruckListModel</h2>

<a id="schematrucklistmodel"></a>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "driver_id": 1,
      "id": 2,
      "location_id": 1,
      "name": "ZachTruck",
      "notes": "Sequim",
      "out_of_service": false,
      "require_odometer": false,
      "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "type": "AwesomeTRUCK Rolloff",
      "weight": 18678
    }
  ],
  "total_count": 1,
  "total_pages": 1
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|current_limit|integer(int64)|true|none|
|current_page|integer(int64)|true|none|
|results|[[TruckModel](#schematruckmodel)]|true|none|
|total_count|integer(int64)|true|none|
|total_pages|integer(int64)|true|none|

<h2 id="tocStruckmodel">TruckModel</h2>

<a id="schematruckmodel"></a>

```json
{
  "driver_id": 1,
  "id": 2,
  "location_id": 1,
  "name": "ZachTruck",
  "notes": "Sequim",
  "out_of_service": false,
  "require_odometer": false,
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "type": "AwesomeTRUCK Rolloff",
  "weight": 18678
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|driver_id|integer(int64)|true|none|
|id|integer(int64)|true|none|
|location_id|integer(int64)|true|none|
|name|string|true|none|
|notes|string|true|none|
|out_of_service|boolean|true|none|
|require_odometer|boolean|true|none|
|third_party_hauler_id|[UUID](#schemauuid)|true|UUID|
|type|string|true|none|
|weight|integer(int64)|true|none|

<h2 id="tocSupdatedjobmodel">UpdatedJobModel</h2>

<a id="schemaupdatedjobmodel"></a>

```json
{
  "arrived_at_dest": "2018-11-18T19:54:55.327000",
  "arrived_on": "2018-11-18T19:54:55.327000",
  "asset_dropped": 1,
  "asset_id": 1,
  "asset_quantity": 1,
  "asset_type_id": 1,
  "completed_by": 1,
  "completed_by_driver": false,
  "completed_on": "2018-11-18T19:54:55.327000",
  "confirmed_on": "2018-11-18T19:54:55.327000",
  "created_by_id": 1,
  "created_with_portal": false,
  "customer_id": 9,
  "customer_notes": "Some customer notes",
  "departed_on": "2018-11-18T19:54:55.327000",
  "desired_asset_desc": "An asset description.",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2018-11-18T19:54:55.327000",
  "dispatcher_notes": "Some dispatcher notes",
  "do_confirm": false,
  "driver_notes": "Some driver notes",
  "dropped_number": "Unused/deprecated field",
  "dump_location_id": 1,
  "dumped_on": "2018-11-18T19:54:55.327000",
  "end_time": "2018-11-18T19:54:55.327000",
  "fail_reason": "Failure reason",
  "final_location_id": 1,
  "flags": "Job notes",
  "id": 1,
  "invoice_notes": "Some invoice notes",
  "is_completed": false,
  "is_declined": false,
  "is_deleted": false,
  "is_failed": false,
  "is_paid": true,
  "job_group_id": 1,
  "location_id": 1,
  "merged_with_route": 1,
  "original_schedule_date": "2018-10-31T11:34:13.690000",
  "pickup_date": "2018-10-31T11:34:13.690000",
  "priority": -1,
  "reference_number": null,
  "removed_number": "string",
  "requested_on": "2018-10-31T11:33:52.920000",
  "require_image": false,
  "require_material": false,
  "require_signature": false,
  "require_weights": false,
  "schedule_date": "2018-10-31T00:00:00",
  "start_location_id": 1,
  "start_time": "2018-10-31T11:33:52.920000",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "times_failed": 0,
  "times_rolled_over": 0,
  "truck_id": 1,
  "type": "D",
  "weighed_on": "2018-10-31T11:33:52.920000"
}

```

### Properties

*allOf*

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|*anonymous*|[BaseJobModel](#schemabasejobmodel)|true|none|

*and*

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|*anonymous*|object|true|none|

<h2 id="tocSassetmodel">AssetModel</h2>

<a id="schemaassetmodel"></a>

```json
{
  "asset_type": {
    "deleted": false,
    "id": 1,
    "is_default": false,
    "location_id": 1,
    "name": "10 yrd",
    "quantity": 2,
    "require_numbers": true,
    "weight": 3245
  },
  "asset_type_id": 1,
  "cluster": 1,
  "customer_id": 1,
  "description": "A description",
  "dispatched_on": "2019-01-04T20:56:01.887Z",
  "id": 1,
  "is_returned": false,
  "last_activity_on": "2019-01-04T20:56:01.887Z",
  "last_rental_invoice_on": "2019-01-04T20:56:01.887Z",
  "latitude": 54.235,
  "location": {
    "id": 1,
    "is_active": true,
    "name": "Sequim",
    "test": "Q1JPIFNvZnR3YXJl"
  },
  "location_id": 1,
  "longitude": 127.123,
  "number": "REF100",
  "quantity": 1,
  "returned_on": "2019-01-04T20:56:01.888Z"
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|asset_type|[AssetTypeModel](#schemaassettypemodel)|true|none|
|asset_type_id|integer(int64)|true|none|
|cluster|integer(int64)|true|none|
|customer_id|integer(int64)|true|none|
|description|string|true|none|
|dispatched_on|string(datetime)|true|none|
|id|integer(int64)|true|none|
|is_returned|boolean|true|none|
|last_activity_on|string(datetime)|true|none|
|last_rental_invoice_on|string(datetime)|true|none|
|latitude|number(float)|true|none|
|location|[LocationModel](#schemalocationmodel)|true|none|
|location_id|integer(int64)|true|none|
|longitude|number(float)|true|none|
|number|string|true|none|
|quantity|integer(int64)|true|none|
|returned_on|string(datetime)|true|none|

<h2 id="tocSlistcustomerresultmodel">ListCustomerResultModel</h2>

<a id="schemalistcustomerresultmodel"></a>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "addresses": [
        {
          "country": "USA",
          "is_active": true,
          "is_billing": true,
          "is_physical": false,
          "is_shipping": false,
          "latitude": 48.076273,
          "line_1": "643 Summer Breeze",
          "line_2": "Suite 34",
          "line_3": "2nd Door on Left",
          "line_4": "Blue slot",
          "locality": "Sequim",
          "longitude": -123.117185,
          "postcode": 98382,
          "region": "WA"
        }
      ],
      "contacts": [
        {
          "email": "nathan@crosoftware.com",
          "fax": "(360) 716-1968",
          "name": "John Doe",
          "notify_on_acknowledged_request": false,
          "notify_on_completed_request": false,
          "notify_on_dispatched_request": false,
          "notify_on_failed_request": false,
          "notify_on_new_request": false,
          "number": "1-111-111-1111"
        }
      ],
      "created_on": "2018-10-31T11:31:30.237000",
      "customer_id": 1,
      "is_active": false,
      "is_commercial": false,
      "last_edited": "2018-10-31T11:54:12.430000",
      "location_id": 1,
      "name": "HOLINC001",
      "note": "Service Location of Holland Inc.",
      "parent_id": 1,
      "reference_number": "Ref#100",
      "renewal_date": "2019-10-02T00:00:00",
      "sales_rep": "John Doe",
      "suspension_id": 1
    }
  ],
  "total_count": 100,
  "total_pages": 1
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|current_limit|integer(int64)|true|none|
|current_page|integer(int64)|true|none|
|results|[[CustomerResultModel](#schemacustomerresultmodel)]|true|none|
|total_count|integer(int64)|true|none|
|total_pages|integer(int64)|true|none|

<h2 id="tocSdestinationmodel">DestinationModel</h2>

<a id="schemadestinationmodel"></a>

```json
{
  "address": "123 Sequim Ave.",
  "city": "Sequim",
  "contact_email": "support@crosoftware.net",
  "contact_name": "John Doe",
  "contact_phone": "(706) 360-7109",
  "id": 1,
  "is_holding_yard": true,
  "latitude": 128.123,
  "location": {
    "id": 1,
    "is_active": true,
    "name": "Sequim",
    "test": "Q1JPIFNvZnR3YXJl"
  },
  "location_id": 1,
  "longitude": 54.234,
  "name": "A Destination",
  "state": "Washington",
  "zip": 98368
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|address|string|true|none|
|city|string|true|none|
|contact_email|string|true|none|
|contact_name|string|true|none|
|contact_phone|string|true|none|
|id|integer(int64)|true|none|
|is_holding_yard|boolean|true|none|
|latitude|number(float)|true|none|
|location|[LocationModel](#schemalocationmodel)|true|none|
|location_id|integer(int64)|true|none|
|longitude|number(float)|true|none|
|name|string|true|none|
|state|string|true|none|
|zip|string|true|none|

<h2 id="tocScustomerresultaddressmodel">CustomerResultAddressModel</h2>

<a id="schemacustomerresultaddressmodel"></a>

```json
{
  "country": "USA",
  "is_active": true,
  "is_billing": true,
  "is_physical": false,
  "is_shipping": false,
  "latitude": 48.076273,
  "line_1": "643 Summer Breeze",
  "line_2": "Suite 34",
  "line_3": "2nd Door on Left",
  "line_4": "Blue slot",
  "locality": "Sequim",
  "longitude": -123.117185,
  "postcode": 98382,
  "region": "WA"
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|country|string|true|none|
|is_active|boolean|true|none|
|is_billing|boolean|true|none|
|is_physical|boolean|true|none|
|is_shipping|boolean|true|none|
|latitude|number(float)|true|none|
|line_1|string|true|none|
|line_2|string|true|none|
|line_3|string|true|none|
|line_4|string|true|none|
|locality|string|true|none|
|longitude|number(float)|true|none|
|postcode|string|true|none|
|region|string|true|none|

<h2 id="tocScustomerresultcontactmodel">CustomerResultContactModel</h2>

<a id="schemacustomerresultcontactmodel"></a>

```json
{
  "email": "nathan@crosoftware.com",
  "fax": "(360) 716-1968",
  "name": "John Doe",
  "notify_on_acknowledged_request": false,
  "notify_on_completed_request": false,
  "notify_on_dispatched_request": false,
  "notify_on_failed_request": false,
  "notify_on_new_request": false,
  "number": "1-111-111-1111"
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|email|string|true|none|
|fax|string|true|none|
|name|string|true|none|
|notify_on_acknowledged_request|boolean|true|none|
|notify_on_completed_request|boolean|true|none|
|notify_on_dispatched_request|boolean|true|none|
|notify_on_failed_request|boolean|true|none|
|notify_on_new_request|boolean|true|none|
|number|string|true|none|

<h2 id="tocScustomerresultmodel">CustomerResultModel</h2>

<a id="schemacustomerresultmodel"></a>

```json
{
  "addresses": [
    {
      "country": "USA",
      "is_active": true,
      "is_billing": true,
      "is_physical": false,
      "is_shipping": false,
      "latitude": 48.076273,
      "line_1": "643 Summer Breeze",
      "line_2": "Suite 34",
      "line_3": "2nd Door on Left",
      "line_4": "Blue slot",
      "locality": "Sequim",
      "longitude": -123.117185,
      "postcode": 98382,
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "email": "nathan@crosoftware.com",
      "fax": "(360) 716-1968",
      "name": "John Doe",
      "notify_on_acknowledged_request": false,
      "notify_on_completed_request": false,
      "notify_on_dispatched_request": false,
      "notify_on_failed_request": false,
      "notify_on_new_request": false,
      "number": "1-111-111-1111"
    }
  ],
  "created_on": "2018-10-31T11:31:30.237000",
  "customer_id": 1,
  "is_active": false,
  "is_commercial": false,
  "last_edited": "2018-10-31T11:54:12.430000",
  "location_id": 1,
  "name": "HOLINC001",
  "note": "Service Location of Holland Inc.",
  "parent_id": 1,
  "reference_number": "Ref#100",
  "renewal_date": "2019-10-02T00:00:00",
  "sales_rep": "John Doe",
  "suspension_id": 1
}

```

### Properties

|Name|Type|Nullable|Description|
|---|---|---|---|---|--|
|addresses|[[CustomerResultAddressModel](#schemacustomerresultaddressmodel)]|true|none|
|contacts|[[CustomerResultContactModel](#schemacustomerresultcontactmodel)]|true|none|
|created_on|string(datetime)|true|none|
|customer_id|integer(int64)|true|none|
|is_active|boolean|true|none|
|is_commercial|boolean|true|none|
|last_edited|string(datetime)|true|none|
|location_id|integer(int64)|true|none|
|name|string|true|none|
|note|string|true|none|
|parent_id|integer(int64)|true|none|
|reference_number|string|true|none|
|renewal_date|string(datetime)|true|none|
|sales_rep|string|true|none|
|suspension_id|integer(int64)|true|none|

