---
title: CRO Software API
language_tabs:
  - csharp: 'C# 2.0'
  - shell: Shell
  - javascript: JS
  - ruby: Ruby
  - python: Python
  - java: Java
toc_footers: []
includes: []
search: true
highlight_theme: darkula
headingLevel: 2

---

<h1 id="cro-software-api">CRO Software API v1.0.0</h1>

Build on & integrate with CRO Software.

Base URLs:

* <a href="https://api.crosoftware.net">https://api.crosoftware.net</a>

Email: <a href="mailto:develop@crosoftware.net">Support</a> 

# Changelog

## Unreleased

### Changed
- Log GPS event now accepts application/json instead of gps_event_json parameter.
- Create/update customer changed from request parameter to JSON customer profile.
- Create/update customer creates/updates customer addresses.
- Create/update customer creates/updates billing zone codes.

### Added
- GET /customer
- GET /customer/{customer_id}
- PATCH /customer/{customer_id}
- GET /customer/{customer_id}/location
- GET /customer/{customer_id}/location/{location_id}
- POST /customer/{customer_id}/location/{location_id}
- PATCH /customer/{customer_id}/location/{location_id}
- GET /customer/{customer_id}/address
- POST /customer/{customer_id}/address
- GET /customer/{customer_id}/address/{address_id}
- PATCH /customer/{customer_id}/address/{address_id}
- DELETE /customer/{customer_id}/address/{address_id}
- GET /customer/{customer_id}/contact
- POST /customer/{customer_id}/contact
- GET /customer/{customer_id}/contact/{contact_id}
- PATCH /customer/{customer_id}/contact/{contact_id}
- POST /location/{location_id}/customer

### Fixed
- Invalid access token no longer returns 500 internal server error.
- <jwt-access-token> corrected to <access-token> in doc.
- Validation issues.
- Filtering issues.

## [0.0.0] - 2019/02/26

### Changed
- Requests using unassigned tenant IDs now return 403 instead of 200.
- Unit test generator now generates test cases for third party roles in DAL.
- Removed predicate and acl (replaced with policy management).
- Changed unit tests from exhaustive to single-sequential.
- Removed tenant_id params (redundant with context)
- Indexed params as kw args for policy enforcement
- Added tenant/location check to policy enforcement

### Added
- POST /location/{location_id}/customer
- PATCH /location/{location_id}/customer/{customer_id}
- GET /location/{location_id}/customer/{customer_id}
- DELETE /location/{location_id}/customer/{customer_id}
- POST /location/{location_id}/gps_event
- GET /tenant
- Added filters to list job endpoint (schedule date range, deleted, completed, driver id, truck id).

### Fixed
- Issue with date comparisons during input validation (aware vs naive)
- Permssions issues found during unit testing (policy info point config)
- ThirdPartyDriver permission issues with List Customers.
- Permissions issues found during acceptance testing.

## [0.0.0] - 2019/02/08

### Added
- Initial implementations for:
  - GET /location/{location_id}/driver
  - GET /location/{location_id}/driver/{driver_id}
  - GET /location/{location_id}/customer
  - POST /hauler
  - POST /hauler/{hauler_id}/connection
  - GET /hauler/{hauler_id}
  - GET /hauler
  - GET /hauler/{hauler_id}/connection
  - GET /location
  - GET /location/{location_id}
  - PATCH /location/{location_id}/job/{job_id}
  - GET /location/{location_id}/job/{job_id}
  - GET /location/{location_id}/job
  - GET /location/{location_id}/truck/{truck_id}
  - GET /location/{location_id}/truck
  - PATCH /location/{location_id}/truck/{truck_id}
  

# Authentication

**oAuth2 authentication.**

To obtain an access token, your CRO API client must complete an OAuth 2.0 flow.
The access token must be passed as an [Authorization: Bearer &lt;token&gt;] header with each request.

