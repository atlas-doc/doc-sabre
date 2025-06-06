# Order List

To get a list of orders as per the parameters entered.

### Dependency

No preceding function needs to be called before 'orderList' API.

### Endpoint {% debug uid="orderList_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/orderList.do](https://sandbox.atriptech.com/orderList.do)

{% hint style="info" %}
The "Order List" API is a feature which lists the orders which have been created on the Atlas platform. After receiving the response, the customer can access individual order by using the queryOrderDetails.do API.

Points to note:

•	All the parameters are optional.

•	Orders in all statuses can be queried.

•	Orders with departure time within 1 year can be retrieved.

•	The time format which is UTC.
{% endhint %}

## Request

{% tabs %}
{% tab title="Schema" %}

### **orderNo**
- **Type:** String  
- **Required:** No  
- **Description:** The unique identifier for the order. Must be a valid order number issued by the system.    
- **Default:** None  
- **Example:** "ZNMKU20220119160129691"

### **airlinePNRs**
- **Type:** Array of Strings  
- **Required:** No  
- **Description:** The airline PNR received in the querryOrderDetails.do response. Please note that this is different from the "PNRCode" element. E.g.: ["FT759J", "8HFT67"] 
- **Default:** None  
- **Example:** `["FT759J", "8HFT67"]`

### **paxName**
- **Type:** String  
- **Required:** No  
- **Description:** Name of the passenger. Format: last name/first name
- **Default:** Empty string  
- **Example:** "Doe/John"

### **contactEmail**
- **Type:** String  
- **Required:** No  
- **Description:** Contact email of the passenger as entered in the order.do request. 
- - **Default:** Empty string  
- **Example:** "johndoe@example.com"

### **fromCity**
- **Type:** String  
- **Required:** No  
- **Description:** Departure city.  
- **Default:** Empty string  
- **Example:** "NYC"

### **toCity**
- **Type:** String  
- **Required:** No  
- **Description:** Destination city.  
- **Default:** Empty string  
- **Example:** "LAX"

### **depDate**
- **Type:** String  
- **Required:** No  
- **Description:** Departure date in `YYYYMMDD` format.  
- **Default:** None  
- **Example:** "20240101"

### **createTimeRangeFrom**
- **Type:** String  
- **Required:** No  
- **Description:** The start time of order creation. This is in UTC. Format: yyyy-MM-dd'T'HH:mm:ss'Z' E.g.: 2024-10-31T19:57:46Z
- **Default:** None  
- **Example:** "2024-10-31T19:57:46Z"

### **createTimeRangeTo**
- **Type:** String  
- **Required:** No  
- **Description:** The end time of order creation. This is in UTC. Format: yyyy-MM-dd'T'HH:mm:ss'Z' E.g.: 2024-10-31T19:57:46Z
- **Default:** None  
- **Example:** "2024-11-01T19:57:46Z"

### **orderStatus**
- **Type:** Array of Integers  
- **Required:** No  
- **Description:** List of possible order statuses.  

  Valid values:
  - 0: Unpaid
  - 1: Ticketing
  - 2: Ticketed
  - 3: Cancelled
- **Default:** None  
- **Example:** `[0, 1, 2, -3]`

### **airlines**
- **Type:** Array of Strings  
- **Required:** No  
- **Description:** List of airline codes.  
- **Default:** None  
- **Example:** `["FR"]`

### **page**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Page number for paginated results.  
- **Default:** `1`  
- **Example:** `1`

### **pageSize**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of records per page. Default: 20 Maximum: 100
- **Default:** `20`  
- **Example:** `20`
    
{% endtab %}

