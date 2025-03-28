---
description: Create an order request to search for flights.
---

# Search

### Dependency

No preceding function needs to be called before `Search`.

### Endpoint {% debug uid="search_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/search.do](https://sandbox.atriptech.com/search.do)

{% hint style="info" %}
**The search results will include a lot of items. Some highlights are:**

* The returned currency is by configuration according to the business agreement between you and Atlas.
* The total cost to purchase for a single adult passenger is: `adultPrice` + `adultTax` + `transactionFeePerPax`
* For the airlines which support pass through payment method, we would set `supportCreditTransPayment` to `1` and present the vendor's fare in the `vendorFare` element. Alternatively, if the airline doesn't support pass through payment method, we would set `supportCreditTransPayment` to `0` and the `vendorFare` element will be `null`.
* You can choose to show or hide `ancillaryProductElements` in search response, according to the configuration of each client in the backend system.
* The 'links' element will have the link to the terms and conditions of the airlines.
* Display Currency is only to be used for display purposes. The amount in the response is not to be used for fare comparison or accounting purposes. The display currency conversion will be available in fares, taxes and ancillary baggage sections of the search and verify response. When the "vendorFare" element is available, the conversion will be from the vendor fare. In the absence of the "vendorFare" element, the conversion would be from the transacted fare.
{% endhint %}

### Request

{% tabs %}
{% tab title="Schema" %}

### **tripType**
- **Type:** String  
- **Required:** Yes  
- **Description:** Indicates the type of trip.  
- **Constraints:** "1" for one-way, "2" for round-trip.  
- **Default:** None  
- **Example:** "2"  

### **adultNum**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of adult passengers.  
- **Constraints:** Must be 1 or greater.  
- **Default:** None  
- **Example:** 1  

### **childNum**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of child passengers.  
- **Constraints:** Cannot be negative.  
- **Default:** 0  
- **Example:** 0  

### **infantNum**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of infant passengers.  
- **Constraints:** Cannot be negative.  
- **Default:** 0  
- **Example:** 0  

### **fromCity**
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure city IATA code.  
- **Constraints:** Must be a valid IATA airport code.  
- **Default:** None  
- **Example:** "KRK"  

### **toCity**
- **Type:** String  
- **Required:** Yes  
- **Description:** Arrival city IATA code.  
- **Constraints:** Must be a valid IATA airport code.  
- **Default:** None  
- **Example:** "LTN"  

### **fromDate**
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure date in YYYYMMDD format.  
- **Constraints:** Must be a valid date.  
- **Default:** None  
- **Example:** "20240326"  

### **retDate**
- **Type:** String  
- **Required:** Yes (if round-trip)  
- **Description:** Return date in YYYYMMDD format.  
- **Constraints:** Required if tripType is "2" (round-trip).  
- **Default:** None  
- **Example:** "20240423"  

### **airlines**
- **Type:** Array of Strings  
- **Required:** No  
- **Description:** List of airline codes to include in the search.  
- **Constraints:** Must be valid IATA airline codes.  
- **Default:** None  
- **Example:** ["FR", "W6", "F9"]  

### **fromFlightNumbers**
- **Type:** Array of Strings  
- **Required:** No  
- **Description:** List of preferred departure flight numbers.  
- **Constraints:** None  
- **Default:** None  
- **Example:** ["FR123", "FR456"]  

### **retFlightNumbers**
- **Type:** Array of Strings  
- **Required:** No  
- **Description:** List of preferred return flight numbers.  
- **Constraints:** None  
- **Default:** None  
- **Example:** ["FR123", "FR456"]  

### **includeMultipleFareFamily**
- **Type:** Boolean  
- **Required:** No  
- **Description:** Indicates if multiple fare families should be included in the search.  
- **Constraints:** true or false  
- **Default:** false  
- **Example:** true  

### **currency**
- **Type:** String  
- **Required:** No  
- **Description:** Currency in which pricing should be calculated.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** "GBP"  

### **displayCurrency**
- **Type:** String  
- **Required:** No  
- **Description:** Currency to be displayed in results.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** "PHP"  

### **requestSource**
- **Type:** String  
- **Required:** No  
- **Description:** Source of the request.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "Organic"  

{% endtab %}

