# Ticketing Complete Notification

### Ticket Notification Webhook

Once a ticket is booked, you will receive the `order.ticketed` notification on your server. You can process it and take action as required. For example, you could send a booking confirmation email with ticket details to your customer.

### EndPoint

The URL you configured to receive notifications

Method : Post

{% tabs %}
{% tab title="Schema" %}
##### **cid**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique client identifier.  
- **Constraints:** Must be a valid alphanumeric string.  
- **Default:** None  
- **Example:** "XXXXXXX"  

##### **data**
- **Type:** Object  
- **Required:** Yes  
- **Description:** Contains order details.  
- **Constraints:** Must be a valid JSON object.  
- **Default:** None  

  ##### **orderNo**
  - **Type:** String  
  - **Required:** Yes  
  - **Description:** Unique order number.  
  - **Constraints:** Must be a valid alphanumeric string.  
  - **Default:** None  
  - **Example:** "TESTL20230922153224323"  
  
  ##### **orderStatus**
  - **Type:** Integer  
  - **Required:** Yes  
  - **Description:** Status of the order.  
  - **Constraints:** Must be a valid integer.  
  - **Default:** None  
  - **Example:** `2`  

  ##### **paxTicketInfos**
  - **Type:** Array  
  - **Required:** Yes  
  - **Description:** List of passenger ticket details.  
  - **Constraints:** Must contain valid passenger objects.  
  - **Default:** None  
  
    Each object contains:
    
    - **airlinePNRs** (Array, Required): List of airline PNRs. Example: `["S30814"]`
    - **ancillaries** (Array, Required): List of ancillary services. Example: `[]`
    - **birthday** (String, Required): Passenger birth date in YYYYMMDD format. Example: "20160202"
    - **cardExpired** (String, Required): Expiry date of identification. Example: "20400101"
    - **cardIssuePlace** (String, Required): Country of issue for identification. Example: "CN"
    - **cardNum** (String, Required): Identification number. Example: "123458"
    - **cardType** (String, Required): Type of identification document. Example: "PP"
    - **gender** (String, Required): Passenger gender. Example: "F"
    - **name** (String, Required): Passenger name. Example: "zhang/lisi"
    - **nationality** (String, Required): Passenger nationality. Example: "CN"
    - **passengerType** (Integer, Required): Type of passenger (0 = Adult, 1 = Child, etc.). Example: `1`
    - **ticketNos** (Array, Required): List of ticket numbers. Example: `["S30814"]`
  
##### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Indicates the status of the request. A value of `-1` indicates an issue.  
- **Constraints:** Must be `-1` for error.  
- **Default:** None  
- **Example:** `-1`  

##### **type**
- **Type:** String  
- **Required:** Yes  
- **Description:** Indicates the type of the response.  
- **Constraints:** Must be a valid string.  
- **Default:** None  
- **Example:** "order.ticketed"

{% endtab %}

{% tab title="Samples" %}
```
{
  "cid": "XXXXXXX",
  "data": {
    "orderNo": "TESTL20230922153224323",
    "orderStatus": 2,
    "paxTicketInfos": [
      {
        "airlinePNRs": [
          "S30814"
        ],
        "ancillaries": [],
        "birthday": "20160202",
        "cardExpired": "20400101",
        "cardIssuePlace": "CN",
        "cardNum": "123458",
        "cardType": "PP",
        "gender": "F",
        "name": "zhang/lisi",
        "nationality": "CN",
        "passengerType": 1,
        "ticketNos": [
          "S30814"
        ]
      },
      {
        "airlinePNRs": [
          "S30814"
        ],
        "ancillaries": [],
        "birthday": "19920202",
        "cardExpired": "20400101",
        "cardIssuePlace": "CN",
        "cardNum": "123457",
        "cardType": "PP",
        "gender": "F",
        "name": "li/si",
        "nationality": "CN",
        "passengerType": 0,
        "ticketNos": [
          "S30814"
        ]
      },
      {
        "airlinePNRs": [
          "S30814"
        ],
        "ancillaries": [],
        "birthday": "19910101",
        "cardExpired": "20400101",
        "cardIssuePlace": "CN",
        "cardNum": "123456",
        "cardType": "PP",
        "gender": "M",
        "name": "zhang/san",
        "nationality": "CN",
        "passengerType": 0,
        "ticketNos": [
          "S30814"
        ]
      }
    ]
  },
  "status": -1,
  "type": "order.ticketed"
}

```
{% endtab %}
{% endtabs %}
