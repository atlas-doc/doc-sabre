# Order Ancillary

### Dependency

The "postBookingAncillarySearch.do" function should be called prior to this one.

#### Procedure:

1. Copy the Session ID into the request body.

2. Type the passenger information and "product code" selected from the response in "postBookingAncillarySearch.do".

### Endpoint {% debug uid="orderAncillary_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/postBookingAncillaryOrder.do](https://sandbox.atriptech.com/postBookingAncillaryOrder.do)

## Request

{% tabs %}
{% tab title="Schema" %}

### **ticketOrderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the ticket order. It is the original order number.
- **Default:** None  
- **Example:** "TESTA20240618162411631"  

### **airlinePNR**
- **Type:** String  
- **Required:** Yes  
- **Description:** Airline PNR associated with the booking.  
- **Default:** None  
- **Example:** "S37310"  

### **carrier**
- **Type:** String  
- **Required:** Yes  
- **Description:** Airline carrier code.  
- **Default:** None  
- **Example:** "5F"  

### **ancillaryCategory**
- **Type:** String  
- **Required:** Yes  
- **Description:** Category of ancillary service requested. Different categories of ancillaries need to be separately requested. Currently we only support "BAGGAGE".
- **Default:** None  
- **Example:** "BAGGAGE"  

### **sessionId**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique session identifier for the request.  
- **Default:** None  
- **Example:** "fb4861a9-d410-41ed-a483-c372f0713e9c"  

### **passengers** (Array of Objects)
- **Type:** Array of Objects  
- **Required:** Yes  
- **Description:** List of passengers for whom ancillaries are being booked.  
- **Default:** None  
- **Example:** See below.  

#### **Passenger Object Fields**

##### **name**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's name in "LASTNAME/FIRSTNAME MIDDLE NAME" format.  
- **Default:** None  
- **Example:** "DOER/DEF"  

##### **passengerType**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Type of passenger (e.g., 0 for adult).  

  Valid values:
  - 0: ADT
  - 1: CHD
- **Default:** None  
- **Example:** "0"  

##### **ancillaries** (Array of Objects)
- **Type:** Array of Objects  
- **Required:** Yes  
- **Description:** List of ancillaries booked for the passenger.  
- **Default:** None  
- **Example:** See below.  

#### **Ancillary Object Fields**

###### **productCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Code identifying the ancillary product.  
- **Default:** None  
- **Example:** "SCI_BAG_1PC_10KG"  

###### **segmentIndex**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Segment index to which this ancillary applies.  
- **Default:** None  
- **Example:** "1"  
            
{% endtab %}