{% tab title="Samples" %}
```
{
  "orderNo": "",
  "airlinePNRs": [
    "FT759J",
    "8HFT67"
  ],
  "paxName": "",
  "contactEmail": "",
  "fromCity": "",
  "toCity": "",
  "depDate": "20240101",
  "createTimeRangeFrom": "2024-10-31T19:57:46Z",
  "createTimeRangeTo": "2024-11-01T19:57:46Z",
  "orderStatus": [
    0,
    1,
    2,
    -3
  ],
  "airlines": [
    "FR"
  ],
  "page": 1,
  "pageSize": 20
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
- **Description:** Unique identifier for the order.  
- **Default:** None  
- **Example:** "TESTA20241122090710695"  

### **pnrCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** PAtlas internal reference code. E.g.: "Z44IPS" 
- **Default:** None  
- **Example:** "Z27T5B"  

### **airlinePNRs**
- **Type:** Array of Strings  
- **Required:** Yes  
- **Description:** The airline PNR received in the querryOrderDetails.do response. Please note that this is different from the "PNRCode" element. E.g.: ["FT759J", "8HFT67"]
- **Default:** None  
- **Example:** ["S86745"]  

### **orderStatus**
- **Type:** Array of Integers  
- **Required:** No  
- **Description:** List of possible order statuses.  

  Valid values:
  - 0: Unpaid
  - 1: Ticketing
  - 2: Ticketed
  - 3: Cancelled
- **Default:** None  
- **Example:** `[0, 1, 2, -3]`

### **travelStartDate**
- **Type:** String | Null  
- **Required:** No  
- **Description:** Start date of travel if available.  
- **Default:** Null  
- **Example:** null  

### **airlines**
- **Type:** Array of Strings  
- **Required:** Yes  
- **Description:** List of airline codes.  
- **Default:** None  
- **Example:** ["SL"]  

### **orderCreateTimestamp**
- **Type:** String  
- **Required:** Yes  
- **Description:** Timestamp when the order was created. Format: yyyy-MM-dd'T'HH:mm:ss'Z'. 
- **Default:** None  
- **Example:** "2024-11-22T01:07:10Z"  

### **paymentTimestamp**
- **Type:** String  
- **Required:** Yes  
- **Description:** Timestamp when payment was completed. Format: yyyy-MM-dd'T'HH:mm:ss'Z'.  
- **Default:** None  
- **Example:** "2024-11-22T01:07:11Z"  

### **paxNames**
- **Type:** Array of Strings  
- **Required:** Yes  
- **Description:** List of passenger names in "LASTNAME/FIRSTNAME" format.  
- **Default:** None  
- **Example:** ["YIJING/tFGo"]  

### **contactEmail**
- **Type:** String  
- **Required:** Yes  
- **Description:** The email as entered in the order.do request.   
- **Default:** None  
- **Example:** "test@test.com"  

### **fromCity**
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure city (IATA code).  
- **Default:** None  
- **Example:** "CNX"  

### **toCity**
- **Type:** String  
- **Required:** Yes  
- **Description:** Destination city (IATA code).  
- **Default:** None  
- **Example:** "BKK"  

### **errorCode**
- **Type:** String 
- **Required:** No  
- **Description:** The error code returned for a cancelled order. This will only be displayed for cancelled orders.
- **Default:** Null  
- **Example:** null  

### **errorMessage**
- **Type:** String  
- **Required:** No  
- **Description:** Error message if applicable.  
- **Default:** Null  
- **Example:** null  

### **page**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Current page number.  
- **Default:** 1  
- **Example:** 1  

### **pageSize**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of records per page.  
- **Default:** 20  
- **Example:** 20  

### **totalRecords**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Total number of records available.  
- **Default:** None  
- **Example:** 2  

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
```
{
    "orders": [
        {
            "orderNo": "TESTA20241122090710695",
            "pnrCode": "Z27T5B",
            "airlinePNRs": [
                "S86745"
            ],
            "orderStatus": 2,
            "travelStartDate": null,
            "airlines": [
                "SL"
            ],
            "orderCreateTimestamp": "2024-11-22T01:07:10Z",
            "paymentTimestamp": "2024-11-22T01:07:11Z",
            "paxNames": [
                "YIJING/tFGo"
            ],
            "contactEmail": "test@test.com",
            "fromCity": "CNX",
            "toCity": "BKK",
            "errorCode": null,
            "errorMessage": null
        },
        {
            "orderNo": "TESTA20241122080618700",
            "pnrCode": "LLQNYJ",
            "airlinePNRs": [
                "S79170|S79170"
            ],
            "orderStatus": 2,
            "travelStartDate": null,
            "airlines": [
                "TF"
            ],
            "orderCreateTimestamp": "2024-11-22T00:06:18Z",
            "paymentTimestamp": "2024-11-22T00:06:19Z",
            "paxNames": [
                "YIJING/gAMM",
                "JIXING/gAMM"
            ],
            "contactEmail": "test@test.com",
            "fromCity": "VBY",
            "toCity": "STO",
            "errorCode": null,
            "errorMessage": null
        }
    ],
    "page": 1,
    "pageSize": 20,
    "totalRecords": 2,
    "status": 0,
    "msg": null
}
```
{% endtab %}
{% endtabs %}
