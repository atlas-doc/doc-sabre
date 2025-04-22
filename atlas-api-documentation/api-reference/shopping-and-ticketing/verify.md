# Verify

### Dependency

The `search` function should be called prior to this call.

### Endpoint {% debug uid="verify_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/verify.do](https://sandbox.atriptech.com/verify.do)

{% hint style="info" %}

* When there is no price change, the "original" and the "new" price and tax will always be the same.
* When there is price change, there will be some difference between the "original" and the "new" price and tax.
* If paymentMethod in the request is 5（MoR）the MoR currency will be returned and amount in “VendorFare” and it’s paymentFee in cardChargeList. The paymentFee amount will not be added to the “VendorFare”.
* If paymentMethod in the request is 3（VCC Passthrough）the VCC Passthrough currency will be returned and amount in “VendorFare” and it’s paymentFee in cardChargeList (if any). The paymentFee amount will be added to the “VendorFare”.

{% endhint %}

### Request

{% tabs %}
{% tab title="Schema" %}

## **routingIdentifier**
- **Type:** String  
- **Required:** Yes  
- **Description:** Encrypted identifier representing the routing details.  
- **Default:** None  
- **Example:** "EXsU8XSpfLYTSaQTVCjrJMJvG/...TthTQ=="  

## **realtimeLuggage**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Whether to request realtime luggage price.

  Valid values:
  - 0: False
  - 1: True
  - Default: 0
- **Default:** 0  
- **Example:** 1  

## **paymentMethod**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Method of payment selected by the user.  

  Valid values:
  - 1 = Deposit
  - 3 = VCC Passthrough
  - 5 = MoR
- **Default:** Deposit  
- **Example:** `3`  

## **maxResponseTime**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** MThe maximum response time for the API, in milliseconds. The API will return an accurate quote within this duration. If the processing exceeds this duration, the system will return a standard quote directly. 
- **Default:** 15000  
- **Example:** 5000

{% endtab %}

{% tab title="Samples" %}
```
{
    "routingIdentifier": "Q0VCX01OTF8xXzIwMjUwNTE2X18xXzBfMHx0dHh6cDYyNDA1fDF8MTE3Ljg4XzExNy44OF8xOC40OF8wLjY1XzI1NC44OV9VU0R8Q0VCX01OTF8xXzIwMjUwNTE2X18xXzBfMF5DRUItREc2ODI5LUQtRFZPLTIwMjUwNTE2MDcxNS0yMDI1MDUxNjA4NDUtR08gQmFzaWMtMS0jRFZPLTVKOTY0LUQtTU5MLTIwMjUwNTE2MTI0NS0yMDI1MDUxNjE0NDUtR08gQmFzaWMtMS1eMTE3Ljg4XzExNy44OF8xOC40OF8wLjY1XzI1NC44OV5BREdCMkJfQURHXl5BREcxQ0VCTU5MNDAwMjAyNTA1MTZeUEhQXjY2NzkuNjheNjY3OS42OF4xMDQ3LjIwfDF8MjAyNTA0MjExMjM4MTB8MHwxNzQ1MjEwMjkwMDY3U3ZiR0d8fHx8fDAuNjV8MnwwfEVVUg==.D7WISkk6alaXzQKZ1XvCz5ptSv2oKnOJuI0Frdvx9XE=",
    "realtimeLuggage": 1,
    "paymentMethod": 3,
    "maxResponseTime": 15000
}
```
{% endtab %}
{% endtabs %}

### Response

{% tabs %}
{% tab title="Schema" %}

## **sessionId**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique session identifier for the booking response. It is required when you call order function to make a reservation to identify which flight and fare the client is choosing. 
- **Default:** None  
- **Example:** "c8ba1074-0c3c-47f2-9b86-f99e5d4e6e2e"  

## **maxSeats**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Maximum number of seats available for booking. Please refer this element and prevent the end-users to choose more passengers than seat count.  
- **Default:** None  
- **Example:** 4  

## **routing**
- **Type:** Object  
- **Required:** Yes  
- **Description:** Routing details for the selected itinerary.  
- **Constraints:** Must contain valid routing details.  
- **Default:** None  
- **Example:** {...}  

*(This is identical to the search.do API response. Please refer the Search API for details.)*

## **rule**
- **Type:** Object  
- **Required:** Yes  
- **Description:** Rules related to baggage, refunds, and changes.  
- **Constraints:** Must contain at least one applicable rule.  
- **Default:** None  
- **Example:** {...}  

