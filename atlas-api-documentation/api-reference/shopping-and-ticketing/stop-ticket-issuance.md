---
description: Tentative stopping ticket issuance.
---

# Stop Ticket Issuance

### Dependency

`Payment` function should be called in prior to this call.

### Endpoint {% debug uid="queryOrderDetails_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/stopTicket.do](https://sandbox.atriptech.com/stopTicket.do)

## Request

{% tabs %}
{% tab title="Schema" %}
### **orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** The unique identifier for the order. Must be a valid order number issued by the system.    
- **Default:** None  
- **Example:** "ZNMKU20220119160129691"

{% endtab %}

{% tab title="Samples" %}
```
{
    "orderNo": "ZNMKU20220119160129691"
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
- **Description:** Status code indicating the processing state.  

  Valid values:
  - 0: success
  - 2: System error

  Success does not mean that the ticket issuance has been stopped successfully. It only means that the system will attempt to stop the ticket issuance.

  The result of stopping ticket issuance needs to be obtained by querying the order status of `Retrieve Booking` after 8 minutes.

  orderStatus: -3, means stop issuance successfully.
    
  orderStatus: 2, means stop issuance failed, the order is issued.

  The definition of the queryOrderDetails order status will be different when the request is sent after the "Stop Ticket Issuance" request.
- **Default:** None  
- **Example:** `0`

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
    "msg": "We are trying to intercept the ticket issuance. Please check the order status for result after 8 minutes"
}
```
{% endtab %}
{% endtabs %}
