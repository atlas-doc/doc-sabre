# Seat Availability

To get seats availability, characteristic and price.

### Dependency

Verify function should be called in prior to this call.

### Endpoint {% debug uid="seatAvailability_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/seatAvailability.do](https://sandbox.atriptech.com/seatAvailability.do)

## Request

{% tabs %}
{% tab title="Schema" %}
### **sessionId**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique session identifier for retrieving seat map information.  
- **Constraints:** Must be a valid UUID.  
- **Default:** None  
- **Example:** "eb3c94a7-ede4-4675-a7bb-a99ba1e10223"  

    **Please note that the sessionID needs to be the same throughout the order.**

{% endtab %}

{% tab title="Samples" %}
```json
{
    "sessionId": "eb3c94a7-ede4-4675-a7bb-a99ba1e10223"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
## **cabins**
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of cabin details per segment.  
- **Constraints:** Must contain at least one cabin entry.  
- **Default:** None  
- **Example:** [{...}]  

### **cabins.segmentIndex**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Flight segment for which seat map is returned.
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** 1  

### **cabins.cabin**
- **Type:** Object  
- **Required:** Yes  
- **Description:** Cabin details, including deck and seat arrangement. This is a list and will be repeated once for upper deck and once for the main deck when the requested cabin is spread across the upper and main deck.
- **Constraints:** Must contain valid seat information.  
- **Default:** None  
- **Example:** {...}  

### **cabin.deck**
- **Type:** String  
- **Required:** Yes  
- **Description:** Deck level of the cabin.  

  Valid values:

  “Upper deck”: Upper deck

  “Main”: Main deck (default)
- **Constraints:** Must be a valid deck name.  
- **Default:** "main"  
- **Example:** "main"  

### **cabin.cabinClass**
- **Type:** Integer  
- **Required:** Yes  
- **Description:**  Service grade of the fare.

  Valid values:

  1 : Economy

  2 : Business

  3 : First Class

  4:  Premium Economy
- **Constraints:** Must be a positive integer.  
- **Default:** 1  
- **Example:** 1  

### **cabin.cabinLayout**
- **Type:** Object  
- **Required:** Yes  
- **Description:** Layout of the cabin, including seat rows and columns.  
- **Constraints:** None  
- **Default:** None  
- **Example:** {...}  

### **cabinLayout.columns**
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of column identifiers and their characteristics. Contains columns and seat information for seat display purposes. Returns the characteristics for each column.  
- **Constraints:** Must contain at least one column entry.  
- **Default:** None  
- **Example:** [{"designator": "A", "characteristics": "W"}]  

#### **cabinLayout.columns.designator**
- **Type:** String  
- **Required:** Yes  
- **Description:** Column designator for seat arrangement. This identifies a seat column position on an aircraft.  
- **Constraints:** Must be a valid character.  
- **Default:** None  
- **Example:** "F"  

#### **cabinLayout.columns.characteristics**
- **Type:** String  
- **Required:** Yes  
- **Description:** Characteristics of the seat column.

  Valid values:

  A: column by the aisle

  M: middle column  

  W: column by the window
- **Constraints:** Must be a valid identifier (e.g., W for Window, A for Aisle).  
- **Default:** None  
- **Example:** "A"  


### **cabinLayout.rows**
- **Type:** Object  
- **Required:** Yes  
- **Description:** Defines the first and last row numbers in the cabin.  
- **Constraints:** Must contain valid row numbers.  
- **Default:** None  
- **Example:** {"first": 4, "last": 20}  

### **cabinLayout.exitRowPositions**
- **Type:** Array  
- **Required:** Yes  
- **Description:** Returns the exit row information, if applicable. This must be returned regardless of whether exit row seats are open or are returned as valid seats.
- **Constraints:** Must contain valid row numbers.  
- **Default:** None  
- **Example:** [{"first": 4, "last": 5}]  

### **cabin.rows**
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of seat rows and their characteristics.  
- **Constraints:** Must contain at least one row.  
- **Default:** None  
- **Example:** [{...}]  

#### **rows.number**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Seat row number in the cabin.  
- **Constraints:** Must be a valid row number.  
- **Default:** None  
- **Example:** 4  

### **rows.seats**
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of seats in the row with their details.  
- **Constraints:** Must contain at least one seat.  
- **Default:** None  
- **Example:** [{...}]  

### **seats.column**
- **Type:** String  
- **Required:** Yes  
- **Description:** Column identifier for the seat.  
- **Constraints:** Must be a valid column designator.  
- **Default:** None  
- **Example:** "A"  

### **seats.seatStatus**
- **Type:** String  
- **Required:** Yes  
- **Description:** Availability status of the seat.  
- **Constraints:** "F" for free, "O" for occupied.  
- **Default:** None  
- **Example:** "F"  

### **seats.seatCharacteristics**
- **Type:** Array  
- **Required:** Yes  
- **Description:** Characteristics of the seat (e.g., Window, Aisle).

    Valid values:

    A: Aisle seat
    
    E: Exit and emergency exit
    
    I:  Seat suitable for adult with an infant
    
    IE：Seat not suitable for child
    
    L:  Leg space seat
    
    U：Seat suitable for unaccompanied minors
    
    V：Seat to be left vacant or offered last
    
    W:  Window seat  
- **Constraints:** None  
- **Default:** None  
- **Example:** ["W", "L", "E"]  

**Example**: refer to IATA definition from codeset 9825, reference 825
    
**Document link**: https://pnr.lt/Failai/Code set Directory v13 2.pdf

### **seats.price**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Price of the seat.
- **Constraints:** Must be a positive Number value.  
- **Default:** None  
- **Example:** 23.52  

### **seats.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency for the seat price.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None
- **Example:** "USD"  

### **seats.vendorPrice**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Price of the seat from the vendor.  
- **Constraints:** Must be a positive Number value.  
- **Default:** None  
- **Example:** 593907.25  

### **seats.vendorCurrency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Vendor's currency for the seat price.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** "VND"  
- **Example:** "VND"  

### **seats.productCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique product code for the seat selection. For seat, the format is SCI_SEAT_seatNumber_carrier_depAirport_arrAirport 
- **Constraints:** None  
- **Default:** None  
- **Example:** "SCI_SEAT_4A_VJ_HND_SGN"  

### **seats.displayCurrency**
- **Type:** String  
- **Required:** No  
- **Description:** Currency used for displaying seat price in the display currancy.  
- **Constraints:** Can be null if not applicable.  
- **Default:** null  
- **Example:** "USD"  

### **seats.displayPrice**
- **Type:** Number  
- **Required:** No  
- **Description:** Seat price displayed in the display currency.  
- **Constraints:** Can be null if not applicable.  
- **Default:** null  
- **Example:** 50.35  

## **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Response status code.  
- **Constraints:** 0 indicates success.  
- **Default:** 0  
- **Example:** 0  

## **msg**
- **Type:** String  
- **Required:** Yes  
- **Description:** Response message.  
- **Constraints:** None  
- **Default:** "success"  
- **Example:** "success"
{% endtab %}

{% tab title="Samples" %}
```json
  {
    "cabins": [
        {
            "segmentIndex": 1,
            "cabin": {
                "deck": "main",
                "cabinClass": 1,
                "cabinLayout": {
                    "columns": [
                        {
                            "designator": "A",
                            "characteristics": "W"
                        },
                        {
                            "designator": "B",
                            "characteristics": "M"
                        },
                        {
                            "designator": "C",
                            "characteristics": "A"
                        },
                        {
                            "designator": "D",
                            "characteristics": "W"
                        },
                        {
                            "designator": "E",
                            "characteristics": "M"
                        },
                        {
                            "designator": "F",
                            "characteristics": "A"
                        }
                    ],
                    "rows": {
                        "first": 4,
                        "last": 20
                    },
                    "exitRowPositions": [
                        {
                            "first": 4,
                            "last": 5
                        },
                        {
                            "first": 10,
                            "last": 11
                        },
                        {
                            "first": 20,
                            "last": 20
                        }
                    ]
                },
                "rows": [
                    {
                        "number": 4,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "L",
                                    "E"
                                ],
                                "price": 23.52,
                                "currency": "USD",
                                "vendorPrice": 593907.25,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_4A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M",
                                    "L",
                                    "E"
                                ],
                                "price": 97.56,
                                "currency": "USD",
                                "vendorPrice": 2463634.10,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_4B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A",
                                    "L",
                                    "E"
                                ],
                                "price": 65.45,
                                "currency": "USD",
                                "vendorPrice": 1652766.30,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_4C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "L",
                                    "E"
                                ],
                                "price": 36.69,
                                "currency": "USD",
                                "vendorPrice": 926597.05,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_4D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M",
                                    "L",
                                    "E"
                                ],
                                "price": 95.09,
                                "currency": "USD",
                                "vendorPrice": 2401318.35,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_4E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A",
                                    "L",
                                    "E"
                                ],
                                "price": 50.35,
                                "currency": "USD",
                                "vendorPrice": 1271495.65,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_4F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    },
                    {
                        "number": 5,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "L",
                                    "E"
                                ],
                                "price": 27.32,
                                "currency": "USD",
                                "vendorPrice": 689797.20,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_5A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M",
                                    "L",
                                    "E"
                                ],
                                "price": 75.31,
                                "currency": "USD",
                                "vendorPrice": 1901774.95,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_5B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A",
                                    "L",
                                    "E"
                                ],
                                "price": 72.55,
                                "currency": "USD",
                                "vendorPrice": 1832083.05,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_5C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "L",
                                    "E"
                                ],
                                "price": 36.66,
                                "currency": "USD",
                                "vendorPrice": 925834.00,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_5D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M",
                                    "L",
                                    "E"
                                ],
                                "price": 95.28,
                                "currency": "USD",
                                "vendorPrice": 2406151.00,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_5E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A",
                                    "L",
                                    "E"
                                ],
                                "price": 97.45,
                                "currency": "USD",
                                "vendorPrice": 2460836.25,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_5F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    },
                    {
                        "number": 6,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 46.67,
                                "currency": "USD",
                                "vendorPrice": 1178657.90,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_6A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 69.50,
                                "currency": "USD",
                                "vendorPrice": 1755015.00,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_6B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 75.59,
                                "currency": "USD",
                                "vendorPrice": 1908896.75,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_6C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 73.32,
                                "currency": "USD",
                                "vendorPrice": 1851413.65,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_6D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 13.66,
                                "currency": "USD",
                                "vendorPrice": 344898.60,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_6E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 19.89,
                                "currency": "USD",
                                "vendorPrice": 502341.25,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_6F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    },
                    {
                        "number": 7,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 44.88,
                                "currency": "USD",
                                "vendorPrice": 1133383.60,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_7A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 36.93,
                                "currency": "USD",
                                "vendorPrice": 932701.45,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_7B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 52.16,
                                "currency": "USD",
                                "vendorPrice": 1317278.65,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_7C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 61.20,
                                "currency": "USD",
                                "vendorPrice": 1545430.60,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_7D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 32.26,
                                "currency": "USD",
                                "vendorPrice": 814683.05,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_7E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 33.42,
                                "currency": "USD",
                                "vendorPrice": 843933.30,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_7F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    },
                    {
                        "number": 8,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 34.52,
                                "currency": "USD",
                                "vendorPrice": 871657.45,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_8A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 73.28,
                                "currency": "USD",
                                "vendorPrice": 1850396.25,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_8B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 35.95,
                                "currency": "USD",
                                "vendorPrice": 907775.15,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_8C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 49.89,
                                "currency": "USD",
                                "vendorPrice": 1259795.55,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_8D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 98.40,
                                "currency": "USD",
                                "vendorPrice": 2484745.15,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_8E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 26.40,
                                "currency": "USD",
                                "vendorPrice": 666651.35,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_8F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    },
                    {
                        "number": 9,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 46.23,
                                "currency": "USD",
                                "vendorPrice": 1167466.50,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_9A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 13.17,
                                "currency": "USD",
                                "vendorPrice": 332689.80,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_9B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 55.13,
                                "currency": "USD",
                                "vendorPrice": 1392057.55,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_9C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 30.42,
                                "currency": "USD",
                                "vendorPrice": 768137.00,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_9D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 94.18,
                                "currency": "USD",
                                "vendorPrice": 2378172.50,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_9E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 46.96,
                                "currency": "USD",
                                "vendorPrice": 1185779.70,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_9F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    },
                    {
                        "number": 10,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "L",
                                    "E"
                                ],
                                "price": 76.35,
                                "currency": "USD",
                                "vendorPrice": 1927973.00,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_10A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M",
                                    "L",
                                    "E"
                                ],
                                "price": 16.29,
                                "currency": "USD",
                                "vendorPrice": 411283.95,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_10B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A",
                                    "L",
                                    "E"
                                ],
                                "price": 54.24,
                                "currency": "USD",
                                "vendorPrice": 1369674.75,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_10C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "L",
                                    "E"
                                ],
                                "price": 59.31,
                                "currency": "USD",
                                "vendorPrice": 1497612.80,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_10D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M",
                                    "L",
                                    "E"
                                ],
                                "price": 80.54,
                                "currency": "USD",
                                "vendorPrice": 2033782.60,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_10E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A",
                                    "L",
                                    "E"
                                ],
                                "price": 96.57,
                                "currency": "USD",
                                "vendorPrice": 2438707.80,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_10F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    },
                    {
                        "number": 11,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "L",
                                    "E"
                                ],
                                "price": 12.13,
                                "currency": "USD",
                                "vendorPrice": 306237.40,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_11A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M",
                                    "L",
                                    "E"
                                ],
                                "price": 16.79,
                                "currency": "USD",
                                "vendorPrice": 424001.45,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_11B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A",
                                    "L",
                                    "E"
                                ],
                                "price": 64.77,
                                "currency": "USD",
                                "vendorPrice": 1635724.85,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_11C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "L",
                                    "E"
                                ],
                                "price": 98.29,
                                "currency": "USD",
                                "vendorPrice": 2481947.30,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_11D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M",
                                    "L",
                                    "E"
                                ],
                                "price": 40.40,
                                "currency": "USD",
                                "vendorPrice": 1020197.85,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_11E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A",
                                    "L",
                                    "E"
                                ],
                                "price": 54.99,
                                "currency": "USD",
                                "vendorPrice": 1388751.00,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_11F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    },
                    {
                        "number": 12,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 58.96,
                                "currency": "USD",
                                "vendorPrice": 1488964.90,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_12A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 13.29,
                                "currency": "USD",
                                "vendorPrice": 335487.65,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_12B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 48.31,
                                "currency": "USD",
                                "vendorPrice": 1219862.60,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_12C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 19.21,
                                "currency": "USD",
                                "vendorPrice": 485045.45,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_12D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 49.53,
                                "currency": "USD",
                                "vendorPrice": 1250638.95,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_12E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 53.72,
                                "currency": "USD",
                                "vendorPrice": 1356448.55,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_12F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    },
                    {
                        "number": 13,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 38.59,
                                "currency": "USD",
                                "vendorPrice": 974414.85,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_13A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 54.53,
                                "currency": "USD",
                                "vendorPrice": 1377050.90,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_13B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 24.45,
                                "currency": "USD",
                                "vendorPrice": 617307.45,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_13C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 53.44,
                                "currency": "USD",
                                "vendorPrice": 1349581.10,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_13D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 30.27,
                                "currency": "USD",
                                "vendorPrice": 764321.75,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_13E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 18.27,
                                "currency": "USD",
                                "vendorPrice": 461390.90,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_13F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    },
                    {
                        "number": 14,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 95.70,
                                "currency": "USD",
                                "vendorPrice": 2416579.35,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_14A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 67.22,
                                "currency": "USD",
                                "vendorPrice": 1697531.90,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_14B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 46.30,
                                "currency": "USD",
                                "vendorPrice": 1169246.95,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_14C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 46.73,
                                "currency": "USD",
                                "vendorPrice": 1179929.65,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_14D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 49.01,
                                "currency": "USD",
                                "vendorPrice": 1237667.10,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_14E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 62.82,
                                "currency": "USD",
                                "vendorPrice": 1586380.95,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_14F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    },
                    {
                        "number": 15,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 97.26,
                                "currency": "USD",
                                "vendorPrice": 2456003.60,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_15A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 65.80,
                                "currency": "USD",
                                "vendorPrice": 1661668.55,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_15B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 82.85,
                                "currency": "USD",
                                "vendorPrice": 2092283.10,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_15C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 57.97,
                                "currency": "USD",
                                "vendorPrice": 1463784.25,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_15D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 39.07,
                                "currency": "USD",
                                "vendorPrice": 986623.65,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_15E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 61.17,
                                "currency": "USD",
                                "vendorPrice": 1544667.55,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_15F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    },
                    {
                        "number": 16,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 91.98,
                                "currency": "USD",
                                "vendorPrice": 2322724.20,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_16A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 71.77,
                                "currency": "USD",
                                "vendorPrice": 1812498.10,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_16B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 56.64,
                                "currency": "USD",
                                "vendorPrice": 1430210.05,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_16C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 89.59,
                                "currency": "USD",
                                "vendorPrice": 2262443.25,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_16D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 91.78,
                                "currency": "USD",
                                "vendorPrice": 2317637.20,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_16E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 31.32,
                                "currency": "USD",
                                "vendorPrice": 791028.50,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_16F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    },
                    {
                        "number": 17,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 23.70,
                                "currency": "USD",
                                "vendorPrice": 598485.55,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_17A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 89.18,
                                "currency": "USD",
                                "vendorPrice": 2252014.90,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_17B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 62.11,
                                "currency": "USD",
                                "vendorPrice": 1568322.10,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_17C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 73.36,
                                "currency": "USD",
                                "vendorPrice": 1852431.05,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_17D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 17.73,
                                "currency": "USD",
                                "vendorPrice": 447656.00,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_17E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 68.82,
                                "currency": "USD",
                                "vendorPrice": 1737973.55,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_17F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    },
                    {
                        "number": 18,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 17.71,
                                "currency": "USD",
                                "vendorPrice": 447147.30,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_18A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 43.00,
                                "currency": "USD",
                                "vendorPrice": 1085820.15,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_18B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 91.94,
                                "currency": "USD",
                                "vendorPrice": 2321706.80,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_18C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 82.49,
                                "currency": "USD",
                                "vendorPrice": 2083126.50,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_18D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 71.83,
                                "currency": "USD",
                                "vendorPrice": 1813769.85,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_18E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 97.69,
                                "currency": "USD",
                                "vendorPrice": 2466940.65,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_18F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    },
                    {
                        "number": 19,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 91.87,
                                "currency": "USD",
                                "vendorPrice": 2319926.35,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_19A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 29.85,
                                "currency": "USD",
                                "vendorPrice": 753893.40,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_19B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 13.42,
                                "currency": "USD",
                                "vendorPrice": 338794.20,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_19C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "I"
                                ],
                                "price": 26.54,
                                "currency": "USD",
                                "vendorPrice": 670212.25,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_19D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M"
                                ],
                                "price": 33.21,
                                "currency": "USD",
                                "vendorPrice": 838591.95,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_19E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A"
                                ],
                                "price": 54.22,
                                "currency": "USD",
                                "vendorPrice": 1369166.05,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_19F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    },
                    {
                        "number": 20,
                        "seats": [
                            {
                                "column": "A",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "L",
                                    "E"
                                ],
                                "price": 24.42,
                                "currency": "USD",
                                "vendorPrice": 616544.40,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_20A_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "B",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M",
                                    "L",
                                    "E"
                                ],
                                "price": 30.49,
                                "currency": "USD",
                                "vendorPrice": 769917.45,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_20B_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "C",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A",
                                    "L",
                                    "E"
                                ],
                                "price": 89.43,
                                "currency": "USD",
                                "vendorPrice": 2258373.65,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_20C_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "D",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "W",
                                    "L",
                                    "E"
                                ],
                                "price": 57.53,
                                "currency": "USD",
                                "vendorPrice": 1452847.20,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_20D_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "E",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "M",
                                    "L",
                                    "E"
                                ],
                                "price": 71.41,
                                "currency": "USD",
                                "vendorPrice": 1803341.50,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_20E_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            },
                            {
                                "column": "F",
                                "seatStatus": "F",
                                "seatCharacteristics": [
                                    "A",
                                    "L",
                                    "E"
                                ],
                                "price": 80.54,
                                "currency": "USD",
                                "vendorPrice": 2033782.60,
                                "vendorCurrency": "VND",
                                "productCode": "SCI_SEAT_20F_VJ_HND_SGN",
                                "displayCurrency": null,
                                "displayPrice": null
                            }
                        ]
                    }
                ]
            }
        }
    ],
    "status": 0,
    "msg": "success"
}
```
{% endtab %}
{% endtabs %}  
