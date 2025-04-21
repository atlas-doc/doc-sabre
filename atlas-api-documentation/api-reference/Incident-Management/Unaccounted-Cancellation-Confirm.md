# Unaccounted Cancellation

### Dependency

No preceding function needs to be carried out.

### Endpoint

[https://sandbox.atriptech.com/event/confirmAbnormalCancelledEvent.do](https://sandbox.atriptech.com/event/confirmAbnormalCancelledEvent.do)

### Request

{% tabs %}
{% tab title="Schema" %}


#### `eventId`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Unique identifier of the event being confirmed.  
- **Default:** `null`  
- **Example:** `"20230323113246035DNIDD"`

#### `result`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** The result of handling the event.  
  Valid values:
  - FLIGHT_CANCELED: Flight Cancelled
  - ABNORMAL_CANCELLATION: Unaccounted Cancellation
  - PASSENGER_CANCELLATION: Cancelled by Passenger
  - NO_CANCELLATION: No Cancellation  
- **Default:** `null`  
- **Example:** `"ABNORMAL_CANCELLATION"`

#### `remark`
- **Type:** `string`  
- **Required:** No  
- **Description:** Optional notes or remarks regarding the abnormal cancellation.  
- **Default:** `""`  
- **Example:** `"Flight cancelled due to weather. No alternative offered."`

{% endtab %}

{% tab title="Samples" %}

**Unaccounted Cancellation Confirm **
```
{
    "eventId":"20230323113246035DNIDD",
    "result":"ABNORMAL_CANCELLATION",
    "remark":""
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
