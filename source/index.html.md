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

## Customers

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
          String url = "https://api.crosoftware.net/location/{location_id}/customer";

          // Headers
          client.Headers.Add("Authorization", "bearer <jwt-access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/location/{location_id}/customer \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <jwt-access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <jwt-access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/location/{location_id}/customer',
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
  'Authorization' => 'bearer <jwt-access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/location/{location_id}/customer',
  params: {
  'Authorization' => 'string',
'X-TENANT-ID' => 'integer(int64)',
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <jwt-access-token>',
  'X-TENANT-ID': '1'
}

r = requests.get('https://api.crosoftware.net/location/{location_id}/customer', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/location/{location_id}/customer");
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

`GET /location/{location_id}/customer`

<a id="opIdlist_customers_for_location"></a>

List customers for location.

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer JWT access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

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
          "email": "develop@crosoftware.com",
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
      "created_on": "2019-02-01T22:43:09.190Z",
      "customer_id": 1,
      "is_active": false,
      "is_commercial": false,
      "last_edited": "2019-02-01T22:43:09.190Z",
      "location_id": 1,
      "name": "DEMOCO001",
      "note": "Service Location of DemoCo Inc.",
      "parent_id": 1,
      "reference_number": "Ref#100",
      "renewal_date": "2019-02-01T22:43:09.190Z",
      "sales_rep": "John Doe",
      "suspension_id": 1
    }
  ],
  "total_count": 100,
  "total_pages": 1
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ListCustomerResultModel](#schemalistcustomerresultmodel)|Paged result sef of customers for location.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

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
          String url = "https://api.crosoftware.net/location/{location_id}/driver/{driver_id}";

          // Headers
          client.Headers.Add("Authorization", "bearer <jwt-access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/location/{location_id}/driver/{driver_id} \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <jwt-access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <jwt-access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/location/{location_id}/driver/{driver_id}',
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
  'Authorization' => 'bearer <jwt-access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/location/{location_id}/driver/{driver_id}',
  params: {
  'Authorization' => 'string',
'X-TENANT-ID' => 'integer(int64)',
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <jwt-access-token>',
  'X-TENANT-ID': '1'
}

r = requests.get('https://api.crosoftware.net/location/{location_id}/driver/{driver_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/location/{location_id}/driver/{driver_id}");
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

`GET /location/{location_id}/driver/{driver_id}`

<a id="opIdget_driver"></a>

Get driver info.

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer JWT access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`driver_id`|path|integer(int64)|true|Driver identifier (internal).|

> Example responses

> 200 Response

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

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DriverModel](#schemadrivermodel)|Driver profile.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

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
          String url = "https://api.crosoftware.net/location/{location_id}/driver";

          // Headers
          client.Headers.Add("Authorization", "bearer <jwt-access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/location/{location_id}/driver \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <jwt-access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <jwt-access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/location/{location_id}/driver',
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
  'Authorization' => 'bearer <jwt-access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/location/{location_id}/driver',
  params: {
  'Authorization' => 'string',
'X-TENANT-ID' => 'integer(int64)',
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <jwt-access-token>',
  'X-TENANT-ID': '1'
}

r = requests.get('https://api.crosoftware.net/location/{location_id}/driver', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/location/{location_id}/driver");
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

`GET /location/{location_id}/driver`

<a id="opIdlist_drivers_for_location"></a>

List drivers for location.

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer JWT access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

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

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DriverListModel](#schemadriverlistmodel)|List of drivers for location.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

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
          String url = "https://api.crosoftware.net/hauler";

          // Headers
          client.Headers.Add("X-TENANT-ID", "1");
          
          // Parameters
          NameValueCollection parameters = new NameValueCollection();
          parameters.Add("company_name", "Cro Scrap");
          parameters.Add("username", "test_user@crosoftware.net");
          parameters.Add("password", "AnExample!Password1000");
          parameters.Add("recaptcha", "<recaptcha-string>");
          
          byte[] json = client.UploadValues(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/hauler?company_name=Cro%20Scrap&username=test_user%40crosoftware.net&password=AnExample%21Password1000&recaptcha=%3Crecaptcha-string%3E \
  -H 'Accept: application/json' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/hauler',
  method: 'post',
  data: '?company_name=Cro%20Scrap&username=test_user%40crosoftware.net&password=AnExample%21Password1000&recaptcha=%3Crecaptcha-string%3E',
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
  'X-TENANT-ID' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/hauler',
  params: {
  'X-TENANT-ID' => 'integer(int64)',
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'X-TENANT-ID': '1'
}

r = requests.post('https://api.crosoftware.net/hauler', params={
  'company_name': 'Cro Scrap',  'username': 'test_user@crosoftware.net',  'password': 'AnExample!Password1000',  'recaptcha': '<recaptcha-string>'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/hauler?company_name=Cro%20Scrap&username=test_user%40crosoftware.net&password=AnExample%21Password1000&recaptcha=%3Crecaptcha-string%3E");
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

`POST /hauler`

<a id="opIdcreate_third_party_hauler"></a>

Create 3rd Party hauler profile.

<aside class="success">
This operation does not require authentication
</aside>

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`company_name`|query|string(stringIdentifier)|true|The comapny identifier issued at account creation. All caps, no spaces, no special characters.|
|`username`|query|string(email)|true|The email address registered for an account. Access control is based on the username. Usernames must conform to the addr-spec defined in RFC 5322.|
|`password`|query|string(password)|true|ASCII string. Min length 6, max length 32.|
|`recaptcha`|query|string(recaptcha)|true|ReCaptcha string.|

> Example responses

> 200 Response

```json
{
  "id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "name": "EXCOID"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerModel](#schemathirdpartyhaulermodel)|Third party hauler profile.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

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
          String url = "https://api.crosoftware.net/hauler/{hauler_id}/connection";

          // Headers
          client.Headers.Add("Authorization", "bearer <jwt-access-token>");
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
curl -X POST https://api.crosoftware.net/hauler/{hauler_id}/connection?tenant_code=CROSCRAP%2B1 \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <jwt-access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <jwt-access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/hauler/{hauler_id}/connection',
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
  'Authorization' => 'bearer <jwt-access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/hauler/{hauler_id}/connection',
  params: {
  'Authorization' => 'string'
'X-TENANT-ID' => 'integer(int64)',
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <jwt-access-token>',
  'X-TENANT-ID': '1'
}

r = requests.post('https://api.crosoftware.net/hauler/{hauler_id}/connection', params={
  'tenant_code': 'CROSCRAP+1'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/hauler/{hauler_id}/connection?tenant_code=CROSCRAP%2B1");
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

`POST /hauler/{hauler_id}/connection`

<a id="opIdget_hauler"></a>

Create hauler connection.

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer JWT access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`hauler_id`|path|[UUID](#schemauuid)|true|Hauler identifier.|
|`tenant_code`|query|string(tenantCode)|true|&lt;YardCode&gt;+&lt;LocationId&gt;. The YardCode is an identifier assigned at account creation.|

> Example responses

> 200 Response

```json
{
  "approved_by": 1,
  "approved_on": "2019-02-01T22:43:09.194Z",
  "denied_on": "string",
  "is_approved": true,
  "location_id": 1,
  "provider_email": "test_hauler@crosoftware.net",
  "provider_id": 2,
  "provider_name": "CRO Scrap - Sequim",
  "provider_phone": "na",
  "requested_on": "2019-02-01T22:43:09.194Z"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[HaulerConnectionModel](#schemahaulerconnectionmodel)|Hauler with given UUID.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

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
          String url = "https://api.crosoftware.net/hauler/{hauler_id}";

          // Headers
          client.Headers.Add("Authorization", "bearer <jwt-access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/hauler/{hauler_id} \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <jwt-access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <jwt-access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/hauler/{hauler_id}',
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
  'Authorization' => 'bearer <jwt-access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/hauler/{hauler_id}',
  params: {
  'Authorization' => 'string',
'X-TENANT-ID' => 'integer(int64)',
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <jwt-access-token>',
  'X-TENANT-ID': '1'
}

r = requests.get('https://api.crosoftware.net/hauler/{hauler_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/hauler/{hauler_id}");
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

`GET /hauler/{hauler_id}`

<a id="opIdget_hauler"></a>

Hauler profile.

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer JWT access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`hauler_id`|path|[UUID](#schemauuid)|true|Hauler identifier.|

> Example responses

> 200 Response

```json
{
  "id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "name": "EXCOID"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerModel](#schemathirdpartyhaulermodel)|Hauler profile.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

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
          String url = "https://api.crosoftware.net/hauler";

          // Headers
          client.Headers.Add("Authorization", "bearer <jwt-access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/hauler \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <jwt-access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <jwt-access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/hauler',
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
  'Authorization' => 'bearer <jwt-access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/hauler',
  params: {
  'Authorization' => 'string',
'X-TENANT-ID' => 'integer(int64)',
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <jwt-access-token>',
  'X-TENANT-ID': '1'
}

r = requests.get('https://api.crosoftware.net/hauler', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/hauler");
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

`GET /hauler`

<a id="opIdlist_haulers"></a>

List third party haulers for tenant.

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer JWT access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "name": "EXCOID"
    }
  ],
  "total_count": 1,
  "total_pages": 1
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerListModel](#schemathirdpartyhaulerlistmodel)|List of third party haulers for tenant.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

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
          String url = "https://api.crosoftware.net/hauler/{hauler_id}/connection";

          // Headers
          client.Headers.Add("Authorization", "bearer <jwt-access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/hauler/{hauler_id}/connection \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <jwt-access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <jwt-access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/hauler/{hauler_id}/connection',
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
  'Authorization' => 'bearer <jwt-access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/hauler/{hauler_id}/connection',
  params: {
  'Authorization' => 'string',
'X-TENANT-ID' => 'integer(int64)',
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <jwt-access-token>',
  'X-TENANT-ID': '1'
}

r = requests.get('https://api.crosoftware.net/hauler/{hauler_id}/connection', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/hauler/{hauler_id}/connection");
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

`GET /hauler/{hauler_id}/connection`

<a id="opIdlist_hauler_connections"></a>

List of 3rd party haulers.

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer JWT access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`hauler_id`|path|[UUID](#schemauuid)|true|Hauler identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

> Example responses

> 200 Response

```json
{
  "approved_by": 1,
  "approved_on": "2019-02-01T22:43:09.197Z",
  "denied_on": "string",
  "is_approved": true,
  "location_id": 1,
  "provider_email": "test_hauler@crosoftware.net",
  "provider_id": 2,
  "provider_name": "CRO Scrap - Sequim",
  "provider_phone": "na",
  "requested_on": "2019-02-01T22:43:09.197Z"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[HaulerConnectionModel](#schemahaulerconnectionmodel)|List|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

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
          String url = "https://api.crosoftware.net/location/{location_id}/job/{job_id}";

          // Headers
          client.Headers.Add("Authorization", "bearer <jwt-access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          // Parameters
          NameValueCollection parameters = new NameValueCollection();
          parameters.Add("truck_id", "0");
          
          byte[] json = client.UploadValues(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/location/{location_id}/job/{job_id}?truck_id=0 \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <jwt-access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <jwt-access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/location/{location_id}/job/{job_id}',
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
  'Authorization' => 'bearer <jwt-access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/location/{location_id}/job/{job_id}',
  params: {
  'Authorization' => 'string'
'X-TENANT-ID' => 'integer(int64)',
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <jwt-access-token>',
  'X-TENANT-ID': '1'
}

r = requests.patch('https://api.crosoftware.net/location/{location_id}/job/{job_id}', params={
  'truck_id': '0'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/location/{location_id}/job/{job_id}?truck_id=0");
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

`PATCH /location/{location_id}/job/{job_id}`

<a id="opIddispatch_job"></a>

Dispatch job.

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer JWT access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`job_id`|path|integer(int64)|true|Job identifier (internal).|
|`truck_id`|query|integer(int64)|true|Truck identifier (internal).|
|`future_job_schedule_date`|query|[DateTime](#schemadatetime)|false|Future dispatch time for job.|

> Example responses

> 200 Response

```json
{
  "arrived_at_dest": "2019-02-01T22:43:09.198Z",
  "arrived_on": "2019-02-01T22:43:09.198Z",
  "asset_dropped": 1,
  "asset_id": 1,
  "asset_quantity": 1,
  "asset_type_id": 1,
  "completed_by": 1,
  "completed_by_driver": false,
  "completed_on": "2019-02-01T22:43:09.198Z",
  "confirmed_on": "2019-02-01T22:43:09.198Z",
  "created_by_id": 1,
  "created_with_portal": false,
  "customer_id": 9,
  "customer_notes": "Some customer notes",
  "departed_on": "2019-02-01T22:43:09.198Z",
  "desired_asset_desc": "An asset description.",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2019-02-01T22:43:09.198Z",
  "dispatcher_notes": "Some dispatcher notes",
  "do_confirm": false,
  "driver_notes": "Some driver notes",
  "dropped_number": "Unused/deprecated field",
  "dump_location_id": 1,
  "dumped_on": "2019-02-01T22:43:09.198Z",
  "end_time": "2019-02-01T22:43:09.198Z",
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
  "original_schedule_date": "2019-02-01T22:43:09.198Z",
  "pickup_date": "2019-02-01T22:43:09.198Z",
  "priority": -1,
  "reference_number": null,
  "removed_number": "string",
  "requested_on": "2019-02-01T22:43:09.198Z",
  "require_image": false,
  "require_material": false,
  "require_signature": false,
  "require_weights": false,
  "schedule_date": "2019-02-01T22:43:09.198Z",
  "start_location_id": 1,
  "start_time": "2019-02-01T22:43:09.198Z",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "times_failed": 0,
  "times_rolled_over": 0,
  "truck_id": 1,
  "type": "D",
  "weighed_on": "2019-02-01T22:43:09.198Z"
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[UpdatedJobModel](#schemaupdatedjobmodel)|UpdatedJobModel|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

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
          String url = "https://api.crosoftware.net/location/{location_id}/job/{job_id}";

          // Headers
          client.Headers.Add("Authorization", "bearer <jwt-access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/location/{location_id}/job/{job_id} \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <jwt-access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <jwt-access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/location/{location_id}/job/{job_id}',
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
  'Authorization' => 'bearer <jwt-access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/location/{location_id}/job/{job_id}',
  params: {
  'Authorization' => 'string',
'X-TENANT-ID' => 'integer(int64)',
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <jwt-access-token>',
  'X-TENANT-ID': '1'
}

r = requests.get('https://api.crosoftware.net/location/{location_id}/job/{job_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/location/{location_id}/job/{job_id}");
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

`GET /location/{location_id}/job/{job_id}`

<a id="opIdget_job"></a>

Get specified job.

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer JWT access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`job_id`|path|integer(int64)|true|Job identifier (internal).|

> Example responses

> 200 Response

```json
{
  "arrived_at_dest": "2019-02-01T22:43:09.200Z",
  "arrived_on": "2019-02-01T22:43:09.200Z",
  "asset_dropped": 1,
  "asset_id": 1,
  "asset_quantity": 1,
  "asset_type_id": 1,
  "completed_by": 1,
  "completed_by_driver": false,
  "completed_on": "2019-02-01T22:43:09.200Z",
  "confirmed_on": "2019-02-01T22:43:09.200Z",
  "created_by_id": 1,
  "created_with_portal": false,
  "customer_id": 9,
  "customer_notes": "Some customer notes",
  "departed_on": "2019-02-01T22:43:09.200Z",
  "desired_asset_desc": "An asset description.",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2019-02-01T22:43:09.200Z",
  "dispatcher_notes": "Some dispatcher notes",
  "do_confirm": false,
  "driver_notes": "Some driver notes",
  "dropped_number": "Unused/deprecated field",
  "dump_location_id": 1,
  "dumped_on": "2019-02-01T22:43:09.200Z",
  "end_time": "2019-02-01T22:43:09.200Z",
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
  "original_schedule_date": "2019-02-01T22:43:09.200Z",
  "pickup_date": "2019-02-01T22:43:09.200Z",
  "priority": -1,
  "reference_number": null,
  "removed_number": "string",
  "requested_on": "2019-02-01T22:43:09.200Z",
  "require_image": false,
  "require_material": false,
  "require_signature": false,
  "require_weights": false,
  "schedule_date": "2019-02-01T22:43:09.200Z",
  "start_location_id": 1,
  "start_time": "2019-02-01T22:43:09.200Z",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "times_failed": 0,
  "times_rolled_over": 0,
  "truck_id": 1,
  "type": "D",
  "weighed_on": "2019-02-01T22:43:09.200Z",
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
    "dispatched_on": "2019-02-01T22:43:09.200Z",
    "id": 1,
    "is_returned": false,
    "last_activity_on": "2019-02-01T22:43:09.200Z",
    "last_rental_invoice_on": "2019-02-01T22:43:09.200Z",
    "latitude": 54.235,
    "location": {
      "id": 1,
      "is_active": true,
      "name": "Sequim"
    },
    "location_id": 1,
    "longitude": 127.123,
    "number": "REF100",
    "quantity": 1,
    "returned_on": "2019-02-01T22:43:09.200Z"
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
    "created_on": "2019-02-01T22:43:09.200Z",
    "id": 9,
    "locations": [
      {
        "created_on": "2019-02-01T22:43:09.200Z",
        "customer_id": 9,
        "is_active": true,
        "is_commercial": false,
        "last_edited": "2019-02-01T22:43:09.200Z",
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
      "name": "Sequim"
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
      "name": "Sequim"
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
      "name": "Sequim"
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

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[JobModel](#schemajobmodel)|JobModel|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

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
          String url = "https://api.crosoftware.net/location/{location_id}/job";

          // Headers
          client.Headers.Add("Authorization", "bearer <jwt-access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/location/{location_id}/job \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <jwt-access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <jwt-access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/location/{location_id}/job',
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
  'Authorization' => 'bearer <jwt-access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/location/{location_id}/job',
  params: {
  'Authorization' => 'string',
'X-TENANT-ID' => 'integer(int64)',
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <jwt-access-token>',
  'X-TENANT-ID': '1'
}

r = requests.get('https://api.crosoftware.net/location/{location_id}/job', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/location/{location_id}/job");
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

`GET /location/{location_id}/job`

<a id="opIdlist_jobs_for_location"></a>

List jobs for location.

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer JWT access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

> Example responses

> 200 Response

```json
{
  "current_limit": 1,
  "current_page": 1,
  "results": [
    {
      "arrived_at_dest": "2019-02-01T22:43:09.202Z",
      "arrived_on": "2019-02-01T22:43:09.202Z",
      "asset_dropped": 1,
      "asset_id": 1,
      "asset_quantity": 1,
      "asset_type_id": 1,
      "completed_by": 1,
      "completed_by_driver": false,
      "completed_on": "2019-02-01T22:43:09.202Z",
      "confirmed_on": "2019-02-01T22:43:09.202Z",
      "created_by_id": 1,
      "created_with_portal": false,
      "customer_id": 9,
      "customer_notes": "Some customer notes",
      "departed_on": "2019-02-01T22:43:09.202Z",
      "desired_asset_desc": "An asset description.",
      "dispatch_priority": "H",
      "dispatched_by_route": 1,
      "dispatched_on": "2019-02-01T22:43:09.202Z",
      "dispatcher_notes": "Some dispatcher notes",
      "do_confirm": false,
      "driver_notes": "Some driver notes",
      "dropped_number": "Unused/deprecated field",
      "dump_location_id": 1,
      "dumped_on": "2019-02-01T22:43:09.202Z",
      "end_time": "2019-02-01T22:43:09.202Z",
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
      "original_schedule_date": "2019-02-01T22:43:09.202Z",
      "pickup_date": "2019-02-01T22:43:09.202Z",
      "priority": -1,
      "reference_number": null,
      "removed_number": "string",
      "requested_on": "2019-02-01T22:43:09.202Z",
      "require_image": false,
      "require_material": false,
      "require_signature": false,
      "require_weights": false,
      "schedule_date": "2019-02-01T22:43:09.202Z",
      "start_location_id": 1,
      "start_time": "2019-02-01T22:43:09.202Z",
      "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "times_failed": 0,
      "times_rolled_over": 0,
      "truck_id": 1,
      "type": "D",
      "weighed_on": "2019-02-01T22:43:09.202Z",
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
        "dispatched_on": "2019-02-01T22:43:09.203Z",
        "id": 1,
        "is_returned": false,
        "last_activity_on": "2019-02-01T22:43:09.203Z",
        "last_rental_invoice_on": "2019-02-01T22:43:09.203Z",
        "latitude": 54.235,
        "location": {
          "id": 1,
          "is_active": true,
          "name": "Sequim"
        },
        "location_id": 1,
        "longitude": 127.123,
        "number": "REF100",
        "quantity": 1,
        "returned_on": "2019-02-01T22:43:09.203Z"
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
        "created_on": "2019-02-01T22:43:09.203Z",
        "id": 9,
        "locations": [
          {
            "created_on": "2019-02-01T22:43:09.203Z",
            "customer_id": 9,
            "is_active": true,
            "is_commercial": false,
            "last_edited": "2019-02-01T22:43:09.203Z",
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
          "name": "Sequim"
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
          "name": "Sequim"
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
          "name": "Sequim"
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

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[JobListModel](#schemajoblistmodel)|List of jobs for location.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

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
          String url = "https://api.crosoftware.net/location/{location_id}";

          // Headers
          client.Headers.Add("Authorization", "bearer <jwt-access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/location/{location_id} \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <jwt-access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <jwt-access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/location/{location_id}',
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
  'Authorization' => 'bearer <jwt-access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/location/{location_id}',
  params: {
  'Authorization' => 'string',
'X-TENANT-ID' => 'integer(int64)',
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <jwt-access-token>',
  'X-TENANT-ID': '1'
}

r = requests.get('https://api.crosoftware.net/location/{location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/location/{location_id}");
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

`GET /location/{location_id}`

<a id="opIdget_location"></a>

Get info for specified location.

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer JWT access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|

> Example responses

> 200 Response

```json
{
  "id": 1,
  "is_active": true,
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
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

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
          String url = "https://api.crosoftware.net/location";

          // Headers
          client.Headers.Add("Authorization", "bearer <jwt-access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/location \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <jwt-access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <jwt-access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/location',
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
  'Authorization' => 'bearer <jwt-access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/location',
  params: {
  'Authorization' => 'string',
'X-TENANT-ID' => 'integer(int64)',
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <jwt-access-token>',
  'X-TENANT-ID': '1'
}

r = requests.get('https://api.crosoftware.net/location', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/location");
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

`GET /location`

<a id="opIdlist_locations"></a>

List locations for tenant.

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer JWT access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

> Example responses

> 200 Response

```json
{
  "current_limit": 1,
  "current_page": 1,
  "results": [
    {
      "id": 1,
      "is_active": true,
      "name": "Sequim"
    }
  ],
  "total_count": 1,
  "total_pages": 1
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[LocationListModel](#schemalocationlistmodel)|List of locations|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

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
          String url = "https://api.crosoftware.net/location/{location_id}/truck/{truck_id}";

          // Headers
          client.Headers.Add("Authorization", "bearer <jwt-access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/location/{location_id}/truck/{truck_id} \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <jwt-access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <jwt-access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/location/{location_id}/truck/{truck_id}',
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
  'Authorization' => 'bearer <jwt-access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/location/{location_id}/truck/{truck_id}',
  params: {
  'Authorization' => 'string',
'X-TENANT-ID' => 'integer(int64)',
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <jwt-access-token>',
  'X-TENANT-ID': '1'
}

r = requests.get('https://api.crosoftware.net/location/{location_id}/truck/{truck_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/location/{location_id}/truck/{truck_id}");
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

`GET /location/{location_id}/truck/{truck_id}`

<a id="opIdget_truck"></a>

Get truck info.

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer JWT access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`truck_id`|path|integer(int64)|true|Truck identifier (internal).|

> Example responses

> 200 Response

```json
{
  "driver_id": 1,
  "id": 2,
  "location_id": 1,
  "name": "AnExampleTruck",
  "notes": "Sequim",
  "out_of_service": false,
  "require_odometer": false,
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "type": "Example Truck Rolloff",
  "weight": 18678
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|string|Truck info.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

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
          String url = "https://api.crosoftware.net/location/{location_id}/truck";

          // Headers
          client.Headers.Add("Authorization", "bearer <jwt-access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/location/{location_id}/truck \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <jwt-access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <jwt-access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/location/{location_id}/truck',
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
  'Authorization' => 'bearer <jwt-access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/location/{location_id}/truck',
  params: {
  'Authorization' => 'string',
'X-TENANT-ID' => 'integer(int64)',
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <jwt-access-token>',
  'X-TENANT-ID': '1'
}

r = requests.get('https://api.crosoftware.net/location/{location_id}/truck', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/location/{location_id}/truck");
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

`GET /location/{location_id}/truck`

<a id="opIdlist_trucks_for_location"></a>

List trucks for location.

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer JWT access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`page_limit`|query|integer(int64)|false|Maximum number of results to include for paged queries. 0 &lt; PageLimit &lt; 1000.|
|`page_index`|query|integer(int64)|false|Dataset page number to retrieve. First page is 1.|

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
      "name": "AnExampleTruck",
      "notes": "Sequim",
      "out_of_service": false,
      "require_odometer": false,
      "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "type": "Example Truck Rolloff",
      "weight": 18678
    }
  ],
  "total_count": 1,
  "total_pages": 1
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TruckListModel](#schematrucklistmodel)|List of trucks for location.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

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
          String url = "https://api.crosoftware.net/location/{location_id}/truck/{truck_id}";

          // Headers
          client.Headers.Add("Authorization", "bearer <jwt-access-token>");
          client.Headers.Add("X-TENANT-ID", "1");
          
          // Parameters
          NameValueCollection parameters = new NameValueCollection();
          parameters.Add("driver_id", "0");
          
          byte[] json = client.UploadValues(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/location/{location_id}/truck/{truck_id}?driver_id=0 \
  -H 'Accept: application/json' \
  -H 'Authorization: bearer <jwt-access-token>' \
  -H 'X-TENANT-ID: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'bearer <jwt-access-token>',
  'X-TENANT-ID':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/location/{location_id}/truck/{truck_id}',
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
  'Authorization' => 'bearer <jwt-access-token>',
  'X-TENANT-ID' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/location/{location_id}/truck/{truck_id}',
  params: {
  'Authorization' => 'string'
'X-TENANT-ID' => 'integer(int64)',
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'bearer <jwt-access-token>',
  'X-TENANT-ID': '1'
}

r = requests.patch('https://api.crosoftware.net/location/{location_id}/truck/{truck_id}', params={
  'driver_id': '0'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/location/{location_id}/truck/{truck_id}?driver_id=0");
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

`PATCH /location/{location_id}/truck/{truck_id}`

<a id="opIdset_truck_driver"></a>

Set driver for truck.

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`Authorization`|header|string|true|Authorization bearer JWT access token.|
|`X-TENANT-ID`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`truck_id`|path|integer(int64)|true|Truck identifier (internal).|
|`driver_id`|query|integer(int64)|true|Location identifier (internal).|

> Example responses

> 200 Response

```json
{
  "driver_id": 1,
  "id": 2,
  "location_id": 1,
  "name": "AnExampleTruck",
  "notes": "Sequim",
  "out_of_service": false,
  "require_odometer": false,
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "type": "Example Truck Rolloff",
  "weight": 18678
}
```

> 400 Response

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TruckModel](#schematruckmodel)|Updated truck profile.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|string|One or more invalid input parameters.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|string|Missing x-tenant-id header or user not authorized for specified tenant.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|string|Resource not found. Commonly due to missing or extra parameters.|

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

<h2 id="tocSaddressmodel">AddressModel</h2>

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

<a id="schemaaddressmodel"></a>

|Name|Type|Description|
|---|---|---|
|`country`|string|-|
|`id`|integer(int64)|-|
|`latitude`|number(float)|-|
|`line_1`|string|-|
|`line_2`|string|-|
|`line_3`|string|-|
|`line_4`|string|-|
|`locality`|string|-|
|`longitude`|number(float)|-|
|`postcode`|string|-|
|`region`|string|-|

<h2 id="tocSassetmodel">AssetModel</h2>

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
  "dispatched_on": "2019-02-01T22:43:09.209Z",
  "id": 1,
  "is_returned": false,
  "last_activity_on": "2019-02-01T22:43:09.209Z",
  "last_rental_invoice_on": "2019-02-01T22:43:09.209Z",
  "latitude": 54.235,
  "location": {
    "id": 1,
    "is_active": true,
    "name": "Sequim"
  },
  "location_id": 1,
  "longitude": 127.123,
  "number": "REF100",
  "quantity": 1,
  "returned_on": "2019-02-01T22:43:09.209Z"
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

<h2 id="tocSbasejobmodel">BaseJobModel</h2>

```json
{
  "arrived_at_dest": "2019-02-01T22:43:09.210Z",
  "arrived_on": "2019-02-01T22:43:09.210Z",
  "asset_dropped": 1,
  "asset_id": 1,
  "asset_quantity": 1,
  "asset_type_id": 1,
  "completed_by": 1,
  "completed_by_driver": false,
  "completed_on": "2019-02-01T22:43:09.210Z",
  "confirmed_on": "2019-02-01T22:43:09.210Z",
  "created_by_id": 1,
  "created_with_portal": false,
  "customer_id": 9,
  "customer_notes": "Some customer notes",
  "departed_on": "2019-02-01T22:43:09.210Z",
  "desired_asset_desc": "An asset description.",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2019-02-01T22:43:09.210Z",
  "dispatcher_notes": "Some dispatcher notes",
  "do_confirm": false,
  "driver_notes": "Some driver notes",
  "dropped_number": "Unused/deprecated field",
  "dump_location_id": 1,
  "dumped_on": "2019-02-01T22:43:09.210Z",
  "end_time": "2019-02-01T22:43:09.210Z",
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
  "original_schedule_date": "2019-02-01T22:43:09.210Z",
  "pickup_date": "2019-02-01T22:43:09.210Z",
  "priority": -1,
  "reference_number": null,
  "removed_number": "string",
  "requested_on": "2019-02-01T22:43:09.210Z",
  "require_image": false,
  "require_material": false,
  "require_signature": false,
  "require_weights": false,
  "schedule_date": "2019-02-01T22:43:09.210Z",
  "start_location_id": 1,
  "start_time": "2019-02-01T22:43:09.210Z",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "times_failed": 0,
  "times_rolled_over": 0,
  "truck_id": 1,
  "type": "D",
  "weighed_on": "2019-02-01T22:43:09.210Z"
}

```

<a id="schemabasejobmodel"></a>

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

<h2 id="tocScustomeraddressmodel">CustomerAddressModel</h2>

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

<a id="schemacustomeraddressmodel"></a>

|Name|Type|Description|
|---|---|---|
|`address`|[AddressModel](#schemaaddressmodel)|-|
|`address_id`|integer(int64)|-|
|`customer_id`|integer(int64)|-|
|`is_active`|boolean|-|
|`is_billing`|boolean|-|
|`is_physical`|boolean|-|
|`is_shipping`|boolean|-|

<h2 id="tocScustomermodel">CustomerModel</h2>

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
  "created_on": "2019-02-01T22:43:09.211Z",
  "id": 9,
  "locations": [
    {
      "created_on": "2019-02-01T22:43:09.211Z",
      "customer_id": 9,
      "is_active": true,
      "is_commercial": false,
      "last_edited": "2019-02-01T22:43:09.211Z",
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

<a id="schemacustomermodel"></a>

|Name|Type|Description|
|---|---|---|
|`addresses`|array[[CustomerAddressModel](#schemacustomeraddressmodel)]|-|
|`created_on`|string(datetime)|-|
|`id`|integer(int64)|-|
|`locations`|array[[JobLocationModel](#schemajoblocationmodel)]|-|
|`name`|string(byte)|-|
|`parent_id`|integer(int64)|-|

<h2 id="tocScustomerresultaddressmodel">CustomerResultAddressModel</h2>

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

<a id="schemacustomerresultaddressmodel"></a>

|Name|Type|Description|
|---|---|---|
|`country`|string|-|
|`is_active`|boolean|-|
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
|`postcode`|string|-|
|`region`|string|-|

<h2 id="tocScustomerresultcontactmodel">CustomerResultContactModel</h2>

```json
{
  "email": "develop@crosoftware.com",
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

<a id="schemacustomerresultcontactmodel"></a>

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

<h2 id="tocScustomerresultmodel">CustomerResultModel</h2>

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
      "email": "develop@crosoftware.com",
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
  "created_on": "2019-02-01T22:43:09.212Z",
  "customer_id": 1,
  "is_active": false,
  "is_commercial": false,
  "last_edited": "2019-02-01T22:43:09.212Z",
  "location_id": 1,
  "name": "DEMOCO001",
  "note": "Service Location of DemoCo Inc.",
  "parent_id": 1,
  "reference_number": "Ref#100",
  "renewal_date": "2019-02-01T22:43:09.212Z",
  "sales_rep": "John Doe",
  "suspension_id": 1
}

```

<a id="schemacustomerresultmodel"></a>

|Name|Type|Description|
|---|---|---|
|`addresses`|array[[CustomerResultAddressModel](#schemacustomerresultaddressmodel)]|-|
|`contacts`|array[[CustomerResultContactModel](#schemacustomerresultcontactmodel)]|-|
|`created_on`|string(datetime)|-|
|`customer_id`|integer(int64)|-|
|`is_active`|boolean|-|
|`is_commercial`|boolean|-|
|`last_edited`|string(datetime)|-|
|`location_id`|integer(int64)|-|
|`name`|string|-|
|`note`|string|-|
|`parent_id`|integer(int64)|-|
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
  "id": 1,
  "is_holding_yard": true,
  "latitude": 128.123,
  "location": {
    "id": 1,
    "is_active": true,
    "name": "Sequim"
  },
  "location_id": 1,
  "longitude": 54.234,
  "name": "A Destination",
  "state": "Washington",
  "zip": 98368
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

<h2 id="tocShaulerconnectionmodel">HaulerConnectionModel</h2>

```json
{
  "approved_by": 1,
  "approved_on": "2019-02-01T22:43:09.213Z",
  "denied_on": "string",
  "is_approved": true,
  "location_id": 1,
  "provider_email": "test_hauler@crosoftware.net",
  "provider_id": 2,
  "provider_name": "CRO Scrap - Sequim",
  "provider_phone": "na",
  "requested_on": "2019-02-01T22:43:09.213Z"
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
  "current_limit": 1,
  "current_page": 1,
  "results": [
    {
      "arrived_at_dest": "2019-02-01T22:43:09.213Z",
      "arrived_on": "2019-02-01T22:43:09.213Z",
      "asset_dropped": 1,
      "asset_id": 1,
      "asset_quantity": 1,
      "asset_type_id": 1,
      "completed_by": 1,
      "completed_by_driver": false,
      "completed_on": "2019-02-01T22:43:09.213Z",
      "confirmed_on": "2019-02-01T22:43:09.213Z",
      "created_by_id": 1,
      "created_with_portal": false,
      "customer_id": 9,
      "customer_notes": "Some customer notes",
      "departed_on": "2019-02-01T22:43:09.213Z",
      "desired_asset_desc": "An asset description.",
      "dispatch_priority": "H",
      "dispatched_by_route": 1,
      "dispatched_on": "2019-02-01T22:43:09.213Z",
      "dispatcher_notes": "Some dispatcher notes",
      "do_confirm": false,
      "driver_notes": "Some driver notes",
      "dropped_number": "Unused/deprecated field",
      "dump_location_id": 1,
      "dumped_on": "2019-02-01T22:43:09.213Z",
      "end_time": "2019-02-01T22:43:09.213Z",
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
      "original_schedule_date": "2019-02-01T22:43:09.213Z",
      "pickup_date": "2019-02-01T22:43:09.213Z",
      "priority": -1,
      "reference_number": null,
      "removed_number": "string",
      "requested_on": "2019-02-01T22:43:09.213Z",
      "require_image": false,
      "require_material": false,
      "require_signature": false,
      "require_weights": false,
      "schedule_date": "2019-02-01T22:43:09.213Z",
      "start_location_id": 1,
      "start_time": "2019-02-01T22:43:09.213Z",
      "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "times_failed": 0,
      "times_rolled_over": 0,
      "truck_id": 1,
      "type": "D",
      "weighed_on": "2019-02-01T22:43:09.213Z",
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
        "dispatched_on": "2019-02-01T22:43:09.213Z",
        "id": 1,
        "is_returned": false,
        "last_activity_on": "2019-02-01T22:43:09.213Z",
        "last_rental_invoice_on": "2019-02-01T22:43:09.213Z",
        "latitude": 54.235,
        "location": {
          "id": 1,
          "is_active": true,
          "name": "Sequim"
        },
        "location_id": 1,
        "longitude": 127.123,
        "number": "REF100",
        "quantity": 1,
        "returned_on": "2019-02-01T22:43:09.213Z"
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
        "created_on": "2019-02-01T22:43:09.214Z",
        "id": 9,
        "locations": [
          {
            "created_on": "2019-02-01T22:43:09.214Z",
            "customer_id": 9,
            "is_active": true,
            "is_commercial": false,
            "last_edited": "2019-02-01T22:43:09.214Z",
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
          "name": "Sequim"
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
          "name": "Sequim"
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
          "name": "Sequim"
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

<a id="schemajoblistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|-|
|`current_page`|integer(int64)|-|
|`results`|array[[JobModel](#schemajobmodel)]|-|
|`total_count`|integer(int64)|-|
|`total_pages`|integer(int64)|-|

<h2 id="tocSjoblocationmodel">JobLocationModel</h2>

```json
{
  "created_on": "2019-02-01T22:43:09.215Z",
  "customer_id": 9,
  "is_active": true,
  "is_commercial": false,
  "last_edited": "2019-02-01T22:43:09.215Z",
  "location_id": 1,
  "note": "string",
  "reference_number": "string",
  "renewal_date": "string",
  "sales_rep": "string",
  "suspension_id": "string"
}

```

<a id="schemajoblocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`created_on`|string(datetime)|-|
|`customer_id`|integer(int64)|-|
|`is_active`|boolean|-|
|`is_commercial`|boolean|-|
|`last_edited`|string(datetime)|-|
|`location_id`|integer(int64)|-|
|`note`|string|-|
|`reference_number`|string|-|
|`renewal_date`|string|-|
|`sales_rep`|string|-|
|`suspension_id`|string|-|

<h2 id="tocSjobmodel">JobModel</h2>

```json
{
  "arrived_at_dest": "2019-02-01T22:43:09.215Z",
  "arrived_on": "2019-02-01T22:43:09.215Z",
  "asset_dropped": 1,
  "asset_id": 1,
  "asset_quantity": 1,
  "asset_type_id": 1,
  "completed_by": 1,
  "completed_by_driver": false,
  "completed_on": "2019-02-01T22:43:09.215Z",
  "confirmed_on": "2019-02-01T22:43:09.215Z",
  "created_by_id": 1,
  "created_with_portal": false,
  "customer_id": 9,
  "customer_notes": "Some customer notes",
  "departed_on": "2019-02-01T22:43:09.215Z",
  "desired_asset_desc": "An asset description.",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2019-02-01T22:43:09.216Z",
  "dispatcher_notes": "Some dispatcher notes",
  "do_confirm": false,
  "driver_notes": "Some driver notes",
  "dropped_number": "Unused/deprecated field",
  "dump_location_id": 1,
  "dumped_on": "2019-02-01T22:43:09.216Z",
  "end_time": "2019-02-01T22:43:09.216Z",
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
  "original_schedule_date": "2019-02-01T22:43:09.216Z",
  "pickup_date": "2019-02-01T22:43:09.216Z",
  "priority": -1,
  "reference_number": null,
  "removed_number": "string",
  "requested_on": "2019-02-01T22:43:09.216Z",
  "require_image": false,
  "require_material": false,
  "require_signature": false,
  "require_weights": false,
  "schedule_date": "2019-02-01T22:43:09.216Z",
  "start_location_id": 1,
  "start_time": "2019-02-01T22:43:09.216Z",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "times_failed": 0,
  "times_rolled_over": 0,
  "truck_id": 1,
  "type": "D",
  "weighed_on": "2019-02-01T22:43:09.216Z",
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
    "dispatched_on": "2019-02-01T22:43:09.216Z",
    "id": 1,
    "is_returned": false,
    "last_activity_on": "2019-02-01T22:43:09.216Z",
    "last_rental_invoice_on": "2019-02-01T22:43:09.216Z",
    "latitude": 54.235,
    "location": {
      "id": 1,
      "is_active": true,
      "name": "Sequim"
    },
    "location_id": 1,
    "longitude": 127.123,
    "number": "REF100",
    "quantity": 1,
    "returned_on": "2019-02-01T22:43:09.216Z"
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
    "created_on": "2019-02-01T22:43:09.216Z",
    "id": 9,
    "locations": [
      {
        "created_on": "2019-02-01T22:43:09.216Z",
        "customer_id": 9,
        "is_active": true,
        "is_commercial": false,
        "last_edited": "2019-02-01T22:43:09.216Z",
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
      "name": "Sequim"
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
      "name": "Sequim"
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
      "name": "Sequim"
    },
    "location_id": 1,
    "longitude": 54.234,
    "name": "A Destination",
    "state": "Washington",
    "zip": 98368
  }
}

```

<a id="schemajobmodel"></a>

*allOf*

|Name|Type|Description|
|---|---|---|
|`-`|[BaseJobModel](#schemabasejobmodel)|-|

*and*

|Name|Type|Description|
|---|---|---|
|`-`|object|-|
|`» asset`|[AssetModel](#schemaassetmodel)|-|
|`» asset_type`|[AssetTypeModel](#schemaassettypemodel)|-|
|`» customer`|[CustomerModel](#schemacustomermodel)|-|
|`» dump_location`|[DestinationModel](#schemadestinationmodel)|-|
|`» final_location`|[DestinationModel](#schemadestinationmodel)|-|
|`» start_location`|[DestinationModel](#schemadestinationmodel)|-|
|`» third_party_hauler_id`|[UUID](#schemauuid)|UUID|

<h2 id="tocSlistcustomerresultmodel">ListCustomerResultModel</h2>

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
          "email": "develop@crosoftware.com",
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
      "created_on": "2019-02-01T22:43:09.217Z",
      "customer_id": 1,
      "is_active": false,
      "is_commercial": false,
      "last_edited": "2019-02-01T22:43:09.217Z",
      "location_id": 1,
      "name": "DEMOCO001",
      "note": "Service Location of DemoCo Inc.",
      "parent_id": 1,
      "reference_number": "Ref#100",
      "renewal_date": "2019-02-01T22:43:09.217Z",
      "sales_rep": "John Doe",
      "suspension_id": 1
    }
  ],
  "total_count": 100,
  "total_pages": 1
}

```

<a id="schemalistcustomerresultmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|-|
|`current_page`|integer(int64)|-|
|`results`|array[[CustomerResultModel](#schemacustomerresultmodel)]|-|
|`total_count`|integer(int64)|-|
|`total_pages`|integer(int64)|-|

<h2 id="tocSlocationlistmodel">LocationListModel</h2>

```json
{
  "current_limit": 1,
  "current_page": 1,
  "results": [
    {
      "id": 1,
      "is_active": true,
      "name": "Sequim"
    }
  ],
  "total_count": 1,
  "total_pages": 1
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
  "id": 1,
  "is_active": true,
  "name": "Sequim"
}

```

<a id="schemalocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`id`|integer(int64)|-|
|`is_active`|boolean|-|
|`name`|string|-|

<h2 id="tocSthirdpartyhaulerlistmodel">ThirdPartyHaulerListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "name": "EXCOID"
    }
  ],
  "total_count": 1,
  "total_pages": 1
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
  "name": "EXCOID"
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
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "driver_id": 1,
      "id": 2,
      "location_id": 1,
      "name": "AnExampleTruck",
      "notes": "Sequim",
      "out_of_service": false,
      "require_odometer": false,
      "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
      "type": "Example Truck Rolloff",
      "weight": 18678
    }
  ],
  "total_count": 1,
  "total_pages": 1
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
  "driver_id": 1,
  "id": 2,
  "location_id": 1,
  "name": "AnExampleTruck",
  "notes": "Sequim",
  "out_of_service": false,
  "require_odometer": false,
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "type": "Example Truck Rolloff",
  "weight": 18678
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

<h2 id="tocSupdatedjobmodel">UpdatedJobModel</h2>

```json
{
  "arrived_at_dest": "2019-02-01T22:43:09.218Z",
  "arrived_on": "2019-02-01T22:43:09.218Z",
  "asset_dropped": 1,
  "asset_id": 1,
  "asset_quantity": 1,
  "asset_type_id": 1,
  "completed_by": 1,
  "completed_by_driver": false,
  "completed_on": "2019-02-01T22:43:09.219Z",
  "confirmed_on": "2019-02-01T22:43:09.219Z",
  "created_by_id": 1,
  "created_with_portal": false,
  "customer_id": 9,
  "customer_notes": "Some customer notes",
  "departed_on": "2019-02-01T22:43:09.219Z",
  "desired_asset_desc": "An asset description.",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2019-02-01T22:43:09.219Z",
  "dispatcher_notes": "Some dispatcher notes",
  "do_confirm": false,
  "driver_notes": "Some driver notes",
  "dropped_number": "Unused/deprecated field",
  "dump_location_id": 1,
  "dumped_on": "2019-02-01T22:43:09.219Z",
  "end_time": "2019-02-01T22:43:09.219Z",
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
  "original_schedule_date": "2019-02-01T22:43:09.219Z",
  "pickup_date": "2019-02-01T22:43:09.219Z",
  "priority": -1,
  "reference_number": null,
  "removed_number": "string",
  "requested_on": "2019-02-01T22:43:09.219Z",
  "require_image": false,
  "require_material": false,
  "require_signature": false,
  "require_weights": false,
  "schedule_date": "2019-02-01T22:43:09.219Z",
  "start_location_id": 1,
  "start_time": "2019-02-01T22:43:09.219Z",
  "third_party_hauler_id": "b8d78911-e1fa-4adc-9b22-3b48dda30522",
  "times_failed": 0,
  "times_rolled_over": 0,
  "truck_id": 1,
  "type": "D",
  "weighed_on": "2019-02-01T22:43:09.219Z"
}

```

<a id="schemaupdatedjobmodel"></a>

*allOf*

|Name|Type|Description|
|---|---|---|
|`-`|[BaseJobModel](#schemabasejobmodel)|-|

*and*

|Name|Type|Description|
|---|---|---|
|`-`|object|-|

