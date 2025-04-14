# Get Luggage

{% hint style="info" %}

In a booking process, please call the 'getLuggage' API to get precise baggage quotes after price verification via 'verify' or 'getOffer'.  

Steps:

1. API sequence
    - Search - Verify- getLuggage - Order - Pay
    - getOffer - getLuggage - Order - Pay
2. For exact baggage prices, request 'getLuggage'.
3. Pass 'offerId' in 'getLuggage' requests:
    - From 'verify': Use sessionId as offerId
    - From 'getOffer': Use its offerId directly.
4. 'getLuggage' returns all flight segments' baggage data, each identified by a unique productCode.
5. In the Order step, use the productCode to add specific baggage products to the ticket order.

{% endhint %}

### Endpoint {% debug uid="getLuggage_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/getLuggage.do](https://sandbox.atriptech.com/getLuggage.do)

## Request

{% tabs %}
{% tab title="Schema" %}

### **offerId**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the offer. offerId returned by getOffer. sessionId returned by verify can also be used.
- **Constraints:** Must be a valid UUID.  
- **Default:** None  
- **Example:** `"1499249e-4149-483b-824c-a4ff8e150a40"`

### **maxResponseTime**  
- **Type:** Integer  
- **Required:** No  
- **Description:** Maximum response time for the request in milliseconds. The API will return an accurate quotation within this time. If this time is exceeded, the system will directly return a rule - based quotation. 
- **Constraints:** Must be a positive integer.  
- **Default:** 15000  
- **Example:** `6000`

{% endtab %}