{% tab title="Samples" %}
```json
{
"cid": "pxmhg93103",
"ticketOrderNo": "TESTA20240618162411631",
"airlinePNR": "S37310",
"carrier": "5F",
"ancillaryCategory": "BAGGAGE",
"sessionId": "fb4861a9-d410-41ed-a483-c372f0713e9c",
"passengers": [{
    "name": "DOER/DEF",
    "passengerType": 0,
    "ancillaries": [
        {
        "productCode": "SCI_BAG_1PC_10KG",
        "segmentIndex": 1
        },
        {
        "productCode": "SCI_BAG_1PC_20KG",
        "segmentIndex": 2
        }
]
}]
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}


### **sessionId**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique session identifier.  
- **Default:** None  
- **Example:** "cde38a72-d7fa-4e5b-9ba5-08b6929143c8"  

### **orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique order number for the ticket purchase.  
- **Default:** None  
- **Example:** "TESTB20240520180835748"  

### **originalOrderNo**
- **Type:** String | Null  
- **Required:** No  
- **Description:** Original order number if applicable.  
- **Default:** Null  
- **Example:** null  

### **ticketOrderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique ticket order number.  
- **Default:** None  
- **Example:** "TESTM20240520171341468"  

### **totalPrice**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Total price of the ticket order.  
- **Default:** None  
- **Example:** "85.51"  

### **totalTransactionFee**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Total transaction fee for the order.  
- **Default:** "0"  
- **Example:** "0"  

### **currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency of the transaction.  
- **Default:** None  
- **Example:** "USD"  

### **vendorTotalPrice**
- **Type:** Number | Null  
- **Required:** No  
- **Description:** Total price from the vendor.  
- **Default:** Null  
- **Example:** null  

### **vendorCurrency**
- **Type:** String | Null  
- **Required:** No  
- **Description:** Currency of the vendor price.  
- **Default:** Null  
- **Example:** null  

### **tktLimitTime**
- **Type:** String  
- **Required:** Yes  
- **Description:** Ticketing limit time. Format: YYYY-MM-DD HH:MM:SS.  
- **Default:** None  
- **Example:** "2024-05-20 18:24:35"  

### **pnrCode**
- **Type:** String | Null  
- **Required:** No  
- **Description:** The pnrCode is the single reference for the booking. This is the Atlas PNR.
- **Default:** Null  
- **Example:** null  

### **includeExtraBaggage**
- **Type:** Boolean | Null  
- **Required:** No  
- **Description:** Indicates if extra baggage is included.  
- **Default:** Null  
- **Example:** null  

#### **Passenger Object Fields**

##### **name**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's full name in "LASTNAME/FIRSTNAME MIDDLENAME" format.  
- **Default:** None  
- **Example:** "TEST/ONE"  

##### **passengerType**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Passenger type (e.g., 0 for adult).  

  Valid values:
  - 0: ADT
  - 1: CHD
  - 2: INF
- **Default:** None  
- **Example:** "0"  

##### **birthday**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's date of birth. Format: YYYYMMDD.    
- **Default:** None  
- **Example:** "19900101"  

##### **gender**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's gender (e.g., M for male, F for female).

  Valid values:
  - M: male
  - F: female
- **Default:** None  
- **Example:** "M"  

##### **cardNum**
- **Type:** String  
- **Required:** Yes  
- **Description:** Identification document number.  
- **Default:** None  
- **Example:** "00000000"  

##### **cardType**
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of identification document (e.g., PP for passport).  

  Valid values:
  - PP - Passport
  - GA - Hong Kong Macau Pass for China mainland citizens
  - TW - Taiwan Pass for China mainland citizens
  - TB - China mainland pass for Taiwanese
  - HY - International Seaman's Certificate
- **Default:** None  
- **Example:** "PP"  

##### **cardIssuePlace**
- **Type:** String  
- **Required:** Yes  
- **Description:** Country where the identification document was issued.  
- **Default:** None  
- **Example:** "SG"  

##### **cardExpired**
- **Type:** String  
- **Required:** Yes  
- **Description:** Expiry date of the identification document. Format: YYYYMMDD.    
- **Default:** None  
- **Example:** "20301231"  

##### **nationality**
- **Type:** String  
- **Required:** Yes  
- **Description:** Nationality of the passenger.  
- **Default:** None  
- **Example:** "SG"  

##### **contactEmails**
- **Type:** Array of Strings  
- **Required:** No  
- **Description:** Passenger contact email address.  
- **Default:** None  
- **Example:** ["test@test.com"]  

##### **contactPhones**
- **Type:** Array of Strings  
- **Required:** No  
- **Description:** Passenger contact phone number.  
- **Default:** None  
- **Example:** ["0001-87291810"]  

#### **Ancillary Object Fields**

###### **productCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Code identifying the ancillary product.  
- **Default:** None  
- **Example:** "SCI_1PC_19KG"  

###### **segmentIndex**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Segment index to which this ancillary applies.  
- **Default:** None  
- **Example:** "1"  

###### **buyMethod**
- **Type:** String  
- **Required:** Yes  
- **Description:** Purchase method for the ancillary product.  
- **Default:** None  
- **Example:** "0"  

###### **offerId**
- **Type:** String | Null  
- **Required:** No  
- **Description:** Unique identifier for the offer.  
- **Default:** Null  
- **Example:** null  

###### **ancillaryPrice**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Price of the ancillary service.  
- **Default:** None  
- **Example:** "85.51"  

### **currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency of the transaction.  
- **Default:** None  
- **Example:** "USD"  

###### **auxSeatElement**
- **Type:** Object | Null  
- **Required:** No  
- **Description:** Additional details if the product is related to seat selection.  
- **Default:** Null  
- **Example:** null

###### **auxBaggageElement** (Nested Object)
- **Type:** Object  
- **Required:** No  
- **Description:** Additional details if the product is baggage-related.  
- **Default:** None  
- **Example:** See below.  

#### **Baggage Element Fields**

- **piece**  
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of baggage pieces.  

  Valid values:
  - 0：No Limitation about piece;
  - greater than 0：Maximum pieces
- **Default:** None  
- **Example:** "0"  

- **weight**  
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Weight of baggage in kilograms.  
- **Default:** None  
- **Example:** "0"  

- **isAllWeight**  
- **Type:** Boolean  
- **Required:** Yes  
- **Description:** Indicates if the weight is cumulative.  

  Valid values:
  - True: The weight is for all the pieces
  - False: The weight is for each piece
- **Default:** true  
- **Example:** true  

- **size**  
- **Type:** String | Null  
- **Required:** No  
- **Description:** Dimensions of baggage if applicable.  
- **Default:** Null  
- **Example:** null  

### **routing**
- **Type:** String | Null  
- **Required:** No  
- **Description:** Routing details if applicable.  
- **Default:** Null  
- **Example:** null  

### **duplicateOrders**
- **Type:** String | Null  
- **Required:** No  
- **Description:** Indicates duplicate orders if any.  
- **Default:** Null  
- **Example:** null  

### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Response status code.  
- **Default:** None  
- **Example:** "0"  

### **msg**
- **Type:** String | Null  
- **Required:** No  
- **Description:** Message related to the response. The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result. 
- **Default:** Null  
- **Example:** null  

{% endtab %}

{% tab title="Samples" %}
```json
{
    "sessionId": "cde38a72-d7fa-4e5b-9ba5-08b6929143c8",
    "orderNo": "TESTB20240520180835748",
    "originalOrderNo": null,
    "ticketOrderNo": "TESTM20240520171341468",
    "totalPrice": 85.51,
    "totalTransactionFee": 0,
    "currency": "USD",
    "vendorTotalPrice": null,
    "vendorCurrency": null,
    "tktLimitTime": "2024-05-20 18:24:35",
    "pnrCode": null,
    "includeExtraBaggage": null,
    "paxTicketInfos": [
        {
            "name": "TEST/ONE",
            "passengerType": 0,
            "birthday": "19900101",
            "gender": "M",
            "cardNum": "00000000",
            "cardType": "PP",
            "cardIssuePlace": "SG",
            "cardExpired": "20301231",
            "nationality": "SG",
            "ticketNos": [],
            "airlinePNRs": [],
            "contactEmails": [
                "test@test.com"
            ],
            "contactPhones": [
                "0001-87291810"
            ],
            "ancillaries": [
                {
                    "productCode": "SCI_1PC_19KG",
                    "segmentIndex": 1,
                    "buyMethod": "0",
                    "offerId": null,
                    "ancillaryPrice": 85.51,
                    "currency": "USD",
                    "auxSeatElement": null,
                    "auxBaggageElement": {
                        "piece": 0,
                        "weight": 0,
                        "isAllWeight": true,
                        "size": null
                    }
                }
            ]
        }
    ],
    "routing": null,
    "duplicateOrders": null,
    "status": 0,
    "msg": null
}

```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you want to pay for the add-ancillary order, please call the [pay](broken-reference/) function as same as the ticketing orders.
{% endhint %}
