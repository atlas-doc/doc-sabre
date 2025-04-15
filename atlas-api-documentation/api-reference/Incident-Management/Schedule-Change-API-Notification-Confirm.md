# Schedule Change-API Notification

### Dependency

No preceding function needs to be carried out.

### Endpoint

[https://sandbox.atriptech.com/event/confirmEvent.do](https://sandbox.atriptech.com/event/confirmEvent.do)

### Request

{% tabs %}
{% tab title="Schema" %}

### **eventId**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier of the event being confirmed (e.g., email notification, schedule change).  
- **Constraints:** Must be a valid alphanumeric string representing a known event in the system.  
- **Default:** None  
- **Example:** `"20230323113246035DNIDD"`

### **remark**
- **Type:** String  
- **Required:** No  
- **Description:** Optional remark or comment provided during confirmation of the event.  
- **Constraints:** Free-text string. Can be left empty.  
- **Default:** `""`  
- **Example:** `"Confirmed by support team after verifying flight delay with airline"`

{% endtab %}


{% tab title="Samples" %}

**Unaccounted Cancellation Confirm **
```
{
    "eventId":"20230323113246035DNIDD",
    "remark":""
}
```

{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Status code representing the result of the API operation.  
- **Constraints:**  
  - `0` = Success  
  - Non-zero values indicate specific error or failure codes (implementation-defined)  
- **Default:** `0`  
- **Example:** `0`

### **msg**
- **Type:** String  
- **Required:** No  
- **Description:** Message describing the result of the operation. The 'msg' element is for the description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.   
- **Constraints:** Can be `null`, empty, or a message string.  
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




