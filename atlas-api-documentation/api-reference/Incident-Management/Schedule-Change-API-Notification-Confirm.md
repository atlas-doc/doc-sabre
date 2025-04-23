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
- **Default:** None  
- **Example:** `"20230323113246035DNIDD"`

### **remark**
- **Type:** String  
- **Required:** No  
- **Description:** Optional remark or comment provided during confirmation of the event.  
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
- **Description:** Response status code.  

  Valid values:
  - 0: success
  - 2: system error
- **Default:** 0  
- **Example:** 0  

### **msg**
- **Type:** String  
- **Required:** No  
- **Description:** Error message. The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.  
- **Default:** null  
- **Example:** null  

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




