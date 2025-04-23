# Schedule Change Notification

### Schedule Change Notification Webhook

In case of flight schedule changes, you will receive the `order.schedulechange` notification on the server, you can process and notify your affected customers about this change.

EndPoint ： The URL you configured to receive notifications

Method : Post

{% tabs %}
{% tab title="Schema" %}
#### **cid**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique client identifier for tracking requests.  
- **Default:** None  
- **Example:** `"XXXXXXX"`

#### **data**  
- **Type:** Object  
- **Required:** Yes  
- **Description:** Contains order-related details, including previous and revised flight segments.  
- **Default:** None  
- **Example:**  
  ```json
  {
    "orderNo": "ATXFQ20230720193244809",
    "previousSegs": [ ... ],
    "revisedSegs": [ ... ],
    "scheduleChangeType": 1
  }
  ```

#### **data.orderNo**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique order number associated with the flight booking.  
- **Default:** None  
- **Example:** `"ATXFQ20230720193244809"`

#### **data.previousSegs**  
- **Type:** Array of Objects  
- **Required:** Yes  
- **Description:** Contains details of the original flight segments before any schedule change.  
- **Default:** None  

##### **data.previousSegs[]**  
- **Type:** Object  
- **Required:** Yes  
- **Description:** Individual flight segment details before the schedule change.  
- **Example:**  
  ```json
  {
    "depAirport": "HKG",
    "arrAirport": "SGN",
    "depTime": "2023-07-24 19:50:00",
    "arrTime": "2023-07-24 21:30:00",
    "carrier": "VJ",
    "flightNumber": "VJ877",
    "codeShare": false,
    "depTerminal": "",
    "arrTerminal": ""
  }
  ```

##### **data.previousSegs[].depAirport**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure airport code (IATA).  
- **Default:** None  
- **Example:** `"HKG"`

##### **data.previousSegs[].arrAirport**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Arrival airport code (IATA).  
- **Default:** None  
- **Example:** `"SGN"`

##### **data.previousSegs[].depTime**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure time in `YYYY-MM-DD HH:MM:SS` format.  
- **Default:** None  
- **Example:** `"2023-07-24 19:50:00"`

##### **data.previousSegs[].arrTime**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Arrival time in `YYYY-MM-DD HH:MM:SS` format.  
- **Default:** None  
- **Example:** `"2023-07-24 21:30:00"`

##### **data.previousSegs[].carrier**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Airline carrier code.  
- **Default:** None  
- **Example:** `"VJ"`

##### **data.previousSegs[].flightNumber**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Flight number assigned by the airline.  
- **Default:** None  
- **Example:** `"VJ877"`

##### **data.previousSegs[].codeShare**  
- **Type:** Boolean  
- **Required:** Yes  
- **Description:** Indicates if the flight is a codeshare.

  Valid values:
  - `true` = Codeshare flight
  - `false` = Not a codeshare flight.  
- **Default:** `false`  
- **Example:** `false`

##### **data.previousSegs[].depTerminal**  
- **Type:** String  
- **Required:** No  
- **Description:** Departure terminal information.  
- **Default:** `""`  
- **Example:** `""`

##### **data.previousSegs[].arrTerminal**  
- **Type:** String  
- **Required:** No  
- **Description:** Arrival terminal information.  
- **Default:** `""`  
- **Example:** `""`

#### **data.revisedSegs**  
- **Type:** Array of Objects  
- **Required:** Yes  
- **Description:** Contains details of the flight segments after the schedule change.  
- **Default:** None  

##### **data.revisedSegs[]**  
- **Type:** Object  
- **Required:** Yes  
- **Description:** Individual flight segment details after the schedule change.  
- **Example:**  
  ```json
  {
    "depAirport": "SGN",
    "arrAirport": "HKG",
    "depTime": "2023-10-19 15:10:00",
    "arrTime": "2023-10-19 18:50:00",
    "carrier": "VJ",
    "flightNumber": "VJ876",
    "codeShare": false,
    "depTerminal": "",
    "arrTerminal": ""
  }
  ```

#### **data.scheduleChangeType**  
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Type of schedule change.  

  Valid values:
  - 1: Schedule change
  - 2: Flight cancel
- **Default:** None  
- **Example:** `1`

#### **notificationId**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the notification event.  
- **Default:** None  
- **Example:** `"20230917143240511TATVO"`

#### **status**  
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Incident staus.  

  Valid values:
  - 0: Unconfirmed
  - 1: Confirmed  
- **Default:** None  
- **Example:** `0`

#### **type**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Notification type.  
- **Default:** None  
- **Example:** `"order.schedulechange"`
{% endtab %}

{% tab title="Samples" %}
**Schedule change with alternative flights**

```
{
    "cid":"XXXXXXX",
    "data":{
        "orderNo":"ATXFQ20230720193244809",
        "previousSegs":[
            {
                "arrAirport":"SGN",
                "arrTerminal":"",
                "arrTime":"2023-07-24 21:30:00",
                "carrier":"VJ",
                "codeShare":false,
                "depAirport":"HKG",
                "depTerminal":"",
                "depTime":"2023-07-24 19:50:00",
                "flightNumber":"VJ877"
            },
            {
                "arrAirport":"HKG",
                "arrTerminal":"",
                "arrTime":"2023-10-18 18:50:00",
                "carrier":"VJ",
                "codeShare":false,
                "depAirport":"SGN",
                "depTerminal":"",
                "depTime":"2023-10-18 14:55:00",
                "flightNumber":"VJ876"
            }
        ],
        "revisedSegs":[
            {
                "arrAirport":"SGN",
                "arrTerminal":"",
                "arrTime":"2023-07-24 21:30:00",
                "carrier":"VJ",
                "codeShare":false,
                "depAirport":"HKG",
                "depTerminal":"",
                "depTime":"2023-07-24 19:50:00",
                "flightNumber":"VJ877"
            },
            {
                "arrAirport":"HKG",
                "arrTerminal":"",
                "arrTime":"2023-10-19 18:50:00",
                "carrier":"VJ",
                "codeShare":false,
                "depAirport":"SGN",
                "depTerminal":"",
                "depTime":"2023-10-19 15:10:00",
                "flightNumber":"VJ876"
            }
        ],
        "scheduleChangeType":1
    },
    "notificationId":"20230917143240511TATVO",
    "status":0,
    "type":"order.schedulechange"
}

```

**Flight cancellation without alternative flight**

```
{
    "cid":"XXXXXXX",
    "data":{
        "orderNo":"ATXFQ20230720193244809",
        "previousSegs":[
            {
                "arrAirport":"SGN",
                "arrTerminal":"",
                "arrTime":"2023-07-24 21:30:00",
                "carrier":"VJ",
                "codeShare":false,
                "depAirport":"HKG",
                "depTerminal":"",
                "depTime":"2023-07-24 19:50:00",
                "flightNumber":"VJ877"
            },
            {
                "arrAirport":"HKG",
                "arrTerminal":"",
                "arrTime":"2023-10-18 18:50:00",
                "carrier":"VJ",
                "codeShare":false,
                "depAirport":"SGN",
                "depTerminal":"",
                "depTime":"2023-10-18 14:55:00",
                "flightNumber":"VJ876"
            }
        ],
        "revisedSegs":[
        ],
        "scheduleChangeType":2
    },
    "notificationId":"20230917143240511TATVO",
    "status":0,
    "type":"order.schedulechange"
}

```
{% endtab %}
{% endtabs %}
