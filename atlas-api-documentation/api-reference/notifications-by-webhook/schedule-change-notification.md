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
- **Description:** Client identifier associated with the order.
- **Constraints:** Must be a valid alphanumeric string.
- **Default:** None
- **Example:** "XXXXXXX"

#### **data**
- **Type:** Object
- **Required:** Yes
- **Description:** Contains detailed information about the order and schedule changes.
- **Constraints:** Must be a valid JSON object.
- **Default:** None

##### **orderNo**
- **Type:** String
- **Required:** Yes
- **Description:** Unique identifier for the order.
- **Constraints:** Must be a valid order number.
- **Default:** None
- **Example:** "ATXFQ20230720193244809"

##### **previousSegs**
- **Type:** Array of Objects
- **Required:** Yes
- **Description:** List of previous flight segments before the schedule change.
- **Constraints:** Must contain at least one flight segment.
- **Default:** None

###### **Flight Segment Fields**

- **arrAirport** (String): Arrival airport code. Example: "SGN"
- **arrTerminal** (String): Arrival terminal information. Example: ""
- **arrTime** (String): Arrival time in format "YYYY-MM-DD HH:mm:ss". Example: "2023-07-24 21:30:00"
- **carrier** (String): Airline carrier code. Example: "VJ"
- **codeShare** (Boolean): Indicates if the flight is a codeshare flight. Example: `false`
- **depAirport** (String): Departure airport code. Example: "HKG"
- **depTerminal** (String): Departure terminal information. Example: ""
- **depTime** (String): Departure time in format "YYYY-MM-DD HH:mm:ss". Example: "2023-07-24 19:50:00"
- **flightNumber** (String): Flight number. Example: "VJ877"

##### **revisedSegs**
- **Type:** Array of Objects
- **Required:** Yes
- **Description:** List of updated flight segments after the schedule change.
- **Constraints:** Must contain at least one revised flight segment.
- **Default:** None

- ###### **Flight Segment Fields**

- **arrAirport** (String): Arrival airport code. Example: "SGN"
- **arrTerminal** (String): Arrival terminal information. Example: ""
- **arrTime** (String): Arrival time in format "YYYY-MM-DD HH:mm:ss". Example: "2023-07-24 21:30:00"
- **carrier** (String): Airline carrier code. Example: "VJ"
- **codeShare** (Boolean): Indicates if the flight is a codeshare flight. Example: `false`
- **depAirport** (String): Departure airport code. Example: "HKG"
- **depTerminal** (String): Departure terminal information. Example: ""
- **depTime** (String): Departure time in format "YYYY-MM-DD HH:mm:ss". Example: "2023-07-24 19:50:00"
- **flightNumber** (String): Flight number. Example: "VJ877"

##### **scheduleChangeType**
- **Type:** Integer
- **Required:** Yes
- **Description:** Type of schedule change.
- **Constraints:** Must be an integer representing a valid schedule change type.
- **Default:** None
- **Example:** `1`

#### **notificationId**
- **Type:** String
- **Required:** Yes
- **Description:** Unique identifier for the notification event.
- **Constraints:** Must be a valid alphanumeric string.
- **Default:** None
- **Example:** "20230917143240511TATVO"

#### **status**
- **Type:** Integer
- **Required:** Yes
- **Description:** Status of the notification.
- **Constraints:** `0` indicates success, other values indicate errors.
- **Default:** `0`
- **Example:** `0`

#### **type**
- **Type:** String
- **Required:** Yes
- **Description:** Type of notification event.
- **Constraints:** Must be a valid event type string.
- **Default:** None
- **Example:** "order.schedulechange"

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
