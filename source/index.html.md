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

<h1 id="cro-software-api">CRO Software API v0.1.0</h1>

Build on & integrate with CRO Software.

Base URLs:

* <a href="https://api.crosoftware.net">https://api.crosoftware.net</a>

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
          String url = "https://api.crosoftware.net/customers/{customer_id}/addresses";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "POST", parameters);
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`body`|body|[CreateCustomerAddressModel](#schemacreatecustomeraddressmodel)|true||

> Example responses

> 200 Response

```json
{
  "country": "US",
  "id": 1,
  "is_active": true,
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressModel](#schemacustomeraddressmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          String url = "https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id}";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "DELETE", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X DELETE https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id} \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id}',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.delete 'https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.delete('https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id}");
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_address_id`|path|integer(int64)|true|Customer address identifier.|

> Example responses

> 200 Response

```json
{
  "country": "US",
  "id": 1,
  "is_active": true,
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressModel](#schemacustomeraddressmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          String url = "https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id}";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id} \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id}',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id}");
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_address_id`|path|integer(int64)|true|Customer address identifier.|

> Example responses

> 200 Response

```json
{
  "country": "US",
  "id": 1,
  "is_active": true,
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressModel](#schemacustomeraddressmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "country": "US",
      "id": 1,
      "is_active": true,
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressListModel](#schemacustomeraddresslistmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          String url = "https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id}";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id}',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.patch 'https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.patch('https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/addresses/{customer_address_id}");
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
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_address_id`|path|integer(int64)|true|Customer address identifier.|
|`body`|body|[UpdateCustomerAddressModel](#schemaupdatecustomeraddressmodel)|true||

> Example responses

> 200 Response

```json
{
  "country": "US",
  "id": 1,
  "is_active": true,
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerAddressModel](#schemacustomeraddressmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "POST", parameters);
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`body`|body|[CreateCustomerContactModel](#schemacreatecustomercontactmodel)|true||

> Example responses

> 200 Response

```json
{
  "email": "john@crosoftware.net, jane@crosoftware.net",
  "fax": "+1 (360) 123-6543",
  "id": 1,
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerContactModel](#schemacustomercontactmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          String url = "https://api.crosoftware.net/customers/{customer_id}/contacts/{customer_contact_id}";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/customers/{customer_id}/contacts/{customer_contact_id} \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/contacts/{customer_contact_id}',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crosoftware.net/customers/{customer_id}/contacts/{customer_contact_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crosoftware.net/customers/{customer_id}/contacts/{customer_contact_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/contacts/{customer_contact_id}");
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_contact_id`|path|integer(int64)|true|Customer contact identifier.|

> Example responses

> 200 Response

```json
{
  "email": "john@crosoftware.net, jane@crosoftware.net",
  "fax": "+1 (360) 123-6543",
  "id": 1,
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerContactModel](#schemacustomercontactmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "id": 1,
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerContactListModel](#schemacustomercontactlistmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          String url = "https://api.crosoftware.net/customers/{customer_id}/contacts/{customer_contact_id}";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/customers/{customer_id}/contacts/{customer_contact_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/contacts/{customer_contact_id}',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.patch 'https://api.crosoftware.net/customers/{customer_id}/contacts/{customer_contact_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.patch('https://api.crosoftware.net/customers/{customer_id}/contacts/{customer_contact_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/contacts/{customer_contact_id}");
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
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_contact_id`|path|integer(int64)|true|Customer contact identifier.|
|`body`|body|[UpdateCustomerContactModel](#schemaupdatecustomercontactmodel)|true||

> Example responses

> 200 Response

```json
{
  "email": "john@crosoftware.net, jane@crosoftware.net",
  "fax": "+1 (360) 123-6543",
  "id": 1,
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerContactModel](#schemacustomercontactmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          String url = "https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.post 'https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.post('https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}");
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

> Body parameter

```json
{
  "is_commercial": true,
  "note": "A note about something",
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "sales_rep_id": "1",
  "suspension_id": 1
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_location_id`|path|integer(int64)|true|Customer location identifier|
|`body`|body|[CreateDispatchCustomerLocationModel](#schemacreatedispatchcustomerlocationmodel)|true||

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "country": "US",
      "id": 1,
      "is_active": true,
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
  "contacts": [
    {
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "id": 1,
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "created_on": "2049-10-31T11:32:38.390000",
  "customer_id": 1,
  "is_active": true,
  "is_commercial": true,
  "last_updated_on": "2049-10-31T11:32:38.390000",
  "location_id": 1,
  "name": "John Doe",
  "note": "A note about something",
  "parent_id": 0,
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "sales_rep_id": "1",
  "suspension_id": 1
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DispatchCustomerLocationModel](#schemadispatchcustomerlocationmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          String url = "https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "DELETE", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X DELETE https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id} \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.delete 'https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.delete('https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}");
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_location_id`|path|integer(int64)|true|Customer location identifier|

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "country": "US",
      "id": 1,
      "is_active": true,
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
  "contacts": [
    {
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "id": 1,
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "created_on": "2049-10-31T11:32:38.390000",
  "customer_id": 1,
  "is_active": true,
  "is_commercial": true,
  "last_updated_on": "2049-10-31T11:32:38.390000",
  "location_id": 1,
  "name": "John Doe",
  "note": "A note about something",
  "parent_id": 0,
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "sales_rep_id": "1",
  "suspension_id": 1
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DispatchCustomerLocationModel](#schemadispatchcustomerlocationmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          String url = "https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id} \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}");
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_location_id`|path|integer(int64)|true|Customer location identifier|

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "country": "US",
      "id": 1,
      "is_active": true,
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
  "contacts": [
    {
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "id": 1,
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "created_on": "2049-10-31T11:32:38.390000",
  "customer_id": 1,
  "is_active": true,
  "is_commercial": true,
  "last_updated_on": "2049-10-31T11:32:38.390000",
  "location_id": 1,
  "name": "John Doe",
  "note": "A note about something",
  "parent_id": 0,
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "sales_rep_id": "1",
  "suspension_id": 1
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DispatchCustomerLocationModel](#schemadispatchcustomerlocationmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|

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
          "id": 1,
          "is_active": true,
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
      "contacts": [
        {
          "email": "john@crosoftware.net, jane@crosoftware.net",
          "fax": "+1 (360) 123-6543",
          "id": 1,
          "name": "John Doe",
          "notify_on_acknowledged_request": true,
          "notify_on_completed_request": true,
          "notify_on_dispatched_request": true,
          "notify_on_failed_request": true,
          "notify_on_new_request": true,
          "number": "+1 (360) 123-6543"
        }
      ],
      "created_on": "2049-10-31T11:32:38.390000",
      "customer_id": 1,
      "is_active": true,
      "is_commercial": true,
      "last_updated_on": "2049-10-31T11:32:38.390000",
      "location_id": 1,
      "name": "John Doe",
      "note": "A note about something",
      "parent_id": 0,
      "reference_number": "A140",
      "renewal_date": "2049-10-31T11:32:38.390000",
      "sales_rep": "Jane Johnson",
      "sales_rep_id": "1",
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DispatchCustomerLocationListModel](#schemadispatchcustomerlocationlistmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          String url = "https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.patch 'https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.patch('https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/customers/{customer_id}/locations/{customer_location_id}");
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

> Body parameter

```json
{
  "is_active": true,
  "is_commercial": true,
  "note": "A note about something",
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "sales_rep_id": "1",
  "suspension_id": 1
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|
|`customer_location_id`|path|integer(int64)|true|Customer location identifier|
|`body`|body|[UpdateDispatchCustomerLocationModel](#schemaupdatedispatchcustomerlocationmodel)|true||

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "country": "US",
      "id": 1,
      "is_active": true,
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
  "contacts": [
    {
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "id": 1,
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "created_on": "2049-10-31T11:32:38.390000",
  "customer_id": 1,
  "is_active": true,
  "is_commercial": true,
  "last_updated_on": "2049-10-31T11:32:38.390000",
  "location_id": 1,
  "name": "John Doe",
  "note": "A note about something",
  "parent_id": 0,
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "sales_rep_id": "1",
  "suspension_id": 1
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DispatchCustomerLocationModel](#schemadispatchcustomerlocationmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "POST", parameters);
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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
  "sales_rep_id": "1",
  "suspension_id": 1
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
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
      "id": 1,
      "is_active": true,
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
  "contacts": [
    {
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "id": 1,
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "created_on": "2049-10-31T11:32:38.390000",
  "customer_id": 1,
  "is_active": true,
  "is_commercial": true,
  "last_updated_on": "2049-10-31T11:32:38.390000",
  "location_id": 1,
  "name": "John Doe",
  "note": "A note about something",
  "parent_id": 0,
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "sales_rep_id": "1",
  "suspension_id": 1
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DispatchCustomerLocationModel](#schemadispatchcustomerlocationmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`customer_id`|path|integer(int64)|true|Customer identifier.|

> Example responses

> 200 Response

```json
{
  "addresses": [
    {
      "country": "US",
      "id": 1,
      "is_active": true,
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
  "contacts": [
    {
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "id": 1,
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "created_on": "2049-10-31T11:32:38.390000",
  "id": 1,
  "last_updated_on": "2049-10-31T11:32:38.390000",
  "locations": [
    {
      "addresses": [
        {
          "country": "US",
          "id": 1,
          "is_active": true,
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
      "contacts": [
        {
          "email": "john@crosoftware.net, jane@crosoftware.net",
          "fax": "+1 (360) 123-6543",
          "id": 1,
          "name": "John Doe",
          "notify_on_acknowledged_request": true,
          "notify_on_completed_request": true,
          "notify_on_dispatched_request": true,
          "notify_on_failed_request": true,
          "notify_on_new_request": true,
          "number": "+1 (360) 123-6543"
        }
      ],
      "created_on": "2049-10-31T11:32:38.390000",
      "customer_id": 1,
      "is_active": true,
      "is_commercial": true,
      "last_updated_on": "2049-10-31T11:32:38.390000",
      "location_id": 1,
      "name": "John Doe",
      "note": "A note about something",
      "parent_id": 0,
      "reference_number": "A140",
      "renewal_date": "2049-10-31T11:32:38.390000",
      "sales_rep": "Jane Johnson",
      "sales_rep_id": "1",
      "suspension_id": 1
    }
  ],
  "name": "John Doe",
  "parent_id": 0
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerModel](#schemacustomermodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          String url = "https://api.crosoftware.net/locations/{location_id}/customers";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          // Parameters
          NameValueCollection parameters = new NameValueCollection();
          parameters.Add("name", "John Doe");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id}/customers?name=John%20Doe \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/customers',
  method: 'get',
  data: '?name=John%20Doe',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}/customers',
  params: {
  'name' => 'string'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}/customers', params={
  'name': 'John Doe'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/customers?name=John%20Doe");
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`name`|query|string|true|Name (free text).|
|`parent_id`|query|integer(int64)|false|If specified, return only children of the specified parent_id.|
|`last_updated_gte`|query|string(DateTime)|false|Return only records updated after (must be in past). If unspecified, return all.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`is_parent`|query|boolean|false|If true, return accounts with no parent. If false, return accounts with a parent. If null, all records returned.|
|`active`|query|boolean|false|If true, return only active records (default). If false, return only inactive records. If unspecified, return all.|
|`created_on_gte`|query|string(DateTime)|false|Return records created on or after the specified date. If unspecified, return all.|

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
          "id": 1,
          "is_active": true,
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
      "contacts": [
        {
          "email": "john@crosoftware.net, jane@crosoftware.net",
          "fax": "+1 (360) 123-6543",
          "id": 1,
          "name": "John Doe",
          "notify_on_acknowledged_request": true,
          "notify_on_completed_request": true,
          "notify_on_dispatched_request": true,
          "notify_on_failed_request": true,
          "notify_on_new_request": true,
          "number": "+1 (360) 123-6543"
        }
      ],
      "created_on": "2049-10-31T11:32:38.390000",
      "customer_id": 1,
      "is_active": true,
      "is_commercial": true,
      "last_updated_on": "2049-10-31T11:32:38.390000",
      "location_id": 1,
      "name": "John Doe",
      "note": "A note about something",
      "parent_id": 0,
      "reference_number": "A140",
      "renewal_date": "2049-10-31T11:32:38.390000",
      "sales_rep": "Jane Johnson",
      "sales_rep_id": "1",
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DispatchCustomerLocationListModel](#schemadispatchcustomerlocationlistmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "PATCH", parameters);
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
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
      "id": 1,
      "is_active": true,
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
  "contacts": [
    {
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "id": 1,
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "created_on": "2049-10-31T11:32:38.390000",
  "id": 1,
  "last_updated_on": "2049-10-31T11:32:38.390000",
  "locations": [
    {
      "addresses": [
        {
          "country": "US",
          "id": 1,
          "is_active": true,
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
      "contacts": [
        {
          "email": "john@crosoftware.net, jane@crosoftware.net",
          "fax": "+1 (360) 123-6543",
          "id": 1,
          "name": "John Doe",
          "notify_on_acknowledged_request": true,
          "notify_on_completed_request": true,
          "notify_on_dispatched_request": true,
          "notify_on_failed_request": true,
          "notify_on_new_request": true,
          "number": "+1 (360) 123-6543"
        }
      ],
      "created_on": "2049-10-31T11:32:38.390000",
      "customer_id": 1,
      "is_active": true,
      "is_commercial": true,
      "last_updated_on": "2049-10-31T11:32:38.390000",
      "location_id": 1,
      "name": "John Doe",
      "note": "A note about something",
      "parent_id": 0,
      "reference_number": "A140",
      "renewal_date": "2049-10-31T11:32:38.390000",
      "sales_rep": "Jane Johnson",
      "sales_rep_id": "1",
      "suspension_id": 1
    }
  ],
  "name": "John Doe",
  "parent_id": 0
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[CustomerModel](#schemacustomermodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
|

## Driver Chat

### Create Message

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
          String url = "https://api.crosoftware.net/drivers/{driver_id}/chats";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/drivers/{driver_id}/chats \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/drivers/{driver_id}/chats',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.post 'https://api.crosoftware.net/drivers/{driver_id}/chats',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.post('https://api.crosoftware.net/drivers/{driver_id}/chats', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/drivers/{driver_id}/chats");
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

`POST /drivers/{driver_id}/chats`

<a id="opIdpost_drivers_by_id_chats"></a>

> Body parameter

```json
{
  "receiver": {
    "id": 1,
    "type": "dispatcher"
  },
  "text": "Hello, World!"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`driver_id`|path|integer(int64)|true|Driver identifier.|
|`body`|body|[CreateDriverChatMessageModel](#schemacreatedriverchatmessagemodel)|true||

> Example responses

> 200 Response

```json
{
  "id": 1,
  "is_edited": 1,
  "is_read": 1,
  "last_edited_on": "2049-10-31T11:32:38.390000",
  "receiver": {
    "id": 1,
    "type": "dispatcher"
  },
  "sender": {
    "id": 1,
    "type": "dispatcher"
  },
  "sent_on": "2049-10-31T11:32:38.390000",
  "text": "Hello, World!"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DriverChatMessageModel](#schemadriverchatmessagemodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
|

### Edit Message

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
          String url = "https://api.crosoftware.net/drivers/{driver_id}/chats/{driver_chat_msg_id}";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/drivers/{driver_id}/chats/{driver_chat_msg_id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/drivers/{driver_id}/chats/{driver_chat_msg_id}',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.patch 'https://api.crosoftware.net/drivers/{driver_id}/chats/{driver_chat_msg_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.patch('https://api.crosoftware.net/drivers/{driver_id}/chats/{driver_chat_msg_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/drivers/{driver_id}/chats/{driver_chat_msg_id}");
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

`PATCH /drivers/{driver_id}/chats/{driver_chat_msg_id}`

<a id="opIdpatch_drivers_by_id_chats_by_id"></a>

> Body parameter

```json
{
  "is_read": 1,
  "text": "Hello, World!"
}
```

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`driver_id`|path|integer(int64)|true|Driver identifier.|
|`driver_chat_msg_id`|path|integer(int64)|true|Driver chat message identifier.|
|`body`|body|[UpdateDriverChatMessageModel](#schemaupdatedriverchatmessagemodel)|true||

> Example responses

> 200 Response

```json
{
  "id": 1,
  "is_edited": 1,
  "is_read": 1,
  "last_edited_on": "2049-10-31T11:32:38.390000",
  "receiver": {
    "id": 1,
    "type": "dispatcher"
  },
  "sender": {
    "id": 1,
    "type": "dispatcher"
  },
  "sent_on": "2049-10-31T11:32:38.390000",
  "text": "Hello, World!"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DriverChatMessageModel](#schemadriverchatmessagemodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
|

### List Messages

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
          String url = "https://api.crosoftware.net/drivers/{driver_id}/chats";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/drivers/{driver_id}/chats \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/drivers/{driver_id}/chats',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crosoftware.net/drivers/{driver_id}/chats',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crosoftware.net/drivers/{driver_id}/chats', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/drivers/{driver_id}/chats");
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

`GET /drivers/{driver_id}/chats`

<a id="opIdget_drivers_by_id_chats"></a>

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`driver_id`|path|integer(int64)|true|Driver identifier.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|
|`end_date`|query|string(DateTime)|false|Filter messages on or before this date.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`is_read`|query|boolean|false|Return only read messages if TRUE, unread messages if FALSE. All messages if NULL or unspecified.|
|`start_date`|query|string(DateTime)|false|Filter messages on or after this date.|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "id": 1,
      "is_edited": 1,
      "is_read": 1,
      "last_edited_on": "2049-10-31T11:32:38.390000",
      "receiver": {
        "id": 1,
        "type": "dispatcher"
      },
      "sender": {
        "id": 1,
        "type": "dispatcher"
      },
      "sent_on": "2049-10-31T11:32:38.390000",
      "text": "Hello, World!"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DriverChatMessageListModel](#schemadriverchatmessagelistmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
|

### List Recipients

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
          String url = "https://api.crosoftware.net/drivers/{driver_id}/chats/recipients";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/drivers/{driver_id}/chats/recipients \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/drivers/{driver_id}/chats/recipients',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crosoftware.net/drivers/{driver_id}/chats/recipients',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crosoftware.net/drivers/{driver_id}/chats/recipients', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/drivers/{driver_id}/chats/recipients");
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

`GET /drivers/{driver_id}/chats/recipients`

<a id="opIdget_drivers_by_id_chats_recipients"></a>

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`driver_id`|path|integer(int64)|true|Driver identifier.|

> Example responses

> 200 Response

```json
[
  {
    "id": 1,
    "name": "John Doe",
    "type": "dispatcher"
  }
]
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Inline|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4 id="undefined-responseschema">Response Schema</h4>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|-|array[[DriverChatRecipientModel](#schemadriverchatrecipientmodel)]|false|none|none|
|» id|integer(int64)|false|none|Driver chat message identifier.|
|» name|string|false|none|Recipient name.|
|» type|string|false|none|Recipient user account type.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DriverModel](#schemadrivermodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|

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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DriverListModel](#schemadriverlistmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          String url = "https://api.crosoftware.net/locations/{location_id}/dump_destinations/{dump_destination_id}";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id}/dump_destinations/{dump_destination_id} \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/dump_destinations/{dump_destination_id}',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}/dump_destinations/{dump_destination_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}/dump_destinations/{dump_destination_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/dump_destinations/{dump_destination_id}");
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`dump_destination_id`|path|integer(int64)|true|Dump destination identifier.|

> Example responses

> 200 Response

```json
{
  "address": "123 Some St.",
  "city": "Sequim",
  "contact_email": "john@crosoftware.net, jane@crosoftware.net",
  "contact_name": "Sequim",
  "contact_phone": "Sequim",
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DumpDestinationModel](#schemadumpdestinationmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          String url = "https://api.crosoftware.net/locations/{location_id}/dump_destinations";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id}/dump_destinations \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/dump_destinations',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}/dump_destinations',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}/dump_destinations', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/dump_destinations");
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|

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
      "contact_email": "john@crosoftware.net, jane@crosoftware.net",
      "contact_name": "Sequim",
      "contact_phone": "Sequim",
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[DumpDestinationListModel](#schemadumpdestinationlistmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "POST", parameters);
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[GpsStopModel](#schemagpsstopmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
curl -X POST https://api.crosoftware.net/haulers/{hauler_uuid}/connections?tenant_code=08767 \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/haulers/{hauler_uuid}/connections',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.post('https://api.crosoftware.net/haulers/{hauler_uuid}/connections', params={
  'tenant_code': '08767'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/haulers/{hauler_uuid}/connections?tenant_code=08767");
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`hauler_uuid`|path|string(Uuid)|true|Third party hauler identifier.|
|`tenant_code`|query|string|true|Confirmation code for hauler creation.|

> Example responses

> 200 Response

```json
{
  "approved_by": 1,
  "approved_on": "2049-10-31T11:32:38.390000",
  "denied_on": "2049-10-31T11:32:38.390000",
  "is_approved": true,
  "location_id": 1,
  "provider_id": 1,
  "provider_name": "John Doe",
  "requested_on": "2049-10-31T11:32:38.390000",
  "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerConnectionModel](#schemathirdpartyhaulerconnectionmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          
          // Parameters
          NameValueCollection parameters = new NameValueCollection();
          parameters.Add("password", "AG00d!P@55w0rd;");
          parameters.Add("recaptcha", "<google captcha str>");
          parameters.Add("username", "test_user_1000");
          parameters.Add("company_name", "BestScrap, Inc.");
          
          byte[] json = client.UploadString(url, "POST", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X POST https://api.crosoftware.net/haulers?password=AG00d%21P%4055w0rd%3B&recaptcha=%3Cgoogle%20captcha%20str%3E&username=test_user_1000&company_name=BestScrap%2C%20Inc. \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/haulers',
  method: 'post',
  data: '?password=AG00d%21P%4055w0rd%3B&recaptcha=%3Cgoogle%20captcha%20str%3E&username=test_user_1000&company_name=BestScrap%2C%20Inc.',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.post 'https://api.crosoftware.net/haulers',
  params: {
  'password' => 'string',
'recaptcha' => 'string',
'username' => 'string',
'company_name' => 'string'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'Authorization': 'Bearer {access-token}'
}

r = requests.post('https://api.crosoftware.net/haulers', params={
  'password': 'AG00d!P@55w0rd;',  'recaptcha': '<google captcha str>',  'username': 'test_user_1000',  'company_name': 'BestScrap, Inc.'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/haulers?password=AG00d%21P%4055w0rd%3B&recaptcha=%3Cgoogle%20captcha%20str%3E&username=test_user_1000&company_name=BestScrap%2C%20Inc.");
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`password`|query|string|true|Login password.|
|`recaptcha`|query|string|true|Recaptcha answer.|
|`username`|query|string|true|Username.|
|`company_name`|query|string|true|Company name (free text).|

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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerModel](#schemathirdpartyhaulermodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerModel](#schemathirdpartyhaulermodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
|

### List Hauler Connections

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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
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
  "results": [
    {
      "approved_by": 1,
      "approved_on": "2049-10-31T11:32:38.390000",
      "denied_on": "2049-10-31T11:32:38.390000",
      "is_approved": true,
      "location_id": 1,
      "provider_id": 1,
      "provider_name": "John Doe",
      "requested_on": "2049-10-31T11:32:38.390000",
      "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerConnectionListModel](#schemathirdpartyhaulerconnectionlistmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[ThirdPartyHaulerListModel](#schemathirdpartyhaulerlistmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/locations/{location_id}/jobs/{job_id} \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`job_id`|path|integer(int64)|true|Job identifier.|
|`new_schedule_date`|query|string(DateTime)|false|New schedule date.|
|`truck_id`|query|boolean|false|If specified, return only records matching this truck (default). If unspecified, return all.|

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
      "driver_self_assignment": true,
      "id": 1,
      "is_active": true,
      "name": "CRO Scrap",
      "use_additional_items": true
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
  "created_with_portal": true,
  "customer": {
    "addresses": [
      {
        "country": "US",
        "id": 1,
        "is_active": true,
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
    "contacts": [
      {
        "email": "john@crosoftware.net, jane@crosoftware.net",
        "fax": "+1 (360) 123-6543",
        "id": 1,
        "name": "John Doe",
        "notify_on_acknowledged_request": true,
        "notify_on_completed_request": true,
        "notify_on_dispatched_request": true,
        "notify_on_failed_request": true,
        "notify_on_new_request": true,
        "number": "+1 (360) 123-6543"
      }
    ],
    "created_on": "2049-10-31T11:32:38.390000",
    "id": 1,
    "last_updated_on": "2049-10-31T11:32:38.390000",
    "locations": [
      {
        "addresses": [
          {
            "country": "US",
            "id": 1,
            "is_active": true,
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
        "contacts": [
          {
            "email": "john@crosoftware.net, jane@crosoftware.net",
            "fax": "+1 (360) 123-6543",
            "id": 1,
            "name": "John Doe",
            "notify_on_acknowledged_request": true,
            "notify_on_completed_request": true,
            "notify_on_dispatched_request": true,
            "notify_on_failed_request": true,
            "notify_on_new_request": true,
            "number": "+1 (360) 123-6543"
          }
        ],
        "created_on": "2049-10-31T11:32:38.390000",
        "customer_id": 1,
        "is_active": true,
        "is_commercial": true,
        "last_updated_on": "2049-10-31T11:32:38.390000",
        "location_id": 1,
        "name": "John Doe",
        "note": "A note about something",
        "parent_id": 0,
        "reference_number": "A140",
        "renewal_date": "2049-10-31T11:32:38.390000",
        "sales_rep": "Jane Johnson",
        "sales_rep_id": "1",
        "suspension_id": 1
      }
    ],
    "name": "John Doe",
    "parent_id": 0
  },
  "customer_id": 1,
  "customer_notes": "A note entered by a customer",
  "departed_on": "2049-10-31T11:32:38.390000",
  "desired_asset_desc": "A note entered by a driver",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2049-10-31T11:32:38.390000",
  "dispatcher_notes": "A note entered by a dispatcher.",
  "do_confirm": true,
  "driver_notes": "A note entered by a driver.",
  "dropped_number": "string",
  "dump_location": {
    "address": "123 Some St.",
    "city": "Sequim",
    "contact_email": "john@crosoftware.net, jane@crosoftware.net",
    "contact_name": "Sequim",
    "contact_phone": "Sequim",
    "description": "A user entered/human readable text description.",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 56.2,
    "location_id": 1,
    "longitude": 128.1,
    "state": "WA",
    "zip": "98368"
  },
  "dump_location_id": 2,
  "dumped_on": "2049-10-31T11:32:38.390000",
  "end_time": "2049-10-31T11:32:38.390000",
  "fail_reason": "A failure description selected by a driver.",
  "final_location": {
    "address": "123 Some St.",
    "city": "Sequim",
    "contact_email": "john@crosoftware.net, jane@crosoftware.net",
    "contact_name": "Sequim",
    "contact_phone": "Sequim",
    "description": "A user entered/human readable text description.",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 56.2,
    "location_id": 1,
    "longitude": 128.1,
    "state": "WA",
    "zip": "98368"
  },
  "final_location_id": 1,
  "flags": "Notes about a job.",
  "id": 1,
  "invoice_notes": "Notes from a billing invoice",
  "is_completed": true,
  "is_declined": true,
  "is_deleted": true,
  "is_failed": true,
  "is_paid": true,
  "job_group_id": 1,
  "last_updated_on": "2049-10-31T11:32:38.390000",
  "location_id": 1,
  "materials": [
    {
      "heavy_weight": 39254.44,
      "light_weight": 34523.11,
      "material_item_id": 1,
      "material_name": "43A",
      "tare_weight": 32358.15
    }
  ],
  "merged_with_route": 1,
  "original_schedule_date": "2049-10-31T11:32:38.390000",
  "pickup_date": "2049-10-31T11:32:38.390000",
  "pickup_item": 1,
  "priority": -3,
  "reference_number": "A140",
  "removed_number": "string",
  "requested_on": "2049-10-31T11:32:38.390000",
  "require_image": true,
  "require_material": true,
  "require_signature": true,
  "require_weights": true,
  "scale_ticket": "A5100",
  "schedule_date": "2049-10-31T11:32:38.390000",
  "start_location": {
    "address": "123 Some St.",
    "city": "Sequim",
    "contact_email": "john@crosoftware.net, jane@crosoftware.net",
    "contact_name": "Sequim",
    "contact_phone": "Sequim",
    "description": "A user entered/human readable text description.",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 56.2,
    "location_id": 1,
    "longitude": 128.1,
    "state": "WA",
    "zip": "98368"
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[JobModel](#schemajobmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
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
      "driver_self_assignment": true,
      "id": 1,
      "is_active": true,
      "name": "CRO Scrap",
      "use_additional_items": true
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
  "created_with_portal": true,
  "customer": {
    "addresses": [
      {
        "country": "US",
        "id": 1,
        "is_active": true,
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
    "contacts": [
      {
        "email": "john@crosoftware.net, jane@crosoftware.net",
        "fax": "+1 (360) 123-6543",
        "id": 1,
        "name": "John Doe",
        "notify_on_acknowledged_request": true,
        "notify_on_completed_request": true,
        "notify_on_dispatched_request": true,
        "notify_on_failed_request": true,
        "notify_on_new_request": true,
        "number": "+1 (360) 123-6543"
      }
    ],
    "created_on": "2049-10-31T11:32:38.390000",
    "id": 1,
    "last_updated_on": "2049-10-31T11:32:38.390000",
    "locations": [
      {
        "addresses": [
          {
            "country": "US",
            "id": 1,
            "is_active": true,
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
        "contacts": [
          {
            "email": "john@crosoftware.net, jane@crosoftware.net",
            "fax": "+1 (360) 123-6543",
            "id": 1,
            "name": "John Doe",
            "notify_on_acknowledged_request": true,
            "notify_on_completed_request": true,
            "notify_on_dispatched_request": true,
            "notify_on_failed_request": true,
            "notify_on_new_request": true,
            "number": "+1 (360) 123-6543"
          }
        ],
        "created_on": "2049-10-31T11:32:38.390000",
        "customer_id": 1,
        "is_active": true,
        "is_commercial": true,
        "last_updated_on": "2049-10-31T11:32:38.390000",
        "location_id": 1,
        "name": "John Doe",
        "note": "A note about something",
        "parent_id": 0,
        "reference_number": "A140",
        "renewal_date": "2049-10-31T11:32:38.390000",
        "sales_rep": "Jane Johnson",
        "sales_rep_id": "1",
        "suspension_id": 1
      }
    ],
    "name": "John Doe",
    "parent_id": 0
  },
  "customer_id": 1,
  "customer_notes": "A note entered by a customer",
  "departed_on": "2049-10-31T11:32:38.390000",
  "desired_asset_desc": "A note entered by a driver",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2049-10-31T11:32:38.390000",
  "dispatcher_notes": "A note entered by a dispatcher.",
  "do_confirm": true,
  "driver_notes": "A note entered by a driver.",
  "dropped_number": "string",
  "dump_location": {
    "address": "123 Some St.",
    "city": "Sequim",
    "contact_email": "john@crosoftware.net, jane@crosoftware.net",
    "contact_name": "Sequim",
    "contact_phone": "Sequim",
    "description": "A user entered/human readable text description.",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 56.2,
    "location_id": 1,
    "longitude": 128.1,
    "state": "WA",
    "zip": "98368"
  },
  "dump_location_id": 2,
  "dumped_on": "2049-10-31T11:32:38.390000",
  "end_time": "2049-10-31T11:32:38.390000",
  "fail_reason": "A failure description selected by a driver.",
  "final_location": {
    "address": "123 Some St.",
    "city": "Sequim",
    "contact_email": "john@crosoftware.net, jane@crosoftware.net",
    "contact_name": "Sequim",
    "contact_phone": "Sequim",
    "description": "A user entered/human readable text description.",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 56.2,
    "location_id": 1,
    "longitude": 128.1,
    "state": "WA",
    "zip": "98368"
  },
  "final_location_id": 1,
  "flags": "Notes about a job.",
  "id": 1,
  "invoice_notes": "Notes from a billing invoice",
  "is_completed": true,
  "is_declined": true,
  "is_deleted": true,
  "is_failed": true,
  "is_paid": true,
  "job_group_id": 1,
  "last_updated_on": "2049-10-31T11:32:38.390000",
  "location_id": 1,
  "materials": [
    {
      "heavy_weight": 39254.44,
      "light_weight": 34523.11,
      "material_item_id": 1,
      "material_name": "43A",
      "tare_weight": 32358.15
    }
  ],
  "merged_with_route": 1,
  "original_schedule_date": "2049-10-31T11:32:38.390000",
  "pickup_date": "2049-10-31T11:32:38.390000",
  "pickup_item": 1,
  "priority": -3,
  "reference_number": "A140",
  "removed_number": "string",
  "requested_on": "2049-10-31T11:32:38.390000",
  "require_image": true,
  "require_material": true,
  "require_signature": true,
  "require_weights": true,
  "scale_ticket": "A5100",
  "schedule_date": "2049-10-31T11:32:38.390000",
  "start_location": {
    "address": "123 Some St.",
    "city": "Sequim",
    "contact_email": "john@crosoftware.net, jane@crosoftware.net",
    "contact_name": "Sequim",
    "contact_phone": "Sequim",
    "description": "A user entered/human readable text description.",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 56.2,
    "location_id": 1,
    "longitude": 128.1,
    "state": "WA",
    "zip": "98368"
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[JobModel](#schemajobmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

<a id="opIdget_locations_by_id_jobs"></a>

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`truck_id`|query|boolean|false|If specified, return only records matching this truck (default). If unspecified, return all.|
|`completed_by_driver`|query|boolean|false|If true, return only records marked completed by a driver. If false, return only records marked incomplete. If unspecified, return all.|
|`failed`|query|boolean|false|If true, return only records marked deleted. If false, return only records marked as deleted. If unspecified, return all.|
|`deleted`|query|boolean|false|If true, return only active records (default). If false, return only inactive records. If unspecified, return all.|
|`schedule_lt`|query|string(DateTime)|false|Return only jobs scheduled before.|
|`last_updated_gte`|query|string(DateTime)|false|Return only records updated after (must be in past). If unspecified, return all.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|
|`schedule_gt`|query|string(DateTime)|false|Return only jobs scheduled after (must be in past). If unspecified, return all.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`driver_id`|query|boolean|false|If specified, return only records matching this driver (default). If unspecified, return all.|
|`completed`|query|boolean|false|If true, return only records marked completed (default). If false, return only records marked incomplete. If unspecified, return all.|
|`created_on_gte`|query|string(DateTime)|false|Return records created on or after the specified date. If unspecified, return all.|

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
          "driver_self_assignment": true,
          "id": 1,
          "is_active": true,
          "name": "CRO Scrap",
          "use_additional_items": true
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
      "created_with_portal": true,
      "customer": {
        "addresses": [
          {
            "country": "US",
            "id": 1,
            "is_active": true,
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
        "contacts": [
          {
            "email": "john@crosoftware.net, jane@crosoftware.net",
            "fax": "+1 (360) 123-6543",
            "id": 1,
            "name": "John Doe",
            "notify_on_acknowledged_request": true,
            "notify_on_completed_request": true,
            "notify_on_dispatched_request": true,
            "notify_on_failed_request": true,
            "notify_on_new_request": true,
            "number": "+1 (360) 123-6543"
          }
        ],
        "created_on": "2049-10-31T11:32:38.390000",
        "id": 1,
        "last_updated_on": "2049-10-31T11:32:38.390000",
        "locations": [
          {
            "addresses": [
              {
                "country": "US",
                "id": 1,
                "is_active": true,
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
            "contacts": [
              {
                "email": "john@crosoftware.net, jane@crosoftware.net",
                "fax": "+1 (360) 123-6543",
                "id": 1,
                "name": "John Doe",
                "notify_on_acknowledged_request": true,
                "notify_on_completed_request": true,
                "notify_on_dispatched_request": true,
                "notify_on_failed_request": true,
                "notify_on_new_request": true,
                "number": "+1 (360) 123-6543"
              }
            ],
            "created_on": "2049-10-31T11:32:38.390000",
            "customer_id": 1,
            "is_active": true,
            "is_commercial": true,
            "last_updated_on": "2049-10-31T11:32:38.390000",
            "location_id": 1,
            "name": "John Doe",
            "note": "A note about something",
            "parent_id": 0,
            "reference_number": "A140",
            "renewal_date": "2049-10-31T11:32:38.390000",
            "sales_rep": "Jane Johnson",
            "sales_rep_id": "1",
            "suspension_id": 1
          }
        ],
        "name": "John Doe",
        "parent_id": 0
      },
      "customer_id": 1,
      "customer_notes": "A note entered by a customer",
      "departed_on": "2049-10-31T11:32:38.390000",
      "desired_asset_desc": "A note entered by a driver",
      "dispatch_priority": "H",
      "dispatched_by_route": 1,
      "dispatched_on": "2049-10-31T11:32:38.390000",
      "dispatcher_notes": "A note entered by a dispatcher.",
      "do_confirm": true,
      "driver_notes": "A note entered by a driver.",
      "dropped_number": "string",
      "dump_location": {
        "address": "123 Some St.",
        "city": "Sequim",
        "contact_email": "john@crosoftware.net, jane@crosoftware.net",
        "contact_name": "Sequim",
        "contact_phone": "Sequim",
        "description": "A user entered/human readable text description.",
        "id": 1,
        "is_holding_yard": true,
        "latitude": 56.2,
        "location_id": 1,
        "longitude": 128.1,
        "state": "WA",
        "zip": "98368"
      },
      "dump_location_id": 2,
      "dumped_on": "2049-10-31T11:32:38.390000",
      "end_time": "2049-10-31T11:32:38.390000",
      "fail_reason": "A failure description selected by a driver.",
      "final_location": {
        "address": "123 Some St.",
        "city": "Sequim",
        "contact_email": "john@crosoftware.net, jane@crosoftware.net",
        "contact_name": "Sequim",
        "contact_phone": "Sequim",
        "description": "A user entered/human readable text description.",
        "id": 1,
        "is_holding_yard": true,
        "latitude": 56.2,
        "location_id": 1,
        "longitude": 128.1,
        "state": "WA",
        "zip": "98368"
      },
      "final_location_id": 1,
      "flags": "Notes about a job.",
      "id": 1,
      "invoice_notes": "Notes from a billing invoice",
      "is_completed": true,
      "is_declined": true,
      "is_deleted": true,
      "is_failed": true,
      "is_paid": true,
      "job_group_id": 1,
      "last_updated_on": "2049-10-31T11:32:38.390000",
      "location_id": 1,
      "materials": [
        {
          "heavy_weight": 39254.44,
          "light_weight": 34523.11,
          "material_item_id": 1,
          "material_name": "43A",
          "tare_weight": 32358.15
        }
      ],
      "merged_with_route": 1,
      "original_schedule_date": "2049-10-31T11:32:38.390000",
      "pickup_date": "2049-10-31T11:32:38.390000",
      "pickup_item": 1,
      "priority": -3,
      "reference_number": "A140",
      "removed_number": "string",
      "requested_on": "2049-10-31T11:32:38.390000",
      "require_image": true,
      "require_material": true,
      "require_signature": true,
      "require_weights": true,
      "scale_ticket": "A5100",
      "schedule_date": "2049-10-31T11:32:38.390000",
      "start_location": {
        "address": "123 Some St.",
        "city": "Sequim",
        "contact_email": "john@crosoftware.net, jane@crosoftware.net",
        "contact_name": "Sequim",
        "contact_phone": "Sequim",
        "description": "A user entered/human readable text description.",
        "id": 1,
        "is_holding_yard": true,
        "latitude": 56.2,
        "location_id": 1,
        "longitude": 128.1,
        "state": "WA",
        "zip": "98368"
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[JobListModel](#schemajoblistmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|

> Example responses

> 200 Response

```json
{
  "driver_self_assignment": true,
  "id": 1,
  "is_active": true,
  "name": "CRO Scrap",
  "use_additional_items": true
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[LocationModel](#schemalocationmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
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
      "driver_self_assignment": true,
      "id": 1,
      "is_active": true,
      "name": "CRO Scrap",
      "use_additional_items": true
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[LocationListModel](#schemalocationlistmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          String url = "https://api.crosoftware.net/locations/{location_id}/materials";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id}/materials \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/materials',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}/materials',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}/materials', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/materials");
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`page_limit`|query|integer(int64)|false|Maximun number of results per page.|
|`page_index`|query|integer(int64)|false|Paged results page index (starting from 1).|

> Example responses

> 200 Response

```json
[
  {
    "created_on": "2049-10-31T11:32:38.390000",
    "description": "A user entered/human readable text description.",
    "factor": 1.1,
    "group_description": "A user entered/human readable text description.",
    "id": 1,
    "line_item_id": 1,
    "location_id": 1,
    "unit_price": 12.75,
    "uom": "A user entered/human readable description of the UOM."
  }
]
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Inline|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4 id="undefined-responseschema">Response Schema</h4>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|-|array[[MaterialModel](#schemamaterialmodel)]|false|none|none|
|» created_on|string(DateTime)|false|none|Timestamp of creation (must be in past).|
|» description|string|false|none|Free-form text description.|
|» factor|number(float)|false|none|none|
|» group_description|string|false|none|Free-form text description.|
|» id|integer(int64)|false|none|Resource identifier.|
|» line_item_id|integer(int64)|false|none|Line item identifier.|
|» location_id|integer(int64)|false|none|Location identifier.|
|» unit_price|number(float)|false|none|Job material name.|
|» uom|string|false|none|Unit of Measure.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
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
      "truck_limit": 30,
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TenantListModel](#schematenantlistmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
|

## Trucks

### Get Job list

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
          String url = "https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}/get_jobs_list_pdf";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}/get_jobs_list_pdf \
  -H 'Accept: application/pdf' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/pdf',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}/get_jobs_list_pdf',
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
  'Accept' => 'application/pdf',
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}/get_jobs_list_pdf',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/pdf',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}/get_jobs_list_pdf', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id}/get_jobs_list_pdf");
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

`GET /locations/{location_id}/trucks/{truck_id}/get_jobs_list_pdf`

<a id="opIdget_locations_by_id_trucks_by_id_get_jobs_list_pdf"></a>

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`truck_id`|path|integer(int64)|true|Truck identifier.|

> Example responses

> 200 Response

> 400 Response

```json
{
  "detail": "Something happened that caused an error.",
  "explanation": "An error has occurred because...",
  "title": "Failed to load data"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|string|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
|

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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TruckModel](#schematruckmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TruckListModel](#schematrucklistmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "PATCH", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X PATCH https://api.crosoftware.net/locations/{location_id}/trucks/{truck_id} \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`truck_id`|path|integer(int64)|true|Truck identifier.|
|`driver_id`|query|boolean|false|If specified, return only records matching this driver (default). If unspecified, return all.|

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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[TruckModel](#schematruckmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          String url = "https://api.crosoftware.net/locations/{location_id}/users/{user_id}";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id}/users/{user_id} \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/users/{user_id}',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}/users/{user_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}/users/{user_id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/users/{user_id}");
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|
|`user_id`|path|integer(int64)|true|User identifier.|

> Example responses

> 200 Response

```json
{
  "dispatcher_id": 1,
  "id": 1,
  "roles": [
    "Dispatcher"
  ],
  "uid": "9f34f340-54d2-4403-a53b-d8017a64734f",
  "username": "test_user_1000"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[UserModel](#schemausermodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          String url = "https://api.crosoftware.net/locations/{location_id}/users";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/locations/{location_id}/users \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/locations/{location_id}/users',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crosoftware.net/locations/{location_id}/users',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crosoftware.net/locations/{location_id}/users', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/locations/{location_id}/users");
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`location_id`|path|integer(int64)|true|Location identifier.|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "dispatcher_id": 1,
      "id": 1,
      "roles": [
        "Dispatcher"
      ],
      "uid": "9f34f340-54d2-4403-a53b-d8017a64734f",
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[UserListResultsModel](#schemauserlistresultsmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "POST", parameters);
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`body`|body|[CreateWebhookModel](#schemacreatewebhookmodel)|true||

> Example responses

> 200 Response

```json
{
  "deleted_at": "2049-10-31T11:32:38.390000",
  "events": [
    "Customer"
  ],
  "id": 1,
  "last_http_fail": "1",
  "last_http_success": "1",
  "secret": "<Secret>",
  "url": "https://test.url"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[WebhookModel](#schemawebhookmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "DELETE", parameters);
          Console.WriteLine(System.Text.Encoding.Default.GetString(json));
      }
  }
}
```

```shell
# You can also use wget
curl -X DELETE https://api.crosoftware.net/hooks/{hook_id} \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`hook_id`|path|integer(int64)|true|Webhook identifier.|

> Example responses

> 200 Response

```json
{
  "deleted_at": "2049-10-31T11:32:38.390000",
  "events": [
    "Customer"
  ],
  "id": 1,
  "last_http_fail": "1",
  "last_http_success": "1",
  "secret": "<Secret>",
  "url": "https://test.url"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[WebhookModel](#schemawebhookmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`hook_id`|path|integer(int64)|true|Webhook identifier.|

> Example responses

> 200 Response

```json
{
  "deleted_at": "2049-10-31T11:32:38.390000",
  "events": [
    "Customer"
  ],
  "id": 1,
  "last_http_fail": "1",
  "last_http_success": "1",
  "secret": "<Secret>",
  "url": "https://test.url"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[WebhookModel](#schemawebhookmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|

> Example responses

> 200 Response

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "deleted_at": "2049-10-31T11:32:38.390000",
      "events": [
        "Customer"
      ],
      "id": 1,
      "last_http_fail": "1",
      "last_http_success": "1",
      "secret": "<Secret>",
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
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[WebhookListModel](#schemawebhooklistmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          String url = "https://api.crosoftware.net/hooks/{hook_id}/ping";

          // Headers
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          string json = client.DownloadString(url);
          Console.WriteLine(json);
      }
  }
}
```

```shell
# You can also use wget
curl -X GET https://api.crosoftware.net/hooks/{hook_id}/ping \
  -H 'Accept: application/json' \
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

};

$.ajax({
  url: 'https://api.crosoftware.net/hooks/{hook_id}/ping',
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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crosoftware.net/hooks/{hook_id}/ping',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crosoftware.net/hooks/{hook_id}/ping', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://api.crosoftware.net/hooks/{hook_id}/ping");
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

 

<h4 id="undefined-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`hook_id`|path|integer(int64)|true|Webhook identifier.|

> Example responses

> 200 Response

```json
{
  "delivery_id": "1",
  "http_status": 200,
  "message": "1"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[WebhookPingResultModel](#schemawebhookpingresultmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-cro-signature|string||HMAC message signature.
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
          client.Headers.Add("x-request-id", "9f34f340-54d2-4403-a53b-d8017a64734f");
          client.Headers.Add("x-tenant-id", "1");
          
          byte[] json = client.UploadString(url, "PATCH", parameters);
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
  -H 'x-request-id: 9f34f340-54d2-4403-a53b-d8017a64734f' \
  -H 'x-tenant-id: 1' \
  -H 'Authorization: Bearer {access-token}'

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'x-request-id':'9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id':'1',
  'Authorization':'Bearer {access-token}'

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
  'x-request-id' => '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id' => '1',
  'Authorization' => 'Bearer {access-token}'
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
  'x-request-id': '9f34f340-54d2-4403-a53b-d8017a64734f',
  'x-tenant-id': '1',
  'Authorization': 'Bearer {access-token}'
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
|`x-request-id`|header|string(Uuid)|true|Request identifier.|
|`x-tenant-id`|header|integer(int64)|true|Tenant identifier.|
|`hook_id`|path|integer(int64)|true|Webhook identifier.|
|`body`|body|[UpdateWebhookModel](#schemaupdatewebhookmodel)|true||

> Example responses

> 200 Response

```json
{
  "deleted_at": "2049-10-31T11:32:38.390000",
  "events": [
    "Customer"
  ],
  "id": 1,
  "last_http_fail": "1",
  "last_http_success": "1",
  "secret": "<Secret>",
  "url": "https://test.url"
}
```

<h4 id="undefined-responses">Responses</h4>

|Status|Meaning|Schema|Description|
|---|---|---|---|
|`200`|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|[WebhookModel](#schemawebhookmodel)|Operation success.|
|`400`|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`401`|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`403`|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`404`|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`406`|[Not Acceptable](https://tools.ietf.org/html/rfc7231#section-6.5.6)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`409`|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|
|`500`|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|[ErrorResponseModel](#schemaerrorresponsemodel)|Resource not found.|

<h4>Response Headers</h4>

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Accept|string||Content-Type header (e.g. application/json).
|
|200|Content-Type|string||Content-Type header (e.g. application/json).
|
|200|x-request-id|string|Uuid|Request identifier.
|
|400|Accept|string||Content-Type header (e.g. application/json).
|
|400|Content-Type|string||Content-Type header (e.g. application/json).
|
|400|x-request-id|string|Uuid|Request identifier.
|
|401|Accept|string||Content-Type header (e.g. application/json).
|
|401|Content-Type|string||Content-Type header (e.g. application/json).
|
|401|x-request-id|string|Uuid|Request identifier.
|
|403|Accept|string||Content-Type header (e.g. application/json).
|
|403|Content-Type|string||Content-Type header (e.g. application/json).
|
|403|x-request-id|string|Uuid|Request identifier.
|
|404|Accept|string||Content-Type header (e.g. application/json).
|
|404|Content-Type|string||Content-Type header (e.g. application/json).
|
|404|x-request-id|string|Uuid|Request identifier.
|
|406|Accept|string||Content-Type header (e.g. application/json).
|
|406|Content-Type|string||Content-Type header (e.g. application/json).
|
|406|x-request-id|string|Uuid|Request identifier.
|
|409|Accept|string||Content-Type header (e.g. application/json).
|
|409|Content-Type|string||Content-Type header (e.g. application/json).
|
|409|x-request-id|string|Uuid|Request identifier.
|
|500|Accept|string||Content-Type header (e.g. application/json).
|
|500|Content-Type|string||Content-Type header (e.g. application/json).
|
|500|x-request-id|string|Uuid|Request identifier.
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
    "driver_self_assignment": true,
    "id": 1,
    "is_active": true,
    "name": "CRO Scrap",
    "use_additional_items": true
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
  "sales_rep_id": "1",
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
|`sales_rep_id`|string|Sales rep identifier. May be an integer provider id, the sales user UUID, or the username.|
|`suspension_id`|integer(int64)|Suspension identifier.|

<h2 id="tocScreatedispatchcustomerlocationmodel">CreateDispatchCustomerLocationModel</h2>

```json
{
  "is_commercial": true,
  "note": "A note about something",
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "sales_rep_id": "1",
  "suspension_id": 1
}

```

<a id="schemacreatedispatchcustomerlocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`is_commercial`|boolean|Commercial address if true, private if false.|
|`note`|string|Notes (free text).|
|`reference_number`|string|Reference number (free text).|
|`renewal_date`|string(DateTime)|Renewal date.|
|`sales_rep`|string|Name of sales representative.|
|`sales_rep_id`|string|Sales rep identifier. May be an integer provider id, the sales user UUID, or the username.|
|`suspension_id`|integer(int64)|Suspension identifier.|

<h2 id="tocScreatedriverchatmessagemodel">CreateDriverChatMessageModel</h2>

```json
{
  "receiver": {
    "id": 1,
    "type": "dispatcher"
  },
  "text": "Hello, World!"
}

```

<a id="schemacreatedriverchatmessagemodel"></a>

|Name|Type|Description|
|---|---|---|
|`receiver`|[DriverChatUserModel](#schemadriverchatusermodel)|-|
|`text`|string(DateTime)|Message text.|

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
      "country": "US",
      "id": 1,
      "is_active": true,
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
  "country": "US",
  "id": 1,
  "is_active": true,
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
|`country`|string|Country code (ISO 3166-1 alpha 2).|
|`id`|integer(int64)|Customer address identifier.|
|`is_active`|boolean|Records marked inactive are treated as deleted (soft delete).|
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
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "id": 1,
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
  "email": "john@crosoftware.net, jane@crosoftware.net",
  "fax": "+1 (360) 123-6543",
  "id": 1,
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
|`email`|string(Email)|Email address comma-separated list.|
|`fax`|string(PhoneNumber)|Fax number (free text).|
|`id`|integer(int64)|Customer contact identifier.|
|`name`|string|Name (free text).|
|`notify_on_acknowledged_request`|boolean|Notify on acknowledge request.|
|`notify_on_completed_request`|boolean|Notify on completed request.|
|`notify_on_dispatched_request`|boolean|Notify on dispatched request.|
|`notify_on_failed_request`|boolean|Notify on failed request.|
|`notify_on_new_request`|boolean|Notify on new request.|
|`number`|string(PhoneNumber)|Phone number (free text).|

<h2 id="tocScustomermodel">CustomerModel</h2>

```json
{
  "addresses": [
    {
      "country": "US",
      "id": 1,
      "is_active": true,
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
  "contacts": [
    {
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "id": 1,
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "created_on": "2049-10-31T11:32:38.390000",
  "id": 1,
  "last_updated_on": "2049-10-31T11:32:38.390000",
  "locations": [
    {
      "addresses": [
        {
          "country": "US",
          "id": 1,
          "is_active": true,
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
      "contacts": [
        {
          "email": "john@crosoftware.net, jane@crosoftware.net",
          "fax": "+1 (360) 123-6543",
          "id": 1,
          "name": "John Doe",
          "notify_on_acknowledged_request": true,
          "notify_on_completed_request": true,
          "notify_on_dispatched_request": true,
          "notify_on_failed_request": true,
          "notify_on_new_request": true,
          "number": "+1 (360) 123-6543"
        }
      ],
      "created_on": "2049-10-31T11:32:38.390000",
      "customer_id": 1,
      "is_active": true,
      "is_commercial": true,
      "last_updated_on": "2049-10-31T11:32:38.390000",
      "location_id": 1,
      "name": "John Doe",
      "note": "A note about something",
      "parent_id": 0,
      "reference_number": "A140",
      "renewal_date": "2049-10-31T11:32:38.390000",
      "sales_rep": "Jane Johnson",
      "sales_rep_id": "1",
      "suspension_id": 1
    }
  ],
  "name": "John Doe",
  "parent_id": 0
}

```

<a id="schemacustomermodel"></a>

|Name|Type|Description|
|---|---|---|
|`addresses`|array[[CustomerAddressModel](#schemacustomeraddressmodel)]|-|
|`contacts`|array[[CustomerContactModel](#schemacustomercontactmodel)]|-|
|`created_on`|string(DateTime)|Timestamp of creation (must be in past).|
|`id`|integer(int64)|Customer identifier.|
|`last_updated_on`|string(DateTime)|-|
|`locations`|array[[DispatchCustomerLocationModel](#schemadispatchcustomerlocationmodel)]|-|
|`name`|string|Name (free text).|
|`parent_id`|integer(int64)|Parent record identifier.|

<h2 id="tocSdispatchcustomerlocationlistmodel">DispatchCustomerLocationListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "addresses": [
        {
          "country": "US",
          "id": 1,
          "is_active": true,
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
      "contacts": [
        {
          "email": "john@crosoftware.net, jane@crosoftware.net",
          "fax": "+1 (360) 123-6543",
          "id": 1,
          "name": "John Doe",
          "notify_on_acknowledged_request": true,
          "notify_on_completed_request": true,
          "notify_on_dispatched_request": true,
          "notify_on_failed_request": true,
          "notify_on_new_request": true,
          "number": "+1 (360) 123-6543"
        }
      ],
      "created_on": "2049-10-31T11:32:38.390000",
      "customer_id": 1,
      "is_active": true,
      "is_commercial": true,
      "last_updated_on": "2049-10-31T11:32:38.390000",
      "location_id": 1,
      "name": "John Doe",
      "note": "A note about something",
      "parent_id": 0,
      "reference_number": "A140",
      "renewal_date": "2049-10-31T11:32:38.390000",
      "sales_rep": "Jane Johnson",
      "sales_rep_id": "1",
      "suspension_id": 1
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schemadispatchcustomerlocationlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[DispatchCustomerLocationModel](#schemadispatchcustomerlocationmodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocSdispatchcustomerlocationmodel">DispatchCustomerLocationModel</h2>

```json
{
  "addresses": [
    {
      "country": "US",
      "id": 1,
      "is_active": true,
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
  "contacts": [
    {
      "email": "john@crosoftware.net, jane@crosoftware.net",
      "fax": "+1 (360) 123-6543",
      "id": 1,
      "name": "John Doe",
      "notify_on_acknowledged_request": true,
      "notify_on_completed_request": true,
      "notify_on_dispatched_request": true,
      "notify_on_failed_request": true,
      "notify_on_new_request": true,
      "number": "+1 (360) 123-6543"
    }
  ],
  "created_on": "2049-10-31T11:32:38.390000",
  "customer_id": 1,
  "is_active": true,
  "is_commercial": true,
  "last_updated_on": "2049-10-31T11:32:38.390000",
  "location_id": 1,
  "name": "John Doe",
  "note": "A note about something",
  "parent_id": 0,
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "sales_rep_id": "1",
  "suspension_id": 1
}

```

<a id="schemadispatchcustomerlocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`addresses`|array[[CustomerAddressModel](#schemacustomeraddressmodel)]|-|
|`contacts`|array[[CustomerContactModel](#schemacustomercontactmodel)]|-|
|`created_on`|string(DateTime)|Timestamp of creation (must be in past).|
|`customer_id`|integer(int64)|Customer identifier.|
|`is_active`|boolean|Records marked inactive are treated as deleted (soft delete).|
|`is_commercial`|boolean|Commercial address if true, private if false.|
|`last_updated_on`|string(DateTime)|-|
|`location_id`|integer(int64)|Location identifier.|
|`name`|string|Name (free text).|
|`note`|string|Notes (free text).|
|`parent_id`|integer(int64)|Parent record identifier.|
|`reference_number`|string|Reference number (free text).|
|`renewal_date`|string(DateTime)|Renewal date.|
|`sales_rep`|string|Name of sales representative.|
|`sales_rep_id`|string|Sales rep identifier. May be an integer provider id, the sales user UUID, or the username.|
|`suspension_id`|integer(int64)|Suspension identifier.|

<h2 id="tocSdriverchatmessagelistmodel">DriverChatMessageListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "id": 1,
      "is_edited": 1,
      "is_read": 1,
      "last_edited_on": "2049-10-31T11:32:38.390000",
      "receiver": {
        "id": 1,
        "type": "dispatcher"
      },
      "sender": {
        "id": 1,
        "type": "dispatcher"
      },
      "sent_on": "2049-10-31T11:32:38.390000",
      "text": "Hello, World!"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schemadriverchatmessagelistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[DriverChatMessageModel](#schemadriverchatmessagemodel)]|-|
|`total_count`|integer(int64)|Paged results total viewable records.|
|`total_pages`|integer(int64)|Paged results total pages.|

<h2 id="tocSdriverchatmessagemodel">DriverChatMessageModel</h2>

```json
{
  "id": 1,
  "is_edited": 1,
  "is_read": 1,
  "last_edited_on": "2049-10-31T11:32:38.390000",
  "receiver": {
    "id": 1,
    "type": "dispatcher"
  },
  "sender": {
    "id": 1,
    "type": "dispatcher"
  },
  "sent_on": "2049-10-31T11:32:38.390000",
  "text": "Hello, World!"
}

```

<a id="schemadriverchatmessagemodel"></a>

|Name|Type|Description|
|---|---|---|
|`id`|integer(int64)|Driver chat message identifier.|
|`is_edited`|boolean|True if message has been changed.|
|`is_read`|boolean|True if message has been changed.|
|`last_edited_on`|string(DateTime)|Message last edit date.|
|`receiver`|[DriverChatUserModel](#schemadriverchatusermodel)|-|
|`sender`|[DriverChatUserModel](#schemadriverchatusermodel)|-|
|`sent_on`|string(DateTime)|Message sent date.|
|`text`|string(DateTime)|Message text.|

<h2 id="tocSdriverchatrecipientmodel">DriverChatRecipientModel</h2>

```json
{
  "id": 1,
  "name": "John Doe",
  "type": "dispatcher"
}

```

<a id="schemadriverchatrecipientmodel"></a>

|Name|Type|Description|
|---|---|---|
|`id`|integer(int64)|Driver chat message identifier.|
|`name`|string|Recipient name.|
|`type`|string|Recipient user account type.|

<h2 id="tocSdriverchatusermodel">DriverChatUserModel</h2>

```json
{
  "id": 1,
  "type": "dispatcher"
}

```

<a id="schemadriverchatusermodel"></a>

|Name|Type|Description|
|---|---|---|
|`id`|integer(int64)|Driver chat message identifier.|
|`type`|string|Recipient user account type.|

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
|`city`|string|Driver city.|
|`disable_shift_tracking`|boolean|Disable shift tracking.|
|`email`|string(Email)|Email address.|
|`id`|integer(int64)|Resource identifier.|
|`license_number`|string|Driver's license number.|
|`location_id`|integer(int64)|Location identifier.|
|`name`|string|Name (free text).|
|`phone_number`|string(PhoneNumber)|Phone number.|
|`state`|string|Driver state.|
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
      "contact_email": "john@crosoftware.net, jane@crosoftware.net",
      "contact_name": "Sequim",
      "contact_phone": "Sequim",
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
  "contact_email": "john@crosoftware.net, jane@crosoftware.net",
  "contact_name": "Sequim",
  "contact_phone": "Sequim",
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
|`city`|string|City.|
|`contact_email`|string(Email)|Email address comma-separated list.|
|`contact_name`|string|Contact name.|
|`contact_phone`|string|Contact phone number.|
|`description`|string|Dump destination description.|
|`id`|integer(int64)|Resource identifier.|
|`is_holding_yard`|boolean|Location is holding yard.|
|`latitude`|number(float)|Latitude.|
|`location_id`|integer(int64)|Location identifier.|
|`longitude`|number(float)|longitude.|
|`state`|string|State.|
|`zip`|string|Zip code.|

<h2 id="tocSemptycontentresponsemodel">EmptyContentResponseModel</h2>

```json
{}

```

<a id="schemaemptycontentresponsemodel"></a>

*None*

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
|`detail`|string|Error details.|
|`explanation`|string|General explanation.|
|`title`|string|Error summary.|

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
          "driver_self_assignment": true,
          "id": 1,
          "is_active": true,
          "name": "CRO Scrap",
          "use_additional_items": true
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
      "created_with_portal": true,
      "customer": {
        "addresses": [
          {
            "country": "US",
            "id": 1,
            "is_active": true,
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
        "contacts": [
          {
            "email": "john@crosoftware.net, jane@crosoftware.net",
            "fax": "+1 (360) 123-6543",
            "id": 1,
            "name": "John Doe",
            "notify_on_acknowledged_request": true,
            "notify_on_completed_request": true,
            "notify_on_dispatched_request": true,
            "notify_on_failed_request": true,
            "notify_on_new_request": true,
            "number": "+1 (360) 123-6543"
          }
        ],
        "created_on": "2049-10-31T11:32:38.390000",
        "id": 1,
        "last_updated_on": "2049-10-31T11:32:38.390000",
        "locations": [
          {
            "addresses": [
              {
                "country": "US",
                "id": 1,
                "is_active": true,
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
            "contacts": [
              {
                "email": "john@crosoftware.net, jane@crosoftware.net",
                "fax": "+1 (360) 123-6543",
                "id": 1,
                "name": "John Doe",
                "notify_on_acknowledged_request": true,
                "notify_on_completed_request": true,
                "notify_on_dispatched_request": true,
                "notify_on_failed_request": true,
                "notify_on_new_request": true,
                "number": "+1 (360) 123-6543"
              }
            ],
            "created_on": "2049-10-31T11:32:38.390000",
            "customer_id": 1,
            "is_active": true,
            "is_commercial": true,
            "last_updated_on": "2049-10-31T11:32:38.390000",
            "location_id": 1,
            "name": "John Doe",
            "note": "A note about something",
            "parent_id": 0,
            "reference_number": "A140",
            "renewal_date": "2049-10-31T11:32:38.390000",
            "sales_rep": "Jane Johnson",
            "sales_rep_id": "1",
            "suspension_id": 1
          }
        ],
        "name": "John Doe",
        "parent_id": 0
      },
      "customer_id": 1,
      "customer_notes": "A note entered by a customer",
      "departed_on": "2049-10-31T11:32:38.390000",
      "desired_asset_desc": "A note entered by a driver",
      "dispatch_priority": "H",
      "dispatched_by_route": 1,
      "dispatched_on": "2049-10-31T11:32:38.390000",
      "dispatcher_notes": "A note entered by a dispatcher.",
      "do_confirm": true,
      "driver_notes": "A note entered by a driver.",
      "dropped_number": "string",
      "dump_location": {
        "address": "123 Some St.",
        "city": "Sequim",
        "contact_email": "john@crosoftware.net, jane@crosoftware.net",
        "contact_name": "Sequim",
        "contact_phone": "Sequim",
        "description": "A user entered/human readable text description.",
        "id": 1,
        "is_holding_yard": true,
        "latitude": 56.2,
        "location_id": 1,
        "longitude": 128.1,
        "state": "WA",
        "zip": "98368"
      },
      "dump_location_id": 2,
      "dumped_on": "2049-10-31T11:32:38.390000",
      "end_time": "2049-10-31T11:32:38.390000",
      "fail_reason": "A failure description selected by a driver.",
      "final_location": {
        "address": "123 Some St.",
        "city": "Sequim",
        "contact_email": "john@crosoftware.net, jane@crosoftware.net",
        "contact_name": "Sequim",
        "contact_phone": "Sequim",
        "description": "A user entered/human readable text description.",
        "id": 1,
        "is_holding_yard": true,
        "latitude": 56.2,
        "location_id": 1,
        "longitude": 128.1,
        "state": "WA",
        "zip": "98368"
      },
      "final_location_id": 1,
      "flags": "Notes about a job.",
      "id": 1,
      "invoice_notes": "Notes from a billing invoice",
      "is_completed": true,
      "is_declined": true,
      "is_deleted": true,
      "is_failed": true,
      "is_paid": true,
      "job_group_id": 1,
      "last_updated_on": "2049-10-31T11:32:38.390000",
      "location_id": 1,
      "materials": [
        {
          "heavy_weight": 39254.44,
          "light_weight": 34523.11,
          "material_item_id": 1,
          "material_name": "43A",
          "tare_weight": 32358.15
        }
      ],
      "merged_with_route": 1,
      "original_schedule_date": "2049-10-31T11:32:38.390000",
      "pickup_date": "2049-10-31T11:32:38.390000",
      "pickup_item": 1,
      "priority": -3,
      "reference_number": "A140",
      "removed_number": "string",
      "requested_on": "2049-10-31T11:32:38.390000",
      "require_image": true,
      "require_material": true,
      "require_signature": true,
      "require_weights": true,
      "scale_ticket": "A5100",
      "schedule_date": "2049-10-31T11:32:38.390000",
      "start_location": {
        "address": "123 Some St.",
        "city": "Sequim",
        "contact_email": "john@crosoftware.net, jane@crosoftware.net",
        "contact_name": "Sequim",
        "contact_phone": "Sequim",
        "description": "A user entered/human readable text description.",
        "id": 1,
        "is_holding_yard": true,
        "latitude": 56.2,
        "location_id": 1,
        "longitude": 128.1,
        "state": "WA",
        "zip": "98368"
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

<h2 id="tocSjobmaterialmodel">JobMaterialModel</h2>

```json
{
  "heavy_weight": 39254.44,
  "light_weight": 34523.11,
  "material_item_id": 1,
  "material_name": "43A",
  "tare_weight": 32358.15
}

```

<a id="schemajobmaterialmodel"></a>

|Name|Type|Description|
|---|---|---|
|`heavy_weight`|number(float)|-|
|`light_weight`|number(float)|-|
|`material_item_id`|integer(int64)|Job materials identifier.|
|`material_name`|string|Job material name.|
|`tare_weight`|number(float)|-|

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
      "driver_self_assignment": true,
      "id": 1,
      "is_active": true,
      "name": "CRO Scrap",
      "use_additional_items": true
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
  "created_with_portal": true,
  "customer": {
    "addresses": [
      {
        "country": "US",
        "id": 1,
        "is_active": true,
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
    "contacts": [
      {
        "email": "john@crosoftware.net, jane@crosoftware.net",
        "fax": "+1 (360) 123-6543",
        "id": 1,
        "name": "John Doe",
        "notify_on_acknowledged_request": true,
        "notify_on_completed_request": true,
        "notify_on_dispatched_request": true,
        "notify_on_failed_request": true,
        "notify_on_new_request": true,
        "number": "+1 (360) 123-6543"
      }
    ],
    "created_on": "2049-10-31T11:32:38.390000",
    "id": 1,
    "last_updated_on": "2049-10-31T11:32:38.390000",
    "locations": [
      {
        "addresses": [
          {
            "country": "US",
            "id": 1,
            "is_active": true,
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
        "contacts": [
          {
            "email": "john@crosoftware.net, jane@crosoftware.net",
            "fax": "+1 (360) 123-6543",
            "id": 1,
            "name": "John Doe",
            "notify_on_acknowledged_request": true,
            "notify_on_completed_request": true,
            "notify_on_dispatched_request": true,
            "notify_on_failed_request": true,
            "notify_on_new_request": true,
            "number": "+1 (360) 123-6543"
          }
        ],
        "created_on": "2049-10-31T11:32:38.390000",
        "customer_id": 1,
        "is_active": true,
        "is_commercial": true,
        "last_updated_on": "2049-10-31T11:32:38.390000",
        "location_id": 1,
        "name": "John Doe",
        "note": "A note about something",
        "parent_id": 0,
        "reference_number": "A140",
        "renewal_date": "2049-10-31T11:32:38.390000",
        "sales_rep": "Jane Johnson",
        "sales_rep_id": "1",
        "suspension_id": 1
      }
    ],
    "name": "John Doe",
    "parent_id": 0
  },
  "customer_id": 1,
  "customer_notes": "A note entered by a customer",
  "departed_on": "2049-10-31T11:32:38.390000",
  "desired_asset_desc": "A note entered by a driver",
  "dispatch_priority": "H",
  "dispatched_by_route": 1,
  "dispatched_on": "2049-10-31T11:32:38.390000",
  "dispatcher_notes": "A note entered by a dispatcher.",
  "do_confirm": true,
  "driver_notes": "A note entered by a driver.",
  "dropped_number": "string",
  "dump_location": {
    "address": "123 Some St.",
    "city": "Sequim",
    "contact_email": "john@crosoftware.net, jane@crosoftware.net",
    "contact_name": "Sequim",
    "contact_phone": "Sequim",
    "description": "A user entered/human readable text description.",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 56.2,
    "location_id": 1,
    "longitude": 128.1,
    "state": "WA",
    "zip": "98368"
  },
  "dump_location_id": 2,
  "dumped_on": "2049-10-31T11:32:38.390000",
  "end_time": "2049-10-31T11:32:38.390000",
  "fail_reason": "A failure description selected by a driver.",
  "final_location": {
    "address": "123 Some St.",
    "city": "Sequim",
    "contact_email": "john@crosoftware.net, jane@crosoftware.net",
    "contact_name": "Sequim",
    "contact_phone": "Sequim",
    "description": "A user entered/human readable text description.",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 56.2,
    "location_id": 1,
    "longitude": 128.1,
    "state": "WA",
    "zip": "98368"
  },
  "final_location_id": 1,
  "flags": "Notes about a job.",
  "id": 1,
  "invoice_notes": "Notes from a billing invoice",
  "is_completed": true,
  "is_declined": true,
  "is_deleted": true,
  "is_failed": true,
  "is_paid": true,
  "job_group_id": 1,
  "last_updated_on": "2049-10-31T11:32:38.390000",
  "location_id": 1,
  "materials": [
    {
      "heavy_weight": 39254.44,
      "light_weight": 34523.11,
      "material_item_id": 1,
      "material_name": "43A",
      "tare_weight": 32358.15
    }
  ],
  "merged_with_route": 1,
  "original_schedule_date": "2049-10-31T11:32:38.390000",
  "pickup_date": "2049-10-31T11:32:38.390000",
  "pickup_item": 1,
  "priority": -3,
  "reference_number": "A140",
  "removed_number": "string",
  "requested_on": "2049-10-31T11:32:38.390000",
  "require_image": true,
  "require_material": true,
  "require_signature": true,
  "require_weights": true,
  "scale_ticket": "A5100",
  "schedule_date": "2049-10-31T11:32:38.390000",
  "start_location": {
    "address": "123 Some St.",
    "city": "Sequim",
    "contact_email": "john@crosoftware.net, jane@crosoftware.net",
    "contact_name": "Sequim",
    "contact_phone": "Sequim",
    "description": "A user entered/human readable text description.",
    "id": 1,
    "is_holding_yard": true,
    "latitude": 56.2,
    "location_id": 1,
    "longitude": 128.1,
    "state": "WA",
    "zip": "98368"
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
|`created_with_portal`|boolean|Set record active state.|
|`customer`|[CustomerModel](#schemacustomermodel)|-|
|`customer_id`|integer(int64)|Customer identifier.|
|`customer_notes`|string|Notes entered by customers to communicate with dispatchers.|
|`departed_on`|string(DateTime)|-|
|`desired_asset_desc`|string|Free-form text entered by dispatchers and drivers to be used as the future asset description.|
|`dispatch_priority`|string|Entered by dispatchers to determine dispatch order.|
|`dispatched_by_route`|integer(int64)|Route id of dispatching route (or NULL if not dispatched by a route).|
|`dispatched_on`|string(DateTime)|Time the job is assigned to a truck.|
|`dispatcher_notes`|string|Entered by dispatchers, read by drivers and dispatchers.|
|`do_confirm`|boolean|Tell dispatcher that a customer should be contacted before job is dispatched.|
|`driver_notes`|string|Entered by drivers when completing or failing a job for dispatchers.|
|`dropped_number`|string|-|
|`dump_location`|[DumpDestinationModel](#schemadumpdestinationmodel)|-|
|`dump_location_id`|integer(int64)|Asset or asset cluster dump location identifier (e.g. trash bin needs dumped before returning from customer).|
|`dumped_on`|string(DateTime)|Dump request completion date.|
|`end_time`|string(DateTime)|Future estimated time of job completion.|
|`fail_reason`|string|Failure description selected by a driver for use by dispatchers.|
|`final_location`|[DumpDestinationModel](#schemadumpdestinationmodel)|-|
|`final_location_id`|integer(int64)|Final location identifier. Used by dispatchers for prioritizing jobs. Used by drivers to know where to leave the asset on job completion.|
|`flags`|string|Job notes.|
|`id`|integer(int64)|Job identifier.|
|`invoice_notes`|string|Invoice notes from the billing system.|
|`is_completed`|boolean|Job completion flag set by dispatchers and drivers.|
|`is_declined`|boolean|Job completion flag set by dispatchers and drivers.|
|`is_deleted`|boolean|Indicates whether job is still valid.|
|`is_failed`|boolean|Set by drivers and dispatchers to indicate a failed job.|
|`is_paid`|boolean|-|
|`job_group_id`|integer(int64)|Job group identifier for group jobs (vs service, exchange, etc.).|
|`last_updated_on`|string(DateTime)|-|
|`location_id`|integer(int64)|Location identifier.|
|`materials`|array[[JobMaterialModel](#schemajobmaterialmodel)]|-|
|`merged_with_route`|integer(int64)|Assigned by dispatchers for dispatchers and drivers.|
|`original_schedule_date`|string(DateTime)|Original scheduling date.|
|`pickup_date`|string(DateTime)|A pickup job is scheduled for this date upon job completion. If the asset or cluster is assigned to a route stop, the route stop will be deleted. Must be in the future.|
|`pickup_item`|integer(int64)|-|
|`priority`|integer(int64)|Assigned by dispatchers for job order completion determination for drivers.|
|`reference_number`|string|Reference number (free text).|
|`removed_number`|string|-|
|`requested_on`|string(DateTime)|Requested date.|
|`require_image`|boolean|Set by dispatchers and drivers, requires drivers to upload one or more job images before completion.|
|`require_material`|boolean|Set by dispatchers and drivers, requires drivers to set a material before completing a job.|
|`require_signature`|boolean|Set by dispatchers and drivers, requires drivers to get a customer signature before job completion.|
|`require_weights`|boolean|Set by disptachers and drivers, requires drivers to set material weights before job completion.|
|`scale_ticket`|string|Scale ticket.|
|`schedule_date`|string(DateTime)|Scheduled job completion date.|
|`start_location`|[DumpDestinationModel](#schemadumpdestinationmodel)|-|
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
      "driver_self_assignment": true,
      "id": 1,
      "is_active": true,
      "name": "CRO Scrap",
      "use_additional_items": true
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
  "driver_self_assignment": true,
  "id": 1,
  "is_active": true,
  "name": "CRO Scrap",
  "use_additional_items": true
}

```

<a id="schemalocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`driver_self_assignment`|boolean|Driver can self assign.|
|`id`|integer(int64)|Location identifier.|
|`is_active`|boolean|Records marked inactive are treated as deleted (soft delete).|
|`name`|string|Name for a location.|
|`use_additional_items`|boolean|Use additional items.|

<h2 id="tocSmaterialmodel">MaterialModel</h2>

```json
{
  "created_on": "2049-10-31T11:32:38.390000",
  "description": "A user entered/human readable text description.",
  "factor": 1.1,
  "group_description": "A user entered/human readable text description.",
  "id": 1,
  "line_item_id": 1,
  "location_id": 1,
  "unit_price": 12.75,
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
|`line_item_id`|integer(int64)|Line item identifier.|
|`location_id`|integer(int64)|Location identifier.|
|`unit_price`|number(float)|Job material name.|
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
      "truck_limit": 30,
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
  "truck_limit": 30,
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
  "results": [
    {
      "approved_by": 1,
      "approved_on": "2049-10-31T11:32:38.390000",
      "denied_on": "2049-10-31T11:32:38.390000",
      "is_approved": true,
      "location_id": 1,
      "provider_id": 1,
      "provider_name": "John Doe",
      "requested_on": "2049-10-31T11:32:38.390000",
      "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f"
    }
  ],
  "total_count": 1001,
  "total_pages": 3
}

```

<a id="schemathirdpartyhaulerconnectionlistmodel"></a>

|Name|Type|Description|
|---|---|---|
|`current_limit`|integer(int64)|Maximun number of results per page.|
|`current_page`|integer(int64)|Paged results page index (starting from 1).|
|`results`|array[[ThirdPartyHaulerConnectionModel](#schemathirdpartyhaulerconnectionmodel)]|-|
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
  "provider_id": 1,
  "provider_name": "John Doe",
  "requested_on": "2049-10-31T11:32:38.390000",
  "third_party_hauler_id": "9f34f340-54d2-4403-a53b-d8017a64734f"
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
|`provider_id`|integer(int64)|Bin provider identifier.|
|`provider_name`|string|Name (free text).|
|`requested_on`|string(DateTime)|Requested date.|
|`third_party_hauler_id`|string(Uuid)|Third party hauler identifier.|

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

<h2 id="tocSupdatedispatchcustomerlocationmodel">UpdateDispatchCustomerLocationModel</h2>

```json
{
  "is_active": true,
  "is_commercial": true,
  "note": "A note about something",
  "reference_number": "A140",
  "renewal_date": "2049-10-31T11:32:38.390000",
  "sales_rep": "Jane Johnson",
  "sales_rep_id": "1",
  "suspension_id": 1
}

```

<a id="schemaupdatedispatchcustomerlocationmodel"></a>

|Name|Type|Description|
|---|---|---|
|`is_active`|boolean|Records marked inactive are treated as deleted (soft delete).|
|`is_commercial`|boolean|Commercial address if true, private if false.|
|`note`|string|Notes (free text).|
|`reference_number`|string|Reference number (free text).|
|`renewal_date`|string(DateTime)|Renewal date.|
|`sales_rep`|string|Name of sales representative.|
|`sales_rep_id`|string|Sales rep identifier. May be an integer provider id, the sales user UUID, or the username.|
|`suspension_id`|integer(int64)|Suspension identifier.|

<h2 id="tocSupdatedriverchatmessagemodel">UpdateDriverChatMessageModel</h2>

```json
{
  "is_read": 1,
  "text": "Hello, World!"
}

```

<a id="schemaupdatedriverchatmessagemodel"></a>

|Name|Type|Description|
|---|---|---|
|`is_read`|boolean|True if message has been changed.|
|`text`|string(DateTime)|Message text.|

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

<h2 id="tocSuserlistresultsmodel">UserListResultsModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "dispatcher_id": 1,
      "id": 1,
      "roles": [
        "Dispatcher"
      ],
      "uid": "9f34f340-54d2-4403-a53b-d8017a64734f",
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
  "dispatcher_id": 1,
  "id": 1,
  "roles": [
    "Dispatcher"
  ],
  "uid": "9f34f340-54d2-4403-a53b-d8017a64734f",
  "username": "test_user_1000"
}

```

<a id="schemausermodel"></a>

|Name|Type|Description|
|---|---|---|
|`dispatcher_id`|integer(int64)|Resource identifier.|
|`id`|integer(int64)|User identifier.|
|`roles`|array[string]|User role.|
|`uid`|string(Uuid)|Identity UUID.|
|`username`|string|Username.|

<h2 id="tocSwebhooklistmodel">WebhookListModel</h2>

```json
{
  "current_limit": 100,
  "current_page": 1,
  "results": [
    {
      "deleted_at": "2049-10-31T11:32:38.390000",
      "events": [
        "Customer"
      ],
      "id": 1,
      "last_http_fail": "1",
      "last_http_success": "1",
      "secret": "<Secret>",
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
  "deleted_at": "2049-10-31T11:32:38.390000",
  "events": [
    "Customer"
  ],
  "id": 1,
  "last_http_fail": "1",
  "last_http_success": "1",
  "secret": "<Secret>",
  "url": "https://test.url"
}

```

<a id="schemawebhookmodel"></a>

|Name|Type|Description|
|---|---|---|
|`deleted_at`|string(DateTime)|Denial date.|
|`events`|array[string]|Hook event.|
|`id`|integer(int64)|Resource identifier.|
|`last_http_fail`|string(DateTime)|Last time of url webhook execution failure.|
|`last_http_success`|string(DateTime)|Last time of url webhook execution success.|
|`secret`|string|Response body HMAC signing key.|
|`url`|string(Url)|Callback URL.|

<h2 id="tocSwebhookpingresultmodel">WebhookPingResultModel</h2>

```json
{
  "delivery_id": "1",
  "http_status": 200,
  "message": "1"
}

```

<a id="schemawebhookpingresultmodel"></a>

|Name|Type|Description|
|---|---|---|
|`delivery_id`|string(Uuid)|Hook execution identifier.|
|`http_status`|integer(int64)|HTTP status return code.|
|`message`|string|Description of ping result.|

