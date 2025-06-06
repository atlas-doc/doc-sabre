# Access to ATRIP 

## Description

This method is to give client the access to ATRIP (Air Travel Retailing and Information Platform) with SSO in client's own system.&#x20;

## Dependency

No preceding function needs to be carried out.

## Endpoint {% debug uid="toOrderDetailWeb_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/toOrderDetailWeb.do](https://sandbox.atriptech.com/toOrderDetailWeb.do)

## Request

{% tabs %}
{% tab title="Schema" %}


### **cid**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique client identifier making the request.  
- **Default:** None  
- **Example:** `"xxxxxx"`

### **orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier of the order for which the action is being performed.  
- **Default:** None  
- **Example:** `"XXXXXXXXXXXXXXXXXXX"`

### **userName**
- **Type:** String  
- **Required:** Yes  
- **Description:** Username of the person performing the action. This is to identify the operator's name in client's system. Atlas will grant access to this operator and track his/her actions in Atlas customer service portal.
- **Default:** None  
- **Example:** `"tony.kal"`

### **role**
- **Type:** String  
- **Required:** Yes  
- **Description:** Role of the user initiating the request, used for authorization or auditing purposes. This is to identify the operator's role. Atlas will grant access to this operator according to the role assigned. 

  Valid values:
  - Customer service : Access to manage orders and request post ticketing services
  - Finance : Access to manage the balance and check statements
  - Developer : Access to manage the system configurations
  - Admin : Full access  
- **Default:** None  
- **Example:** `"TICKETING"`

{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid":"xxxxxx", 
    "orderNo": "XXXXXXXXXXXXXXXXXXX",
    "userName": "tony.kal",
    "role": "TICKETING"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
### **url**
- **Type:** String  
- **Required:** Yes  
- **Description:** A URL with token to access to Atlas customer service portal. 
- **Default:** None  
- **Example:** `"https://example.com/redirect/booking/confirmation.pdf"`  

### **msg**
- **Type:** String  
- **Required:** No  
- **Description:** Response message. The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result. 
- **Default:** null  
- **Example:** null  

### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Status code indicating the success or failure of the operation.  

  Valid values:
  - 0: success
  - 2: System error
  - 3: unauthorized access
- **Default:** None  
- **Example:** `0`

{% endtab %}

{% tab title="Samples" %}
```json
{
    "url": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
    "msg": null,
    "status": 0
}
```
{% endtab %}
{% endtabs %}

###
