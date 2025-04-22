# Retrieve Booking

### Dependency

`Order` function should be called in prior to this call.

### Endpoint {% debug uid="queryOrderDetails_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/queryOrderDetails.do](https://sandbox.atriptech.com/queryOrderDetails.do)

{% hint style="info" %}
Please refer to the below information for the usage of the queryOrderDetails.do API.

1. All the parameters can be used together, if required.

2. “OrderNo” is “required” if “airlinePNR” and “carrier” cannot be provided upon calling the API. Inversely, “airlinePNR” and “carrier” are “required” if “OrderNo” cannot be provided. All remaining fields in the request are optional.

3. The PNR (Passenger Name Record) for an airline ticket order or a luggage purchase order must be kept consistent, as per airline regulations.

4. The input parameters orderNo, airlinePNR, carrier, and other optional fields will be validated together to ensure they belong to the same order data source. If any of these input parameters do not match with others, the API will return an error.

5. Airline ticket orders and associated post-booking ancillary orders can be retrieved using the following methods: (airline ticket orders + post-booking ancillary orders):
    - orderNo
    - airlinePNR + carrier
    - orderNo + airlinePNR + carrier
    - orderNo + airlinePNR + carrier + other optional parameters

6. In case the parameters of “airlinePNR” and “carrier” cannot identify an unique order (e.g BC - PNR is made up with 4 number), customer needs to enter additional parameters such as "name" for identification. In such scenarios, API will respond with error msg ”Multi-orderNos are identified, please request again with extra parameters added.”

{% endhint %}


## Request

{% tabs %}
{% tab title="Schema" %}

### **orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the flight booking order. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.  
- **Default:** None  
- **Example:** "TESTA20240627114717735"  

### **pnrCode**
- **Type:** String  
- **Required:** No  
- **Description:** The pnrCode is the single reference for the booking. This is the Atlas PNR.
- **Default:** None  
- **Example:** "XYZ87T"  

### **airlinePNR**
- **Type:** String  
- **Required:** No  
- **Description:** The record locator of the airline.
- **Default:** None  
- **Example:** "S75666"  

### **carrier**
- **Type:** String  
- **Required:** No  
- **Description:** Airline carrier code.  
- **Default:** None  
- **Example:** "G9"  

### **passengers** (Array)
- **Type:** Array  
- **Required:** No  
- **Description:** List of passengers included in the booking.  
- **Default:** None  
- **Example:** [{...}]  

#### **passengers.name**
- **Type:** String  
- **Required:** No  
- **Description:** Full name of the passenger. Must be in "LastName/FirstName MiddleName" format.  
- **Default:** None  
- **Example:** "Kotwal/Behram"  

### **routing** (Object)
- **Type:** Object  
- **Required:** No  
- **Description:** Contains segment details of the booked flight.  
- **Default:** None  
- **Example:** {...}  

#### **routing.fromSegments** (Array)
- **Type:** Array  
- **Required:** No  
- **Description:** List of departure segments.  
- **Default:** None  
- **Example:** [{...}]  

##### **fromSegments.segmentIndex**
- **Type:** Integer  
- **Required:** No  
- **Description:** Index of the segment in the route.  
- **Default:** None  
- **Example:** 1  

##### **fromSegments.carrier**
- **Type:** String  
- **Required:** No  
- **Description:** Airline carrier code for the segment.  
- **Default:** None  
- **Example:** "G9"  

##### **fromSegments.flightNumber**
- **Type:** String  
- **Required:** No  
- **Description:** Flight number of the segment.  
- **Default:** None  
- **Example:** "G9147"  

##### **fromSegments.depAirport**
- **Type:** String  
- **Required:** No  
- **Description:** Departure airport code.  
- **Default:** None  
- **Example:** "SHJ"  

##### **fromSegments.arrAirport**
- **Type:** String  
- **Required:** No  
- **Description:** Arrival airport code.  
- **Default:** None  
- **Example:** "JED"  

