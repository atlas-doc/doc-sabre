# Search Ancillary

### Dependency

No preceding function needs to be carried out.
The order should be ticketed and the departure date should be in the future.

### Endpoint {% debug uid="searchAncillary_1.0" %}{% enddebug %}


[https://sandbox.atriptech.com/postBookingAncillarySearch.do](https://sandbox.atriptech.com/postBookingAncillarySearch.do)

{% hint style="info" %}
Please note the below "Rules & Restrictions" while initiating a post-ticketing transaction.

1. **Single Booking Limit:** Check-in baggage and Carry-on baggage can be added to the segment of passenger either in-booking or post-booking phase altogether or separately, but each type of baggage can only be added one time for the given segment throughout the whole flow. This rule aims to simplify the baggage booking flow for customers by sending the query only one time to book multiple baggages.

2. **Product Code:** "Product code" contains various baggage offerings in aspects of baggage pieces and weights for each airline.

3. **Restrictions for Infants:** Baggage ancillary is not allowed to be booked for infant passenger.

4. ** Post-Booking Baggage Additions:**
   It is not allowed to add the same type of post-booking baggage to a ticketed order the second time unless the first purchase fails in payment. Please refer to the below scenarios:

	a. When the post-booking order is in "ticket-in-process" and "ticketed" status, it's not allowed to order another one. If any query is called, API will respond with an error message.

	b. When the post-booking order is in "cancelled" status, the customer can create another order.

	c. When the post-booking order is in "unpaid" status, the customer can create another order. However, if one of the orders completes the payment and moves to "ticketing-in-process" status, the other orders will stop processing the payment.

5. **Existing Baggage Policies:** In case the air ticket order already contains free baggage, it’s subject to airline’s ancillary policy whether additional baggage is allowed to be purchase either at the booking flow or the post-booking flow.

6. **Consistent Product Codes in Connecting Flights:** Same “product code” for baggage is mandatory to be added to each segment in connecting flights. If the "product code" is different for each of the segment (in the same direction)  or not added for all the sectors, the API will respond with an error message.

7. **Round-Trip Baggage Rule:** Rule No.6 doesn't work for round trip flights. This means that the outbound and inbound segments can have different product codes. For example, outbound journey may have a product code of 1PC and 10KG while the inbound journey may have a product code of 20KG. This is allowed.

8. **API Request Information:** The details of only the passenger for whom the ancillary needs to be added must be sent in the API RQ.
{% endhint %}

**For "Order" status, please refer to the the response of the "queryOrderDetails.do" API.**

## Request

{% tabs %}
{% tab title="Schema" %}
### **ticketOrderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the ticket order.  
- **Constraints:** Cannot be null or empty.  
- **Default:** None  
- **Example:** "TESTA20240618162411631"  

### **airlinePNR**
- **Type:** String  
- **Required:** Yes  
- **Description:** PNR code assigned by the airline.  
- **Constraints:** Cannot be null or empty.  
- **Default:** None  
- **Example:** "S74883"  

### **carrier**
- **Type:** String  
- **Required:** Yes  
- **Description:** Airline carrier code.  
- **Constraints:** Must be a valid airline code.  
- **Default:** None  
- **Example:** "MM"  

### **ancillaryCategory**
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of ancillary service requested. Different categories of ancillaries need to be separately requested. Currently we only support "BAGGAGE".
- **Constraints:** Must be a valid ancillary category (e.g., "BAGGAGE").  
- **Default:** None  
- **Example:** "BAGGAGE"  

### **displayCurrency**
- **Type:** String  
- **Required:** Yes  
- **Description:** The alternative currency in which the fare and taxes amount needs to be displayed. The 3-letter currency code should be entered.
- **Constraints:** Must be a valid three-letter currency code (ISO 4217).  
- **Default:** None  
- **Example:** "CNY"
    
{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid": "xxxxxxxxxx",
    "ticketOrderNo": "TESTA20240618162411631",
    "airlinePNR": "S74883",
    "carrier": "MM",
    "ancillaryCategory": "BAGGAGE",
    "displayCurrency": "CNY"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Status code of the response (0 indicates success).  
- **Constraints:** Must be a valid status code.  
- **Default:** None  
- **Example:** "0"  

### **msg**
- **Type:** String  
- **Required:** Yes  
- **Description:** Message indicating success or failure of the request. The 'msg' element is for the description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.
- **Constraints:** None  
- **Default:** None  
- **Example:** "success"  

### **sessionId**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique session identifier.  
- **Constraints:** Cannot be null or empty.  
- **Default:** None  
- **Example:** "90223f62-fd87-45b4-9a32-68f03f9f85c8"  

### **ticketOrderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique ticket order number.  
- **Constraints:** Cannot be null or empty.  
- **Default:** None  
- **Example:** "TESTA20240618162411631"  

### **supportCreditTransPayment**
- **Type:** String  
- **Required:** Yes  
- **Description:** Indicates if credit transaction payment is supported (0 for no, 1 for yes).  

  Valid values:

  0: The credit card details will not be passed through and only pre-payment is allowed.

  1: The API will allow you to pass through client’s credit card details for payment. The customer can also use pre-payment as a method of payment.
- **Constraints:** Must be 0 or 1.  
- **Default:** "0"  
- **Example:** "0"  

### **currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency code for the transaction.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** "USD"  

## Flight Segment Fields

### **segmentIndex**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Index of the flight segment.  
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** "1"  

### **carrier**
- **Type:** String  
- **Required:** Yes  
- **Description:** Airline carrier code.  
- **Constraints:** Must be a valid airline code.  
- **Default:** None  
- **Example:** "5F"  

### **flightNumber**
- **Type:** String  
- **Required:** Yes  
- **Description:** Flight number assigned by the carrier.  
- **Constraints:** Cannot be null or empty.  
- **Default:** None  
- **Example:** "5F617"  

### **depAirport**
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure airport IATA code.  
- **Constraints:** Must be a valid IATA airport code.  
- **Default:** None  
- **Example:** "RMO"  

### **depTime**
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure time of the flight.  
- **Constraints:** Format: YYYYMMDDHHMM.  
- **Default:** None  
- **Example:** "202408200810"  

### **arrAirport**
- **Type:** String  
- **Required:** Yes  
- **Description:** Arrival airport IATA code.  
- **Constraints:** Must be a valid IATA airport code.  
- **Default:** None  
- **Example:** "LTN"  

### **arrTime**
- **Type:** String  
- **Required:** Yes  
- **Description:** Arrival time of the flight.  
- **Constraints:** Format: YYYYMMDDHHMM.  
- **Default:** None  
- **Example:** "202408200940"  

### **stopCities**
- **Type:** String  
- **Required:** No  
- **Description:** List of stopover cities if applicable.  
- **Constraints:** Can be empty if no stopovers.  
- **Default:** ""  
- **Example:** ""  

### **duration**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Flight duration in minutes.  
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** "210"  

### **codeShare**
- **Type:** Boolean  
- **Required:** Yes  
- **Description:** Indicates if the flight is operated under a codeshare agreement.  
- **Constraints:** Must be true or false.  
- **Default:** false  
- **Example:** false  

### **cabin**
- **Type:** String  
- **Required:** No  
- **Description:** Cabin class of the flight segment.  
- **Constraints:** Can be empty if not specified.  
- **Default:** ""  
- **Example:** ""  

### **cabinClass**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Numeric representation of cabin class (e.g., 1 for economy, 2 for business).  

  Valid values:

  1 : Economy

  2 : Business

  3 : First Class

  4: Premium Economy
- **Constraints:** Must be a valid class indicator.  
- **Default:** None  
- **Example:** "1"  

### **seatCount**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of available seats on the flight segment.  
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** "4"  

### **aircraftCode**
- **Type:** String  
- **Required:** No  
- **Description:** Aircraft model code if available.  
- **Constraints:** Can be empty if not specified.  
- **Default:** ""  
- **Example:** ""  

### **depTerminal**
- **Type:** String  
- **Required:** No  
- **Description:** Departure terminal of the airport.  
- **Constraints:** Can be empty if not specified.  
- **Default:** ""  
- **Example:** ""  

### **arrTerminal**
- **Type:** String  
- **Required:** No  
- **Description:** Arrival terminal of the airport.  
- **Constraints:** Can be empty if not specified.  
- **Default:** ""  
- **Example:** ""  

### **operatingCarrier**
- **Type:** String  
- **Required:** No  
- **Description:** Carrier actually operating the flight if different from the marketing carrier.  
- **Constraints:** Can be empty if not specified.  
- **Default:** None  
- **Example:** "5F"  

### **operatingFlightnumber**
- **Type:** String  
- **Required:** No  
- **Description:** Flight number assigned by the operating carrier.  
- **Constraints:** Can be empty if not specified.  
- **Default:** ""  
- **Example:** ""  

### **fareFamily**
- **Type:** String  
- **Required:** Yes  
- **Description:** Fare family category of the ticket.  
- **Constraints:** Cannot be null or empty.  
- **Default:** None  
- **Example:** "LOYAL"  

## Ancillary Product Fields

### **segmentIndex**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Index of the flight segment to which this product applies.  
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** "1"  

### **endSegmentIndex**
- **Type:** Integer | Null  
- **Required:** No  
- **Description:** Index of the last segment if applicable.  
- **Constraints:** Can be null if not applicable.  
- **Default:** Null  
- **Example:** null  

### **productCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Code identifying the ancillary product.  
- **Constraints:** Cannot be null or empty.  
- **Default:** None  
- **Example:** "SCI_BAG_1PC_10KG"  

### **productName**
- **Type:** String  
- **Required:** Yes  
- **Description:** Name of the ancillary product.  

  Valid values:

  StandardCheckInBaggage

  CabinBaggageOverheadLocker
- **Constraints:** Cannot be null or empty.  
- **Default:** None  
- **Example:** "Standard Check-in Baggage"  

### **productType**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Type of ancillary product.  

  Valid values:

  1: Standard Check-in baggage

  3: Cabin Baggage Overhead Locker

  6: Seat

  Currently only "Standard Check-in Baggage" and "Cabin Baggage Overhead Locker" are available.
- **Constraints:** Must be a valid product type identifier.  
- **Default:** None  
- **Example:** "1"  

### **canPurchaseWithTicket**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Indicates if the product can be purchased with the ticket (0 for no, 1 for yes).  
- **Constraints:** Must be 0 or 1.  
- **Default:** "0"  
- **Example:** "0"  

### **canPurchasePostTicket**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Indicates if the product can be purchased after ticket issuance (0 for no, 1 for yes).  
- **Constraints:** Must be 0 or 1.  
- **Default:** "1"  
- **Example:** "1"  

### **price**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Price of the product in the base currency.  
- **Constraints:** Must be a positive number.  
- **Default:** None  
- **Example:** "22.88"  

### **currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency of the product price.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** "USD"  

### **vendorPrice**
- **Type:** Number | Null  
- **Required:** No  
- **Description:** Vendor-specific price if available.  
- **Constraints:** Can be null if not applicable.  
- **Default:** Null  
- **Example:** null  

### **vendorCurrency**
- **Type:** String | Null  
- **Required:** No  
- **Description:** Vendor-specific currency if available.  
- **Constraints:** Can be null if not applicable.  
- **Default:** Null  
- **Example:** null  

### **clientTechnicalServiceFee**
- **Type:** Number  
- **Required:** No  
- **Description:** Additional service fee charged to the client.  
- **Constraints:** Must be a non-negative number.  
- **Default:** "0.00"  
- **Example:** "0.00"  

### **clientTechnicalServiceFeeMode**
- **Type:** String  
- **Required:** No  
- **Description:** Mode of applying service fee (e.g., PER_PAX).  

  Valid values:

  PER_SEGMENT: Each segment of an itinerary (per passenger)

  PER_TICKET: No. of tickets in a booking

  PER_PAX: Per passenger

  PER_BOOKING: Per atlas booking (order #)
- **Constraints:** Can be empty if not applicable.  
- **Default:** "PER_PAX"  
- **Example:** "PER_PAX"  

### **auxBaggageElement** (Nested Object)
- **Type:** Object  
- **Required:** No  
- **Description:** Additional details if the product is baggage-related.  
- **Constraints:** Can be null if not applicable.  
- **Default:** None  
- **Example:** See below.  

#### **Baggage Element Fields**
- **piece**  
  - **Type:** Integer  
  - **Required:** Yes  
  - **Description:** Number of baggage pieces.  

  Valid values:

  0：No Limitation about piece;

  greater than 0：Maximum pieces
  - **Constraints:** Must be a positive integer.  
  - **Default:** None  
  - **Example:** "1"  

- **weight**  
  - **Type:** Integer  
  - **Required:** Yes  
  - **Description:** Weight of baggage in kilograms.  
  - **Constraints:** Must be a positive number.  
  - **Default:** None  
  - **Example:** "10"  

- **isAllWeight**  
  - **Type:** Boolean  
  - **Required:** Yes  
  - **Description:** Indicates if the weight is cumulative.  

  Valid values:

  True: The weight is for all the pieces

  False: The weight is for each piece
  - **Constraints:** Must be true or false.  
  - **Default:** true  
  - **Example:** true  

- **size**  
  - **Type:** String  
  - **Required:** No  
  - **Description:** Dimensions of baggage if applicable.  
  - **Constraints:** Can be empty if not specified.  
  - **Default:** ""  
  - **Example:** ""  

### **offerId**
- **Type:** String | Null  
- **Required:** No  
- **Description:** Unique identifier for the offer. This will be "null" in the booking flow but will have an id in the post-ticketing flow.
- **Constraints:** Can be null if not applicable.  
- **Default:** Null  
- **Example:** null  

### **categoryCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Category of the ancillary product.  
- **Constraints:** Cannot be null or empty.  
- **Default:** None  
- **Example:** "StandardCheckInBaggage"  

### **ancillaryCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Code representing the ancillary product. This will be identical to the "product code". 
- **Constraints:** Cannot be null or empty.  
- **Default:** None  
- **Example:** "SCI_BAG_1PC_10KG"  

### **auxSeatElement**
- **Type:** Object | Null  
- **Required:** No  
- **Description:** Additional details if the product is related to seat selection.  
- **Constraints:** Can be null if not applicable.  
- **Default:** Null  
- **Example:** null  

### **displayPrice**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Price of the product in the display currency.  
- **Constraints:** Must be a positive number.  
- **Default:** None  
- **Example:** "165.89"  

### **displayCurrency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Display currency of the price.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** "CNY"  




{% endtab %}

{% tab title="Samples" %}
```json
{
    "status": 0,
    "msg": "success",
    "sessionId": "90223f62-fd87-45b4-9a32-68f03f9f85c8",
    "ticketOrderNo": "TESTA20240618162411631",
    "supportCreditTransPayment": "0",
    "currency": "USD",
    "fromSegments": [
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
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_1PC_10KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 22.88,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 46.20,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 34.54,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 74.58,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 49.81,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 124.11,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 105.16,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "displayPrice": 762.70,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_3PC_60KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 132.01,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 184.19,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "displayPrice": 1335.90,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "COL_BAG_1PC_10KG",
            "productName": "Cabin Baggage Overhead Lock",
            "productType": 3,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 22.71,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 43.48,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 39.93,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 44.09,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 89.28,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 81.05,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 141.74,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 138.97,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "displayPrice": 1007.90,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_3PC_60KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 98.49,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "displayPrice": 714.30,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_3PC_90KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 272.31,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 22.04,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
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