{% tab title="Samples" %}
```
{
  "tripType": "2",
  "adultNum": 1,
  "childNum": 0,
  "infantNum": 0,
  "fromCity": "KRK",
  "toCity": "LTN",
  "fromDate": "20240326",
  "retDate": "20240423",
  "airlines": [
    "FR",
    "W6",
    "F9"
  ],
  "fromFlightNumbers": [
    "FR123",
    "FR456"
  ],
  "retFlightNumbers": [
    "FR123",
    "FR456"
  ],
  "includeMultipleFareFamily": true,
  "currency": "GBP",
  "displayCurrency": "PHP",
  "requestSource": "Organic"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}

### **routings**
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of available flight options.  
- **Constraints:** Must contain at least one routing option.  
- **Default:** None  
- **Example:** [{...}]  

#### **routings.fid**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the flight.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "2ex3fC8fhO9-tp5yRHzmmfaFZTmKk-AmiileVzjrMn03uznhGSbRVdhdb239v6gV"  

#### **routings.routingIdentifier**
- **Type:** String  
- **Required:** Yes  
- **Description:** Identifier for the routing.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "TEFYX0xBU18xXzIwMjUwNDE5X18xXzBfMHx0dHh6cDYyNDA1fDF8NDAuOThfNDAuOThfMTAuMDBfMC42NV85Mi42MV9VU0R8TEFYX0xBU18xXzIwMjUwNDE5X18xXzBfMF5PTlQtRjk0MjA2LS1MQVMtMjAyNTA0MTkyMjAyLTIwMjUwNDE5MjMxMy1CYXNpYyBGYXJlLTEtXjQwLjk4XzQwLjk4XzEwLjAwXzAuNjVfOTIuNjFeQUY5X0FGOV5eQUY5MUxBWExBUzIwMDIwMjUwNDE5XlVTRF40MC45OF40MC45OF4xMC4wMHwxfDIwMjUwMzIwMTkwMjMyfDB8MTc0MjQ2ODU1MjIzMGt0Q2hxfHx8fHwwLjY1fDJ8MHxVU0Q=.nE15gqdNlu6fdhXI0uiKGp1JfLfNw0zWSSGNxIkY7gQ="  

#### **routings.supportCreditTransPayment**
- **Type:** String  
- **Required:** No  
- **Description:** Indicates if VCC payment is supported.  
- **Constraints:**

    0: The credit card details will not be passed through and only pre-payment is allowed.

    1: The API will allow you to pass through client’s credit card details for payment. The customer can also use pre-payment as a method of payment. 
- **Default:** "0"  
- **Example:** "1"  

#### **routings.supportPaymentMethods**
- **Type:** Array  
- **Required:** No  
- **Description:** List of supported payment method identifiers. 1: Deposit 3: VCC Passthrough  5: MOR 
- **Constraints:** Must be a valid list of numeric payment method identifiers.  
- **Default:** None  
- **Example:** [1, 5, 3]  

#### **routings.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency code for the flight pricing. This is the currency in which Atlas settles transactions with you. 
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** "USD"  

#### **routings.adultPrice**
- **Type:** Number  
- **Required:** Yes  
- **Description:** The base fare price for an adult passenger.  
- **Constraints:** Must be a positive number.  
- **Default:** None  
- **Example:** 96.03  

#### **routings.adultTax**
- **Type:** Number  
- **Required:** Yes  
- **Description:** The tax amount applicable to an adult ticket.  
- **Constraints:** Must be a positive number or zero.  
- **Default:** None  
- **Example:** 0.18  

#### **routings.adultDetails**
- **Type:** Array  
- **Required:** Yes  
- **Description:** Breakdown of adult fare and tax details.  
- **Constraints:** Must contain objects with valid pricing details.  
- **Default:** None  
- **Example:**  
  ```json
  [
    {"code": "farePrice", "type": "base", "amount": 96.03, "description": ""},
    {"code": "tax", "type": "tax", "amount": 0.18, "description": ""}
  ]
  ```

#### **routings.childPrice**
- **Type:** Number  
- **Required:** Yes  
- **Description:** The base fare price for a child passenger.  
- **Constraints:** Must be a positive number.  
- **Default:** None  
- **Example:** 96.03  

#### **routings.childTax**
- **Type:** Number  
- **Required:** Yes  
- **Description:** The tax amount applicable to a child ticket.  
- **Constraints:** Must be a positive number or zero.  
- **Default:** None  
- **Example:** 0.18  

#### **routings.childDetails**
- **Type:** Array  
- **Required:** Yes  
- **Description:** Breakdown of child fare and tax details.  
- **Constraints:** Must contain objects with valid pricing details.  
- **Default:** None  
- **Example:**  
  ```json
  [
    {"code": "farePrice", "type": "base", "amount": 96.03, "description": ""},
    {"code": "tax", "type": "tax", "amount": 0.18, "description": ""}
  ]
  ```

#### **routings.infantPrice**
- **Type:** Number  
- **Required:** Yes  
- **Description:** The base fare price for an infant passenger.  
- **Constraints:** Must be a positive number.  
- **Default:** None  
- **Example:** 51.04  

#### **routings.infantTax**
- **Type:** Number  
- **Required:** Yes  
- **Description:** The tax amount applicable to an infant ticket.  
- **Constraints:** Must be a positive number or zero.  
- **Default:** None  
- **Example:** 0  

#### **routings.infantDetails**
- **Type:** Array  
- **Required:** Yes  
- **Description:** Breakdown of infant fare and tax details.  
- **Constraints:** Must contain objects with valid pricing details.  
- **Default:** None  
- **Example:**  
  ```json
  [
    {"code": "farePrice", "type": "base", "amount": 51.04, "description": ""},
    {"code": "tax", "type": "tax", "amount": 0, "description": ""}
  ]
  ```

#### **routings.adultDetails**
- **Type:** Array  
- **Required:** Yes  
- **Description:** A summary of all fare breakdowns, including adults, children, and infants.  
- **Constraints:** Must contain at least one valid pricing object.  
- **Default:** None  
- **Example:**  
  ```json
  [
    {"category": "Adult", "price": 96.03, "tax": 0.18},
    {"category": "Child", "price": 96.03, "tax": 0.18},
    {"category": "Infant", "price": 51.04, "tax": 0}
  ]
  ```

#### **routings.infantAllowed**
- **Type:** Boolean  
- **Required:** No  
- **Description:** Indicates if infants are allowed.  
- **Constraints:** True or False  
- **Default:** True  
- **Example:** true  

#### **routings.transactionFeePerPax**
- **Type:** Float  
- **Required:** No  
- **Description:** Technical service fee per passenger as per the signed contract.  
- **Constraints:** Must be a positive number.  
- **Default:** 0.0  
- **Example:** 0.65  

#### **routings.transactionFee**
- **Type:** Float  
- **Required:** No  
- **Description:** Technical service fee as per "transactionFeeMode". 
- **Constraints:** Must be a positive number.  
- **Default:** 0.0  
- **Example:** 0.65  

#### **routings.transactionFeeMode**
- **Type:** String  
- **Required:** No  
- **Description:** Defines how transaction fees are applied.  
- **Constraints:**

  The criteria of calculating the transaction fee as per the contractual agreement.

  Transaction Fee Mode values:

  PER_SEGMENT: Each segment of an itinerary (per passenger)

  PER_TICKET: No. of tickets in a booking

  PER_PAX: Per passenger

  PER_BOOKING: Per atlas booking (order #)  
- **Default:** None  
- **Example:** "PER_TICKET"  

#### **routings.nationalityType**
- **Type:** Integer  
- **Required:** No  
- **Description:** Defines whether nationality is required.  
- **Constraints:**

Nationality limitation values

0 No Limitation (optional)

1 Allowed (required)

2 Forbidden (not to be entered)
- **Default:** 0  
- **Example:** 0  

#### **routings.nationality**
- **Type:** String  
- **Required:** No  
- **Description:** Passenger nationality.  
- **Constraints:** This is the nationality of the passenger. Pass the IATA country code and use a comma if there is more than one country. 
- **Default:** ""  
- **Example:** "US"  

#### **routings.suitAge**
- **Type:** String  
- **Required:** No  
- **Description:** Deprecated Field. Ignore it.  
- **Constraints:** None  
- **Default:** ""  
- **Example:** ""  

#### **routings.PaxType**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger type for booking.  
- **Constraints:** Example values: "ADT", "CHD", "INF"  
- **Default:** "ADT"  
- **Example:** "ADT"  


## **fromSegments**
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of segments for outbound flights.  
- **Constraints:** Must contain at least one segment.  
- **Default:** None  
- **Example:** [{...}]

### **fromSegments.segmentIndex**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Segment sequence. Starts from 1. If it is return trip, sequence for outbound trip and inbound trip would be together.  
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** 1  

### **fromSegments.carrier**
- **Type:** String  
- **Required:** Yes  
- **Description:** Airline carrier code.  
- **Constraints:** Must be a valid IATA airline code.  
- **Default:** None  
- **Example:** "F9"  

### **fromSegments.flightNumber**
- **Type:** String  
- **Required:** Yes  
- **Description:** Flight number for the segment.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "F92232"  

### **fromSegments.depAirport**
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure airport IATA code.  
- **Constraints:** Must be a valid IATA code.  
- **Default:** None  
- **Example:** "ONT"  

### **fromSegments.depTime**
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure time in YYYYMMDDHHMM format.  
- **Constraints:** Must follow the format YYYYMMDDHHMM.  
- **Default:** None  
- **Example:** "202504101502"  

### **fromSegments.arrAirport**
- **Type:** String  
- **Required:** Yes  
- **Description:** Arrival airport IATA code.  
- **Constraints:** Must be a valid IATA code.  
- **Default:** None  
- **Example:** "LAS"  

### **fromSegments.arrTime**
- **Type:** String  
- **Required:** Yes  
- **Description:** Arrival time in YYYYMMDDHHMM format.  
- **Constraints:** Must follow the format YYYYMMDDHHMM.  
- **Default:** None  
- **Example:** "202504101615"  

### **fromSegments.stopCities**
- **Type:** String  
- **Required:** No  
- **Description:** Stopover cities (if applicable). Name of cities from where the passengers will take connecting flights. Include IATA code of cities and use a comma in case of multiple cities to separate transfer airports count is higher than 1. Blank means non-stop flight.
- **Constraints:** None  
- **Default:** ""  
- **Example:** "SUB"  

### **fromSegments.duration**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Duration of the flight segment in minutes.  
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** 73  

### **fromSegments.codeShare**
- **Type:** Boolean  
- **Required:** No  
- **Description:** Indicates if the flight is codeshared.  
- **Constraints:** True or False  

  True : code share

  False : Not code share
- **Default:** false  
- **Example:** false  

### **fromSegments.cabin**
- **Type:** String  
- **Required:** No  
- **Description:** Booking code for the fare. For the LCCs which do not provide cabin options, the cabin string will be blank.
- **Constraints:** None  
- **Default:** ""  
- **Example:** "Y"  

### **fromSegments.cabinClass**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Service grade of the fare.
- **Constraints:** Must be a positive integer. 

  Valid values:

  1 : Economy

  2 : Business

  3 : First Class

  4: Premium Economy 
- **Default:** None  
- **Example:** 1  

### **fromSegments.seatCount**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Available seat count.  
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** 4  

### **fromSegments.aircraftCode**
- **Type:** String  
- **Required:** No  
- **Description:** This value identifies the aircraft model, which is the IATA aircraft code. For example, Airbus A380 = 388, Airbus A350 = 351.
- **Constraints:** None  
- **Default:** ""  
- **Example:** "388"  

### **fromSegments.depTerminal**
- **Type:** String  
- **Required:** No  
- **Description:** Departure terminal information.  
- **Constraints:** None  
- **Default:** ""  
- **Example:** "T1"  

### **fromSegments.arrTerminal**
- **Type:** String  
- **Required:** No  
- **Description:** Arrival terminal information.  
- **Constraints:** None  
- **Default:** ""  
- **Example:** "T3"  

### **fromSegments.operatingCarrier**
- **Type:** String  
- **Required:** Yes  
- **Description:** Operating airline carrier code. 
- **Constraints:** Must be a valid IATA airline code.  
- **Default:** None  
- **Example:** "F9"  

### **fromSegments.operatingFlightnumber**
- **Type:** String  
- **Required:** No  
- **Description:** Operating airline flight number.  
- **Constraints:** None  
- **Default:** ""  
- **Example:** ""  

### **fromSegments.fareFamily**
- **Type:** String  
- **Required:** No  
- **Description:** Fare Family as per the information received from the airline.
- **Constraints:** None  
- **Default:** "Basic Fare"  
- **Example:** "Basic Fare"  

## **retSegments**
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of segments for return flights.  
- **Constraints:** Must contain at least one segment.  
- **Default:** None  
- **Example:** [{...}]

## **rule**
- **Type:** Object  
- **Required:** Yes  
- **Description:** Contains baggage-related information and policies.  
- **Constraints:** None  
- **Default:** None  
- **Example:** {...}

### **rule.hasBaggage**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Indicates if free checked-in or cabin baggage is included.  
- **Constraints:** 1 for included, 0 for not included.  
- **Default:** 1  
- **Example:** 1  

### **rule.baggageElements**
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of free baggage allowances and restrictions per segment.  
- **Constraints:** Must contain at least one baggage element.  
- **Default:** None  
- **Example:** [{...}]

#### **rule.baggageElements.segmentNo**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Segment number to which the baggage applies. Segment sequence, start from 1. If it is roundtrip, sequence outbound and inbound will be together. 
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** 1  

#### **rule.baggageElements.baggageType**
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of baggage allowed.  

There are 4 options for baggage:

StandardCheckInBaggage: Standard Check-in Baggage.

CabinBaggage: Usually refers to the Cabin Baggage Overhead Locker. Transition value. It will gradually transition to CabinBaggageOverheadLocker.

CabinBaggageOverheadLocker: Cabin Baggage Overhead Locker.

CabinBaggageUnderSeat: Cabin Baggage Under Seat. Usually refers to the personal item.
- **Constraints:** Accepts predefined baggage types (e.g., "CabinBaggageUnderSeat", "StandardCheckInBaggage").  
- **Default:** None  
- **Example:** "CabinBaggageUnderSeat"  

#### **rule.baggageElements.passengerType**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Passenger type for baggage allowance.  
- **Constraints:** 0 for ADT, 1 for CHD and 2 for INF.
- **Default:** 0  
- **Example:** 0  

#### **rule.baggageElements.baggagePiece**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of baggage pieces allowed.  

  0: No limitation on the number of pieces

  higher than 0: Maximum pieces
- **Constraints:** Must be a non-negative integer.  
- **Default:** 1  
- **Example:** 1  

#### **rule.baggageElements.baggageWeight**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Weight of the baggage in kilograms.  
  0: No free baggage

  -1: No limitation on weight.
- **Constraints:** -1 indicates no weight limit, positive values indicate a weight restriction.  
- **Default:** -1  
- **Example:** -1  

#### **rule.baggageElements.baggageSize**
- **Type:** String  
- **Required:** No  
- **Description:** Dimensions of the baggage allowed.  
- **Constraints:** Format should be L*W*H (e.g., 45*35*20cm). Empty means no limitations. 
- **Default:** ""  
- **Example:** "45*35*20cm"  



## **refundRules**
- **Type:** Array  
- **Required:** Yes  
- **Description:** Refund policy details associated with the flight booking. This function is used to fetch the refund rules of the selected airline. There is only one array for one way, and two arrays for round-trip. The first array is for the outbound, and the second array is for the inbound. 
- **Constraints:** None.  
- **Default:** None  
- **Example:** [{...}]

### **refundRules.refundType**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Type of refund allowed.  
- **Constraints:** 

0: Wholly unused ticket

1: Partially used ticket (For example, when the passenger has used an outbound flight and wants to refund an inbound flight.)
- **Default:** 0  
- **Example:** 0  

### **refundRules.refundStatus**
- **Type:** String  
- **Required:** Yes  
- **Description:** Refund eligibility status.  
- **Constraints:** "T" for refundable, "F" for non-refundable, "H" for refundable with restrictions
- **Default:** "T"  
- **Example:** "T"  

### **refundRules.refundFee**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Fee applied for processing the refund (for the most restrictive condition).

If refundStatus = H, it should not be null

If refundStatus = T/F, it can be null  
- **Constraints:** Must be a non-negative value.  
- **Default:** 0.0  
- **Example:** 0.0  

### **refundRules.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** The currency of airline's rule, if refundStatus = H, it should not be "null".
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** "USD"  
- **Example:** "USD"  

### **refundRules.refNoshow**
- **Type:** String  
- **Required:** Yes  
- **Description:** Indicates if a no-show affects refunds (for the most restrictive condition).

T: Non refundable

H: Refundable with restrictions

F: Free for refund  
- **Constraints:** "T" for non-refundable, "F" for free for refund, "H" for refundable with restrictions.  
- **Default:** "T"  
- **Example:** "T"  

### **refundRules.refNoShowCondition**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Time before scheduled flight departure.  
- **Constraints:** Must be a valid predefined condition code.  
- **Default:** 0  
- **Example:** 0  

### **refundRules.refNoshowFee**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Total refund fee (for the most restrictive condition):

If refNoshow = H, it should not be "null".

This value includes the refund fee and no-show penalty
- **Constraints:** Must be a non-negative value.  
- **Default:** 0.0  
- **Example:** 0.0  

### **refundRules.ruleDetailList**
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of all rules. Inside the ruleList are detailed airline rules for time periods, while outside the ruleList are the strictest rules before and after Noshow.
- **Constraints:** None.  
- **Default:** None  
- **Example:** [{...}]

#### **refundRules.ruleDetailList.ruleId**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Unique identifier for the refund rule.  
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** 36608  

#### **refundRules.ruleDetailList.status**
- **Type:** String  
- **Required:** Yes  
- **Description:** Status of the refund rule.  

T: Non refundable

H: Refundable with restrictions

F: Free for refund  
- **Constraints:** "T" for non-refundable, "F" for free for refund, "H" for refundable with restrictions.  
- **Default:** "T"  
- **Example:** "T"  

#### **refundRules.ruleDetailList.startMinute**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Starting time of rule application. Positive numbers represent XXX minutes before departure. Negative numbers represent XXX minutes after departure. 
- **Constraints:** Can be negative (past flights) or positive (future flights).  
- **Default:** 0  
- **Example:** 0  

#### **refundRules.ruleDetailList.endMinute**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Ending time of rule application. Positive numbers represent XXX minutes before departure. Negative numbers represent XXX minutes after departure.
- **Constraints:** Negative values indicate rules valid in the past.  
- **Default:** -525600  
- **Example:** -525600  

#### **refundRules.ruleDetailList.amount**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Refund amount associated with the rule.  
- **Constraints:** Must be a non-negative value.  
- **Default:** 0.0  
- **Example:** 0.0  

#### **refundRules.ruleDetailList.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** The currency of airline's rule. If refundStatus = H, it should not be "null".
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** "USD"  
- **Example:** "USD"  

## **changesRules**
- **Type:** Array  
- **Required:** Yes  
- **Description:** Rules defining ticket changes, including fees and conditions. This function is used to fetch the change rules of the selected airline. There is only one array for one way, and two arrays for round-trip. The first array is for the outbound, and the second array is for the inbound.
- **Constraints:** None.  
- **Default:** None  
- **Example:** [{...}]

### **changesRules.changesType**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Type of flight change allowed.  
- **Constraints:** 

  0: Wholly unused ticket

  1: Partially used ticket (For example. When the passenger has used an outbound flight and wants to change an inbound flight)  
- **Default:** 0  
- **Example:** 0  

### **changesRules.changesStatus**
- **Type:** String  
- **Required:** Yes  
- **Description:** Change eligibility status  (for the most restrictive condition).  

  T: Non changeable

  H: Changeable with restrictions

  F: Free flight change
- **Constraints:** "T" for non-changeable, "H" for changeable with restrictions, "F" for free flight change.  
- **Default:** "T"  
- **Example:** "T"  

### **changesRules.changesFee**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Fee applied for making changes to the ticket (for the most restrictive condition).  If changesStatus = H, it should not be "null" and if changesStatus = T/F, it can be "null"
- **Constraints:** Must be a non-negative value.  
- **Default:** 0.0  
- **Example:** 0.0  

### **changesRules.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency in which change fees are applied. If changesStatus = H, it should not be "null". 
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** "USD"  
- **Example:** "USD"  

### **changesRules.revNoshow**
- **Type:** String  
- **Required:** Yes  
- **Description:** Indicates if a no-show affects changes (for the most restrictive condition).  

  T: Non changeable

  H: Changeable with restrictions

  F: Free flight change
- **Constraints:** "T" for non-changeable, "H" for changeable with restrictions, "F" for free flight change.  
- **Default:** "T"  
- **Example:** "T"  

### **changesRules.revNoShowCondition**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Time before scheduled flight departure.  
- **Constraints:** Must be a valid predefined condition code.  
- **Default:** 0  
- **Example:** 0  

### **changesRules.revNoshowFee**
- **Type:** Float  
- **Required:** Yes  
- **Description:** The total fee charged to change flight in case of no show. If revNoshow = H, it should not be "null." This value includes the change flight fee and no-show penalty.
- **Constraints:** Must be a non-negative value.  
- **Default:** 0.0  
- **Example:** 0.0  

### **changesRules.ruleDetailList**
- **Type:** Array  
- **Required:** Yes  
- **Description:** Detailed change policies applied at different time frames.  
- **Constraints:** Must contain at least one rule detail entry.  
- **Default:** None  
- **Example:** [{...}]

*(Fields for changesRules.ruleDetailList remain similar to refundRules.ruleDetailList)*

## **serviceElements**
- **Type:** Array  
- **Required:** Yes  
- **Description:** Additional service elements included in the booking. This function is used to fetch the other service rules of the selected airline. There is only one array for one way, and two arrays for round-trip. The first array is for the outbound, and the second array is for the inbound.
- **Constraints:** Must contain at least one service element.  
- **Default:** None  
- **Example:** [{...}]

### **serviceElements.hasFreeSeat**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Indicates whether free seat selection is available.  

  0: Not included

  1: All included

  2：Part included
- **Constraints:** 0 for no free seat, 1 for free seat, 2 for part included.  
- **Default:** 0  
- **Example:** 0  

### **serviceElements.hasFreeMeal**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Indicates whether free meal service is available.  

  0: Not included

  1: Included
- **Constraints:** 0 for no free meal, 1 for free meal.  
- **Default:** 0  
- **Example:** 0  


## **ancillaryProductElements**
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of ancillary products available for purchase. The details of the extra baggage offering are available in the ancillaryProductElements within both “search” and the “verify” response.
- **Constraints:** None 
- **Default:** None  
- **Example:** [{...}]

### **ancillaryProductElements.segmentIndex**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Segment number to which the ancillary product applies. Starts from 1. If it is return trip, sequence for outbound trip and inbound trip would be together. 
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** 1  

### **ancillaryProductElements.endSegmentIndex**
- **Type:** Integer  
- **Required:** No  
- **Description:** Last segment index for multi-segment applicability.  
- **Constraints:** Can be null if not applicable.  
- **Default:** null  
- **Example:** null  

### **ancillaryProductElements.productCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique code identifying the ancillary product. It would be used in the order request. 
- **Constraints:** Must be a valid product code.  
- **Default:** None  
- **Example:** "SCI_BAG_1PC_18KG"  

### **ancillaryProductElements.productName**
- **Type:** String  
- **Required:** Yes  
- **Description:** Name of the ancillary product.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "StandardCheckInBaggage"  

### **ancillaryProductElements.productType**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Type of ancillary product.  

  1: Check-in baggage

  3: Cabin Baggage Overhead Locker

  Currently, only baggage is available.
- **Constraints:** Must be a valid predefined type.  
- **Default:** 1  
- **Example:** 1  

### **ancillaryProductElements.canPurchaseWithTicket**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Indicates if the product can be purchased with the ticket.  
- **Constraints:** 1 for yes, 0 for no.  
- **Default:** 1  
- **Example:** 1  

### **ancillaryProductElements.canPurchasePostTicket**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Indicates if the product can be purchased after ticket issuance.  
- **Constraints:** 1 for yes, 0 for no.  
- **Default:** 0  
- **Example:** 0  

### **ancillaryProductElements.price**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Price of the ancillary product.  
- **Constraints:** Must be a non-negative value.  
- **Default:** None  
- **Example:** 68.00  

### **ancillaryProductElements.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency in which the ancillary product is priced.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** "USD"  
- **Example:** "USD"  

### **ancillaryProductElements.vendorPrice**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Vendor price of the ancillary product.  
- **Constraints:** Must be a non-negative value.  
- **Default:** None  
- **Example:** 68.00  

### **ancillaryProductElements.vendorCurrency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency in which the vendor prices the ancillary product.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** "USD"  
- **Example:** "USD"  

### **ancillaryProductElements.clientTechnicalServiceFee**
- **Type:** Float  
- **Required:** Yes  
- **Description:** The service fee charged by Atlas for the purchase of the ancillary.
- **Constraints:** Must be a non-negative value.  
- **Default:** 0  
- **Example:** 0  

### **ancillaryProductElements.clientTechnicalServiceFeeMode**
- **Type:** String  
- **Required:** No  
- **Description:** Mode of applying the technical service fee.  

  Transaction Fee Mode values:

  PER_SEGMENT: Each segment of an itinerary (per passenger)

  PER_TICKET: No. of tickets in a booking

  PER_PAX: Per passenger

  PER_BOOKING: Per atlas booking (order #)  
- **Constraints:** Can be null if not applicable.  
- **Default:** null  
- **Example:** null  

### **ancillaryProductElements.auxBaggageElement**
- **Type:** Object  
- **Required:** Yes  
- **Description:** Additional details related to baggage ancillary products.  
- **Constraints:** None  
- **Default:** None  
- **Example:** {...}

#### **auxBaggageElement.piece**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of baggage pieces allowed.  
- **Constraints:** Must be a positive integer.  
- **Default:** 1  
- **Example:** 1  

#### **auxBaggageElement.weight**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Weight limit in kilograms.  

  0：No Limitation about piece;

  higher than 0：Maximum pieces
- **Constraints:** Must be a positive integer.  
- **Default:** 18  
- **Example:** 18  

#### **auxBaggageElement.isAllWeight**
- **Type:** Boolean  
- **Required:** Yes  
- **Description:** Value mentions maximum weight for ancillary baggage; this should be greater than 0.
- **Constraints:** true or false.  
- **Default:** true  
- **Example:** true  

### **auxBaggageElement.size**
- **Type:** String  
- **Required:** No  
- **Description:** Dimensions of the baggage allowed.  
- **Constraints:** Format should be L*W*H (e.g., 45*35*20cm).  
- **Default:** ""  
- **Example:** "45*35*20cm"  

### **ancillaryProductElements.offerId**
- **Type:** String  
- **Required:** No  
- **Description:** The identifier of the offer of ancillary product. This will be "null" in the booking flow but will have an id in the post-ticketing flow.
- **Constraints:** Can be null if not applicable.  
- **Default:** null  
- **Example:** null  

### **ancillaryProductElements.maxQty**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Maximum quantity of the ancillary product that can be purchased.  
- **Constraints:** Must be a positive integer.  
- **Default:** 1  
- **Example:** 1  

### **ancillaryProductElements.minQty**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Minimum quantity of the ancillary product that must be purchased.  
- **Constraints:** Must be a positive integer.  
- **Default:** 1  
- **Example:** 1  

### **ancillaryProductElements.categoryCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Category classification of the ancillary product.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "StandardCheckInBaggage"  

### **ancillaryProductElements.ancillaryCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Code uniquely identifying the ancillary product.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "SCI_BAG_1PC_18KG"  

### **ancillaryProductElements.auxSeatElement**
- **Type:** Object  
- **Required:** No  
- **Description:** Additional details related to seat selection (if applicable).  
- **Constraints:** Can be null if not applicable.  
- **Default:** null  
- **Example:** null  

### **ancillaryProductElements.displayPrice**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Price displayed to the user for the ancillary product in display currency.  
- **Constraints:** Must be a non-negative value.  
- **Default:** None  
- **Example:** 68.00  

### **ancillaryProductElements.displayCurrency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency in which the display price is shown.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** "USD"  
- **Example:** "USD"  



## **vendorFare**
- **Type:** Object  
- **Required:** No  
- **Description:** Vendor-specific fare details.  
- **Constraints:** Can be null if not available.  
- **Default:** null  
- **Example:** null  

## **bundleOptions**
- **Type:** Array  
- **Required:** No  
- **Description:** Available fare bundle options.  
- **Constraints:** Can be empty if no bundle options are available.  
- **Default:** []  
- **Example:** []  

## **links**
- **Type:** Object  
- **Required:** No  
- **Description:** Links to additional resources related to the booking.  
- **Constraints:** Can be null if no links are available.  
- **Default:** null  
- **Example:** null  

## **separateBookings**
- **Type:** Boolean  
- **Required:** No  
- **Description:** Indicates if the booking is split into multiple reservations.  
- **Constraints:** true or false.  
- **Default:** false  
- **Example:** false  

## **refreshTime**
- **Type:** String  
- **Required:** Yes  
- **Description:** Timestamp of when the data was last refreshed in cache.  
- **Constraints:** Must be in ISO 8601 format.  
- **Default:** None  
- **Example:** "2025-03-21T06:37:46Z"  

## **displayFare**
- **Type:** Object  
- **Required:** YNo 
- **Description:** Pricing details displayed to the user in the display fare currency.  
- **Constraints:** Must contain a valid currency field.  
- **Default:** None  
- **Example:** { "currency": "PHP" }  

### **displayFare.currency**
- **Type:** String  
- **Required:** No  
- **Description:** Currency in which the fare is displayed.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** "PHP"  
- **Example:** "PHP"  

{% endtab %}

{% tab title="Samples" %}
```
{
    "routings": [
        {
            "fid": "YDkI0hwzBfb9ddFvrDAYxiXIM5_TOsvzyHw_YGVbGKPA0UWjv7PPyg..",
            "routingIdentifier": "RFhCX1JVSF8xXzIwMjUwMzI2X18xXzBfMHxMWk85NDYzMV9hcGlfMXwxfDYyLjA5XzYyLjA5XzM5Ljg2XzAuMDBfMTY0LjA0X1VTRHxEWEJfUlVIXzFfMjAyNTAzMjZfXzFfMF8wXkRYQi1GMzUwOC0tUlVILTIwMjUwMzI2MjA1MC0yMDI1MDMyNjIxNTAtZmx5LTEtXjYyLjA5XzYyLjA5XzM5Ljg2XzAuMDBfMTY0LjA0XkFGM0FQSV9BRjNBUEleXkFGM0FQSTFEWEJSVUgyMDAyMDI1MDMyNl5VU0ReNjIuMDleNjIuMDleMzkuODZ8MHwyMDI1MDMyMTE1MDcxNnwwfDE3NDI1NDA4MzYyNDFDNzUwVHx8fHx8MC4wMHwzfDB8UEhQ./M+dNu7dXmuDdTm+ptn2ggbAqbU5wrfNObXu6RbD0SY=",
            "supportCreditTransPayment": "0",
            "supportPaymentMethods": [
                1
            ],
            "currency": "USD",
            "adultPrice": 61.96,
            "adultTax": 0.13,
            "childPrice": 61.96,
            "childTax": 0.13,
            "infantPrice": 39.86,
            "infantTax": 0.00,
            "infantAllowed": true,
            "transactionFeePerPax": 0.00,
            "transactionFee": 0.00,
            "transactionFeeMode": "PER_PAX",
            "nationalityType": 0,
            "nationality": "",
            "suitAge": "",
            "PaxType": "ADT",
            "fromSegments": [
                {
                    "segmentIndex": 1,
                    "carrier": "F3",
                    "flightNumber": "F3508",
                    "depAirport": "DXB",
                    "depTime": "202503262050",
                    "arrAirport": "RUH",
                    "arrTime": "202503262150",
                    "stopCities": "",
                    "duration": 120,
                    "codeShare": false,
                    "cabin": "",
                    "cabinClass": 1,
                    "seatCount": 9,
                    "aircraftCode": "320",
                    "depTerminal": "1",
                    "arrTerminal": "4",
                    "operatingCarrier": "",
                    "operatingFlightnumber": "",
                    "fareFamily": "fly"
                }
            ],
            "retSegments": [],
            "combineIndexs": [],
            "rule": {
                "hasBaggage": 1,
                "baggageElements": [
                    {
                        "segmentNo": 1,
                        "baggageType": "CabinBaggageUnderSeat",
                        "passengerType": 0,
                        "baggagePiece": 1,
                        "baggageWeight": -1,
                        "baggageSize": "40*30*20cm"
                    },
                    {
                        "segmentNo": 1,
                        "baggageType": "StandardCheckInBaggage",
                        "passengerType": 0,
                        "baggagePiece": 0,
                        "baggageWeight": 0,
                        "baggageSize": ""
                    }
                ],
                "refundRules": [
                    {
                        "refundType": 0,
                        "refundStatus": "T",
                        "refundFee": 0.0,
                        "currency": "USD",
                        "refNoshow": "T",
                        "refNoShowCondition": 0,
                        "refNoshowFee": 0.0,
                        "ruleDetailList": [
                            {
                                "ruleId": 35618,
                                "status": "T",
                                "startMinute": 525600,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "USD"
                            },
                            {
                                "ruleId": 35621,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "USD"
                            }
                        ]
                    }
                ],
                "changesRules": [
                    {
                        "changesType": 0,
                        "changesStatus": "T",
                        "changesFee": 0.0,
                        "currency": "USD",
                        "revNoshow": "T",
                        "revNoShowCondition": 0,
                        "revNoshowFee": 0.0,
                        "ruleDetailList": [
                            {
                                "ruleId": 35633,
                                "status": "H",
                                "startMinute": 525600,
                                "endMinute": 90,
                                "amount": 250.0,
                                "currency": "SAR"
                            },
                            {
                                "ruleId": 35636,
                                "status": "T",
                                "startMinute": 90,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "USD"
                            },
                            {
                                "ruleId": 35639,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "USD"
                            }
                        ]
                    }
                ],
                "serviceElements": [
                    {
                        "hasFreeSeat": 0,
                        "hasFreeMeal": 0
                    }
                ]
            },
            "ancillaryProductElements": [
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_BAG_1PC_25KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 1,
                    "price": 50.73,
                    "currency": "USD",
                    "vendorPrice": 50.73,
                    "vendorCurrency": "USD",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 1,
                        "weight": 25,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_BAG_1PC_25KG",
                    "auxSeatElement": null,
                    "displayPrice": 2906.22,
                    "displayCurrency": "PHP"
                },
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_BAG_1PC_15KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 1,
                    "price": 30.78,
                    "currency": "USD",
                    "vendorPrice": 30.78,
                    "vendorCurrency": "USD",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 1,
                        "weight": 15,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_BAG_1PC_15KG",
                    "auxSeatElement": null,
                    "displayPrice": 1763.32,
                    "displayCurrency": "PHP"
                }
            ],
            "vendorFare": null,
            "bundleOptions": [],
            "links": null,
            "separateBookings": false,
            "refreshTime": "2025-03-21T06:37:46Z",
            "displayFare": {
                "currency": "PHP",
                "exchangeRate": 57.28800000,
                "adultPrice": 3549.56,
                "adultTax": 7.45,
                "childPrice": 3549.56,
                "childTax": 7.45,
                "infantPrice": 2283.50,
                "infantTax": 0.00
            },
            "ancillarySupported": [
                "luggage"
            ]
        },
        {
            "fid": "NambpKP2quvdOaGHmrQQkFvfmXFGCrSuUktChVpxQFQ2RyRdSb0vQA..",
            "routingIdentifier": "RFhCX1JVSF8xXzIwMjUwMzI2X18xXzBfMHxMWk85NDYzMV9hcGlfMXwxfDY0LjQ2XzY0LjQ2XzI5LjcxXzAuMDBfMTU4LjYzX1VTRHxEWEJfUlVIXzFfMjAyNTAzMjZfXzFfMF8wXkRYQi1GMzUxNC0tUlVILTIwMjUwMzI2MDAwMS0yMDI1MDMyNjAwNTUtZmx5LTEtXjY0LjQ2XzY0LjQ2XzI5LjcxXzAuMDBfMTU4LjYzXkFGM0FQSV9BRjNBUEleXkFGM0FQSTFEWEJSVUgyMDAyMDI1MDMyNl5VU0ReNjQuNDZeNjQuNDZeMjkuNzF8MHwyMDI1MDMyMTE1MDcxNnwwfDE3NDI1NDA4MzYyNDFDNzUwVHx8fHx8MC4wMHwzfDB8UEhQ.iXYJ/0J5PwMNJqv6dMdzuuxKCUSjHR023Fx/o/JXxn8=",
            "supportCreditTransPayment": "0",
            "supportPaymentMethods": [
                1
            ],
            "currency": "USD",
            "adultPrice": 64.33,
            "adultTax": 0.13,
            "childPrice": 64.33,
            "childTax": 0.13,
            "infantPrice": 29.71,
            "infantTax": 0.00,
            "infantAllowed": true,
            "transactionFeePerPax": 0.00,
            "transactionFee": 0.00,
            "transactionFeeMode": "PER_PAX",
            "nationalityType": 0,
            "nationality": "",
            "suitAge": "",
            "PaxType": "ADT",
            "fromSegments": [
                {
                    "segmentIndex": 1,
                    "carrier": "F3",
                    "flightNumber": "F3514",
                    "depAirport": "DXB",
                    "depTime": "202503260001",
                    "arrAirport": "RUH",
                    "arrTime": "202503260055",
                    "stopCities": "",
                    "duration": 114,
                    "codeShare": false,
                    "cabin": "",
                    "cabinClass": 1,
                    "seatCount": 9,
                    "aircraftCode": "320",
                    "depTerminal": "1",
                    "arrTerminal": "4",
                    "operatingCarrier": "",
                    "operatingFlightnumber": "",
                    "fareFamily": "fly"
                }
            ],
            "retSegments": [],
            "combineIndexs": [],
            "rule": {
                "hasBaggage": 1,
                "baggageElements": [
                    {
                        "segmentNo": 1,
                        "baggageType": "CabinBaggageUnderSeat",
                        "passengerType": 0,
                        "baggagePiece": 1,
                        "baggageWeight": -1,
                        "baggageSize": "40*30*20cm"
                    },
                    {
                        "segmentNo": 1,
                        "baggageType": "StandardCheckInBaggage",
                        "passengerType": 0,
                        "baggagePiece": 0,
                        "baggageWeight": 0,
                        "baggageSize": ""
                    }
                ],
                "refundRules": [
                    {
                        "refundType": 0,
                        "refundStatus": "T",
                        "refundFee": 0.0,
                        "currency": "USD",
                        "refNoshow": "T",
                        "refNoShowCondition": 0,
                        "refNoshowFee": 0.0,
                        "ruleDetailList": [
                            {
                                "ruleId": 35618,
                                "status": "T",
                                "startMinute": 525600,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "USD"
                            },
                            {
                                "ruleId": 35621,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "USD"
                            }
                        ]
                    }
                ],
                "changesRules": [
                    {
                        "changesType": 0,
                        "changesStatus": "T",
                        "changesFee": 0.0,
                        "currency": "USD",
                        "revNoshow": "T",
                        "revNoShowCondition": 0,
                        "revNoshowFee": 0.0,
                        "ruleDetailList": [
                            {
                                "ruleId": 35633,
                                "status": "H",
                                "startMinute": 525600,
                                "endMinute": 90,
                                "amount": 250.0,
                                "currency": "SAR"
                            },
                            {
                                "ruleId": 35636,
                                "status": "T",
                                "startMinute": 90,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "USD"
                            },
                            {
                                "ruleId": 35639,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "USD"
                            }
                        ]
                    }
                ],
                "serviceElements": [
                    {
                        "hasFreeSeat": 0,
                        "hasFreeMeal": 0
                    }
                ]
            },
            "ancillaryProductElements": [
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_BAG_1PC_25KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 1,
                    "price": 52.09,
                    "currency": "USD",
                    "vendorPrice": 52.09,
                    "vendorCurrency": "USD",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 1,
                        "weight": 25,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_BAG_1PC_25KG",
                    "auxSeatElement": null,
                    "displayPrice": 2984.13,
                    "displayCurrency": "PHP"
                },
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_BAG_1PC_15KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 1,
                    "price": 29.09,
                    "currency": "USD",
                    "vendorPrice": 29.09,
                    "vendorCurrency": "USD",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 1,
                        "weight": 15,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_BAG_1PC_15KG",
                    "auxSeatElement": null,
                    "displayPrice": 1666.51,
                    "displayCurrency": "PHP"
                }
            ],
            "vendorFare": null,
            "bundleOptions": [],
            "links": null,
            "separateBookings": false,
            "refreshTime": "2025-03-21T06:37:46Z",
            "displayFare": {
                "currency": "PHP",
                "exchangeRate": 57.28800000,
                "adultPrice": 3685.34,
                "adultTax": 7.45,
                "childPrice": 3685.34,
                "childTax": 7.45,
                "infantPrice": 1702.03,
                "infantTax": 0.00
            },
            "ancillarySupported": [
                "luggage"
            ]
        },
        {
            "fid": "tDROWXwNKf9ix0iSmX02Pah_QkxPAuQOfhGXtx9FCzQOTGDxLPGYBQ..",
            "routingIdentifier": "RFhCX1JVSF8xXzIwMjUwMzI2X18xXzBfMHxMWk85NDYzMV9hcGlfMXwxfDQ1LjMyXzQ1LjMyXzI1Ljg4XzAuMDBfMTE2LjUyX1VTRHxEWEJfUlVIXzFfMjAyNTAzMjZfXzFfMF8wXkRYQi1GMzUwNi0tUlVILTIwMjUwMzI2MTI1MC0yMDI1MDMyNjEzNTAtZmx5LTEtXjQ1LjMyXzQ1LjMyXzI1Ljg4XzAuMDBfMTE2LjUyXkFGM0FQSV9BRjNBUEleXkFGM0FQSTFEWEJSVUgyMDAyMDI1MDMyNl5VU0ReNDUuMzJeNDUuMzJeMjUuODh8MHwyMDI1MDMyMTE1MDcxNnwwfDE3NDI1NDA4MzYyNDFDNzUwVHx8fHx8MC4wMHwzfDB8UEhQ.PenZ2+d843mpmTvXxm1p8fOm1Tae1yAFzZ8GmJLGffM=",
            "supportCreditTransPayment": "0",
            "supportPaymentMethods": [
                1
            ],
            "currency": "USD",
            "adultPrice": 45.19,
            "adultTax": 0.13,
            "childPrice": 45.19,
            "childTax": 0.13,
            "infantPrice": 25.88,
            "infantTax": 0.00,
            "infantAllowed": true,
            "transactionFeePerPax": 0.00,
            "transactionFee": 0.00,
            "transactionFeeMode": "PER_PAX",
            "nationalityType": 0,
            "nationality": "",
            "suitAge": "",
            "PaxType": "ADT",
            "fromSegments": [
                {
                    "segmentIndex": 1,
                    "carrier": "F3",
                    "flightNumber": "F3506",
                    "depAirport": "DXB",
                    "depTime": "202503261250",
                    "arrAirport": "RUH",
                    "arrTime": "202503261350",
                    "stopCities": "",
                    "duration": 120,
                    "codeShare": false,
                    "cabin": "",
                    "cabinClass": 1,
                    "seatCount": 9,
                    "aircraftCode": "320",
                    "depTerminal": "1",
                    "arrTerminal": "4",
                    "operatingCarrier": "",
                    "operatingFlightnumber": "",
                    "fareFamily": "fly"
                }
            ],
            "retSegments": [],
            "combineIndexs": [],
            "rule": {
                "hasBaggage": 1,
                "baggageElements": [
                    {
                        "segmentNo": 1,
                        "baggageType": "CabinBaggageUnderSeat",
                        "passengerType": 0,
                        "baggagePiece": 1,
                        "baggageWeight": -1,
                        "baggageSize": "40*30*20cm"
                    },
                    {
                        "segmentNo": 1,
                        "baggageType": "StandardCheckInBaggage",
                        "passengerType": 0,
                        "baggagePiece": 0,
                        "baggageWeight": 0,
                        "baggageSize": ""
                    }
                ],
                "refundRules": [
                    {
                        "refundType": 0,
                        "refundStatus": "T",
                        "refundFee": 0.0,
                        "currency": "USD",
                        "refNoshow": "T",
                        "refNoShowCondition": 0,
                        "refNoshowFee": 0.0,
                        "ruleDetailList": [
                            {
                                "ruleId": 35618,
                                "status": "T",
                                "startMinute": 525600,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "USD"
                            },
                            {
                                "ruleId": 35621,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "USD"
                            }
                        ]
                    }
                ],
                "changesRules": [
                    {
                        "changesType": 0,
                        "changesStatus": "T",
                        "changesFee": 0.0,
                        "currency": "USD",
                        "revNoshow": "T",
                        "revNoShowCondition": 0,
                        "revNoshowFee": 0.0,
                        "ruleDetailList": [
                            {
                                "ruleId": 35633,
                                "status": "H",
                                "startMinute": 525600,
                                "endMinute": 90,
                                "amount": 250.0,
                                "currency": "SAR"
                            },
                            {
                                "ruleId": 35636,
                                "status": "T",
                                "startMinute": 90,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "USD"
                            },
                            {
                                "ruleId": 35639,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "USD"
                            }
                        ]
                    }
                ],
                "serviceElements": [
                    {
                        "hasFreeSeat": 0,
                        "hasFreeMeal": 0
                    }
                ]
            },
            "ancillaryProductElements": [
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_BAG_1PC_25KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 1,
                    "price": 55.66,
                    "currency": "USD",
                    "vendorPrice": 55.66,
                    "vendorCurrency": "USD",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 1,
                        "weight": 25,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_BAG_1PC_25KG",
                    "auxSeatElement": null,
                    "displayPrice": 3188.65,
                    "displayCurrency": "PHP"
                },
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_BAG_1PC_15KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 1,
                    "price": 17.85,
                    "currency": "USD",
                    "vendorPrice": 17.85,
                    "vendorCurrency": "USD",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 1,
                        "weight": 15,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_BAG_1PC_15KG",
                    "auxSeatElement": null,
                    "displayPrice": 1022.59,
                    "displayCurrency": "PHP"
                }
            ],
            "vendorFare": null,
            "bundleOptions": [],
            "links": null,
            "separateBookings": false,
            "refreshTime": "2025-03-21T06:37:46Z",
            "displayFare": {
                "currency": "PHP",
                "exchangeRate": 57.28800000,
                "adultPrice": 2588.84,
                "adultTax": 7.45,
                "childPrice": 2588.84,
                "childTax": 7.45,
                "infantPrice": 1482.61,
                "infantTax": 0.00
            },
            "ancillarySupported": [
                "luggage"
            ]
        },
        {
            "fid": "qZrmKcOxE8jpkyktYLrHJqFRxn5voJjk2xQuck-wiaBP5j2wkCnJFQ..",
            "routingIdentifier": "RFhCX1JVSF8xXzIwMjUwMzI2X18xXzBfMHxMWk85NDYzMV9hcGlfMXwxfDQzLjY3XzQzLjY3XzI2LjgxXzAuMDBfMTE0LjE1X1VTRHxEWEJfUlVIXzFfMjAyNTAzMjZfXzFfMF8wXkRYQi1GMzUxMi0tUlVILTIwMjUwMzI2MjEzMC0yMDI1MDMyNjIyMjUtZmx5LTEtXjQzLjY3XzQzLjY3XzI2LjgxXzAuMDBfMTE0LjE1XkFGM0FQSV9BRjNBUEleXkFGM0FQSTFEWEJSVUgyMDAyMDI1MDMyNl5VU0ReNDMuNjdeNDMuNjdeMjYuODF8MHwyMDI1MDMyMTE1MDcxNnwwfDE3NDI1NDA4MzYyNDFDNzUwVHx8fHx8MC4wMHwzfDB8UEhQ.dnYSafnNAc+0BFNUT7ODskVXugUilckm3p9NCCj6SKw=",
            "supportCreditTransPayment": "0",
            "supportPaymentMethods": [
                1
            ],
            "currency": "USD",
            "adultPrice": 43.54,
            "adultTax": 0.13,
            "childPrice": 43.54,
            "childTax": 0.13,
            "infantPrice": 26.81,
            "infantTax": 0.00,
            "infantAllowed": true,
            "transactionFeePerPax": 0.00,
            "transactionFee": 0.00,
            "transactionFeeMode": "PER_PAX",
            "nationalityType": 0,
            "nationality": "",
            "suitAge": "",
            "PaxType": "ADT",
            "fromSegments": [
                {
                    "segmentIndex": 1,
                    "carrier": "F3",
                    "flightNumber": "F3512",
                    "depAirport": "DXB",
                    "depTime": "202503262130",
                    "arrAirport": "RUH",
                    "arrTime": "202503262225",
                    "stopCities": "",
                    "duration": 115,
                    "codeShare": false,
                    "cabin": "",
                    "cabinClass": 1,
                    "seatCount": 9,
                    "aircraftCode": "320",
                    "depTerminal": "1",
                    "arrTerminal": "4",
                    "operatingCarrier": "",
                    "operatingFlightnumber": "",
                    "fareFamily": "fly"
                }
            ],
            "retSegments": [],
            "combineIndexs": [],
            "rule": {
                "hasBaggage": 1,
                "baggageElements": [
                    {
                        "segmentNo": 1,
                        "baggageType": "CabinBaggageUnderSeat",
                        "passengerType": 0,
                        "baggagePiece": 1,
                        "baggageWeight": -1,
                        "baggageSize": "40*30*20cm"
                    },
                    {
                        "segmentNo": 1,
                        "baggageType": "StandardCheckInBaggage",
                        "passengerType": 0,
                        "baggagePiece": 0,
                        "baggageWeight": 0,
                        "baggageSize": ""
                    }
                ],
                "refundRules": [
                    {
                        "refundType": 0,
                        "refundStatus": "T",
                        "refundFee": 0.0,
                        "currency": "USD",
                        "refNoshow": "T",
                        "refNoShowCondition": 0,
                        "refNoshowFee": 0.0,
                        "ruleDetailList": [
                            {
                                "ruleId": 35618,
                                "status": "T",
                                "startMinute": 525600,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "USD"
                            },
                            {
                                "ruleId": 35621,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "USD"
                            }
                        ]
                    }
                ],
                "changesRules": [
                    {
                        "changesType": 0,
                        "changesStatus": "T",
                        "changesFee": 0.0,
                        "currency": "USD",
                        "revNoshow": "T",
                        "revNoShowCondition": 0,
                        "revNoshowFee": 0.0,
                        "ruleDetailList": [
                            {
                                "ruleId": 35633,
                                "status": "H",
                                "startMinute": 525600,
                                "endMinute": 90,
                                "amount": 250.0,
                                "currency": "SAR"
                            },
                            {
                                "ruleId": 35636,
                                "status": "T",
                                "startMinute": 90,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "USD"
                            },
                            {
                                "ruleId": 35639,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "USD"
                            }
                        ]
                    }
                ],
                "serviceElements": [
                    {
                        "hasFreeSeat": 0,
                        "hasFreeMeal": 0
                    }
                ]
            },
            "ancillaryProductElements": [
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_BAG_1PC_25KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 1,
                    "price": 53.77,
                    "currency": "USD",
                    "vendorPrice": 53.77,
                    "vendorCurrency": "USD",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 1,
                        "weight": 25,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_BAG_1PC_25KG",
                    "auxSeatElement": null,
                    "displayPrice": 3080.38,
                    "displayCurrency": "PHP"
                },
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_BAG_1PC_15KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 1,
                    "price": 16.97,
                    "currency": "USD",
                    "vendorPrice": 16.97,
                    "vendorCurrency": "USD",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 1,
                        "weight": 15,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_BAG_1PC_15KG",
                    "auxSeatElement": null,
                    "displayPrice": 972.18,
                    "displayCurrency": "PHP"
                }
            ],
            "vendorFare": null,
            "bundleOptions": [],
            "links": null,
            "separateBookings": false,
            "refreshTime": "2025-03-21T06:37:46Z",
            "displayFare": {
                "currency": "PHP",
                "exchangeRate": 57.28800000,
                "adultPrice": 2494.32,
                "adultTax": 7.45,
                "childPrice": 2494.32,
                "childTax": 7.45,
                "infantPrice": 1535.89,
                "infantTax": 0.00
            },
            "ancillarySupported": [
                "luggage"
            ]
        },
        {
            "fid": "pSPZSHm7yoBvPztz8_RcIcJt7DXCtIqz4PgHfPcMJwmasztZagL0Ww..",
            "routingIdentifier": "RFhCX1JVSF8xXzIwMjUwMzI2X18xXzBfMHxMWk85NDYzMV9hcGlfMXwxfDQwLjUwXzQwLjUwXzIwLjg0XzAuMDBfMTAxLjg0X1VTRHxEWEJfUlVIXzFfMjAyNTAzMjZfXzFfMF8wXkRXQy1GMzUyNi0tUlVILTIwMjUwMzI2MjMzMC0yMDI1MDMyNzAwMzAtZmx5LTEtXjQwLjUwXzQwLjUwXzIwLjg0XzAuMDBfMTAxLjg0XkFGM0FQSV9BRjNBUEleXkFGM0FQSTFEWEJSVUgyMDAyMDI1MDMyNl5VU0ReNDAuNTBeNDAuNTBeMjAuODR8MHwyMDI1MDMyMTE1MDcxNnwwfDE3NDI1NDA4MzYyNDFDNzUwVHx8fHx8MC4wMHwzfDB8UEhQ.NdCjyLpmZVvEDNGvpw7RhxOSOg/T0/sfekjhVTDBVVY=",
            "supportCreditTransPayment": "0",
            "supportPaymentMethods": [
                1
            ],
            "currency": "USD",
            "adultPrice": 40.37,
            "adultTax": 0.13,
            "childPrice": 40.37,
            "childTax": 0.13,
            "infantPrice": 20.84,
            "infantTax": 0.00,
            "infantAllowed": true,
            "transactionFeePerPax": 0.00,
            "transactionFee": 0.00,
            "transactionFeeMode": "PER_PAX",
            "nationalityType": 0,
            "nationality": "",
            "suitAge": "",
            "PaxType": "ADT",
            "fromSegments": [
                {
                    "segmentIndex": 1,
                    "carrier": "F3",
                    "flightNumber": "F3526",
                    "depAirport": "DWC",
                    "depTime": "202503262330",
                    "arrAirport": "RUH",
                    "arrTime": "202503270030",
                    "stopCities": "",
                    "duration": 120,
                    "codeShare": false,
                    "cabin": "",
                    "cabinClass": 1,
                    "seatCount": 9,
                    "aircraftCode": "320",
                    "depTerminal": "",
                    "arrTerminal": "4",
                    "operatingCarrier": "",
                    "operatingFlightnumber": "",
                    "fareFamily": "fly"
                }
            ],
            "retSegments": [],
            "combineIndexs": [],
            "rule": {
                "hasBaggage": 1,
                "baggageElements": [
                    {
                        "segmentNo": 1,
                        "baggageType": "CabinBaggageUnderSeat",
                        "passengerType": 0,
                        "baggagePiece": 1,
                        "baggageWeight": -1,
                        "baggageSize": "40*30*20cm"
                    },
                    {
                        "segmentNo": 1,
                        "baggageType": "StandardCheckInBaggage",
                        "passengerType": 0,
                        "baggagePiece": 0,
                        "baggageWeight": 0,
                        "baggageSize": ""
                    }
                ],
                "refundRules": [
                    {
                        "refundType": 0,
                        "refundStatus": "T",
                        "refundFee": 0.0,
                        "currency": "USD",
                        "refNoshow": "T",
                        "refNoShowCondition": 0,
                        "refNoshowFee": 0.0,
                        "ruleDetailList": [
                            {
                                "ruleId": 35618,
                                "status": "T",
                                "startMinute": 525600,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "USD"
                            },
                            {
                                "ruleId": 35621,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "USD"
                            }
                        ]
                    }
                ],
                "changesRules": [
                    {
                        "changesType": 0,
                        "changesStatus": "T",
                        "changesFee": 0.0,
                        "currency": "USD",
                        "revNoshow": "T",
                        "revNoShowCondition": 0,
                        "revNoshowFee": 0.0,
                        "ruleDetailList": [
                            {
                                "ruleId": 35633,
                                "status": "H",
                                "startMinute": 525600,
                                "endMinute": 90,
                                "amount": 250.0,
                                "currency": "SAR"
                            },
                            {
                                "ruleId": 35636,
                                "status": "T",
                                "startMinute": 90,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "USD"
                            },
                            {
                                "ruleId": 35639,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "USD"
                            }
                        ]
                    }
                ],
                "serviceElements": [
                    {
                        "hasFreeSeat": 0,
                        "hasFreeMeal": 0
                    }
                ]
            },
            "ancillaryProductElements": [
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_BAG_1PC_25KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 1,
                    "price": 51.28,
                    "currency": "USD",
                    "vendorPrice": 51.28,
                    "vendorCurrency": "USD",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 1,
                        "weight": 25,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_BAG_1PC_25KG",
                    "auxSeatElement": null,
                    "displayPrice": 2937.73,
                    "displayCurrency": "PHP"
                },
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_BAG_1PC_15KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 1,
                    "price": 30.88,
                    "currency": "USD",
                    "vendorPrice": 30.88,
                    "vendorCurrency": "USD",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 1,
                        "weight": 15,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_BAG_1PC_15KG",
                    "auxSeatElement": null,
                    "displayPrice": 1769.05,
                    "displayCurrency": "PHP"
                }
            ],
            "vendorFare": null,
            "bundleOptions": [],
            "links": null,
            "separateBookings": false,
            "refreshTime": "2025-03-21T06:37:46Z",
            "displayFare": {
                "currency": "PHP",
                "exchangeRate": 57.28800000,
                "adultPrice": 2312.72,
                "adultTax": 7.45,
                "childPrice": 2312.72,
                "childTax": 7.45,
                "infantPrice": 1193.88,
                "infantTax": 0.00
            },
            "ancillarySupported": [
                "luggage"
            ]
        }
    ],
    "status": 0,
    "msg": null
}
```
{% endtab %}
{% endtabs %}

## How to ......

### 1. How to search for Oneway or Roundtrip flights?

If you want to search for oneway flights, please set `tripType` as 1 and keep `retDate` blank

```json
{
    "tripType": "1",
    "fromDate": "20220125",
    "retDate": "",
}
```

In the response, the `retSegments` of each routing will be empty

```json
"routings": [
    {
        "fromSegments": [
            {...}
        ],
        "retSegments": []
    },
    {
        "fromSegments": [
            {...}
        ],
        "retSegments": []
    },
    ...
]
```

If you want to search for roundtrip flights, please set `tripType` as 2 and input `retDate`

```css
{
    "tripType": "2",
    "fromDate": "20220125",
    "retDate": "20220128",
}
```

In the response, the <mark style="color:green;">`retSegments`</mark> of each routing will be empty

```json
"routings": [
    {
        "fromSegments": [
            {...}
        ],
        "retSegments": [
            {...}
        ]
    },
    {
        "fromSegments": [
            {...}
        ],
        "retSegments": [
            {...}
        ]
    },
    ...
]
```

### 2. How to identify direct or connection flights

Regarding direct flights, there will be only one segment in `fromSegments` or `retSegments`

```javascript
 {
 "fromSegments": [
                {
                    ...
                }
            ],
 "retSegments": [
                {
                    ...
                }
            ]
}
```

Regarding connection flights, there will be multiple segments in `fromSegments` or `retSegments`

```json
 {
 "fromSegments": [
                {
                    ...
                },
                {
                    ...
                }
            ],
 "retSegments": [
                {
                    ...
                },
                {
                    ...
                },
                {
                    ...
                }
            ]
}
```

### 3. Where is the baggage allowance mentioned?

#### 3.1. Free checked-in or cabin baggage

The free checked-in or cabin baggage allowance for each fare is available within both `search` and the `verify` response.

{% tabs %}
{% tab title="Schema" %}
**Baggage Element**

*   **segmentNo **<mark style="color:blue;">**int**</mark>

    Segment sequence, start from 1.

    If it is roundtrip, sequence outbond and inbound together.
    
*   **baggageType **<mark style="color:blue;">**string**</mark>

    There are 4 options for baggage:

    StandardCheckInBaggage: Standard Check-in Baggage.

    CabinBaggage: Usually refers to the Cabin Baggage Overhead Locker. Transition value. It will gradually transition to CabinBaggageOverheadLocker.

    CabinBaggageOverheadLocker: Cabin Baggage Overhead Locker.

    CabinBaggageUnderSeat: Cabin Baggage Under Seat. Usually refers to the personal item.
*   **passengerType **<mark style="color:blue;">**string**</mark>

    0: ADT

    1: CHD

    2: INF

    If search or verify for ADT only, then only ADT is returned;

    If search or verify for ADT+CHD, then ADT and CHD are returned.
*   **baggagePiece **<mark style="color:blue;">**int**</mark>

    Baggage pieces：

    0 No limitation

    \>0 Maximum pieces
*   **baggageWeight **<mark style="color:blue;">**int**</mark>

    Baggage Weight, with the unit of KG

    0 means No Free baggage 
    -1 meas No limitation on weight. 

*   **baggageSize **<mark style="color:blue;">**string**</mark>

    Baggage Size: 
    
    length＊width＊height and units. eg. "56＊36＊23cm", "18＊14＊8inch". 
    
    Or Total dimensions (length + width + height) of each piece. eg. "L+W+H<=158cm". 
    
    Empty means no limitation.

{% endtab %}

{% tab title="Samples" %}
```json
{
...,
"rule": {
        "hasBaggage": 0,
        "baggageElements": [
          {
            "segmentNo": 1,
            "baggageType": "StandardCheckInBaggage",
            "passengerType": 0,
            "baggagePiece": 0,
            "baggageWeight": 0,
            "baggageSize": ""
          },
          {
            "segmentNo": 2,
            "baggageType": "StandardCheckInBaggage",
            "passengerType": 0,
            "baggagePiece": 0,
            "baggageWeight": 0,
            "baggageSize": "40*25*20cm"
          }
        ],
                "refundRules": [{...}],
                "changesRules":[{...}]
            }
...
}jso
```
{% endtab %}
{% endtabs %}

#### 3.2. Extra baggage offering

The details of the extra baggage offering are available in the `ancillaryProductElements` within both “search” and the “verify” response

{% tabs %}
{% tab title="Schema" %}
**ancillaryProductElement**

*   **`segmentIndex`  **<mark style="color:blue;">**int**</mark>

Segment sequence. Starts from 1. If it is return trip, sequence for outbound trip and inbound trip would be together.
    
*   **`endSegmentIndex`  **<mark style="color:blue;">**int**</mark>

The last segment for which this information is applicable.
    
*   **`productCode`  **<mark style="color:blue;">**string**</mark>

Unique identifier for the ancillary product. It would be used in the order request.
*   **`productName`  **<mark style="color:blue;">**string**</mark>

Ancillary product name.
*   **`productType`  **<mark style="color:blue;">**int**</mark>

Ancillary product type

1: Check-in baggage

3: Cabin Baggage Overhead Locker

Currently, only baggage is available.
    
*   **`canPurchaseWithTicket`  **<mark style="color:blue;">**int**</mark>

This ancillary product can be purchased during the booking flow. 
    
1=Yes; 0=No  
    
*   **`canPurchasePostTicket`  **<mark style="color:blue;">**int**</mark>

This ancillary product can be purchased in the post-ticketing flow. 
    
1=Yes; 0=No  
    
*   **`price`  **<mark style="color:blue;">**decimal**</mark>

Price for this ancillary.
    
*   **`currency`  **<mark style="color:blue;">**string**</mark>

The currency in which Atlas settles transactions with you.
    
*   **`vendorPrice`  **<mark style="color:blue;">**decimal**</mark>

The price charged by the vendor for the ancillary.
    
*   **`vendorCurrency`  **<mark style="color:blue;">**string**</mark>

The currency in which the vendor charges for the ancillary.
    
*   **`clientTechnicalServiceFee`  **<mark style="color:blue;">**decimal**</mark>

The service fee charged by Atlas for the purchase of the ancillary.
    
* **`auxBaggageElement` Object<**[**AuxBaggageElement**](search.md#10.-auxbaggage-element-schema)**>**
  * **`auxBaggageElement` includes the following parameters**
    *   **`piece`  **<mark style="color:blue;">**int**</mark>

        0：No Limitation about piece;

        \>0：Maximum pieces
    *   **`weight`  **<mark style="color:blue;">**int**</mark>

        Value mentions maximum weight for ancillary baggage; this should be greater than 0.
    *   **`isAllWeight`  **<mark style="color:blue;">**boolean**</mark>

        True：The weight is for all the pieces

        False：The weight is for each piece
        
    *   **`size`  **<mark style="color:blue;">**string**</mark>

        Maximum size for ancillary baggage
        
*   **`offerId`  **<mark style="color:blue;">**string**</mark>

The identifier of the offer of ancillary product. This will be "null" in the booking flow but will have an id in the post-ticketing flow.

*   **`maxQty`  **<mark style="color:blue;">**string**</mark>

Maximum purchase quantity per product

*   **`minQty`  **<mark style="color:blue;">**string**</mark>

Starting purchase quantity per product

*   **`ancillaryCode`  **<mark style="color:blue;">**string**</mark>

The code for this ancillary option. This will be identical to the `productCode`.
{% endtab %}

{% tab title="Samples" %}
```json
 "ancillaryProductElements": [
        {
          "segmentIndex": 1,
          "endSegmentIndex": null,
          "productCode": "SCI_BAG_1PC_15KG",
          "productName": "StandardCheckInBaggage",
          "productType": 1,
          "canPurchaseWithTicket": 1,
          "canPurchasePostTicket": 1,
          "price": 37.94,
          "currency": "USD",
          "vendorPrice": 34.49,
          "vendorCurrency": "GBP",
          "clientTechnicalServiceFee": 0,
          "auxBaggageElement": {
            "piece": 1,
            "weight": 15,
            "isAllWeight": true
          },
          "offerId": null,
          "ancillaryCode": "SCI_BAG_1PC_15KG"
        },
        {
          "segmentIndex": 1,
          "endSegmentIndex": null,
          "productCode": "SCI_BAG_1PC_23KG",
          "productName": "StandardCheckInBaggage",
          "productType": 1,
          "canPurchaseWithTicket": 1,
          "canPurchasePostTicket": 1,
          "price": 40.69,
          "currency": "USD",
          "vendorPrice": 36.99,
          "vendorCurrency": "GBP",
          "clientTechnicalServiceFee": 0,
          "auxBaggageElement": {
            "piece": 1,
            "weight": 23,
            "isAllWeight": true
          },
          "offerId": null,
          "ancillaryCode": "SCI_BAG_1PC_23KG"
        },
        {
          "segmentIndex": 2,
          "endSegmentIndex": null,
          "productCode": "SCI_BAG_1PC_23KG",
          "productName": "StandardCheckInBaggage",
          "productType": 1,
          "canPurchaseWithTicket": 1,
          "canPurchasePostTicket": 1,
          "price": 52.76,
          "currency": "USD",
          "vendorPrice": 48.49,
          "vendorCurrency": "EUR",
          "clientTechnicalServiceFee": 0,
          "auxBaggageElement": {
            "piece": 1,
            "weight": 23,
            "isAllWeight": true
          },
          "offerId": null,
          "ancillaryCode": "SCI_BAG_1PC_23KG"
        }
      ]
```
{% endtab %}
{% endtabs %}
