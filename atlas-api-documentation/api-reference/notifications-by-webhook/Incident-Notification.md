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
- **Description:** Unique client identifier for tracking the request.  
- **Constraints:** Must be a valid alphanumeric string.  
- **Example:** `"xxxxxxxxxx"`

### **type**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Incident type.  

  Valid values:

  email.schedulechange: Schedule Change-Email Notification

  abnormal.cancelled: Unaccounted Cancellation

  order.schedulechange: Schedule Change-API Notification
- **Constraints:** Must be `"email.schedulechange"`.  
- **Example:** `"email.schedulechange"`

### **notificationId**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the notification event.  
- **Constraints:** Must be a valid alphanumeric string.  
- **Example:** `"20230323113246035DNIDD"`

### **status**  
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Incident status.

  Valid values:

  0: Unconfirmed 

  1: Confirmed  
- **Constraints:** None   
- **Example:** `0`

### **data**  
- **Type:** Object  
- **Required:** Yes  
- **Description:** Contains details of the email notification related to the schedule change.  

#### **data.orderNo**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique order number associated with the flight booking.  
- **Constraints:** Must be a valid order identifier.  
- **Example:** `"TESTS20230323103458265"`

#### **data.emailSubject**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Subject line of the email notification sent to the customer.  
- **Constraints:** Must be a valid text string.  
- **Example:** `"IMPORTANT: Flight delay notice. Confirmation Code KDK7QG"`

#### **data.emailLink**  
- **Type:** String (URL)  
- **Required:** Yes  
- **Description:** Direct link to the email details page for further information.  
- **Constraints:** Must be a valid URL.  
- **Example:** `"https://theatlas/#/email-detail/4378270"`

{% endtab %}
      
{% tab title="Samples" %}
**Schedule Change-Email Notification**

```
{
    "cid":"xxxxxxxxxx",
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

> **Tip**: The customer’s server URL needs to be registered with Atlas to receive notifications via webhook.

This can be done via API as shown below:

```
{

    "cid": "XXXXXXXX",
    
    "url": "https://xxx.com/xxxx"
    
}
```
The registration can also be done via ATRIP in the “Customer Information” tab of the “My Profile” menu.

Receiving notifications:

Three types of Incident notifications will be received. They are:

a. [Schedule Change – Email Notification]
Any schedule change email notification received from the airline using Atlas generated email id.

Sample:

```
{

    "cid":"xxxxxxxxxx",

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
Please note that the email link has a validity period of 10 minutes. The data received in the email will need to be stored at the customer’s end.


b. [Schedule Change - API Notification]

Structured Notification of Schedule Change. Information on old and new flights.

Sample:

```
{

  "cid": "xxxxxxxxxx",

  "data": {

    "orderNo": "XCEWF20221203094515954",

    "previousSegs": [

      {

        "arrAirport": "DPS",

        "arrTerminal": "",

        "arrTime": "2023-01-24 10:35:00",

        "carrier": "IU",

        "codeShare": false,

        "depAirport": "CGK",

        "depTerminal": "",

        "depTime": "2023-01-24 07:45:00",

        "flightNumber": "IU740"

      },

      {

        "arrAirport": "CGK",

        "arrTerminal": "",

        "arrTime": "2023-04-24 16:05:00",

        "carrier": "IU",

        "codeShare": false,

        "depAirport": "DPS",

        "depTerminal": "",

        "depTime": "2023-04-24 15:15:00",

        "flightNumber": "IU759"

      }

    ],

    "revisedSegs": [

      {

        "arrAirport": "CGK",

        "arrTerminal": "",

        "arrTime": "2023-04-24 16:05:00",

        "carrier": "IU",

        "codeShare": false,

        "depAirport": "DPS",

        "depTerminal": "",

        "depTime": "2023-04-24 15:15:00",

        "flightNumber": "IU743"

      }

    ],

    "scheduleChangeType": 1

  },

  "notificationId": "20230424050252711WZDMB",

  "status": 0,

  "type": "order.schedulechange"

}
```
c. [Unaccounted Cancellation]

These are cancellations made by our customers, airlines or passengers themselves. This info will be sent to the customers to confirm the same and inform the customer, if necessary.

Sample:

```
{

  "cid": "xxxxxxxxxx",

  "data": {

    "orderNo": "RQWUV20230617185232880",

    "vendorRefundInformation": "FULLY"

  },

  "notificationId": "20230906014000568DRLNX",

  "status": 0,

  "type": "abnormal.cancelled"

}
```
