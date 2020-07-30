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

<h1 id="cro-software-api">CRO Software API v1.0.3</h1>

Build on & integrate with CRO Software.

Base URLs:

* <a href="https://api.crosoftware.net/v0">https://api.crosoftware.net/v0</a>

Email: <a href="mailto:develop@crosoftware.net">Support</a> 

# Changelog
## [1.0.7] - 2020/07/31
### Changed
- Removed role Public from user role list when listing users.
- Changed list-customer operations to return results based on role (GET /customers, etc.).
- Updated billing/shipping address logic to be based on parent_id.

### Added
- Added active, last_updated_gte, created_on_gte, is_parent, parent_id filters to GET location/x/customers.
- Added company_id filter to user list DAL functions
- Added active filter to list_users.
- Added filter parent_id to /customers.
- Added Dispatcher to Administrator roles results.
- Added is_parent, location_id, is_active filters to GET /customers.
- Added is_dispatched to list job filters.
- Added CrmUser role.

### Fixed
- Corrected UserModel.id to UserModel.dispatcher_id for provider_id filter.
- Fixed issue with suspension_id nullability.
- Fixed incorrect location id column logic for all location-specific resources.
- Fixed Dispatcher role validation for null location_id for all endpoints.

## [1.0.6] - 2020/06/04
### Changed
- Changed customer address create to accept null for country, region, locality, & postcode if line_1 is null.

## [1.0.5] - 2020/05/20

### Changed
- Changed POST /locations/{location_id}/customers to allow omitted and/or NULL contact name, email, number, and fax.

## [1.0.4] - 2020/05/09

### Added
- Email, name, & phone number inputs as csv to POST /locations/{location_id}/customers.
- completed_by_driver filter to GET /locations/{location_id}/jobs.
- Job materials data to GET /locations/{location_id}/jobs.
- Field is_active to PATCH /customers/{customer_id}/locations/{location_id}.
- GET locations/{location_id}/dump_destinations.
- GET locations/{location_id}/dump_destinations/{dump_destination_id}.
- Customer dupe detection logic (name & address).

### Changed
- Changed POST /locations/{location_id}/customers to allow omitted and/or NULL renewal_date.
- Limited job dispatch to Dispatchers.

## [1.0.3] - 2019/10/21

### Added
- Parameter max_address_edit_distance to POST /locations/{location_id}/customers.
- Name filter to GET /location/{location_id}/users.

### Changed
- Duplicate customers created via POST /locations/{location_id}/customers now return 409 conflict.
- Updated parent_id, line_2, line_3, line_4 to be optional fields for POST /locations/{location_id}/customers.

### Fixed
- Added missing 'id' field to /tenant return results.

## [1.0.2] - 2019/09/25

### Added
- Added GET /locations/{location_id}/materials.
- Added GET /locations/{location_id}/users.
- Added GET /locations/{location_id}/users/{user_id}.
- Added scale_ticket field to JobModel.
- Added webhooks callbacks.
- Added webhook ping endpoint to API.
- Fixed issue in user location authorization for Admin roles.

### Changed
- Changed field inputs type validation to restrict to specified type (e.g. JSON int not implicitly converted to string).
- Changed requests with Admin users to also auth for Dispatched authorized calls.
- Renamed GET /customers 'filter_name' param to 'name'.

### Fixed
- Fixed header param naming issue in customer locations.
- Fixed authorization header spec.
- Fixed customer_id/location_id mixup in the CustomerLocation endpoints.
- Fixed bug in date filter validation.
- Fixed exception handling for missing/invalid endpoint arguments.
- Fixed exception bug and indentation error.

## [1.0.1] - 2019/07/30

### Fixed
- Un-flipped Customer ID and Location ID on the "Add customer to location" endpoint.

### Added
- Added filter_last_update_gte and filter_created_on_gte to GET /customers and GET /location/{loc_id}/jobs.
- Changed requests with Admin users to also auth for Dispatcher authorized calls.

### Changed
- Renamed GET /customers 'filter_name' param to 'name'.

## [0.0.0] - 2019/04/16

### Fixed
- Changed MultiTenantSAConnector to raise InputError on connection if missing tenant id.
- Fixed fence post error in paged queries logic.

### Added
- Exception handling to endpoint arg processing.
- Support for X-REQUEST-ID header.
- 'materials' list to job records (for GET /locations/{location_id}/jobs/{job_id} only).

### Changed
- Changed customer contact and address to Dispatcher role access (removed ThirdPartyDispatcher role access).
- Changed argument validation to raise InputError on invalid signature profile (vs HTTP 500).
- Changed scope list support (vs single scope).
- Changed tenant db session logic to raise InputError on x-tenant-id missing.

## [0.0.0] - 2019/04/09

### Fixed
- Improved /location/{location_id}/customers GET query performance.

### Added
- No external adds.

### Changed
- Pluralized endpoint URLs.
- Changed CustomerLocationApi.list_customers to RoleGroup.Authenticated.

## [0.0.0] - 2019/03/11