*(This is identical to the search.do API response. Please refer the Search API for details.)*

## **ancillaryProductElements**
- **Type:** Array  
- **Required:** No  
- **Description:** List of ancillary products available for purchase.  
- **Constraints:** Can be empty if no ancillary products are offered.  
- **Default:** []  
- **Example:** []  

*(This is identical to the search.do API response. Please refer the Search API for details.)*

## **vendorFare**
- **Type:** Object  
- **Required:** Yes  
- **Description:** Pricing details provided by the vendor.  
- **Constraints:** Must contain valid currency and price details.  
- **Default:** None  
- **Example:** {...}  

*(Existing fields for vendorFare remain unchanged)*

## **links**
- **Type:** Array  
- **Required:** No  
- **Description:** List of links related to the booking, such as terms and conditions.
- **Default:** []  
- **Example:** [{"carrier": "F9", "kind": "terms", "link": "https://www.flyfrontier.com/legal/contract-of-carriage?mobile=true", "description": "Carrier terms and conditions"}]  

## **separateBookings**
- **Type:** Boolean  
- **Required:** No  
- **Description:** Indicates whether the booking consists of separate reservations.

  Valid values:
  - true: Separate bookings created
  - false: Single booking created. 
- **Default:** false  
- **Example:** false  

## **refreshTime**
- **Type:** String  
- **Required:** No  
- **Description:** Timestamp of the last data refresh in the cache.  
- **Default:** null  
- **Example:** null  

## **displayFare**
- **Type:** Object  
- **Required:** Yes  
- **Description:** The converted fare as per the display currency. 
- **Default:** None  
- **Example:** { "currency": "PHP" }  

*(Existing fields for displayFare remain unchanged)*

## **ancillarySupported**
- **Type:** Array  
- **Required:** No  
- **Description:** List of supported ancillary products.  
- **Default:** []  
- **Example:** ["seat"]  

## **bookingRequirement**
- **Type:** Object  
- **Required:** Yes  
- **Description:** Passenger booking requirements including personal details.  
- **Default:** None  
- **Example:** {...}  

### **bookingRequirement.passenger**
- **Type:** Object  
- **Required:** Yes  
- **Description:** Passenger-specific details required for booking.  
- **Default:** None  
- **Example:** {...}

#### **bookingRequirement.passenger.birthday**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's date of birth. Must follow YYYY-MM-DD format.    
- **Default:** None  
- **Example:** "1990-01-01"  

#### **bookingRequirement.passenger.cardIssuePlace**
- **Type:** String  
- **Required:** Yes  
- **Description:** Place where the passenger's identification card was issued.  
- **Default:** None  
- **Example:** "USA"  

#### **bookingRequirement.passenger.cardNum**
- **Type:** String  
- **Required:** Yes  
- **Description:** Identification card number of the passenger.  
- **Default:** None  
- **Example:** "A12345678"  

#### **bookingRequirement.passenger.passengerType**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Type of passenger (e.g., adult, child, infant).

  Valid values:
  - 0 = Adult
  - 1 = Child
  - 2 = Infant.  
- **Default:** None  
- **Example:** 0  

#### **bookingRequirement.passenger.gender**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's gender.

  Valid values:
  - "M" for Male
  - "F" for Female.  
- **Default:** None  
- **Example:** "M"  

#### **bookingRequirement.passenger.nationality**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's nationality. Must be a valid country code.  
- **Default:** None  
- **Example:** "USA"  

#### **bookingRequirement.passenger.cardExpired**
- **Type:** String  
- **Required:** Yes  
- **Description:** Expiration date of the passenger's identification card. Must follow YYYY-MM-DD format.  
- **Default:** None  
- **Example:** "2030-12-31"  

#### **bookingRequirement.passenger.name**
- **Type:** String  
- **Required:** Yes  
- **Description:** Full name of the passenger. Maximum length: 30 characters for first name, 30 characters for last name.    
- **Default:** None  
- **Example:** "John Doe"  

#### **bookingRequirement.passenger.cardType**
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of identification card used.  
- **Default:** None  
- **Example:** "Passport"  

### **cardChargeList**
- **Type:** Array of Objects  
- **Required:** No  
- **Description:** List of credit/debit card surcharge configurations. Each object specifies the card type and either a percentage-based or fixed charge to be applied during payment.  
- **Default:** `[]`  
- **Example:**
  ```json
  [
    {
      "cardType": "Amex",
      "percentage": 0.05,
      "charge": null,
      "currency": null
    }
  ]
  ```