##### **fromSegments.fromDate**
- **Type:** String  
- **Required:** No  
- **Description:** Flight departure date in YYYYMMDD format.  
- **Default:** None  
- **Example:** "20240716"  

### **isCompletedOrder**
- **Type:** Boolean  
- **Required:** Yes  
- **Description:** Indicates if the order is completed.
  
  Valid values:
  - true: Show the full details of main order and post-booking order
  - false: Only show the details of given order
- **Default:** "false"  
- **Example:** "true"  

{% endtab %}

{% tab title="Samples" %}
```json
{
    "orderNo": "TESTA20240627114717735",
    "pnrCode": "XYZ87T",
    "airlinePNR": "S75666",
    "carrier": "G9",
    "passengers": [
        {
            "name": "Kotwal/Behram"
        }
    ],
    "routing": {
        "fromSegments": [
            {
                "segmentIndex": 1,
                "carrier": "G9",
                "flightNumber": "G9147",
                "depAirport": "SHJ",
                "arrAirport": "JED",
                "fromDate": "20240716"
            }
        ]
    },
    "isCompletedOrder": "true"
}       
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
### **orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the flight booking order. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.  
- **Default:** None  
- **Example:** "TESTA20240627114717735" 

### **orderList** (Array)
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of all orders associated with the booking.  
- **Default:** None  
- **Example:** [{...}]  

#### **orderList.orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Order number for the booking.  
- **Default:** None  
- **Example:** "TESTA20240627114717735"  

#### **orderList.orderStatus**
- **Type:** String  
- **Required:** Yes  
- **Description:** Status of the order.
  
  Valid values:
  - 0: Unpaid
  - 1: Ticketing-in-Process
  - 2: Ticketed
  - -3: Cancelled(When the booking is failed due to the request information) Order number
- **Default:** None  
- **Example:** "2"  

#### **orderList.ticketStatus**
- **Type:** String  
- **Required:** Yes  
- **Description:** Status of ticket issuance.
  
  Valid values:
  - 0: Ticket not issued
  - 1: Ticket issued  
- **Default:** None  
- **Example:** "1"  

#### **orderList.totalPrice**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Total fare of this order in the currency Atlas settled with you.  
- **Default:** None  
- **Example:** 86.31  

#### **orderList.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** The currency Atlas settled with you.  
- **Default:** "USD"  
- **Example:** "USD"  

#### **orderList.tktLimitTime**
- **Type:** **string**  
- **Required:** Yes  
- **Description:** Ticketing deadline timestamp. Format: **yyyy-MM-dd HH:mm:ss**   
- **Default:** None  
- **Example:** **"2024-06-27 13:07:21"**

#### **orderList.vendorTotalPrice**
- **Type:** **number**  
- **Required:** Yes  
- **Description:** Total cost from the vendor including fare and tax.  
- **Default:** **0.0**  
- **Example:** **316.96**

#### **orderList.vendorCost**
- **Type:** **number**  
- **Required:** Yes  
- **Description:** Actual fare of this order in the vendor's currency. If the order does not support VCC passthrough or BYOA, this fare will not be displayed.  
- **Default:** **0.0**  
- **Example:** **312.69**

#### **orderList.vendorTotalAncillaryPrice**
- **Type:** **number**  
- **Required:** Yes  
- **Description:** Total ancillary fare of this order in the vendor's currency. 
- **Default:** **0.0**  
- **Example:** **0**

#### **orderList.vendorCurrency**
- **Type:** **string**  
- **Required:** Yes  
- **Description:** Vendor's transaction currency.  
- **Default:** **"USD"**  
- **Example:** **"AED"**

#### **orderList.adultTotalFare**
- **Type:** **number**  
- **Required:** Yes  
- **Description:** Total fare for adult passengers.  
- **Default:** **0.0**  
- **Example:** **86.31**

#### **orderList.childTotalFare**
- **Type:** **number**  
- **Required:** No  
- **Description:** Total fare for child passengers.  
- **Default:** **0.0**  
- **Example:** **86.31**

#### **orderList.infantTotalFare**
- **Type:** **number**  
- **Required:** No  
- **Description:** Total fare for infant passengers.  
- **Default:** **0.0**  
- **Example:** **153.79**

#### **orderList.totalAncillaryPrice**
- **Type:** **number**  
- **Required:** Yes  
- **Description:** Total paid by user for ancillaries.  
- **Default:** **0.0**  
- **Example:** **0**

#### **orderList.totalTransactionFee**
- **Type:** **number**  
- **Required:** Yes  
- **Description:** Platform fee added to booking.  
- **Default:** **0.0**  
- **Example:** **1**

#### **orderList.paymentFee**
- **Type:** **number | null**  
- **Required:** No  
- **Description:** Fee for selected payment method.  
- **Default:** **null**  
- **Example:** **null**

#### **orderList.supportPaymentMethod**
- **Type:** **integer**  
- **Required:** Yes  
- **Description:** Code for allowed payment method.
  
  Valid values:
  - 1: Pre-payment
  - 3: VCC
  - 5: MOR
- **Default:** **1**  
- **Example:** **3**

### **pnrCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** The pnrCode is the single reference for the booking. This is the Atlas PNR. 
- **Default:** None  
- **Example:** "ODNSPH"  

### **paxTicketInfos** (Array)
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of passenger details. This is the same format as the PAXTicketInfo in order response.
- **Default:** None  
- **Example:** [{...}]  

#### **paxTicketInfos.name**
- **Type:** String  
- **Required:** Yes  
- **Description:** Full name of the passenger. Must be in "LastName/FirstName MiddleName" format.    
- **Default:** None  
- **Example:** "Kotwal/Behram"  

#### **paxTicketInfos.passengerType**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Passenger type (0 = adult, 1 = child, 2 = infant).  
- **Default:** None  
- **Example:** 0  

### **routing** (Object)
- **Type:** Object  
- **Required:** Yes  
- **Description:** Contains segment details of the booked flight. The structure is the same format as "Routing" in order response.  
- **Default:** None  
- **Example:** {...}  

### **ancillaryProductElements** (Array)
- **Type:** Array  
- **Required:** No  
- **Description:** List of ancillary products purchased with the booking. The structure is the same format as "Ancillaries" in order response.  
- **Default:** None  
- **Example:** [{...}]  

### **airlineBookings** (Array)
- **Type:** Array  
- **Required:** No  
- **Description:** List of airline-specific booking details.  
- **Default:** None  
- **Example:** [{...}]  

#### **airlineBookings.airlineCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Two-letter airline code.  
- **Default:** None  
- **Example:** "XC"  

#### **airlineBookings.airlineName**
- **Type:** String  
- **Required:** Yes  
- **Description:** Name of the airline.  
- **Default:** None  
- **Example:** "Corendon Airlines"  

#### **airlineBookings.airlinePnr**
- **Type:** String  
- **Required:** No  
- **Description:** Passenger Name Record (PNR) issued by the airline.  
- **Default:** None  
- **Example:** "S017554"  

#### **airlineBookings.airlineWebSiteAddress**
- **Type:** String  
- **Required:** Yes  
- **Description:** Website link for airline services.  
- **Default:** None  
- **Example:** "https://www.corendon-airlines.com"  

#### **airlineBookings.mmbEmail**
- **Type:** String  
- **Required:** Yes  
- **Description:** Email address for managing the booking.  
- **Default:** None  
- **Example:** "SARABAGCI@WEB.DE"  

#### **airlineBookings.tailDigitsOfPaymentCard**
- **Type:** String  
- **Required:** No  
- **Description:** Last few digits of the payment card used for booking.  
- **Default:** Null  
- **Example:** Null  

#### **airlineBookings.extras** (Array)
- **Type:** Array  
- **Required:** No  
- **Description:** Additional airline booking details.  
- **Default:** None  
- **Example:** [{...}]  

##### **extras.name**
- **Type:** String  
- **Required:** Yes  
- **Description:** Name of the extra field.  
- **Default:** None  
- **Example:** "email"  

##### **extras.remark**
- **Type:** String  
- **Required:** Yes  
- **Description:** Additional remarks about the extra field.  
- **Default:** None  
- **Example:** "email"  

##### **extras.value**
- **Type:** String  
- **Required:** No  
- **Description:** Value assigned to the extra field.  
- **Default:** Null  
- **Example:** Null  

### **itineraryDownload**
- **Type:** String  
- **Required:** No  
- **Description:** URL to download the itinerary document.  
- **Default:** None  
- **Example:** "https://api-sg.atriptech.com/itineraryDownload.do?orderNo=8b83jgNhkaYaktdGP0fboCRs8w5cQTow"  

### **contact** (Object)
- **Type:** Object  
- **Required:** Yes  
- **Description:** Contact details for the booking.  
- **Default:** None  
- **Example:** {...}  

#### **contact.name**
- **Type:** String  
- **Required:** Yes  
- **Description:** Name of the contact person.  
- **Default:** None  
- **Example:** "KURT/ESRA"  

#### **contact.address**
- **Type:** String  
- **Required:** No  
- **Description:** Address of the contact person.  
- **Default:** Null  
- **Example:** None  

#### **contact.postcode**
- **Type:** String  
- **Required:** No  
- **Description:** Postal code of the contact person's address.  
- **Default:** Null  
- **Example:** None  

#### **contact.email**
- **Type:** String  
- **Required:** Yes  
- **Description:** Email address of the contact person.  
- **Default:** None  
- **Example:** "SAARABAGCI@WEB.DE"  

#### **contact.mobile**
- **Type:** String  
- **Required:** Yes  
- **Description:** Mobile phone number of the contact person. XXXX(digital country code)-XXXXXXXX(phone number). Examples: 0001-87291810, 0086-13928109091, 0971-19201998
- **Default:** None  
- **Example:** "0046-771407000"  

### **ancillaryBuyMethod**
- **Type:** String  
- **Required:** No  
- **Description:** Indicates the method used for purchasing ancillary services.

  Valid values:
  - 0 = pre-purchase
  - 1 = post-purchase.  
- **Default:** "0"  
- **Example:** "0"  

### **errorCode**
- **Type:** String  
- **Required:** No  
- **Description:** Error code indicating issues during booking or fare retrieval.  
- **Default:** None  
- **Example:** "601"  

### **errorMessage**
- **Type:** String  
- **Required:** No  
- **Description:** Description of the error encountered during the booking process.  
- **Default:** None  
- **Example:** "Fare changed"  

### **airlineMessage**
- **Type:** String  
- **Required:** No  
- **Description:** Airline-specific error message or code.  
- **Default:** None  
- **Example:** "301"  

### **paymentOptions**
- **Type:** Array of Objects  
- **Required:** Yes  
- **Description:** A list of payment method options, including details of service fees and ticket fares per method.  
- **Default:** None  
- **Example:**
  ```json
  [
    {
      "paymentMethod": 3,
      "serviceFee": {
        "amount": 10.00,
        "currency": "USD",
        "deductFrom": "DEPOSIT"
      },
      "ticketFare": {
        "amount": 123744.40,
        "currency": "KRW",
        "deductFrom": "CARD"
      },
      "paymentFee": null
    }
  ]
  ```

### **paymentOptions[].paymentMethod**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Method of payment selected by the user.  

  Valid values:
  - 1 = Deposit
  - 3 = VCC Passthrough
  - 5 = MoR
- **Default:** Deposit  
- **Example:** `3`  

### **paymentOptions[].serviceFee**
- **Type:** Object  
- **Required:** No  
- **Description:** Service fee details for this payment method.  
- **Default:** `null`  
- **Example:**
  ```json
  {
    "amount": 10.00,
    "currency": "USD",
    "deductFrom": "DEPOSIT"
  }
  ```
#### **paymentOptions[].serviceFee.amount**
- **Type:** Number (Float)  
- **Required:** Yes  
- **Description:** Amount of the service fee.  
- **Default:** `0.00`  
- **Example:** `10.00`

#### **paymentOptions[].serviceFee.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency in which the service fee is charged.  
- **Default:** None  
- **Example:** `"USD"`

#### **paymentOptions[].serviceFee.deductFrom**
- **Type:** String  
- **Required:** Yes  
- **Description:** Indicates the account source for fee deduction.  

  Valid values:
  - DEPOSIT = Deduct from pre-funded deposit  
  - CARD = Deduct from credit/debit card  
- **Default:** `"CARD"`  
- **Example:** `"DEPOSIT"`

### **paymentOptions[].ticketFare**
- **Type:** Object  
- **Required:** Yes  
- **Description:** Fare details for the ticket paid under the selected method.  
- **Default:** None  
- **Example:**
  ```json
  {
    "amount": 123744.40,
    "currency": "KRW",
    "deductFrom": "CARD"
  }
  ```

#### **paymentOptions[].ticketFare.amount**
- **Type:** Number (Float)  
- **Required:** Yes  
- **Description:** The fare amount for the ticket.  
- **Default:** None  
- **Example:** `123744.40`

#### **paymentOptions[].ticketFare.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency of the ticket fare.  
- **Default:** None  
- **Example:** `"KRW"`

#### **paymentOptions[].ticketFare.deductFrom**
- **Type:** String  
- **Required:** Yes  
- **Description:** Indicates where the fare amount is deducted from.  

  Valid values:
  - DEPOSIT = Deduct from pre-funded deposit  
  - CARD = Deduct from credit/debit card  
- **Default:** `"CARD"`  
- **Example:** `"CARD"`

### **paymentFee**
- **Type:** Object  
- **Required:** No  
- **Description:** Additional fee charged for using a specific payment method. Typically includes service/processing charges applied at checkout.  
- **Default:** `null`  
- **Example:**
  ```json
  {
    "amount": 4.03,
    "currency": "USD",
    "deductFrom": "CARD",
    "displayAmount": 3.73
  }
  ```

### **paymentFee.amount**
- **Type:** Number (Float)  
- **Required:** Yes  
- **Description:** Actual fee amount charged for the selected payment method.  
- **Default:** `0.00`  
- **Example:** `4.03`

### **paymentFee.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency in which the fee is charged.  
- **Default:** Follows system or booking currency.  
- **Example:** `"USD"`

### **paymentFee.deductFrom**
- **Type:** String  
- **Required:** Yes  
- **Description:** Indicates the source from which the fee will be deducted.  

  Valid values:
  - DEPOSIT = Deduct from pre-funded deposit  
  - CARD = Deduct from credit/debit card  
- **Default:** `"CARD"`  
- **Example:** `"CARD"`

### **paymentFee.displayAmount**
- **Type:** Number 
- **Required:** Yes  
- **Description:** Display amount in the user-selected display currency (e.g., converted from system currency).  
- **Default:** Matches `amount` if no conversion applied  
- **Example:** `3.73`

### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Response status code. 

  Valid values:
  - 0: success
  - 2: System error 
- **Default:** 0  
- **Example:** 0  

### **msg**
- **Type:** String  
- **Required:** Yes  
- **Description:** Response message. The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.
- **Default:** "success"  
- **Example:** "success"  
       
{% endtab %}

{% tab title="Samples" %}
```
{
  "orderNo": "TESTA20240627114717735",
  "orderList": [
    {
      "orderNo": "TESTA20240627114717735",
      "orderStatus": "2",
      "ticketStatus": "1",
      "totalPrice": 86.31,
      "currency": "USD",
      "tktLimitTime": "2024-06-27 13:07:21",
      "vendorTotalPrice": 316.96,
      "vendorCost": 312.69,
      "vendorTotalAncillaryPrice": 0,
      "vendorCurrency": "AED",
      "adultTotalFare": 86.31,
      "childTotalFare": 86.31,
      "infantTotalFare": 153.79,
      "totalAncillaryPrice": 0,
      "totalTransactionFee": 1,
      "paymentFee": null,
      "supportPaymentMethod": 3
    },
    {
      "orderNo": "TESTB20240627120309525",
      "orderStatus": "0",
      "ticketStatus": "0",
      "totalPrice": 174.27,
      "currency": "USD",
      "tktLimitTime": "2024-06-27 12:19:10",
      "vendorTotalPrice": 640,
      "vendorCost": 312.69,
      "vendorTotalAncillaryPrice": 640,
      "vendorCurrency": "AED",
      "adultTotalFare": 0,
      "childTotalFare": null,
      "infantTotalFare": null,
      "totalAncillaryPrice": 174.27,
      "totalTransactionFee": 0,
      "paymentFee": null,
      "supportPaymentMethod": 1
    }
  ],
  "pnrCode": "ODNSPH",
  "orderStatus": null,
  "ticketStatus": null,
  "paxTicketInfos": [
    {
      "name": "Kotwal/Behram",
      "passengerType": 0,
      "birthday": "19890922",
      "gender": "M",
      "cardNum": "00000011",
      "cardType": "PP",
      "cardIssuePlace": "SG",
      "cardExpired": "20301230",
      "nationality": "LK",
      "ticketNos": [
        "S75666"
      ],
      "airlinePNRs": [
        "S75666"
      ],
      "contactEmails": [
        "TEST@GMAIL.COM"
      ],
      "contactPhones": [
        "0086-13928109091"
      ],
      "ancillaries": [
        {
          "productCode": "SCI_SEAT_B2_F9_PHL_LAS",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 63.8,
          "currency": "USD",
          "vendorPrice": 63.8,
          "vendorCurrency": "USD",
          "productType": null,
          "auxBaggageElement": null,
          "auxSeatElement": {
            "row": "2",
            "column": "B"
          }
        },
        {
          "productCode": "SCI_SEAT_A27_F9_LAS_ORD",
          "segmentIndex": 2,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 49.24,
          "currency": "USD",
          "vendorPrice": 49.24,
          "vendorCurrency": "USD",
          "productType": null,
          "auxBaggageElement": null,
          "auxSeatElement": {
            "row": "27",
            "column": "A"
          }
        },
        {
          "productCode": "SCI_2PC_52KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 174.27,
          "currency": "USD",
          "vendorPrice": 640,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_2PC_52KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 174.27,
          "currency": "USD",
          "vendorPrice": 640,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_2PC_52KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 174.27,
          "currency": "USD",
          "vendorPrice": 640,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_2PC_52KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 174.27,
          "currency": "USD",
          "vendorPrice": 640,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_2PC_52KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 174.27,
          "currency": "USD",
          "vendorPrice": 640,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_17KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 109.74,
          "currency": "USD",
          "vendorPrice": 403,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_17KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 109.74,
          "currency": "USD",
          "vendorPrice": 403,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_17KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 109.74,
          "currency": "USD",
          "vendorPrice": 403,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_17KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 109.74,
          "currency": "USD",
          "vendorPrice": 403,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_17KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 109.74,
          "currency": "USD",
          "vendorPrice": 403,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_17KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 109.74,
          "currency": "USD",
          "vendorPrice": 403,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_17KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 109.74,
          "currency": "USD",
          "vendorPrice": 403,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_22KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 50.11,
          "currency": "USD",
          "vendorPrice": 184,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_22KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 50.11,
          "currency": "USD",
          "vendorPrice": 184,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_22KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 50.11,
          "currency": "USD",
          "vendorPrice": 184,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_22KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 50.11,
          "currency": "USD",
          "vendorPrice": 184,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_22KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 50.11,
          "currency": "USD",
          "vendorPrice": 184,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_22KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 50.11,
          "currency": "USD",
          "vendorPrice": 184,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_22KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 50.11,
          "currency": "USD",
          "vendorPrice": 184,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_22KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 50.11,
          "currency": "USD",
          "vendorPrice": 184,
          "vendorCurrency": "AED"
        }
      ]
    }
  ],
  "totalPrice": 2126.72,
  "currency": "USD",
  "tktLimitTime": null,
  "vendorTotalPrice": null,
  "vendorTotalAncillaryPrice": null,
  "vendorCurrency": null,
  "adultTotalFare": null,
  "childTotalFare": null,
  "infantTotalFare": null,
  "totalAncillaryPrice": null,
  "totalTransactionFee": null,
  "paymentFee": null,
  "supportPaymentMethod": 0,
  "supportPaymentMethods": null,
  "paymentMethod": null,
  "routing": {
    "fid": "lyuXAz1MVngismacM3wuiwJtmFMsLpRTfm0K2S99dsxi-G5TKL1BQQ..",
    "routingIdentifier": "aLLgQXmljm5IEm4F2B7GwEeO9d1gEcWId1SPa2qQU/Exzrmp46qTnP1Bf8nnsQGPliUgxaZGnRxPBBjFHiIgMWXmfDNoWMGlSBAzSStrZYrR/1H8sZENAaLkHq7StdgtFnCqK5m26fQhrveoISCbmz7ZAsfQcCDlbofv55bj9l6/mtrrU77wm6+6J5IB8vVHEHelUNgWevC0TCz2rsfF/wT88pb2eHTQlNmhNqBiXAjDiX47D2mSWlhB0LYI3ocs6P0jM9lV4hVrt+xXjNBBMYqAiG3TPWx6QfeTBjgt1+IwfYdzurVeKVFL3OSZMV2ZywXRwCf8qQtJX8OEUh9CzKFYopbYAwkGfOPJc9sd07lubzPS1rZmyg==",
    "supportCreditTransPayment": "1",
    "currency": "USD",
    "adultPrice": 65.93,
    "adultTax": 20.38,
    "childPrice": 65.93,
    "childTax": 20.38,
    "infantPrice": 153.79,
    "infantTax": 0,
    "infantAllowed": true,
    "transactionFeePerPax": 1,
    "transactionFee": 1,
    "transactionFeeMode": "PER_PAX",
    "nationalityType": 0,
    "nationality": "",
    "suitAge": "",
    "PaxType": "ADT",
    "fromSegments": [
      {
        "segmentIndex": 1,
        "carrier": "G9",
        "flightNumber": "G9147",
        "depAirport": "SHJ",
        "depTime": "202407161400",
        "arrAirport": "JED",
        "arrTime": "202407161550",
        "stopCities": "",
        "duration": 170,
        "codeShare": false,
        "cabin": "",
        "cabinClass": 1,
        "seatCount": 2,
        "aircraftCode": "",
        "depTerminal": "",
        "arrTerminal": "",
        "operatingCarrier": "G9",
        "operatingFlightnumber": "",
        "fareFamily": "lowest"
      }
    ],
    "retSegments": [],
    "combineIndexs": [],
    "rule": {
      "hasBaggage": 1,
      "baggageElements": [
        {
          "segmentNo": 1,
          "baggageType": "CabinBaggageOverheadLocker",
          "passengerType": 0,
          "baggagePiece": 1,
          "baggageWeight": 10,
          "baggageSize": null
        }
      ],
      "refundRules": [
        {
          "refundType": 0,
          "refundStatus": "T",
          "refundFee": 0,
          "currency": "AED",
          "refNoshow": "T",
          "refNoShowCondition": 0,
          "refNoshowFee": 0,
          "ruleDetailList": [
            {
              "ruleId": 31233,
              "status": "T",
              "startMinute": 525600,
              "endMinute": 4320,
              "amount": 0,
              "currency": "AED"
            },
            {
              "ruleId": 31235,
              "status": "T",
              "startMinute": 4320,
              "endMinute": 1440,
              "amount": 0,
              "currency": "AED"
            },
            {
              "ruleId": 31237,
              "status": "T",
              "startMinute": 1440,
              "endMinute": 0,
              "amount": 0,
              "currency": "AED"
            },
            {
              "ruleId": 31243,
              "status": "T",
              "startMinute": 0,
              "endMinute": -525600,
              "amount": 0,
              "currency": "AED"
            }
          ]
        }
      ],
      "changesRules": [
        {
          "changesType": 0,
          "changesStatus": "T",
          "changesFee": 0,
          "currency": "AED",
          "revNoshow": "T",
          "revNoShowCondition": 0,
          "revNoshowFee": 0,
          "ruleDetailList": [
            {
              "ruleId": 20046,
              "status": "H",
              "startMinute": 525600,
              "endMinute": 4320,
              "amount": 200,
              "currency": "AED"
            },
            {
              "ruleId": 20048,
              "status": "H",
              "startMinute": 4320,
              "endMinute": 1440,
              "amount": 200,
              "currency": "AED"
            },
            {
              "ruleId": 20050,
              "status": "T",
              "startMinute": 1440,
              "endMinute": 0,
              "amount": 0,
              "currency": "AED"
            },
            {
              "ruleId": 20056,
              "status": "T",
              "startMinute": 0,
              "endMinute": -525600,
              "amount": 0,
              "currency": "AED"
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
        "productCode": "SCI_1PC_20KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 7.33,
        "currency": "USD",
        "vendorPrice": 26.89,
        "vendorCurrency": "AED",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 20,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_1PC_20KG",
        "auxSeatElement": null,
        "displayPrice": null,
        "displayCurrency": null
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_2PC_30KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 27.03,
        "currency": "USD",
        "vendorPrice": 99.24,
        "vendorCurrency": "AED",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 2,
          "weight": 30,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_2PC_30KG",
        "auxSeatElement": null,
        "displayPrice": null,
        "displayCurrency": null
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_2PC_40KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 36.94,
        "currency": "USD",
        "vendorPrice": 135.63,
        "vendorCurrency": "AED",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 2,
          "weight": 40,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_2PC_40KG",
        "auxSeatElement": null,
        "displayPrice": null,
        "displayCurrency": null
      }
    ],
    "vendorFare": {
      "vendorAdultPrice": 242.1,
      "vendorAdultTax": 74.86,
      "vendorChildPrice": 242.1,
      "vendorChildTax": 74.86,
      "vendorInfantPrice": 564.78,
      "vendorInfantTax": 0,
      "vendorCurrency": "AED"
    },
    "bundleOptions": [],
    "links": null,
    "separateBookings": false,
    "refreshTime": null,
    "displayFare": null
  },
  "airlineBookings": [
    {
      "airlineCode": "G9",
      "airlineName": "Air Arabia",
      "airlinePnr": "S75666",
      "airlineWebSiteAddress": "https://www.airarabia.com",
      "mmbEmail": "TEST@GMAIL.COM",
      "tailDigitsOfPaymentCard": null,
      "extras": [
        {
          "name": "email",
          "remark": "email",
          "value": "TEST@GMAIL.COM"
        }
      ]
    }
  ],
  "itineraryDownload": "http://121.40.236.223:8081/itineraryDownload.do?orderNo=FKEm34znpwyGDFss5iwdXC7TNqd8iZaO",
  "contact": {
    "name": "TEST",
    "address": "A-3 NOIDA",
    "postcode": "201307",
    "email": "TEST@GMAIL.COM",
    "mobile": "0086-13928109091"
  },
  "ancillaryBuyMethod": null,
  "errorCode": "601",
  "errorMessage": "Fare changed",
  "airlineMessage": "301",
  "locale": "",
  "paymentOptions": [
    {
      "paymentMethod": 5,
      "serviceFee": {
        "amount": 10.00,
        "currency": "USD",
        "deductFrom": "DEPOSIT"
      },
      "ticketFare": {
        "amount": 84.46,
        "currency": "USD",
        "deductFrom": "CARD"
      },
      "paymentFee": {
        "amount": 4.03,
        "currency": "USD",
        "deductFrom": "CARD",
        "displayAmount": 3.73
      }
    }
  ],
  "status": 0,
  "msg": "success"
}
```
{% endtab %}
{% endtabs %}
