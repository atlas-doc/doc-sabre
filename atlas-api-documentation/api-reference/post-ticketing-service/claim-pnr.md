# PNR Claim

### Dependency

No preceding function needs to be carried out.

### Endpoint {% debug uid="PNRClaim_1.0" %}{% enddebug %}
    
[https://sandbox.atriptech.com/pnr/claim.do](https://sandbox.atriptech.com/pnr/claim.do)

## Request

{% tabs %}
{% tab title="Schema" %}

#### **mmb.airlinePnr**
- **Type:** String  
- **Required:** Yes  
- **Description:** Airline's Passenger Name Record (PNR) code.  
- **Default:** None  
- **Example:** `"S1BE6Z"`  

#### **mmb.email**
- **Type:** String  
- **Required:** Yes  
- **Description:** Email address associated with the booking. This is the contact email in the booking. 
- **Default:** None  
- **Example:** `"TESTABC22Oct@pnrclaim.com"`  

### **passengers[]**

#### **passengers[].name**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's full name in the format LASTNAME/FIRSTNAME MiddleName.  
- **Default:** None  
- **Example:** `"test/abc"`  

#### **passengers[].passengerType**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Passenger type indicator.  

  Valid values:
  - `0` = Adult  
  - `1` = Child  
  - `2` = Infant  
- **Default:** None  
- **Example:** `0`  

#### **passengers[].birthday**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's date of birth. Format: `YYYYMMDD` . 
- **Default:** None  
- **Example:** `"20001010"`  

#### **passengers[].gender**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's gender.  

  Valid values:
  - `M`: Male
  - `F`: Female  
- **Default:** None  
- **Example:** `"M"`  

#### **passengers[].cardNum**
- **Type:** String  
- **Required:** No  
- **Description:** Document number (passport or ID).  
- **Default:** `""`  
- **Example:** `""`  

#### **passengers[].cardType**
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of identification document.  

  Valid values:
  - `"PP"` = Passport  
  - `"ID"` = National ID  
- **Default:** None  
- **Example:** `"PP"`  

#### **passengers[].cardIssuePlace**
- **Type:** String  
- **Required:** No  
- **Description:** Country or authority that issued the document.  
- **Default:** `""`  
- **Example:** `""`  

#### **passengers[].cardExpired**
- **Type:** String  
- **Required:** No  
- **Description:** Expiry date of the document. Format: `YYYYMMDD`   
- **Default:** None  
- **Example:** `"20241010"`  

#### **passengers[].nationality**
- **Type:** String  
- **Required:** No  
- **Description:** Passenger's nationality.  
- **Default:** `""`  
- **Example:** `""`  

### **fromSegments[]**

#### **fromSegments[].carrier**
- **Type:** String  
- **Required:** Yes  
- **Description:** Airline carrier code.  
- **Default:** None  
- **Example:** `"AK"`  

#### **fromSegments[].flightNumber**
- **Type:** String  
- **Required:** Yes  
- **Description:** Flight number.  
- **Default:** None  
- **Example:** `"AK128"`  

#### **fromSegments[].depAirport**
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure airport code (IATA).  
- **Default:** None  
- **Example:** `"DEL"`  

#### **fromSegments[].arrAirport**
- **Type:** String  
- **Required:** Yes  
- **Description:** Arrival airport code (IATA).  
- **Default:** None  
- **Example:** `"BOM"`  

#### **fromSegments[].depTime**
- **Type:** String  
- **Required:** Yes  
- **Description:** Scheduled departure time. Format `YYYYMMDDHHmm`. 202203100300 means 10MAR2022 03:00 A.M.  
- **Default:** None  
- **Example:** `"202411201600"`  

#### **fromSegments[].arrTime**
- **Type:** String  
- **Required:** Yes  
- **Description:** Scheduled arrival time. Format `YYYYMMDDHHmm`. 202203100300 means 10MAR2022 03:00 A.M.  
- **Default:** None  
- **Example:** `"202411201820"`  

#### **fromSegments[].stopCities**
- **Type:** String  
- **Required:** No  
- **Description:** Comma-separated stopover cities, if any. Name of cities from where the passengers will take connecting flights. Include IATA code of cities and use a comma in case of multiple cities to separate if transfer airports count is higher than 1. For example: CGK, SUB. Blank means non-stop flight.
- **Default:** `""`  
- **Example:** `""`  

#### **fromSegments[].codeShare**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Indicates if this is a codeshare flight.  

  Valid values:
  - `0` = No  
  - `1` = Yes  
- **Default:** `0`  
- **Example:** `0`  

#### **fromSegments[].operatingCarrier**
- **Type:** String  
- **Required:** No  
- **Description:** Operating airline carrier for codeshare flights. It is blank when codeshare=false  
- **Default:** `""`  
- **Example:** `""`  

#### **fromSegments[].operatingFlightNumber**
- **Type:** String  
- **Required:** No  
- **Description:** Operating carrier's flight number. It is blank when codeshare=false  
- **Default:** `""`  
- **Example:** `""`  

#### **fromSegments[].depTerminal**
- **Type:** String  
- **Required:** No  
- **Description:** Departure terminal.  
- **Default:** `""`  
- **Example:** `"T2"`  

#### **fromSegments[].arrTerminal**
- **Type:** String  
- **Required:** No  
- **Description:** Arrival terminal.  
- **Default:** `""`  
- **Example:** `"T1"`  

#### **fromSegments[].cabinClass**
- **Type:** String  
- **Required:** Yes  
- **Description:** Cabin class code (e.g., Economy, Business). Service grade of the fare.

  Valid values:
  - 1: Economy
  - 2: Business
  - 3: First Class
  - 4: Premium Economy  
- **Default:** None  
- **Example:** `"1"`  

#### **fromSegments[].fareFamily**
- **Type:** String  
- **Required:** No  
- **Description:** Fare family name associated with the ticket.  
- **Default:** `""`  
- **Example:** `"Flexi"`  

#### **fromSegments[].flightIndex**
- **Type:** Integer / Null  
- **Required:** No  
- **Description:** Index of the flight in multi-leg itineraries.  
- **Default:** `null`  
- **Example:** `null`  

#### **fromSegments[].duration**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Duration of the flight in minutes.  
- **Default:** None  
- **Example:** `140`  

#### **retSegments**
- **Type:** Null or Array  
- **Required:** No  
- **Description:** Return flight segments (if round-trip). All the elements are the same as the "fromSegments" information.  
- **Default:** `null`  
- **Example:** `null`  

{% endtab %}

{% tab title="Samples" %}
```json
{
  "mmb": {
    "airlinePnr": "S1BE6Z",
    "email": "TESTABC22Oct@pnrclaim.com"
  },
  "passengers": [
    {
      "name": "test/abc",
      "passengerType": 0,
      "birthday": "20001010",
      "gender": "M",
      "cardNum": "",
      "cardType": "PP",
      "cardIssuePlace": "",
      "cardExpired": "20241010",
      "nationality": ""
    }
  ],
  "fromSegments": [
    {
      "carrier": "AK",
      "flightNumber": "AK128",
      "depAirport": "DEL",
      "arrAirport": "BOM",
      "depTime": "202411201600",
      "arrTime": "202411201820",
      "stopCities": "",
      "codeShare": 0,
      "operatingCarrier": "",
      "operatingFlightNumber": "",
      "depTerminal": "T2",
      "arrTerminal": "T1",
      "cabinClass": "1",
      "fareFamily": "Flexi",
      "flightIndex": null,
      "duration": 140
    }
  ],
  "retSegments": null
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
#### **orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique order number generated after successful booking.  
- **Default:** None  
- **Example:** `"TESTC20241022100111040"`  

#### **pnrCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Atlas PNR.  
- **Default:** None  
- **Example:** `"RCOFMU"`  

### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Response status code.  

  Valid values:
  - 0: success
  - 2: system error
- **Default:** 0  
- **Example:** 0  

### **msg**
- **Type:** String  
- **Required:** No  
- **Description:** Error message. The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.  
- **Default:** null  
- **Example:** null

{% endtab %}

{% tab title="Samples" %}
```json
{
    "orderNo": "TESTC20241022100111040",
    "pnrCode": "RCOFMU",
    "status": 0,
    "msg": null
}
```
{% endtab %}
{% endtabs %}
