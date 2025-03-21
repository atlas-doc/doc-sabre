# Real-time Search

### Dependency

No preceding function needs to be called before this call.

### Endpoint {% debug uid="search_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/realTimeSearch.do](https://sandbox.atriptech.com/realTimeSearch.do)

{% hint style="info" %}
**Points to note for real-time search:**

* This function will only be opened by Atlas after understanding the requirements. 
* The content of the RQ and RS remains the same. Once the search response is received, the exact same flow needs to be followed for verify, book and pay process. The end-points for these services also remain the same.
* The timeout duration is 120s
* As this is a LIVE search, we would recommend that the airline filter is used during the search process to speed-up the response.
* Please contact your Business Development Director or Account Manager if you require access to this functionality.
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

## **acceptCacheIfTimeout**
- **Type:** Boolean  
- **Required:** No  
- **Description:** Indicates whether cached results should be accepted in case of timeout. If "false", then the request will time-out if it exceeds 120s and no results will be displayed. If "true", then after 120s cache results will be displayed. 
- **Constraints:** true or false.  
- **Default:** true  
- **Example:** true  

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
  "tripType": "1",
  "adultNum": 1,
  "childNum": 0,
  "infantNum": 0,
  "fromCity": "CEB",
  "toCity": "DXB",
  "fromDate": "20230721",
  "retDate": "",
  "airlines": ["5J"],
  "acceptCacheIfTimeout": true,
  "requestSource": "Organic"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}

The response is identical to the search.do API response. Please refer to the "Search" section for details.
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
