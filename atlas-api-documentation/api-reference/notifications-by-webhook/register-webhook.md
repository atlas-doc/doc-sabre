# Register Webhook

## Endpoint {% debug uid="search_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/updateWebhookURL.do](https://sandbox.atriptech.com/updateWebhookURL.do)

## Request

{% tabs %}
{% tab title="Schema" %}
##### **cid**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique client identifier.  
- **Default:** None  
- **Example:** "XXXXXXXX"  

##### **url**
- **Type:** String  
- **Required:** Yes  
- **Description:** The URL address to receive webhook message.  
- **Default:** None  
- **Example:** "https://xxx.com/xxxx"  

{% endtab %}

{% tab title="Sample" %}
```json
{
    "cid": "XXXXXXXX",
    "url": "https://xxx.com/xxxx"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
#### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Response status code.  

  Valid values:
  - 0: success
  - 2: system error
- **Default:** 0  
- **Example:** 0  

#### **msg**
- **Type:** String  
- **Required:** No  
- **Description:** Error message. The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.  
- **Default:** null  
- **Example:** null

{% endtab %}

{% tab title="Sample" %}
```
{
    "status": 0,
    "msg": "success"
}
```


{% endtab %}
{% endtabs %}