### Changed
- Log GPS event now accepts application/json instead of gps_event_json parameter.
- Create/update customer changed from request parameter to JSON customer profile.
- Create/update customer creates/updates customer addresses.
- Create/update customer creates/updates billing zone codes.
- Policy verification moved to function entry points.

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
- ThirdPartyDriver permission issues with List Customers.

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
    - Authorization URL = [https://idp.crobins.net/oauth2/auth](https://idp.crobins.net/oauth2/auth)
    - Token URL = [https://idp.crobins.net/oauth2/token](https://idp.crobins.net/oauth2/token)

|Scope|Scope Description|
|---|---|
|api|CRO API access|

- Flow: implicit
    - Authorization URL = [https://idp.crobins.net/oauth2/auth](https://idp.crobins.net/oauth2/auth)

|Scope|Scope Description|
|---|---|
|api|CRO API access|

- Flow: password

    - Token URL = [https://idp.crobins.net/oauth2/token](https://idp.crobins.net/oauth2/token)

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
          String url = "https://api.crosoftware.net/v0/customers/{customer_id}/addresses";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/v0/customers/{customer_id}/addresses \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers/{customer_id}/addresses',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/v0/customers/{customer_id}/addresses',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.post('https://api.crosoftware.net/v0/customers/{customer_id}/addresses', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers/{customer_id}/addresses");
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
  "is_billing": true,
  "is_shipping": true,
  "latitude": 56.2,
  "line_1": "123 Some St.",
  "line_2": "Office #34",
  "line_3": "Box #2",
  "line_4": "Drop in Blue Box",
  "locality": "Sequim",
  "longitude": 128.1,
  "postcode": "98368",
  "region": "WA"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`body`|body|[CreateCustomerAddressModel](#schemacreatecustomeraddressmodel)|true||

> Example responses

> 200 Response

```json
{
  "address_id": 1,
  "country": "US",
  "is_billing": true,
  "is_physical": true,
  "is_shipping": true,
  "latitude": 56.2,
  "line_1": "123 Some St.",
  "line_2": "Office #34",
  "line_3": "Box #2",
  "line_4": "Drop in Blue Box",
  "locality": "Sequim",
  "longitude": 128.1,
  "postcode": "98368",
  "region": "WA"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressModel](#schemacustomeraddressmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "DELETE", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X DELETE https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.delete 'https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.delete('https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id}");
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

`DELETE /customers/{customer_id}/addresses/{customer_address_id}`

<a id="opIddelete_customers_by_id_addresses_by_id"></a>

Deactivate a customer address.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_address_id`|path|integer(int64)|true|Customer address identifier.|

> Example responses

> 200 Response

```json
{
  "address_id": 1,
  "country": "US",
  "is_billing": true,
  "is_physical": true,
  "is_shipping": true,
  "latitude": 56.2,
  "line_1": "123 Some St.",
  "line_2": "Office #34",
  "line_3": "Box #2",
  "line_4": "Drop in Blue Box",
  "locality": "Sequim",
  "longitude": 128.1,
  "postcode": "98368",
  "region": "WA"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressModel](#schemacustomeraddressmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id}");
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

`GET /customers/{customer_id}/addresses/{customer_address_id}`

<a id="opIdget_customers_by_id_addresses_by_id"></a>

Get a customer address.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_address_id`|path|integer(int64)|true|Customer address identifier.|

> Example responses

> 200 Response

```json
{
  "address_id": 1,
  "country": "US",
  "is_billing": true,
  "is_physical": true,
  "is_shipping": true,
  "latitude": 56.2,
  "line_1": "123 Some St.",
  "line_2": "Office #34",
  "line_3": "Box #2",
  "line_4": "Drop in Blue Box",
  "locality": "Sequim",
  "longitude": 128.1,
  "postcode": "98368",
  "region": "WA"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressModel](#schemacustomeraddressmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/customers/{customer_id}/addresses";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/customers/{customer_id}/addresses \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers/{customer_id}/addresses',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/customers/{customer_id}/addresses',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/customers/{customer_id}/addresses', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers/{customer_id}/addresses");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`active`|query|boolean|false|If true, return only active records (default). If false, return only inactive records. If unspecified, return all.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "address_id": 1,
      "country": "US",
      "is_billing": true,
      "is_physical": true,
      "is_shipping": true,
      "latitude": 56.2,
      "line_1": "123 Some St.",
      "line_2": "Office #34",
      "line_3": "Box #2",
      "line_4": "Drop in Blue Box",
      "locality": "Sequim",
      "longitude": 128.1,
      "postcode": "98368",
      "region": "WA"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressListModel](#schemacustomeraddresslistmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.patch('https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers/{customer_id}/addresses/{customer_address_id}");
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

`PATCH /customers/{customer_id}/addresses/{customer_address_id}`

<a id="opIdpatch_customers_by_id_addresses_by_id"></a>

Update a customer address.

> Body parameter

```json
{
  "country": "US",
  "is_billing": true,
  "is_shipping": true,
  "latitude": 56.2,
  "line_1": "123 Some St.",
  "line_2": "Office #34",
  "line_3": "Box #2",
  "line_4": "Drop in Blue Box",
  "locality": "Sequim",
  "longitude": 128.1,
  "postcode": "98368",
  "region": "WA"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_address_id`|path|integer(int64)|true|Customer address identifier.|
|`body`|body|[UpdateCustomerAddressModel](#schemaupdatecustomeraddressmodel)|true||

> Example responses

> 200 Response

```json
{
  "address_id": 1,
  "country": "US",
  "is_billing": true,
  "is_physical": true,
  "is_shipping": true,
  "latitude": 56.2,
  "line_1": "123 Some St.",
  "line_2": "Office #34",
  "line_3": "Box #2",
  "line_4": "Drop in Blue Box",
  "locality": "Sequim",
  "longitude": 128.1,
  "postcode": "98368",
  "region": "WA"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressModel](#schemacustomeraddressmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/customers/{customer_id}/contacts";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/v0/customers/{customer_id}/contacts \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers/{customer_id}/contacts',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/v0/customers/{customer_id}/contacts',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.post('https://api.crosoftware.net/v0/customers/{customer_id}/contacts', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers/{customer_id}/contacts");
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
  "email": "john@crosoftware.net, jane@crosoftware.net",
  "fax": "+1 (360) 123-6543",
  "name": "John Doe",
  "notify_on_acknowledged_request": true,
  "notify_on_completed_request": true,
  "notify_on_dispatched_request": true,
  "notify_on_failed_request": true,
  "notify_on_new_request": true,
  "number": "+1 (360) 123-6543"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`body`|body|[CreateCustomerContactModel](#schemacreatecustomercontactmodel)|true||

> Example responses

> 200 Response

```json
{
  "contact_id": 1,
  "email": "john@crosoftware.net, jane@crosoftware.net",
  "fax": "+1 (360) 123-6543",
  "name": "John Doe",
  "notify_on_acknowledged_request": true,
  "notify_on_completed_request": true,
  "notify_on_dispatched_request": true,
  "notify_on_failed_request": true,
  "notify_on_new_request": true,
  "number": "+1 (360) 123-6543"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerContactModel](#schemacustomercontactmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/customers/{customer_id}/contacts/{customer_contact_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/customers/{customer_id}/contacts/{customer_contact_id} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers/{customer_id}/contacts/{customer_contact_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/customers/{customer_id}/contacts/{customer_contact_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/customers/{customer_id}/contacts/{customer_contact_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers/{customer_id}/contacts/{customer_contact_id}");
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

`GET /customers/{customer_id}/contacts/{customer_contact_id}`

<a id="opIdget_customers_by_id_contacts_by_id"></a>

Get a customer contact.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_contact_id`|path|integer(int64)|true|Customer contact identifier.|

> Example responses

> 200 Response

```json
{
  "contact_id": 1,
  "email": "john@crosoftware.net, jane@crosoftware.net",
  "fax": "+1 (360) 123-6543",
  "name": "John Doe",
  "notify_on_acknowledged_request": true,
  "notify_on_completed_request": true,
  "notify_on_dispatched_request": true,
  "notify_on_failed_request": true,
  "notify_on_new_request": true,
  "number": "+1 (360) 123-6543"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerContactModel](#schemacustomercontactmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/customers/{customer_id}/contacts";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/customers/{customer_id}/contacts \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers/{customer_id}/contacts',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/customers/{customer_id}/contacts',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/customers/{customer_id}/contacts', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers/{customer_id}/contacts");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "contact_id": 1,
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerContactListModel](#schemacustomercontactlistmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/customers/{customer_id}/contacts/{customer_contact_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/v0/customers/{customer_id}/contacts/{customer_contact_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers/{customer_id}/contacts/{customer_contact_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/v0/customers/{customer_id}/contacts/{customer_contact_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.patch('https://api.crosoftware.net/v0/customers/{customer_id}/contacts/{customer_contact_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers/{customer_id}/contacts/{customer_contact_id}");
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

`PATCH /customers/{customer_id}/contacts/{customer_contact_id}`

<a id="opIdpatch_customers_by_id_contacts_by_id"></a>

Update a customer contact.

> Body parameter

```json
{
  "email": "john@crosoftware.net, jane@crosoftware.net",
  "fax": "+1 (360) 123-6543",
  "name": "John Doe",
  "notify_on_acknowledged_request": true,
  "notify_on_completed_request": true,
  "notify_on_dispatched_request": true,
  "notify_on_failed_request": true,
  "notify_on_new_request": true,
  "number": "+1 (360) 123-6543"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_contact_id`|path|integer(int64)|true|Customer contact identifier.|
|`body`|body|[UpdateCustomerContactModel](#schemaupdatecustomercontactmodel)|true||

> Example responses

> 200 Response

```json
{
  "contact_id": 1,
  "email": "john@crosoftware.net, jane@crosoftware.net",
  "fax": "+1 (360) 123-6543",
  "name": "John Doe",
  "notify_on_acknowledged_request": true,
  "notify_on_completed_request": true,
  "notify_on_dispatched_request": true,
  "notify_on_failed_request": true,
  "notify_on_new_request": true,
  "number": "+1 (360) 123-6543"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerContactModel](#schemacustomercontactmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.post('https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}");
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

`POST /customers/{customer_id}/locations/{customer_location_id}`

<a id="opIdpost_customers_by_id_locations_by_id"></a>

Add customer location profile.

> Body parameter

```json
{
  "is_commercial": true,
  "note": "A note about something",
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "suspension_id": 1
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_location_id`|path|integer(int64)|true|Customer location identifier|
|`body`|body|[CreateCustomerLocationModel](#schemacreatecustomerlocationmodel)|true||

> Example responses

> 200 Response

```json
{
  "id": 1,
  "is_commercial": true,
  "note": "A note about something",
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "suspension_id": 1
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationModel](#schemacustomerlocationmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "DELETE", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X DELETE https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.delete 'https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.delete('https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}");
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

`DELETE /customers/{customer_id}/locations/{customer_location_id}`

<a id="opIddelete_customers_by_id_locations_by_id"></a>

Deactivate (soft delete) customer location profile.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_location_id`|path|integer(int64)|true|Customer location identifier|

> Example responses

> 200 Response

```json
{
  "id": 1,
  "is_commercial": true,
  "note": "A note about something",
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "suspension_id": 1
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationModel](#schemacustomerlocationmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}");
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

`GET /customers/{customer_id}/locations/{customer_location_id}`

<a id="opIdget_customers_by_id_locations_by_id"></a>

Get a customer contact.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_location_id`|path|integer(int64)|true|Customer location identifier|

> Example responses

> 200 Response

```json
{
  "id": 1,
  "is_commercial": true,
  "note": "A note about something",
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "suspension_id": 1
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationModel](#schemacustomerlocationmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/customers/{customer_id}/locations";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/customers/{customer_id}/locations \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers/{customer_id}/locations',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/customers/{customer_id}/locations',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/customers/{customer_id}/locations', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers/{customer_id}/locations");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`active`|query|boolean|false|If true, return only active records (default). If false, return only inactive records. If unspecified, return all.|
|`parent_id`|query|integer(int64)|false|If specified, return only children of the specified parent_id.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "id": 1,
      "is_commercial": true,
      "note": "A note about something",
      "reference_number": "A140",
      "renewal_date": "2049-10-31T11:32:38.390000",
      "sales_rep": "Jane Johnson",
      "suspension_id": 1
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationListModel](#schemacustomerlocationlistmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.patch('https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers/{customer_id}/locations/{customer_location_id}");
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

`PATCH /customers/{customer_id}/locations/{customer_location_id}`

<a id="opIdpatch_customers_by_id_locations_by_id"></a>

Update customer location profile.

> Body parameter

```json
{
  "is_active": true,
  "is_commercial": true,
  "note": "A note about something",
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "suspension_id": 1
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_location_id`|path|integer(int64)|true|Customer location identifier|
|`body`|body|[UpdateCustomerLocationModel](#schemaupdatecustomerlocationmodel)|true||

> Example responses

> 200 Response

```json
{
  "id": 1,
  "is_commercial": true,
  "note": "A note about something",
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "suspension_id": 1
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationModel](#schemacustomerlocationmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/customers";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/v0/locations/{location_id}/customers \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/customers',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/v0/locations/{location_id}/customers',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.post('https://api.crosoftware.net/v0/locations/{location_id}/customers', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/customers");
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
      "is_billing": true,
      "is_shipping": true,
      "latitude": 56.2,
      "line_1": "123 Some St.",
      "line_2": "Office #34",
      "line_3": "Box #2",
      "line_4": "Drop in Blue Box",
      "locality": "Sequim",
      "longitude": 128.1,
      "postcode": "98368",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "is_commercial": true,
  "name": "John Doe",
  "note": "A note about something",
  "parent_id": 0,
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "suspension_id": 1
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`max_address_edit_distance`|query|integer(int64)|false|Maximum address edit distance (levenshtein).|
|`body`|body|[CreateCustomerModel](#schemacreatecustomermodel)|true||

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "country": "US",
      "is_billing": true,
      "is_shipping": true,
      "latitude": 56.2,
      "line_1": "123 Some St.",
      "line_2": "Office #34",
      "line_3": "Box #2",
      "line_4": "Drop in Blue Box",
      "locality": "Sequim",
      "longitude": 128.1,
      "postcode": "98368",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "is_commercial": true,
  "name": "John Doe",
  "note": "A note about something",
  "parent_id": 0,
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "suspension_id": 1
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CreateCustomerModel](#schemacreatecustomermodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/customers/{customer_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/customers/{customer_id} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers/{customer_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/customers/{customer_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/customers/{customer_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers/{customer_id}");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "country": "US",
      "is_billing": true,
      "is_shipping": true,
      "latitude": 56.2,
      "line_1": "123 Some St.",
      "line_2": "Office #34",
      "line_3": "Box #2",
      "line_4": "Drop in Blue Box",
      "locality": "Sequim",
      "longitude": 128.1,
      "postcode": "98368",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "customer_id": 1,
  "is_commercial": true,
  "name": "John Doe",
  "note": "A note about something",
  "parent_id": 0,
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "suspension_id": 1
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerModel](#schemacustomermodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/customers/{location_customer_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/locations/{location_id}/customers/{location_customer_id} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/customers/{location_customer_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/locations/{location_id}/customers/{location_customer_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/locations/{location_id}/customers/{location_customer_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/customers/{location_customer_id}");
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

`GET /locations/{location_id}/customers/{location_customer_id}`

<a id="opIdget_locations_by_id_customers_by_id"></a>

Get customer for location.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`location_customer_id`|path|integer(int64)|true|Location customer identifier.|

> Example responses

> 200 Response

```json
{
  "id": 1,
  "is_commercial": true,
  "note": "A note about something",
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "suspension_id": 1
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationModel](#schemacustomerlocationmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/customers";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/customers \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/customers',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/customers', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`name`|query|string|false|If specified, return only records with matching names. Wildcard is &#039;*&#039;.|
|`active`|query|boolean|false|If true, return only active records (default). If false, return only inactive records. If unspecified, return all.|
|`last_updated_gte`|query|string(DateTime)|false|Return only records updated after (must be in past). If unspecified, return all.|
|`created_on_gte`|query|string(DateTime)|false|Return records created on or after the specified date. If unspecified, return all.|
|`is_parent`|query|boolean|false|If true, return accounts with no parent. If false, return accounts with a parent. If null, all records returned.|
|`parent_id`|query|integer(int64)|false|If specified, return only children of the specified parent_id.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|

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
          "country": "US",
          "is_billing": true,
          "is_shipping": true,
          "latitude": 56.2,
          "line_1": "123 Some St.",
          "line_2": "Office #34",
          "line_3": "Box #2",
          "line_4": "Drop in Blue Box",
          "locality": "Sequim",
          "longitude": 128.1,
          "postcode": "98368",
          "region": "WA"
        }
      ],
      "contacts": [
        {
          "email": "john@crosoftware.net, jane@crosoftware.net",
          "fax": "+1 (360) 123-6543",
          "name": "John Doe",
          "notify_on_acknowledged_request": true,
          "notify_on_completed_request": true,
          "notify_on_dispatched_request": true,
          "notify_on_failed_request": true,
          "notify_on_new_request": true,
          "number": "+1 (360) 123-6543"
        }
      ],
      "customer_id": 1,
      "is_commercial": true,
      "name": "John Doe",
      "note": "A note about something",
      "parent_id": 0,
      "reference_number": "A140",
      "renewal_date": "2049-10-31T11:32:38.390000",
      "sales_rep": "Jane Johnson",
      "suspension_id": 1
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerListModel](#schemacustomerlistmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/customers";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/locations/{location_id}/customers \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/customers',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/locations/{location_id}/customers',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/locations/{location_id}/customers', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/customers");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`name`|query|string|false|If specified, return only records with matching names. Wildcard is &#039;*&#039;.|
|`active`|query|boolean|false|If true, return only active records (default). If false, return only inactive records. If unspecified, return all.|
|`last_updated_gte`|query|string(DateTime)|false|Return only records updated after (must be in past). If unspecified, return all.|
|`created_on_gte`|query|string(DateTime)|false|Return records created on or after the specified date. If unspecified, return all.|
|`is_parent`|query|boolean|false|If true, return accounts with no parent. If false, return accounts with a parent. If null, all records returned.|
|`parent_id`|query|integer(int64)|false|If specified, return only children of the specified parent_id.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "id": 1,
      "is_commercial": true,
      "note": "A note about something",
      "reference_number": "A140",
      "renewal_date": "2049-10-31T11:32:38.390000",
      "sales_rep": "Jane Johnson",
      "suspension_id": 1
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerLocationListModel](#schemacustomerlocationlistmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/customers/{customer_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/v0/customers/{customer_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/customers/{customer_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/v0/customers/{customer_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.patch('https://api.crosoftware.net/v0/customers/{customer_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/customers/{customer_id}");
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
  "name": "John Doe",
  "parent_id": 0
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`body`|body|[UpdateCustomerModel](#schemaupdatecustomermodel)|true||

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "country": "US",
      "is_billing": true,
      "is_shipping": true,
      "latitude": 56.2,
      "line_1": "123 Some St.",
      "line_2": "Office #34",
      "line_3": "Box #2",
      "line_4": "Drop in Blue Box",
      "locality": "Sequim",
      "longitude": 128.1,
      "postcode": "98368",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "customer_id": 1,
  "is_commercial": true,
  "name": "John Doe",
  "note": "A note about something",
  "parent_id": 0,
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "suspension_id": 1
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerModel](#schemacustomermodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/drivers/{driver_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/locations/{location_id}/drivers/{driver_id} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/drivers/{driver_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/locations/{location_id}/drivers/{driver_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/locations/{location_id}/drivers/{driver_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/drivers/{driver_id}");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`driver_id`|path|integer(int64)|true|Driver identifier.|

> Example responses

> 200 Response

```json
{
  "address": "123 Some St.",
  "can_convert_to_group": true,
  "can_create_requests": true,
  "can_edit_requests": true,
  "can_reposition_asset": true,
  "city": "Sequim",
  "disable_shift_tracking": true,
  "email": "test@crosoftware.net",
  "id": 1,
  "license_number": "AJONDO251Z",
  "location_id": 1,
  "name": "John Doe",
  "phone_number": "+1 (360) 123-6543",
  "state": "WA",
  "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f",
  "zip": "98368"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DriverModel](#schemadrivermodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/drivers";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/locations/{location_id}/drivers \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/drivers',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/locations/{location_id}/drivers',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/locations/{location_id}/drivers', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/drivers");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "address": "123 Some St.",
      "can_convert_to_group": true,
      "can_create_requests": true,
      "can_edit_requests": true,
      "can_reposition_asset": true,
      "city": "Sequim",
      "disable_shift_tracking": true,
      "email": "test@crosoftware.net",
      "id": 1,
      "license_number": "AJONDO251Z",
      "location_id": 1,
      "name": "John Doe",
      "phone_number": "+1 (360) 123-6543",
      "state": "WA",
      "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f",
      "zip": "98368"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DriverListModel](#schemadriverlistmodel)|HTTP call succeeded.|
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

## Dump Destinations

### Get Dump Destination

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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/dump_destinations/{dump_destination_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/locations/{location_id}/dump_destinations/{dump_destination_id} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/dump_destinations/{dump_destination_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/locations/{location_id}/dump_destinations/{dump_destination_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/locations/{location_id}/dump_destinations/{dump_destination_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/dump_destinations/{dump_destination_id}");
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

`GET /locations/{location_id}/dump_destinations/{dump_destination_id}`

<a id="opIdget_locations_by_id_dump_destinations_by_id"></a>

Get dump destination.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`dump_destination_id`|path|integer(int64)|true|Dump destination identifier.|

> Example responses

> 200 Response

```json
{
  "address": "123 Some St.",
  "city": "Sequim",
  "contact_email": "test@crosoftware.net",
  "contact_name": "John Doe",
  "contact_phone": "+1 (360) 123-6543",
  "description": "A user entered/human readable text description.",
  "id": 1,
  "is_holding_yard": true,
  "latitude": 56.2,
  "location_id": 1,
  "longitude": 128.1,
  "state": "WA",
  "zip": "98368"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DumpDestinationModel](#schemadumpdestinationmodel)|HTTP call succeeded.|
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

### List Dump Destinations

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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/dump_destinations";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/locations/{location_id}/dump_destinations \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/dump_destinations',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/locations/{location_id}/dump_destinations',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/locations/{location_id}/dump_destinations', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/dump_destinations");
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

`GET /locations/{location_id}/dump_destinations`

<a id="opIdget_locations_by_id_dump_destinations"></a>

List dump destinations.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "address": "123 Some St.",
      "city": "Sequim",
      "contact_email": "test@crosoftware.net",
      "contact_name": "John Doe",
      "contact_phone": "+1 (360) 123-6543",
      "description": "A user entered/human readable text description.",
      "id": 1,
      "is_holding_yard": true,
      "latitude": 56.2,
      "location_id": 1,
      "longitude": 128.1,
      "state": "WA",
      "zip": "98368"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DumpDestinationListModel](#schemadumpdestinationlistmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/gps_events";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/v0/locations/{location_id}/gps_events \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/gps_events',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/v0/locations/{location_id}/gps_events',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.post('https://api.crosoftware.net/v0/locations/{location_id}/gps_events', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/gps_events");
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
      "heading": 0,
      "latitude": 56.2,
      "longitude": 128.1,
      "speed": 10.1
    },
    "timestamp": "2049-10-31T11:32:38.390000"
  }
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`body`|body|[GpsEventProfileModel](#schemagpseventprofilemodel)|true||

> Example responses

> 200 Response

```json
{
  "bearing": 0,
  "created_on": "2049-10-31T11:32:38.390000",
  "device_name": "John Doe",
  "driver_id": 1,
  "id": 1,
  "latitude": 56.2,
  "longitude": 128.1,
  "truck_id": 1,
  "velocity": 10.1
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[GpsStopModel](#schemagpsstopmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/haulers/{hauler_uuid}/connections";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          // Parameters
          NameValueCollection parameters = new NameValueCollection();
          parameters.Add("tenant_code", "08767");
          
          byte[] json = client.UploadString(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/v0/haulers/{hauler_uuid}/connections?tenant_code=08767 \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/haulers/{hauler_uuid}/connections',
  method: 'post',
  data: '?tenant_code=08767',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/v0/haulers/{hauler_uuid}/connections',
  params: {
  'tenant_code' => 'string'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.post('https://api.crosoftware.net/v0/haulers/{hauler_uuid}/connections', params={
  'tenant_code': '08767'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/haulers/{hauler_uuid}/connections?tenant_code=08767");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`hauler_uuid`|path|string(Uuid)|true|Third party hauler identifier.|
|`tenant_code`|query|string|true|Confirmation code for hauler creation.|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": {
    "approved_by": 1,
    "approved_on": "2049-10-31T11:32:38.390000",
    "denied_on": "2049-10-31T11:32:38.390000",
    "is_approved": true,
    "location_id": 1,
    "provider_email": "test@crosoftware.net",
    "provider_id": 1,
    "provider_name": "John Doe",
    "provider_phone": "+1 (360) 123-6543",
    "requested_on": "2049-10-31T11:32:38.390000"
  },
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerConnectionListModel](#schemathirdpartyhaulerconnectionlistmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/haulers";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          // Parameters
          NameValueCollection parameters = new NameValueCollection();
          parameters.Add("company_name", "BestScrap, Inc.");
          parameters.Add("username", "test_user_1000");
          parameters.Add("password", "AG00d!P@55w0rd;");
          parameters.Add("recaptcha", "<google captcha str>");
          
          byte[] json = client.UploadString(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/v0/haulers?company_name=BestScrap%2C%20Inc.&username=test_user_1000&password=AG00d%21P%4055w0rd%3B&recaptcha=%3Cgoogle%20captcha%20str%3E \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/haulers',
  method: 'post',
  data: '?company_name=BestScrap%2C%20Inc.&username=test_user_1000&password=AG00d%21P%4055w0rd%3B&recaptcha=%3Cgoogle%20captcha%20str%3E',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/v0/haulers',
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
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.post('https://api.crosoftware.net/v0/haulers', params={
  'company_name': 'BestScrap, Inc.',  'username': 'test_user_1000',  'password': 'AG00d!P@55w0rd;',  'recaptcha': '<google captcha str>'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/haulers?company_name=BestScrap%2C%20Inc.&username=test_user_1000&password=AG00d%21P%4055w0rd%3B&recaptcha=%3Cgoogle%20captcha%20str%3E");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`company_name`|query|string|true|Company name (free text).|
|`username`|query|string|true|Username.|
|`password`|query|string|true|Login password.|
|`recaptcha`|query|string|true|Recaptcha answer.|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": {
    "approved_by": 1,
    "approved_on": "2049-10-31T11:32:38.390000",
    "denied_on": "2049-10-31T11:32:38.390000",
    "is_approved": true,
    "location_id": 1,
    "provider_email": "test@crosoftware.net",
    "provider_id": 1,
    "provider_name": "John Doe",
    "provider_phone": "+1 (360) 123-6543",
    "requested_on": "2049-10-31T11:32:38.390000"
  },
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerConnectionListModel](#schemathirdpartyhaulerconnectionlistmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/haulers/{hauler_uuid}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/haulers/{hauler_uuid} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/haulers/{hauler_uuid}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/haulers/{hauler_uuid}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/haulers/{hauler_uuid}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/haulers/{hauler_uuid}");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`hauler_uuid`|path|string(Uuid)|true|Third party hauler identifier.|

> Example responses

> 200 Response

```json
{
  "id": "9f34f340-54d2-4403-a53b-d8017a64734f",
  "name": "John Doe"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerModel](#schemathirdpartyhaulermodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/haulers/{hauler_uuid}/connections";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/haulers/{hauler_uuid}/connections \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/haulers/{hauler_uuid}/connections',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/haulers/{hauler_uuid}/connections',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/haulers/{hauler_uuid}/connections', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/haulers/{hauler_uuid}/connections");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`hauler_uuid`|path|string(Uuid)|true|Third party hauler identifier.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": {
    "approved_by": 1,
    "approved_on": "2049-10-31T11:32:38.390000",
    "denied_on": "2049-10-31T11:32:38.390000",
    "is_approved": true,
    "location_id": 1,
    "provider_email": "test@crosoftware.net",
    "provider_id": 1,
    "provider_name": "John Doe",
    "provider_phone": "+1 (360) 123-6543",
    "requested_on": "2049-10-31T11:32:38.390000"
  },
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerConnectionListModel](#schemathirdpartyhaulerconnectionlistmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/haulers";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/haulers \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/haulers',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/haulers',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/haulers', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/haulers");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "id": "9f34f340-54d2-4403-a53b-d8017a64734f",
      "name": "John Doe"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerListModel](#schemathirdpartyhaulerlistmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/jobs/{job_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/v0/locations/{location_id}/jobs/{job_id} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/jobs/{job_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/v0/locations/{location_id}/jobs/{job_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.patch('https://api.crosoftware.net/v0/locations/{location_id}/jobs/{job_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/jobs/{job_id}");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`job_id`|path|integer(int64)|true|Job identifier.|
|`truck_id`|query|integer(int64)|false|Truck identifier.|
|`new_schedule_date`|query|string(DateTime)|false|New schedule date.|

> Example responses

> 200 Response

```json
{
  "arrived_at_dest": "2049-10-31T11:32:38.390000",
  "arrived_on": "2049-10-31T11:32:38.390000",
  "asset_dropped": 101,
  "asset_id": 1,
  "asset_quantity": 1,
  "asset_type_id": 1,
  "completed_by": 1,
  "completed_by_driver": true,
  "completed_on": "2049-10-31T11:32:38.390000",
  "confirmed_on": "2049-10-31T11:32:38.390000",
  "created_by_id": 1,
  "customer_id": 1,
  "customer_notes": "A note entered by a customer",
  "desired_asset_desc": "A note entered by a driver",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2049-10-31T11:32:38.390000",
  "dispatcher_notes": "A note entered by a dispatcher.",
  "do_confirm": true,
  "driver_notes": "A note entered by a driver.",
  "dump_location_id": 2,
  "dumped_on": "2049-10-31T11:32:38.390000",
  "end_time": "2049-10-31T11:32:38.390000",
  "fail_reason": "A failure description selected by a driver.",
  "final_location_id": 1,
  "flags": "Notes about a job.",
  "id": 1,
  "invoice_notes": "Notes from a billing invoice",
  "is_completed": true,
  "is_declined": true,
  "is_deleted": true,
  "is_failed": true,
  "job_group_id": 1,
  "location_id": 1,
  "merged_with_route": 1,
  "original_schedule_date": "2049-10-31T11:32:38.390000",
  "pickup_date": "2049-10-31T11:32:38.390000",
  "priority": -3,
  "reference_number": "A140",
  "requested_on": "2049-10-31T11:32:38.390000",
  "require_image": true,
  "require_material": true,
  "require_signature": true,
  "require_weights": true,
  "scale_ticket": "A5100",
  "schedule_date": "2049-10-31T11:32:38.390000",
  "start_location_id": 1,
  "start_time": "2049-10-31T11:32:38.390000",
  "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f",
  "times_failed": 2,
  "times_rolled_over": 1,
  "truck_id": 1,
  "type": "D",
  "weighed_on": "2049-10-31T11:32:38.390000"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[UpdatedJobModel](#schemaupdatedjobmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/jobs/{job_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/locations/{location_id}/jobs/{job_id} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/jobs/{job_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/locations/{location_id}/jobs/{job_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/locations/{location_id}/jobs/{job_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/jobs/{job_id}");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`job_id`|path|integer(int64)|true|Job identifier.|

> Example responses

> 200 Response

```json
{
  "arrived_at_dest": "2049-10-31T11:32:38.390000",
  "arrived_on": "2049-10-31T11:32:38.390000",
  "asset": {
    "asset_type": {
      "deleted": true,
      "id": 1,
      "is_default": true,
      "location_id": 1,
      "name": "John Doe",
      "quantity": 3,
      "require_numbers": true,
      "weight": 10192.77
    },
    "asset_type_id": 1,
    "cluster": 1,
    "customer_id": 1,
    "description": "A user entered/human readable text description.",
    "dispatched_on": "2049-10-31T11:32:38.390000",
    "id": 1,
    "is_returned": true,
    "last_activity_on": "2049-10-31T11:32:38.390000",
    "last_rental_invoice_on": "2049-10-31T11:32:38.390000",
    "latitude": 56.2,
    "location": {
      "id": 1,
      "is_active": true,
      "name": "CRO Scrap"
    },
    "location_id": 1,
    "longitude": 128.1,
    "number": "+1 (360) 123-6543",
    "quantity": 3,
    "returned_on": "2049-10-31T11:32:38.390000"
  },
  "asset_dropped": 101,
  "asset_id": 1,
  "asset_quantity": 1,
  "asset_type": {
    "deleted": true,
    "id": 1,
    "is_default": true,
    "location_id": 1,
    "name": "John Doe",
    "quantity": 3,
    "require_numbers": true,
    "weight": 10192.77
  },
  "asset_type_id": 1,
  "completed_by": 1,
  "completed_by_driver": true,
  "completed_on": "2049-10-31T11:32:38.390000",
  "confirmed_on": "2049-10-31T11:32:38.390000",
  "created_by_id": 1,
  "customer": {
    "addresses": [
      {
        "country": "US",
        "is_billing": true,
        "is_shipping": true,
        "latitude": 56.2,
        "line_1": "123 Some St.",
        "line_2": "Office #34",
        "line_3": "Box #2",
        "line_4": "Drop in Blue Box",
        "locality": "Sequim",
        "longitude": 128.1,
        "postcode": "98368",
        "region": "WA"
      }
    ],
    "contacts": [
      {
        "email": "john@crosoftware.net, jane@crosoftware.net",
        "fax": "+1 (360) 123-6543",
        "name": "John Doe",
        "notify_on_acknowledged_request": true,
        "notify_on_completed_request": true,
        "notify_on_dispatched_request": true,
        "notify_on_failed_request": true,
        "notify_on_new_request": true,
        "number": "+1 (360) 123-6543"
      }
    ],
    "customer_id": 1,
    "is_commercial": true,
    "name": "John Doe",
    "note": "A note about something",
    "parent_id": 0,
    "reference_number": "A140",
    "renewal_date": "2049-10-31T11:32:38.390000",
    "sales_rep": "Jane Johnson",
    "suspension_id": 1
  },
  "customer_id": 1,
  "customer_notes": "A note entered by a customer",
  "desired_asset_desc": "A note entered by a driver",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2049-10-31T11:32:38.390000",
  "dispatcher_notes": "A note entered by a dispatcher.",
  "do_confirm": true,
  "driver_notes": "A note entered by a driver.",
  "dump_location": {
    "id": 1,
    "is_active": true,
    "name": "CRO Scrap"
  },
  "dump_location_id": 2,
  "dumped_on": "2049-10-31T11:32:38.390000",
  "end_time": "2049-10-31T11:32:38.390000",
  "fail_reason": "A failure description selected by a driver.",
  "final_location": {
    "id": 1,
    "is_active": true,
    "name": "CRO Scrap"
  },
  "final_location_id": 1,
  "flags": "Notes about a job.",
  "invoice_notes": "Notes from a billing invoice",
  "is_completed": true,
  "is_declined": true,
  "is_deleted": true,
  "is_failed": true,
  "job_group_id": 1,
  "location_id": 1,
  "merged_with_route": 1,
  "original_schedule_date": "2049-10-31T11:32:38.390000",
  "pickup_date": "2049-10-31T11:32:38.390000",
  "priority": -3,
  "reference_number": "A140",
  "requested_on": "2049-10-31T11:32:38.390000",
  "require_image": true,
  "require_material": true,
  "require_signature": true,
  "require_weights": true,
  "scale_ticket": "A5100",
  "schedule_date": "2049-10-31T11:32:38.390000",
  "start_location": {
    "id": 1,
    "is_active": true,
    "name": "CRO Scrap"
  },
  "start_location_id": 1,
  "start_time": "2049-10-31T11:32:38.390000",
  "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f",
  "times_failed": 2,
  "times_rolled_over": 1,
  "truck_id": 1,
  "type": "D",
  "weighed_on": "2049-10-31T11:32:38.390000"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[JobModel](#schemajobmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/jobs";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/locations/{location_id}/jobs \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/jobs',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/locations/{location_id}/jobs',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/locations/{location_id}/jobs', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/jobs");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|
|`schedule_gt`|query|string(DateTime)|false|Return only jobs scheduled after (must be in past). If unspecified, return all.|
|`schedule_lt`|query|string(DateTime)|false|Return only jobs scheduled before.|
|`deleted`|query|boolean|false|If true, return only active records (default). If false, return only inactive records. If unspecified, return all.|
|`completed`|query|boolean|false|If true, return only records marked completed. If false, return only records marked incomplete. If unspecified, return all.|
|`completed_by_driver`|query|boolean|false|If true, return only records marked completed by a driver. If false, return only records marked incomplete. If unspecified, return all.|
|`failed`|query|boolean|false|If true, return only records marked deleted. If false, return only records marked as deleted. If unspecified, return all.|
|`driver_id`|query|boolean|false|If specified, return only records matching this driver (default). If unspecified, return all.|
|`truck_id`|query|boolean|false|If specified, return only records matching this truck (default). If unspecified, return all.|
|`last_updated_gte`|query|string(DateTime)|false|Return only records updated after (must be in past). If unspecified, return all.|
|`created_on_gte`|query|string(DateTime)|false|Return records created on or after the specified date. If unspecified, return all.|
|`is_dispatched`|query|boolean|false|Filter jobs based on dispatch status. If true, records with a valid truck_id (dispatched) are returned. If false, records with no truck_id (not dispatched) are returned. If null, all records are returned.|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "arrived_at_dest": "2049-10-31T11:32:38.390000",
      "arrived_on": "2049-10-31T11:32:38.390000",
      "asset": {
        "asset_type": {
          "deleted": true,
          "id": 1,
          "is_default": true,
          "location_id": 1,
          "name": "John Doe",
          "quantity": 3,
          "require_numbers": true,
          "weight": 10192.77
        },
        "asset_type_id": 1,
        "cluster": 1,
        "customer_id": 1,
        "description": "A user entered/human readable text description.",
        "dispatched_on": "2049-10-31T11:32:38.390000",
        "id": 1,
        "is_returned": true,
        "last_activity_on": "2049-10-31T11:32:38.390000",
        "last_rental_invoice_on": "2049-10-31T11:32:38.390000",
        "latitude": 56.2,
        "location": {
          "id": 1,
          "is_active": true,
          "name": "CRO Scrap"
        },
        "location_id": 1,
        "longitude": 128.1,
        "number": "+1 (360) 123-6543",
        "quantity": 3,
        "returned_on": "2049-10-31T11:32:38.390000"
      },
      "asset_dropped": 101,
      "asset_id": 1,
      "asset_quantity": 1,
      "asset_type": {
        "deleted": true,
        "id": 1,
        "is_default": true,
        "location_id": 1,
        "name": "John Doe",
        "quantity": 3,
        "require_numbers": true,
        "weight": 10192.77
      },
      "asset_type_id": 1,
      "completed_by": 1,
      "completed_by_driver": true,
      "completed_on": "2049-10-31T11:32:38.390000",
      "confirmed_on": "2049-10-31T11:32:38.390000",
      "created_by_id": 1,
      "customer": {
        "addresses": [
          {
            "country": "US",
            "is_billing": true,
            "is_shipping": true,
            "latitude": 56.2,
            "line_1": "123 Some St.",
            "line_2": "Office #34",
            "line_3": "Box #2",
            "line_4": "Drop in Blue Box",
            "locality": "Sequim",
            "longitude": 128.1,
            "postcode": "98368",
            "region": "WA"
          }
        ],
        "contacts": [
          {
            "email": "john@crosoftware.net, jane@crosoftware.net",
            "fax": "+1 (360) 123-6543",
            "name": "John Doe",
            "notify_on_acknowledged_request": true,
            "notify_on_completed_request": true,
            "notify_on_dispatched_request": true,
            "notify_on_failed_request": true,
            "notify_on_new_request": true,
            "number": "+1 (360) 123-6543"
          }
        ],
        "customer_id": 1,
        "is_commercial": true,
        "name": "John Doe",
        "note": "A note about something",
        "parent_id": 0,
        "reference_number": "A140",
        "renewal_date": "2049-10-31T11:32:38.390000",
        "sales_rep": "Jane Johnson",
        "suspension_id": 1
      },
      "customer_id": 1,
      "customer_notes": "A note entered by a customer",
      "desired_asset_desc": "A note entered by a driver",
      "dispatch_priority": "H",
      "dispatched_by_route": 1,
      "dispatched_on": "2049-10-31T11:32:38.390000",
      "dispatcher_notes": "A note entered by a dispatcher.",
      "do_confirm": true,
      "driver_notes": "A note entered by a driver.",
      "dump_location": {
        "id": 1,
        "is_active": true,
        "name": "CRO Scrap"
      },
      "dump_location_id": 2,
      "dumped_on": "2049-10-31T11:32:38.390000",
      "end_time": "2049-10-31T11:32:38.390000",
      "fail_reason": "A failure description selected by a driver.",
      "final_location": {
        "id": 1,
        "is_active": true,
        "name": "CRO Scrap"
      },
      "final_location_id": 1,
      "flags": "Notes about a job.",
      "invoice_notes": "Notes from a billing invoice",
      "is_completed": true,
      "is_declined": true,
      "is_deleted": true,
      "is_failed": true,
      "job_group_id": 1,
      "location_id": 1,
      "merged_with_route": 1,
      "original_schedule_date": "2049-10-31T11:32:38.390000",
      "pickup_date": "2049-10-31T11:32:38.390000",
      "priority": -3,
      "reference_number": "A140",
      "requested_on": "2049-10-31T11:32:38.390000",
      "require_image": true,
      "require_material": true,
      "require_signature": true,
      "require_weights": true,
      "scale_ticket": "A5100",
      "schedule_date": "2049-10-31T11:32:38.390000",
      "start_location": {
        "id": 1,
        "is_active": true,
        "name": "CRO Scrap"
      },
      "start_location_id": 1,
      "start_time": "2049-10-31T11:32:38.390000",
      "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f",
      "times_failed": 2,
      "times_rolled_over": 1,
      "truck_id": 1,
      "type": "D",
      "weighed_on": "2049-10-31T11:32:38.390000"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[JobListModel](#schemajoblistmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/locations/{location_id} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/locations/{location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/locations/{location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|

> Example responses

> 200 Response

```json
{
  "id": 1,
  "is_active": true,
  "name": "CRO Scrap"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[LocationModel](#schemalocationmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/locations";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/locations \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/locations',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/locations', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "id": 1,
      "is_active": true,
      "name": "CRO Scrap"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[LocationListModel](#schemalocationlistmodel)|HTTP call succeeded.|
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

## Materials

### List Materials

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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/materials";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/locations/{location_id}/materials \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/materials',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/locations/{location_id}/materials',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/locations/{location_id}/materials', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/materials");
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

`GET /locations/{location_id}/materials`

<a id="opIdget_locations_by_id_materials"></a>

List all job materials.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "created_on": "2049-10-31T11:32:38.390000",
      "description": "A user entered/human readable text description.",
      "factor": 1.1,
      "group_description": "A user entered/human readable text description.",
      "id": 1,
      "line_item_id": 1,
      "uom": "A user entered/human readable description of the UOM."
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[MaterialListModel](#schemamateriallistmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/tenants";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/tenants \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/tenants',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/tenants',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/tenants', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/tenants");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "address": "123 Some St.",
      "city": "Sequim",
      "code": "BESTSCRAP",
      "created_on": "2049-10-31T11:32:38.390000",
      "email": "test@crosoftware.net",
      "id": 1,
      "is_active": true,
      "name": "John Doe",
      "phone": "+1 (360) 123-6543",
      "state": "WA",
      "truck_limit": 0,
      "zip": "98368"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TenantListModel](#schematenantlistmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/trucks/{truck_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/locations/{location_id}/trucks/{truck_id} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/trucks/{truck_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/locations/{location_id}/trucks/{truck_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/locations/{location_id}/trucks/{truck_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/trucks/{truck_id}");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`truck_id`|path|integer(int64)|true|Truck identifier.|

> Example responses

> 200 Response

```json
{
  "driver_id": 1,
  "id": 1,
  "location_id": 1,
  "name": "John Doe",
  "notes": "A note about something",
  "out_of_service": true,
  "require_odometer": true,
  "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f",
  "type": "FlatHauler",
  "weight": 23100.1
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|string|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/trucks";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/locations/{location_id}/trucks \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/trucks',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/locations/{location_id}/trucks',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/locations/{location_id}/trucks', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/trucks");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "driver_id": 1,
      "id": 1,
      "location_id": 1,
      "name": "John Doe",
      "notes": "A note about something",
      "out_of_service": true,
      "require_odometer": true,
      "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f",
      "type": "FlatHauler",
      "weight": 23100.1
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TruckListModel](#schematrucklistmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/trucks/{truck_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          // Parameters
          NameValueCollection parameters = new NameValueCollection();
          parameters.Add("driver_id", "1");
          
          byte[] json = client.UploadString(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/v0/locations/{location_id}/trucks/{truck_id}?driver_id=1 \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/trucks/{truck_id}',
  method: 'patch',
  data: '?driver_id=1',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/v0/locations/{location_id}/trucks/{truck_id}',
  params: {
  'driver_id' => 'integer(int64)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.patch('https://api.crosoftware.net/v0/locations/{location_id}/trucks/{truck_id}', params={
  'driver_id': '1'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/trucks/{truck_id}?driver_id=1");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`truck_id`|path|integer(int64)|true|Truck identifier.|
|`driver_id`|query|integer(int64)|true|Driver identifier.|

> Example responses

> 200 Response

```json
{
  "driver_id": 1,
  "id": 1,
  "location_id": 1,
  "name": "John Doe",
  "notes": "A note about something",
  "out_of_service": true,
  "require_odometer": true,
  "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f",
  "type": "FlatHauler",
  "weight": 23100.1
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TruckModel](#schematruckmodel)|HTTP call succeeded.|
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

## Users

### Get User

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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/users/{user_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/locations/{location_id}/users/{user_id} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/users/{user_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/locations/{location_id}/users/{user_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/locations/{location_id}/users/{user_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/users/{user_id}");
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

`GET /locations/{location_id}/users/{user_id}`

<a id="opIdget_locations_by_id_users_by_id"></a>

Get user.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`user_id`|path|integer(int64)|true|User identifier.|

> Example responses

> 200 Response

```json
{
  "id": 1,
  "roles": [
    "Dispatcher"
  ],
  "username": "test_user_1000"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[UserModel](#schemausermodel)|HTTP call succeeded.|
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

### List Users

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
          String url = "https://api.crosoftware.net/v0/locations/{location_id}/users";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/locations/{location_id}/users \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/locations/{location_id}/users',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/locations/{location_id}/users',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/locations/{location_id}/users', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/locations/{location_id}/users");
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

`GET /locations/{location_id}/users`

<a id="opIdget_locations_by_id_users"></a>

List users.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`username`|query|string|false|If specified, return only records with matching usernames. If unspecified, return all. Wildcard is &#039;*&#039;.|
|`active`|query|boolean|false|If true, return only active records (default). If false, return only inactive records. If unspecified, return all.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "id": 1,
      "roles": [
        "Dispatcher"
      ],
      "username": "test_user_1000"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[UserListResultsModel](#schemauserlistresultsmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/hooks";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/v0/hooks \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/hooks',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.post 'https://api.crosoftware.net/v0/hooks',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.post('https://api.crosoftware.net/v0/hooks', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/hooks");
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
    "Customer"
  ],
  "secret": "<Secret>",
  "url": "https://test.url"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`body`|body|[CreateWebhookModel](#schemacreatewebhookmodel)|true||

> Example responses

> 200 Response

```json
{
  "events": [
    "Customer"
  ],
  "secret": "<Secret>",
  "url": "https://test.url"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CreateWebhookModel](#schemacreatewebhookmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/hooks/{hook_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "DELETE", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X DELETE https://api.crosoftware.net/v0/hooks/{hook_id} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/hooks/{hook_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.delete 'https://api.crosoftware.net/v0/hooks/{hook_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.delete('https://api.crosoftware.net/v0/hooks/{hook_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/hooks/{hook_id}");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`hook_id`|path|integer(int64)|true|Webhook identifier.|

> Example responses

> 200 Response

```json
{
  "events": [
    "Customer"
  ],
  "id": 1,
  "last_http_fail": "1",
  "last_http_success": "1",
  "url": "https://test.url"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[WebhookModel](#schemawebhookmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/hooks/{hook_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/hooks/{hook_id} \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/hooks/{hook_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/hooks/{hook_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/hooks/{hook_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/hooks/{hook_id}");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`hook_id`|path|integer(int64)|true|Webhook identifier.|

> Example responses

> 200 Response

```json
{
  "events": [
    "Customer"
  ],
  "id": 1,
  "last_http_fail": "1",
  "last_http_success": "1",
  "url": "https://test.url"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[WebhookModel](#schemawebhookmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/hooks";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/hooks \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/hooks',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/hooks',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/hooks', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/hooks");
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
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`deleted`|query|boolean|false|Is record deleted (soft delete).|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "events": [
        "Customer"
      ],
      "id": 1,
      "last_http_fail": "1",
      "last_http_success": "1",
      "url": "https://test.url"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[WebhookListModel](#schemawebhooklistmodel)|HTTP call succeeded.|
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

### Ping Hook

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
          String url = "https://api.crosoftware.net/v0/hooks/{hook_id}/ping";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/v0/hooks/{hook_id}/ping \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/hooks/{hook_id}/ping',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.get 'https://api.crosoftware.net/v0/hooks/{hook_id}/ping',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.get('https://api.crosoftware.net/v0/hooks/{hook_id}/ping', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/hooks/{hook_id}/ping");
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

`GET /hooks/{hook_id}/ping`

<a id="opIdget_hooks_by_id_ping"></a>

Ping webhook by id.

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`hook_id`|path|integer(int64)|true|Webhook identifier.|

> Example responses

> 200 Response

```json
{
  "delivery_id": "1",
  "http_status": 200
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[WebhookPingResultModel](#schemawebhookpingresultmodel)|HTTP call succeeded.|
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
          String url = "https://api.crosoftware.net/v0/hooks/{hook_id}";

          // Headers
          client.Headers.Add("authorization", "bearer VGhlIGxhenkgYnJvd24gZm94");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/v0/hooks/{hook_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'authorization: bearer VGhlIGxhenkgYnJvd24gZm94' \
  -H 'x-tenant-id: 1'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'authorization':'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id':'1'

};

$.ajax({
  url: 'https://api.crosoftware.net/v0/hooks/{hook_id}',
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
  'authorization' => 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id' => '1'
}

result = RestClient.patch 'https://api.crosoftware.net/v0/hooks/{hook_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'authorization': 'bearer VGhlIGxhenkgYnJvd24gZm94',
  'x-tenant-id': '1'
}

r = requests.patch('https://api.crosoftware.net/v0/hooks/{hook_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/v0/hooks/{hook_id}");
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
    "Customer"
  ],
  "secret": "<Secret>",
  "url": "https://test.url"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`authorization`|header|string|false|Authorization header.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`hook_id`|path|integer(int64)|true|Webhook identifier.|
|`body`|body|[UpdateWebhookModel](#schemaupdatewebhookmodel)|true||

> Example responses

> 200 Response

```json
{
  "events": [
    "Customer"
  ],
  "secret": "<Secret>",
  "url": "https://test.url"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[UpdateWebhookModel](#schemaupdatewebhookmodel)|HTTP call succeeded.|
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
    "deleted": true,
    "id": 1,
    "is_default": true,
    "location_id": 1,
    "name": "John Doe",
    "quantity": 3,
    "require_numbers": true,
    "weight": 10192.77
  },
  "asset_type_id": 1,
  "cluster": 1,
  "customer_id": 1,
  "description": "A user entered/human readable text description.",
  "dispatched_on": "2049-10-31T11:32:38.390000",
  "id": 1,
  "is_returned": true,
  "last_activity_on": "2049-10-31T11:32:38.390000",
  "last_rental_invoice_on": "2049-10-31T11:32:38.390000",
  "latitude": 56.2,
  "location": {
    "id": 1,
    "is_active": true,
    "name": "CRO Scrap"
  },
  "location_id": 1,
  "longitude": 128.1,
  "number": "+1 (360) 123-6543",
  "quantity": 3,
  "returned_on": "2049-10-31T11:32:38.390000"
}

```

<a id="schemaassetmodel"></a>

|Name|Type|Description|
|---|---|---|
|`asset_type`|[AssetTypeModel](#schemaassettypemodel)|-|
|`asset_type_id`|integer(int64)|Selected asset for the job (job types 'D', 'L', 'E').|
|`cluster`|integer(int64)|Cluster id.|
|`customer_id`|integer(int64)|Customer identifier.|
|`description`|string|Free-form text description.|
|`dispatched_on`|string(DateTime)|Time the asset was dispatched.|
|`id`|integer(int64)|Resource identifier.|
|`is_returned`|boolean|Is asset returned.|
|`last_activity_on`|string(DateTime)|Last activity time.|
|`last_rental_invoice_on`|string(DateTime)|Last rental invoice time.|
|`latitude`|number(float)|Latitude.|
|`location`|[LocationModel](#schemalocationmodel)|-|
|`location_id`|integer(int64)|Location identifier.|
|`longitude`|number(float)|longitude.|
|`number`|string(PhoneNumber)|Phone number (free text).|
|`quantity`|integer(int64)|Asset quantity.|
|`returned_on`|string(DateTime)|Time the asset was returned.|

<h2 id="tocSassettypemodel">AssetTypeModel</h2>

```json
{
  "deleted": true,
  "id": 1,
  "is_default": true,
  "location_id": 1,
  "name": "John Doe",
  "quantity": 3,
  "require_numbers": true,
  "weight": 10192.77
}

```

<a id="schemaassettypemodel"></a>

|Name|Type|Description|
|---|---|---|
|`deleted`|boolean|Is record deleted (soft delete).|
|`id`|integer(int64)|Resource identifier.|
|`is_default`|boolean|Is asset the default asset.|
|`location_id`|integer(int64)|Location identifier.|
|`name`|string|Name (free text).|
|`quantity`|integer(int64)|Asset type quantity.|
|`require_numbers`|boolean|Require asset numbers.|
|`weight`|number(float)|-|

<h2 id="tocScreatecustomeraddressmodel">CreateCustomerAddressModel</h2>

```json
{
  "country": "US",
  "is_billing": true,
  "is_shipping": true,
  "latitude": 56.2,
  "line_1": "123 Some St.",
  "line_2": "Office #34",
  "line_3": "Box #2",
  "line_4": "Drop in Blue Box",
  "locality": "Sequim",
  "longitude": 128.1,
  "postcode": "98368",
  "region": "WA"
}

```

<a id="schemacreatecustomeraddressmodel"></a>

|Name|Type|Description|
|---|---|---|
|`country`|string|Country code (ISO 3166-1 alpha 2).|
|`is_billing`|boolean|If true, this is the customer's billing address.|
|`is_shipping`|boolean|Customer's shipping address if true.|
|`latitude`|number(float)|Latitude.|
|`line_1`|string|Street address.|
|`line_2`|string|Street address line 2.|
|`line_3`|string|Street address line 3.|
|`line_4`|string|Street address line 4 (doubles as county).|
|`locality`|string|Address locality (e.g. city).|
|`longitude`|number(float)|longitude.|
|`postcode`|string|Postal code (may include letters and symbols).|
|`region`|string|Address region (e.g. state).|

<h2 id="tocScreatecustomercontactmodel">CreateCustomerContactModel</h2>

```json
{
  "email": "john@crosoftware.net, jane@crosoftware.net",
  "fax": "+1 (360) 123-6543",
  "name": "John Doe",
  "notify_on_acknowledged_request": true,
  "notify_on_completed_request": true,
  "notify_on_dispatched_request": true,
  "notify_on_failed_request": true,
  "notify_on_new_request": true,
  "number": "+1 (360) 123-6543"
}

```

<a id="schemacreatecustomercontactmodel"></a>

|Name|Type|Description|
|---|---|---|
|`email`|string(Email)|Email address comma-separated list.|
|`fax`|string(PhoneNumber)|Fax number (free text).|
|`name`|string|Name (free text).|
|`notify_on_acknowledged_request`|boolean|Notify on acknowledge request.|
|`notify_on_completed_request`|boolean|Notify on completed request.|
|`notify_on_dispatched_request`|boolean|Notify on dispatched request.|
|`notify_on_failed_request`|boolean|Notify on failed request.|
|`notify_on_new_request`|boolean|Notify on new request.|
|`number`|string(PhoneNumber)|Phone number (free text).|

<h2 id="tocScreatecustomerlocationmodel">CreateCustomerLocationModel</h2>

```json
{
  "is_commercial": true,
  "note": "A note about something",
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "suspension_id": 1
}

```

<a id="schemacreatecustomerlocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`is_commercial`|boolean|Commercial address if true, private if false.|
|`note`|string|Notes (free text).|
|`reference_number`|string|Reference number (free text).|
|`renewal_date`|string(DateTime)|Renewal date.|
|`sales_rep`|string|Name of sales representative.|
|`suspension_id`|integer(int64)|Suspension identifier.|

<h2 id="tocScreatecustomermodel">CreateCustomerModel</h2>

```json
{
  "addresses": [
    {
      "country": "US",
      "is_billing": true,
      "is_shipping": true,
      "latitude": 56.2,
      "line_1": "123 Some St.",
      "line_2": "Office #34",
      "line_3": "Box #2",
      "line_4": "Drop in Blue Box",
      "locality": "Sequim",
      "longitude": 128.1,
      "postcode": "98368",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "is_commercial": true,
  "name": "John Doe",
  "note": "A note about something",
  "parent_id": 0,
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "suspension_id": 1
}

```

<a id="schemacreatecustomermodel"></a>

|Name|Type|Description|
|---|---|---|
|`addresses`|array[[CreateCustomerAddressModel](#schemacreatecustomeraddressmodel)]|-|
|`contacts`|array[[CreateCustomerContactModel](#schemacreatecustomercontactmodel)]|-|
|`is_commercial`|boolean|Commercial address if true, private if false.|
|`name`|string|Name (free text).|
|`note`|string|Notes (free text).|
|`parent_id`|integer(int64)|Parent record identifier.|
|`reference_number`|string|Reference number (free text).|
|`renewal_date`|string(DateTime)|Renewal date.|
|`sales_rep`|string|Name of sales representative.|
|`suspension_id`|integer(int64)|Suspension identifier.|

<h2 id="tocScreatewebhookmodel">CreateWebhookModel</h2>

```json
{
  "events": [
    "Customer"
  ],
  "secret": "<Secret>",
  "url": "https://test.url"
}

```

<a id="schemacreatewebhookmodel"></a>

|Name|Type|Description|
|---|---|---|
|`events`|array[string]|Hook event.|
|`secret`|string|Response body HMAC signing key.|
|`url`|string(Url)|Callback URL.|

<h2 id="tocScustomeraddresslistmodel">CustomerAddressListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "address_id": 1,
      "country": "US",
      "is_billing": true,
      "is_physical": true,
      "is_shipping": true,
      "latitude": 56.2,
      "line_1": "123 Some St.",
      "line_2": "Office #34",
      "line_3": "Box #2",
      "line_4": "Drop in Blue Box",
      "locality": "Sequim",
      "longitude": 128.1,
      "postcode": "98368",
      "region": "WA"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schemacustomeraddresslistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[CustomerAddressModel](#schemacustomeraddressmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocScustomeraddressmodel">CustomerAddressModel</h2>

```json
{
  "address_id": 1,
  "country": "US",
  "is_billing": true,
  "is_physical": true,
  "is_shipping": true,
  "latitude": 56.2,
  "line_1": "123 Some St.",
  "line_2": "Office #34",
  "line_3": "Box #2",
  "line_4": "Drop in Blue Box",
  "locality": "Sequim",
  "longitude": 128.1,
  "postcode": "98368",
  "region": "WA"
}

```

<a id="schemacustomeraddressmodel"></a>

|Name|Type|Description|
|---|---|---|
|`address_id`|integer(int64)|Customer address identifier.|
|`country`|string|Country code (ISO 3166-1 alpha 2).|
|`is_billing`|boolean|If true, this is the customer's billing address.|
|`is_physical`|boolean|Physical address if true.|
|`is_shipping`|boolean|Customer's shipping address if true.|
|`latitude`|number(float)|Latitude.|
|`line_1`|string|Street address.|
|`line_2`|string|Street address line 2.|
|`line_3`|string|Street address line 3.|
|`line_4`|string|Street address line 4 (doubles as county).|
|`locality`|string|Address locality (e.g. city).|
|`longitude`|number(float)|longitude.|
|`postcode`|string|Postal code (may include letters and symbols).|
|`region`|string|Address region (e.g. state).|

<h2 id="tocScustomercontactlistmodel">CustomerContactListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "contact_id": 1,
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schemacustomercontactlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[CustomerContactModel](#schemacustomercontactmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocScustomercontactmodel">CustomerContactModel</h2>

```json
{
  "contact_id": 1,
  "email": "john@crosoftware.net, jane@crosoftware.net",
  "fax": "+1 (360) 123-6543",
  "name": "John Doe",
  "notify_on_acknowledged_request": true,
  "notify_on_completed_request": true,
  "notify_on_dispatched_request": true,
  "notify_on_failed_request": true,
  "notify_on_new_request": true,
  "number": "+1 (360) 123-6543"
}

```

<a id="schemacustomercontactmodel"></a>

|Name|Type|Description|
|---|---|---|
|`contact_id`|integer(int64)|Customer contact identifier.|
|`email`|string(Email)|Email address comma-separated list.|
|`fax`|string(PhoneNumber)|Fax number (free text).|
|`name`|string|Name (free text).|
|`notify_on_acknowledged_request`|boolean|Notify on acknowledge request.|
|`notify_on_completed_request`|boolean|Notify on completed request.|
|`notify_on_dispatched_request`|boolean|Notify on dispatched request.|
|`notify_on_failed_request`|boolean|Notify on failed request.|
|`notify_on_new_request`|boolean|Notify on new request.|
|`number`|string(PhoneNumber)|Phone number (free text).|

<h2 id="tocScustomerlistmodel">CustomerListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "addresses": [
        {
          "country": "US",
          "is_billing": true,
          "is_shipping": true,
          "latitude": 56.2,
          "line_1": "123 Some St.",
          "line_2": "Office #34",
          "line_3": "Box #2",
          "line_4": "Drop in Blue Box",
          "locality": "Sequim",
          "longitude": 128.1,
          "postcode": "98368",
          "region": "WA"
        }
      ],
      "contacts": [
        {
          "email": "john@crosoftware.net, jane@crosoftware.net",
          "fax": "+1 (360) 123-6543",
          "name": "John Doe",
          "notify_on_acknowledged_request": true,
          "notify_on_completed_request": true,
          "notify_on_dispatched_request": true,
          "notify_on_failed_request": true,
          "notify_on_new_request": true,
          "number": "+1 (360) 123-6543"
        }
      ],
      "customer_id": 1,
      "is_commercial": true,
      "name": "John Doe",
      "note": "A note about something",
      "parent_id": 0,
      "reference_number": "A140",
      "renewal_date": "2049-10-31T11:32:38.390000",
      "sales_rep": "Jane Johnson",
      "suspension_id": 1
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schemacustomerlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[CustomerModel](#schemacustomermodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocScustomerlocationlistmodel">CustomerLocationListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "id": 1,
      "is_commercial": true,
      "note": "A note about something",
      "reference_number": "A140",
      "renewal_date": "2049-10-31T11:32:38.390000",
      "sales_rep": "Jane Johnson",
      "suspension_id": 1
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schemacustomerlocationlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[CustomerLocationModel](#schemacustomerlocationmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocScustomerlocationmodel">CustomerLocationModel</h2>

```json
{
  "id": 1,
  "is_commercial": true,
  "note": "A note about something",
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "suspension_id": 1
}

```

<a id="schemacustomerlocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`id`|integer(int64)|Resource identifier.|
|`is_commercial`|boolean|Commercial address if true, private if false.|
|`note`|string|Notes (free text).|
|`reference_number`|string|Reference number (free text).|
|`renewal_date`|string(DateTime)|Renewal date.|
|`sales_rep`|string|Name of sales representative.|
|`suspension_id`|integer(int64)|Suspension identifier.|

<h2 id="tocScustomermodel">CustomerModel</h2>

```json
{
  "addresses": [
    {
      "country": "US",
      "is_billing": true,
      "is_shipping": true,
      "latitude": 56.2,
      "line_1": "123 Some St.",
      "line_2": "Office #34",
      "line_3": "Box #2",
      "line_4": "Drop in Blue Box",
      "locality": "Sequim",
      "longitude": 128.1,
      "postcode": "98368",
      "region": "WA"
    }
  ],
  "contacts": [
    {
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "customer_id": 1,
  "is_commercial": true,
  "name": "John Doe",
  "note": "A note about something",
  "parent_id": 0,
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "suspension_id": 1
}

```

<a id="schemacustomermodel"></a>

|Name|Type|Description|
|---|---|---|
|`addresses`|array[[CreateCustomerAddressModel](#schemacreatecustomeraddressmodel)]|-|
|`contacts`|array[[CreateCustomerContactModel](#schemacreatecustomercontactmodel)]|-|
|`customer_id`|integer(int64)|Customer identifier.|
|`is_commercial`|boolean|Commercial address if true, private if false.|
|`name`|string|Name (free text).|
|`note`|string|Notes (free text).|
|`parent_id`|integer(int64)|Parent record identifier.|
|`reference_number`|string|Reference number (free text).|
|`renewal_date`|string(DateTime)|Renewal date.|
|`sales_rep`|string|Name of sales representative.|
|`suspension_id`|integer(int64)|Suspension identifier.|

<h2 id="tocSdriverlistmodel">DriverListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "address": "123 Some St.",
      "can_convert_to_group": true,
      "can_create_requests": true,
      "can_edit_requests": true,
      "can_reposition_asset": true,
      "city": "Sequim",
      "disable_shift_tracking": true,
      "email": "test@crosoftware.net",
      "id": 1,
      "license_number": "AJONDO251Z",
      "location_id": 1,
      "name": "John Doe",
      "phone_number": "+1 (360) 123-6543",
      "state": "WA",
      "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f",
      "zip": "98368"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schemadriverlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[DriverModel](#schemadrivermodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocSdrivermodel">DriverModel</h2>

```json
{
  "address": "123 Some St.",
  "can_convert_to_group": true,
  "can_create_requests": true,
  "can_edit_requests": true,
  "can_reposition_asset": true,
  "city": "Sequim",
  "disable_shift_tracking": true,
  "email": "test@crosoftware.net",
  "id": 1,
  "license_number": "AJONDO251Z",
  "location_id": 1,
  "name": "John Doe",
  "phone_number": "+1 (360) 123-6543",
  "state": "WA",
  "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f",
  "zip": "98368"
}

```

<a id="schemadrivermodel"></a>

|Name|Type|Description|
|---|---|---|
|`address`|string|Street address.|
|`can_convert_to_group`|boolean|Can driver convert to group.|
|`can_create_requests`|boolean|Can driver create requests.|
|`can_edit_requests`|boolean|Can driver edit requests.|
|`can_reposition_asset`|boolean|Can driver reposition asset.|
|`city`|string|Address locality (e.g. city).|
|`disable_shift_tracking`|boolean|Disable shift tracking.|
|`email`|string(Email)|Email address.|
|`id`|integer(int64)|Resource identifier.|
|`license_number`|string|Driver's license number.|
|`location_id`|integer(int64)|Location identifier.|
|`name`|string|Name (free text).|
|`phone_number`|string(PhoneNumber)|Phone number (free text).|
|`state`|string|Address region (e.g. state).|
|`third_party_hauler_id`|string(Uuid)|Third party hauler identifier.|
|`zip`|string|Postal code (may include letters and symbols).|

<h2 id="tocSdumpdestinationlistmodel">DumpDestinationListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "address": "123 Some St.",
      "city": "Sequim",
      "contact_email": "test@crosoftware.net",
      "contact_name": "John Doe",
      "contact_phone": "+1 (360) 123-6543",
      "description": "A user entered/human readable text description.",
      "id": 1,
      "is_holding_yard": true,
      "latitude": 56.2,
      "location_id": 1,
      "longitude": 128.1,
      "state": "WA",
      "zip": "98368"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schemadumpdestinationlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[DumpDestinationModel](#schemadumpdestinationmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocSdumpdestinationmodel">DumpDestinationModel</h2>

```json
{
  "address": "123 Some St.",
  "city": "Sequim",
  "contact_email": "test@crosoftware.net",
  "contact_name": "John Doe",
  "contact_phone": "+1 (360) 123-6543",
  "description": "A user entered/human readable text description.",
  "id": 1,
  "is_holding_yard": true,
  "latitude": 56.2,
  "location_id": 1,
  "longitude": 128.1,
  "state": "WA",
  "zip": "98368"
}

```

<a id="schemadumpdestinationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`address`|string|Street address.|
|`city`|string|Address locality (e.g. city).|
|`contact_email`|string(Email)|Email address.|
|`contact_name`|string|Name (free text).|
|`contact_phone`|string(PhoneNumber)|Phone number (free text).|
|`description`|string|Free-form text description.|
|`id`|integer(int64)|Resource identifier.|
|`is_holding_yard`|boolean|Location is holding yard.|
|`latitude`|number(float)|Latitude.|
|`location_id`|integer(int64)|Location identifier.|
|`longitude`|number(float)|longitude.|
|`state`|string|Address region (e.g. state).|
|`zip`|string|Postal code (may include letters and symbols).|

<h2 id="tocSerrorresponsemodel">ErrorResponseModel</h2>

```json
{
  "detail": "Something happened that caused an error.",
  "explanation": "An error has occurred because...",
  "title": "Failed to load data"
}

```

<a id="schemaerrorresponsemodel"></a>

|Name|Type|Description|
|---|---|---|
|`detail`|string|Error message details.|
|`explanation`|string|Error message general explanation.|
|`title`|string|Error message data identifier.|

<h2 id="tocSgpseventcoordsprofilemodel">GpsEventCoordsProfileModel</h2>

```json
{
  "heading": 0,
  "latitude": 56.2,
  "longitude": 128.1,
  "speed": 10.1
}

```

<a id="schemagpseventcoordsprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`heading`|number(float)|Direction of travel at time of measurement.|
|`latitude`|number(float)|Latitude.|
|`longitude`|number(float)|longitude.|
|`speed`|number(float)|Rate of travel at time of measurement.|

<h2 id="tocSgpseventlocationprofilemodel">GpsEventLocationProfileModel</h2>

```json
{
  "coords": {
    "heading": 0,
    "latitude": 56.2,
    "longitude": 128.1,
    "speed": 10.1
  },
  "timestamp": "2049-10-31T11:32:38.390000"
}

```

<a id="schemagpseventlocationprofilemodel"></a>

|Name|Type|Description|
|---|---|---|
|`coords`|[GpsEventCoordsProfileModel](#schemagpseventcoordsprofilemodel)|-|
|`timestamp`|string(DateTime)|Timestamp of creation (must be in past).|

<h2 id="tocSgpseventprofilemodel">GpsEventProfileModel</h2>

```json
{
  "location": {
    "coords": {
      "heading": 0,
      "latitude": 56.2,
      "longitude": 128.1,
      "speed": 10.1
    },
    "timestamp": "2049-10-31T11:32:38.390000"
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
  "bearing": 0,
  "created_on": "2049-10-31T11:32:38.390000",
  "device_name": "John Doe",
  "driver_id": 1,
  "id": 1,
  "latitude": 56.2,
  "longitude": 128.1,
  "truck_id": 1,
  "velocity": 10.1
}

```

<a id="schemagpsstopmodel"></a>

|Name|Type|Description|
|---|---|---|
|`bearing`|number(float)|Direction of travel at time of measurement.|
|`created_on`|string(DateTime)|Timestamp of creation (must be in past).|
|`device_name`|string|Name (free text).|
|`driver_id`|integer(int64)|Driver identifier.|
|`id`|integer(int64)|Resource identifier.|
|`latitude`|number(float)|Latitude.|
|`longitude`|number(float)|longitude.|
|`truck_id`|integer(int64)|Truck identifier.|
|`velocity`|number(float)|Rate of travel at time of measurement.|

<h2 id="tocSjoblistmodel">JobListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "arrived_at_dest": "2049-10-31T11:32:38.390000",
      "arrived_on": "2049-10-31T11:32:38.390000",
      "asset": {
        "asset_type": {
          "deleted": true,
          "id": 1,
          "is_default": true,
          "location_id": 1,
          "name": "John Doe",
          "quantity": 3,
          "require_numbers": true,
          "weight": 10192.77
        },
        "asset_type_id": 1,
        "cluster": 1,
        "customer_id": 1,
        "description": "A user entered/human readable text description.",
        "dispatched_on": "2049-10-31T11:32:38.390000",
        "id": 1,
        "is_returned": true,
        "last_activity_on": "2049-10-31T11:32:38.390000",
        "last_rental_invoice_on": "2049-10-31T11:32:38.390000",
        "latitude": 56.2,
        "location": {
          "id": 1,
          "is_active": true,
          "name": "CRO Scrap"
        },
        "location_id": 1,
        "longitude": 128.1,
        "number": "+1 (360) 123-6543",
        "quantity": 3,
        "returned_on": "2049-10-31T11:32:38.390000"
      },
      "asset_dropped": 101,
      "asset_id": 1,
      "asset_quantity": 1,
      "asset_type": {
        "deleted": true,
        "id": 1,
        "is_default": true,
        "location_id": 1,
        "name": "John Doe",
        "quantity": 3,
        "require_numbers": true,
        "weight": 10192.77
      },
      "asset_type_id": 1,
      "completed_by": 1,
      "completed_by_driver": true,
      "completed_on": "2049-10-31T11:32:38.390000",
      "confirmed_on": "2049-10-31T11:32:38.390000",
      "created_by_id": 1,
      "customer": {
        "addresses": [
          {
            "country": "US",
            "is_billing": true,
            "is_shipping": true,
            "latitude": 56.2,
            "line_1": "123 Some St.",
            "line_2": "Office #34",
            "line_3": "Box #2",
            "line_4": "Drop in Blue Box",
            "locality": "Sequim",
            "longitude": 128.1,
            "postcode": "98368",
            "region": "WA"
          }
        ],
        "contacts": [
          {
            "email": "john@crosoftware.net, jane@crosoftware.net",
            "fax": "+1 (360) 123-6543",
            "name": "John Doe",
            "notify_on_acknowledged_request": true,
            "notify_on_completed_request": true,
            "notify_on_dispatched_request": true,
            "notify_on_failed_request": true,
            "notify_on_new_request": true,
            "number": "+1 (360) 123-6543"
          }
        ],
        "customer_id": 1,
        "is_commercial": true,
        "name": "John Doe",
        "note": "A note about something",
        "parent_id": 0,
        "reference_number": "A140",
        "renewal_date": "2049-10-31T11:32:38.390000",
        "sales_rep": "Jane Johnson",
        "suspension_id": 1
      },
      "customer_id": 1,
      "customer_notes": "A note entered by a customer",
      "desired_asset_desc": "A note entered by a driver",
      "dispatch_priority": "H",
      "dispatched_by_route": 1,
      "dispatched_on": "2049-10-31T11:32:38.390000",
      "dispatcher_notes": "A note entered by a dispatcher.",
      "do_confirm": true,
      "driver_notes": "A note entered by a driver.",
      "dump_location": {
        "id": 1,
        "is_active": true,
        "name": "CRO Scrap"
      },
      "dump_location_id": 2,
      "dumped_on": "2049-10-31T11:32:38.390000",
      "end_time": "2049-10-31T11:32:38.390000",
      "fail_reason": "A failure description selected by a driver.",
      "final_location": {
        "id": 1,
        "is_active": true,
        "name": "CRO Scrap"
      },
      "final_location_id": 1,
      "flags": "Notes about a job.",
      "invoice_notes": "Notes from a billing invoice",
      "is_completed": true,
      "is_declined": true,
      "is_deleted": true,
      "is_failed": true,
      "job_group_id": 1,
      "location_id": 1,
      "merged_with_route": 1,
      "original_schedule_date": "2049-10-31T11:32:38.390000",
      "pickup_date": "2049-10-31T11:32:38.390000",
      "priority": -3,
      "reference_number": "A140",
      "requested_on": "2049-10-31T11:32:38.390000",
      "require_image": true,
      "require_material": true,
      "require_signature": true,
      "require_weights": true,
      "scale_ticket": "A5100",
      "schedule_date": "2049-10-31T11:32:38.390000",
      "start_location": {
        "id": 1,
        "is_active": true,
        "name": "CRO Scrap"
      },
      "start_location_id": 1,
      "start_time": "2049-10-31T11:32:38.390000",
      "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f",
      "times_failed": 2,
      "times_rolled_over": 1,
      "truck_id": 1,
      "type": "D",
      "weighed_on": "2049-10-31T11:32:38.390000"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schemajoblistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[JobModel](#schemajobmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocSjobmodel">JobModel</h2>

```json
{
  "arrived_at_dest": "2049-10-31T11:32:38.390000",
  "arrived_on": "2049-10-31T11:32:38.390000",
  "asset": {
    "asset_type": {
      "deleted": true,
      "id": 1,
      "is_default": true,
      "location_id": 1,
      "name": "John Doe",
      "quantity": 3,
      "require_numbers": true,
      "weight": 10192.77
    },
    "asset_type_id": 1,
    "cluster": 1,
    "customer_id": 1,
    "description": "A user entered/human readable text description.",
    "dispatched_on": "2049-10-31T11:32:38.390000",
    "id": 1,
    "is_returned": true,
    "last_activity_on": "2049-10-31T11:32:38.390000",
    "last_rental_invoice_on": "2049-10-31T11:32:38.390000",
    "latitude": 56.2,
    "location": {
      "id": 1,
      "is_active": true,
      "name": "CRO Scrap"
    },
    "location_id": 1,
    "longitude": 128.1,
    "number": "+1 (360) 123-6543",
    "quantity": 3,
    "returned_on": "2049-10-31T11:32:38.390000"
  },
  "asset_dropped": 101,
  "asset_id": 1,
  "asset_quantity": 1,
  "asset_type": {
    "deleted": true,
    "id": 1,
    "is_default": true,
    "location_id": 1,
    "name": "John Doe",
    "quantity": 3,
    "require_numbers": true,
    "weight": 10192.77
  },
  "asset_type_id": 1,
  "completed_by": 1,
  "completed_by_driver": true,
  "completed_on": "2049-10-31T11:32:38.390000",
  "confirmed_on": "2049-10-31T11:32:38.390000",
  "created_by_id": 1,
  "customer": {
    "addresses": [
      {
        "country": "US",
        "is_billing": true,
        "is_shipping": true,
        "latitude": 56.2,
        "line_1": "123 Some St.",
        "line_2": "Office #34",
        "line_3": "Box #2",
        "line_4": "Drop in Blue Box",
        "locality": "Sequim",
        "longitude": 128.1,
        "postcode": "98368",
        "region": "WA"
      }
    ],
    "contacts": [
      {
        "email": "john@crosoftware.net, jane@crosoftware.net",
        "fax": "+1 (360) 123-6543",
        "name": "John Doe",
        "notify_on_acknowledged_request": true,
        "notify_on_completed_request": true,
        "notify_on_dispatched_request": true,
        "notify_on_failed_request": true,
        "notify_on_new_request": true,
        "number": "+1 (360) 123-6543"
      }
    ],
    "customer_id": 1,
    "is_commercial": true,
    "name": "John Doe",
    "note": "A note about something",
    "parent_id": 0,
    "reference_number": "A140",
    "renewal_date": "2049-10-31T11:32:38.390000",
    "sales_rep": "Jane Johnson",
    "suspension_id": 1
  },
  "customer_id": 1,
  "customer_notes": "A note entered by a customer",
  "desired_asset_desc": "A note entered by a driver",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2049-10-31T11:32:38.390000",
  "dispatcher_notes": "A note entered by a dispatcher.",
  "do_confirm": true,
  "driver_notes": "A note entered by a driver.",
  "dump_location": {
    "id": 1,
    "is_active": true,
    "name": "CRO Scrap"
  },
  "dump_location_id": 2,
  "dumped_on": "2049-10-31T11:32:38.390000",
  "end_time": "2049-10-31T11:32:38.390000",
  "fail_reason": "A failure description selected by a driver.",
  "final_location": {
    "id": 1,
    "is_active": true,
    "name": "CRO Scrap"
  },
  "final_location_id": 1,
  "flags": "Notes about a job.",
  "invoice_notes": "Notes from a billing invoice",
  "is_completed": true,
  "is_declined": true,
  "is_deleted": true,
  "is_failed": true,
  "job_group_id": 1,
  "location_id": 1,
  "merged_with_route": 1,
  "original_schedule_date": "2049-10-31T11:32:38.390000",
  "pickup_date": "2049-10-31T11:32:38.390000",
  "priority": -3,
  "reference_number": "A140",
  "requested_on": "2049-10-31T11:32:38.390000",
  "require_image": true,
  "require_material": true,
  "require_signature": true,
  "require_weights": true,
  "scale_ticket": "A5100",
  "schedule_date": "2049-10-31T11:32:38.390000",
  "start_location": {
    "id": 1,
    "is_active": true,
    "name": "CRO Scrap"
  },
  "start_location_id": 1,
  "start_time": "2049-10-31T11:32:38.390000",
  "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f",
  "times_failed": 2,
  "times_rolled_over": 1,
  "truck_id": 1,
  "type": "D",
  "weighed_on": "2049-10-31T11:32:38.390000"
}

```

<a id="schemajobmodel"></a>

|Name|Type|Description|
|---|---|---|
|`arrived_at_dest`|string(DateTime)|Entered by driver for dispatcher and customer. Asset arrival at destination time. Only applicable for jobs with a valid dump destination.|
|`arrived_on`|string(DateTime)|Drive start time entered by driver for dispatcher and customer (arrived at job slider).|
|`asset`|[AssetModel](#schemaassetmodel)|-|
|`asset_dropped`|integer(int64)|Reference to deployed asset entered by driver for customer, dispatcher applicable to job types 'D', 'E'.|
|`asset_id`|integer(int64)|Job asset identifier. Applicable to job types 'E', 'P', 'R'.|
|`asset_quantity`|integer(int64)|How many assets are being serviced within a cluster (for jobs assigned to an asset cluster). For jobs dispatched by routes, or manually dispatched route stops, this value is 0 or 1.|
|`asset_type`|[AssetTypeModel](#schemaassettypemodel)|-|
|`asset_type_id`|integer(int64)|Selected asset for the job (job types 'D', 'L', 'E').|
|`completed_by`|integer(int64)|Dispatcher or driver id.|
|`completed_by_driver`|boolean|If TRUE, completed by driver. If FALSE, completed by dispatcher.|
|`completed_on`|string(DateTime)|Job completion time.|
|`confirmed_on`|string(DateTime)|Job confirmation date.|
|`created_by_id`|integer(int64)|Customer, dispatcher, or driver id.|
|`customer`|[CustomerModel](#schemacustomermodel)|-|
|`customer_id`|integer(int64)|Customer identifier.|
|`customer_notes`|string|Notes entered by customers to communicate with dispatchers.|
|`desired_asset_desc`|string|Free-form text entered by dispatchers and drivers to be used as the future asset description.|
|`dispatch_priority`|string|Entered by dispatchers to determine dispatch order.|
|`dispatched_by_route`|integer(int64)|Route id of dispatching route (or NULL if not dispatched by a route).|
|`dispatched_on`|string(DateTime)|Time the job is assigned to a truck.|
|`dispatcher_notes`|string|Entered by dispatchers, read by drivers and dispatchers.|
|`do_confirm`|boolean|Tell dispatcher that a customer should be contacted before job is dispatched.|
|`driver_notes`|string|Entered by drivers when completing or failing a job for dispatchers.|
|`dump_location`|[LocationModel](#schemalocationmodel)|-|
|`dump_location_id`|integer(int64)|Asset or asset cluster dump location identifier (e.g. trash bin needs dumped before returning from customer).|
|`dumped_on`|string(DateTime)|Dump request completion date.|
|`end_time`|string(DateTime)|Future estimated time of job completion.|
|`fail_reason`|string|Failure description selected by a driver for use by dispatchers.|
|`final_location`|[LocationModel](#schemalocationmodel)|-|
|`final_location_id`|integer(int64)|Final location identifier. Used by dispatchers for prioritizing jobs. Used by drivers to know where to leave the asset on job completion.|
|`flags`|string|Job notes.|
|`invoice_notes`|string|Invoice notes from the billing system.|
|`is_completed`|boolean|Job completion flag set by dispatchers and drivers.|
|`is_declined`|boolean|Job completion flag set by dispatchers and drivers.|
|`is_deleted`|boolean|Indicates whether job is still valid.|
|`is_failed`|boolean|Set by drivers and dispatchers to indicate a failed job.|
|`job_group_id`|integer(int64)|Job group identifier for group jobs (vs service, exchange, etc.).|
|`location_id`|integer(int64)|Location identifier.|
|`merged_with_route`|integer(int64)|Assigned by dispatchers for dispatchers and drivers.|
|`original_schedule_date`|string(DateTime)|Original scheduling date.|
|`pickup_date`|string(DateTime)|A pickup job is scheduled for this date upon job completion. If the asset or cluster is assigned to a route stop, the route stop will be deleted. Must be in the future.|
|`priority`|integer(int64)|Assigned by dispatchers for job order completion determination for drivers.|
|`reference_number`|string|Reference number (free text).|
|`requested_on`|string(DateTime)|Requested date.|
|`require_image`|boolean|Set by dispatchers and drivers, requires drivers to upload one or more job images before completion.|
|`require_material`|boolean|Set by dispatchers and drivers, requires drivers to set a material before completing a job.|
|`require_signature`|boolean|Set by dispatchers and drivers, requires drivers to get a customer signature before job completion.|
|`require_weights`|boolean|Set by disptachers and drivers, requires drivers to set material weights before job completion.|
|`scale_ticket`|string|Scale ticket.|
|`schedule_date`|string(DateTime)|Scheduled job completion date.|
|`start_location`|[LocationModel](#schemalocationmodel)|-|
|`start_location_id`|integer(int64)|Pickup location for asset or asset cluster Set by dispatchers and drivers for drivers.|
|`start_time`|string(DateTime)|Time customer has requested job start, set by dispatchers for dispatchers and drivers.|
|`third_party_hauler_id`|string(Uuid)|Third party hauler identifier.|
|`times_failed`|integer(int64)|Number of times a job has been attempted and failed.|
|`times_rolled_over`|integer(int64)|Tracks job age in days for dispatchers.|
|`truck_id`|integer(int64)|Truck identifier.|
|`type`|string|Set by dispatchers and customers. Represents physical actions to execute on job start.|
|`weighed_on`|string(DateTime)|Time of truck weight entry.|

<h2 id="tocSlocationlistmodel">LocationListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "id": 1,
      "is_active": true,
      "name": "CRO Scrap"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schemalocationlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[LocationModel](#schemalocationmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocSlocationmodel">LocationModel</h2>

```json
{
  "id": 1,
  "is_active": true,
  "name": "CRO Scrap"
}

```

<a id="schemalocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`id`|integer(int64)|Location identifier.|
|`is_active`|boolean|Records marked inactive are treated as deleted (soft delete).|
|`name`|string|Name for a location.|

<h2 id="tocSmateriallistmodel">MaterialListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "created_on": "2049-10-31T11:32:38.390000",
      "description": "A user entered/human readable text description.",
      "factor": 1.1,
      "group_description": "A user entered/human readable text description.",
      "id": 1,
      "line_item_id": 1,
      "uom": "A user entered/human readable description of the UOM."
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schemamateriallistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[MaterialModel](#schemamaterialmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocSmaterialmodel">MaterialModel</h2>

```json
{
  "created_on": "2049-10-31T11:32:38.390000",
  "description": "A user entered/human readable text description.",
  "factor": 1.1,
  "group_description": "A user entered/human readable text description.",
  "id": 1,
  "line_item_id": 1,
  "uom": "A user entered/human readable description of the UOM."
}

```

<a id="schemamaterialmodel"></a>

|Name|Type|Description|
|---|---|---|
|`created_on`|string(DateTime)|Timestamp of creation (must be in past).|
|`description`|string|Free-form text description.|
|`factor`|number(float)|-|
|`group_description`|string|Free-form text description.|
|`id`|integer(int64)|Resource identifier.|
|`line_item_id`|integer(int64)|Resource identifier.|
|`uom`|string|Unit of Measure.|

<h2 id="tocStenantlistmodel">TenantListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "address": "123 Some St.",
      "city": "Sequim",
      "code": "BESTSCRAP",
      "created_on": "2049-10-31T11:32:38.390000",
      "email": "test@crosoftware.net",
      "id": 1,
      "is_active": true,
      "name": "John Doe",
      "phone": "+1 (360) 123-6543",
      "state": "WA",
      "truck_limit": 0,
      "zip": "98368"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schematenantlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[TenantModel](#schematenantmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocStenantmodel">TenantModel</h2>

```json
{
  "address": "123 Some St.",
  "city": "Sequim",
  "code": "BESTSCRAP",
  "created_on": "2049-10-31T11:32:38.390000",
  "email": "test@crosoftware.net",
  "id": 1,
  "is_active": true,
  "name": "John Doe",
  "phone": "+1 (360) 123-6543",
  "state": "WA",
  "truck_limit": 0,
  "zip": "98368"
}

```

<a id="schematenantmodel"></a>

|Name|Type|Description|
|---|---|---|
|`address`|string|Street address.|
|`city`|string|Address locality (e.g. city).|
|`code`|string|Facility identifier.|
|`created_on`|string(DateTime)|Timestamp of creation (must be in past).|
|`email`|string(Email)|Email address.|
|`id`|integer(int64)|Resource identifier.|
|`is_active`|boolean|Records marked inactive are treated as deleted (soft delete).|
|`name`|string|Name (free text).|
|`phone`|string(PhoneNumber)|Phone number (free text).|
|`state`|string|Address region (e.g. state).|
|`truck_limit`|integer(int64)|Maximum trucks configurable for tenant.|
|`zip`|string|Postal code (may include letters and symbols).|

<h2 id="tocSthirdpartyhaulerconnectionlistmodel">ThirdPartyHaulerConnectionListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": {
    "approved_by": 1,
    "approved_on": "2049-10-31T11:32:38.390000",
    "denied_on": "2049-10-31T11:32:38.390000",
    "is_approved": true,
    "location_id": 1,
    "provider_email": "test@crosoftware.net",
    "provider_id": 1,
    "provider_name": "John Doe",
    "provider_phone": "+1 (360) 123-6543",
    "requested_on": "2049-10-31T11:32:38.390000"
  },
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schemathirdpartyhaulerconnectionlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|[ThirdPartyHaulerConnectionModel](#schemathirdpartyhaulerconnectionmodel)|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocSthirdpartyhaulerconnectionmodel">ThirdPartyHaulerConnectionModel</h2>

```json
{
  "approved_by": 1,
  "approved_on": "2049-10-31T11:32:38.390000",
  "denied_on": "2049-10-31T11:32:38.390000",
  "is_approved": true,
  "location_id": 1,
  "provider_email": "test@crosoftware.net",
  "provider_id": 1,
  "provider_name": "John Doe",
  "provider_phone": "+1 (360) 123-6543",
  "requested_on": "2049-10-31T11:32:38.390000"
}

```

<a id="schemathirdpartyhaulerconnectionmodel"></a>

|Name|Type|Description|
|---|---|---|
|`approved_by`|integer(int64)|Approved by.|
|`approved_on`|string(DateTime)|Approval date.|
|`denied_on`|string(DateTime)|Denial date.|
|`is_approved`|boolean|Approved record state.|
|`location_id`|integer(int64)|Location identifier.|
|`provider_email`|string(Email)|Email address.|
|`provider_id`|integer(int64)|Bin provider identifier.|
|`provider_name`|string|Name (free text).|
|`provider_phone`|string(PhoneNumber)|Phone number (free text).|
|`requested_on`|string(DateTime)|Requested date.|

<h2 id="tocSthirdpartyhaulerlistmodel">ThirdPartyHaulerListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "id": "9f34f340-54d2-4403-a53b-d8017a64734f",
      "name": "John Doe"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schemathirdpartyhaulerlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[ThirdPartyHaulerModel](#schemathirdpartyhaulermodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocSthirdpartyhaulermodel">ThirdPartyHaulerModel</h2>

```json
{
  "id": "9f34f340-54d2-4403-a53b-d8017a64734f",
  "name": "John Doe"
}

```

<a id="schemathirdpartyhaulermodel"></a>

|Name|Type|Description|
|---|---|---|
|`id`|string(Uuid)|Third party hauler identifier.|
|`name`|string|Name (free text).|

<h2 id="tocStrucklistmodel">TruckListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "driver_id": 1,
      "id": 1,
      "location_id": 1,
      "name": "John Doe",
      "notes": "A note about something",
      "out_of_service": true,
      "require_odometer": true,
      "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f",
      "type": "FlatHauler",
      "weight": 23100.1
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schematrucklistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[TruckModel](#schematruckmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocStruckmodel">TruckModel</h2>

```json
{
  "driver_id": 1,
  "id": 1,
  "location_id": 1,
  "name": "John Doe",
  "notes": "A note about something",
  "out_of_service": true,
  "require_odometer": true,
  "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f",
  "type": "FlatHauler",
  "weight": 23100.1
}

```

<a id="schematruckmodel"></a>

|Name|Type|Description|
|---|---|---|
|`driver_id`|integer(int64)|Driver identifier.|
|`id`|integer(int64)|Resource identifier.|
|`location_id`|integer(int64)|Location identifier.|
|`name`|string|Name (free text).|
|`notes`|string|Notes (free text).|
|`out_of_service`|boolean|Truck out of service.|
|`require_odometer`|boolean|Require odometer.|
|`third_party_hauler_id`|string(Uuid)|Third party hauler identifier.|
|`type`|string|Truck type (free text).|
|`weight`|number(float)|Truck empty weight.|

<h2 id="tocSupdatecustomeraddressmodel">UpdateCustomerAddressModel</h2>

```json
{
  "country": "US",
  "is_billing": true,
  "is_shipping": true,
  "latitude": 56.2,
  "line_1": "123 Some St.",
  "line_2": "Office #34",
  "line_3": "Box #2",
  "line_4": "Drop in Blue Box",
  "locality": "Sequim",
  "longitude": 128.1,
  "postcode": "98368",
  "region": "WA"
}

```

<a id="schemaupdatecustomeraddressmodel"></a>

|Name|Type|Description|
|---|---|---|
|`country`|string|Country code (ISO 3166-1 alpha 2).|
|`is_billing`|boolean|If true, this is the customer's billing address.|
|`is_shipping`|boolean|Customer's shipping address if true.|
|`latitude`|number(float)|Latitude.|
|`line_1`|string|Street address.|
|`line_2`|string|Street address line 2.|
|`line_3`|string|Street address line 3.|
|`line_4`|string|Street address line 4 (doubles as county).|
|`locality`|string|Address locality (e.g. city).|
|`longitude`|number(float)|longitude.|
|`postcode`|string|Postal code (may include letters and symbols).|
|`region`|string|Address region (e.g. state).|

<h2 id="tocSupdatecustomercontactmodel">UpdateCustomerContactModel</h2>

```json
{
  "email": "john@crosoftware.net, jane@crosoftware.net",
  "fax": "+1 (360) 123-6543",
  "name": "John Doe",
  "notify_on_acknowledged_request": true,
  "notify_on_completed_request": true,
  "notify_on_dispatched_request": true,
  "notify_on_failed_request": true,
  "notify_on_new_request": true,
  "number": "+1 (360) 123-6543"
}

```

<a id="schemaupdatecustomercontactmodel"></a>

|Name|Type|Description|
|---|---|---|
|`email`|string(Email)|Email address comma-separated list.|
|`fax`|string(PhoneNumber)|Fax number (free text).|
|`name`|string|Name (free text).|
|`notify_on_acknowledged_request`|boolean|Notify on acknowledge request.|
|`notify_on_completed_request`|boolean|Notify on completed request.|
|`notify_on_dispatched_request`|boolean|Notify on dispatched request.|
|`notify_on_failed_request`|boolean|Notify on failed request.|
|`notify_on_new_request`|boolean|Notify on new request.|
|`number`|string(PhoneNumber)|Phone number (free text).|

<h2 id="tocSupdatecustomerlocationmodel">UpdateCustomerLocationModel</h2>

```json
{
  "is_active": true,
  "is_commercial": true,
  "note": "A note about something",
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "suspension_id": 1
}

```

<a id="schemaupdatecustomerlocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`is_active`|boolean|Records marked inactive are treated as deleted (soft delete).|
|`is_commercial`|boolean|Commercial address if true, private if false.|
|`note`|string|Notes (free text).|
|`reference_number`|string|Reference number (free text).|
|`renewal_date`|string(DateTime)|Renewal date.|
|`sales_rep`|string|Name of sales representative.|
|`suspension_id`|integer(int64)|Suspension identifier.|

<h2 id="tocSupdatecustomermodel">UpdateCustomerModel</h2>

```json
{
  "name": "John Doe",
  "parent_id": 0
}

```

<a id="schemaupdatecustomermodel"></a>

|Name|Type|Description|
|---|---|---|
|`name`|string|Name (free text).|
|`parent_id`|integer(int64)|Parent record identifier.|

<h2 id="tocSupdatewebhookmodel">UpdateWebhookModel</h2>

```json
{
  "events": [
    "Customer"
  ],
  "secret": "<Secret>",
  "url": "https://test.url"
}

```

<a id="schemaupdatewebhookmodel"></a>

|Name|Type|Description|
|---|---|---|
|`events`|array[string]|Hook event.|
|`secret`|string|Response body HMAC signing key.|
|`url`|string(Url)|Callback URL.|

<h2 id="tocSupdatedjobmodel">UpdatedJobModel</h2>

```json
{
  "arrived_at_dest": "2049-10-31T11:32:38.390000",
  "arrived_on": "2049-10-31T11:32:38.390000",
  "asset_dropped": 101,
  "asset_id": 1,
  "asset_quantity": 1,
  "asset_type_id": 1,
  "completed_by": 1,
  "completed_by_driver": true,
  "completed_on": "2049-10-31T11:32:38.390000",
  "confirmed_on": "2049-10-31T11:32:38.390000",
  "created_by_id": 1,
  "customer_id": 1,
  "customer_notes": "A note entered by a customer",
  "desired_asset_desc": "A note entered by a driver",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2049-10-31T11:32:38.390000",
  "dispatcher_notes": "A note entered by a dispatcher.",
  "do_confirm": true,
  "driver_notes": "A note entered by a driver.",
  "dump_location_id": 2,
  "dumped_on": "2049-10-31T11:32:38.390000",
  "end_time": "2049-10-31T11:32:38.390000",
  "fail_reason": "A failure description selected by a driver.",
  "final_location_id": 1,
  "flags": "Notes about a job.",
  "id": 1,
  "invoice_notes": "Notes from a billing invoice",
  "is_completed": true,
  "is_declined": true,
  "is_deleted": true,
  "is_failed": true,
  "job_group_id": 1,
  "location_id": 1,
  "merged_with_route": 1,
  "original_schedule_date": "2049-10-31T11:32:38.390000",
  "pickup_date": "2049-10-31T11:32:38.390000",
  "priority": -3,
  "reference_number": "A140",
  "requested_on": "2049-10-31T11:32:38.390000",
  "require_image": true,
  "require_material": true,
  "require_signature": true,
  "require_weights": true,
  "scale_ticket": "A5100",
  "schedule_date": "2049-10-31T11:32:38.390000",
  "start_location_id": 1,
  "start_time": "2049-10-31T11:32:38.390000",
  "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f",
  "times_failed": 2,
  "times_rolled_over": 1,
  "truck_id": 1,
  "type": "D",
  "weighed_on": "2049-10-31T11:32:38.390000"
}

```

<a id="schemaupdatedjobmodel"></a>

|Name|Type|Description|
|---|---|---|
|`arrived_at_dest`|string(DateTime)|Entered by driver for dispatcher and customer. Asset arrival at destination time. Only applicable for jobs with a valid dump destination.|
|`arrived_on`|string(DateTime)|Drive start time entered by driver for dispatcher and customer (arrived at job slider).|
|`asset_dropped`|integer(int64)|Reference to deployed asset entered by driver for customer, dispatcher applicable to job types 'D', 'E'.|
|`asset_id`|integer(int64)|Job asset identifier. Applicable to job types 'E', 'P', 'R'.|
|`asset_quantity`|integer(int64)|How many assets are being serviced within a cluster (for jobs assigned to an asset cluster). For jobs dispatched by routes, or manually dispatched route stops, this value is 0 or 1.|
|`asset_type_id`|integer(int64)|Selected asset for the job (job types 'D', 'L', 'E').|
|`completed_by`|integer(int64)|Dispatcher or driver id.|
|`completed_by_driver`|boolean|If TRUE, completed by driver. If FALSE, completed by dispatcher.|
|`completed_on`|string(DateTime)|Job completion time.|
|`confirmed_on`|string(DateTime)|Job confirmation date.|
|`created_by_id`|integer(int64)|Customer, dispatcher, or driver id.|
|`customer_id`|integer(int64)|Customer identifier.|
|`customer_notes`|string|Notes entered by customers to communicate with dispatchers.|
|`desired_asset_desc`|string|Free-form text entered by dispatchers and drivers to be used as the future asset description.|
|`dispatch_priority`|string|Entered by dispatchers to determine dispatch order.|
|`dispatched_by_route`|integer(int64)|Route id of dispatching route (or NULL if not dispatched by a route).|
|`dispatched_on`|string(DateTime)|Time the job is assigned to a truck.|
|`dispatcher_notes`|string|Entered by dispatchers, read by drivers and dispatchers.|
|`do_confirm`|boolean|Tell dispatcher that a customer should be contacted before job is dispatched.|
|`driver_notes`|string|Entered by drivers when completing or failing a job for dispatchers.|
|`dump_location_id`|integer(int64)|Asset or asset cluster dump location identifier (e.g. trash bin needs dumped before returning from customer).|
|`dumped_on`|string(DateTime)|Dump request completion date.|
|`end_time`|string(DateTime)|Future estimated time of job completion.|
|`fail_reason`|string|Failure description selected by a driver for use by dispatchers.|
|`final_location_id`|integer(int64)|Final location identifier. Used by dispatchers for prioritizing jobs. Used by drivers to know where to leave the asset on job completion.|
|`flags`|string|Job notes.|
|`id`|integer(int64)|Resource identifier.|
|`invoice_notes`|string|Invoice notes from the billing system.|
|`is_completed`|boolean|Job completion flag set by dispatchers and drivers.|
|`is_declined`|boolean|Job completion flag set by dispatchers and drivers.|
|`is_deleted`|boolean|Indicates whether job is still valid.|
|`is_failed`|boolean|Set by drivers and dispatchers to indicate a failed job.|
|`job_group_id`|integer(int64)|Job group identifier for group jobs (vs service, exchange, etc.).|
|`location_id`|integer(int64)|Location identifier.|
|`merged_with_route`|integer(int64)|Assigned by dispatchers for dispatchers and drivers.|
|`original_schedule_date`|string(DateTime)|Original scheduling date.|
|`pickup_date`|string(DateTime)|A pickup job is scheduled for this date upon job completion. If the asset or cluster is assigned to a route stop, the route stop will be deleted. Must be in the future.|
|`priority`|integer(int64)|Assigned by dispatchers for job order completion determination for drivers.|
|`reference_number`|string|Reference number (free text).|
|`requested_on`|string(DateTime)|Requested date.|
|`require_image`|boolean|Set by dispatchers and drivers, requires drivers to upload one or more job images before completion.|
|`require_material`|boolean|Set by dispatchers and drivers, requires drivers to set a material before completing a job.|
|`require_signature`|boolean|Set by dispatchers and drivers, requires drivers to get a customer signature before job completion.|
|`require_weights`|boolean|Set by disptachers and drivers, requires drivers to set material weights before job completion.|
|`scale_ticket`|string|Scale ticket.|
|`schedule_date`|string(DateTime)|Scheduled job completion date.|
|`start_location_id`|integer(int64)|Pickup location for asset or asset cluster Set by dispatchers and drivers for drivers.|
|`start_time`|string(DateTime)|Time customer has requested job start, set by dispatchers for dispatchers and drivers.|
|`third_party_hauler_id`|string(Uuid)|Third party hauler identifier.|
|`times_failed`|integer(int64)|Number of times a job has been attempted and failed.|
|`times_rolled_over`|integer(int64)|Tracks job age in days for dispatchers.|
|`truck_id`|integer(int64)|Truck identifier.|
|`type`|string|Set by dispatchers and customers. Represents physical actions to execute on job start.|
|`weighed_on`|string(DateTime)|Time of truck weight entry.|

<h2 id="tocSuserlistresultsmodel">UserListResultsModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "id": 1,
      "roles": [
        "Dispatcher"
      ],
      "username": "test_user_1000"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schemauserlistresultsmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[UserModel](#schemausermodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocSusermodel">UserModel</h2>

```json
{
  "id": 1,
  "roles": [
    "Dispatcher"
  ],
  "username": "test_user_1000"
}

```

<a id="schemausermodel"></a>

|Name|Type|Description|
|---|---|---|
|`id`|integer(int64)|User identifier.|
|`roles`|array[string]|User role.|
|`username`|string|Username.|

<h2 id="tocSwebhooklistmodel">WebhookListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "events": [
        "Customer"
      ],
      "id": 1,
      "last_http_fail": "1",
      "last_http_success": "1",
      "url": "https://test.url"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schemawebhooklistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[WebhookModel](#schemawebhookmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocSwebhookmodel">WebhookModel</h2>

```json
{
  "events": [
    "Customer"
  ],
  "id": 1,
  "last_http_fail": "1",
  "last_http_success": "1",
  "url": "https://test.url"
}

```

<a id="schemawebhookmodel"></a>

|Name|Type|Description|
|---|---|---|
|`events`|array[string]|Hook event.|
|`id`|integer(int64)|Resource identifier.|
|`last_http_fail`|string(DateTime)|Last time of url webhook execution failure.|
|`last_http_success`|string(DateTime)|Last time of url webhook execution success.|
|`url`|string(Url)|Callback URL.|

<h2 id="tocSwebhookpingresultmodel">WebhookPingResultModel</h2>

```json
{
  "delivery_id": "1",
  "http_status": 200
}

```

<a id="schemawebhookpingresultmodel"></a>

|Name|Type|Description|
|---|---|---|
|`delivery_id`|string(Uuid)|Hook execution identifier.|
|`http_status`|integer(int64)|HTTP status return code.|