{% tab title="Samples" %}
```json
{ 

    "offerId": "1499249e-4149-483b-824c-a4ff8e150a40",  

    "maxResponseTime": 6000 

} 
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}

### **msg**
- **Type:** String  
- **Required:** Yes  
- **Description:** Information used to describe the result. Do not use this field to check the success or failure of the request. Only use the 'status' code for checking.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "Success"  

### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Status code of the API response.  
  - 0: Success  
  - 2: System error  
- **Constraints:** Must be a valid integer.  
- **Default:** None  
- **Example:** 0  

### **offerId**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Unique identifier for this search. It is required to identify which ancillary service the customer has selected when calling the order function for booking. Required to identify the ancillary service selected for booking.  
- **Constraints:** Must be a valid integer.  
- **Default:** None  
- **Example:** 123456  

### **currency**
- **Type:** String  
- **Required:** No  
- **Description:** The currency used for settlement transactions.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** "USD"  

### **inboundSegments**
- **Type:** Array  
- **Required:** No  
- **Description:** List of inbound flight segments.  
- **Constraints:** None  
- **Default:** None  
- **Example:** [{...}]  

### **outboundSegments**
- **Type:** Array  
- **Required:** No  
- **Description:** List of outbound flight segments.  
- **Constraints:** None  
- **Default:** None  
- **Example:** [{...}]  

### **segmentIndex**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Flight segment sequence, starting from 1. If round-trip, the sequences of inbound and outbound segments are calculated together.  
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** 1  

### **carrier**
- **Type:** String  
- **Required:** No  
- **Description:** Carrier code.  
- **Constraints:** Must be a valid IATA carrier code.  
- **Default:** None  
- **Example:** "AA"  

### **flightNumber**
- **Type:** String  
- **Required:** Yes  
- **Description:** Flight number.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "100"  

### **depAirport**
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA code of the departure airport.  
- **Constraints:** Must be a valid IATA code.  
- **Default:** None  
- **Example:** "JFK"  

### **depTime**
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure time in the format YYYYMMDDHHMM.  
- **Constraints:** Must be in the specified format.  
- **Default:** None  
- **Example:** "202503011100"  

### **arrAirport**
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA code of the arrival airport.  
- **Constraints:** Must be a valid IATA code.  
- **Default:** None  
- **Example:** "LAX"  

### **stopCities**
- **Type:** String  
- **Required:** No  
- **Description:** Stopover cities, separated by commas.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "ATL, DFW"  

### **cabinClass**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Classification number of the cabin class.  
- **Constraints:** Must be a valid integer.  
- **Default:** None  
- **Example:** 1  

### **seatCount**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Available seat number.  
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** 5  

### **aircraftCode**
- **Type:** String  
- **Required:** No  
- **Description:** Aircraft model code.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "B737"  

### **depTerminal**
- **Type:** String  
- **Required:** No  
- **Description:** Departure terminal information.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "T1"  

### **arrTerminal**
- **Type:** String  
- **Required:** No  
- **Description:** Arrival terminal information.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "T3"  

### **operatingCarrier**
- **Type:** String  
- **Required:** Yes  
- **Description:** Code of the actual operating airline.  
- **Constraints:** Must be a valid IATA carrier code.  
- **Default:** None  
- **Example:** "DL"  

### **operatingFlightNumber**
- **Type:** String  
- **Required:** No  
- **Description:** Actual operating flight number.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "456"  

### **ancillariesProductElements**
- **Type:** Array  
- **Required:** No  
- **Description:** List of ancillary services provided for this order.  
- **Constraints:** None  
- **Default:** None  
- **Example:** [{...}]  

### **productCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier of the ancillary service.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "BAG01"  

### **productName**
- **Type:** String  
- **Required:** Yes  
- **Description:** Name of the ancillary service.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "Extra Baggage"  

### **productType**
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of ancillary service.  
- **Constraints:** 1: Standard Check-in baggage, 3: Cabin Baggage Overhead Locker.  
- **Default:** None  
- **Example:** "1"  

### **canPurchaseWithTicket**
- **Type:** Boolean  
- **Required:** Yes
- **Description:** Indicates if the ancillary can be purchased with the ticket.  
- **Constraints:** True or False  
- **Default:** None  
- **Example:** true  

### **canPurchasePostTicket**
- **Type:** Boolean  
- **Required:** Yes  
- **Description:** Indicates if the ancillary can be purchased after the ticket is issued.  
- **Constraints:** True or False  
- **Default:** None  
- **Example:** false  

### **price**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Price of the ancillary service.  
- **Constraints:** Must be a positive number.  
- **Default:** None  
- **Example:** 50.00  

### **vendorPrice**
- **Type:** Number  
- **Required:** No  
- **Description:** Price charged by the vendor.  
- **Constraints:** Must be a positive number.  
- **Default:** None  
- **Example:** 45.00  

### **vendorCurrency**
- **Type:** String  
- **Required:** No  
- **Description:** Currency used by the vendor for pricing.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** "USD"  

### **maxQty**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Maximum quantity allowed for purchase.  
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** 3  

### **minQty**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Minimum quantity required for purchase.  
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** 1  

### **categoryCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Code representing the category of the ancillary service.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "BAGGAGE"  

### **auxBaggageElement**
- **Type:** Object  
- **Required:** No  
- **Description:** Contains the following parameters: 
  - piece: Maximum number of pieces limit (0 means no limit) 
  - weight: Maximum weight, should be greater than 0 
  - isAllWeight: Whether the weight applies to all pieces or each piece 
  - size: Maximum size 
  - maxQty: Maximum purchase quantity for each product 
  - minQty: Starting purchase quantity for each product 
- **Constraints:** None  
- **Default:** None  
- **Example:** "23kg allowance"  

### **ancillaryCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique code for identifying the ancillary service.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "ANC123"  

### **displayCurrency**
- **Type:** String  
- **Required:** No  
- **Description:** Display currency, corresponding with it you request in verify or getOffer.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** "EUR"  

### **displayPrice**
- **Type:** Number  
- **Required:** No  
- **Description:** Price in the display currency.  
- **Constraints:** Must be a positive number.  
- **Default:** None  
- **Example:** 150.00

{% endtab %}

{% tab title="Samples" %}
```json
{
  "status": 0,
  "msg": "success",
  "offerId": "90223f62-fd87-45b4-9a32-68f03f9f85c8",
  "currency": "USD",
  "inboundSegments": [
    {
      "segmentIndex": 1,
      "carrier": "5F",
      "flightNumber": "5F617",
      "depAirport": "RMO",
      "depTime": "202408200810",
      "arrAirport": "LTN",
      "arrTime": "202408200940",
      "stopCities": "",
      "duration": 210,
      "codeShare": false,
      "cabin": "",
      "cabinClass": 1,
      "seatCount": 4,
      "aircraftCode": "",
      "depTerminal": "",
      "arrTerminal": "",
      "operatingCarrier": "5F",
      "operatingFlightnumber": "",
      "fareFamily": "LOYAL"
    }
  ],
  "retSegments": [
    {
      "segmentIndex": 2,
      "carrier": "5F",
      "flightNumber": "5F618",
      "depAirport": "LTN",
      "depTime": "202408251040",
      "arrAirport": "RMO",
      "arrTime": "202408251550",
      "stopCities": "",
      "duration": 190,
      "codeShare": false,
      "cabin": "",
      "cabinClass": 1,
      "seatCount": 4,
      "aircraftCode": "",
      "depTerminal": "",
      "arrTerminal": "",
      "operatingCarrier": "5F",
      "operatingFlightnumber": "",
      "fareFamily": "LOYAL"
    }
  ],
  "ancillaryProductElements": [
    {
      "segmentIndex": 1,
      "productCode": "SCI_BAG_1PC_10KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 22.88,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 1,
        "weight": 10,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_1PC_10KG",
      "auxSeatElement": null,
      "displayPrice": 165.89,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 1,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_1PC_20KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 46.2,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 1,
        "weight": 20,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_1PC_20KG",
      "auxSeatElement": null,
      "displayPrice": 335.08,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 1,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_1PC_30KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 34.54,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 1,
        "weight": 30,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_1PC_30KG",
      "auxSeatElement": null,
      "displayPrice": 250.48,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 1,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_2PC_20KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 74.58,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 2,
        "weight": 20,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_2PC_20KG",
      "auxSeatElement": null,
      "displayPrice": 540.86,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 1,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_2PC_40KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 49.81,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 2,
        "weight": 40,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_2PC_40KG",
      "auxSeatElement": null,
      "displayPrice": 361.21,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 1,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_2PC_60KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 124.11,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 2,
        "weight": 60,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_2PC_60KG",
      "auxSeatElement": null,
      "displayPrice": 900.09,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 1,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_3PC_30KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 105.16,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 3,
        "weight": 30,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_3PC_30KG",
      "auxSeatElement": null,
      "displayPrice": 762.7,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 1,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_3PC_60KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 132.01,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 3,
        "weight": 60,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_3PC_60KG",
      "auxSeatElement": null,
      "displayPrice": 957.38,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 1,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_3PC_90KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 184.19,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 3,
        "weight": 90,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_3PC_90KG",
      "auxSeatElement": null,
      "displayPrice": 1335.9,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 1,
      "endSegmentIndex": null,
      "productCode": "COL_BAG_1PC_10KG",
      "productName": "Cabin Baggage Overhead Lock",
      "productType": 3,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 22.71,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 1,
        "weight": 10,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "CabinBaggageOverheadLocker",
      "ancillaryCode": "COL_BAG_1PC_10KG",
      "auxSeatElement": null,
      "displayPrice": 164.71,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 2,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_1PC_10KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 43.48,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 1,
        "weight": 10,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_1PC_10KG",
      "auxSeatElement": null,
      "displayPrice": 315.33,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 2,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_1PC_20KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 39.93,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 1,
        "weight": 20,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_1PC_20KG",
      "auxSeatElement": null,
      "displayPrice": 289.59,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 2,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_1PC_30KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 44.09,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 1,
        "weight": 30,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_1PC_30KG",
      "auxSeatElement": null,
      "displayPrice": 319.73,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 2,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_2PC_20KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 89.28,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 2,
        "weight": 20,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_2PC_20KG",
      "auxSeatElement": null,
      "displayPrice": 647.49,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 2,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_2PC_40KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 81.05,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 2,
        "weight": 40,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_2PC_40KG",
      "auxSeatElement": null,
      "displayPrice": 587.84,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 2,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_2PC_60KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 141.74,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 2,
        "weight": 60,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_2PC_60KG",
      "auxSeatElement": null,
      "displayPrice": 1027.97,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 2,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_3PC_30KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 138.97,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 3,
        "weight": 30,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_3PC_30KG",
      "auxSeatElement": null,
      "displayPrice": 1007.9,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 2,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_3PC_60KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 98.49,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 3,
        "weight": 60,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_3PC_60KG",
      "auxSeatElement": null,
      "displayPrice": 714.3,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 2,
      "endSegmentIndex": null,
      "productCode": "SCI_BAG_3PC_90KG",
      "productName": "Standard Check-in Baggage",
      "productType": 1,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 272.31,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 3,
        "weight": 90,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "StandardCheckInBaggage",
      "ancillaryCode": "SCI_BAG_3PC_90KG",
      "auxSeatElement": null,
      "displayPrice": 1974.96,
      "displayCurrency": "CNY"
    },
    {
      "segmentIndex": 2,
      "endSegmentIndex": null,
      "productCode": "COL_BAG_1PC_10KG",
      "productName": "Cabin Baggage Overhead Lock",
      "productType": 3,
      "canPurchaseWithTicket": 1,
      "canPurchasePostTicket": 0,
      "price": 22.04,
      "currency": "USD",
      "vendorPrice": null,
      "vendorCurrency": null,
      "clientTechnicalServiceFee": 0,
      "clientTechnicalServiceFeeMode": "PER_PAX",
      "auxBaggageElement": {
        "piece": 1,
        "weight": 10,
        "isAllWeight": true,
        "size": ""
      },
      "offerId": null,
      "maxQty": 1,
      "minQty": 1,
      "categoryCode": "CabinBaggageOverheadLocker",
      "ancillaryCode": "COL_BAG_1PC_10KG",
      "auxSeatElement": null,
      "displayPrice": 159.83,
      "displayCurrency": "CNY"
    }
  ]
}
```
{% endtab %}
{% endtabs %}  


