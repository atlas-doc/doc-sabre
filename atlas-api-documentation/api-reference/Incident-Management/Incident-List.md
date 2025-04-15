# Incident List

The "Incident List" is used to retrieve incidents in batches.

### Dependency

No preceding function needs to be carried out.

### Endpoint
[https://sandbox.atriptech.com/event/getPageList.do](https://sandbox.atriptech.com/event/getPageList.do)

### Request

{% tabs %}
{% tab title="Schema" %}

### **eventId**
- **Type:** String  
- **Required:** No  
- **Description:** Unique identifier for the event (Incident ID).  
- **Constraints:** Alphanumeric string, can be empty to fetch all.  
- **Default:** `""`  
- **Example:** `""`

### **orderNo**
- **Type:** String  
- **Required:** No  
- **Description:** Order number associated with the event.  
- **Constraints:** Alphanumeric format.  
- **Default:** `""`  
- **Example:** `"ORD20230811113115020"`

### **eventType**
- **Type:** String  
- **Required:** No  
- **Description:** Type of the event (e.g., `scheduleChange`, `ticketed`, `cancelled`).  
  Valid values:
  - email.schedulechange: Schedule Change-Email Notification
  - abnormal.cancelled: Unacounted Cancellation
  - order.schedulechange: Schedule Change-API Notification.
- **Constraints:** Must match supported event type codes.  
- **Default:** `""`  
- **Example:** `"scheduleChange"`

### **eventStatus**
- **Type:** Array of Integers  
- **Required:** No  
- **Description:** List of status codes to filter events.  
  Valid values:
  - 0: Unconfirmed 
  - 1: Confirmed
- **Constraints:**  None
- **Default:** `[]`  
- **Example:** `[0, 1]`

### **airline**
- **Type:** String  
- **Required:** No  
- **Description:** IATA code of the airline related to the event.  
- **Constraints:** Must be a valid 2-letter IATA airline code.  
- **Default:** `""`  
- **Example:** `"W4"`

### **eventTimeStart**
- **Type:** String  
- **Required:** No  
- **Description:** Start time of the event search window.  
- **Constraints:** Must be in format `YYYY-MM-DD HH:mm:ss`  
- **Default:** `null`  
- **Example:** `"2023-04-01 00:00:00"`

### **eventTimeEnd**
- **Type:** String  
- **Required:** No  
- **Description:** End time of the event search window.  
- **Constraints:** Must be in format `YYYY-MM-DD HH:mm:ss`  
- **Default:** `null`  
- **Example:** `"2023-05-01 00:00:00"`

### **depTimeStart**
- **Type:** String or Null  
- **Required:** No  
- **Description:** Optional filter for departure time start.  
- **Constraints:** Must be `null` or a valid timestamp in `YYYY-MM-DD HH:mm:ss` format.  
- **Default:** `null`  
- **Example:** `null`

### **depTimeEnd**
- **Type:** String or Null  
- **Required:** No  
- **Description:** Optional filter for departure time end.  
- **Constraints:** Must be `null` or a valid timestamp in `YYYY-MM-DD HH:mm:ss` format.  
- **Default:** `null`  
- **Example:** `null`

### **pageIndex**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Page number for pagination.  
- **Constraints:** Must be ≥ 1  
- **Default:** `1`  
- **Example:** `1`

### **pageSize**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of results to return per page.  
- **Constraints:** Must be ≥ 1 and ≤ 1000  
- **Default:** `100`  
- **Example:** `100`

{% endtab %}


{% tab title="Samples" %}
**Unaccounted Cancellation Confirm **
```
{
    "eventId":"",
    "orderNo":"",
    "eventType":"",
    "eventStatus":[0,1],
    "airline":"",
    "eventTimeStart":"2023-04-01 00:00:00",
    "eventTimeEnd":"2023-05-01 00:00:00",
    "depTimeStart":null,
    "depTimeEnd":null,
    "pageIndex":1,
    "pageSize":100
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
- **Description:** List of event records matching the query criteria.  
- **Constraints:** Can be empty if no records found.  
- **Default:** `[]`  
- **Example:** `[ { ... } ]`

### **records[].eventId**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier of the event (Incident Id).  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"20230401003644225YJQGR"`

### **records[].orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Primary order number associated with the event.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"HCNMN20230227142411968"`

### **records[].subOrderNo**
- **Type:** String  
- **Required:** No  
- **Description:** Sub-order number associated with a specific itinerary or passenger.  
- **Constraints:** Alphanumeric string, may include underscore (`_`).  
- **Default:** None  
- **Example:** `"HCNMN20230227142411968_1"`

### **records[].eventType**
- **Type:** String  
- **Required:** No  
- **Description:** Type of the event (e.g., `scheduleChange`, `ticketed`, `cancelled`).  
  Valid values:
  - email.schedulechange: Schedule Change-Email Notification
  - abnormal.cancelled: Unacounted Cancellation
  - order.schedulechange: Schedule Change-API Notification.
- **Constraints:** Must match supported event type codes.  
- **Default:** `""`  
- **Example:** `"scheduleChange"`

### **records[].eventStatus**
- **Type:** Array of Integers  
- **Required:** No  
- **Description:** List of status codes to filter events.  
  Valid values:
  - 0: Unconfirmed 
  - 1: Confirmed
- **Constraints:**  None
- **Default:** `[]`  
- **Example:** `[0, 1]`

### **records[].eventTime**
- **Type:** String  
- **Required:** Yes  
- **Description:** Incident receiving time. UTC+08:00
- **Constraints:** Format: `MMM d, yyyy hh:mm:ss A`  
- **Default:** None  
- **Example:** `"Apr 1, 2023 12:36:44 AM"`

### **records[].extraInfo**
- **Type:** String  
- **Required:** No  
- **Description:** Additional metadata or reference ID related to the event.  
- **Constraints:** Optional string.  
- **Default:** `null`  
- **Example:** `"4775822"`

### **records[].confirmedResult**
- **Type:** String or Null  
- **Required:** No  
- **Description:** Incident Reason. Schedule Change Type & Cancelled Type.
- **Constraints:** Can be `null` or free-text string.  
- **Default:** `null`  
- **Example:** `null`

### **records[].confirmedRemark**
- **Type:** String or Null  
- **Required:** No  
- **Description:** Remarks provided during confirmation.  
- **Constraints:** Can be `null` or any free-text comment.  
- **Default:** `null`  
- **Example:** `null`

### **records[].clientCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Identifier for the client.
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"TAC00001"`

### **records[].createTime**
- **Type:** String  
- **Required:** Yes  
- **Description:** Incident create time. UTC+08:00 
- **Constraints:** Format: `MMM d, yyyy hh:mm:ss A`  
- **Default:** None  
- **Example:** `"Apr 1, 2023 12:36:44 AM"`

### **records[].updateIme** (Note: Likely a typo; should be `updateTime`)
- **Type:** String  
- **Required:** Yes  
- **Description:** Timestamp of the last update to the event record. UTC+08:00  
- **Constraints:** Format: `MMM d, yyyy hh:mm:ss A`  
- **Default:** None  
- **Example:** `"Apr 1, 2023 12:36:44 AM"`

### **records[].airline**
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA airline code associated with the event.  
- **Constraints:** 2-letter IATA code.  
- **Default:** None  
- **Example:** `"F9"`

### **records[].depTime**
- **Type:** String  
- **Required:** No  
- **Description:** Scheduled departure time for the affected flight.  
- **Constraints:** Format: `MMM d, yyyy hh:mm:ss A`  
- **Default:** None  
- **Example:** `"Mar 31, 2023 11:12:00 AM"`

### **records[].confirmTime**
- **Type:** String or Null  
- **Required:** No  
- **Description:** Timestamp when the event was confirmed.  
- **Constraints:** Same as above format or `null`.  
- **Default:** `null`  
- **Example:** `null`

### **records[].confirmUsr**
- **Type:** String or Null  
- **Required:** No  
- **Description:** Username or system that confirmed the event.  
- **Constraints:** Alphanumeric string or `null`.  
- **Default:** `null`  
- **Example:** `null`

### **records[].notified**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Sent the notification or not.  
  Valid values:
  - 1: YES. 
  - 0: No
- **Constraints:** None
- **Default:** `0`  
- **Example:** `1`

### **records[].pnr**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger Name Record (PNR) associated with the booking.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"G7ZNW5"`

### **records[].paxName**
- **Type:** String  
- **Required:** Yes  
- **Description:** Comma-separated list of passenger names.  
- **Constraints:** Free-text.  
- **Default:** None  
- **Example:** `"SOWERS/REBECCA MUSETTA,STEPHENS/DAVID JEROME"`

### **records[].paxEmail**
- **Type:** String  
- **Required:** Yes  
- **Description:** Email address used to notify passengers.  
- **Constraints:** Valid email format.  
- **Default:** None  
- **Example:** `"GeraldineDushkin2005@ttjipiao.top"`
    
{% endtab %}

{% tab title="Samples" %}
```
{
    "records": [
        {
            "eventId": "20230401003644225YJQGR",
            "orderNo": "HCNMN20230227142411968",
            "subOrderNo": "HCNMN20230227142411968_1",
            "eventType": "email.schedulechange",
            "eventStatus": 0,
            "eventTime": "Apr 1, 2023 12:36:44 AM",
            "extraInfo": "4775822",
            "confirmedResult": null,
            "confirmedRemark": null,
            "clientCode": "TAC00001",
            "createTime": "Apr 1, 2023 12:36:44 AM",
            "updateIme": "Apr 1, 2023 12:36:44 AM",
            "airline": "F9",
            "depTime": "Mar 31, 2023 11:12:00 AM",
            "confirmTime": null,
            "confirmUsr": null,
            "notified": 1,
            "pnr": "G7ZNW5",
            "paxName": "SOWERS/REBECCA MUSETTA,STEPHENS/DAVID JEROME",
            "paxEmail": "GeraldineDushkin2005@ttjipiao.top"
        },
    …
    ]
}
```
{% endtab %}
{% endtabs %}
