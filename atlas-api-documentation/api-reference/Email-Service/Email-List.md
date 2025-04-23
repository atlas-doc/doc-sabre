# Email List

The "Email List" is used to retrieve email in batches.

### Dependency

No preceding function needs to be carried out.

### Endpoint
[https://sandbox.atriptech.com/queryMail.do](https://sandbox.atriptech.com/queryMail.do)

### Request

{% hint style="info" %}

- At least one of the order number, receiving time and/or creation time must be specified for querying.
- You can only query data for up to one month at a time.

{% endhint %}

{% tabs %}
{% tab title="Schema" %}


### **orderNo**
- **Type:** String  
- **Required:** No  
- **Description:** Unique order number used to filter email records linked to a specific order.  
- **Default:** `null`  
- **Example:** `"TESTD20230811113115020"`

### **emailReceivingDateStart**
- **Type:** String  
- **Required:** No  
- **Description:** Start date-time to filter emails based on when they were received. This is the time Atlas received the email. Must be in format `YYYY-MM-DD HH:mm:ss`   
- **Default:** `null`  
- **Example:** `"2022-12-11 18:33:33"`

### **emailReceivingDateEnd**
- **Type:** String  
- **Required:** No  
- **Description:** End date-time to filter emails based on when they were received. This is the time Atlas received the email. Must be in format `YYYY-MM-DD HH:mm:ss`   
 - **Default:** `null`  
- **Example:** `"2022-12-11 18:33:33"`

### **createTimeStart**
- **Type:** String  
- **Required:** No  
- **Description:** Start date-time to filter emails based on system record creation time. Create Time is the time when Atlas created this email record in the Email list. Generally, it will be later than the receiving time. Must be in format `YYYY-MM-DD HH:mm:ss`   
- **Default:** `null`  
- **Example:** `"2022-12-11 18:33:33"`

### **createTimeEnd**
- **Type:** String  
- **Required:** No  
- **Description:** End date-time to filter emails based on system record creation time. Create Time is the time when Atlas created this email record in the Email list. Generally, it will be later than the receiving time. Must be in format `YYYY-MM-DD HH:mm:ss`  
- **Default:** `null`  
- **Example:** `"2022-12-11 18:33:45"`

### **emailCategories**
- **Type:** Array of Strings  
- **Required:** No  
- **Description:** Filters results based on specific email categories (e.g., transaction or marketing types).  

  Valid values:

  - Schedule change
  - Receipt
  - Payment Success
  - Verification
  - Trip Reminder
  - Promo code
  - Travel Itinerary
  - Advertisement
  - PNR Cancellation Success
  - Payment Due
  - Unidentified
  - Duplicated Schedule Change
  - Unaccounted Cancellation
- **Default:** `[]`  
- **Example:** `["Payment Success", "Advertisement"]`

### **pageIndex**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** The current page number for pagination.  
- **Default:** `1`  
- **Example:** `1`

### **pageSize**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of results to return per page. Maximum number=1000 
- **Default:** `100`  
- **Example:** `100`

{% endtab %}


{% tab title="Samples" %}
```
{
  "orderNo": "TESTD20230811113115020",
  "emailReceivingDateStart": "2022-12-11 18:33:33",
  "emailReceivingDateEnd": "2022-12-11 18:33:33",
  "createTimeStart": "2022-12-11 18:33:33",
  "createTimeEnd": "2022-12-11 18:33:45",
  "emailCategories": ["Payment Success","Advertisement"],
  "pageIndex": 1,
  "pageSize": 100
}
```

{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}


### **records**
- **Type:** Array of Objects  
- **Required:** Yes  
- **Description:** List of email records matching the request filters.  
- **Default:** `[]`  
- **Example:**
  ```json
  [
    {
      "orderNo": "TESTD20230811113115020",
      "emailReceivingDate": "2022-12-11 18:33:33",
      "uniqueCode": "2b5435c63102ac28d840b2a54f61e2db",
      "emailCategory": "Unidentified",
      "from": "xiaoyebiao@qq.com",
      "to": "connexpay@mx.theatlas.top",
      "emailSubject": "sda",
      "emailLink": "http://order-oss-sg.oss-ap-southeast-1.aliyuncs.com/2022/12/2b5435c63102ac28d840b2a54f61e2db.eml?...",
      "createTime": "2022-12-11 18:33:45"
    }
  ]
  ```

### **records[].orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique order number associated with the email.  
- **Default:** None  
- **Example:** `"TESTD20230811113115020"`

### **records[].emailReceivingDate**
- **Type:** String  
- **Required:** Yes  
- **Description:** Date and time when the email was received by Atlas. Format: `YYYY-MM-DD HH:mm:ss`   
- **Default:** None  
- **Example:** `"2022-12-11 18:33:33"`

### **records[].uniqueCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier (hash) for the email record.  
- **Default:** None  
- **Example:** `"2b5435c63102ac28d840b2a54f61e2db"`

### **records[].emailCategory**
- **Type:** String  
- **Required:** Yes  
- **Description:** Category assigned to the email. Atlas categorizes emails but does not guarantee accuracy in classification.  

  Valid values:

  - Schedule change
  - Receipt
  - Payment Success
  - Verification
  - Trip Reminder
  - Promo code
  - Travel Itinerary
  - Advertisement
  - PNR Cancellation Success
  - Payment Due
  - Unidentified
  - Duplicated Schedule Change
  - Unaccounted Cancellation
- **Constraints:** Predefined values like `"Payment Success"`, `"Advertisement"`, `"Booking Confirmation"`, or `"Unidentified"`.  
- **Default:** `"Unidentified"`  
- **Example:** `"Unidentified"`

### **records[].from**
- **Type:** String  
- **Required:** Yes  
- **Description:** Email address of the sender.  
- **Default:** None  
- **Example:** `"xiaoyebiao@qq.com"`

### **records[].to**
- **Type:** String  
- **Required:** Yes  
- **Description:** Email address of the receiver.  
- **Default:** None  
- **Example:** `"connexpay@mx.theatlas.top"`

### **records[].emailSubject**
- **Type:** String  
- **Required:** No  
- **Description:** Subject line of the email.  
- **Default:** `""`  
- **Example:** `"sda"`

### **records[].emailLink**
- **Type:** String  
- **Required:** Yes  
- **Description:** Downloadable link to the full email content (EML format). Email Link is only valid for 10 mins.  
- **Default:** None  
- **Example:**  
  `"http://order-oss-sg.oss-ap-southeast-1.aliyuncs.com/2022/12/2b5435c63102ac28d840b2a54f61e2db.eml?..."`

### **records[].createTime**
- **Type:** String  
- **Required:** Yes  
- **Description:** Timestamp when this email record was stored in the system. Format: `YYYY-MM-DD HH:mm:ss`  
- **Default:** None  
- **Example:** `"2022-12-11 18:33:45"`

### **hasNext**
- **Type:** Boolean  
- **Required:** Yes  
- **Description:** Indicates whether more records are available for pagination.  

  Valid values:
  - true: There is a next page
  - false：There is no next page
- **Constraints:** `true` or `false`  
- **Default:** `false`  
- **Example:** `false`

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
  "records": [
    {
      "orderNo": "TESTD20230811113115020",
      "emailReceivingDate": "2022-12-11 18:33:33",
      "uniqueCode": "2b5435c63102ac28d840b2a54f61e2db",
      "emailCategory": "Unidentified",
      "from": "xiaoyebiao@qq.com",
      "to": "connexpay@mx.theatlas.top",
      "emailSubject": "sda",
      "emailLink": "http://order-oss-sg.oss-ap-southeast-1.aliyuncs.com/2022/12/2b5435c63102ac28d840b2a54f61e2db.eml?Expires=1704364782&OSSAccessKeyId=LTAI5tDmTE9iwtNdsqxVXuom&Signature=Hl6vBTM8lv%2Fan%2FFnCVQmQnwaXnk%3D",
      "createTime": "2022-12-11 18:33:45"
    }
  ],
  "hasNext": false,
  "status": 0,
  "msg": "success"
}
```

{% endtab %}
{% endtabs %}



  








