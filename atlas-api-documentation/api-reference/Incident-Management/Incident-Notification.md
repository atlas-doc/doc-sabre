# Incident Notification

### Incident Notification Webhook

In case of any incident, you will receive the incident notification on your server. You can process and notify your affected customers about this incident.

EndPoint ： The URL you configured to receive notifications

Method : Post

{% tabs %}
{% tab title="Schema" %}

### **cid**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique client identifier submitting the email notification event.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"rggat40831"`

### **type**
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of notification event. 
  Valid values:
  - email.schedulechange: Schedule Change-Email Notification
  - abnormal.cancelled: Unacounted Cancellation
  - order.schedulechange: Schedule Change-API Notification. 
- **Constraints:** Must match one of the predefined event types. 
- **Default:** None  
- **Example:** `"email.schedulechange"`

### **notificationId**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the email notification event.  
- **Constraints:** Must be unique across all events.  
- **Default:** None  
- **Example:** `"20230323113246035DNIDD"`

### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Status of the notification event.  
- **Constraints:**  
  - `0` = Success  
  - Non-zero values can indicate error 
- **Default:** `0`  
- **Example:** `0`

### **data**
- **Type:** Object  
- **Required:** Yes  
- **Description:** Contains details of the email content and metadata.  
- **Constraints:** Must include all subfields.  
- **Default:** None  
- **Example:**
  ```json
  {
    "orderNo": "TESTS20230323103458265",
    "emailSubject": "IMPORTANT: Flight delay notice. Confirmation Code KDK7QG",
    "emailLink": "https://theatlas/#/email-detail/4378270"
  }
  ```

#### **data.orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** The order number to which the email notification relates.  
- **Constraints:** Alphanumeric, system-generated.  
- **Default:** None  
- **Example:** `"TESTS20230323103458265"`

#### **data.emailReceivingDate**
- **Type:** String  
- **Required:** Yes  
- **Description:** Date and time when the email was received by Atlas.  
- **Constraints:** Format: `YYYY-MM-DD HH:mm:ss`  
- **Default:** None  
- **Example:** `"2022-12-11 18:33:33"`

#### **data.emailSubject**
- **Type:** String  
- **Required:** Yes  
- **Description:** The subject line of the email that was received.  
- **Constraints:** Free text.  
- **Default:** `""`  
- **Example:** `"IMPORTANT: Flight delay notice. Confirmation Code KDK7QG"`

#### **data.emailLink**
- **Type:** String  
- **Required:** Yes  
- **Description:** URL link to view the full email content in the system.  
- **Constraints:** Must be a valid URL.  
- **Default:** None  
- **Example:** `"https://theatlas/#/email-detail/4378270"`

```
{
    "cid":"rggat40831",
    "type":"email.schedulechange",
    "notificationId":"20230323113246035DNIDD",
    "status":0,
    "data":{
        "orderNo":"TESTS20230323103458265",
        "emailSubject":"IMPORTANT: Flight delay notice. Confirmation Code KDK7QG",
        "emailLink":"https://theatlas/#/email-detail/4378270"
    }
}
```
{% endtab %}
{% endtabs %}