- Flow: authorizationCode
    - Authorization URL = [https://auth.crosandbox.com/oauth2/auth](https://auth.crosandbox.com/oauth2/auth)
    - Token URL = [https://auth.crosandbox.com/oauth2/token](https://auth.crosandbox.com/oauth2/token)

|Scope|Scope Description|
|---|---|
|api|CRO API access|

- Flow: implicit
    - Authorization URL = [https://auth.crosandbox.com/oauth2/auth](https://auth.crosandbox.com/oauth2/auth)

|Scope|Scope Description|
|---|---|
|api|CRO API access|

- Flow: password

    - Token URL = [https://auth.crosandbox.com/oauth2/token](https://auth.crosandbox.com/oauth2/token)

|Scope|Scope Description|
|---|---|
|api|CRO API access|

- Flow: clientCredentials

    - Token URL = [https://auth.crosandbox.com/oauth2/token](https://auth.crosandbox.com/oauth2/token)

|Scope|Scope Description|
|---|---|
|api|CRO API access|

<h1 id="cro-software-api-dispatch">Dispatch</h1>

For 3rd party integration with CRO

## Customer Addresses

### Add Address

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers/{customer_id}/addresses";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadValues(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/customers/{customer_id}/addresses \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/addresses',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/customers/{customer_id}/addresses',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.post('https://api.crosoftware.net/customers/{customer_id}/addresses', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/addresses");
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

`POST /customers/{customer_id}/addresses`

<a id="opIdpost_customers_by_id_addresses"></a>

Add customer addresses.

> Body parameter

```json
{
  "country": "US",
  "is_billing": "0",
  "is_shipping": "0",
  "latitude": "-90",
  "line_1": "321 Chase Rd",
  "line_2": "P.O. Box 256",
  "line_3": "3rd Floor",
  "line_4": "Last door on the left (blue)",
  "locality": "Sequim",
  "longitude": "-180",
  "postcode": "98368",
  "region": "WA"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||
|`body`|body|[CreateCustomerAddressModel](#schemacreatecustomeraddressmodel)|true||

> Example responses

> 200 Response

```json
{
  "address_id": "1",
  "country": "US",
  "is_billing": "0",
  "is_physical": "0",
  "is_shipping": "0",
  "latitude": "-90",
  "line_1": "321 Chase Rd",
  "line_2": "P.O. Box 256",
  "line_3": "3rd Floor",
  "line_4": "Last door on the left (blue)",
  "locality": "Sequim",
  "longitude": "-180",
  "postcode": "98368",
  "region": "WA"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressModel](#schemacustomeraddressmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Deactivate Address

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadValues(url, "DELETE", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X DELETE https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id} \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id}',
  method: 'delete',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.delete 'https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.delete('https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
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

`DELETE /customers/{customer_id}/addresses/{address_id}`

<a id="opIddelete_customers_by_id_addresses_by_id"></a>

Deactivate a customer address.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||
|`address_id`|path|integer(int64)|true||

> Example responses

> 200 Response

```json
{
  "address_id": "1",
  "country": "US",
  "is_billing": "0",
  "is_physical": "0",
  "is_shipping": "0",
  "latitude": "-90",
  "line_1": "321 Chase Rd",
  "line_2": "P.O. Box 256",
  "line_3": "3rd Floor",
  "line_4": "Last door on the left (blue)",
  "locality": "Sequim",
  "longitude": "-180",
  "postcode": "98368",
  "region": "WA"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressModel](#schemacustomeraddressmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Get Address

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id} \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id}");
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

`GET /customers/{customer_id}/addresses/{address_id}`

<a id="opIdget_customers_by_id_addresses_by_id"></a>

Get a customer address.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||
|`address_id`|path|integer(int64)|true||

> Example responses

> 200 Response

```json
{
  "address_id": "1",
  "country": "US",
  "is_billing": "0",
  "is_physical": "0",
  "is_shipping": "0",
  "latitude": "-90",
  "line_1": "321 Chase Rd",
  "line_2": "P.O. Box 256",
  "line_3": "3rd Floor",
  "line_4": "Last door on the left (blue)",
  "locality": "Sequim",
  "longitude": "-180",
  "postcode": "98368",
  "region": "WA"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressModel](#schemacustomeraddressmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### List Addresses

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers/{customer_id}/addresses";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/customers/{customer_id}/addresses \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/addresses',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/customers/{customer_id}/addresses',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/customers/{customer_id}/addresses', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/addresses");
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

`GET /customers/{customer_id}/addresses`

<a id="opIdget_customers_by_id_addresses"></a>

List customer addresses.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||
|`filter_active`|query|boolean|false||
|`page_limit`|query|integer(int64)|false||
|`page_index`|query|integer(int64)|false||

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "address_id": "1",
      "country": "US",
      "is_billing": "0",
      "is_physical": "0",
      "is_shipping": "0",
      "latitude": "-90",
      "line_1": "321 Chase Rd",
      "line_2": "P.O. Box 256",
      "line_3": "3rd Floor",
      "line_4": "Last door on the left (blue)",
      "locality": "Sequim",
      "longitude": "-180",
      "postcode": "98368",
      "region": "WA"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressListModel](#schemacustomeraddresslistmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Update Address

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadValues(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id}',
  method: 'patch',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.patch('https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/addresses/{address_id}");
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

`PATCH /customers/{customer_id}/addresses/{address_id}`

<a id="opIdpatch_customers_by_id_addresses_by_id"></a>

Update a customer address.

> Body parameter

```json
{
  "country": "US",
  "is_billing": "0",
  "is_shipping": "0",
  "latitude": "-90",
  "line_1": "321 Chase Rd",
  "line_2": "P.O. Box 256",
  "line_3": "3rd Floor",
  "line_4": "Last door on the left (blue)",
  "locality": "Sequim",
  "longitude": "-180",
  "postcode": "98368",
  "region": "WA"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||
|`address_id`|path|integer(int64)|true||
|`body`|body|[UpdateCustomerAddressModel](#schemaupdatecustomeraddressmodel)|true||

> Example responses

> 200 Response

```json
{
  "address_id": "1",
  "country": "US",
  "is_billing": "0",
  "is_physical": "0",
  "is_shipping": "0",
  "latitude": "-90",
  "line_1": "321 Chase Rd",
  "line_2": "P.O. Box 256",
  "line_3": "3rd Floor",
  "line_4": "Last door on the left (blue)",
  "locality": "Sequim",
  "longitude": "-180",
  "postcode": "98368",
  "region": "WA"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressModel](#schemacustomeraddressmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

## Customer Contacts

### Create Contact

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers/{customer_id}/contacts";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadValues(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/customers/{customer_id}/contacts \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/contacts',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/customers/{customer_id}/contacts',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.post('https://api.crosoftware.net/customers/{customer_id}/contacts', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/contacts");
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

`POST /customers/{customer_id}/contacts`

<a id="opIdpost_customers_by_id_contacts"></a>

Create new customer contact.

> Body parameter

```json
{
  "email": "support@crosoftware.net",
  "fax": "+1 (360) 733-1649",
  "name": "John C. Doe",
  "notify_on_acknowledged_request": "0",
  "notify_on_completed_request": "0",
  "notify_on_dispatched_request": "0",
  "notify_on_failed_request": "0",
  "notify_on_new_request": "0",
  "number": "+1 (360) 733-1649"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||
|`body`|body|[CreateCustomerContactModel](#schemacreatecustomercontactmodel)|true||

> Example responses

> 200 Response

```json
{
  "contact_id": "1",
  "email": "support@crosoftware.net",
  "fax": "+1 (360) 733-1649",
  "name": "John C. Doe",
  "notify_on_acknowledged_request": "0",
  "notify_on_completed_request": "0",
  "notify_on_dispatched_request": "0",
  "notify_on_failed_request": "0",
  "notify_on_new_request": "0",
  "number": "+1 (360) 733-1649"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerContactModel](#schemacustomercontactmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Get Contact

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers/{customer_id}/contacts/{contact_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/customers/{customer_id}/contacts/{contact_id} \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/contacts/{contact_id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/customers/{customer_id}/contacts/{contact_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/customers/{customer_id}/contacts/{contact_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/contacts/{contact_id}");
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

`GET /customers/{customer_id}/contacts/{contact_id}`

<a id="opIdget_customers_by_id_contacts_by_id"></a>

Get a customer contact.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||
|`contact_id`|path|integer(int64)|true||

> Example responses

> 200 Response

```json
{
  "contact_id": "1",
  "email": "support@crosoftware.net",
  "fax": "+1 (360) 733-1649",
  "name": "John C. Doe",
  "notify_on_acknowledged_request": "0",
  "notify_on_completed_request": "0",
  "notify_on_dispatched_request": "0",
  "notify_on_failed_request": "0",
  "notify_on_new_request": "0",
  "number": "+1 (360) 733-1649"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerContactModel](#schemacustomercontactmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### List Contacts

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers/{customer_id}/contacts";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/customers/{customer_id}/contacts \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/contacts',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/customers/{customer_id}/contacts',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/customers/{customer_id}/contacts', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/contacts");
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

`GET /customers/{customer_id}/contacts`

<a id="opIdget_customers_by_id_contacts"></a>

List customer contacts.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||
|`page_limit`|query|integer(int64)|false||
|`page_index`|query|integer(int64)|false||

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "contact_id": "1",
      "email": "support@crosoftware.net",
      "fax": "+1 (360) 733-1649",
      "name": "John C. Doe",
      "notify_on_acknowledged_request": "0",
      "notify_on_completed_request": "0",
      "notify_on_dispatched_request": "0",
      "notify_on_failed_request": "0",
      "notify_on_new_request": "0",
      "number": "+1 (360) 733-1649"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerContactListModel](#schemacustomercontactlistmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Update Contact

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers/{customer_id}/contacts/{contact_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadValues(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/customers/{customer_id}/contacts/{contact_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/contacts/{contact_id}',
  method: 'patch',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/customers/{customer_id}/contacts/{contact_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.patch('https://api.crosoftware.net/customers/{customer_id}/contacts/{contact_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/contacts/{contact_id}");
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

`PATCH /customers/{customer_id}/contacts/{contact_id}`

<a id="opIdpatch_customers_by_id_contacts_by_id"></a>

Update a customer contact.

> Body parameter

```json
{
  "email": "support@crosoftware.net",
  "fax": "+1 (360) 733-1649",
  "name": "John C. Doe",
  "notify_on_acknowledged_request": "0",
  "notify_on_completed_request": "0",
  "notify_on_dispatched_request": "0",
  "notify_on_failed_request": "0",
  "notify_on_new_request": "0",
  "number": "+1 (360) 733-1649"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||
|`contact_id`|path|integer(int64)|true||
|`body`|body|[UpdateCustomerContactModel](#schemaupdatecustomercontactmodel)|true||

> Example responses

> 200 Response

```json
{
  "contact_id": "1",
  "email": "support@crosoftware.net",
  "fax": "+1 (360) 733-1649",
  "name": "John C. Doe",
  "notify_on_acknowledged_request": "0",
  "notify_on_completed_request": "0",
  "notify_on_dispatched_request": "0",
  "notify_on_failed_request": "0",
  "notify_on_new_request": "0",
  "number": "+1 (360) 733-1649"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerContactModel](#schemacustomercontactmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

## Customer Locations

### Add Customer Location

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadValues(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.post('https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}");
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

`POST /customers/{customer_id}/locations/{customer_id}`

<a id="opIdpost_customers_by_id_locations_by_id"></a>

Add customer location profile.

> Body parameter

```json
{
  "is_commercial": "0",
  "note": "Bin located in alley.",
  "reference_number": "REF#100A61",
  "renewal_date": "2018-10-31T11:32:38.390000",
  "sales_rep": "John C. Doe",
  "suspension_id": "1"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||
|`body`|body|[CreateCustomerLocationModel](#schemacreatecustomerlocationmodel)|true||

> Example responses

> 200 Response

```json
{
  "id": "1",
  "is_commercial": "0",
  "note": "Bin located in alley.",
  "reference_number": "REF#100A61",
  "renewal_date": "2018-10-31T11:32:38.390000",
  "sales_rep": "John C. Doe",
  "suspension_id": "1"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationModel](#schemacustomerlocationmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Deactivate Customer

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadValues(url, "DELETE", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X DELETE https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id} \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}',
  method: 'delete',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.delete 'https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.delete('https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
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

`DELETE /customers/{customer_id}/locations/{customer_id}`

<a id="opIddelete_customers_by_id_locations_by_id"></a>

Deactivate (soft delete) customer location profile.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||

> Example responses

> 200 Response

```json
{
  "id": "1",
  "is_commercial": "0",
  "note": "Bin located in alley.",
  "reference_number": "REF#100A61",
  "renewal_date": "2018-10-31T11:32:38.390000",
  "sales_rep": "John C. Doe",
  "suspension_id": "1"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationModel](#schemacustomerlocationmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Get Customer Location

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id} \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}");
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

`GET /customers/{customer_id}/locations/{customer_id}`

<a id="opIdget_customers_by_id_locations_by_id"></a>

Get a customer contact.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||

> Example responses

> 200 Response

```json
{
  "id": "1",
  "is_commercial": "0",
  "note": "Bin located in alley.",
  "reference_number": "REF#100A61",
  "renewal_date": "2018-10-31T11:32:38.390000",
  "sales_rep": "John C. Doe",
  "suspension_id": "1"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationModel](#schemacustomerlocationmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### List Customer Locations

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers/{customer_id}/locations";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/customers/{customer_id}/locations \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/locations',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/customers/{customer_id}/locations',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/customers/{customer_id}/locations', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/locations");
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

`GET /customers/{customer_id}/locations`

<a id="opIdget_customers_by_id_locations"></a>

Update customer location profile.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||
|`filter_active`|query|boolean|false||
|`page_limit`|query|integer(int64)|false||
|`page_index`|query|integer(int64)|false||

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "id": "1",
      "is_commercial": "0",
      "note": "Bin located in alley.",
      "reference_number": "REF#100A61",
      "renewal_date": "2018-10-31T11:32:38.390000",
      "sales_rep": "John C. Doe",
      "suspension_id": "1"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationListModel](#schemacustomerlocationlistmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Update Customer Location

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadValues(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}',
  method: 'patch',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.patch('https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/locations/{customer_id}");
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

`PATCH /customers/{customer_id}/locations/{customer_id}`

<a id="opIdpatch_customers_by_id_locations_by_id"></a>

Update customer location profile.

> Body parameter

```json
{
  "is_commercial": "0",
  "note": "Bin located in alley.",
  "reference_number": "REF#100A61",
  "renewal_date": "2018-10-31T11:32:38.390000",
  "sales_rep": "John C. Doe",
  "suspension_id": "1"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||
|`body`|body|[UpdateCustomerLocationModel](#schemaupdatecustomerlocationmodel)|true||

> Example responses

> 200 Response

```json
{
  "id": "1",
  "is_commercial": "0",
  "note": "Bin located in alley.",
  "reference_number": "REF#100A61",
  "renewal_date": "2018-10-31T11:32:38.390000",
  "sales_rep": "John C. Doe",
  "suspension_id": "1"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationModel](#schemacustomerlocationmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

## Customers

### Create Customer

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/locations/{location_id}/customers";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadValues(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/locations/{location_id}/customers \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/customers',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/locations/{location_id}/customers',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.post('https://api.crosoftware.net/locations/{location_id}/customers', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/customers");
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

`POST /locations/{location_id}/customers`

<a id="opIdpost_locations_by_id_customers"></a>

Create customer for location.

> Body parameter

```json
{
  "addresses": [
    {
      "country": "US",
      "is_billing": "0",
      "is_shipping": "0",
      "latitude": "-90",
      "line_1": "321 Chase Rd",
      "line_2": "P.O. Box 256",
      "line_3": "3rd Floor",
      "line_4": "Last door on the left (blue)",
      "locality": "Sequim",
      "longitude": "-180",
      "postcode": "98368",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "email": "support@crosoftware.net",
      "fax": "+1 (360) 733-1649",
      "name": "John C. Doe",
      "notify_on_acknowledged_request": "0",
      "notify_on_completed_request": "0",
      "notify_on_dispatched_request": "0",
      "notify_on_failed_request": "0",
      "notify_on_new_request": "0",
      "number": "+1 (360) 733-1649"
    }
  ],
  "is_commercial": "0",
  "name": "John C. Doe",
  "note": "Bin located in alley.",
  "parent_id": "1",
  "reference_number": "REF#100A61",
  "renewal_date": "2018-10-31T11:32:38.390000",
  "sales_rep": "John C. Doe",
  "suspension_id": "1"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`location_id`|path|integer(int64)|true||
|`body`|body|[CreateCustomerModel](#schemacreatecustomermodel)|true||

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "country": "US",
      "is_billing": "0",
      "is_shipping": "0",
      "latitude": "-90",
      "line_1": "321 Chase Rd",
      "line_2": "P.O. Box 256",
      "line_3": "3rd Floor",
      "line_4": "Last door on the left (blue)",
      "locality": "Sequim",
      "longitude": "-180",
      "postcode": "98368",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "email": "support@crosoftware.net",
      "fax": "+1 (360) 733-1649",
      "name": "John C. Doe",
      "notify_on_acknowledged_request": "0",
      "notify_on_completed_request": "0",
      "notify_on_dispatched_request": "0",
      "notify_on_failed_request": "0",
      "notify_on_new_request": "0",
      "number": "+1 (360) 733-1649"
    }
  ],
  "is_commercial": "0",
  "name": "John C. Doe",
  "note": "Bin located in alley.",
  "parent_id": "1",
  "reference_number": "REF#100A61",
  "renewal_date": "2018-10-31T11:32:38.390000",
  "sales_rep": "John C. Doe",
  "suspension_id": "1"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CreateCustomerModel](#schemacreatecustomermodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Get Customer

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers/{customer_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/customers/{customer_id} \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/customers/{customer_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/customers/{customer_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}");
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

`GET /customers/{customer_id}`

<a id="opIdget_customers_by_id"></a>

Customer model.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "country": "US",
      "is_billing": "0",
      "is_shipping": "0",
      "latitude": "-90",
      "line_1": "321 Chase Rd",
      "line_2": "P.O. Box 256",
      "line_3": "3rd Floor",
      "line_4": "Last door on the left (blue)",
      "locality": "Sequim",
      "longitude": "-180",
      "postcode": "98368",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "email": "support@crosoftware.net",
      "fax": "+1 (360) 733-1649",
      "name": "John C. Doe",
      "notify_on_acknowledged_request": "0",
      "notify_on_completed_request": "0",
      "notify_on_dispatched_request": "0",
      "notify_on_failed_request": "0",
      "notify_on_new_request": "0",
      "number": "+1 (360) 733-1649"
    }
  ],
  "customer_id": "1",
  "is_commercial": "0",
  "name": "John C. Doe",
  "note": "Bin located in alley.",
  "parent_id": "1",
  "reference_number": "REF#100A61",
  "renewal_date": "2018-10-31T11:32:38.390000",
  "sales_rep": "John C. Doe",
  "suspension_id": "1"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerModel](#schemacustomermodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Get Customer for Location

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/locations/{location_id}/customers/{customer_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id}/customers/{customer_id} \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/customers/{customer_id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}/customers/{customer_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}/customers/{customer_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/customers/{customer_id}");
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

`GET /locations/{location_id}/customers/{customer_id}`

<a id="opIdget_locations_by_id_customers_by_id"></a>

Get customer for location.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`location_id`|path|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||

> Example responses

> 200 Response

```json
{
  "id": "1",
  "is_commercial": "0",
  "note": "Bin located in alley.",
  "reference_number": "REF#100A61",
  "renewal_date": "2018-10-31T11:32:38.390000",
  "sales_rep": "John C. Doe",
  "suspension_id": "1"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationModel](#schemacustomerlocationmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### List Customers

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/customers \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/customers',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/customers', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers");
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

`GET /customers`

<a id="opIdget_customers"></a>

List of customers.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`name`|query|string|false||
|`last_updated_gte`|query|string(DateTime)|false||
|`created_on_gte`|query|string(DateTime)|false||
|`page_limit`|query|integer(int64)|false||
|`page_index`|query|integer(int64)|false||

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "addresses": [
        {
          "country": "US",
          "is_billing": "0",
          "is_shipping": "0",
          "latitude": "-90",
          "line_1": "321 Chase Rd",
          "line_2": "P.O. Box 256",
          "line_3": "3rd Floor",
          "line_4": "Last door on the left (blue)",
          "locality": "Sequim",
          "longitude": "-180",
          "postcode": "98368",
          "region": "WA"
        }
      ],
      "contacts": [
        {
          "email": "support@crosoftware.net",
          "fax": "+1 (360) 733-1649",
          "name": "John C. Doe",
          "notify_on_acknowledged_request": "0",
          "notify_on_completed_request": "0",
          "notify_on_dispatched_request": "0",
          "notify_on_failed_request": "0",
          "notify_on_new_request": "0",
          "number": "+1 (360) 733-1649"
        }
      ],
      "customer_id": "1",
      "is_commercial": "0",
      "name": "John C. Doe",
      "note": "Bin located in alley.",
      "parent_id": "1",
      "reference_number": "REF#100A61",
      "renewal_date": "2018-10-31T11:32:38.390000",
      "sales_rep": "John C. Doe",
      "suspension_id": "1"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerListModel](#schemacustomerlistmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### List Customers for Location

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/locations/{location_id}/customers";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id}/customers \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/customers',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}/customers',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}/customers', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/customers");
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

`GET /locations/{location_id}/customers`

<a id="opIdget_locations_by_id_customers"></a>

List customers for location.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`location_id`|path|integer(int64)|true||
|`name`|query|string|false||
|`page_limit`|query|integer(int64)|false||
|`page_index`|query|integer(int64)|false||

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "id": "1",
      "is_commercial": "0",
      "note": "Bin located in alley.",
      "reference_number": "REF#100A61",
      "renewal_date": "2018-10-31T11:32:38.390000",
      "sales_rep": "John C. Doe",
      "suspension_id": "1"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationListModel](#schemacustomerlocationlistmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Update Customer

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/customers/{customer_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadValues(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/customers/{customer_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}',
  method: 'patch',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/customers/{customer_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.patch('https://api.crosoftware.net/customers/{customer_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}");
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

`PATCH /customers/{customer_id}`

<a id="opIdpatch_customers_by_id"></a>

Customer model.

> Body parameter

```json
{
  "name": "John C. Doe",
  "parent_id": "1"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`customer_id`|path|integer(int64)|true||
|`body`|body|[UpdateCustomerModel](#schemaupdatecustomermodel)|true||

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "country": "US",
      "is_billing": "0",
      "is_shipping": "0",
      "latitude": "-90",
      "line_1": "321 Chase Rd",
      "line_2": "P.O. Box 256",
      "line_3": "3rd Floor",
      "line_4": "Last door on the left (blue)",
      "locality": "Sequim",
      "longitude": "-180",
      "postcode": "98368",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "email": "support@crosoftware.net",
      "fax": "+1 (360) 733-1649",
      "name": "John C. Doe",
      "notify_on_acknowledged_request": "0",
      "notify_on_completed_request": "0",
      "notify_on_dispatched_request": "0",
      "notify_on_failed_request": "0",
      "notify_on_new_request": "0",
      "number": "+1 (360) 733-1649"
    }
  ],
  "customer_id": "1",
  "is_commercial": "0",
  "name": "John C. Doe",
  "note": "Bin located in alley.",
  "parent_id": "1",
  "reference_number": "REF#100A61",
  "renewal_date": "2018-10-31T11:32:38.390000",
  "sales_rep": "John C. Doe",
  "suspension_id": "1"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerModel](#schemacustomermodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

## Drivers

### Get Driver

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/locations/{location_id}/drivers/{driver_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id}/drivers/{driver_id} \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/drivers/{driver_id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}/drivers/{driver_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}/drivers/{driver_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/drivers/{driver_id}");
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

`GET /locations/{location_id}/drivers/{driver_id}`

<a id="opIdget_locations_by_id_drivers_by_id"></a>

Get driver.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`location_id`|path|integer(int64)|true||
|`driver_id`|path|integer(int64)|true||

> Example responses

> 200 Response

```json
{
  "address": "321 Chase Rd",
  "can_convert_to_group": "0",
  "can_create_requests": "0",
  "can_edit_requests": "0",
  "can_reposition_asset": "0",
  "city": "Sequim",
  "disable_shift_tracking": "0",
  "email": "support@crosoftware.net",
  "id": "1",
  "license_number": "12ZA24WA-21",
  "location_id": "1",
  "name": "John C. Doe",
  "phone_number": "+1 (360) 733-1649",
  "state": "WA",
  "third_party_hauler_id": "defbc66e-f908-40d9-9ee5-655a1f699311",
  "zip": "98368"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DriverModel](#schemadrivermodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### List Drivers

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/locations/{location_id}/drivers";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id}/drivers \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/drivers',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}/drivers',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}/drivers', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/drivers");
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

`GET /locations/{location_id}/drivers`

<a id="opIdget_locations_by_id_drivers"></a>

List drivers.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`location_id`|path|integer(int64)|true||
|`page_limit`|query|integer(int64)|false||
|`page_index`|query|integer(int64)|false||

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "address": "321 Chase Rd",
      "can_convert_to_group": "0",
      "can_create_requests": "0",
      "can_edit_requests": "0",
      "can_reposition_asset": "0",
      "city": "Sequim",
      "disable_shift_tracking": "0",
      "email": "support@crosoftware.net",
      "id": "1",
      "license_number": "12ZA24WA-21",
      "location_id": "1",
      "name": "John C. Doe",
      "phone_number": "+1 (360) 733-1649",
      "state": "WA",
      "third_party_hauler_id": "defbc66e-f908-40d9-9ee5-655a1f699311",
      "zip": "98368"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DriverListModel](#schemadriverlistmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

## GPS

### Log GPS Event

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/locations/{location_id}/gps_events";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadValues(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/locations/{location_id}/gps_events \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/gps_events',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/locations/{location_id}/gps_events',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.post('https://api.crosoftware.net/locations/{location_id}/gps_events', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/gps_events");
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

`POST /locations/{location_id}/gps_events`

<a id="opIdpost_locations_by_id_gps_events"></a>

Log a GPS event.

> Body parameter

```json
{
  "location": {
    "coords": {
      "heading": "0",
      "latitude": "-90",
      "longitude": "-180",
      "speed": "0"
    },
    "timestamp": "2018-10-31T11:32:38.390000"
  }
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`location_id`|path|integer(int64)|true||
|`body`|body|[GpsEventProfileModel](#schemagpseventprofilemodel)|true||

> Example responses

> 200 Response

```json
{
  "bearing": "0",
  "created_on": "2018-10-31T11:32:38.390000",
  "device_name": "John C. Doe",
  "driver_id": "1",
  "id": "1",
  "latitude": "-90",
  "longitude": "-180",
  "truck_id": "1",
  "velocity": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[GpsStopModel](#schemagpsstopmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

## Haulers

### Create Connection

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/haulers/{hauler_uuid}/connections";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          // Parameters
          NameValueCollection parameters = new NameValueCollection();
          parameters.Add("tenant_code", "CROSCRAPCO+101");
          
          byte[] json = client.UploadValues(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/haulers/{hauler_uuid}/connections?tenant_code=CROSCRAPCO%2B101 \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/haulers/{hauler_uuid}/connections',
  method: 'post',
  data: '?tenant_code=CROSCRAPCO%2B101',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/haulers/{hauler_uuid}/connections',
  params: {
  'tenant_code' => 'string'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.post('https://api.crosoftware.net/haulers/{hauler_uuid}/connections', params={
  'tenant_code': 'CROSCRAPCO+101'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/haulers/{hauler_uuid}/connections?tenant_code=CROSCRAPCO%2B101");
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

`POST /haulers/{hauler_uuid}/connections`

<a id="opIdpost_haulers_by_id_connections"></a>

Create third party connection.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`hauler_uuid`|path|string(Uuid)|true||
|`tenant_code`|query|string|true||

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": {
    "approved_by": "1",
    "approved_on": "2018-10-31T11:32:38.390000",
    "denied_on": "2018-10-31T11:32:38.390000",
    "is_approved": "0",
    "location_id": "1",
    "provider_email": "support@crosoftware.net",
    "provider_id": "1",
    "provider_name": "John C. Doe",
    "provider_phone": "+1 (360) 733-1649",
    "requested_on": "2018-10-31T11:32:38.390000"
  },
  "total_count": "0",
  "total_pages": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerConnectionListModel](#schemathirdpartyhaulerconnectionlistmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Create Hauler

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/haulers";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          // Parameters
          NameValueCollection parameters = new NameValueCollection();
          parameters.Add("company_name", "CRO Scrap Example Inc.");
          parameters.Add("username", "a_user@crosoftware.net");
          parameters.Add("password", "cro1sher3!");
          parameters.Add("recaptcha", "<recaptcha-string>");
          
          byte[] json = client.UploadValues(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/haulers?company_name=CRO%20Scrap%20Example%20Inc.&username=a_user%40crosoftware.net&password=cro1sher3%21&recaptcha=%3Crecaptcha-string%3E \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/haulers',
  method: 'post',
  data: '?company_name=CRO%20Scrap%20Example%20Inc.&username=a_user%40crosoftware.net&password=cro1sher3%21&recaptcha=%3Crecaptcha-string%3E',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/haulers',
  params: {
  'company_name' => 'string',
'username' => 'string',
'password' => 'string',
'recaptcha' => 'string'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.post('https://api.crosoftware.net/haulers', params={
  'company_name': 'CRO Scrap Example Inc.',  'username': 'a_user@crosoftware.net',  'password': 'cro1sher3!',  'recaptcha': '<recaptcha-string>'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/haulers?company_name=CRO%20Scrap%20Example%20Inc.&username=a_user%40crosoftware.net&password=cro1sher3%21&recaptcha=%3Crecaptcha-string%3E");
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

`POST /haulers`

<a id="opIdpost_haulers"></a>

Create third party hauler.

<aside class="success">
This operation does not require authentication
</aside>

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`company_name`|query|string|true||
|`username`|query|string|true||
|`password`|query|string|true||
|`recaptcha`|query|string|true||

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": {
    "approved_by": "1",
    "approved_on": "2018-10-31T11:32:38.390000",
    "denied_on": "2018-10-31T11:32:38.390000",
    "is_approved": "0",
    "location_id": "1",
    "provider_email": "support@crosoftware.net",
    "provider_id": "1",
    "provider_name": "John C. Doe",
    "provider_phone": "+1 (360) 733-1649",
    "requested_on": "2018-10-31T11:32:38.390000"
  },
  "total_count": "0",
  "total_pages": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerConnectionListModel](#schemathirdpartyhaulerconnectionlistmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Get Hauler

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/haulers/{hauler_uuid}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/haulers/{hauler_uuid} \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/haulers/{hauler_uuid}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/haulers/{hauler_uuid}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/haulers/{hauler_uuid}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/haulers/{hauler_uuid}");
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

`GET /haulers/{hauler_uuid}`

<a id="opIdget_haulers_by_id"></a>

Get third party hauler.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`hauler_uuid`|path|string(Uuid)|true||

> Example responses

> 200 Response

```json
{
  "id": "defbc66e-f908-40d9-9ee5-655a1f699311",
  "name": "John C. Doe"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerModel](#schemathirdpartyhaulermodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### List Connections

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/haulers/{hauler_uuid}/connections";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/haulers/{hauler_uuid}/connections \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/haulers/{hauler_uuid}/connections',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/haulers/{hauler_uuid}/connections',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/haulers/{hauler_uuid}/connections', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/haulers/{hauler_uuid}/connections");
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

`GET /haulers/{hauler_uuid}/connections`

<a id="opIdget_haulers_by_id_connections"></a>

List third party hauler connections.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`hauler_uuid`|path|string(Uuid)|true||
|`page_limit`|query|integer(int64)|false||
|`page_index`|query|integer(int64)|false||

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": {
    "approved_by": "1",
    "approved_on": "2018-10-31T11:32:38.390000",
    "denied_on": "2018-10-31T11:32:38.390000",
    "is_approved": "0",
    "location_id": "1",
    "provider_email": "support@crosoftware.net",
    "provider_id": "1",
    "provider_name": "John C. Doe",
    "provider_phone": "+1 (360) 733-1649",
    "requested_on": "2018-10-31T11:32:38.390000"
  },
  "total_count": "0",
  "total_pages": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerConnectionListModel](#schemathirdpartyhaulerconnectionlistmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### List Haulers

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/haulers";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/haulers \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/haulers',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/haulers',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/haulers', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/haulers");
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

`GET /haulers`

<a id="opIdget_haulers"></a>

List third party haulers.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`page_limit`|query|integer(int64)|false||
|`page_index`|query|integer(int64)|false||

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "id": "defbc66e-f908-40d9-9ee5-655a1f699311",
      "name": "John C. Doe"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerListModel](#schemathirdpartyhaulerlistmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

## Jobs

### Dispatch Job

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/locations/{location_id}/jobs/{job_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadValues(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/locations/{location_id}/jobs/{job_id} \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/jobs/{job_id}',
  method: 'patch',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/locations/{location_id}/jobs/{job_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.patch('https://api.crosoftware.net/locations/{location_id}/jobs/{job_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/jobs/{job_id}");
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

`PATCH /locations/{location_id}/jobs/{job_id}`

<a id="opIdpatch_locations_by_id_jobs_by_id"></a>

Dispatch a job by id.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`location_id`|path|integer(int64)|true||
|`job_id`|path|integer(int64)|true||
|`truck_id`|query|boolean|false||
|`new_schedule_date`|query|string(DateTime)|false||

> Example responses

> 200 Response

```json
{
  "arrived_at_dest": "2018-10-31T11:32:38.390000",
  "arrived_on": "2018-10-31T11:32:38.390000",
  "asset_dropped": "0",
  "asset_id": "1",
  "asset_quantity": "0",
  "asset_type_id": "1",
  "completed_by": "1",
  "completed_by_driver": "0",
  "completed_on": "2018-10-31T11:32:38.390000",
  "confirmed_on": "2018-10-31T11:32:38.390000",
  "created_by_id": "1",
  "customer_id": "1",
  "customer_notes": "Some notes from a customer to a dispatcher.",
  "desired_asset_desc": "Some asset characteristics.",
  "dispatch_priority": "H",
  "dispatched_by_route": "1",
  "dispatched_on": "2018-10-31T11:32:38.390000",
  "dispatcher_notes": "Some dispatcher notes.",
  "do_confirm": "0",
  "driver_notes": "Some driver notes.",
  "dump_location_id": "1",
  "dumped_on": "2018-10-31T11:32:38.390000",
  "end_time": "2018-10-31T11:32:38.390000",
  "fail_reason": "A reason for failure.",
  "final_location_id": "1",
  "flags": "A reason for failure.",
  "id": "1",
  "invoice_notes": "Some invoice notes.",
  "is_completed": "0",
  "is_declined": "0",
  "is_deleted": "0",
  "is_failed": "0",
  "job_group_id": "1",
  "location_id": "1",
  "merged_with_route": "1",
  "original_schedule_date": "2018-10-31T11:32:38.390000",
  "pickup_date": "2018-10-31T11:32:38.390000",
  "priority": "-999999",
  "reference_number": "REF#100A61",
  "requested_on": "2018-10-31T11:32:38.390000",
  "require_image": "0",
  "require_material": "0",
  "require_signature": "0",
  "require_weights": "0",
  "schedule_date": "2018-10-31T11:32:38.390000",
  "start_location_id": "1",
  "start_time": "2018-10-31T11:32:38.390000",
  "third_party_hauler_id": "defbc66e-f908-40d9-9ee5-655a1f699311",
  "times_failed": "0",
  "times_rolled_over": "0",
  "truck_id": "1",
  "type": "R",
  "weighed_on": "2018-10-31T11:32:38.390000"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[UpdatedJobModel](#schemaupdatedjobmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Get Job

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/locations/{location_id}/jobs/{job_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id}/jobs/{job_id} \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/jobs/{job_id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}/jobs/{job_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}/jobs/{job_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/jobs/{job_id}");
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

`GET /locations/{location_id}/jobs/{job_id}`

<a id="opIdget_locations_by_id_jobs_by_id"></a>

Get job by id.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`location_id`|path|integer(int64)|true||
|`job_id`|path|integer(int64)|true||

> Example responses

> 200 Response

```json
{
  "arrived_at_dest": "2018-10-31T11:32:38.390000",
  "arrived_on": "2018-10-31T11:32:38.390000",
  "asset": {
    "asset_type": {
      "deleted": "0",
      "id": "1",
      "is_default": "0",
      "location_id": "1",
      "name": "John C. Doe",
      "quantity": "0",
      "require_numbers": "0",
      "weight": "0"
    },
    "asset_type_id": "1",
    "cluster": "1",
    "customer_id": "1",
    "description": "Some description.",
    "dispatched_on": "2018-10-31T11:32:38.390000",
    "id": "1",
    "is_returned": "0",
    "last_activity_on": "2018-10-31T11:32:38.390000",
    "last_rental_invoice_on": "2018-10-31T11:32:38.390000",
    "latitude": "-90",
    "location": {
      "id": "1",
      "is_active": "0",
      "name": "John C. Doe"
    },
    "location_id": "1",
    "longitude": "-180",
    "number": "+1 (360) 733-1649",
    "quantity": "0",
    "returned_on": "2018-10-31T11:32:38.390000"
  },
  "asset_dropped": "0",
  "asset_id": "1",
  "asset_quantity": "0",
  "asset_type": {
    "deleted": "0",
    "id": "1",
    "is_default": "0",
    "location_id": "1",
    "name": "John C. Doe",
    "quantity": "0",
    "require_numbers": "0",
    "weight": "0"
  },
  "asset_type_id": "1",
  "completed_by": "1",
  "completed_by_driver": "0",
  "completed_on": "2018-10-31T11:32:38.390000",
  "confirmed_on": "2018-10-31T11:32:38.390000",
  "created_by_id": "1",
  "customer": {
    "addresses": [
      {
        "country": "US",
        "is_billing": "0",
        "is_shipping": "0",
        "latitude": "-90",
        "line_1": "321 Chase Rd",
        "line_2": "P.O. Box 256",
        "line_3": "3rd Floor",
        "line_4": "Last door on the left (blue)",
        "locality": "Sequim",
        "longitude": "-180",
        "postcode": "98368",
        "region": "WA"
      }
    ],
    "contacts": [
      {
        "email": "support@crosoftware.net",
        "fax": "+1 (360) 733-1649",
        "name": "John C. Doe",
        "notify_on_acknowledged_request": "0",
        "notify_on_completed_request": "0",
        "notify_on_dispatched_request": "0",
        "notify_on_failed_request": "0",
        "notify_on_new_request": "0",
        "number": "+1 (360) 733-1649"
      }
    ],
    "customer_id": "1",
    "is_commercial": "0",
    "name": "John C. Doe",
    "note": "Bin located in alley.",
    "parent_id": "1",
    "reference_number": "REF#100A61",
    "renewal_date": "2018-10-31T11:32:38.390000",
    "sales_rep": "John C. Doe",
    "suspension_id": "1"
  },
  "customer_id": "1",
  "customer_notes": "Some notes from a customer to a dispatcher.",
  "desired_asset_desc": "Some asset characteristics.",
  "dispatch_priority": "H",
  "dispatched_by_route": "1",
  "dispatched_on": "2018-10-31T11:32:38.390000",
  "dispatcher_notes": "Some dispatcher notes.",
  "do_confirm": "0",
  "driver_notes": "Some driver notes.",
  "dump_location": {
    "id": "1",
    "is_active": "0",
    "name": "John C. Doe"
  },
  "dump_location_id": "1",
  "dumped_on": "2018-10-31T11:32:38.390000",
  "end_time": "2018-10-31T11:32:38.390000",
  "fail_reason": "A reason for failure.",
  "final_location": {
    "id": "1",
    "is_active": "0",
    "name": "John C. Doe"
  },
  "final_location_id": "1",
  "flags": "A reason for failure.",
  "invoice_notes": "Some invoice notes.",
  "is_completed": "0",
  "is_declined": "0",
  "is_deleted": "0",
  "is_failed": "0",
  "job_group_id": "1",
  "location_id": "1",
  "merged_with_route": "1",
  "original_schedule_date": "2018-10-31T11:32:38.390000",
  "pickup_date": "2018-10-31T11:32:38.390000",
  "priority": "-999999",
  "reference_number": "REF#100A61",
  "requested_on": "2018-10-31T11:32:38.390000",
  "require_image": "0",
  "require_material": "0",
  "require_signature": "0",
  "require_weights": "0",
  "schedule_date": "2018-10-31T11:32:38.390000",
  "start_location": {
    "id": "1",
    "is_active": "0",
    "name": "John C. Doe"
  },
  "start_location_id": "1",
  "start_time": "2018-10-31T11:32:38.390000",
  "third_party_hauler_id": "defbc66e-f908-40d9-9ee5-655a1f699311",
  "times_failed": "0",
  "times_rolled_over": "0",
  "truck_id": "1",
  "type": "R",
  "weighed_on": "2018-10-31T11:32:38.390000"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[JobModel](#schemajobmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### List Jobs

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/locations/{location_id}/jobs";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          // Parameters
          NameValueCollection parameters = new NameValueCollection();
          parameters.Add("schedule_gt", "2018-10-31T11:32:38.390000");
          parameters.Add("schedule_lt", "2018-10-31T11:32:38.390000");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id}/jobs?schedule_gt=2018-10-31T11%3A32%3A38.390000&schedule_lt=2018-10-31T11%3A32%3A38.390000 \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/jobs',
  method: 'get',
  data: '?schedule_gt=2018-10-31T11%3A32%3A38.390000&schedule_lt=2018-10-31T11%3A32%3A38.390000',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}/jobs',
  params: {
  'schedule_gt' => 'string(DateTime)',
'schedule_lt' => 'string(DateTime)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}/jobs', params={
  'schedule_gt': '2018-10-31T11:32:38.390000',  'schedule_lt': '2018-10-31T11:32:38.390000'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/jobs?schedule_gt=2018-10-31T11%3A32%3A38.390000&schedule_lt=2018-10-31T11%3A32%3A38.390000");
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

`GET /locations/{location_id}/jobs`

<a id="opIdget_locations_by_id_jobs"></a>

List jobs.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`location_id`|path|integer(int64)|true||
|`page_limit`|query|integer(int64)|false||
|`page_index`|query|integer(int64)|false||
|`schedule_gt`|query|string(DateTime)|true||
|`schedule_lt`|query|string(DateTime)|true||
|`deleted`|query|boolean|false||
|`completed`|query|boolean|false||
|`failed`|query|boolean|false||
|`driver_id`|query|boolean|false||
|`truck_id`|query|boolean|false||
|`last_updated_gte`|query|string(DateTime)|false||
|`created_on_gte`|query|string(DateTime)|false||

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "arrived_at_dest": "2018-10-31T11:32:38.390000",
      "arrived_on": "2018-10-31T11:32:38.390000",
      "asset": {
        "asset_type": {
          "deleted": "0",
          "id": "1",
          "is_default": "0",
          "location_id": "1",
          "name": "John C. Doe",
          "quantity": "0",
          "require_numbers": "0",
          "weight": "0"
        },
        "asset_type_id": "1",
        "cluster": "1",
        "customer_id": "1",
        "description": "Some description.",
        "dispatched_on": "2018-10-31T11:32:38.390000",
        "id": "1",
        "is_returned": "0",
        "last_activity_on": "2018-10-31T11:32:38.390000",
        "last_rental_invoice_on": "2018-10-31T11:32:38.390000",
        "latitude": "-90",
        "location": {
          "id": "1",
          "is_active": "0",
          "name": "John C. Doe"
        },
        "location_id": "1",
        "longitude": "-180",
        "number": "+1 (360) 733-1649",
        "quantity": "0",
        "returned_on": "2018-10-31T11:32:38.390000"
      },
      "asset_dropped": "0",
      "asset_id": "1",
      "asset_quantity": "0",
      "asset_type": {
        "deleted": "0",
        "id": "1",
        "is_default": "0",
        "location_id": "1",
        "name": "John C. Doe",
        "quantity": "0",
        "require_numbers": "0",
        "weight": "0"
      },
      "asset_type_id": "1",
      "completed_by": "1",
      "completed_by_driver": "0",
      "completed_on": "2018-10-31T11:32:38.390000",
      "confirmed_on": "2018-10-31T11:32:38.390000",
      "created_by_id": "1",
      "customer": {
        "addresses": [
          {
            "country": "US",
            "is_billing": "0",
            "is_shipping": "0",
            "latitude": "-90",
            "line_1": "321 Chase Rd",
            "line_2": "P.O. Box 256",
            "line_3": "3rd Floor",
            "line_4": "Last door on the left (blue)",
            "locality": "Sequim",
            "longitude": "-180",
            "postcode": "98368",
            "region": "WA"
          }
        ],
        "contacts": [
          {
            "email": "support@crosoftware.net",
            "fax": "+1 (360) 733-1649",
            "name": "John C. Doe",
            "notify_on_acknowledged_request": "0",
            "notify_on_completed_request": "0",
            "notify_on_dispatched_request": "0",
            "notify_on_failed_request": "0",
            "notify_on_new_request": "0",
            "number": "+1 (360) 733-1649"
          }
        ],
        "customer_id": "1",
        "is_commercial": "0",
        "name": "John C. Doe",
        "note": "Bin located in alley.",
        "parent_id": "1",
        "reference_number": "REF#100A61",
        "renewal_date": "2018-10-31T11:32:38.390000",
        "sales_rep": "John C. Doe",
        "suspension_id": "1"
      },
      "customer_id": "1",
      "customer_notes": "Some notes from a customer to a dispatcher.",
      "desired_asset_desc": "Some asset characteristics.",
      "dispatch_priority": "H",
      "dispatched_by_route": "1",
      "dispatched_on": "2018-10-31T11:32:38.390000",
      "dispatcher_notes": "Some dispatcher notes.",
      "do_confirm": "0",
      "driver_notes": "Some driver notes.",
      "dump_location": {
        "id": "1",
        "is_active": "0",
        "name": "John C. Doe"
      },
      "dump_location_id": "1",
      "dumped_on": "2018-10-31T11:32:38.390000",
      "end_time": "2018-10-31T11:32:38.390000",
      "fail_reason": "A reason for failure.",
      "final_location": {
        "id": "1",
        "is_active": "0",
        "name": "John C. Doe"
      },
      "final_location_id": "1",
      "flags": "A reason for failure.",
      "invoice_notes": "Some invoice notes.",
      "is_completed": "0",
      "is_declined": "0",
      "is_deleted": "0",
      "is_failed": "0",
      "job_group_id": "1",
      "location_id": "1",
      "merged_with_route": "1",
      "original_schedule_date": "2018-10-31T11:32:38.390000",
      "pickup_date": "2018-10-31T11:32:38.390000",
      "priority": "-999999",
      "reference_number": "REF#100A61",
      "requested_on": "2018-10-31T11:32:38.390000",
      "require_image": "0",
      "require_material": "0",
      "require_signature": "0",
      "require_weights": "0",
      "schedule_date": "2018-10-31T11:32:38.390000",
      "start_location": {
        "id": "1",
        "is_active": "0",
        "name": "John C. Doe"
      },
      "start_location_id": "1",
      "start_time": "2018-10-31T11:32:38.390000",
      "third_party_hauler_id": "defbc66e-f908-40d9-9ee5-655a1f699311",
      "times_failed": "0",
      "times_rolled_over": "0",
      "truck_id": "1",
      "type": "R",
      "weighed_on": "2018-10-31T11:32:38.390000"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[JobListModel](#schemajoblistmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

## Locations

### Get Location

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/locations/{location_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id} \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}");
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

`GET /locations/{location_id}`

<a id="opIdget_locations_by_id"></a>

Get location by id.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`location_id`|path|integer(int64)|true||

> Example responses

> 200 Response

```json
{
  "id": "1",
  "is_active": "0",
  "name": "John C. Doe"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[LocationModel](#schemalocationmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### List Locations

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/locations";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/locations',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/locations', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations");
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

`GET /locations`

<a id="opIdget_locations"></a>

List locations for this user.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`page_limit`|query|integer(int64)|false||
|`page_index`|query|integer(int64)|false||

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "id": "1",
      "is_active": "0",
      "name": "John C. Doe"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[LocationListModel](#schemalocationlistmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

## Tenants

### List Tenants

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/tenants";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/tenants \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/tenants',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/tenants',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/tenants', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/tenants");
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

`GET /tenants`

<a id="opIdget_tenants"></a>

List tenants for this user.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`page_limit`|query|integer(int64)|false||
|`page_index`|query|integer(int64)|false||

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "address": "321 Chase Rd",
      "city": "Sequim",
      "code": "CROSCRAPCO",
      "created_on": "2018-10-31T11:32:38.390000",
      "email": "support@crosoftware.net",
      "id": "1",
      "is_active": "0",
      "name": "John C. Doe",
      "phone": "+1 (360) 733-1649",
      "state": "WA",
      "truck_limit": "0",
      "zip": "98368"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TenantListModel](#schematenantlistmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

## Trucks

### Get Truck

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id} \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}");
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

`GET /locations/{location_id}/trucks/{truck_id}`

<a id="opIdget_locations_by_id_trucks_by_id"></a>

Get truck.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`location_id`|path|integer(int64)|true||
|`truck_id`|path|integer(int64)|true||

> Example responses

> 200 Response

```json
{
  "driver_id": "1",
  "id": "1",
  "location_id": "1",
  "name": "John C. Doe",
  "notes": "Bin located in alley.",
  "out_of_service": "0",
  "require_odometer": "0",
  "third_party_hauler_id": "defbc66e-f908-40d9-9ee5-655a1f699311",
  "type": "R59",
  "weight": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|string|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### List Trucks

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/locations/{location_id}/trucks";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id}/trucks \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/trucks',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}/trucks',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}/trucks', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/trucks");
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

`GET /locations/{location_id}/trucks`

<a id="opIdget_locations_by_id_trucks"></a>

List trucks.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`location_id`|path|integer(int64)|true||
|`page_limit`|query|integer(int64)|false||
|`page_index`|query|integer(int64)|false||

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "driver_id": "1",
      "id": "1",
      "location_id": "1",
      "name": "John C. Doe",
      "notes": "Bin located in alley.",
      "out_of_service": "0",
      "require_odometer": "0",
      "third_party_hauler_id": "defbc66e-f908-40d9-9ee5-655a1f699311",
      "type": "R59",
      "weight": "0"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TruckListModel](#schematrucklistmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Set Truck Driver

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadValues(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id} \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}',
  method: 'patch',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.patch('https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}");
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

`PATCH /locations/{location_id}/trucks/{truck_id}`

<a id="opIdpatch_locations_by_id_trucks_by_id"></a>

Set driver for truck.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`location_id`|path|integer(int64)|true||
|`truck_id`|path|integer(int64)|true||
|`driver_id`|query|boolean|false||

> Example responses

> 200 Response

```json
{
  "driver_id": "1",
  "id": "1",
  "location_id": "1",
  "name": "John C. Doe",
  "notes": "Bin located in alley.",
  "out_of_service": "0",
  "require_odometer": "0",
  "third_party_hauler_id": "defbc66e-f908-40d9-9ee5-655a1f699311",
  "type": "R59",
  "weight": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TruckModel](#schematruckmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

## Webhooks

### Create Hook

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/hooks";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadValues(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/hooks \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/hooks',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/hooks',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.post('https://api.crosoftware.net/hooks', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/hooks");
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

`POST /hooks`

<a id="opIdpost_hooks"></a>

Create new webhook.

> Body parameter

```json
{
  "events": [
    "customer"
  ],
  "url": "http://your.callback.url.net"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`body`|body|[CreateWebhookModel](#schemacreatewebhookmodel)|true||

> Example responses

> 200 Response

```json
{
  "events": [
    "customer"
  ],
  "url": "http://your.callback.url.net"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CreateWebhookModel](#schemacreatewebhookmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Delete Hook

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/hooks/{hook_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadValues(url, "DELETE", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X DELETE https://api.crosoftware.net/hooks/{hook_id} \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/hooks/{hook_id}',
  method: 'delete',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.delete 'https://api.crosoftware.net/hooks/{hook_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.delete('https://api.crosoftware.net/hooks/{hook_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/hooks/{hook_id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
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

`DELETE /hooks/{hook_id}`

<a id="opIddelete_hooks_by_id"></a>

Deactivate (soft delete) webhook by id.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`hook_id`|path|integer(int64)|true||

> Example responses

> 200 Response

```json
{
  "events": [
    "customer"
  ],
  "id": "1",
  "url": "http://your.callback.url.net"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[WebhookModel](#schemawebhookmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Get Hook

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/hooks/{hook_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/hooks/{hook_id} \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/hooks/{hook_id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/hooks/{hook_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/hooks/{hook_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/hooks/{hook_id}");
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

`GET /hooks/{hook_id}`

<a id="opIdget_hooks_by_id"></a>

Get webhook by id.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`hook_id`|path|integer(int64)|true||

> Example responses

> 200 Response

```json
{
  "events": [
    "customer"
  ],
  "id": "1",
  "url": "http://your.callback.url.net"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[WebhookModel](#schemawebhookmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### List Hooks

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/hooks";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/hooks \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/hooks',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/hooks',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/hooks', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/hooks");
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

`GET /hooks`

<a id="opIdget_hooks"></a>

List webhooks.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`deleted`|query|boolean|false||
|`page_limit`|query|integer(int64)|false||
|`page_index`|query|integer(int64)|false||

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "events": [
        "customer"
      ],
      "id": "1",
      "url": "http://your.callback.url.net"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[WebhookListModel](#schemawebhooklistmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

### Update Hook

> Code samples

```csharp
using System;
using System.Net;
using System.Collections.Specialized;

namespace CROSoftware
{
  public class DemoClient
  {
      static public void Main ()
      {
          WebClient client = new WebClient();

          // URL    
          String url = "https://api.crosoftware.net/hooks/{hook_id}";

          // Headers
          client.Headers.Add("authorization", "[object Object]");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadValues(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/hooks/{hook_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: [object Object]' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/hooks/{hook_id}',
  method: 'patch',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'authorization' => {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/hooks/{hook_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': {
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
},
  'x-tenant-id': '1'
}

r = requests.patch('https://api.crosoftware.net/hooks/{hook_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/hooks/{hook_id}");
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

`PATCH /hooks/{hook_id}`

<a id="opIdpatch_hooks_by_id"></a>

Update webhook.

> Body parameter

```json
{
  "events": [
    "customer"
  ],
  "url": "http://your.callback.url.net"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|[AuthorizationHeaderModel](#schemaauthorizationheadermodel)|true||
|`x-tenant-id`|header|integer(int64)|true||
|`hook_id`|path|integer(int64)|true||
|`body`|body|[UpdateWebhookModel](#schemaupdatewebhookmodel)|true||

> Example responses

> 200 Response

```json
{
  "events": [
    "customer"
  ],
  "url": "http://your.callback.url.net"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[UpdateWebhookModel](#schemaupdatewebhookmodel)|OK.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|401 Unauthorized.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|403 Forbidden.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|x-request-id|string||Request identifier.
|
|401|x-request-id|string||Request identifier.
|
|403|x-request-id|string||Request identifier.
|

# Schemas

<h2 id="tocSassetmodel">AssetModel</h2>

```json
{
  "asset_type": {
    "deleted": "0",
    "id": "1",
    "is_default": "0",
    "location_id": "1",
    "name": "John C. Doe",
    "quantity": "0",
    "require_numbers": "0",
    "weight": "0"
  },
  "asset_type_id": "1",
  "cluster": "1",
  "customer_id": "1",
  "description": "Some description.",
  "dispatched_on": "2018-10-31T11:32:38.390000",
  "id": "1",
  "is_returned": "0",
  "last_activity_on": "2018-10-31T11:32:38.390000",
  "last_rental_invoice_on": "2018-10-31T11:32:38.390000",
  "latitude": "-90",
  "location": {
    "id": "1",
    "is_active": "0",
    "name": "John C. Doe"
  },
  "location_id": "1",
  "longitude": "-180",
  "number": "+1 (360) 733-1649",
  "quantity": "0",
  "returned_on": "2018-10-31T11:32:38.390000"
}

```

<a id="schemaassetmodel"></a>

|Name|Type|Description|
|---|---|---|
|`asset_type`|[AssetTypeModel](#schemaassettypemodel)|-|
|`asset_type_id`|integer(int64)|Selected asset for the job (job types 'D', 'L', 'E'). Must be valid resource identifier (integer).|
|`cluster`|integer(int64)|Cluster id. Must be valid resource identifier (integer).|
|`customer_id`|integer(int64)|Customer identifier. Must be valid resource identifier (integer).|
|`description`|string|Free-form text description. Must be at least 1 and no more than 2048 characters.|
|`dispatched_on`|string(DateTime)|Time the asset was dispatched. Must be a date in an ISO 8601 compatible format.|
|`id`|integer(int64)|Resource identifier (integer) Must be valid resource identifier (integer).|
|`is_returned`|boolean|Is asset returned. Must be one of [0, 1, True, False] (case insensitive).|
|`last_activity_on`|string(DateTime)|Last activity time. Must be a date in an ISO 8601 compatible format.|
|`last_rental_invoice_on`|string(DateTime)|Last rental invoice time. Must be a date in an ISO 8601 compatible format.|
|`latitude`|number(float)|Latitude. Must be float greater than or equal to -90. Must be float less than or equal to 90.|
|`location`|[LocationModel](#schemalocationmodel)|-|
|`location_id`|integer(int64)|Location identifier (integer) Must be valid resource identifier (integer).|
|`longitude`|number(float)|longitude. Must be float greater than or equal to -180. Must be float less than or equal to 180.|
|`number`|string(PhoneNumber)|Phone number (free text). At least 7 characters, not more than 15.|
|`quantity`|integer(int64)|Asset quantity. Must be integer greater than or equal to 0.|
|`returned_on`|string(DateTime)|Time the asset was returned. Must be a date in an ISO 8601 compatible format.|

<h2 id="tocSassettypemodel">AssetTypeModel</h2>

```json
{
  "deleted": "0",
  "id": "1",
  "is_default": "0",
  "location_id": "1",
  "name": "John C. Doe",
  "quantity": "0",
  "require_numbers": "0",
  "weight": "0"
}

```

<a id="schemaassettypemodel"></a>

|Name|Type|Description|
|---|---|---|
|`deleted`|boolean|Is record deleted (soft delete). Must be one of [0, 1, True, False] (case insensitive).|
|`id`|integer(int64)|Resource identifier (integer) Must be valid resource identifier (integer).|
|`is_default`|boolean|Is asset the default asset. Must be one of [0, 1, True, False] (case insensitive).|
|`location_id`|integer(int64)|Location identifier (integer) Must be valid resource identifier (integer).|
|`name`|string|Name (free text). Must be at least 1 and no more than 64 characters.|
|`quantity`|integer(int64)|Asset type quantity. Must be integer greater than or equal to 0.|
|`require_numbers`|boolean|Require asset numbers. Must be one of [0, 1, True, False] (case insensitive).|
|`weight`|number(float)|Must be integer greater than or equal to 0.|

<h2 id="tocSauthorizationheadermodel">AuthorizationHeaderModel</h2>

```json
{
  "authtype": "bearer",
  "params": "asdf1234.asdf+1234.asdf"
}

```

<a id="schemaauthorizationheadermodel"></a>

|Name|Type|Description|
|---|---|---|
|`authtype`|string|Athorization bearer. Must match expression ^bearer$|
|`params`|string|Athorization access token. Must be no longer than 255 characters. Must match expression ^[a-z0-9_\-\.+\/~\=]{16,255}$|

<h2 id="tocScreatecustomeraddressmodel">CreateCustomerAddressModel</h2>

```json
{
  "country": "US",
  "is_billing": "0",
  "is_shipping": "0",
  "latitude": "-90",
  "line_1": "321 Chase Rd",
  "line_2": "P.O. Box 256",
  "line_3": "3rd Floor",
  "line_4": "Last door on the left (blue)",
  "locality": "Sequim",
  "longitude": "-180",
  "postcode": "98368",
  "region": "WA"
}

```

<a id="schemacreatecustomeraddressmodel"></a>

|Name|Type|Description|
|---|---|---|
|`country`|string|Country code (ISO 3166-1 alpha 2). Must be a 2 character country code.|
|`is_billing`|boolean|If true, this is the customer's billing address. Must be one of [0, 1, True, False] (case insensitive).|
|`is_shipping`|boolean|Customer's shipping address if true. Must be one of [0, 1, True, False] (case insensitive).|
|`latitude`|number(float)|Latitude. Must be float greater than or equal to -90. Must be float less than or equal to 90.|
|`line_1`|string|Street address. Must be at least 1 and no more than 256 characters.|
|`line_2`|string|Street address line 2. Must be at least 1 and no more than 256 characters.|
|`line_3`|string|Street address line 3. Must be at least 1 and no more than 256 characters.|
|`line_4`|string|Street address line 4 (doubles as county). Must be at least 1 and no more than 256 characters.|
|`locality`|string|Address locality (e.g. city). Must be at least 1 and no more than 86 characters.|
|`longitude`|number(float)|longitude. Must be float greater than or equal to -180. Must be float less than or equal to 180.|
|`postcode`|string|Postal code (may include letters and symbols). Must be at least 1 and no more than 86 characters.|
|`region`|string|Address region (e.g. state). Must be at least 1 and no more than 32 characters.|

<h2 id="tocScreatecustomercontactmodel">CreateCustomerContactModel</h2>

```json
{
  "email": "support@crosoftware.net",
  "fax": "+1 (360) 733-1649",
  "name": "John C. Doe",
  "notify_on_acknowledged_request": "0",
  "notify_on_completed_request": "0",
  "notify_on_dispatched_request": "0",
  "notify_on_failed_request": "0",
  "notify_on_new_request": "0",
  "number": "+1 (360) 733-1649"
}

```

<a id="schemacreatecustomercontactmodel"></a>

|Name|Type|Description|
|---|---|---|
|`email`|string(Email)|Email address. Must be a valid email address.|
|`fax`|string(PhoneNumber)|Fax number (free text). At least 7 characters, not more than 15.|
|`name`|string|Name (free text). Must be at least 1 and no more than 64 characters.|
|`notify_on_acknowledged_request`|boolean|Notify on acknowledge request. Must be one of [0, 1, True, False] (case insensitive).|
|`notify_on_completed_request`|boolean|Notify on completed request. Must be one of [0, 1, True, False] (case insensitive).|
|`notify_on_dispatched_request`|boolean|Notify on dispatched request. Must be one of [0, 1, True, False] (case insensitive).|
|`notify_on_failed_request`|boolean|Notify on failed request. Must be one of [0, 1, True, False] (case insensitive).|
|`notify_on_new_request`|boolean|Notify on new request. Must be one of [0, 1, True, False] (case insensitive).|
|`number`|string(PhoneNumber)|Phone number (free text). At least 7 characters, not more than 15.|

<h2 id="tocScreatecustomerlocationmodel">CreateCustomerLocationModel</h2>

```json
{
  "is_commercial": "0",
  "note": "Bin located in alley.",
  "reference_number": "REF#100A61",
  "renewal_date": "2018-10-31T11:32:38.390000",
  "sales_rep": "John C. Doe",
  "suspension_id": "1"
}

```

<a id="schemacreatecustomerlocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`is_commercial`|boolean|Commercial address if true, private if false. Must be one of [0, 1, True, False] (case insensitive).|
|`note`|string|Notes (free text). Must be at least 1 and no more than 2048 characters.|
|`reference_number`|string|Reference number (free text). Must be at least 1 and no more than 256 characters.|
|`renewal_date`|string(DateTime)|Renewal date. Must be a date in an ISO 8601 compatible format.|
|`sales_rep`|string|Name of sales representative. Must be at least 1 and no more than 64 characters.|
|`suspension_id`|integer(int64)|Suspension identifier. Must be valid resource identifier (integer).|

<h2 id="tocScreatecustomermodel">CreateCustomerModel</h2>

```json
{
  "addresses": [
    {
      "country": "US",
      "is_billing": "0",
      "is_shipping": "0",
      "latitude": "-90",
      "line_1": "321 Chase Rd",
      "line_2": "P.O. Box 256",
      "line_3": "3rd Floor",
      "line_4": "Last door on the left (blue)",
      "locality": "Sequim",
      "longitude": "-180",
      "postcode": "98368",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "email": "support@crosoftware.net",
      "fax": "+1 (360) 733-1649",
      "name": "John C. Doe",
      "notify_on_acknowledged_request": "0",
      "notify_on_completed_request": "0",
      "notify_on_dispatched_request": "0",
      "notify_on_failed_request": "0",
      "notify_on_new_request": "0",
      "number": "+1 (360) 733-1649"
    }
  ],
  "is_commercial": "0",
  "name": "John C. Doe",
  "note": "Bin located in alley.",
  "parent_id": "1",
  "reference_number": "REF#100A61",
  "renewal_date": "2018-10-31T11:32:38.390000",
  "sales_rep": "John C. Doe",
  "suspension_id": "1"
}

```

<a id="schemacreatecustomermodel"></a>

|Name|Type|Description|
|---|---|---|
|`addresses`|array[[CreateCustomerAddressModel](#schemacreatecustomeraddressmodel)]|-|
|`contacts`|array[[CreateCustomerContactModel](#schemacreatecustomercontactmodel)]|-|
|`is_commercial`|boolean|Commercial address if true, private if false. Must be one of [0, 1, True, False] (case insensitive).|
|`name`|string|Name (free text). Must be at least 1 and no more than 64 characters.|
|`note`|string|Notes (free text). Must be at least 1 and no more than 2048 characters.|
|`parent_id`|integer(int64)|Parent record identifier (integer) Must be valid resource identifier (integer).|
|`reference_number`|string|Reference number (free text). Must be at least 1 and no more than 256 characters.|
|`renewal_date`|string(DateTime)|Renewal date. Must be a date in an ISO 8601 compatible format.|
|`sales_rep`|string|Name of sales representative. Must be at least 1 and no more than 64 characters.|
|`suspension_id`|integer(int64)|Suspension identifier. Must be valid resource identifier (integer).|

<h2 id="tocScreatewebhookmodel">CreateWebhookModel</h2>

```json
{
  "events": [
    "customer"
  ],
  "url": "http://your.callback.url.net"
}

```

<a id="schemacreatewebhookmodel"></a>

|Name|Type|Description|
|---|---|---|
|`events`|array[string]|Hook event. Must be a valid hook event (one of: customer, job).|
|`url`|string(Url)|Callback URL. URL conforming to RFC 1738.|

<h2 id="tocScustomeraddresslistmodel">CustomerAddressListModel</h2>

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "address_id": "1",
      "country": "US",
      "is_billing": "0",
      "is_physical": "0",
      "is_shipping": "0",
      "latitude": "-90",
      "line_1": "321 Chase Rd",
      "line_2": "P.O. Box 256",
      "line_3": "3rd Floor",
      "line_4": "Last door on the left (blue)",
      "locality": "Sequim",
      "longitude": "-180",
      "postcode": "98368",
      "region": "WA"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}

```

<a id="schemacustomeraddresslistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page. Must be integer greater than or equal to 1. Must be integer less than or equal to 1000.|
|`current_page`|integer(int64)|Paged results page index (starting from 1). Must be integer greater than or equal to 1. Must be integer less than or equal to 10000.|
|`results`|array[[CustomerAddressModel](#schemacustomeraddressmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records. Must be integer greater than or equal to 0. Must be integer less than or equal to 100000.|
|`total_pages`|integer(int64)|Paged results total pages. Must be integer greater than or equal to 0. Must be integer less than or equal to 1000.|

<h2 id="tocScustomeraddressmodel">CustomerAddressModel</h2>

```json
{
  "address_id": "1",
  "country": "US",
  "is_billing": "0",
  "is_physical": "0",
  "is_shipping": "0",
  "latitude": "-90",
  "line_1": "321 Chase Rd",
  "line_2": "P.O. Box 256",
  "line_3": "3rd Floor",
  "line_4": "Last door on the left (blue)",
  "locality": "Sequim",
  "longitude": "-180",
  "postcode": "98368",
  "region": "WA"
}

```

<a id="schemacustomeraddressmodel"></a>

|Name|Type|Description|
|---|---|---|
|`address_id`|integer(int64)|Customer address identifier. Must be valid resource identifier (integer).|
|`country`|string|Country code (ISO 3166-1 alpha 2). Must be a 2 character country code.|
|`is_billing`|boolean|If true, this is the customer's billing address. Must be one of [0, 1, True, False] (case insensitive).|
|`is_physical`|boolean|Physical address if true. Must be one of [0, 1, True, False] (case insensitive).|
|`is_shipping`|boolean|Customer's shipping address if true. Must be one of [0, 1, True, False] (case insensitive).|
|`latitude`|number(float)|Latitude. Must be float greater than or equal to -90. Must be float less than or equal to 90.|
|`line_1`|string|Street address. Must be at least 1 and no more than 256 characters.|
|`line_2`|string|Street address line 2. Must be at least 1 and no more than 256 characters.|
|`line_3`|string|Street address line 3. Must be at least 1 and no more than 256 characters.|
|`line_4`|string|Street address line 4 (doubles as county). Must be at least 1 and no more than 256 characters.|
|`locality`|string|Address locality (e.g. city). Must be at least 1 and no more than 86 characters.|
|`longitude`|number(float)|longitude. Must be float greater than or equal to -180. Must be float less than or equal to 180.|
|`postcode`|string|Postal code (may include letters and symbols). Must be at least 1 and no more than 86 characters.|
|`region`|string|Address region (e.g. state). Must be at least 1 and no more than 32 characters.|

<h2 id="tocScustomercontactlistmodel">CustomerContactListModel</h2>

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "contact_id": "1",
      "email": "support@crosoftware.net",
      "fax": "+1 (360) 733-1649",
      "name": "John C. Doe",
      "notify_on_acknowledged_request": "0",
      "notify_on_completed_request": "0",
      "notify_on_dispatched_request": "0",
      "notify_on_failed_request": "0",
      "notify_on_new_request": "0",
      "number": "+1 (360) 733-1649"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}

```

<a id="schemacustomercontactlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page. Must be integer greater than or equal to 1. Must be integer less than or equal to 1000.|
|`current_page`|integer(int64)|Paged results page index (starting from 1). Must be integer greater than or equal to 1. Must be integer less than or equal to 10000.|
|`results`|array[[CustomerContactModel](#schemacustomercontactmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records. Must be integer greater than or equal to 0. Must be integer less than or equal to 100000.|
|`total_pages`|integer(int64)|Paged results total pages. Must be integer greater than or equal to 0. Must be integer less than or equal to 1000.|

<h2 id="tocScustomercontactmodel">CustomerContactModel</h2>

```json
{
  "contact_id": "1",
  "email": "support@crosoftware.net",
  "fax": "+1 (360) 733-1649",
  "name": "John C. Doe",
  "notify_on_acknowledged_request": "0",
  "notify_on_completed_request": "0",
  "notify_on_dispatched_request": "0",
  "notify_on_failed_request": "0",
  "notify_on_new_request": "0",
  "number": "+1 (360) 733-1649"
}

```

<a id="schemacustomercontactmodel"></a>

|Name|Type|Description|
|---|---|---|
|`contact_id`|integer(int64)|Customer contact identifier. Must be valid resource identifier (integer).|
|`email`|string(Email)|Email address. Must be a valid email address.|
|`fax`|string(PhoneNumber)|Fax number (free text). At least 7 characters, not more than 15.|
|`name`|string|Name (free text). Must be at least 1 and no more than 64 characters.|
|`notify_on_acknowledged_request`|boolean|Notify on acknowledge request. Must be one of [0, 1, True, False] (case insensitive).|
|`notify_on_completed_request`|boolean|Notify on completed request. Must be one of [0, 1, True, False] (case insensitive).|
|`notify_on_dispatched_request`|boolean|Notify on dispatched request. Must be one of [0, 1, True, False] (case insensitive).|
|`notify_on_failed_request`|boolean|Notify on failed request. Must be one of [0, 1, True, False] (case insensitive).|
|`notify_on_new_request`|boolean|Notify on new request. Must be one of [0, 1, True, False] (case insensitive).|
|`number`|string(PhoneNumber)|Phone number (free text). At least 7 characters, not more than 15.|

<h2 id="tocScustomerlistmodel">CustomerListModel</h2>

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "addresses": [
        {
          "country": "US",
          "is_billing": "0",
          "is_shipping": "0",
          "latitude": "-90",
          "line_1": "321 Chase Rd",
          "line_2": "P.O. Box 256",
          "line_3": "3rd Floor",
          "line_4": "Last door on the left (blue)",
          "locality": "Sequim",
          "longitude": "-180",
          "postcode": "98368",
          "region": "WA"
        }
      ],
      "contacts": [
        {
          "email": "support@crosoftware.net",
          "fax": "+1 (360) 733-1649",
          "name": "John C. Doe",
          "notify_on_acknowledged_request": "0",
          "notify_on_completed_request": "0",
          "notify_on_dispatched_request": "0",
          "notify_on_failed_request": "0",
          "notify_on_new_request": "0",
          "number": "+1 (360) 733-1649"
        }
      ],
      "customer_id": "1",
      "is_commercial": "0",
      "name": "John C. Doe",
      "note": "Bin located in alley.",
      "parent_id": "1",
      "reference_number": "REF#100A61",
      "renewal_date": "2018-10-31T11:32:38.390000",
      "sales_rep": "John C. Doe",
      "suspension_id": "1"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}

```

<a id="schemacustomerlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page. Must be integer greater than or equal to 1. Must be integer less than or equal to 1000.|
|`current_page`|integer(int64)|Paged results page index (starting from 1). Must be integer greater than or equal to 1. Must be integer less than or equal to 10000.|
|`results`|array[[CustomerModel](#schemacustomermodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records. Must be integer greater than or equal to 0. Must be integer less than or equal to 100000.|
|`total_pages`|integer(int64)|Paged results total pages. Must be integer greater than or equal to 0. Must be integer less than or equal to 1000.|

<h2 id="tocScustomerlocationlistmodel">CustomerLocationListModel</h2>

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "id": "1",
      "is_commercial": "0",
      "note": "Bin located in alley.",
      "reference_number": "REF#100A61",
      "renewal_date": "2018-10-31T11:32:38.390000",
      "sales_rep": "John C. Doe",
      "suspension_id": "1"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}

```

<a id="schemacustomerlocationlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page. Must be integer greater than or equal to 1. Must be integer less than or equal to 1000.|
|`current_page`|integer(int64)|Paged results page index (starting from 1). Must be integer greater than or equal to 1. Must be integer less than or equal to 10000.|
|`results`|array[[CustomerLocationModel](#schemacustomerlocationmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records. Must be integer greater than or equal to 0. Must be integer less than or equal to 100000.|
|`total_pages`|integer(int64)|Paged results total pages. Must be integer greater than or equal to 0. Must be integer less than or equal to 1000.|

<h2 id="tocScustomerlocationmodel">CustomerLocationModel</h2>

```json
{
  "id": "1",
  "is_commercial": "0",
  "note": "Bin located in alley.",
  "reference_number": "REF#100A61",
  "renewal_date": "2018-10-31T11:32:38.390000",
  "sales_rep": "John C. Doe",
  "suspension_id": "1"
}

```

<a id="schemacustomerlocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`id`|integer(int64)|Resource identifier (integer) Must be valid resource identifier (integer).|
|`is_commercial`|boolean|Commercial address if true, private if false. Must be one of [0, 1, True, False] (case insensitive).|
|`note`|string|Notes (free text). Must be at least 1 and no more than 2048 characters.|
|`reference_number`|string|Reference number (free text). Must be at least 1 and no more than 256 characters.|
|`renewal_date`|string(DateTime)|Renewal date. Must be a date in an ISO 8601 compatible format.|
|`sales_rep`|string|Name of sales representative. Must be at least 1 and no more than 64 characters.|
|`suspension_id`|integer(int64)|Suspension identifier. Must be valid resource identifier (integer).|

<h2 id="tocScustomermodel">CustomerModel</h2>

```json
{
  "addresses": [
    {
      "country": "US",
      "is_billing": "0",
      "is_shipping": "0",
      "latitude": "-90",
      "line_1": "321 Chase Rd",
      "line_2": "P.O. Box 256",
      "line_3": "3rd Floor",
      "line_4": "Last door on the left (blue)",
      "locality": "Sequim",
      "longitude": "-180",
      "postcode": "98368",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "email": "support@crosoftware.net",
      "fax": "+1 (360) 733-1649",
      "name": "John C. Doe",
      "notify_on_acknowledged_request": "0",
      "notify_on_completed_request": "0",
      "notify_on_dispatched_request": "0",
      "notify_on_failed_request": "0",
      "notify_on_new_request": "0",
      "number": "+1 (360) 733-1649"
    }
  ],
  "customer_id": "1",
  "is_commercial": "0",
  "name": "John C. Doe",
  "note": "Bin located in alley.",
  "parent_id": "1",
  "reference_number": "REF#100A61",
  "renewal_date": "2018-10-31T11:32:38.390000",
  "sales_rep": "John C. Doe",
  "suspension_id": "1"
}

```

<a id="schemacustomermodel"></a>

|Name|Type|Description|
|---|---|---|
|`addresses`|array[[CreateCustomerAddressModel](#schemacreatecustomeraddressmodel)]|-|
|`contacts`|array[[CreateCustomerContactModel](#schemacreatecustomercontactmodel)]|-|
|`customer_id`|integer(int64)|Customer identifier. Must be valid resource identifier (integer).|
|`is_commercial`|boolean|Commercial address if true, private if false. Must be one of [0, 1, True, False] (case insensitive).|
|`name`|string|Name (free text). Must be at least 1 and no more than 64 characters.|
|`note`|string|Notes (free text). Must be at least 1 and no more than 2048 characters.|
|`parent_id`|integer(int64)|Parent record identifier (integer) Must be valid resource identifier (integer).|
|`reference_number`|string|Reference number (free text). Must be at least 1 and no more than 256 characters.|
|`renewal_date`|string(DateTime)|Renewal date. Must be a date in an ISO 8601 compatible format.|
|`sales_rep`|string|Name of sales representative. Must be at least 1 and no more than 64 characters.|
|`suspension_id`|integer(int64)|Suspension identifier. Must be valid resource identifier (integer).|

<h2 id="tocSdriverlistmodel">DriverListModel</h2>

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "address": "321 Chase Rd",
      "can_convert_to_group": "0",
      "can_create_requests": "0",
      "can_edit_requests": "0",
      "can_reposition_asset": "0",
      "city": "Sequim",
      "disable_shift_tracking": "0",
      "email": "support@crosoftware.net",
      "id": "1",
      "license_number": "12ZA24WA-21",
      "location_id": "1",
      "name": "John C. Doe",
      "phone_number": "+1 (360) 733-1649",
      "state": "WA",
      "third_party_hauler_id": "defbc66e-f908-40d9-9ee5-655a1f699311",
      "zip": "98368"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}

```

<a id="schemadriverlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page. Must be integer greater than or equal to 1. Must be integer less than or equal to 1000.|
|`current_page`|integer(int64)|Paged results page index (starting from 1). Must be integer greater than or equal to 1. Must be integer less than or equal to 10000.|
|`results`|array[[DriverModel](#schemadrivermodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records. Must be integer greater than or equal to 0. Must be integer less than or equal to 100000.|
|`total_pages`|integer(int64)|Paged results total pages. Must be integer greater than or equal to 0. Must be integer less than or equal to 1000.|

<h2 id="tocSdrivermodel">DriverModel</h2>

```json
{
  "address": "321 Chase Rd",
  "can_convert_to_group": "0",
  "can_create_requests": "0",
  "can_edit_requests": "0",
  "can_reposition_asset": "0",
  "city": "Sequim",
  "disable_shift_tracking": "0",
  "email": "support@crosoftware.net",
  "id": "1",
  "license_number": "12ZA24WA-21",
  "location_id": "1",
  "name": "John C. Doe",
  "phone_number": "+1 (360) 733-1649",
  "state": "WA",
  "third_party_hauler_id": "defbc66e-f908-40d9-9ee5-655a1f699311",
  "zip": "98368"
}

```

<a id="schemadrivermodel"></a>

|Name|Type|Description|
|---|---|---|
|`address`|string|Street address. Must be at least 1 and no more than 256 characters.|
|`can_convert_to_group`|boolean|Can driver convert to group. Must be one of [0, 1, True, False] (case insensitive).|
|`can_create_requests`|boolean|Can driver create requests. Must be one of [0, 1, True, False] (case insensitive).|
|`can_edit_requests`|boolean|Can driver edit requests. Must be one of [0, 1, True, False] (case insensitive).|
|`can_reposition_asset`|boolean|Can driver reposition asset. Must be one of [0, 1, True, False] (case insensitive).|
|`city`|string|Address locality (e.g. city). Must be at least 1 and no more than 86 characters.|
|`disable_shift_tracking`|boolean|Disable shift tracking. Must be one of [0, 1, True, False] (case insensitive).|
|`email`|string(Email)|Email address. Must be a valid email address.|
|`id`|integer(int64)|Resource identifier (integer) Must be valid resource identifier (integer).|
|`license_number`|string|Driver's license number. Must be at least 1 and no more than 100 characters.|
|`location_id`|integer(int64)|Location identifier (integer) Must be valid resource identifier (integer).|
|`name`|string|Name (free text). Must be at least 1 and no more than 64 characters.|
|`phone_number`|string(PhoneNumber)|Phone number (free text). At least 7 characters, not more than 15.|
|`state`|string|Address region (e.g. state). Must be at least 1 and no more than 32 characters.|
|`third_party_hauler_id`|string(Uuid)|Third party hauler identifier. Must be a valid UUID.|
|`zip`|string|Postal code (may include letters and symbols). Must be at least 1 and no more than 86 characters.|

<h2 id="tocSerrorresponsemodel">ErrorResponseModel</h2>

```json
{
  "detail": "Something went wrong.",
  "explanation": "The server was unable to comply because something went wrong.",
  "title": "some_field_name"
}

```

<a id="schemaerrorresponsemodel"></a>

|Name|Type|Description|
|---|---|---|
|`detail`|string|Error message details. Must be a string.|
|`explanation`|string|Error message general explanation. Must be a string.|
|`title`|string|Error message data identifier. Must be a string.|

<h2 id="tocSgpseventcoordsprofilemodel">GpsEventCoordsProfileModel</h2>

```json
{
  "heading": "0",
  "latitude": "-90",
  "longitude": "-180",
  "speed": "0"
}

```

<a id="schemagpseventcoordsprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`heading`|number(float)|Direction of travel at time of measurement. Must be float greater than or equal to 0. Must be float less than 360.|
|`latitude`|number(float)|Latitude. Must be float greater than or equal to -90. Must be float less than or equal to 90.|
|`longitude`|number(float)|longitude. Must be float greater than or equal to -180. Must be float less than or equal to 180.|
|`speed`|number(float)|Rate of travel at time of measurement. Must be float greater than or equal to 0.|

<h2 id="tocSgpseventlocationprofilemodel">GpsEventLocationProfileModel</h2>

```json
{
  "coords": {
    "heading": "0",
    "latitude": "-90",
    "longitude": "-180",
    "speed": "0"
  },
  "timestamp": "2018-10-31T11:32:38.390000"
}

```

<a id="schemagpseventlocationprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`coords`|[GpsEventCoordsProfileModel](#schemagpseventcoordsprofilemodel)|-|
|`timestamp`|string(DateTime)|Timestamp of creation (must be in past). Must be a date occurring in the past in an ISO 8601 compatible format.|

<h2 id="tocSgpseventprofilemodel">GpsEventProfileModel</h2>

```json
{
  "location": {
    "coords": {
      "heading": "0",
      "latitude": "-90",
      "longitude": "-180",
      "speed": "0"
    },
    "timestamp": "2018-10-31T11:32:38.390000"
  }
}

```

<a id="schemagpseventprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`location`|[GpsEventLocationProfileModel](#schemagpseventlocationprofilemodel)|-|

<h2 id="tocSgpsstopmodel">GpsStopModel</h2>

```json
{
  "bearing": "0",
  "created_on": "2018-10-31T11:32:38.390000",
  "device_name": "John C. Doe",
  "driver_id": "1",
  "id": "1",
  "latitude": "-90",
  "longitude": "-180",
  "truck_id": "1",
  "velocity": "0"
}

```

<a id="schemagpsstopmodel"></a>

|Name|Type|Description|
|---|---|---|
|`bearing`|number(float)|Direction of travel at time of measurement. Must be float greater than or equal to 0. Must be float less than 360.|
|`created_on`|string(DateTime)|Timestamp of creation (must be in past). Must be a date occurring in the past in an ISO 8601 compatible format.|
|`device_name`|string|Name (free text). Must be at least 1 and no more than 64 characters.|
|`driver_id`|integer(int64)|Driver identifier. Must be valid resource identifier (integer).|
|`id`|integer(int64)|Resource identifier (integer) Must be valid resource identifier (integer).|
|`latitude`|number(float)|Latitude. Must be float greater than or equal to -90. Must be float less than or equal to 90.|
|`longitude`|number(float)|longitude. Must be float greater than or equal to -180. Must be float less than or equal to 180.|
|`truck_id`|integer(int64)|Truck identifier. Must be valid resource identifier (integer).|
|`velocity`|number(float)|Rate of travel at time of measurement. Must be float greater than or equal to 0.|

<h2 id="tocSjoblistmodel">JobListModel</h2>

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "arrived_at_dest": "2018-10-31T11:32:38.390000",
      "arrived_on": "2018-10-31T11:32:38.390000",
      "asset": {
        "asset_type": {
          "deleted": "0",
          "id": "1",
          "is_default": "0",
          "location_id": "1",
          "name": "John C. Doe",
          "quantity": "0",
          "require_numbers": "0",
          "weight": "0"
        },
        "asset_type_id": "1",
        "cluster": "1",
        "customer_id": "1",
        "description": "Some description.",
        "dispatched_on": "2018-10-31T11:32:38.390000",
        "id": "1",
        "is_returned": "0",
        "last_activity_on": "2018-10-31T11:32:38.390000",
        "last_rental_invoice_on": "2018-10-31T11:32:38.390000",
        "latitude": "-90",
        "location": {
          "id": "1",
          "is_active": "0",
          "name": "John C. Doe"
        },
        "location_id": "1",
        "longitude": "-180",
        "number": "+1 (360) 733-1649",
        "quantity": "0",
        "returned_on": "2018-10-31T11:32:38.390000"
      },
      "asset_dropped": "0",
      "asset_id": "1",
      "asset_quantity": "0",
      "asset_type": {
        "deleted": "0",
        "id": "1",
        "is_default": "0",
        "location_id": "1",
        "name": "John C. Doe",
        "quantity": "0",
        "require_numbers": "0",
        "weight": "0"
      },
      "asset_type_id": "1",
      "completed_by": "1",
      "completed_by_driver": "0",
      "completed_on": "2018-10-31T11:32:38.390000",
      "confirmed_on": "2018-10-31T11:32:38.390000",
      "created_by_id": "1",
      "customer": {
        "addresses": [
          {
            "country": "US",
            "is_billing": "0",
            "is_shipping": "0",
            "latitude": "-90",
            "line_1": "321 Chase Rd",
            "line_2": "P.O. Box 256",
            "line_3": "3rd Floor",
            "line_4": "Last door on the left (blue)",
            "locality": "Sequim",
            "longitude": "-180",
            "postcode": "98368",
            "region": "WA"
          }
        ],
        "contacts": [
          {
            "email": "support@crosoftware.net",
            "fax": "+1 (360) 733-1649",
            "name": "John C. Doe",
            "notify_on_acknowledged_request": "0",
            "notify_on_completed_request": "0",
            "notify_on_dispatched_request": "0",
            "notify_on_failed_request": "0",
            "notify_on_new_request": "0",
            "number": "+1 (360) 733-1649"
          }
        ],
        "customer_id": "1",
        "is_commercial": "0",
        "name": "John C. Doe",
        "note": "Bin located in alley.",
        "parent_id": "1",
        "reference_number": "REF#100A61",
        "renewal_date": "2018-10-31T11:32:38.390000",
        "sales_rep": "John C. Doe",
        "suspension_id": "1"
      },
      "customer_id": "1",
      "customer_notes": "Some notes from a customer to a dispatcher.",
      "desired_asset_desc": "Some asset characteristics.",
      "dispatch_priority": "H",
      "dispatched_by_route": "1",
      "dispatched_on": "2018-10-31T11:32:38.390000",
      "dispatcher_notes": "Some dispatcher notes.",
      "do_confirm": "0",
      "driver_notes": "Some driver notes.",
      "dump_location": {
        "id": "1",
        "is_active": "0",
        "name": "John C. Doe"
      },
      "dump_location_id": "1",
      "dumped_on": "2018-10-31T11:32:38.390000",
      "end_time": "2018-10-31T11:32:38.390000",
      "fail_reason": "A reason for failure.",
      "final_location": {
        "id": "1",
        "is_active": "0",
        "name": "John C. Doe"
      },
      "final_location_id": "1",
      "flags": "A reason for failure.",
      "invoice_notes": "Some invoice notes.",
      "is_completed": "0",
      "is_declined": "0",
      "is_deleted": "0",
      "is_failed": "0",
      "job_group_id": "1",
      "location_id": "1",
      "merged_with_route": "1",
      "original_schedule_date": "2018-10-31T11:32:38.390000",
      "pickup_date": "2018-10-31T11:32:38.390000",
      "priority": "-999999",
      "reference_number": "REF#100A61",
      "requested_on": "2018-10-31T11:32:38.390000",
      "require_image": "0",
      "require_material": "0",
      "require_signature": "0",
      "require_weights": "0",
      "schedule_date": "2018-10-31T11:32:38.390000",
      "start_location": {
        "id": "1",
        "is_active": "0",
        "name": "John C. Doe"
      },
      "start_location_id": "1",
      "start_time": "2018-10-31T11:32:38.390000",
      "third_party_hauler_id": "defbc66e-f908-40d9-9ee5-655a1f699311",
      "times_failed": "0",
      "times_rolled_over": "0",
      "truck_id": "1",
      "type": "R",
      "weighed_on": "2018-10-31T11:32:38.390000"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}

```

<a id="schemajoblistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page. Must be integer greater than or equal to 1. Must be integer less than or equal to 1000.|
|`current_page`|integer(int64)|Paged results page index (starting from 1). Must be integer greater than or equal to 1. Must be integer less than or equal to 10000.|
|`results`|array[[JobModel](#schemajobmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records. Must be integer greater than or equal to 0. Must be integer less than or equal to 100000.|
|`total_pages`|integer(int64)|Paged results total pages. Must be integer greater than or equal to 0. Must be integer less than or equal to 1000.|

<h2 id="tocSjobmodel">JobModel</h2>

```json
{
  "arrived_at_dest": "2018-10-31T11:32:38.390000",
  "arrived_on": "2018-10-31T11:32:38.390000",
  "asset": {
    "asset_type": {
      "deleted": "0",
      "id": "1",
      "is_default": "0",
      "location_id": "1",
      "name": "John C. Doe",
      "quantity": "0",
      "require_numbers": "0",
      "weight": "0"
    },
    "asset_type_id": "1",
    "cluster": "1",
    "customer_id": "1",
    "description": "Some description.",
    "dispatched_on": "2018-10-31T11:32:38.390000",
    "id": "1",
    "is_returned": "0",
    "last_activity_on": "2018-10-31T11:32:38.390000",
    "last_rental_invoice_on": "2018-10-31T11:32:38.390000",
    "latitude": "-90",
    "location": {
      "id": "1",
      "is_active": "0",
      "name": "John C. Doe"
    },
    "location_id": "1",
    "longitude": "-180",
    "number": "+1 (360) 733-1649",
    "quantity": "0",
    "returned_on": "2018-10-31T11:32:38.390000"
  },
  "asset_dropped": "0",
  "asset_id": "1",
  "asset_quantity": "0",
  "asset_type": {
    "deleted": "0",
    "id": "1",
    "is_default": "0",
    "location_id": "1",
    "name": "John C. Doe",
    "quantity": "0",
    "require_numbers": "0",
    "weight": "0"
  },
  "asset_type_id": "1",
  "completed_by": "1",
  "completed_by_driver": "0",
  "completed_on": "2018-10-31T11:32:38.390000",
  "confirmed_on": "2018-10-31T11:32:38.390000",
  "created_by_id": "1",
  "customer": {
    "addresses": [
      {
        "country": "US",
        "is_billing": "0",
        "is_shipping": "0",
        "latitude": "-90",
        "line_1": "321 Chase Rd",
        "line_2": "P.O. Box 256",
        "line_3": "3rd Floor",
        "line_4": "Last door on the left (blue)",
        "locality": "Sequim",
        "longitude": "-180",
        "postcode": "98368",
        "region": "WA"
      }
    ],
    "contacts": [
      {
        "email": "support@crosoftware.net",
        "fax": "+1 (360) 733-1649",
        "name": "John C. Doe",
        "notify_on_acknowledged_request": "0",
        "notify_on_completed_request": "0",
        "notify_on_dispatched_request": "0",
        "notify_on_failed_request": "0",
        "notify_on_new_request": "0",
        "number": "+1 (360) 733-1649"
      }
    ],
    "customer_id": "1",
    "is_commercial": "0",
    "name": "John C. Doe",
    "note": "Bin located in alley.",
    "parent_id": "1",
    "reference_number": "REF#100A61",
    "renewal_date": "2018-10-31T11:32:38.390000",
    "sales_rep": "John C. Doe",
    "suspension_id": "1"
  },
  "customer_id": "1",
  "customer_notes": "Some notes from a customer to a dispatcher.",
  "desired_asset_desc": "Some asset characteristics.",
  "dispatch_priority": "H",
  "dispatched_by_route": "1",
  "dispatched_on": "2018-10-31T11:32:38.390000",
  "dispatcher_notes": "Some dispatcher notes.",
  "do_confirm": "0",
  "driver_notes": "Some driver notes.",
  "dump_location": {
    "id": "1",
    "is_active": "0",
    "name": "John C. Doe"
  },
  "dump_location_id": "1",
  "dumped_on": "2018-10-31T11:32:38.390000",
  "end_time": "2018-10-31T11:32:38.390000",
  "fail_reason": "A reason for failure.",
  "final_location": {
    "id": "1",
    "is_active": "0",
    "name": "John C. Doe"
  },
  "final_location_id": "1",
  "flags": "A reason for failure.",
  "invoice_notes": "Some invoice notes.",
  "is_completed": "0",
  "is_declined": "0",
  "is_deleted": "0",
  "is_failed": "0",
  "job_group_id": "1",
  "location_id": "1",
  "merged_with_route": "1",
  "original_schedule_date": "2018-10-31T11:32:38.390000",
  "pickup_date": "2018-10-31T11:32:38.390000",
  "priority": "-999999",
  "reference_number": "REF#100A61",
  "requested_on": "2018-10-31T11:32:38.390000",
  "require_image": "0",
  "require_material": "0",
  "require_signature": "0",
  "require_weights": "0",
  "schedule_date": "2018-10-31T11:32:38.390000",
  "start_location": {
    "id": "1",
    "is_active": "0",
    "name": "John C. Doe"
  },
  "start_location_id": "1",
  "start_time": "2018-10-31T11:32:38.390000",
  "third_party_hauler_id": "defbc66e-f908-40d9-9ee5-655a1f699311",
  "times_failed": "0",
  "times_rolled_over": "0",
  "truck_id": "1",
  "type": "R",
  "weighed_on": "2018-10-31T11:32:38.390000"
}

```

<a id="schemajobmodel"></a>

|Name|Type|Description|
|---|---|---|
|`arrived_at_dest`|string(DateTime)|Entered by driver for dispatcher and customer. Asset arrival at destination time. Only applicable for jobs with a valid dump destination. Must be a date in an ISO 8601 compatible format.|
|`arrived_on`|string(DateTime)|Drive start time entered by driver for dispatcher and customer (arrived at job slider). Must be a date in an ISO 8601 compatible format.|
|`asset`|[AssetModel](#schemaassetmodel)|-|
|`asset_dropped`|integer(int64)|Reference to deployed asset entered by driver for customer, dispatcher applicable to job types  'D', 'E'. Must be integer greater than or equal to 0. Must be integer less than or equal to 10000.|
|`asset_id`|integer(int64)|Job asset identifier. Applicable to job types 'E', 'P', 'R'. Must be valid resource identifier (integer).|
|`asset_quantity`|integer(int64)|How many assets are being serviced within a cluster (for jobs assigned to an asset cluster). For jobs dispatched by routes, or manually dispatched route stops, this value is 0 or 1. Must be integer greater than or equal to 0.|
|`asset_type`|[AssetTypeModel](#schemaassettypemodel)|-|
|`asset_type_id`|integer(int64)|Selected asset for the job (job types 'D', 'L', 'E'). Must be valid resource identifier (integer).|
|`completed_by`|integer(int64)|Dispatcher or driver id. Must be valid resource identifier (integer).|
|`completed_by_driver`|boolean|If TRUE, completed by driver. If FALSE, completed by dispatcher. Must be one of [0, 1, True, False] (case insensitive).|
|`completed_on`|string(DateTime)|Job completion time. Must be a date occurring in the past in an ISO 8601 compatible format.|
|`confirmed_on`|string(DateTime)|Job confirmation date. Must be a date occurring in the past in an ISO 8601 compatible format.|
|`created_by_id`|integer(int64)|Customer, dispatcher, or driver id. Must be valid resource identifier (integer).|
|`customer`|[CustomerModel](#schemacustomermodel)|-|
|`customer_id`|integer(int64)|Customer identifier. Must be valid resource identifier (integer).|
|`customer_notes`|string|Notes entered by customers to communicate with dispatchers. Must be at least 0 and no more than 2048 characters.|
|`desired_asset_desc`|string|Free-form text entered by dispatchers and drivers to be used as the future asset description. Must be at least 1 and no more than 2048 characters.|
|`dispatch_priority`|string|Entered by dispatchers to determine dispatch order. Must be one of: 'H', 'M', 'L' (where 'H'='High', 'M'='Medium', 'L'='Low').|
|`dispatched_by_route`|integer(int64)|Route id of dispatching route (or NULL if not dispatched by a route). Must be valid resource identifier (integer).|
|`dispatched_on`|string(DateTime)|Time the job is assigned to a truck. Must be a date in an ISO 8601 compatible format.|
|`dispatcher_notes`|string|Entered by dispatchers, read by drivers and dispatchers. Must be at least 1 and no more than 2048 characters.|
|`do_confirm`|boolean|Tell dispatcher that a customer should be contacted before job is dispatched. Must be one of [0, 1, True, False] (case insensitive).|
|`driver_notes`|string|Entered by drivers when completing or failing a job for dispatchers. Must be at least 1 and no more than 2048 characters.|
|`dump_location`|[LocationModel](#schemalocationmodel)|-|
|`dump_location_id`|integer(int64)|Asset or asset cluster dump location identifier (e.g. trash bin needs dumped before returning from customer). Must be valid resource identifier (integer).|
|`dumped_on`|string(DateTime)|Dump request completion date. Must be a date in an ISO 8601 compatible format.|
|`end_time`|string(DateTime)|Future estimated time of job completion. Must be a date in an ISO 8601 compatible format.|
|`fail_reason`|string|Failure description selected by a driver for use by dispatchers. Must be at least 0 and no more than 64 characters.|
|`final_location`|[LocationModel](#schemalocationmodel)|-|
|`final_location_id`|integer(int64)|Final location identifier. Used by dispatchers for prioritizing jobs. Used by drivers to know where to leave the asset on job completion. Must be valid resource identifier (integer).|
|`flags`|string|Job notes. Must be at least 0 and no more than 64 characters.|
|`invoice_notes`|string|Invoice notes from the billing system. Must be at least 1 and no more than 2048 characters.|
|`is_completed`|boolean|Job completion flag set by dispatchers and drivers. Must be one of [0, 1, True, False] (case insensitive).|
|`is_declined`|boolean|Job completion flag set by dispatchers and drivers. Must be one of [0, 1, True, False] (case insensitive).|
|`is_deleted`|boolean|Indicates whether job is still valid. Must be one of [0, 1, True, False] (case insensitive).|
|`is_failed`|boolean|Set by drivers and dispatchers to indicate a failed job. Must be one of [0, 1, True, False] (case insensitive).|
|`job_group_id`|integer(int64)|Job group identifier for group jobs (vs service, exchange, etc.). Must be valid resource identifier (integer).|
|`location_id`|integer(int64)|Location identifier (integer) Must be valid resource identifier (integer).|
|`merged_with_route`|integer(int64)|Assigned by dispatchers for dispatchers and drivers. Must be valid resource identifier (integer).|
|`original_schedule_date`|string(DateTime)|Original scheduling date. Must be a date in an ISO 8601 compatible format.|
|`pickup_date`|string(DateTime)|A pickup job is scheduled for this date upon job completion. If the asset or cluster is assigned to a route stop, the route stop will be deleted. Must be in the future. Must be a date in an ISO 8601 compatible format.|
|`priority`|integer(int64)|Assigned by dispatchers for job order completion determination for drivers. Must be integer greater than or equal to -999999. Must be integer less than or equal to -1.|
|`reference_number`|string|Reference number (free text). Must be at least 1 and no more than 256 characters.|
|`requested_on`|string(DateTime)|Requested date. Must be a date occurring in the past in an ISO 8601 compatible format.|
|`require_image`|boolean|Set by dispatchers and drivers, requires drivers to upload one or more job images before completion. Must be one of [0, 1, True, False] (case insensitive).|
|`require_material`|boolean|Set by dispatchers and drivers, requires drivers to set a material before completing a job. Must be one of [0, 1, True, False] (case insensitive).|
|`require_signature`|boolean|Set by dispatchers and drivers, requires drivers to get a customer signature before job completion. Must be one of [0, 1, True, False] (case insensitive).|
|`require_weights`|boolean|Set by disptachers and drivers, requires drivers to set material weights before job completion. Must be one of [0, 1, True, False] (case insensitive).|
|`schedule_date`|string(DateTime)|Scheduled job completion date. Must be a date in an ISO 8601 compatible format.|
|`start_location`|[LocationModel](#schemalocationmodel)|-|
|`start_location_id`|integer(int64)|Pickup location for asset or asset cluster Set by dispatchers and drivers for drivers. Must be valid resource identifier (integer).|
|`start_time`|string(DateTime)|Time customer has requested job start, set by dispatchers for dispatchers and drivers. Must be a date in an ISO 8601 compatible format.|
|`third_party_hauler_id`|string(Uuid)|Third party hauler identifier. Must be a valid UUID.|
|`times_failed`|integer(int64)|Number of times a job has been attempted and failed. Must be integer greater than or equal to 0.|
|`times_rolled_over`|integer(int64)|Tracks job age in days for dispatchers. Must be integer greater than or equal to 0.|
|`truck_id`|integer(int64)|Truck identifier. Must be valid resource identifier (integer).|
|`type`|string|Set by dispatchers and customers. Represents physical actions to execute on job start. Must be one of: 'R', 'P', 'D', 'E', 'L'.|
|`weighed_on`|string(DateTime)|Time of truck weight entry. Must be a date occurring in the past in an ISO 8601 compatible format.|

<h2 id="tocSlocationlistmodel">LocationListModel</h2>

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "id": "1",
      "is_active": "0",
      "name": "John C. Doe"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}

```

<a id="schemalocationlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page. Must be integer greater than or equal to 1. Must be integer less than or equal to 1000.|
|`current_page`|integer(int64)|Paged results page index (starting from 1). Must be integer greater than or equal to 1. Must be integer less than or equal to 10000.|
|`results`|array[[LocationModel](#schemalocationmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records. Must be integer greater than or equal to 0. Must be integer less than or equal to 100000.|
|`total_pages`|integer(int64)|Paged results total pages. Must be integer greater than or equal to 0. Must be integer less than or equal to 1000.|

<h2 id="tocSlocationmodel">LocationModel</h2>

```json
{
  "id": "1",
  "is_active": "0",
  "name": "John C. Doe"
}

```

<a id="schemalocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`id`|integer(int64)|Location identifier (integer) Must be valid resource identifier (integer).|
|`is_active`|boolean|Records marked inactive are treated as deleted (soft delete). Must be one of [0, 1, True, False] (case insensitive).|
|`name`|string|Name (free text). Must be at least 1 and no more than 64 characters.|

<h2 id="tocStenantlistmodel">TenantListModel</h2>

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "address": "321 Chase Rd",
      "city": "Sequim",
      "code": "CROSCRAPCO",
      "created_on": "2018-10-31T11:32:38.390000",
      "email": "support@crosoftware.net",
      "id": "1",
      "is_active": "0",
      "name": "John C. Doe",
      "phone": "+1 (360) 733-1649",
      "state": "WA",
      "truck_limit": "0",
      "zip": "98368"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}

```

<a id="schematenantlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page. Must be integer greater than or equal to 1. Must be integer less than or equal to 1000.|
|`current_page`|integer(int64)|Paged results page index (starting from 1). Must be integer greater than or equal to 1. Must be integer less than or equal to 10000.|
|`results`|array[[TenantModel](#schematenantmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records. Must be integer greater than or equal to 0. Must be integer less than or equal to 100000.|
|`total_pages`|integer(int64)|Paged results total pages. Must be integer greater than or equal to 0. Must be integer less than or equal to 1000.|

<h2 id="tocStenantmodel">TenantModel</h2>

```json
{
  "address": "321 Chase Rd",
  "city": "Sequim",
  "code": "CROSCRAPCO",
  "created_on": "2018-10-31T11:32:38.390000",
  "email": "support@crosoftware.net",
  "id": "1",
  "is_active": "0",
  "name": "John C. Doe",
  "phone": "+1 (360) 733-1649",
  "state": "WA",
  "truck_limit": "0",
  "zip": "98368"
}

```

<a id="schematenantmodel"></a>

|Name|Type|Description|
|---|---|---|
|`address`|string|Street address. Must be at least 1 and no more than 256 characters.|
|`city`|string|Address locality (e.g. city). Must be at least 1 and no more than 86 characters.|
|`code`|string|Facility identifier. Must be at least 1 and no more than 64 characters.|
|`created_on`|string(DateTime)|Timestamp of creation (must be in past). Must be a date occurring in the past in an ISO 8601 compatible format.|
|`email`|string(Email)|Email address. Must be a valid email address.|
|`id`|integer(int64)|Resource identifier (integer) Must be valid resource identifier (integer).|
|`is_active`|boolean|Records marked inactive are treated as deleted (soft delete). Must be one of [0, 1, True, False] (case insensitive).|
|`name`|string|Name (free text). Must be at least 1 and no more than 64 characters.|
|`phone`|string(PhoneNumber)|Phone number (free text). At least 7 characters, not more than 15.|
|`state`|string|Address region (e.g. state). Must be at least 1 and no more than 32 characters.|
|`truck_limit`|integer(int64)|Maximum trucks configurable for tenant. Must be integer greater than or equal to 0.|
|`zip`|string|Postal code (may include letters and symbols). Must be at least 1 and no more than 86 characters.|

<h2 id="tocSthirdpartyhaulerconnectionlistmodel">ThirdPartyHaulerConnectionListModel</h2>

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": {
    "approved_by": "1",
    "approved_on": "2018-10-31T11:32:38.390000",
    "denied_on": "2018-10-31T11:32:38.390000",
    "is_approved": "0",
    "location_id": "1",
    "provider_email": "support@crosoftware.net",
    "provider_id": "1",
    "provider_name": "John C. Doe",
    "provider_phone": "+1 (360) 733-1649",
    "requested_on": "2018-10-31T11:32:38.390000"
  },
  "total_count": "0",
  "total_pages": "0"
}

```

<a id="schemathirdpartyhaulerconnectionlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page. Must be integer greater than or equal to 1. Must be integer less than or equal to 1000.|
|`current_page`|integer(int64)|Paged results page index (starting from 1). Must be integer greater than or equal to 1. Must be integer less than or equal to 10000.|
|`results`|[ThirdPartyHaulerConnectionModel](#schemathirdpartyhaulerconnectionmodel)|-|
|`total_count`|integer(int64)|Paged results total viewable records. Must be integer greater than or equal to 0. Must be integer less than or equal to 100000.|
|`total_pages`|integer(int64)|Paged results total pages. Must be integer greater than or equal to 0. Must be integer less than or equal to 1000.|

<h2 id="tocSthirdpartyhaulerconnectionmodel">ThirdPartyHaulerConnectionModel</h2>

```json
{
  "approved_by": "1",
  "approved_on": "2018-10-31T11:32:38.390000",
  "denied_on": "2018-10-31T11:32:38.390000",
  "is_approved": "0",
  "location_id": "1",
  "provider_email": "support@crosoftware.net",
  "provider_id": "1",
  "provider_name": "John C. Doe",
  "provider_phone": "+1 (360) 733-1649",
  "requested_on": "2018-10-31T11:32:38.390000"
}

```

<a id="schemathirdpartyhaulerconnectionmodel"></a>

|Name|Type|Description|
|---|---|---|
|`approved_by`|integer(int64)|Approved by. Must be valid resource identifier (integer).|
|`approved_on`|string(DateTime)|Approval date. Must be a date in an ISO 8601 compatible format.|
|`denied_on`|string(DateTime)|Denial date. Must be a date in an ISO 8601 compatible format.|
|`is_approved`|boolean|Approved record state. Must be one of [0, 1, True, False] (case insensitive).|
|`location_id`|integer(int64)|Location identifier (integer) Must be valid resource identifier (integer).|
|`provider_email`|string(Email)|Email address. Must be a valid email address.|
|`provider_id`|integer(int64)|Bin provider identifier (integer) Must be valid resource identifier (integer).|
|`provider_name`|string|Name (free text). Must be at least 1 and no more than 64 characters.|
|`provider_phone`|string(PhoneNumber)|Phone number (free text). At least 7 characters, not more than 15.|
|`requested_on`|string(DateTime)|Requested date. Must be a date occurring in the past in an ISO 8601 compatible format.|

<h2 id="tocSthirdpartyhaulerlistmodel">ThirdPartyHaulerListModel</h2>

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "id": "defbc66e-f908-40d9-9ee5-655a1f699311",
      "name": "John C. Doe"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}

```

<a id="schemathirdpartyhaulerlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page. Must be integer greater than or equal to 1. Must be integer less than or equal to 1000.|
|`current_page`|integer(int64)|Paged results page index (starting from 1). Must be integer greater than or equal to 1. Must be integer less than or equal to 10000.|
|`results`|array[[ThirdPartyHaulerModel](#schemathirdpartyhaulermodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records. Must be integer greater than or equal to 0. Must be integer less than or equal to 100000.|
|`total_pages`|integer(int64)|Paged results total pages. Must be integer greater than or equal to 0. Must be integer less than or equal to 1000.|

<h2 id="tocSthirdpartyhaulermodel">ThirdPartyHaulerModel</h2>

```json
{
  "id": "defbc66e-f908-40d9-9ee5-655a1f699311",
  "name": "John C. Doe"
}

```

<a id="schemathirdpartyhaulermodel"></a>

|Name|Type|Description|
|---|---|---|
|`id`|string(Uuid)|Third party hauler identifier. Must be a valid UUID.|
|`name`|string|Name (free text). Must be at least 1 and no more than 64 characters.|

<h2 id="tocStrucklistmodel">TruckListModel</h2>

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "driver_id": "1",
      "id": "1",
      "location_id": "1",
      "name": "John C. Doe",
      "notes": "Bin located in alley.",
      "out_of_service": "0",
      "require_odometer": "0",
      "third_party_hauler_id": "defbc66e-f908-40d9-9ee5-655a1f699311",
      "type": "R59",
      "weight": "0"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}

```

<a id="schematrucklistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page. Must be integer greater than or equal to 1. Must be integer less than or equal to 1000.|
|`current_page`|integer(int64)|Paged results page index (starting from 1). Must be integer greater than or equal to 1. Must be integer less than or equal to 10000.|
|`results`|array[[TruckModel](#schematruckmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records. Must be integer greater than or equal to 0. Must be integer less than or equal to 100000.|
|`total_pages`|integer(int64)|Paged results total pages. Must be integer greater than or equal to 0. Must be integer less than or equal to 1000.|

<h2 id="tocStruckmodel">TruckModel</h2>

```json
{
  "driver_id": "1",
  "id": "1",
  "location_id": "1",
  "name": "John C. Doe",
  "notes": "Bin located in alley.",
  "out_of_service": "0",
  "require_odometer": "0",
  "third_party_hauler_id": "defbc66e-f908-40d9-9ee5-655a1f699311",
  "type": "R59",
  "weight": "0"
}

```

<a id="schematruckmodel"></a>

|Name|Type|Description|
|---|---|---|
|`driver_id`|integer(int64)|Driver identifier. Must be valid resource identifier (integer).|
|`id`|integer(int64)|Resource identifier (integer) Must be valid resource identifier (integer).|
|`location_id`|integer(int64)|Location identifier (integer) Must be valid resource identifier (integer).|
|`name`|string|Name (free text). Must be at least 1 and no more than 64 characters.|
|`notes`|string|Notes (free text). Must be at least 1 and no more than 2048 characters.|
|`out_of_service`|boolean|Truck out of service. Must be one of [0, 1, True, False] (case insensitive).|
|`require_odometer`|boolean|Require odometer. Must be one of [0, 1, True, False] (case insensitive).|
|`third_party_hauler_id`|string(Uuid)|Third party hauler identifier. Must be a valid UUID.|
|`type`|string|Truck type (free text). Must be at least 1 and no more than 50 characters.|
|`weight`|number(float)|Truck empty weight. Must be float greater than or equal to 0. Must be float less than or equal to 10000000.|

<h2 id="tocSupdatecustomeraddressmodel">UpdateCustomerAddressModel</h2>

```json
{
  "country": "US",
  "is_billing": "0",
  "is_shipping": "0",
  "latitude": "-90",
  "line_1": "321 Chase Rd",
  "line_2": "P.O. Box 256",
  "line_3": "3rd Floor",
  "line_4": "Last door on the left (blue)",
  "locality": "Sequim",
  "longitude": "-180",
  "postcode": "98368",
  "region": "WA"
}

```

<a id="schemaupdatecustomeraddressmodel"></a>

|Name|Type|Description|
|---|---|---|
|`country`|string|Country code (ISO 3166-1 alpha 2). Must be a 2 character country code.|
|`is_billing`|boolean|If true, this is the customer's billing address. Must be one of [0, 1, True, False] (case insensitive).|
|`is_shipping`|boolean|Customer's shipping address if true. Must be one of [0, 1, True, False] (case insensitive).|
|`latitude`|number(float)|Latitude. Must be float greater than or equal to -90. Must be float less than or equal to 90.|
|`line_1`|string|Street address. Must be at least 1 and no more than 256 characters.|
|`line_2`|string|Street address line 2. Must be at least 1 and no more than 256 characters.|
|`line_3`|string|Street address line 3. Must be at least 1 and no more than 256 characters.|
|`line_4`|string|Street address line 4 (doubles as county). Must be at least 1 and no more than 256 characters.|
|`locality`|string|Address locality (e.g. city). Must be at least 1 and no more than 86 characters.|
|`longitude`|number(float)|longitude. Must be float greater than or equal to -180. Must be float less than or equal to 180.|
|`postcode`|string|Postal code (may include letters and symbols). Must be at least 1 and no more than 86 characters.|
|`region`|string|Address region (e.g. state). Must be at least 1 and no more than 32 characters.|

<h2 id="tocSupdatecustomercontactmodel">UpdateCustomerContactModel</h2>

```json
{
  "email": "support@crosoftware.net",
  "fax": "+1 (360) 733-1649",
  "name": "John C. Doe",
  "notify_on_acknowledged_request": "0",
  "notify_on_completed_request": "0",
  "notify_on_dispatched_request": "0",
  "notify_on_failed_request": "0",
  "notify_on_new_request": "0",
  "number": "+1 (360) 733-1649"
}

```

<a id="schemaupdatecustomercontactmodel"></a>

|Name|Type|Description|
|---|---|---|
|`email`|string(Email)|Email address. Must be a valid email address.|
|`fax`|string(PhoneNumber)|Fax number (free text). At least 7 characters, not more than 15.|
|`name`|string|Name (free text). Must be at least 1 and no more than 64 characters.|
|`notify_on_acknowledged_request`|boolean|Notify on acknowledge request. Must be one of [0, 1, True, False] (case insensitive).|
|`notify_on_completed_request`|boolean|Notify on completed request. Must be one of [0, 1, True, False] (case insensitive).|
|`notify_on_dispatched_request`|boolean|Notify on dispatched request. Must be one of [0, 1, True, False] (case insensitive).|
|`notify_on_failed_request`|boolean|Notify on failed request. Must be one of [0, 1, True, False] (case insensitive).|
|`notify_on_new_request`|boolean|Notify on new request. Must be one of [0, 1, True, False] (case insensitive).|
|`number`|string(PhoneNumber)|Phone number (free text). At least 7 characters, not more than 15.|

<h2 id="tocSupdatecustomerlocationmodel">UpdateCustomerLocationModel</h2>

```json
{
  "is_commercial": "0",
  "note": "Bin located in alley.",
  "reference_number": "REF#100A61",
  "renewal_date": "2018-10-31T11:32:38.390000",
  "sales_rep": "John C. Doe",
  "suspension_id": "1"
}

```

<a id="schemaupdatecustomerlocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`is_commercial`|boolean|Commercial address if true, private if false. Must be one of [0, 1, True, False] (case insensitive).|
|`note`|string|Notes (free text). Must be at least 1 and no more than 2048 characters.|
|`reference_number`|string|Reference number (free text). Must be at least 1 and no more than 256 characters.|
|`renewal_date`|string(DateTime)|Renewal date. Must be a date in an ISO 8601 compatible format.|
|`sales_rep`|string|Name of sales representative. Must be at least 1 and no more than 64 characters.|
|`suspension_id`|integer(int64)|Suspension identifier. Must be valid resource identifier (integer).|

<h2 id="tocSupdatecustomermodel">UpdateCustomerModel</h2>

```json
{
  "name": "John C. Doe",
  "parent_id": "1"
}

```

<a id="schemaupdatecustomermodel"></a>

|Name|Type|Description|
|---|---|---|
|`name`|string|Name (free text). Must be at least 1 and no more than 64 characters.|
|`parent_id`|integer(int64)|Parent record identifier (integer) Must be valid resource identifier (integer).|

<h2 id="tocSupdatewebhookmodel">UpdateWebhookModel</h2>

```json
{
  "events": [
    "customer"
  ],
  "url": "http://your.callback.url.net"
}

```

<a id="schemaupdatewebhookmodel"></a>

|Name|Type|Description|
|---|---|---|
|`events`|array[string]|Hook event. Must be a valid hook event (one of: customer, job).|
|`url`|string(Url)|Callback URL. URL conforming to RFC 1738.|

<h2 id="tocSupdatedjobmodel">UpdatedJobModel</h2>

```json
{
  "arrived_at_dest": "2018-10-31T11:32:38.390000",
  "arrived_on": "2018-10-31T11:32:38.390000",
  "asset_dropped": "0",
  "asset_id": "1",
  "asset_quantity": "0",
  "asset_type_id": "1",
  "completed_by": "1",
  "completed_by_driver": "0",
  "completed_on": "2018-10-31T11:32:38.390000",
  "confirmed_on": "2018-10-31T11:32:38.390000",
  "created_by_id": "1",
  "customer_id": "1",
  "customer_notes": "Some notes from a customer to a dispatcher.",
  "desired_asset_desc": "Some asset characteristics.",
  "dispatch_priority": "H",
  "dispatched_by_route": "1",
  "dispatched_on": "2018-10-31T11:32:38.390000",
  "dispatcher_notes": "Some dispatcher notes.",
  "do_confirm": "0",
  "driver_notes": "Some driver notes.",
  "dump_location_id": "1",
  "dumped_on": "2018-10-31T11:32:38.390000",
  "end_time": "2018-10-31T11:32:38.390000",
  "fail_reason": "A reason for failure.",
  "final_location_id": "1",
  "flags": "A reason for failure.",
  "id": "1",
  "invoice_notes": "Some invoice notes.",
  "is_completed": "0",
  "is_declined": "0",
  "is_deleted": "0",
  "is_failed": "0",
  "job_group_id": "1",
  "location_id": "1",
  "merged_with_route": "1",
  "original_schedule_date": "2018-10-31T11:32:38.390000",
  "pickup_date": "2018-10-31T11:32:38.390000",
  "priority": "-999999",
  "reference_number": "REF#100A61",
  "requested_on": "2018-10-31T11:32:38.390000",
  "require_image": "0",
  "require_material": "0",
  "require_signature": "0",
  "require_weights": "0",
  "schedule_date": "2018-10-31T11:32:38.390000",
  "start_location_id": "1",
  "start_time": "2018-10-31T11:32:38.390000",
  "third_party_hauler_id": "defbc66e-f908-40d9-9ee5-655a1f699311",
  "times_failed": "0",
  "times_rolled_over": "0",
  "truck_id": "1",
  "type": "R",
  "weighed_on": "2018-10-31T11:32:38.390000"
}

```

<a id="schemaupdatedjobmodel"></a>

|Name|Type|Description|
|---|---|---|
|`arrived_at_dest`|string(DateTime)|Entered by driver for dispatcher and customer. Asset arrival at destination time. Only applicable for jobs with a valid dump destination. Must be a date in an ISO 8601 compatible format.|
|`arrived_on`|string(DateTime)|Drive start time entered by driver for dispatcher and customer (arrived at job slider). Must be a date in an ISO 8601 compatible format.|
|`asset_dropped`|integer(int64)|Reference to deployed asset entered by driver for customer, dispatcher applicable to job types  'D', 'E'. Must be integer greater than or equal to 0. Must be integer less than or equal to 10000.|
|`asset_id`|integer(int64)|Job asset identifier. Applicable to job types 'E', 'P', 'R'. Must be valid resource identifier (integer).|
|`asset_quantity`|integer(int64)|How many assets are being serviced within a cluster (for jobs assigned to an asset cluster). For jobs dispatched by routes, or manually dispatched route stops, this value is 0 or 1. Must be integer greater than or equal to 0.|
|`asset_type_id`|integer(int64)|Selected asset for the job (job types 'D', 'L', 'E'). Must be valid resource identifier (integer).|
|`completed_by`|integer(int64)|Dispatcher or driver id. Must be valid resource identifier (integer).|
|`completed_by_driver`|boolean|If TRUE, completed by driver. If FALSE, completed by dispatcher. Must be one of [0, 1, True, False] (case insensitive).|
|`completed_on`|string(DateTime)|Job completion time. Must be a date occurring in the past in an ISO 8601 compatible format.|
|`confirmed_on`|string(DateTime)|Job confirmation date. Must be a date occurring in the past in an ISO 8601 compatible format.|
|`created_by_id`|integer(int64)|Customer, dispatcher, or driver id. Must be valid resource identifier (integer).|
|`customer_id`|integer(int64)|Customer identifier. Must be valid resource identifier (integer).|
|`customer_notes`|string|Notes entered by customers to communicate with dispatchers. Must be at least 0 and no more than 2048 characters.|
|`desired_asset_desc`|string|Free-form text entered by dispatchers and drivers to be used as the future asset description. Must be at least 1 and no more than 2048 characters.|
|`dispatch_priority`|string|Entered by dispatchers to determine dispatch order. Must be one of: 'H', 'M', 'L' (where 'H'='High', 'M'='Medium', 'L'='Low').|
|`dispatched_by_route`|integer(int64)|Route id of dispatching route (or NULL if not dispatched by a route). Must be valid resource identifier (integer).|
|`dispatched_on`|string(DateTime)|Time the job is assigned to a truck. Must be a date in an ISO 8601 compatible format.|
|`dispatcher_notes`|string|Entered by dispatchers, read by drivers and dispatchers. Must be at least 1 and no more than 2048 characters.|
|`do_confirm`|boolean|Tell dispatcher that a customer should be contacted before job is dispatched. Must be one of [0, 1, True, False] (case insensitive).|
|`driver_notes`|string|Entered by drivers when completing or failing a job for dispatchers. Must be at least 1 and no more than 2048 characters.|
|`dump_location_id`|integer(int64)|Asset or asset cluster dump location identifier (e.g. trash bin needs dumped before returning from customer). Must be valid resource identifier (integer).|
|`dumped_on`|string(DateTime)|Dump request completion date. Must be a date in an ISO 8601 compatible format.|
|`end_time`|string(DateTime)|Future estimated time of job completion. Must be a date in an ISO 8601 compatible format.|
|`fail_reason`|string|Failure description selected by a driver for use by dispatchers. Must be at least 0 and no more than 64 characters.|
|`final_location_id`|integer(int64)|Final location identifier. Used by dispatchers for prioritizing jobs. Used by drivers to know where to leave the asset on job completion. Must be valid resource identifier (integer).|
|`flags`|string|Job notes. Must be at least 0 and no more than 64 characters.|
|`id`|integer(int64)|Resource identifier (integer) Must be valid resource identifier (integer).|
|`invoice_notes`|string|Invoice notes from the billing system. Must be at least 1 and no more than 2048 characters.|
|`is_completed`|boolean|Job completion flag set by dispatchers and drivers. Must be one of [0, 1, True, False] (case insensitive).|
|`is_declined`|boolean|Job completion flag set by dispatchers and drivers. Must be one of [0, 1, True, False] (case insensitive).|
|`is_deleted`|boolean|Indicates whether job is still valid. Must be one of [0, 1, True, False] (case insensitive).|
|`is_failed`|boolean|Set by drivers and dispatchers to indicate a failed job. Must be one of [0, 1, True, False] (case insensitive).|
|`job_group_id`|integer(int64)|Job group identifier for group jobs (vs service, exchange, etc.). Must be valid resource identifier (integer).|
|`location_id`|integer(int64)|Location identifier (integer) Must be valid resource identifier (integer).|
|`merged_with_route`|integer(int64)|Assigned by dispatchers for dispatchers and drivers. Must be valid resource identifier (integer).|
|`original_schedule_date`|string(DateTime)|Original scheduling date. Must be a date in an ISO 8601 compatible format.|
|`pickup_date`|string(DateTime)|A pickup job is scheduled for this date upon job completion. If the asset or cluster is assigned to a route stop, the route stop will be deleted. Must be in the future. Must be a date in an ISO 8601 compatible format.|
|`priority`|integer(int64)|Assigned by dispatchers for job order completion determination for drivers. Must be integer greater than or equal to -999999. Must be integer less than or equal to -1.|
|`reference_number`|string|Reference number (free text). Must be at least 1 and no more than 256 characters.|
|`requested_on`|string(DateTime)|Requested date. Must be a date occurring in the past in an ISO 8601 compatible format.|
|`require_image`|boolean|Set by dispatchers and drivers, requires drivers to upload one or more job images before completion. Must be one of [0, 1, True, False] (case insensitive).|
|`require_material`|boolean|Set by dispatchers and drivers, requires drivers to set a material before completing a job. Must be one of [0, 1, True, False] (case insensitive).|
|`require_signature`|boolean|Set by dispatchers and drivers, requires drivers to get a customer signature before job completion. Must be one of [0, 1, True, False] (case insensitive).|
|`require_weights`|boolean|Set by disptachers and drivers, requires drivers to set material weights before job completion. Must be one of [0, 1, True, False] (case insensitive).|
|`schedule_date`|string(DateTime)|Scheduled job completion date. Must be a date in an ISO 8601 compatible format.|
|`start_location_id`|integer(int64)|Pickup location for asset or asset cluster Set by dispatchers and drivers for drivers. Must be valid resource identifier (integer).|
|`start_time`|string(DateTime)|Time customer has requested job start, set by dispatchers for dispatchers and drivers. Must be a date in an ISO 8601 compatible format.|
|`third_party_hauler_id`|string(Uuid)|Third party hauler identifier. Must be a valid UUID.|
|`times_failed`|integer(int64)|Number of times a job has been attempted and failed. Must be integer greater than or equal to 0.|
|`times_rolled_over`|integer(int64)|Tracks job age in days for dispatchers. Must be integer greater than or equal to 0.|
|`truck_id`|integer(int64)|Truck identifier. Must be valid resource identifier (integer).|
|`type`|string|Set by dispatchers and customers. Represents physical actions to execute on job start. Must be one of: 'R', 'P', 'D', 'E', 'L'.|
|`weighed_on`|string(DateTime)|Time of truck weight entry. Must be a date occurring in the past in an ISO 8601 compatible format.|

<h2 id="tocSwebhooklistmodel">WebhookListModel</h2>

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "events": [
        "customer"
      ],
      "id": "1",
      "url": "http://your.callback.url.net"
    }
  ],
  "total_count": "0",
  "total_pages": "0"
}

```

<a id="schemawebhooklistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page. Must be integer greater than or equal to 1. Must be integer less than or equal to 1000.|
|`current_page`|integer(int64)|Paged results page index (starting from 1). Must be integer greater than or equal to 1. Must be integer less than or equal to 10000.|
|`results`|array[[WebhookModel](#schemawebhookmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records. Must be integer greater than or equal to 0. Must be integer less than or equal to 100000.|
|`total_pages`|integer(int64)|Paged results total pages. Must be integer greater than or equal to 0. Must be integer less than or equal to 1000.|

<h2 id="tocSwebhookmodel">WebhookModel</h2>

```json
{
  "events": [
    "customer"
  ],
  "id": "1",
  "url": "http://your.callback.url.net"
}

```

<a id="schemawebhookmodel"></a>

|Name|Type|Description|
|---|---|---|
|`events`|array[string]|Hook event. Must be a valid hook event (one of: customer, job).|
|`id`|integer(int64)|Resource identifier (integer) Must be valid resource identifier (integer).|
|`url`|string(Url)|Callback URL. URL conforming to RFC 1738.|

