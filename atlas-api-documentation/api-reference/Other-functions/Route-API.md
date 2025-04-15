# City Pairs API

The "City pairs API" can be used to download the city pairs supported by Atlas as well as by the airlines. The customer can use this structured data and transfer the city pair information into their mid-back office systems.

**This API is only available in the production environment.**

## Dependency

There is no dependency for this call.

## Endpoint

[https://xxxx.xxxxxxxx.com/route/export.do](https://xxxx.xxxxxxxx.com/route/export.do)

## Request

{% tabs %}
{% tab title="Schema" %}
### **routeType**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Type of route being queried.  

  Valid values:

  1 = Airline routes

  2 = Atlas routes
- **Constraints:**  
- **Default:** None  
- **Example:** `1`

### **airlines**
- **Type:** Array of Strings  
- **Required:** No  
- **Description:** List of preferred airline codes to filter routes.  
- **Constraints:** Must be valid 2-letter IATA airline codes.  
- **Default:** `[]`  
- **Example:** `["EI"]`

### **fromCity**
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA airport or city code representing the departure location.  
- **Constraints:** Must be a valid 3-letter IATA code.  
- **Default:** None  
- **Example:** `"DUB"`

### **fromCountry**
- **Type:** String  
- **Required:** Yes  
- **Description:** ISO 3166-1 alpha-2 country code of the departure location.  
- **Constraints:** Must be a valid 2-letter country code.  
- **Default:** None  
- **Example:** `"IE"`

### **toCity**
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA airport or city code representing the destination location.  
- **Constraints:** Must be a valid 3-letter IATA code.  
- **Default:** None  
- **Example:** `"SAN"`

### **toCountry**
- **Type:** String  
- **Required:** Yes  
- **Description:** ISO 3166-1 alpha-2 country code of the destination location.  
- **Constraints:** Must be a valid 2-letter country code.  
- **Default:** None  
- **Example:** `"IE"`

{% endtab %}

{% tab title="Samples" %}
```
{
    "routeType": 1,
  
    "fromCity": "LON",
    "fromCountry": "GB",
    "toCity": "AMS",
    "toCountry": "NL"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}

### **data**
- **Type:** Array of Objects  
- **Required:** Yes  
- **Description:** List of available route schedules matching the search criteria.  
- **Constraints:** Can be empty if no routes are available.  
- **Default:** `[]`  
- **Example:**
  ```json
  [
    {
      "airlines": ["EI"],
      "fromCity": "DUB",
      "fromCountry": "IE",
      "toCity": "SAN",
      "toCountry": "IE",
      "isDirect": false,
      "scheduleStart": "20241024",
      "scheduleEnd": "20250428",
      "updateDate": "20241031"
    }
  ]
  ```

### **data[].airlines**
- **Type:** Array of Strings  
- **Required:** Yes  
- **Description:** List of airline codes operating the route.  
- **Constraints:** Must be valid 2-letter IATA airline codes.  
- **Default:** `[]`  
- **Example:** `["EI"]`

### **data[].fromCity**
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA code for the departure city/airport.  
- **Constraints:** Must be a valid 3-letter code.  
- **Default:** None  
- **Example:** `"DUB"`

### **data[].fromCountry**
- **Type:** String  
- **Required:** Yes  
- **Description:** ISO 3166-1 alpha-2 code of the departure country.  
- **Constraints:** Must be a valid 2-letter country code.  
- **Default:** None  
- **Example:** `"IE"`

### **data[].toCity**
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA code for the destination city/airport.  
- **Constraints:** Must be a valid 3-letter code.  
- **Default:** None  
- **Example:** `"SAN"`

### **data[].toCountry**
- **Type:** String  
- **Required:** Yes  
- **Description:** ISO 3166-1 alpha-2 code of the destination country.  
- **Constraints:** Must be a valid 2-letter country code.  
- **Default:** None  
- **Example:** `"IE"`

### **data[].isDirect**
- **Type:** Boolean  
- **Required:** Yes  
- **Description:** Indicates whether the route is a direct flight.  

  Valid values:

  True: Direct Flight 

  False: Transfer Flight 

  This data will only be available when the "routeType" = 2 (Atlas Routes)
- **Constraints:** `true` = direct flight, `false` = includes stops or connections.  
- **Default:** `false`  
- **Example:** `false`

### **data[].scheduleStart**
- **Type:** String  
- **Required:** Yes  
- **Description:** The start date of the booking window. The format is YYYYMMDD.  
- **Constraints:** Must be a valid date string.  
- **Default:** None  
- **Example:** `"20241024"`

### **data[].scheduleEnd**
- **Type:** String  
- **Required:** Yes  
- **Description:**  The end date of the booking window. The format is YYYYMMDD.
- **Constraints:** Must be a valid date string.  
- **Default:** None  
- **Example:** `"20250428"`

### **data[].updateDate**
- **Type:** String  
- **Required:** Yes  
- **Description:** The date when the routing data was updated. The format is YYYYMMDD.
- **Constraints:** Must be a valid date string.  
- **Default:** None  
- **Example:** `"20241031"`

### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Response status code.  
- **Constraints:** 0 indicates success.  
- **Default:** 0  
- **Example:** 0  

### **msg**
- **Type:** String  
- **Required:** No  
- **Description:** Response message.  
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** null  
    
{% endtab %}

{% tab title="Samples" %}
```
{
  "data": [
    {
      "airlines": [
        "U2"
      ],
      "fromCity": "LON",
      "fromCountry": "GB",
      "toCity": "AMS",
      "toCountry": "NL",
      "isDirect": null,
      "scheduleStart": null,
      "scheduleEnd": null,
      "updateDate": "20250408"
    },
    {
      "airlines": [
        "DS"
      ],
      "fromCity": "LON",
      "fromCountry": "GB",
      "toCity": "AMS",
      "toCountry": "NL",
      "isDirect": null,
      "scheduleStart": null,
      "scheduleEnd": null,
      "updateDate": "20250408"
    },
    {
      "airlines": [
        "EC"
      ],
      "fromCity": "LON",
      "fromCountry": "GB",
      "toCity": "AMS",
      "toCountry": "NL",
      "isDirect": null,
      "scheduleStart": null,
      "scheduleEnd": null,
      "updateDate": "20250408"
    },
    {
      "airlines": [
        "DH"
      ],
      "fromCity": "LON",
      "fromCountry": "GB",
      "toCity": "AMS",
      "toCountry": "NL",
      "isDirect": null,
      "scheduleStart": null,
      "scheduleEnd": null,
      "updateDate": "20250402"
    },
    {
      "airlines": [
        "D8"
      ],
      "fromCity": "LON",
      "fromCountry": "GB",
      "toCity": "AMS",
      "toCountry": "NL",
      "isDirect": null,
      "scheduleStart": null,
      "scheduleEnd": null,
      "updateDate": "20250402"
    },
    {
      "airlines": [
        "LE"
      ],
      "fromCity": "LON",
      "fromCountry": "GB",
      "toCity": "AMS",
      "toCountry": "NL",
      "isDirect": null,
      "scheduleStart": null,
      "scheduleEnd": null,
      "updateDate": "20250402"
    },
    {
      "airlines": [
        "DY"
      ],
      "fromCity": "LON",
      "fromCountry": "GB",
      "toCity": "AMS",
      "toCountry": "NL",
      "isDirect": null,
      "scheduleStart": null,
      "scheduleEnd": null,
      "updateDate": "20250402"
    },
    {
      "airlines": [
        "6E"
      ],
      "fromCity": "LON",
      "fromCountry": "GB",
      "toCity": "AMS",
      "toCountry": "NL",
      "isDirect": null,
      "scheduleStart": null,
      "scheduleEnd": null,
      "updateDate": "20241210"
    },
    {
      "airlines": [
        "GQ"
      ],
      "fromCity": "LON",
      "fromCountry": "GB",
      "toCity": "AMS",
      "toCountry": "NL",
      "isDirect": null,
      "scheduleStart": null,
      "scheduleEnd": null,
      "updateDate": "20250217"
    }
  ],
  "status": 0,
  "msg": null
}
```
{% endtab %}
{% endtabs %}
