# Ticketing Complete Notification

### Ticket Notification Webhook

Once a ticket is booked, you will receive the `order.ticketed` notification on your server. You can process it and take action as required. For example, you could send a booking confirmation email with ticket details to your customer.

### EndPoint

The URL you configured to receive notifications

Method : Post

{% tabs %}
{% tab title="Schema" %}
#### **cid**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique client identifier for tracking requests.  
- **Constraints:** Must be a valid alphanumeric string.  
- **Default:** None  
- **Example:** `"XXXXXXX"`

#### **data**  
- **Type:** Object  
- **Required:** Yes  
- **Description:** Contains order-related information.  
- **Constraints:** Must be a valid JSON object.  
- **Default:** None  
- **Example:**  
  ```json
  {
    "orderNo": "TESTL20230922153224323",
    "orderStatus": 2,
    "paxTicketInfos": [ ... ]
  }
  ```

#### **data.orderNo**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique order number associated with the ticket purchase.  
- **Constraints:** Must be a valid order identifier.  
- **Default:** None  
- **Example:** `"TESTL20230922153224323"`

#### **data.orderStatus**  
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Status of the order.  
- **Constraints:**  
  0: Unpaid

  1: Ticketing-in-Process

  2: Ticketed

 -3: Cancelled(When the booking is failed due to the request information) Order number
- **Default:** None  
- **Example:** `2`

#### **data.paxTicketInfos**  
- **Type:** Array of Objects  
- **Required:** Yes  
- **Description:** Contains details of passengers and their associated ticket information.  
- **Constraints:** Must contain at least one valid passenger entry.  
- **Default:** None  

##### **data.paxTicketInfos[]**  
- **Type:** Object  
- **Required:** Yes  
- **Description:** Individual passenger ticket details.  
- **Constraints:** Each entry must be a valid passenger information object.  
- **Example:**  
  ```json
  {
    "name": "zhang/lisi",
    "passengerType": 1,
    "birthday": "20160202",
    "gender": "F",
    "cardNum": "123458",
    "cardType": "PP",
    "cardIssuePlace": "CN",
    "cardExpired": "20400101",
    "nationality": "CN",
    "ticketNos": ["S30814"],
    "airlinePNRs": ["S30814"],
    "ancillaries": []
  }
  ```

##### **data.paxTicketInfos[].name**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger name in standard airline format (SURNAME/GIVENNAME).  
- **Constraints:** Must follow `LASTNAME/FIRSTNAME` format.  
- **Default:** None  
- **Example:** `"zhang/lisi"`

##### **data.paxTicketInfos[].passengerType**  
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Type of passenger.  
- **Constraints:**  
  - `0` = Adult  
  - `1` = Child  
  - `2` = Infant  
- **Default:** None  
- **Example:** `1`

##### **data.paxTicketInfos[].birthday**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's date of birth in `YYYYMMDD` format.  
- **Constraints:** Must be a valid date in the past.  
- **Default:** None  
- **Example:** `"20160202"`

##### **data.paxTicketInfos[].gender**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger gender.  
- **Constraints:** `M` for Male, `F` for Female.  
- **Default:** None  
- **Example:** `"F"`

##### **data.paxTicketInfos[].cardNum**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Identification document number (passport or national ID).
- **Constraints:** Must be a valid alphanumeric string.  
- **Default:** None  
- **Example:** `"123458"`

##### **data.paxTicketInfos[].cardType**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of identification document.  

  Valid values:

  PP - Passport

  GA - Hong Kong Macau Pass for China mainland citizens

  TW - Taiwan Pass for China mainland citizens

  TB - China mainland pass for Taiwanese

  HY - International Seaman's Certificate  
- **Constraints:** As above 
- **Default:** None  
- **Example:** `"PP"`

##### **data.paxTicketInfos[].cardIssuePlace**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Country or authority that issued the identification document.  
- **Constraints:** Must be a valid country code (e.g., `"CN"` for China).  
- **Default:** None  
- **Example:** `"CN"`

##### **data.paxTicketInfos[].cardExpired**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Expiry date of the identification document in `YYYYMMDD` format.  
- **Constraints:** Must be a valid date in the future.  
- **Default:** None  
- **Example:** `"20400101"`

##### **data.paxTicketInfos[].nationality**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger’s nationality using country codes (ISO 3166-1 alpha-2).  
- **Constraints:** Must be a valid country code.  
- **Default:** None  
- **Example:** `"CN"`

##### **data.paxTicketInfos[].ticketNos**  
- **Type:** Array of Strings  
- **Required:** Yes  
- **Description:** List of issued ticket numbers associated with the passenger.  
- **Constraints:** Must contain at least one valid ticket number.  
- **Default:** None  
- **Example:** `["S30814"]`

##### **data.paxTicketInfos[].airlinePNRs**  
- **Type:** Array of Strings  
- **Required:** Yes  
- **Description:** List of Passenger Name Record (PNR) codes.  
- **Constraints:** Must contain at least one valid PNR.  
- **Default:** None  
- **Example:** `["S30814"]`

##### **data.paxTicketInfos[].ancillaries**  
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of ancillary services associated with the passenger (e.g., extra baggage, seat selection).  
- **Constraints:** Can be empty if no ancillaries are purchased.  
- **Default:** `[]`  
- **Example:** `[]`

#### **status**  
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Indicates the response status.  
- **Constraints:** -1 indicates an error or inactive status.  
- **Default:** None  
- **Example:** `-1`

#### **type**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Specifies the type of response message.  
- **Constraints:** Must be a valid response type string.  
- **Default:** None  
- **Example:** `"order.ticketed"`

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