#### **cardChargeList[].cardType**
- **Type:** String  
- **Required:** Yes  
- **Description:** The card brand/type to which the charge rule applies.

  Valid values:
  - Amex
  - Visa
  - Mastercard
  - JCB
  - Discover
  - DinersClub
- **Default:** None  
- **Example:** `"Amex"`

#### **cardChargeList[].percentage**
- **Type:** Number
- **Required:** No  
- **Description:** Percentage of the total transaction to be added as a surcharge.  
- **Default:** `0.0`  
- **Example:** `0.05` (i.e., 5%)

#### **cardChargeList[].charge**
- **Type:** Number or Null  
- **Required:** No  
- **Description:** Fixed surcharge amount applied for this card type.  
- **Default:** `null`  
- **Example:** `null`  

#### **cardChargeList[].currency**
- **Type:** String or Null  
- **Required:** No  
- **Description:** Currency in which the fixed charge is denominated.  
- **Default:** `null`  
- **Example:** `null`

## **priceChange**
- **Type:** Object  
- **Required:** Yes  
- **Description:** Indicates if there has been a change in ticket price.  
- **Default:** None  
- **Example:** {...}  

## **priceChange**
- **Type:** Object  
- **Required:** Yes  
- **Description:** Indicates if there has been a change in ticket pricing.  
- **Default:** None  
- **Example:** {...}  

### **priceChange.isPriceChange**
- **Type:** Boolean  
- **Required:** Yes  
- **Description:** Indicates whether the ticket price has changed.
  Valid values:
  true: Price change
  false: No price change
- **Default:** false  
- **Example:** false  

### **priceChange.originalAdultPrice**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Original price for an adult ticket.  
- **Default:** None  
- **Example:** 40.85  

### **priceChange.originalAdultTax**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Original tax for an adult ticket.  
- **Default:** None  
- **Example:** 0.13  

### **priceChange.originalChildPrice**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Original price for a child ticket.  
- **Default:** None  
- **Example:** 40.85  

### **priceChange.originalChildTax**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Original tax for a child ticket.  
- **Default:** None  
- **Example:** 0.13  

### **priceChange.originalInfantPrice**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Original price for an infant ticket.  
- **Default:** None  
- **Example:** 10.00  

### **priceChange.originalInfantTax**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Original tax for an infant ticket.  
- **Default:** None  
- **Example:** 0.00  

*(Fields for new prices remain similar to original prices.)*

### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Response status code.  

  Valid values:
  - 0: success
  - 1: request data format error
  - 2: route is forbidden
  - 3: unauthorized access
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
```
{
  "sessionId": "e1ee90f2-6e38-4423-b018-081e7a0a877f",
  "maxSeats": 9,
  "routing": {
    "fid": "NNQPjln9io_VkVCLML-tV4uTWB1-bYVbwEbgbq1gwbbyIGmv3IQjvGArLc-kVkfqqonjuSrhTmd6q9tCSQ5JdEbgsLbAG9YqlESmEgnTm4P1GEmT5TthTQ..",
    "routingIdentifier": "EXsU8XSpfLYTSaQTVCjrJMJvG/ysDtKYfq1WIi9iKV3RuKGQWRYoLHwlk3d3nfx3CfcndJLEJ0OelZh4CJOznF9aTBiw3WJrCv1w5tPrnLqsrzEwGf6LU4JnimIHlZ8g9Mbw9o1UAsRxu28yDTH1sxCUiQXhe9aQqCnWwMFh28gA/nj6IKNh5/yz0GWbBL6s1yDekyABUkLWmuWriKG76AcSFeTleOVJEjXfFd3mUvpZJe1wsRs5TI/Nma2Sz/cOdhAjhrTIFnOMJEKInVplSW3JYquYRVlKPNaFSuoF5K7IHGWlTR0X2vJysOfDQQZWR7Qv1wj0wUrE1kfV4vUrurLMbC/8XlxjYBc7iz9giHkbTb9r/K5/eabN+BX2cuBjtcmNH0T9SwZdxpCXnsjGxdC6wjGifmzacvdkADFsgfWzqaR6+aEfwt4jQKkit64X8IoXcz9XqDadvtpoFyrQz1tXYb6UK8+doiventK1gdc8oJQnVwpWZPELvPlBkk4NAyGgJvlATBKELGGnovqHmndI9ffItZth6YPlLhv9P5f1GEmT5TthTQ==",
    "supportCreditTransPayment": "1",
    "currency": "USD",
    "adultPrice": 60.97,
    "adultTax": 20.68,
    "childPrice": 60.97,
    "childTax": 20.68,
    "infantPrice": 77.46,
    "infantTax": 0,
    "infantAllowed": true,
    "transactionFeePerPax": 0.65,
    "transactionFee": 0.65,
    "transactionFeeMode": "PER_TICKET",
    "nationalityType": 0,
    "nationality": "",
    "suitAge": "",
    "PaxType": "ADT",
    "fromSegments": [
      {
        "segmentIndex": 1,
        "carrier": "W6",
        "flightNumber": "W65001",
        "depAirport": "KRK",
        "depTime": "202403260600",
        "arrAirport": "LTN",
        "arrTime": "202403260735",
        "stopCities": "",
        "duration": 155,
        "codeShare": false,
        "cabin": "",
        "cabinClass": 1,
        "seatCount": 9,
        "aircraftCode": "",
        "depTerminal": "",
        "arrTerminal": "",
        "operatingCarrier": "W6",
        "operatingFlightnumber": "",
        "fareFamily": "Basic"
      }
    ],
    "retSegments": [
      {
        "segmentIndex": 2,
        "carrier": "W6",
        "flightNumber": "W62002",
        "depAirport": "LTN",
        "depTime": "202404230815",
        "arrAirport": "KRK",
        "arrTime": "202404231140",
        "stopCities": "",
        "duration": 145,
        "codeShare": false,
        "cabin": "",
        "cabinClass": 1,
        "seatCount": 9,
        "aircraftCode": "",
        "depTerminal": "",
        "arrTerminal": "",
        "operatingCarrier": "W6",
        "operatingFlightnumber": "",
        "fareFamily": "Basic"
      }
    ],
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
        },
        {
          "segmentNo": 2,
          "baggageType": "CabinBaggageUnderSeat",
          "passengerType": 0,
          "baggagePiece": 1,
          "baggageWeight": -1,
          "baggageSize": "40*30*20cm"
        },
        {
          "segmentNo": 2,
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
          "refundFee": 0,
          "currency": "EUR",
          "refNoshow": "T",
          "refNoShowCondition": 0,
          "refNoshowFee": 0,
          "ruleDetailList": [
            {
              "ruleId": 2988,
              "status": "H",
              "startMinute": 525600,
              "endMinute": 20160,
              "amount": 65,
              "currency": "EUR"
            },
            {
              "ruleId": 2990,
              "status": "H",
              "startMinute": 20160,
              "endMinute": 180,
              "amount": 85,
              "currency": "EUR"
            },
            {
              "ruleId": 2993,
              "status": "T",
              "startMinute": 180,
              "endMinute": 0,
              "amount": 0,
              "currency": "EUR"
            },
            {
              "ruleId": 2996,
              "status": "T",
              "startMinute": 0,
              "endMinute": -525600,
              "amount": 0,
              "currency": "EUR"
            }
          ]
        },
        {
          "refundType": 0,
          "refundStatus": "T",
          "refundFee": 0,
          "currency": "EUR",
          "refNoshow": "T",
          "refNoShowCondition": 0,
          "refNoshowFee": 0,
          "ruleDetailList": [
            {
              "ruleId": 2988,
              "status": "H",
              "startMinute": 525600,
              "endMinute": 20160,
              "amount": 65,
              "currency": "EUR"
            },
            {
              "ruleId": 2990,
              "status": "H",
              "startMinute": 20160,
              "endMinute": 180,
              "amount": 85,
              "currency": "EUR"
            },
            {
              "ruleId": 2993,
              "status": "T",
              "startMinute": 180,
              "endMinute": 0,
              "amount": 0,
              "currency": "EUR"
            },
            {
              "ruleId": 2996,
              "status": "T",
              "startMinute": 0,
              "endMinute": -525600,
              "amount": 0,
              "currency": "EUR"
            }
          ]
        }
      ],
      "changesRules": [
        {
          "changesType": 0,
          "changesStatus": "T",
          "changesFee": 0,
          "currency": "EUR",
          "revNoshow": "T",
          "revNoShowCondition": 0,
          "revNoshowFee": 0,
          "ruleDetailList": [
            {
              "ruleId": 10153,
              "status": "H",
              "startMinute": 525600,
              "endMinute": 43200,
              "amount": 40,
              "currency": "EUR"
            },
            {
              "ruleId": 10155,
              "status": "H",
              "startMinute": 43200,
              "endMinute": 10080,
              "amount": 45,
              "currency": "EUR"
            },
            {
              "ruleId": 10157,
              "status": "H",
              "startMinute": 10080,
              "endMinute": 180,
              "amount": 50,
              "currency": "EUR"
            },
            {
              "ruleId": 10160,
              "status": "T",
              "startMinute": 180,
              "endMinute": 0,
              "amount": 0,
              "currency": "EUR"
            },
            {
              "ruleId": 10163,
              "status": "T",
              "startMinute": 0,
              "endMinute": -525600,
              "amount": 0,
              "currency": "EUR"
            }
          ]
        },
        {
          "changesType": 0,
          "changesStatus": "T",
          "changesFee": 0,
          "currency": "EUR",
          "revNoshow": "T",
          "revNoShowCondition": 0,
          "revNoshowFee": 0,
          "ruleDetailList": [
            {
              "ruleId": 10153,
              "status": "H",
              "startMinute": 525600,
              "endMinute": 43200,
              "amount": 40,
              "currency": "EUR"
            },
            {
              "ruleId": 10155,
              "status": "H",
              "startMinute": 43200,
              "endMinute": 10080,
              "amount": 45,
              "currency": "EUR"
            },
            {
              "ruleId": 10157,
              "status": "H",
              "startMinute": 10080,
              "endMinute": 180,
              "amount": 50,
              "currency": "EUR"
            },
            {
              "ruleId": 10160,
              "status": "T",
              "startMinute": 180,
              "endMinute": 0,
              "amount": 0,
              "currency": "EUR"
            },
            {
              "ruleId": 10163,
              "status": "T",
              "startMinute": 0,
              "endMinute": -525600,
              "amount": 0,
              "currency": "EUR"
            }
          ]
        }
      ],
      "serviceElements": [
        {
          "hasFreeSeat": 0,
          "hasFreeMeal": 0
        },
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
        "productCode": "SCI_1PC_10KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 59.32,
        "currency": "USD",
        "vendorPrice": 235,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 10,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_1PC_10KG",
        "auxSeatElement": null,
        "displayPrice": 3316.95,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_1PC_20KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 90.62,
        "currency": "USD",
        "vendorPrice": 359,
        "vendorCurrency": "PLN",
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
        "displayPrice": 5067.17,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_2PC_40KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 189.05,
        "currency": "USD",
        "vendorPrice": 749,
        "vendorCurrency": "PLN",
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
        "displayPrice": 10571.89,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_3PC_60KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 289.76,
        "currency": "USD",
        "vendorPrice": 1148,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 3,
          "weight": 60,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_3PC_60KG",
        "auxSeatElement": null,
        "displayPrice": 16203.64,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_4PC_80KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 391.73,
        "currency": "USD",
        "vendorPrice": 1552,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 4,
          "weight": 80,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_4PC_80KG",
        "auxSeatElement": null,
        "displayPrice": 21905.97,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_5PC_100KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 495.97,
        "currency": "USD",
        "vendorPrice": 1965,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 5,
          "weight": 100,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_5PC_100KG",
        "auxSeatElement": null,
        "displayPrice": 27735.32,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_6PC_120KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 603.74,
        "currency": "USD",
        "vendorPrice": 2392,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 6,
          "weight": 120,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_6PC_120KG",
        "auxSeatElement": null,
        "displayPrice": 33762.29,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_1PC_26KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 92.89,
        "currency": "USD",
        "vendorPrice": 368,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 26,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_1PC_26KG",
        "auxSeatElement": null,
        "displayPrice": 5194.2,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_2PC_52KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 193.85,
        "currency": "USD",
        "vendorPrice": 768,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 2,
          "weight": 52,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_2PC_52KG",
        "auxSeatElement": null,
        "displayPrice": 10840.07,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_3PC_78KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 297.08,
        "currency": "USD",
        "vendorPrice": 1177,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 3,
          "weight": 78,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_3PC_78KG",
        "auxSeatElement": null,
        "displayPrice": 16612.97,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_4PC_104KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 401.57,
        "currency": "USD",
        "vendorPrice": 1591,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 4,
          "weight": 104,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_4PC_104KG",
        "auxSeatElement": null,
        "displayPrice": 22456.44,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_5PC_130KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 508.34,
        "currency": "USD",
        "vendorPrice": 2014,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 5,
          "weight": 130,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_5PC_130KG",
        "auxSeatElement": null,
        "displayPrice": 28426.94,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_6PC_156KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 618.38,
        "currency": "USD",
        "vendorPrice": 2450,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 6,
          "weight": 156,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_6PC_156KG",
        "auxSeatElement": null,
        "displayPrice": 34580.94,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_1PC_32KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 96.67,
        "currency": "USD",
        "vendorPrice": 383,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 32,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_1PC_32KG",
        "auxSeatElement": null,
        "displayPrice": 5405.92,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_2PC_64KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 201.42,
        "currency": "USD",
        "vendorPrice": 798,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 2,
          "weight": 64,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_2PC_64KG",
        "auxSeatElement": null,
        "displayPrice": 11263.51,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_3PC_96KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 308.44,
        "currency": "USD",
        "vendorPrice": 1222,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 3,
          "weight": 96,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_3PC_96KG",
        "auxSeatElement": null,
        "displayPrice": 17248.13,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_4PC_128KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 416.46,
        "currency": "USD",
        "vendorPrice": 1650,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 4,
          "weight": 128,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_4PC_128KG",
        "auxSeatElement": null,
        "displayPrice": 23289.2,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_5PC_160KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 526.76,
        "currency": "USD",
        "vendorPrice": 2087,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 5,
          "weight": 160,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_5PC_160KG",
        "auxSeatElement": null,
        "displayPrice": 29457.31,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_6PC_192KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 640.59,
        "currency": "USD",
        "vendorPrice": 2538,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 6,
          "weight": 192,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_6PC_192KG",
        "auxSeatElement": null,
        "displayPrice": 35823.03,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "CBOL_1PC_10KG",
        "productName": "CabinBaggageOverheadLocker",
        "productType": 3,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 29.79,
        "currency": "USD",
        "vendorPrice": 118,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
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
        "ancillaryCode": "CBOL_1PC_10KG",
        "auxSeatElement": null,
        "displayPrice": 1665.54,
        "displayCurrency": "PHP"
      }
    ],
    "vendorFare": {
      "vendorAdultPrice": 241.53,
      "vendorAdultTax": 81.94,
      "vendorChildPrice": 241.53,
      "vendorChildTax": 81.94,
      "vendorInfantPrice": 306.88,
      "vendorInfantTax": 0,
      "vendorCurrency": "PLN"
    },
    "bundleOptions": [],
    "links": [
      {
        "kind": "terms",
        "link": "https://wizzair.com/en-gb/legal/general-conditions-of-carriage-for-passengers-and-baggage",
        "description": "Carrier terms and conditions"
      }
    ],
    "separateBookings": false,
    "refreshTime": null,
    "displayFare": {
      "currency": "PHP",
      "exchangeRate": 14.1146661,
      "adultPrice": 3408.69,
      "adultTax": 1156.24,
      "childPrice": 3408.69,
      "childTax": 1156.24,
      "infantPrice": 4330.77,
      "infantTax": 0
    }
  },
  "bookingRequirement": {
    "passenger": {
      "cardIssuePlace": {
        "type": "string",
        "required": false,
        "description": null,
        "maxLength": null
      },
      "birthday": {
        "type": "string",
        "required": false,
        "description": null,
        "maxLength": null
      },
      "cardNum": {
        "type": "string",
        "required": false,
        "description": null,
        "maxLength": null
      },
      "passengerType": {
        "type": "int",
        "required": true,
        "description": null,
        "maxLength": null
      },
      "nationality": {
        "type": "string",
        "required": false,
        "description": null,
        "maxLength": null
      },
      "gender": {
        "type": "string",
        "required": true,
        "description": null,
        "maxLength": null
      },
      "cardExpired": {
        "type": "string",
        "required": false,
        "description": null,
        "maxLength": null
      },
      "cardType": {
        "type": "string",
        "required": false,
        "description": null,
        "maxLength": null
      },
      "name": {
        "type": "string",
        "required": true,
        "description": null,
        "maxLength": null
      }
    }
  },
  "priceChange": {
    "isPriceChange": false,
    "originalAdultPrice": 60.97,
    "originalAdultTax": 20.68,
    "originalChildPrice": 60.97,
    "originalChildTax": 20.68,
    "originalInfantPrice": 77.46,
    "originalInfantTax": 0,
    "newAdultPrice": 60.97,
    "newAdultTax": 20.68,
    "newChildPrice": 60.97,
    "newChildTax": 20.68,
    "newInfantPrice": 77.46,
    "newInfantTax": 0
  },
  "status": 0,
  "msg": "success"
}
```
{% endtab %}
{% endtabs %}
