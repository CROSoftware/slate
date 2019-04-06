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

<h1 id="cro-software-api">CRO Software API v0</h1>

Build on & integrate with CRO Software.

Base URLs:

* <a href="https://api.crosoftware.net">https://api.crosoftware.net</a>

Email: <a href="mailto:develop@crosoftware.net">Support</a> 

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdadd_customer_address"></a>

Add customer address.

> Body parameter

```json
{
  "country": "US",
  "is_billing": "True",
  "is_shipping": "False",
  "latitude": "46.881398",
  "line_1": "643 Summer Breeze",
  "line_2": "Suite 34",
  "line_3": "2nd Door on Left",
  "line_4": "Blue slot",
  "locality": "Sequim",
  "longitude": "-121.276566",
  "postcode": "98382",
  "region": "WA"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`body`|body|[AddCustomerAddressProfileModel](#schemaaddcustomeraddressprofilemodel)|true||

> Example responses

> 200 Response

```json
{
  "address_id": "1",
  "country": "US",
  "is_billing": "True",
  "is_physical": "True",
  "is_shipping": "False",
  "latitude": "46.881398",
  "line_1": "643 Summer Breeze",
  "line_2": "Suite 34",
  "line_3": "2nd Door on Left",
  "line_4": "Blue slot",
  "locality": "Sequim",
  "longitude": "-121.276566",
  "postcode": "98382",
  "region": "WA"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressModel](#schemacustomeraddressmodel)|Added customer address profile.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIddeactivate_customer_address"></a>

Deactivate (remove from use) customer address.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`address_id`|path|integer(int64)|true|Address identifier.|

> Example responses

> 200 Response

```json
{
  "address_id": "1",
  "country": "US",
  "is_billing": "True",
  "is_physical": "True",
  "is_shipping": "False",
  "latitude": "46.881398",
  "line_1": "643 Summer Breeze",
  "line_2": "Suite 34",
  "line_3": "2nd Door on Left",
  "line_4": "Blue slot",
  "locality": "Sequim",
  "longitude": "-121.276566",
  "postcode": "98382",
  "region": "WA"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressModel](#schemacustomeraddressmodel)|Deactivated (removed from use) customer address.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdget_customer_address"></a>

Customer address profile.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`address_id`|path|integer(int64)|true|Address identifier.|

> Example responses

> 200 Response

```json
{
  "address_id": "1",
  "country": "US",
  "is_billing": "True",
  "is_physical": "True",
  "is_shipping": "False",
  "latitude": "46.881398",
  "line_1": "643 Summer Breeze",
  "line_2": "Suite 34",
  "line_3": "2nd Door on Left",
  "line_4": "Blue slot",
  "locality": "Sequim",
  "longitude": "-121.276566",
  "postcode": "98382",
  "region": "WA"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressModel](#schemacustomeraddressmodel)|Address Profile|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdlist_customer_addresses"></a>

List of customer location settings.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

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
      "is_billing": "True",
      "is_physical": "True",
      "is_shipping": "False",
      "latitude": "46.881398",
      "line_1": "643 Summer Breeze",
      "line_2": "Suite 34",
      "line_3": "2nd Door on Left",
      "line_4": "Blue slot",
      "locality": "Sequim",
      "longitude": "-121.276566",
      "postcode": "98382",
      "region": "WA"
    }
  ],
  "total_count": "1",
  "total_pages": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressListModel](#schemacustomeraddresslistmodel)|List|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdupdate_customer_address"></a>

Update customer address.

> Body parameter

```json
{
  "country": "US",
  "is_billing": "True",
  "is_physical": "True",
  "is_shipping": "False",
  "latitude": "46.881398",
  "line_1": "643 Summer Breeze",
  "line_2": "Suite 34",
  "line_3": "2nd Door on Left",
  "line_4": "Blue slot",
  "locality": "Sequim",
  "longitude": "-121.276566",
  "postcode": "98382",
  "region": "WA"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`address_id`|path|integer(int64)|true|Address identifier.|
|`body`|body|[UpdateCustomerAddressProfileModel](#schemaupdatecustomeraddressprofilemodel)|true||

> Example responses

> 200 Response

```json
{
  "address_id": "1",
  "country": "US",
  "is_billing": "True",
  "is_physical": "True",
  "is_shipping": "False",
  "latitude": "46.881398",
  "line_1": "643 Summer Breeze",
  "line_2": "Suite 34",
  "line_3": "2nd Door on Left",
  "line_4": "Blue slot",
  "locality": "Sequim",
  "longitude": "-121.276566",
  "postcode": "98382",
  "region": "WA"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressModel](#schemacustomeraddressmodel)|Updated customer address profile.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

## Customer Contacts

### Add Contact

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdadd_customer_contact"></a>

Add customer contact.

> Body parameter

```json
{
  "email": "develop@crosoftware.com",
  "fax": "(360) 716-1968",
  "name": "John Doe",
  "notify_on_acknowledged_request": "False",
  "notify_on_completed_request": "False",
  "notify_on_dispatched_request": "False",
  "notify_on_failed_request": "False",
  "notify_on_new_request": "False",
  "number": "1-111-111-1111"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`body`|body|[AddCustomerContactProfileModel](#schemaaddcustomercontactprofilemodel)|true||

> Example responses

> 200 Response

```json
{
  "contact_id": "1",
  "email": "develop@crosoftware.com",
  "fax": "(360) 716-1968",
  "name": "John Doe",
  "notify_on_acknowledged_request": "False",
  "notify_on_completed_request": "False",
  "notify_on_dispatched_request": "False",
  "notify_on_failed_request": "False",
  "notify_on_new_request": "False",
  "number": "1-111-111-1111"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerContactModel](#schemacustomercontactmodel)|Added customer contact profile.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdget_customer_contact"></a>

Customer contact profile.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`contact_id`|path|integer(int64)|true|Contact identifier.|

> Example responses

> 200 Response

```json
{
  "contact_id": "1",
  "email": "develop@crosoftware.com",
  "fax": "(360) 716-1968",
  "name": "John Doe",
  "notify_on_acknowledged_request": "False",
  "notify_on_completed_request": "False",
  "notify_on_dispatched_request": "False",
  "notify_on_failed_request": "False",
  "notify_on_new_request": "False",
  "number": "1-111-111-1111"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerContactModel](#schemacustomercontactmodel)|Contact Profile|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdlist_customer_contacts"></a>

List of customer contacts.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

> Example responses

> 200 Response

```json
{
  "current_limit": "100",
  "current_page": "1",
  "results": [
    {
      "contact_id": "1",
      "email": "develop@crosoftware.com",
      "fax": "(360) 716-1968",
      "name": "John Doe",
      "notify_on_acknowledged_request": "False",
      "notify_on_completed_request": "False",
      "notify_on_dispatched_request": "False",
      "notify_on_failed_request": "False",
      "notify_on_new_request": "False",
      "number": "1-111-111-1111"
    }
  ],
  "total_count": "100",
  "total_pages": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerContactListModel](#schemacustomercontactlistmodel)|List|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdupdate_customer_contact"></a>

Update customer contact.

> Body parameter

```json
{
  "email": "develop@crosoftware.com",
  "fax": "(360) 716-1968",
  "name": "John Doe",
  "notify_on_acknowledged_request": "False",
  "notify_on_completed_request": "False",
  "notify_on_dispatched_request": "False",
  "notify_on_failed_request": "False",
  "notify_on_new_request": "False",
  "number": "1-111-111-1111"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`contact_id`|path|integer(int64)|true|Contact identifier.|
|`body`|body|[UpdateCustomerContactProfileModel](#schemaupdatecustomercontactprofilemodel)|true||

> Example responses

> 200 Response

```json
{
  "contact_id": "1",
  "email": "develop@crosoftware.com",
  "fax": "(360) 716-1968",
  "name": "John Doe",
  "notify_on_acknowledged_request": "False",
  "notify_on_completed_request": "False",
  "notify_on_dispatched_request": "False",
  "notify_on_failed_request": "False",
  "notify_on_new_request": "False",
  "number": "1-111-111-1111"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerContactModel](#schemacustomercontactmodel)|Updated customer contact profile.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

## Customer Locations

### Add Location

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
          String url = "https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}";

          // Headers
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          byte[] json = client.UploadValues(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/customers/{customer_id}/locations/{location_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}',
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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
}

r = requests.post('https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}");
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

`POST /customers/{customer_id}/locations/{location_id}`

<a id="opIdadd_customer_location"></a>

Add customer to location.

> Body parameter

```json
{
  "is_commercial": "True",
  "note": "An example note",
  "reference_number": "R100-10C",
  "renewal_date": "2100-02-12T01:32:45.640000",
  "sales_rep": "John Smith",
  "suspension_id": "1"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`body`|body|[AddCustomerLocationProfileModel](#schemaaddcustomerlocationprofilemodel)|true||

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "address_id": "1",
      "country": "US",
      "is_billing": "True",
      "is_physical": "True",
      "is_shipping": "False",
      "latitude": "46.881398",
      "line_1": "643 Summer Breeze",
      "line_2": "Suite 34",
      "line_3": "2nd Door on Left",
      "line_4": "Blue slot",
      "locality": "Sequim",
      "longitude": "-121.276566",
      "postcode": "98382",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "contact_id": "1",
      "email": "develop@crosoftware.com",
      "fax": "(360) 716-1968",
      "name": "John Doe",
      "notify_on_acknowledged_request": "False",
      "notify_on_completed_request": "False",
      "notify_on_dispatched_request": "False",
      "notify_on_failed_request": "False",
      "notify_on_new_request": "False",
      "number": "1-111-111-1111"
    }
  ],
  "created_on": "2019-03-08T16:40:37.647000",
  "customer_id": "2",
  "is_active": "True",
  "is_commercial": "False",
  "last_edited": "2019-03-08T16:40:37.647000",
  "name": "Jane Smith",
  "note": "An example note",
  "parent_id": "1",
  "reference_number": "1234",
  "renewal_date": "2100-03-08T16:40:37.647000",
  "sales_rep": "Jane Doe",
  "suspension_id": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationModel](#schemacustomerlocationmodel)|Added customer location profile.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          String url = "https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}";

          // Headers
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          byte[] json = client.UploadValues(url, "DELETE", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X DELETE https://api.crosoftware.net/customers/{customer_id}/locations/{location_id} \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}',
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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.delete 'https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
}

r = requests.delete('https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}");
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

`DELETE /customers/{customer_id}/locations/{location_id}`

<a id="opIddeactivate_customer_at_location"></a>

Deactivate customer at location.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "address_id": "1",
      "country": "US",
      "is_billing": "True",
      "is_physical": "True",
      "is_shipping": "False",
      "latitude": "46.881398",
      "line_1": "643 Summer Breeze",
      "line_2": "Suite 34",
      "line_3": "2nd Door on Left",
      "line_4": "Blue slot",
      "locality": "Sequim",
      "longitude": "-121.276566",
      "postcode": "98382",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "contact_id": "1",
      "email": "develop@crosoftware.com",
      "fax": "(360) 716-1968",
      "name": "John Doe",
      "notify_on_acknowledged_request": "False",
      "notify_on_completed_request": "False",
      "notify_on_dispatched_request": "False",
      "notify_on_failed_request": "False",
      "notify_on_new_request": "False",
      "number": "1-111-111-1111"
    }
  ],
  "created_on": "2019-03-08T16:40:37.647000",
  "customer_id": "2",
  "is_active": "True",
  "is_commercial": "False",
  "last_edited": "2019-03-08T16:40:37.647000",
  "name": "Jane Smith",
  "note": "An example note",
  "parent_id": "1",
  "reference_number": "1234",
  "renewal_date": "2100-03-08T16:40:37.647000",
  "sales_rep": "Jane Doe",
  "suspension_id": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationModel](#schemacustomerlocationmodel)|Deactivated customer profile for customer at given location.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          String url = "https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}";

          // Headers
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/customers/{customer_id}/locations/{location_id} \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}',
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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
}

r = requests.get('https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}");
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

`GET /customers/{customer_id}/locations/{location_id}`

<a id="opIdget_customer_location"></a>

Customer location settings for given location.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "address_id": "1",
      "country": "US",
      "is_billing": "True",
      "is_physical": "True",
      "is_shipping": "False",
      "latitude": "46.881398",
      "line_1": "643 Summer Breeze",
      "line_2": "Suite 34",
      "line_3": "2nd Door on Left",
      "line_4": "Blue slot",
      "locality": "Sequim",
      "longitude": "-121.276566",
      "postcode": "98382",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "contact_id": "1",
      "email": "develop@crosoftware.com",
      "fax": "(360) 716-1968",
      "name": "John Doe",
      "notify_on_acknowledged_request": "False",
      "notify_on_completed_request": "False",
      "notify_on_dispatched_request": "False",
      "notify_on_failed_request": "False",
      "notify_on_new_request": "False",
      "number": "1-111-111-1111"
    }
  ],
  "created_on": "2019-03-08T16:40:37.647000",
  "customer_id": "2",
  "is_active": "True",
  "is_commercial": "False",
  "last_edited": "2019-03-08T16:40:37.647000",
  "name": "Jane Smith",
  "note": "An example note",
  "parent_id": "1",
  "reference_number": "1234",
  "renewal_date": "2100-03-08T16:40:37.647000",
  "sales_rep": "Jane Doe",
  "suspension_id": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationModel](#schemacustomerlocationmodel)|Customer Location Profile|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdlist_customer_locations"></a>

List of customer location settings.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

> Example responses

> 200 Response

```json
{
  "current_limit": "100",
  "current_page": "1",
  "results": [
    {
      "addresses": [
        {
          "address_id": "1",
          "country": "US",
          "is_billing": "True",
          "is_physical": "True",
          "is_shipping": "False",
          "latitude": "46.881398",
          "line_1": "643 Summer Breeze",
          "line_2": "Suite 34",
          "line_3": "2nd Door on Left",
          "line_4": "Blue slot",
          "locality": "Sequim",
          "longitude": "-121.276566",
          "postcode": "98382",
          "region": "WA"
        }
      ],
      "contacts": [
        {
          "contact_id": "1",
          "email": "develop@crosoftware.com",
          "fax": "(360) 716-1968",
          "name": "John Doe",
          "notify_on_acknowledged_request": "False",
          "notify_on_completed_request": "False",
          "notify_on_dispatched_request": "False",
          "notify_on_failed_request": "False",
          "notify_on_new_request": "False",
          "number": "1-111-111-1111"
        }
      ],
      "created_on": "2019-03-08T16:40:37.647000",
      "customer_id": "2",
      "is_active": "True",
      "is_commercial": "False",
      "last_edited": "2019-03-08T16:40:37.647000",
      "name": "Jane Smith",
      "note": "An example note",
      "parent_id": "1",
      "reference_number": "1234",
      "renewal_date": "2100-03-08T16:40:37.647000",
      "sales_rep": "Jane Doe",
      "suspension_id": "1"
    }
  ],
  "total_count": "100",
  "total_pages": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationListModel](#schemacustomerlocationlistmodel)|Customer Location List|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

### Update Location

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
          String url = "https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}";

          // Headers
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          byte[] json = client.UploadValues(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/customers/{customer_id}/locations/{location_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}',
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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
}

r = requests.patch('https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/locations/{location_id}");
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

`PATCH /customers/{customer_id}/locations/{location_id}`

<a id="opIdupdate_customer_location"></a>

Update customer location settings.

> Body parameter

```json
{
  "is_commercial": "True",
  "note": "An example note",
  "reference_number": "R100-10C",
  "renewal_date": "2100-02-12T01:32:45.640000",
  "sales_rep": "John Smith",
  "suspension_id": "1"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`body`|body|[UpdateCustomerLocationProfileModel](#schemaupdatecustomerlocationprofilemodel)|true||

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "address_id": "1",
      "country": "US",
      "is_billing": "True",
      "is_physical": "True",
      "is_shipping": "False",
      "latitude": "46.881398",
      "line_1": "643 Summer Breeze",
      "line_2": "Suite 34",
      "line_3": "2nd Door on Left",
      "line_4": "Blue slot",
      "locality": "Sequim",
      "longitude": "-121.276566",
      "postcode": "98382",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "contact_id": "1",
      "email": "develop@crosoftware.com",
      "fax": "(360) 716-1968",
      "name": "John Doe",
      "notify_on_acknowledged_request": "False",
      "notify_on_completed_request": "False",
      "notify_on_dispatched_request": "False",
      "notify_on_failed_request": "False",
      "notify_on_new_request": "False",
      "number": "1-111-111-1111"
    }
  ],
  "created_on": "2019-03-08T16:40:37.647000",
  "customer_id": "2",
  "is_active": "True",
  "is_commercial": "False",
  "last_edited": "2019-03-08T16:40:37.647000",
  "name": "Jane Smith",
  "note": "An example note",
  "parent_id": "1",
  "reference_number": "1234",
  "renewal_date": "2100-03-08T16:40:37.647000",
  "sales_rep": "Jane Doe",
  "suspension_id": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationModel](#schemacustomerlocationmodel)|Added customer location profile.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

## Customers

### Create Customer for Location

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdcreate_customer_at_location"></a>

Create customer for location.

> Body parameter

```json
{
  "addresses": [
    {
      "country": "US",
      "is_billing": "True",
      "is_shipping": "False",
      "latitude": "46.881398",
      "line_1": "643 Summer Breeze",
      "line_2": "Suite 34",
      "line_3": "2nd Door on Left",
      "line_4": "Blue slot",
      "locality": "Sequim",
      "longitude": "-121.276566",
      "postcode": "98382",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "email": "develop@crosoftware.com",
      "fax": "(360) 716-1968",
      "name": "John Doe",
      "notify_on_acknowledged_request": "False",
      "notify_on_completed_request": "False",
      "notify_on_dispatched_request": "False",
      "notify_on_failed_request": "False",
      "notify_on_new_request": "False",
      "number": "1-111-111-1111"
    }
  ],
  "is_commercial": "False",
  "name": "DEMOCO001",
  "note": "Service Location of DemoCo Inc.",
  "parent_id": "1",
  "reference_number": "Ref#100",
  "renewal_date": "2100-02-18T15:53:55.851Z",
  "sales_rep": "John Doe",
  "suspension_id": "1"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`body`|body|[CreateCustomerProfileModel](#schemacreatecustomerprofilemodel)|true||

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "address_id": "1",
      "country": "US",
      "is_billing": "True",
      "is_physical": "True",
      "is_shipping": "False",
      "latitude": "46.881398",
      "line_1": "643 Summer Breeze",
      "line_2": "Suite 34",
      "line_3": "2nd Door on Left",
      "line_4": "Blue slot",
      "locality": "Sequim",
      "longitude": "-121.276566",
      "postcode": "98382",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "contact_id": "1",
      "email": "develop@crosoftware.com",
      "fax": "(360) 716-1968",
      "name": "John Doe",
      "notify_on_acknowledged_request": "False",
      "notify_on_completed_request": "False",
      "notify_on_dispatched_request": "False",
      "notify_on_failed_request": "False",
      "notify_on_new_request": "False",
      "number": "1-111-111-1111"
    }
  ],
  "customer_id": "1",
  "locations": [
    {
      "created_on": "2019-02-12T01:32:45.980000",
      "is_active": "True",
      "is_commercial": "True",
      "last_edited": "2019-02-12T01:32:45.990000",
      "location_id": "1",
      "note": "An example note",
      "reference_number": "REF#A1631",
      "renewal_date": "2019-10-02T00:00:00",
      "sales_rep": "John Doe",
      "suspension_id": "1"
    }
  ],
  "name": "Sequim Waste Inc.",
  "parent_id": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerModel](#schemacustomermodel)|New customer profile for customer at given location.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdget_customer"></a>

Customer profile.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "address_id": "1",
      "country": "US",
      "is_billing": "True",
      "is_physical": "True",
      "is_shipping": "False",
      "latitude": "46.881398",
      "line_1": "643 Summer Breeze",
      "line_2": "Suite 34",
      "line_3": "2nd Door on Left",
      "line_4": "Blue slot",
      "locality": "Sequim",
      "longitude": "-121.276566",
      "postcode": "98382",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "contact_id": "1",
      "email": "develop@crosoftware.com",
      "fax": "(360) 716-1968",
      "name": "John Doe",
      "notify_on_acknowledged_request": "False",
      "notify_on_completed_request": "False",
      "notify_on_dispatched_request": "False",
      "notify_on_failed_request": "False",
      "notify_on_new_request": "False",
      "number": "1-111-111-1111"
    }
  ],
  "customer_id": "1",
  "locations": [
    {
      "created_on": "2019-02-12T01:32:45.980000",
      "is_active": "True",
      "is_commercial": "True",
      "last_edited": "2019-02-12T01:32:45.990000",
      "location_id": "1",
      "note": "An example note",
      "reference_number": "REF#A1631",
      "renewal_date": "2019-10-02T00:00:00",
      "sales_rep": "John Doe",
      "suspension_id": "1"
    }
  ],
  "name": "Sequim Waste Inc.",
  "parent_id": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerModel](#schemacustomermodel)|Customer Profile|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdget_customer_for_location"></a>

Get customer for location.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "address_id": "1",
      "country": "US",
      "is_billing": "True",
      "is_physical": "True",
      "is_shipping": "False",
      "latitude": "46.881398",
      "line_1": "643 Summer Breeze",
      "line_2": "Suite 34",
      "line_3": "2nd Door on Left",
      "line_4": "Blue slot",
      "locality": "Sequim",
      "longitude": "-121.276566",
      "postcode": "98382",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "contact_id": "1",
      "email": "develop@crosoftware.com",
      "fax": "(360) 716-1968",
      "name": "John Doe",
      "notify_on_acknowledged_request": "False",
      "notify_on_completed_request": "False",
      "notify_on_dispatched_request": "False",
      "notify_on_failed_request": "False",
      "notify_on_new_request": "False",
      "number": "1-111-111-1111"
    }
  ],
  "created_on": "2019-03-08T16:40:37.647000",
  "customer_id": "2",
  "is_active": "True",
  "is_commercial": "False",
  "last_edited": "2019-03-08T16:40:37.647000",
  "name": "Jane Smith",
  "note": "An example note",
  "parent_id": "1",
  "reference_number": "1234",
  "renewal_date": "2100-03-08T16:40:37.647000",
  "sales_rep": "Jane Doe",
  "suspension_id": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationModel](#schemacustomerlocationmodel)|Customer profile for customer at given location.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdlist_customers"></a>

List of customers.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

> Example responses

> 200 Response

```json
{
  "current_limit": "100",
  "current_page": "1",
  "results": [
    {
      "addresses": [
        {
          "address_id": "1",
          "country": "US",
          "is_billing": "True",
          "is_physical": "True",
          "is_shipping": "False",
          "latitude": "46.881398",
          "line_1": "643 Summer Breeze",
          "line_2": "Suite 34",
          "line_3": "2nd Door on Left",
          "line_4": "Blue slot",
          "locality": "Sequim",
          "longitude": "-121.276566",
          "postcode": "98382",
          "region": "WA"
        }
      ],
      "contacts": [
        {
          "contact_id": "1",
          "email": "develop@crosoftware.com",
          "fax": "(360) 716-1968",
          "name": "John Doe",
          "notify_on_acknowledged_request": "False",
          "notify_on_completed_request": "False",
          "notify_on_dispatched_request": "False",
          "notify_on_failed_request": "False",
          "notify_on_new_request": "False",
          "number": "1-111-111-1111"
        }
      ],
      "customer_id": "1",
      "locations": [
        {
          "created_on": "2019-02-12T01:32:45.980000",
          "is_active": "True",
          "is_commercial": "True",
          "last_edited": "2019-02-12T01:32:45.990000",
          "location_id": "1",
          "note": "An example note",
          "reference_number": "REF#A1631",
          "renewal_date": "2019-10-02T00:00:00",
          "sales_rep": "John Doe",
          "suspension_id": "1"
        }
      ],
      "name": "Sequim Waste Inc.",
      "parent_id": "1"
    }
  ],
  "total_count": "100",
  "total_pages": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerListModel](#schemacustomerlistmodel)|List|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdlist_customers_for_location"></a>

List customers for location.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

> Example responses

> 200 Response

```json
{
  "current_limit": "100",
  "current_page": "1",
  "results": [
    {
      "addresses": [
        {
          "address_id": "1",
          "country": "US",
          "is_billing": "True",
          "is_physical": "True",
          "is_shipping": "False",
          "latitude": "46.881398",
          "line_1": "643 Summer Breeze",
          "line_2": "Suite 34",
          "line_3": "2nd Door on Left",
          "line_4": "Blue slot",
          "locality": "Sequim",
          "longitude": "-121.276566",
          "postcode": "98382",
          "region": "WA"
        }
      ],
      "contacts": [
        {
          "contact_id": "1",
          "email": "develop@crosoftware.com",
          "fax": "(360) 716-1968",
          "name": "John Doe",
          "notify_on_acknowledged_request": "False",
          "notify_on_completed_request": "False",
          "notify_on_dispatched_request": "False",
          "notify_on_failed_request": "False",
          "notify_on_new_request": "False",
          "number": "1-111-111-1111"
        }
      ],
      "created_on": "2019-03-08T16:40:37.647000",
      "customer_id": "2",
      "is_active": "True",
      "is_commercial": "False",
      "last_edited": "2019-03-08T16:40:37.647000",
      "name": "Jane Smith",
      "note": "An example note",
      "parent_id": "1",
      "reference_number": "1234",
      "renewal_date": "2100-03-08T16:40:37.647000",
      "sales_rep": "Jane Doe",
      "suspension_id": "1"
    }
  ],
  "total_count": "100",
  "total_pages": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationListModel](#schemacustomerlocationlistmodel)|Paged result sef of customers for location.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdupdate_customer"></a>

Update customer.

> Body parameter

```json
{
  "name": "Sequim Waste Inc.",
  "parent_id": "1"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`body`|body|[UpdateCustomerProfileModel](#schemaupdatecustomerprofilemodel)|true||

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "address_id": "1",
      "country": "US",
      "is_billing": "True",
      "is_physical": "True",
      "is_shipping": "False",
      "latitude": "46.881398",
      "line_1": "643 Summer Breeze",
      "line_2": "Suite 34",
      "line_3": "2nd Door on Left",
      "line_4": "Blue slot",
      "locality": "Sequim",
      "longitude": "-121.276566",
      "postcode": "98382",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "contact_id": "1",
      "email": "develop@crosoftware.com",
      "fax": "(360) 716-1968",
      "name": "John Doe",
      "notify_on_acknowledged_request": "False",
      "notify_on_completed_request": "False",
      "notify_on_dispatched_request": "False",
      "notify_on_failed_request": "False",
      "notify_on_new_request": "False",
      "number": "1-111-111-1111"
    }
  ],
  "customer_id": "1",
  "locations": [
    {
      "created_on": "2019-02-12T01:32:45.980000",
      "is_active": "True",
      "is_commercial": "True",
      "last_edited": "2019-02-12T01:32:45.990000",
      "location_id": "1",
      "note": "An example note",
      "reference_number": "REF#A1631",
      "renewal_date": "2019-10-02T00:00:00",
      "sales_rep": "John Doe",
      "suspension_id": "1"
    }
  ],
  "name": "Sequim Waste Inc.",
  "parent_id": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerModel](#schemacustomermodel)|Updated customer profile.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdget_driver"></a>

Get driver info.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`driver_id`|path|integer(int64)|true|Driver identifier (internal).|

> Example responses

> 200 Response

```json
{
  "address": "1234 Cro St",
  "can_convert_to_group": "False",
  "can_create_requests": "False",
  "can_edit_requests": "False",
  "can_reposition_asset": "False",
  "city": "Sequim",
  "disable_shift_tracking": "False",
  "email": "john@crosoftware.net",
  "id": "2",
  "license_number": "123ABC",
  "location_id": "1",
  "name": "John Denver",
  "phone_number": "(360) 718-1234",
  "state": "WA",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "zip": "98368"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DriverModel](#schemadrivermodel)|Driver profile.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdlist_drivers_for_location"></a>

List drivers for location.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

> Example responses

> 200 Response

```json
{
  "current_limit": "100",
  "current_page": "1",
  "results": [
    {
      "address": "1234 Cro St",
      "can_convert_to_group": "False",
      "can_create_requests": "False",
      "can_edit_requests": "False",
      "can_reposition_asset": "False",
      "city": "Sequim",
      "disable_shift_tracking": "False",
      "email": "john@crosoftware.net",
      "id": "2",
      "license_number": "123ABC",
      "location_id": "1",
      "name": "John Denver",
      "phone_number": "(360) 718-1234",
      "state": "WA",
      "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "zip": "98368"
    }
  ],
  "total_count": "1",
  "total_pages": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DriverListModel](#schemadriverlistmodel)|List of drivers for location.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdlog_gps_event"></a>

Log GPS event.

> Body parameter

```json
{
  "location": {
    "coords": {
      "heading": "184.57",
      "latitude": "37.33517518",
      "longitude": "-122.03255055",
      "speed": "2.41"
    },
    "timestamp": "2019-02-07T00:12:19.354Z"
  }
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`body`|body|[GpsEventProfileModel](#schemagpseventprofilemodel)|true||

> Example responses

> 200 Response

```json
{
  "bearing": "184.57",
  "created_on": "2019-02-07T00:12:19.354000",
  "device_name": "N/A",
  "driver_id": "2",
  "id": "3",
  "latitude": "37.33517518",
  "longitude": "-122.03255055",
  "truck_id": "string",
  "velocity": "2.41"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[GpsEventModel](#schemagpseventmodel)|GPS event profile.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

## Haulers

### Create 3rd Party Hauler

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
          byte[] json = client.UploadValues(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/haulers \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

$.ajax({
  url: 'https://api.crosoftware.net/haulers',
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
  'Accept' => 'application/json'
}

result = RestClient.post 'https://api.crosoftware.net/haulers',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json'
}

r = requests.post('https://api.crosoftware.net/haulers', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/haulers");
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

<a id="opIdcreate_third_party_hauler"></a>

Create 3rd Party hauler profile.

<aside class="success">
This operation does not require authentication
</aside>

> Body parameter

```json
{
  "company_name": "An Example Company, Inc.",
  "password": "password",
  "recaptcha": "somecaptcha",
  "username": "company_user"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`body`|body|[CreateThirdPartyHaulerProfileModel](#schemacreatethirdpartyhaulerprofilemodel)|true||

> Example responses

> 200 Response

```json
{
  "id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "name": "SMS594"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerModel](#schemathirdpartyhaulermodel)|Third party hauler profile.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          String url = "https://api.crosoftware.net/halers/{hauler_id}/connections";

          // Headers
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          // Parameters
          NameValueCollection parameters = new NameValueCollection();
          parameters.Add("tenant_code", "CROSCRAP+1");
          
          byte[] json = client.UploadValues(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/halers/{hauler_id}/connections?tenant_code=CROSCRAP%2B1 \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/halers/{hauler_id}/connections',
  method: 'post',
  data: '?tenant_code=CROSCRAP%2B1',
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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/halers/{hauler_id}/connections',
  params: {
  'tenant_code' => 'string(tenantCode)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
}

r = requests.post('https://api.crosoftware.net/halers/{hauler_id}/connections', params={
  'tenant_code': 'CROSCRAP+1'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/halers/{hauler_id}/connections?tenant_code=CROSCRAP%2B1");
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

`POST /halers/{hauler_id}/connections`

<a id="opIdcreate_hauler_connection"></a>

Create hauler connection.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`hauler_id`|path|[UUID](#schemauuid)|true|Hauler identifier.|
|`tenant_code`|query|string(tenantCode)|true|&lt;YardCode&gt;+&lt;LocationId&gt;. The YardCode is an identifier assigned at account creation.|

> Example responses

> 200 Response

```json
{
  "approved_by": "1",
  "approved_on": "2018-10-31T11:24:53.153000",
  "denied_on": "string",
  "is_approved": "True",
  "location_id": "1",
  "provider_email": "test_hauler@crosoftware.net",
  "provider_id": "2",
  "provider_name": "CRO Scrap - Sequim",
  "provider_phone": "na",
  "requested_on": "2018-10-31T18:24:06.723000"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[HaulerConnectionModel](#schemahaulerconnectionmodel)|Hauler with given UUID.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          String url = "https://api.crosoftware.net/halers/{hauler_id}";

          // Headers
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/halers/{hauler_id} \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/halers/{hauler_id}',
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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/halers/{hauler_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
}

r = requests.get('https://api.crosoftware.net/halers/{hauler_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/halers/{hauler_id}");
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

`GET /halers/{hauler_id}`

<a id="opIdget_hauler"></a>

Hauler profile.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`hauler_id`|path|[UUID](#schemauuid)|true|Hauler identifier.|

> Example responses

> 200 Response

```json
{
  "id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "name": "SMS594"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerModel](#schemathirdpartyhaulermodel)|Hauler profile.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

### List 3rd Party Haulers

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdlist_haulers"></a>

List third party haulers for tenant.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

> Example responses

> 200 Response

```json
{
  "current_limit": "100",
  "current_page": "1",
  "results": [
    {
      "id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "name": "SMS594"
    }
  ],
  "total_count": "1",
  "total_pages": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerListModel](#schemathirdpartyhaulerlistmodel)|List of third party haulers for tenant.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          String url = "https://api.crosoftware.net/halers/{hauler_id}/connections";

          // Headers
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/halers/{hauler_id}/connections \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/halers/{hauler_id}/connections',
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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/halers/{hauler_id}/connections',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
}

r = requests.get('https://api.crosoftware.net/halers/{hauler_id}/connections', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/halers/{hauler_id}/connections");
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

`GET /halers/{hauler_id}/connections`

<a id="opIdlist_hauler_connections"></a>

List of 3rd party haulers.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`hauler_id`|path|[UUID](#schemauuid)|true|Hauler identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

> Example responses

> 200 Response

```json
{
  "approved_by": "1",
  "approved_on": "2018-10-31T11:24:53.153000",
  "denied_on": "string",
  "is_approved": "True",
  "location_id": "1",
  "provider_email": "test_hauler@crosoftware.net",
  "provider_id": "2",
  "provider_name": "CRO Scrap - Sequim",
  "provider_phone": "na",
  "requested_on": "2018-10-31T18:24:06.723000"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[HaulerConnectionModel](#schemahaulerconnectionmodel)|List|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          // Parameters
          NameValueCollection parameters = new NameValueCollection();
          parameters.Add("truck_id", "0");
          
          byte[] json = client.UploadValues(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/locations/{location_id}/jobs/{job_id}?truck_id=0 \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/jobs/{job_id}',
  method: 'patch',
  data: '?truck_id=0',
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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/locations/{location_id}/jobs/{job_id}',
  params: {
  'truck_id' => 'integer(int64)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
}

r = requests.patch('https://api.crosoftware.net/locations/{location_id}/jobs/{job_id}', params={
  'truck_id': '0'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/jobs/{job_id}?truck_id=0");
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

<a id="opIddispatch_job"></a>

Dispatch job.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`job_id`|path|integer(int64)|true|Job identifier (internal).|
|`truck_id`|query|integer(int64)|true|Truck identifier (internal).|
|`future_job_schedule_date`|query|[DateTime](#schemadatetime)|false|Future dispatch time for job.|

> Example responses

> 200 Response

```json
{
  "arrived_at_dest": "2018-11-18T19:54:55.327000",
  "arrived_on": "2018-11-18T19:54:55.327000",
  "asset_dropped": "1",
  "asset_id": "1",
  "asset_quantity": "1",
  "asset_type_id": "1",
  "completed_by": "1",
  "completed_by_driver": "False",
  "completed_on": "2018-11-18T19:54:55.327000",
  "confirmed_on": "2018-11-18T19:54:55.327000",
  "created_by_id": "1",
  "created_with_portal": "False",
  "customer_id": "9",
  "customer_notes": "Some customer notes",
  "departed_on": "2018-11-18T19:54:55.327000",
  "desired_asset_desc": "An asset description.",
  "dispatch_priority": "H",
  "dispatched_by_route": "1",
  "dispatched_on": "2018-11-18T19:54:55.327000",
  "dispatcher_notes": "Some dispatcher notes",
  "do_confirm": "False",
  "driver_notes": "Some driver notes",
  "dropped_number": "Unused/deprecated field",
  "dump_location_id": "1",
  "dumped_on": "2018-11-18T19:54:55.327000",
  "end_time": "2018-11-18T19:54:55.327000",
  "fail_reason": "Failure reason",
  "final_location_id": "1",
  "flags": "Job notes",
  "id": "1",
  "invoice_notes": "Some invoice notes",
  "is_completed": "False",
  "is_declined": "False",
  "is_deleted": "False",
  "is_failed": "False",
  "is_paid": true,
  "job_group_id": "1",
  "location_id": "1",
  "merged_with_route": "1",
  "original_schedule_date": "2018-10-31T11:34:13.690000",
  "pickup_date": "2018-10-31T11:34:13.690000",
  "priority": "-1",
  "reference_number": null,
  "removed_number": "string",
  "requested_on": "2018-10-31T11:33:52.920000",
  "require_image": "False",
  "require_material": "False",
  "require_signature": "False",
  "require_weights": "False",
  "schedule_date": "2018-10-31T00:00:00",
  "start_location_id": "1",
  "start_time": "2018-10-31T11:33:52.920000",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "times_failed": "0",
  "times_rolled_over": "0",
  "truck_id": "1",
  "type": "D",
  "weighed_on": "2018-10-31T11:33:52.920000"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[UpdatedJobModel](#schemaupdatedjobmodel)|UpdatedJobModel|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdget_job"></a>

Get specified job.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`job_id`|path|integer(int64)|true|Job identifier (internal).|

> Example responses

> 200 Response

```json
{
  "arrived_at_dest": "2018-11-18T19:54:55.327000",
  "arrived_on": "2018-11-18T19:54:55.327000",
  "asset": {
    "asset_type": {
      "deleted": "False",
      "id": "1",
      "is_default": "False",
      "location_id": "1",
      "name": "10 yrd",
      "quantity": "2",
      "require_numbers": "True",
      "weight": "3245"
    },
    "asset_type_id": "1",
    "cluster": "1",
    "customer_id": "1",
    "description": "A description",
    "dispatched_on": "2018-10-31T11:34:13.690000",
    "id": "1",
    "is_returned": "False",
    "last_activity_on": "2018-10-31T11:34:13.690000",
    "last_rental_invoice_on": "2018-10-31T11:34:13.690000",
    "latitude": "54.235",
    "location": {
      "id": "1",
      "is_active": "True",
      "name": "Sequim"
    },
    "location_id": "1",
    "longitude": "127.123",
    "number": "REF100",
    "quantity": "1",
    "returned_on": "2018-10-31T11:34:13.690000"
  },
  "asset_dropped": "1",
  "asset_id": "1",
  "asset_quantity": "1",
  "asset_type": {
    "deleted": "False",
    "id": "1",
    "is_default": "False",
    "location_id": "1",
    "name": "10 yrd",
    "quantity": "2",
    "require_numbers": "True",
    "weight": "3245"
  },
  "asset_type_id": "1",
  "completed_by": "1",
  "completed_by_driver": "False",
  "completed_on": "2018-11-18T19:54:55.327000",
  "confirmed_on": "2018-11-18T19:54:55.327000",
  "created_by_id": "1",
  "created_with_portal": "False",
  "customer": {
    "addresses": [
      {
        "address_id": "1",
        "country": "US",
        "is_billing": "True",
        "is_physical": "True",
        "is_shipping": "False",
        "latitude": "46.881398",
        "line_1": "643 Summer Breeze",
        "line_2": "Suite 34",
        "line_3": "2nd Door on Left",
        "line_4": "Blue slot",
        "locality": "Sequim",
        "longitude": "-121.276566",
        "postcode": "98382",
        "region": "WA"
      }
    ],
    "contacts": [
      {
        "contact_id": "1",
        "email": "develop@crosoftware.com",
        "fax": "(360) 716-1968",
        "name": "John Doe",
        "notify_on_acknowledged_request": "False",
        "notify_on_completed_request": "False",
        "notify_on_dispatched_request": "False",
        "notify_on_failed_request": "False",
        "notify_on_new_request": "False",
        "number": "1-111-111-1111"
      }
    ],
    "customer_id": "1",
    "locations": [
      {
        "created_on": "2019-02-12T01:32:45.980000",
        "is_active": "True",
        "is_commercial": "True",
        "last_edited": "2019-02-12T01:32:45.990000",
        "location_id": "1",
        "note": "An example note",
        "reference_number": "REF#A1631",
        "renewal_date": "2019-10-02T00:00:00",
        "sales_rep": "John Doe",
        "suspension_id": "1"
      }
    ],
    "name": "Sequim Waste Inc.",
    "parent_id": "1"
  },
  "customer_id": "9",
  "customer_notes": "Some customer notes",
  "departed_on": "2018-11-18T19:54:55.327000",
  "desired_asset_desc": "An asset description.",
  "dispatch_priority": "H",
  "dispatched_by_route": "1",
  "dispatched_on": "2018-11-18T19:54:55.327000",
  "dispatcher_notes": "Some dispatcher notes",
  "do_confirm": "False",
  "driver_notes": "Some driver notes",
  "dropped_number": "Unused/deprecated field",
  "dump_location": {
    "address": "123 Sequim Ave.",
    "city": "Sequim",
    "contact_email": "support@crosoftware.net",
    "contact_name": "John Doe",
    "contact_phone": "(706) 360-7109",
    "id": "1",
    "is_holding_yard": "True",
    "latitude": "128.123",
    "location": {
      "id": "1",
      "is_active": "True",
      "name": "Sequim"
    },
    "location_id": "1",
    "longitude": "54.234",
    "name": "A Destination",
    "state": "Washington",
    "zip": "98368"
  },
  "dump_location_id": "1",
  "dumped_on": "2018-11-18T19:54:55.327000",
  "end_time": "2018-11-18T19:54:55.327000",
  "fail_reason": "Failure reason",
  "final_location": {
    "address": "123 Sequim Ave.",
    "city": "Sequim",
    "contact_email": "support@crosoftware.net",
    "contact_name": "John Doe",
    "contact_phone": "(706) 360-7109",
    "id": "1",
    "is_holding_yard": "True",
    "latitude": "128.123",
    "location": {
      "id": "1",
      "is_active": "True",
      "name": "Sequim"
    },
    "location_id": "1",
    "longitude": "54.234",
    "name": "A Destination",
    "state": "Washington",
    "zip": "98368"
  },
  "final_location_id": "1",
  "flags": "Job notes",
  "id": "1",
  "invoice_notes": "Some invoice notes",
  "is_completed": "False",
  "is_declined": "False",
  "is_deleted": "False",
  "is_failed": "False",
  "is_paid": true,
  "job_group_id": "1",
  "location_id": "1",
  "merged_with_route": "1",
  "original_schedule_date": "2018-10-31T11:34:13.690000",
  "pickup_date": "2018-10-31T11:34:13.690000",
  "priority": "-1",
  "reference_number": null,
  "removed_number": "string",
  "requested_on": "2018-10-31T11:33:52.920000",
  "require_image": "False",
  "require_material": "False",
  "require_signature": "False",
  "require_weights": "False",
  "schedule_date": "2018-10-31T00:00:00",
  "start_location": {
    "address": "123 Sequim Ave.",
    "city": "Sequim",
    "contact_email": "support@crosoftware.net",
    "contact_name": "John Doe",
    "contact_phone": "(706) 360-7109",
    "id": "1",
    "is_holding_yard": "True",
    "latitude": "128.123",
    "location": {
      "id": "1",
      "is_active": "True",
      "name": "Sequim"
    },
    "location_id": "1",
    "longitude": "54.234",
    "name": "A Destination",
    "state": "Washington",
    "zip": "98368"
  },
  "start_location_id": "1",
  "start_time": "2018-10-31T11:33:52.920000",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "times_failed": "0",
  "times_rolled_over": "0",
  "truck_id": "1",
  "type": "D",
  "weighed_on": "2018-10-31T11:33:52.920000"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[JobModel](#schemajobmodel)|JobModel|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

### List jobs

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id}/jobs \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/jobs',
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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}/jobs',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}/jobs', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/jobs");
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

<a id="opIdlist_jobs_for_location"></a>

List jobs for location.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|
|`schedule_gt`|query|[DateTime](#schemadatetime)|false|Filter jobs with scheduled dates ocurring after this date.|
|`schedule_lt`|query|[DateTime](#schemadatetime)|false|Filter jobs with scheduled dates ocurring before this date.|
|`completed`|query|[Boolean](#schemaboolean)|false|True: return completed jobs. False: return jobs not marked completed. Unspecified: return jobs independent of failed status.|
|`failed`|query|[Boolean](#schemaboolean)|false|True: return failed jobs. False: return jobs not marked failed. Unspecified: return jobs independent of failed status.|
|`driver_id`|query|integer(int64)|false|Specified: return jobs assignable to driver. Unspecified: do not filter jobs by driver.|
|`truck_id`|query|integer(int64)|false|Specified: return jobs assigned to given truck. Unspecified: do not filter jobs by truck.|

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "arrived_at_dest": "2018-11-18T19:54:55.327000",
      "arrived_on": "2018-11-18T19:54:55.327000",
      "asset": {
        "asset_type": {
          "deleted": "False",
          "id": "1",
          "is_default": "False",
          "location_id": "1",
          "name": "10 yrd",
          "quantity": "2",
          "require_numbers": "True",
          "weight": "3245"
        },
        "asset_type_id": "1",
        "cluster": "1",
        "customer_id": "1",
        "description": "A description",
        "dispatched_on": "2018-10-31T11:34:13.690000",
        "id": "1",
        "is_returned": "False",
        "last_activity_on": "2018-10-31T11:34:13.690000",
        "last_rental_invoice_on": "2018-10-31T11:34:13.690000",
        "latitude": "54.235",
        "location": {
          "id": "1",
          "is_active": "True",
          "name": "Sequim"
        },
        "location_id": "1",
        "longitude": "127.123",
        "number": "REF100",
        "quantity": "1",
        "returned_on": "2018-10-31T11:34:13.690000"
      },
      "asset_dropped": "1",
      "asset_id": "1",
      "asset_quantity": "1",
      "asset_type": {
        "deleted": "False",
        "id": "1",
        "is_default": "False",
        "location_id": "1",
        "name": "10 yrd",
        "quantity": "2",
        "require_numbers": "True",
        "weight": "3245"
      },
      "asset_type_id": "1",
      "completed_by": "1",
      "completed_by_driver": "False",
      "completed_on": "2018-11-18T19:54:55.327000",
      "confirmed_on": "2018-11-18T19:54:55.327000",
      "created_by_id": "1",
      "created_with_portal": "False",
      "customer": {
        "addresses": [
          {
            "address_id": "1",
            "country": "US",
            "is_billing": "True",
            "is_physical": "True",
            "is_shipping": "False",
            "latitude": "46.881398",
            "line_1": "643 Summer Breeze",
            "line_2": "Suite 34",
            "line_3": "2nd Door on Left",
            "line_4": "Blue slot",
            "locality": "Sequim",
            "longitude": "-121.276566",
            "postcode": "98382",
            "region": "WA"
          }
        ],
        "contacts": [
          {
            "contact_id": "1",
            "email": "develop@crosoftware.com",
            "fax": "(360) 716-1968",
            "name": "John Doe",
            "notify_on_acknowledged_request": "False",
            "notify_on_completed_request": "False",
            "notify_on_dispatched_request": "False",
            "notify_on_failed_request": "False",
            "notify_on_new_request": "False",
            "number": "1-111-111-1111"
          }
        ],
        "customer_id": "1",
        "locations": [
          {
            "created_on": "2019-02-12T01:32:45.980000",
            "is_active": "True",
            "is_commercial": "True",
            "last_edited": "2019-02-12T01:32:45.990000",
            "location_id": "1",
            "note": "An example note",
            "reference_number": "REF#A1631",
            "renewal_date": "2019-10-02T00:00:00",
            "sales_rep": "John Doe",
            "suspension_id": "1"
          }
        ],
        "name": "Sequim Waste Inc.",
        "parent_id": "1"
      },
      "customer_id": "9",
      "customer_notes": "Some customer notes",
      "departed_on": "2018-11-18T19:54:55.327000",
      "desired_asset_desc": "An asset description.",
      "dispatch_priority": "H",
      "dispatched_by_route": "1",
      "dispatched_on": "2018-11-18T19:54:55.327000",
      "dispatcher_notes": "Some dispatcher notes",
      "do_confirm": "False",
      "driver_notes": "Some driver notes",
      "dropped_number": "Unused/deprecated field",
      "dump_location": {
        "address": "123 Sequim Ave.",
        "city": "Sequim",
        "contact_email": "support@crosoftware.net",
        "contact_name": "John Doe",
        "contact_phone": "(706) 360-7109",
        "id": "1",
        "is_holding_yard": "True",
        "latitude": "128.123",
        "location": {
          "id": "1",
          "is_active": "True",
          "name": "Sequim"
        },
        "location_id": "1",
        "longitude": "54.234",
        "name": "A Destination",
        "state": "Washington",
        "zip": "98368"
      },
      "dump_location_id": "1",
      "dumped_on": "2018-11-18T19:54:55.327000",
      "end_time": "2018-11-18T19:54:55.327000",
      "fail_reason": "Failure reason",
      "final_location": {
        "address": "123 Sequim Ave.",
        "city": "Sequim",
        "contact_email": "support@crosoftware.net",
        "contact_name": "John Doe",
        "contact_phone": "(706) 360-7109",
        "id": "1",
        "is_holding_yard": "True",
        "latitude": "128.123",
        "location": {
          "id": "1",
          "is_active": "True",
          "name": "Sequim"
        },
        "location_id": "1",
        "longitude": "54.234",
        "name": "A Destination",
        "state": "Washington",
        "zip": "98368"
      },
      "final_location_id": "1",
      "flags": "Job notes",
      "id": "1",
      "invoice_notes": "Some invoice notes",
      "is_completed": "False",
      "is_declined": "False",
      "is_deleted": "False",
      "is_failed": "False",
      "is_paid": true,
      "job_group_id": "1",
      "location_id": "1",
      "merged_with_route": "1",
      "original_schedule_date": "2018-10-31T11:34:13.690000",
      "pickup_date": "2018-10-31T11:34:13.690000",
      "priority": "-1",
      "reference_number": null,
      "removed_number": "string",
      "requested_on": "2018-10-31T11:33:52.920000",
      "require_image": "False",
      "require_material": "False",
      "require_signature": "False",
      "require_weights": "False",
      "schedule_date": "2018-10-31T00:00:00",
      "start_location": {
        "address": "123 Sequim Ave.",
        "city": "Sequim",
        "contact_email": "support@crosoftware.net",
        "contact_name": "John Doe",
        "contact_phone": "(706) 360-7109",
        "id": "1",
        "is_holding_yard": "True",
        "latitude": "128.123",
        "location": {
          "id": "1",
          "is_active": "True",
          "name": "Sequim"
        },
        "location_id": "1",
        "longitude": "54.234",
        "name": "A Destination",
        "state": "Washington",
        "zip": "98368"
      },
      "start_location_id": "1",
      "start_time": "2018-10-31T11:33:52.920000",
      "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "times_failed": "0",
      "times_rolled_over": "0",
      "truck_id": "1",
      "type": "D",
      "weighed_on": "2018-10-31T11:33:52.920000"
    }
  ],
  "total_count": "1",
  "total_pages": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[JobListModel](#schemajoblistmodel)|List of jobs for location.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdget_location"></a>

Get info for specified location.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|

> Example responses

> 200 Response

```json
{
  "id": "1",
  "is_active": "True",
  "name": "Sequim"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[LocationModel](#schemalocationmodel)|Location info.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdlist_locations"></a>

List locations for tenant.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

> Example responses

> 200 Response

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "id": "1",
      "is_active": "True",
      "name": "Sequim"
    }
  ],
  "total_count": "1",
  "total_pages": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[LocationListModel](#schemalocationlistmodel)|List of locations|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdlist_tenants"></a>

List tenants for this user.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

> Example responses

> 200 Response

```json
{
  "current_limit": "100",
  "current_page": "1",
  "results": [
    {
      "address": "123 some st",
      "city": "Sequim",
      "code": "CROSCRAP",
      "created_on": "2019-02-12T01:32:45.640000",
      "email": "test_admin@crosoftware.net",
      "id": "1",
      "is_active": "True",
      "name": "CRO Scrap",
      "phone": "1234567890",
      "state": "WA",
      "truck_limit": "string",
      "zip": "98360"
    }
  ],
  "total_count": "1",
  "total_pages": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TenantListModel](#schematenantlistmodel)|Paged list response of tenants.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdget_truck"></a>

Get truck info.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`truck_id`|path|integer(int64)|true|Truck identifier (internal).|

> Example responses

> 200 Response

```json
{
  "driver_id": "1",
  "id": "2",
  "location_id": "1",
  "name": "ZachTruck",
  "notes": "Sequim",
  "out_of_service": "False",
  "require_odometer": "False",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "type": "AwesomeTRUCK Rolloff",
  "weight": "18678"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|string|Truck info.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
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
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
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
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
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

<a id="opIdlist_trucks_for_location"></a>

List trucks for location.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

> Example responses

> 200 Response

```json
{
  "current_limit": "100",
  "current_page": "1",
  "results": [
    {
      "driver_id": "1",
      "id": "2",
      "location_id": "1",
      "name": "ZachTruck",
      "notes": "Sequim",
      "out_of_service": "False",
      "require_odometer": "False",
      "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "type": "AwesomeTRUCK Rolloff",
      "weight": "18678"
    }
  ],
  "total_count": "1",
  "total_pages": "1"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TruckListModel](#schematrucklistmodel)|List of trucks for location.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

### Set Driver

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
          client.Headers.Add("Authorization", "bearer <access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          // Parameters
          NameValueCollection parameters = new NameValueCollection();
          parameters.Add("driver_id", "0");
          
          byte[] json = client.UploadValues(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}?driver_id=0 \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}',
  method: 'patch',
  data: '?driver_id=0',
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
  'Authorization' => 'bearer <access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}',
  params: {
  'driver_id' => 'integer(int64)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <access-token>',
  'X-TENANT-ID': '1'
}

r = requests.patch('https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}', params={
  'driver_id': '0'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}?driver_id=0");
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

<a id="opIdset_truck_driver"></a>

Set driver for truck.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`truck_id`|path|integer(int64)|true|Truck identifier (internal).|
|`driver_id`|query|integer(int64)|true|Location identifier (internal).|

> Example responses

> 200 Response

```json
{
  "driver_id": "1",
  "id": "2",
  "location_id": "1",
  "name": "ZachTruck",
  "notes": "Sequim",
  "out_of_service": "False",
  "require_odometer": "False",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "type": "AwesomeTRUCK Rolloff",
  "weight": "18678"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TruckModel](#schematruckmodel)|Updated truck profile.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found.|

# Schemas

<h2 id="tocSdatetime">DateTime</h2>

```json
"2018-10-31T11:32:38.390000"

```

<a id="schemadatetime"></a>

*YYYY-MM-DDThh:mm:ss.ssssss
ISO 8601 DateTime Format (GMT)
*

|Name|Type|Description|
|---|---|---|
|`-`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT)|

<h2 id="tocSuuid">UUID</h2>

```json
"b8d78911-e1fa-4adc-9b22-3b48dda30522"

```

<a id="schemauuid"></a>

*UUID
*

|Name|Type|Description|
|---|---|---|
|`-`|string(uuid)|UUID|

<h2 id="tocSboolean">Boolean</h2>

```json
"string"

```

<a id="schemaboolean"></a>

*May be case insensitive True|False or 1|0.
*

|Name|Type|Description|
|---|---|---|
|`-`|string(boolean)|May be case insensitive True|False or 1|0.|

<h2 id="tocSaddcustomeraddressprofilemodel">AddCustomerAddressProfileModel</h2>

```json
{
  "country": "US",
  "is_billing": "True",
  "is_shipping": "False",
  "latitude": "46.881398",
  "line_1": "643 Summer Breeze",
  "line_2": "Suite 34",
  "line_3": "2nd Door on Left",
  "line_4": "Blue slot",
  "locality": "Sequim",
  "longitude": "-121.276566",
  "postcode": "98382",
  "region": "WA"
}

```

<a id="schemaaddcustomeraddressprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`country`|string|-|
|`is_billing`|boolean|-|
|`is_shipping`|boolean|-|
|`latitude`|number(float)|-|
|`line_1`|string|-|
|`line_2`|string|-|
|`line_3`|string|-|
|`line_4`|string|-|
|`locality`|string|-|
|`longitude`|number(float)|-|
|`postcode`|integer(int64)|-|
|`region`|string|-|

<h2 id="tocSaddcustomercontactprofilemodel">AddCustomerContactProfileModel</h2>

```json
{
  "email": "develop@crosoftware.com",
  "fax": "(360) 716-1968",
  "name": "John Doe",
  "notify_on_acknowledged_request": "False",
  "notify_on_completed_request": "False",
  "notify_on_dispatched_request": "False",
  "notify_on_failed_request": "False",
  "notify_on_new_request": "False",
  "number": "1-111-111-1111"
}

```

<a id="schemaaddcustomercontactprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`email`|string|-|
|`fax`|string|-|
|`name`|string|-|
|`notify_on_acknowledged_request`|boolean|-|
|`notify_on_completed_request`|boolean|-|
|`notify_on_dispatched_request`|boolean|-|
|`notify_on_failed_request`|boolean|-|
|`notify_on_new_request`|boolean|-|
|`number`|string|-|

<h2 id="tocSaddcustomerlocationprofilemodel">AddCustomerLocationProfileModel</h2>

```json
{
  "is_commercial": "True",
  "note": "An example note",
  "reference_number": "R100-10C",
  "renewal_date": "2100-02-12T01:32:45.640000",
  "sales_rep": "John Smith",
  "suspension_id": "1"
}

```

<a id="schemaaddcustomerlocationprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`is_commercial`|boolean|-|
|`note`|string|-|
|`reference_number`|string|-|
|`renewal_date`|string(datetime)|-|
|`sales_rep`|string|-|
|`suspension_id`|integer(int64)|-|

<h2 id="tocSassetmodel">AssetModel</h2>

```json
{
  "asset_type": {
    "deleted": "False",
    "id": "1",
    "is_default": "False",
    "location_id": "1",
    "name": "10 yrd",
    "quantity": "2",
    "require_numbers": "True",
    "weight": "3245"
  },
  "asset_type_id": "1",
  "cluster": "1",
  "customer_id": "1",
  "description": "A description",
  "dispatched_on": "2018-10-31T11:34:13.690000",
  "id": "1",
  "is_returned": "False",
  "last_activity_on": "2018-10-31T11:34:13.690000",
  "last_rental_invoice_on": "2018-10-31T11:34:13.690000",
  "latitude": "54.235",
  "location": {
    "id": "1",
    "is_active": "True",
    "name": "Sequim"
  },
  "location_id": "1",
  "longitude": "127.123",
  "number": "REF100",
  "quantity": "1",
  "returned_on": "2018-10-31T11:34:13.690000"
}

```

<a id="schemaassetmodel"></a>

|Name|Type|Description|
|---|---|---|
|`asset_type`|[AssetTypeModel](#schemaassettypemodel)|-|
|`asset_type_id`|integer(int64)|-|
|`cluster`|integer(int64)|-|
|`customer_id`|integer(int64)|-|
|`description`|string|-|
|`dispatched_on`|string(datetime)|-|
|`id`|integer(int64)|-|
|`is_returned`|boolean|-|
|`last_activity_on`|string(datetime)|-|
|`last_rental_invoice_on`|string(datetime)|-|
|`latitude`|number(float)|-|
|`location`|[LocationModel](#schemalocationmodel)|-|
|`location_id`|integer(int64)|-|
|`longitude`|number(float)|-|
|`number`|string|-|
|`quantity`|integer(int64)|-|
|`returned_on`|string(datetime)|-|

<h2 id="tocSassettypemodel">AssetTypeModel</h2>

```json
{
  "deleted": "False",
  "id": "1",
  "is_default": "False",
  "location_id": "1",
  "name": "10 yrd",
  "quantity": "2",
  "require_numbers": "True",
  "weight": "3245"
}

```

<a id="schemaassettypemodel"></a>

|Name|Type|Description|
|---|---|---|
|`deleted`|boolean|-|
|`id`|integer(int64)|-|
|`is_default`|boolean|-|
|`location_id`|integer(int64)|-|
|`name`|string|-|
|`quantity`|integer(int64)|-|
|`require_numbers`|boolean|-|
|`weight`|integer(int64)|-|

<h2 id="tocScreatecustomerprofilemodel">CreateCustomerProfileModel</h2>

```json
{
  "addresses": [
    {
      "country": "US",
      "is_billing": "True",
      "is_shipping": "False",
      "latitude": "46.881398",
      "line_1": "643 Summer Breeze",
      "line_2": "Suite 34",
      "line_3": "2nd Door on Left",
      "line_4": "Blue slot",
      "locality": "Sequim",
      "longitude": "-121.276566",
      "postcode": "98382",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "email": "develop@crosoftware.com",
      "fax": "(360) 716-1968",
      "name": "John Doe",
      "notify_on_acknowledged_request": "False",
      "notify_on_completed_request": "False",
      "notify_on_dispatched_request": "False",
      "notify_on_failed_request": "False",
      "notify_on_new_request": "False",
      "number": "1-111-111-1111"
    }
  ],
  "is_commercial": "False",
  "name": "DEMOCO001",
  "note": "Service Location of DemoCo Inc.",
  "parent_id": "1",
  "reference_number": "Ref#100",
  "renewal_date": "2100-02-18T15:53:55.851Z",
  "sales_rep": "John Doe",
  "suspension_id": "1"
}

```

<a id="schemacreatecustomerprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`addresses`|array[[AddCustomerAddressProfileModel](#schemaaddcustomeraddressprofilemodel)]|-|
|`contacts`|array[[AddCustomerContactProfileModel](#schemaaddcustomercontactprofilemodel)]|-|
|`is_commercial`|boolean|-|
|`name`|string|-|
|`note`|string|-|
|`parent_id`|integer(int64)|-|
|`reference_number`|string|-|
|`renewal_date`|string(datetime)|-|
|`sales_rep`|string|-|
|`suspension_id`|integer(int64)|-|

<h2 id="tocScreatethirdpartyhaulerprofilemodel">CreateThirdPartyHaulerProfileModel</h2>

```json
{
  "company_name": "An Example Company, Inc.",
  "password": "password",
  "recaptcha": "somecaptcha",
  "username": "company_user"
}

```

<a id="schemacreatethirdpartyhaulerprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`company_name`|string|-|
|`password`|string(byte)|-|
|`recaptcha`|string|-|
|`username`|string|-|

<h2 id="tocScustomeraddresslistmodel">CustomerAddressListModel</h2>

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "address_id": "1",
      "country": "US",
      "is_billing": "True",
      "is_physical": "True",
      "is_shipping": "False",
      "latitude": "46.881398",
      "line_1": "643 Summer Breeze",
      "line_2": "Suite 34",
      "line_3": "2nd Door on Left",
      "line_4": "Blue slot",
      "locality": "Sequim",
      "longitude": "-121.276566",
      "postcode": "98382",
      "region": "WA"
    }
  ],
  "total_count": "1",
  "total_pages": "1"
}

```

<a id="schemacustomeraddresslistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|-|
|`current_page`|integer(int64)|-|
|`results`|array[[CustomerAddressModel](#schemacustomeraddressmodel)]|-|
|`total_count`|integer(int64)|-|
|`total_pages`|integer(int64)|-|

<h2 id="tocScustomeraddressmodel">CustomerAddressModel</h2>

```json
{
  "address_id": "1",
  "country": "US",
  "is_billing": "True",
  "is_physical": "True",
  "is_shipping": "False",
  "latitude": "46.881398",
  "line_1": "643 Summer Breeze",
  "line_2": "Suite 34",
  "line_3": "2nd Door on Left",
  "line_4": "Blue slot",
  "locality": "Sequim",
  "longitude": "-121.276566",
  "postcode": "98382",
  "region": "WA"
}

```

<a id="schemacustomeraddressmodel"></a>

|Name|Type|Description|
|---|---|---|
|`address_id`|integer(int64)|-|
|`country`|string|-|
|`is_billing`|boolean|-|
|`is_physical`|boolean|-|
|`is_shipping`|boolean|-|
|`latitude`|number(float)|-|
|`line_1`|string|-|
|`line_2`|string|-|
|`line_3`|string|-|
|`line_4`|string|-|
|`locality`|string|-|
|`longitude`|number(float)|-|
|`postcode`|integer(int64)|-|
|`region`|string|-|

<h2 id="tocScustomercontactlistmodel">CustomerContactListModel</h2>

```json
{
  "current_limit": "100",
  "current_page": "1",
  "results": [
    {
      "contact_id": "1",
      "email": "develop@crosoftware.com",
      "fax": "(360) 716-1968",
      "name": "John Doe",
      "notify_on_acknowledged_request": "False",
      "notify_on_completed_request": "False",
      "notify_on_dispatched_request": "False",
      "notify_on_failed_request": "False",
      "notify_on_new_request": "False",
      "number": "1-111-111-1111"
    }
  ],
  "total_count": "100",
  "total_pages": "1"
}

```

<a id="schemacustomercontactlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|-|
|`current_page`|integer(int64)|-|
|`results`|array[[CustomerContactModel](#schemacustomercontactmodel)]|-|
|`total_count`|integer(int64)|-|
|`total_pages`|integer(int64)|-|

<h2 id="tocScustomercontactmodel">CustomerContactModel</h2>

```json
{
  "contact_id": "1",
  "email": "develop@crosoftware.com",
  "fax": "(360) 716-1968",
  "name": "John Doe",
  "notify_on_acknowledged_request": "False",
  "notify_on_completed_request": "False",
  "notify_on_dispatched_request": "False",
  "notify_on_failed_request": "False",
  "notify_on_new_request": "False",
  "number": "1-111-111-1111"
}

```

<a id="schemacustomercontactmodel"></a>

|Name|Type|Description|
|---|---|---|
|`contact_id`|integer(int64)|-|
|`email`|string|-|
|`fax`|string|-|
|`name`|string|-|
|`notify_on_acknowledged_request`|boolean|-|
|`notify_on_completed_request`|boolean|-|
|`notify_on_dispatched_request`|boolean|-|
|`notify_on_failed_request`|boolean|-|
|`notify_on_new_request`|boolean|-|
|`number`|string|-|

<h2 id="tocScustomerlistmodel">CustomerListModel</h2>

```json
{
  "current_limit": "100",
  "current_page": "1",
  "results": [
    {
      "addresses": [
        {
          "address_id": "1",
          "country": "US",
          "is_billing": "True",
          "is_physical": "True",
          "is_shipping": "False",
          "latitude": "46.881398",
          "line_1": "643 Summer Breeze",
          "line_2": "Suite 34",
          "line_3": "2nd Door on Left",
          "line_4": "Blue slot",
          "locality": "Sequim",
          "longitude": "-121.276566",
          "postcode": "98382",
          "region": "WA"
        }
      ],
      "contacts": [
        {
          "contact_id": "1",
          "email": "develop@crosoftware.com",
          "fax": "(360) 716-1968",
          "name": "John Doe",
          "notify_on_acknowledged_request": "False",
          "notify_on_completed_request": "False",
          "notify_on_dispatched_request": "False",
          "notify_on_failed_request": "False",
          "notify_on_new_request": "False",
          "number": "1-111-111-1111"
        }
      ],
      "customer_id": "1",
      "locations": [
        {
          "created_on": "2019-02-12T01:32:45.980000",
          "is_active": "True",
          "is_commercial": "True",
          "last_edited": "2019-02-12T01:32:45.990000",
          "location_id": "1",
          "note": "An example note",
          "reference_number": "REF#A1631",
          "renewal_date": "2019-10-02T00:00:00",
          "sales_rep": "John Doe",
          "suspension_id": "1"
        }
      ],
      "name": "Sequim Waste Inc.",
      "parent_id": "1"
    }
  ],
  "total_count": "100",
  "total_pages": "1"
}

```

<a id="schemacustomerlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|-|
|`current_page`|integer(int64)|-|
|`results`|array[[CustomerModel](#schemacustomermodel)]|-|
|`total_count`|integer(int64)|-|
|`total_pages`|integer(int64)|-|

<h2 id="tocScustomerlocationlistmodel">CustomerLocationListModel</h2>

```json
{
  "current_limit": "100",
  "current_page": "1",
  "results": [
    {
      "addresses": [
        {
          "address_id": "1",
          "country": "US",
          "is_billing": "True",
          "is_physical": "True",
          "is_shipping": "False",
          "latitude": "46.881398",
          "line_1": "643 Summer Breeze",
          "line_2": "Suite 34",
          "line_3": "2nd Door on Left",
          "line_4": "Blue slot",
          "locality": "Sequim",
          "longitude": "-121.276566",
          "postcode": "98382",
          "region": "WA"
        }
      ],
      "contacts": [
        {
          "contact_id": "1",
          "email": "develop@crosoftware.com",
          "fax": "(360) 716-1968",
          "name": "John Doe",
          "notify_on_acknowledged_request": "False",
          "notify_on_completed_request": "False",
          "notify_on_dispatched_request": "False",
          "notify_on_failed_request": "False",
          "notify_on_new_request": "False",
          "number": "1-111-111-1111"
        }
      ],
      "created_on": "2019-03-08T16:40:37.647000",
      "customer_id": "2",
      "is_active": "True",
      "is_commercial": "False",
      "last_edited": "2019-03-08T16:40:37.647000",
      "name": "Jane Smith",
      "note": "An example note",
      "parent_id": "1",
      "reference_number": "1234",
      "renewal_date": "2100-03-08T16:40:37.647000",
      "sales_rep": "Jane Doe",
      "suspension_id": "1"
    }
  ],
  "total_count": "100",
  "total_pages": "1"
}

```

<a id="schemacustomerlocationlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|-|
|`current_page`|integer(int64)|-|
|`results`|array[[CustomerLocationModel](#schemacustomerlocationmodel)]|-|
|`total_count`|integer(int64)|-|
|`total_pages`|integer(int64)|-|

<h2 id="tocScustomerlocationmodel">CustomerLocationModel</h2>

```json
{
  "addresses": [
    {
      "address_id": "1",
      "country": "US",
      "is_billing": "True",
      "is_physical": "True",
      "is_shipping": "False",
      "latitude": "46.881398",
      "line_1": "643 Summer Breeze",
      "line_2": "Suite 34",
      "line_3": "2nd Door on Left",
      "line_4": "Blue slot",
      "locality": "Sequim",
      "longitude": "-121.276566",
      "postcode": "98382",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "contact_id": "1",
      "email": "develop@crosoftware.com",
      "fax": "(360) 716-1968",
      "name": "John Doe",
      "notify_on_acknowledged_request": "False",
      "notify_on_completed_request": "False",
      "notify_on_dispatched_request": "False",
      "notify_on_failed_request": "False",
      "notify_on_new_request": "False",
      "number": "1-111-111-1111"
    }
  ],
  "created_on": "2019-03-08T16:40:37.647000",
  "customer_id": "2",
  "is_active": "True",
  "is_commercial": "False",
  "last_edited": "2019-03-08T16:40:37.647000",
  "name": "Jane Smith",
  "note": "An example note",
  "parent_id": "1",
  "reference_number": "1234",
  "renewal_date": "2100-03-08T16:40:37.647000",
  "sales_rep": "Jane Doe",
  "suspension_id": "1"
}

```

<a id="schemacustomerlocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`addresses`|array[[CustomerAddressModel](#schemacustomeraddressmodel)]|-|
|`contacts`|array[[CustomerContactModel](#schemacustomercontactmodel)]|-|
|`created_on`|string(datetime)|-|
|`customer_id`|integer(int64)|-|
|`is_active`|boolean|-|
|`is_commercial`|boolean|-|
|`last_edited`|string(datetime)|-|
|`name`|string|-|
|`note`|string|-|
|`parent_id`|integer(int64)|-|
|`reference_number`|string(byte)|-|
|`renewal_date`|string(datetime)|-|
|`sales_rep`|string|-|
|`suspension_id`|integer(int64)|-|

<h2 id="tocScustomermodel">CustomerModel</h2>

```json
{
  "addresses": [
    {
      "address_id": "1",
      "country": "US",
      "is_billing": "True",
      "is_physical": "True",
      "is_shipping": "False",
      "latitude": "46.881398",
      "line_1": "643 Summer Breeze",
      "line_2": "Suite 34",
      "line_3": "2nd Door on Left",
      "line_4": "Blue slot",
      "locality": "Sequim",
      "longitude": "-121.276566",
      "postcode": "98382",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "contact_id": "1",
      "email": "develop@crosoftware.com",
      "fax": "(360) 716-1968",
      "name": "John Doe",
      "notify_on_acknowledged_request": "False",
      "notify_on_completed_request": "False",
      "notify_on_dispatched_request": "False",
      "notify_on_failed_request": "False",
      "notify_on_new_request": "False",
      "number": "1-111-111-1111"
    }
  ],
  "customer_id": "1",
  "locations": [
    {
      "created_on": "2019-02-12T01:32:45.980000",
      "is_active": "True",
      "is_commercial": "True",
      "last_edited": "2019-02-12T01:32:45.990000",
      "location_id": "1",
      "note": "An example note",
      "reference_number": "REF#A1631",
      "renewal_date": "2019-10-02T00:00:00",
      "sales_rep": "John Doe",
      "suspension_id": "1"
    }
  ],
  "name": "Sequim Waste Inc.",
  "parent_id": "1"
}

```

<a id="schemacustomermodel"></a>

|Name|Type|Description|
|---|---|---|
|`addresses`|array[[CustomerAddressModel](#schemacustomeraddressmodel)]|-|
|`contacts`|array[[CustomerContactModel](#schemacustomercontactmodel)]|-|
|`customer_id`|integer(int64)|-|
|`locations`|array[[CustomerModelLocationModel](#schemacustomermodellocationmodel)]|-|
|`name`|string|-|
|`parent_id`|integer(int64)|-|

<h2 id="tocScustomermodellocationmodel">CustomerModelLocationModel</h2>

```json
{
  "created_on": "2019-02-12T01:32:45.980000",
  "is_active": "True",
  "is_commercial": "True",
  "last_edited": "2019-02-12T01:32:45.990000",
  "location_id": "1",
  "note": "An example note",
  "reference_number": "REF#A1631",
  "renewal_date": "2019-10-02T00:00:00",
  "sales_rep": "John Doe",
  "suspension_id": "1"
}

```

<a id="schemacustomermodellocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`created_on`|string(datetime)|-|
|`is_active`|boolean|-|
|`is_commercial`|boolean|-|
|`last_edited`|string(datetime)|-|
|`location_id`|integer(int64)|-|
|`note`|string|-|
|`reference_number`|string|-|
|`renewal_date`|string(datetime)|-|
|`sales_rep`|string|-|
|`suspension_id`|integer(int64)|-|

<h2 id="tocSdestinationmodel">DestinationModel</h2>

```json
{
  "address": "123 Sequim Ave.",
  "city": "Sequim",
  "contact_email": "support@crosoftware.net",
  "contact_name": "John Doe",
  "contact_phone": "(706) 360-7109",
  "id": "1",
  "is_holding_yard": "True",
  "latitude": "128.123",
  "location": {
    "id": "1",
    "is_active": "True",
    "name": "Sequim"
  },
  "location_id": "1",
  "longitude": "54.234",
  "name": "A Destination",
  "state": "Washington",
  "zip": "98368"
}

```

<a id="schemadestinationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`address`|string|-|
|`city`|string|-|
|`contact_email`|string|-|
|`contact_name`|string|-|
|`contact_phone`|string|-|
|`id`|integer(int64)|-|
|`is_holding_yard`|boolean|-|
|`latitude`|number(float)|-|
|`location`|[LocationModel](#schemalocationmodel)|-|
|`location_id`|integer(int64)|-|
|`longitude`|number(float)|-|
|`name`|string|-|
|`state`|string|-|
|`zip`|string|-|

<h2 id="tocSdriverlistmodel">DriverListModel</h2>

```json
{
  "current_limit": "100",
  "current_page": "1",
  "results": [
    {
      "address": "1234 Cro St",
      "can_convert_to_group": "False",
      "can_create_requests": "False",
      "can_edit_requests": "False",
      "can_reposition_asset": "False",
      "city": "Sequim",
      "disable_shift_tracking": "False",
      "email": "john@crosoftware.net",
      "id": "2",
      "license_number": "123ABC",
      "location_id": "1",
      "name": "John Denver",
      "phone_number": "(360) 718-1234",
      "state": "WA",
      "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "zip": "98368"
    }
  ],
  "total_count": "1",
  "total_pages": "1"
}

```

<a id="schemadriverlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|-|
|`current_page`|integer(int64)|-|
|`results`|array[[DriverModel](#schemadrivermodel)]|-|
|`total_count`|integer(int64)|-|
|`total_pages`|integer(int64)|-|

<h2 id="tocSdrivermodel">DriverModel</h2>

```json
{
  "address": "1234 Cro St",
  "can_convert_to_group": "False",
  "can_create_requests": "False",
  "can_edit_requests": "False",
  "can_reposition_asset": "False",
  "city": "Sequim",
  "disable_shift_tracking": "False",
  "email": "john@crosoftware.net",
  "id": "2",
  "license_number": "123ABC",
  "location_id": "1",
  "name": "John Denver",
  "phone_number": "(360) 718-1234",
  "state": "WA",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "zip": "98368"
}

```

<a id="schemadrivermodel"></a>

|Name|Type|Description|
|---|---|---|
|`address`|string|-|
|`can_convert_to_group`|boolean|-|
|`can_create_requests`|boolean|-|
|`can_edit_requests`|boolean|-|
|`can_reposition_asset`|boolean|-|
|`city`|string|-|
|`disable_shift_tracking`|boolean|-|
|`email`|string|-|
|`id`|integer(int64)|-|
|`license_number`|string|-|
|`location_id`|integer(int64)|-|
|`name`|string|-|
|`phone_number`|string|-|
|`state`|string|-|
|`third_party_hauler_id`|[UUID](#schemauuid)|UUID|
|`zip`|string|-|

<h2 id="tocSgpseventcoordsprofilemodel">GpsEventCoordsProfileModel</h2>

```json
{
  "heading": "184.57",
  "latitude": "37.33517518",
  "longitude": "-122.03255055",
  "speed": "2.41"
}

```

<a id="schemagpseventcoordsprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`heading`|number(float)|-|
|`latitude`|number(float)|-|
|`longitude`|number(float)|-|
|`speed`|number(float)|-|

<h2 id="tocSgpseventlocationprofilemodel">GpsEventLocationProfileModel</h2>

```json
{
  "coords": {
    "heading": "184.57",
    "latitude": "37.33517518",
    "longitude": "-122.03255055",
    "speed": "2.41"
  },
  "timestamp": "2019-02-07T00:12:19.354Z"
}

```

<a id="schemagpseventlocationprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`coords`|[GpsEventCoordsProfileModel](#schemagpseventcoordsprofilemodel)|-|
|`timestamp`|string(datetime)|-|

<h2 id="tocSgpseventmodel">GpsEventModel</h2>

```json
{
  "bearing": "184.57",
  "created_on": "2019-02-07T00:12:19.354000",
  "device_name": "N/A",
  "driver_id": "2",
  "id": "3",
  "latitude": "37.33517518",
  "longitude": "-122.03255055",
  "truck_id": "string",
  "velocity": "2.41"
}

```

<a id="schemagpseventmodel"></a>

|Name|Type|Description|
|---|---|---|
|`bearing`|number(float)|-|
|`created_on`|string(datetime)|-|
|`device_name`|string|-|
|`driver_id`|integer(int64)|-|
|`id`|integer(int64)|-|
|`latitude`|number(float)|-|
|`longitude`|number(float)|-|
|`truck_id`|string|-|
|`velocity`|number(float)|-|

<h2 id="tocSgpseventprofilemodel">GpsEventProfileModel</h2>

```json
{
  "location": {
    "coords": {
      "heading": "184.57",
      "latitude": "37.33517518",
      "longitude": "-122.03255055",
      "speed": "2.41"
    },
    "timestamp": "2019-02-07T00:12:19.354Z"
  }
}

```

<a id="schemagpseventprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`location`|[GpsEventLocationProfileModel](#schemagpseventlocationprofilemodel)|-|

<h2 id="tocShaulerconnectionmodel">HaulerConnectionModel</h2>

```json
{
  "approved_by": "1",
  "approved_on": "2018-10-31T11:24:53.153000",
  "denied_on": "string",
  "is_approved": "True",
  "location_id": "1",
  "provider_email": "test_hauler@crosoftware.net",
  "provider_id": "2",
  "provider_name": "CRO Scrap - Sequim",
  "provider_phone": "na",
  "requested_on": "2018-10-31T18:24:06.723000"
}

```

<a id="schemahaulerconnectionmodel"></a>

|Name|Type|Description|
|---|---|---|
|`approved_by`|integer(int64)|-|
|`approved_on`|string(datetime)|-|
|`denied_on`|string|-|
|`is_approved`|boolean|-|
|`location_id`|integer(int64)|-|
|`provider_email`|string|-|
|`provider_id`|integer(int64)|-|
|`provider_name`|string|-|
|`provider_phone`|string|-|
|`requested_on`|string(datetime)|-|

<h2 id="tocSjoblistmodel">JobListModel</h2>

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "arrived_at_dest": "2018-11-18T19:54:55.327000",
      "arrived_on": "2018-11-18T19:54:55.327000",
      "asset": {
        "asset_type": {
          "deleted": "False",
          "id": "1",
          "is_default": "False",
          "location_id": "1",
          "name": "10 yrd",
          "quantity": "2",
          "require_numbers": "True",
          "weight": "3245"
        },
        "asset_type_id": "1",
        "cluster": "1",
        "customer_id": "1",
        "description": "A description",
        "dispatched_on": "2018-10-31T11:34:13.690000",
        "id": "1",
        "is_returned": "False",
        "last_activity_on": "2018-10-31T11:34:13.690000",
        "last_rental_invoice_on": "2018-10-31T11:34:13.690000",
        "latitude": "54.235",
        "location": {
          "id": "1",
          "is_active": "True",
          "name": "Sequim"
        },
        "location_id": "1",
        "longitude": "127.123",
        "number": "REF100",
        "quantity": "1",
        "returned_on": "2018-10-31T11:34:13.690000"
      },
      "asset_dropped": "1",
      "asset_id": "1",
      "asset_quantity": "1",
      "asset_type": {
        "deleted": "False",
        "id": "1",
        "is_default": "False",
        "location_id": "1",
        "name": "10 yrd",
        "quantity": "2",
        "require_numbers": "True",
        "weight": "3245"
      },
      "asset_type_id": "1",
      "completed_by": "1",
      "completed_by_driver": "False",
      "completed_on": "2018-11-18T19:54:55.327000",
      "confirmed_on": "2018-11-18T19:54:55.327000",
      "created_by_id": "1",
      "created_with_portal": "False",
      "customer": {
        "addresses": [
          {
            "address_id": "1",
            "country": "US",
            "is_billing": "True",
            "is_physical": "True",
            "is_shipping": "False",
            "latitude": "46.881398",
            "line_1": "643 Summer Breeze",
            "line_2": "Suite 34",
            "line_3": "2nd Door on Left",
            "line_4": "Blue slot",
            "locality": "Sequim",
            "longitude": "-121.276566",
            "postcode": "98382",
            "region": "WA"
          }
        ],
        "contacts": [
          {
            "contact_id": "1",
            "email": "develop@crosoftware.com",
            "fax": "(360) 716-1968",
            "name": "John Doe",
            "notify_on_acknowledged_request": "False",
            "notify_on_completed_request": "False",
            "notify_on_dispatched_request": "False",
            "notify_on_failed_request": "False",
            "notify_on_new_request": "False",
            "number": "1-111-111-1111"
          }
        ],
        "customer_id": "1",
        "locations": [
          {
            "created_on": "2019-02-12T01:32:45.980000",
            "is_active": "True",
            "is_commercial": "True",
            "last_edited": "2019-02-12T01:32:45.990000",
            "location_id": "1",
            "note": "An example note",
            "reference_number": "REF#A1631",
            "renewal_date": "2019-10-02T00:00:00",
            "sales_rep": "John Doe",
            "suspension_id": "1"
          }
        ],
        "name": "Sequim Waste Inc.",
        "parent_id": "1"
      },
      "customer_id": "9",
      "customer_notes": "Some customer notes",
      "departed_on": "2018-11-18T19:54:55.327000",
      "desired_asset_desc": "An asset description.",
      "dispatch_priority": "H",
      "dispatched_by_route": "1",
      "dispatched_on": "2018-11-18T19:54:55.327000",
      "dispatcher_notes": "Some dispatcher notes",
      "do_confirm": "False",
      "driver_notes": "Some driver notes",
      "dropped_number": "Unused/deprecated field",
      "dump_location": {
        "address": "123 Sequim Ave.",
        "city": "Sequim",
        "contact_email": "support@crosoftware.net",
        "contact_name": "John Doe",
        "contact_phone": "(706) 360-7109",
        "id": "1",
        "is_holding_yard": "True",
        "latitude": "128.123",
        "location": {
          "id": "1",
          "is_active": "True",
          "name": "Sequim"
        },
        "location_id": "1",
        "longitude": "54.234",
        "name": "A Destination",
        "state": "Washington",
        "zip": "98368"
      },
      "dump_location_id": "1",
      "dumped_on": "2018-11-18T19:54:55.327000",
      "end_time": "2018-11-18T19:54:55.327000",
      "fail_reason": "Failure reason",
      "final_location": {
        "address": "123 Sequim Ave.",
        "city": "Sequim",
        "contact_email": "support@crosoftware.net",
        "contact_name": "John Doe",
        "contact_phone": "(706) 360-7109",
        "id": "1",
        "is_holding_yard": "True",
        "latitude": "128.123",
        "location": {
          "id": "1",
          "is_active": "True",
          "name": "Sequim"
        },
        "location_id": "1",
        "longitude": "54.234",
        "name": "A Destination",
        "state": "Washington",
        "zip": "98368"
      },
      "final_location_id": "1",
      "flags": "Job notes",
      "id": "1",
      "invoice_notes": "Some invoice notes",
      "is_completed": "False",
      "is_declined": "False",
      "is_deleted": "False",
      "is_failed": "False",
      "is_paid": true,
      "job_group_id": "1",
      "location_id": "1",
      "merged_with_route": "1",
      "original_schedule_date": "2018-10-31T11:34:13.690000",
      "pickup_date": "2018-10-31T11:34:13.690000",
      "priority": "-1",
      "reference_number": null,
      "removed_number": "string",
      "requested_on": "2018-10-31T11:33:52.920000",
      "require_image": "False",
      "require_material": "False",
      "require_signature": "False",
      "require_weights": "False",
      "schedule_date": "2018-10-31T00:00:00",
      "start_location": {
        "address": "123 Sequim Ave.",
        "city": "Sequim",
        "contact_email": "support@crosoftware.net",
        "contact_name": "John Doe",
        "contact_phone": "(706) 360-7109",
        "id": "1",
        "is_holding_yard": "True",
        "latitude": "128.123",
        "location": {
          "id": "1",
          "is_active": "True",
          "name": "Sequim"
        },
        "location_id": "1",
        "longitude": "54.234",
        "name": "A Destination",
        "state": "Washington",
        "zip": "98368"
      },
      "start_location_id": "1",
      "start_time": "2018-10-31T11:33:52.920000",
      "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "times_failed": "0",
      "times_rolled_over": "0",
      "truck_id": "1",
      "type": "D",
      "weighed_on": "2018-10-31T11:33:52.920000"
    }
  ],
  "total_count": "1",
  "total_pages": "1"
}

```

<a id="schemajoblistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|-|
|`current_page`|integer(int64)|-|
|`results`|array[[JobModel](#schemajobmodel)]|-|
|`total_count`|integer(int64)|-|
|`total_pages`|integer(int64)|-|

<h2 id="tocSjobmodel">JobModel</h2>

```json
{
  "arrived_at_dest": "2018-11-18T19:54:55.327000",
  "arrived_on": "2018-11-18T19:54:55.327000",
  "asset": {
    "asset_type": {
      "deleted": "False",
      "id": "1",
      "is_default": "False",
      "location_id": "1",
      "name": "10 yrd",
      "quantity": "2",
      "require_numbers": "True",
      "weight": "3245"
    },
    "asset_type_id": "1",
    "cluster": "1",
    "customer_id": "1",
    "description": "A description",
    "dispatched_on": "2018-10-31T11:34:13.690000",
    "id": "1",
    "is_returned": "False",
    "last_activity_on": "2018-10-31T11:34:13.690000",
    "last_rental_invoice_on": "2018-10-31T11:34:13.690000",
    "latitude": "54.235",
    "location": {
      "id": "1",
      "is_active": "True",
      "name": "Sequim"
    },
    "location_id": "1",
    "longitude": "127.123",
    "number": "REF100",
    "quantity": "1",
    "returned_on": "2018-10-31T11:34:13.690000"
  },
  "asset_dropped": "1",
  "asset_id": "1",
  "asset_quantity": "1",
  "asset_type": {
    "deleted": "False",
    "id": "1",
    "is_default": "False",
    "location_id": "1",
    "name": "10 yrd",
    "quantity": "2",
    "require_numbers": "True",
    "weight": "3245"
  },
  "asset_type_id": "1",
  "completed_by": "1",
  "completed_by_driver": "False",
  "completed_on": "2018-11-18T19:54:55.327000",
  "confirmed_on": "2018-11-18T19:54:55.327000",
  "created_by_id": "1",
  "created_with_portal": "False",
  "customer": {
    "addresses": [
      {
        "address_id": "1",
        "country": "US",
        "is_billing": "True",
        "is_physical": "True",
        "is_shipping": "False",
        "latitude": "46.881398",
        "line_1": "643 Summer Breeze",
        "line_2": "Suite 34",
        "line_3": "2nd Door on Left",
        "line_4": "Blue slot",
        "locality": "Sequim",
        "longitude": "-121.276566",
        "postcode": "98382",
        "region": "WA"
      }
    ],
    "contacts": [
      {
        "contact_id": "1",
        "email": "develop@crosoftware.com",
        "fax": "(360) 716-1968",
        "name": "John Doe",
        "notify_on_acknowledged_request": "False",
        "notify_on_completed_request": "False",
        "notify_on_dispatched_request": "False",
        "notify_on_failed_request": "False",
        "notify_on_new_request": "False",
        "number": "1-111-111-1111"
      }
    ],
    "customer_id": "1",
    "locations": [
      {
        "created_on": "2019-02-12T01:32:45.980000",
        "is_active": "True",
        "is_commercial": "True",
        "last_edited": "2019-02-12T01:32:45.990000",
        "location_id": "1",
        "note": "An example note",
        "reference_number": "REF#A1631",
        "renewal_date": "2019-10-02T00:00:00",
        "sales_rep": "John Doe",
        "suspension_id": "1"
      }
    ],
    "name": "Sequim Waste Inc.",
    "parent_id": "1"
  },
  "customer_id": "9",
  "customer_notes": "Some customer notes",
  "departed_on": "2018-11-18T19:54:55.327000",
  "desired_asset_desc": "An asset description.",
  "dispatch_priority": "H",
  "dispatched_by_route": "1",
  "dispatched_on": "2018-11-18T19:54:55.327000",
  "dispatcher_notes": "Some dispatcher notes",
  "do_confirm": "False",
  "driver_notes": "Some driver notes",
  "dropped_number": "Unused/deprecated field",
  "dump_location": {
    "address": "123 Sequim Ave.",
    "city": "Sequim",
    "contact_email": "support@crosoftware.net",
    "contact_name": "John Doe",
    "contact_phone": "(706) 360-7109",
    "id": "1",
    "is_holding_yard": "True",
    "latitude": "128.123",
    "location": {
      "id": "1",
      "is_active": "True",
      "name": "Sequim"
    },
    "location_id": "1",
    "longitude": "54.234",
    "name": "A Destination",
    "state": "Washington",
    "zip": "98368"
  },
  "dump_location_id": "1",
  "dumped_on": "2018-11-18T19:54:55.327000",
  "end_time": "2018-11-18T19:54:55.327000",
  "fail_reason": "Failure reason",
  "final_location": {
    "address": "123 Sequim Ave.",
    "city": "Sequim",
    "contact_email": "support@crosoftware.net",
    "contact_name": "John Doe",
    "contact_phone": "(706) 360-7109",
    "id": "1",
    "is_holding_yard": "True",
    "latitude": "128.123",
    "location": {
      "id": "1",
      "is_active": "True",
      "name": "Sequim"
    },
    "location_id": "1",
    "longitude": "54.234",
    "name": "A Destination",
    "state": "Washington",
    "zip": "98368"
  },
  "final_location_id": "1",
  "flags": "Job notes",
  "id": "1",
  "invoice_notes": "Some invoice notes",
  "is_completed": "False",
  "is_declined": "False",
  "is_deleted": "False",
  "is_failed": "False",
  "is_paid": true,
  "job_group_id": "1",
  "location_id": "1",
  "merged_with_route": "1",
  "original_schedule_date": "2018-10-31T11:34:13.690000",
  "pickup_date": "2018-10-31T11:34:13.690000",
  "priority": "-1",
  "reference_number": null,
  "removed_number": "string",
  "requested_on": "2018-10-31T11:33:52.920000",
  "require_image": "False",
  "require_material": "False",
  "require_signature": "False",
  "require_weights": "False",
  "schedule_date": "2018-10-31T00:00:00",
  "start_location": {
    "address": "123 Sequim Ave.",
    "city": "Sequim",
    "contact_email": "support@crosoftware.net",
    "contact_name": "John Doe",
    "contact_phone": "(706) 360-7109",
    "id": "1",
    "is_holding_yard": "True",
    "latitude": "128.123",
    "location": {
      "id": "1",
      "is_active": "True",
      "name": "Sequim"
    },
    "location_id": "1",
    "longitude": "54.234",
    "name": "A Destination",
    "state": "Washington",
    "zip": "98368"
  },
  "start_location_id": "1",
  "start_time": "2018-10-31T11:33:52.920000",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "times_failed": "0",
  "times_rolled_over": "0",
  "truck_id": "1",
  "type": "D",
  "weighed_on": "2018-10-31T11:33:52.920000"
}

```

<a id="schemajobmodel"></a>

|Name|Type|Description|
|---|---|---|
|`arrived_at_dest`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Entered by driver for dispatcher and customer. Asset arrival at destination time. Only applicable for jobs with a valid dump destination.|
|`arrived_on`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Drive start time entered by driver for dispatcher and customer (arrived at job slider).|
|`asset`|[AssetModel](#schemaassetmodel)|-|
|`asset_dropped`|integer(int64)|Reference to deployed asset entered by driver for customer, dispatcher applicable to job types 'D', 'E'.|
|`asset_id`|integer(int64)|Applicable to job types 'E', 'P', 'R'.|
|`asset_quantity`|integer(int64)|How many assets are being serviced within a cluster (for jobs assigned to an asset cluster). For jobs dispatched by routes, or manually dispatched route stops, this value is 0 or 1.|
|`asset_type`|[AssetTypeModel](#schemaassettypemodel)|-|
|`asset_type_id`|integer(int64)|Selected asset for the job (job types 'D', 'L', 'E').|
|`completed_by`|integer(int64)|Dispatcher or driver id.|
|`completed_by_driver`|boolean|If TRUE, completed by driver. If FALSE, completed by dispatcher.|
|`completed_on`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Job completion time (must be in the past).|
|`confirmed_on`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Must be in the past.|
|`created_by_id`|integer(int64)|Customer, dispatcher, or driver id.|
|`created_with_portal`|boolean|Unused field|
|`customer`|[CustomerModel](#schemacustomermodel)|-|
|`customer_id`|integer(int64)|Customer identifier.|
|`customer_notes`|string|Notes entered by customers to communicate with dispatchers.|
|`departed_on`|string(datetime)|Unused/deprecated|
|`desired_asset_desc`|string|Free-form text entered by dispatchers and drivers to be used as the future asset description.|
|`dispatch_priority`|string|Entered by dispatchers to determine dispatch order. Can be 'H', 'M', 'L' (High, Medium, Low).|
|`dispatched_by_route`|integer(int64)|Route id of dispatching route (or NULL if not dispatched by a route).|
|`dispatched_on`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Time the job is assigned to a truck.|
|`dispatcher_notes`|string|Entered by dispatchers, read by drivers and dispatchers.|
|`do_confirm`|boolean|Tell dispatcher that a customer should be contacted before job is dispatched.|
|`driver_notes`|string|Entered by drivers when completing or failing a job for dispatchers.|
|`dropped_number`|string|Unused/deprecated|
|`dump_location`|[DestinationModel](#schemadestinationmodel)|-|
|`dump_location_id`|integer(int64)|Asset or asset cluster dump location identifier (e.g. trash bin needs  dumped before returning from customer).|
|`dumped_on`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Dump request completion date.|
|`end_time`|string(datetime)|Future estimated time of job completion.|
|`fail_reason`|string|Failure description selected by a driver for use by dispatchers.|
|`final_location`|[DestinationModel](#schemadestinationmodel)|-|
|`final_location_id`|integer(int64)|Final location identifier. Used by dispatchers for prioritizing jobs. Used by drivers to know where to leave the asset on job completion.|
|`flags`|string|Job notes.|
|`id`|integer(int64)|Job identifier.|
|`invoice_notes`|string|Invoice notes from the billing system.|
|`is_completed`|boolean|Job completion flag set by dispatchers and drivers.|
|`is_declined`|boolean|Job completion flag set by dispatchers and drivers.|
|`is_deleted`|boolean|Indicates whether job is still valid.|
|`is_failed`|boolean|Set by drivers and dispatchers to indicate a failed job.|
|`is_paid`|boolean|Unused/deprecated|
|`job_group_id`|integer(int64)|Job group identifier for group jobs (vs service, exchange, etc.).|
|`location_id`|integer(int64)|Owning location for the job.|
|`merged_with_route`|integer(int64)|Assigned by dispatchers for dispatchers and drivers.|
|`original_schedule_date`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Original scheduling date.|
|`pickup_date`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) A pickup job is scheduled for this date upon job completion. If the asset or cluster is assigned to a route stop, the route stop will be deleted. Must be in the future.|
|`priority`|integer(int64)|Assigned by dispatchers for job order completion determination for drivers.|
|`reference_number`|string|Provider-specific billing/reporting field.|
|`removed_number`|string|Unused/deprecated|
|`requested_on`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Job creation date.|
|`require_image`|boolean|Set by dispatchers and drivers, requires drivers to upload one or more job images before completion.|
|`require_material`|boolean|Set by dispatchers and drivers, requires drivers to set a material before completing a job.|
|`require_signature`|boolean|Set by dispatchers and drivers, requires drivers to get a customer signature before job completion.|
|`require_weights`|boolean|Set by disptachers and drivers, requires drivers to set material weights before job completion.|
|`schedule_date`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Scheduled job completion date.|
|`start_location`|[DestinationModel](#schemadestinationmodel)|-|
|`start_location_id`|integer(int64)|Pickup location for asset or asset cluster Set by dispatchers and drivers for drivers.|
|`start_time`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Time customer has requested job start, set by dispatchers for dispatchers and drivers.|
|`third_party_hauler_id`|[UUID](#schemauuid)|UUID|
|`times_failed`|integer(int64)|Number of times a job has been attempted and failed.|
|`times_rolled_over`|integer(int64)|Tracks job age in days for dispatchers.|
|`truck_id`|integer(int64)|Set by dispatchers to determine job visibility for drivers.|
|`type`|string|Set by dispatchers and customers. Represents physical actions to execute on job start. 'D', 'E', 'L', 'P', 'R'|
|`weighed_on`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Time of truck weight entry.|

<h2 id="tocSlocationlistmodel">LocationListModel</h2>

```json
{
  "current_limit": "1",
  "current_page": "1",
  "results": [
    {
      "id": "1",
      "is_active": "True",
      "name": "Sequim"
    }
  ],
  "total_count": "1",
  "total_pages": "1"
}

```

<a id="schemalocationlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|-|
|`current_page`|integer(int64)|-|
|`results`|array[[LocationModel](#schemalocationmodel)]|-|
|`total_count`|integer(int64)|-|
|`total_pages`|integer(int64)|-|

<h2 id="tocSlocationmodel">LocationModel</h2>

```json
{
  "id": "1",
  "is_active": "True",
  "name": "Sequim"
}

```

<a id="schemalocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`id`|integer(int64)|-|
|`is_active`|boolean|-|
|`name`|string|-|

<h2 id="tocStenantlistmodel">TenantListModel</h2>

```json
{
  "current_limit": "100",
  "current_page": "1",
  "results": [
    {
      "address": "123 some st",
      "city": "Sequim",
      "code": "CROSCRAP",
      "created_on": "2019-02-12T01:32:45.640000",
      "email": "test_admin@crosoftware.net",
      "id": "1",
      "is_active": "True",
      "name": "CRO Scrap",
      "phone": "1234567890",
      "state": "WA",
      "truck_limit": "string",
      "zip": "98360"
    }
  ],
  "total_count": "1",
  "total_pages": "1"
}

```

<a id="schematenantlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|-|
|`current_page`|integer(int64)|-|
|`results`|array[[TenantModel](#schematenantmodel)]|-|
|`total_count`|integer(int64)|-|
|`total_pages`|integer(int64)|-|

<h2 id="tocStenantmodel">TenantModel</h2>

```json
{
  "address": "123 some st",
  "city": "Sequim",
  "code": "CROSCRAP",
  "created_on": "2019-02-12T01:32:45.640000",
  "email": "test_admin@crosoftware.net",
  "id": "1",
  "is_active": "True",
  "name": "CRO Scrap",
  "phone": "1234567890",
  "state": "WA",
  "truck_limit": "string",
  "zip": "98360"
}

```

<a id="schematenantmodel"></a>

|Name|Type|Description|
|---|---|---|
|`address`|string|-|
|`city`|string|-|
|`code`|string(byte)|-|
|`created_on`|string(datetime)|-|
|`email`|string|-|
|`id`|integer(int64)|-|
|`is_active`|boolean|-|
|`name`|string|-|
|`phone`|string|-|
|`state`|string|-|
|`truck_limit`|string|-|
|`zip`|string|-|

<h2 id="tocSthirdpartyhaulerlistmodel">ThirdPartyHaulerListModel</h2>

```json
{
  "current_limit": "100",
  "current_page": "1",
  "results": [
    {
      "id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "name": "SMS594"
    }
  ],
  "total_count": "1",
  "total_pages": "1"
}

```

<a id="schemathirdpartyhaulerlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|-|
|`current_page`|integer(int64)|-|
|`results`|array[[ThirdPartyHaulerModel](#schemathirdpartyhaulermodel)]|-|
|`total_count`|integer(int64)|-|
|`total_pages`|integer(int64)|-|

<h2 id="tocSthirdpartyhaulermodel">ThirdPartyHaulerModel</h2>

```json
{
  "id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "name": "SMS594"
}

```

<a id="schemathirdpartyhaulermodel"></a>

|Name|Type|Description|
|---|---|---|
|`id`|[UUID](#schemauuid)|UUID|
|`name`|string|-|

<h2 id="tocStrucklistmodel">TruckListModel</h2>

```json
{
  "current_limit": "100",
  "current_page": "1",
  "results": [
    {
      "driver_id": "1",
      "id": "2",
      "location_id": "1",
      "name": "ZachTruck",
      "notes": "Sequim",
      "out_of_service": "False",
      "require_odometer": "False",
      "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "type": "AwesomeTRUCK Rolloff",
      "weight": "18678"
    }
  ],
  "total_count": "1",
  "total_pages": "1"
}

```

<a id="schematrucklistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|-|
|`current_page`|integer(int64)|-|
|`results`|array[[TruckModel](#schematruckmodel)]|-|
|`total_count`|integer(int64)|-|
|`total_pages`|integer(int64)|-|

<h2 id="tocStruckmodel">TruckModel</h2>

```json
{
  "driver_id": "1",
  "id": "2",
  "location_id": "1",
  "name": "ZachTruck",
  "notes": "Sequim",
  "out_of_service": "False",
  "require_odometer": "False",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "type": "AwesomeTRUCK Rolloff",
  "weight": "18678"
}

```

<a id="schematruckmodel"></a>

|Name|Type|Description|
|---|---|---|
|`driver_id`|integer(int64)|-|
|`id`|integer(int64)|-|
|`location_id`|integer(int64)|-|
|`name`|string|-|
|`notes`|string|-|
|`out_of_service`|boolean|-|
|`require_odometer`|boolean|-|
|`third_party_hauler_id`|[UUID](#schemauuid)|UUID|
|`type`|string|-|
|`weight`|integer(int64)|-|

<h2 id="tocSupdatecustomeraddressprofilemodel">UpdateCustomerAddressProfileModel</h2>

```json
{
  "country": "US",
  "is_billing": "True",
  "is_physical": "True",
  "is_shipping": "False",
  "latitude": "46.881398",
  "line_1": "643 Summer Breeze",
  "line_2": "Suite 34",
  "line_3": "2nd Door on Left",
  "line_4": "Blue slot",
  "locality": "Sequim",
  "longitude": "-121.276566",
  "postcode": "98382",
  "region": "WA"
}

```

<a id="schemaupdatecustomeraddressprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`country`|string|-|
|`is_billing`|boolean|-|
|`is_physical`|boolean|-|
|`is_shipping`|boolean|-|
|`latitude`|number(float)|-|
|`line_1`|string|-|
|`line_2`|string|-|
|`line_3`|string|-|
|`line_4`|string|-|
|`locality`|string|-|
|`longitude`|number(float)|-|
|`postcode`|integer(int64)|-|
|`region`|string|-|

<h2 id="tocSupdatecustomercontactprofilemodel">UpdateCustomerContactProfileModel</h2>

```json
{
  "email": "develop@crosoftware.com",
  "fax": "(360) 716-1968",
  "name": "John Doe",
  "notify_on_acknowledged_request": "False",
  "notify_on_completed_request": "False",
  "notify_on_dispatched_request": "False",
  "notify_on_failed_request": "False",
  "notify_on_new_request": "False",
  "number": "1-111-111-1111"
}

```

<a id="schemaupdatecustomercontactprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`email`|string|-|
|`fax`|string|-|
|`name`|string|-|
|`notify_on_acknowledged_request`|boolean|-|
|`notify_on_completed_request`|boolean|-|
|`notify_on_dispatched_request`|boolean|-|
|`notify_on_failed_request`|boolean|-|
|`notify_on_new_request`|boolean|-|
|`number`|string|-|

<h2 id="tocSupdatecustomerlocationprofilemodel">UpdateCustomerLocationProfileModel</h2>

```json
{
  "is_commercial": "True",
  "note": "An example note",
  "reference_number": "R100-10C",
  "renewal_date": "2100-02-12T01:32:45.640000",
  "sales_rep": "John Smith",
  "suspension_id": "1"
}

```

<a id="schemaupdatecustomerlocationprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`is_commercial`|boolean|-|
|`note`|string|-|
|`reference_number`|string|-|
|`renewal_date`|string(datetime)|-|
|`sales_rep`|string|-|
|`suspension_id`|integer(int64)|-|

<h2 id="tocSupdatecustomerprofilemodel">UpdateCustomerProfileModel</h2>

```json
{
  "name": "Sequim Waste Inc.",
  "parent_id": "1"
}

```

<a id="schemaupdatecustomerprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`name`|string|-|
|`parent_id`|integer(int64)|-|

<h2 id="tocSupdatedjobmodel">UpdatedJobModel</h2>

```json
{
  "arrived_at_dest": "2018-11-18T19:54:55.327000",
  "arrived_on": "2018-11-18T19:54:55.327000",
  "asset_dropped": "1",
  "asset_id": "1",
  "asset_quantity": "1",
  "asset_type_id": "1",
  "completed_by": "1",
  "completed_by_driver": "False",
  "completed_on": "2018-11-18T19:54:55.327000",
  "confirmed_on": "2018-11-18T19:54:55.327000",
  "created_by_id": "1",
  "created_with_portal": "False",
  "customer_id": "9",
  "customer_notes": "Some customer notes",
  "departed_on": "2018-11-18T19:54:55.327000",
  "desired_asset_desc": "An asset description.",
  "dispatch_priority": "H",
  "dispatched_by_route": "1",
  "dispatched_on": "2018-11-18T19:54:55.327000",
  "dispatcher_notes": "Some dispatcher notes",
  "do_confirm": "False",
  "driver_notes": "Some driver notes",
  "dropped_number": "Unused/deprecated field",
  "dump_location_id": "1",
  "dumped_on": "2018-11-18T19:54:55.327000",
  "end_time": "2018-11-18T19:54:55.327000",
  "fail_reason": "Failure reason",
  "final_location_id": "1",
  "flags": "Job notes",
  "id": "1",
  "invoice_notes": "Some invoice notes",
  "is_completed": "False",
  "is_declined": "False",
  "is_deleted": "False",
  "is_failed": "False",
  "is_paid": true,
  "job_group_id": "1",
  "location_id": "1",
  "merged_with_route": "1",
  "original_schedule_date": "2018-10-31T11:34:13.690000",
  "pickup_date": "2018-10-31T11:34:13.690000",
  "priority": "-1",
  "reference_number": null,
  "removed_number": "string",
  "requested_on": "2018-10-31T11:33:52.920000",
  "require_image": "False",
  "require_material": "False",
  "require_signature": "False",
  "require_weights": "False",
  "schedule_date": "2018-10-31T00:00:00",
  "start_location_id": "1",
  "start_time": "2018-10-31T11:33:52.920000",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "times_failed": "0",
  "times_rolled_over": "0",
  "truck_id": "1",
  "type": "D",
  "weighed_on": "2018-10-31T11:33:52.920000"
}

```

<a id="schemaupdatedjobmodel"></a>

|Name|Type|Description|
|---|---|---|
|`arrived_at_dest`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Entered by driver for dispatcher and customer. Asset arrival at destination time. Only applicable for jobs with a valid dump destination.|
|`arrived_on`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Drive start time entered by driver for dispatcher and customer (arrived at job slider).|
|`asset_dropped`|integer(int64)|Reference to deployed asset entered by driver for customer, dispatcher applicable to job types 'D', 'E'.|
|`asset_id`|integer(int64)|Applicable to job types 'E', 'P', 'R'.|
|`asset_quantity`|integer(int64)|How many assets are being serviced within a cluster (for jobs assigned to an asset cluster). For jobs dispatched by routes, or manually dispatched route stops, this value is 0 or 1.|
|`asset_type_id`|integer(int64)|Selected asset for the job (job types 'D', 'L', 'E').|
|`completed_by`|integer(int64)|Dispatcher or driver id.|
|`completed_by_driver`|boolean|If TRUE, completed by driver. If FALSE, completed by dispatcher.|
|`completed_on`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Job completion time (must be in the past).|
|`confirmed_on`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Must be in the past.|
|`created_by_id`|integer(int64)|Customer, dispatcher, or driver id.|
|`created_with_portal`|boolean|Unused field|
|`customer_id`|integer(int64)|Customer identifier.|
|`customer_notes`|string|Notes entered by customers to communicate with dispatchers.|
|`departed_on`|string(datetime)|Unused/deprecated|
|`desired_asset_desc`|string|Free-form text entered by dispatchers and drivers to be used as the future asset description.|
|`dispatch_priority`|string|Entered by dispatchers to determine dispatch order. Can be 'H', 'M', 'L' (High, Medium, Low).|
|`dispatched_by_route`|integer(int64)|Route id of dispatching route (or NULL if not dispatched by a route).|
|`dispatched_on`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Time the job is assigned to a truck.|
|`dispatcher_notes`|string|Entered by dispatchers, read by drivers and dispatchers.|
|`do_confirm`|boolean|Tell dispatcher that a customer should be contacted before job is dispatched.|
|`driver_notes`|string|Entered by drivers when completing or failing a job for dispatchers.|
|`dropped_number`|string|Unused/deprecated|
|`dump_location_id`|integer(int64)|Asset or asset cluster dump location identifier (e.g. trash bin needs  dumped before returning from customer).|
|`dumped_on`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Dump request completion date.|
|`end_time`|string(datetime)|Future estimated time of job completion.|
|`fail_reason`|string|Failure description selected by a driver for use by dispatchers.|
|`final_location_id`|integer(int64)|Final location identifier. Used by dispatchers for prioritizing jobs. Used by drivers to know where to leave the asset on job completion.|
|`flags`|string|Job notes.|
|`id`|integer(int64)|Job identifier.|
|`invoice_notes`|string|Invoice notes from the billing system.|
|`is_completed`|boolean|Job completion flag set by dispatchers and drivers.|
|`is_declined`|boolean|Job completion flag set by dispatchers and drivers.|
|`is_deleted`|boolean|Indicates whether job is still valid.|
|`is_failed`|boolean|Set by drivers and dispatchers to indicate a failed job.|
|`is_paid`|boolean|Unused/deprecated|
|`job_group_id`|integer(int64)|Job group identifier for group jobs (vs service, exchange, etc.).|
|`location_id`|integer(int64)|Owning location for the job.|
|`merged_with_route`|integer(int64)|Assigned by dispatchers for dispatchers and drivers.|
|`original_schedule_date`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Original scheduling date.|
|`pickup_date`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) A pickup job is scheduled for this date upon job completion. If the asset or cluster is assigned to a route stop, the route stop will be deleted. Must be in the future.|
|`priority`|integer(int64)|Assigned by dispatchers for job order completion determination for drivers.|
|`reference_number`|string|Provider-specific billing/reporting field.|
|`removed_number`|string|Unused/deprecated|
|`requested_on`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Job creation date.|
|`require_image`|boolean|Set by dispatchers and drivers, requires drivers to upload one or more job images before completion.|
|`require_material`|boolean|Set by dispatchers and drivers, requires drivers to set a material before completing a job.|
|`require_signature`|boolean|Set by dispatchers and drivers, requires drivers to get a customer signature before job completion.|
|`require_weights`|boolean|Set by disptachers and drivers, requires drivers to set material weights before job completion.|
|`schedule_date`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Scheduled job completion date.|
|`start_location_id`|integer(int64)|Pickup location for asset or asset cluster Set by dispatchers and drivers for drivers.|
|`start_time`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Time customer has requested job start, set by dispatchers for dispatchers and drivers.|
|`third_party_hauler_id`|[UUID](#schemauuid)|UUID|
|`times_failed`|integer(int64)|Number of times a job has been attempted and failed.|
|`times_rolled_over`|integer(int64)|Tracks job age in days for dispatchers.|
|`truck_id`|integer(int64)|Set by dispatchers to determine job visibility for drivers.|
|`type`|string|Set by dispatchers and customers. Represents physical actions to execute on job start. 'D', 'E', 'L', 'P', 'R'|
|`weighed_on`|string(datetime)|YYYY-MM-DDThh:mm:ss.ssssss ISO 8601 DateTime Format (GMT) Time of truck weight entry.|

