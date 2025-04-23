# Schedule Change-Email Notification

### Dependency

No preceding function needs to be carried out.

### Endpoint

[https://sandbox.atriptech.com/event/confirmEmailScheduleChangeEvent.do](https://sandbox.atriptech.com/event/confirmEmailScheduleChangeEvent.do)

### Request

{% tabs %}
{% tab title="Schema" %}


#### `eventId`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Unique identifier of the schedule change event.  
- **Default:** `null`  
- **Example:** `"20230323113246035DNIDD"`

#### `result`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Action taken in response to the schedule change.  
  Valid values:
  - FLIGHT_CHANGE: Flight Change  
  - FLIGHT_CANCELED: Flight Cancelled
  - NO_SCHEDULE_CHANGE: No Schedule Change 
- **Default:** `null`  
- **Example:** `"FLIGHT_CHANGE"`

#### `remark`
- **Type:** `string`  
- **Required:** No  
- **Description:** Optional remark or comment associated with the result.  
- **Default:** `""`  
- **Example:** `"Confirmed by customer via call"`

#### `changedFlights`
- **Type:** `array`  
- **Required:** Required if `result = "FLIGHT_CHANGE"`  
- **Description:** List of changed flight details.  
- **Default:** `[]`  
- **Example:**
```json
[
  {
    "originalFlightNo": "FZ2323",
    "newDepartureTime": "2023-04-23 13:30",
    "newArrivalTime": "2023-04-23 15:30"
  }
]
```

#### `changedFlights[].originalFlightNo`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Flight number before the change. Must include airline code prefix (e.g., "FZ2323").  
- **Default:** `null`  
- **Example:** `"FZ2323"`

#### `changedFlights[].newDepartureTime`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Updated departure time. Format `yyyy-MM-dd HH:mm`  
- **Default:** `null`  
- **Example:** `"2023-04-23 13:30"`

#### `changedFlights[].newArrivalTime`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Updated arrival time. Format `yyyy-MM-dd HH:mm`  
- **Default:** `null`  
- **Example:** `"2023-04-23 15:30"`

{% endtab %}

{% tab title="Samples" %}
**Schedule Change-Email Notification Confirm with Flight Change**
```
{
    "eventId":"20230323113246035DNIDD",
    "result":"FLIGHT_CHANGE",
    "remark":"",
    "changedFlights":[
        {
        "originalFlightNo":"FZ2323",
        "newDepartureTime":"2023-04-23 13:30",
        "newArrivalTime":"2023-04-23 15:30"
    }
    ]
}
```
**Schedule Change-Email Notification Confirm with Flight Cancelled**
```
{
    "event":"20230323113246035DNIDD",
    "result":"FLIGHT_CANCELED",
    "remark":"",
    "changedFlights":["FZ3423","FZ3467"]
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}


#### `status`
- **Type:** `integer`  
- **Required:** Yes  
- **Description:** Status code representing the outcome of the API request.  

   Valid values: 
  - `0` = Success  
  - Any non-zero value indicates an error or failure.  
- **Default:** `0`  
- **Example:** `0`

#### `msg`
- **Type:** `string`  
- **Required:** No  
- **Description:** Message describing the result of the API call. The 'msg' element is for the description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.  
- **Default:** `"success"`  
- **Example:** `"success"`
{% endtab %}

{% tab title="Samples" %}
```
{
    "status": 0,
    "msg": "success"
}
```
{% endtab %}
{% endtabs %}




