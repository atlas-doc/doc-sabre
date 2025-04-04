# Email Notification

### Email Notification Webhook

Once Altas' email service receives the airline's email, the customer will receive the `email.all` notification on the server.

EndPoint ： The URL you configured to receive notifications

Method : Post

{% tabs %}
{% tab title="Schema" %}
##### `cid`  
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique client identifier.  
- **Constraints:** Max length: 50 characters.  
- **Default:** None  
- **Example:** `"XXXXX"`  

##### `notificationId`  
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the notification event.  
- **Constraints:** Max length: 50 characters.  
- **Default:** None  
- **Example:** `"20240105105430470MJMOR"`  

##### `status`  
- **Type:** Integer  
- **Required:** Yes  
- **Description:** In this type of notification status always = -1. This is an internal field and should be ignored.  
- **Constraints:** None
- **Default:** None  
- **Example:** `-1`  

##### `type`  
- **Type:** String  
- **Required:** Yes  
- **Description:** Notification type.  
- **Constraints:** Must be `"email.all"`.  
- **Default:** None  
- **Example:** `"email.all"`  

##### `data`  
- **Type:** Object  
- **Required:** Yes  
- **Description:** Contains email-related details.  
- **Constraints:** Cannot be empty.  
- **Default:** None  
- **Example:** `{ ... }`  

##### `data.orderNo`  
- **Type:** String  
- **Required:** Yes  
- **Description:** Order number associated with the email.  
- **Constraints:** Max length: 50 characters.  
- **Default:** None  
- **Example:** `"XXXXXX"`  

##### `data.emailReceivingDate`  
- **Type:** String  
- **Required:** Yes  
- **Description:** Date and time when the email was received by Atlas (UTC).  
- **Constraints:** Format: `YYYY-MM-DD HH:mm:ss`.  
- **Default:** None  
- **Example:** `"2024-01-05 10:54:21"`  

##### `data.uniqueCode`  
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique code for identifying the email.  
- **Constraints:** Must be exactly 32 characters.  
- **Default:** None  
- **Example:** `"e4afbecfd5727817ff73a71a94a2a64d"`  

##### `data.emailCategory`  
- **Type:** String  
- **Required:** Yes  
- **Description:** Atlas email categories. Atlas categorizes emails but does not guarantee accuracy in classification.

  Valid values:

  Schedule change

  Receipt

  Payment Success

  Verification

  Trip Reminder

  Promo code

  Travel Itinerary

  Advertisement

  PNR Cancellation Success

  Payment Due

  Unidentified

  Duplicated Schedule Change

  Unaccounted Cancellation  
- **Constraints:** Possible values: `"Payment Success"`, `"Booking Confirmation"`, `"Cancellation"`.  
- **Default:** None  
- **Example:** `"Payment Success"`  

##### `data.from`  
- **Type:** String  
- **Required:** Yes  
- **Description:** Sender’s email address.  
- **Constraints:** Must be a valid email format.  
- **Default:** None  
- **Example:** `"donotreply@easyjet.com"`  

##### `data.to`  
- **Type:** String  
- **Required:** Yes  
- **Description:** Recipient’s email address.  
- **Constraints:** Must be a valid email format.  
- **Default:** None  
- **Example:** `"NSDLZCQTGJTEYXOMFOD@gorn.top"`  

##### `data.emailSubject`  
- **Type:** String  
- **Required:** Yes  
- **Description:** Subject of the email.  
- **Constraints:** Max length: 100 characters.  
- **Default:** None  
- **Example:** `"easyJet booking reference: XXXXX"`  

##### `data.emailLink`  
- **Type:** String  
- **Required:** Yes  
- **Description:** URL link to access the email content. Email Link is only valid for 10 mins.
- **Constraints:** Must be a valid URL format.  
- **Default:** None  
- **Example:** `"http://order-oss-sg.oss-ap-southeast-1.aliyuncs.com/...eml?Expires=1704426870..."`  

##### `data.createTime`  
- **Type:** String  
- **Required:** Yes  
- **Description:** Create Time is the time when Atlas created this email record in the Email list. Generally, it will be later than the receiving time.  
- **Constraints:** Format: `YYYY-MM-DD HH:mm:ss`.  
- **Default:** None  
- **Example:** `"2024-01-05 10:54:26"`  
{% endtab %}

{% tab title="Samples" %}

```
{
    "cid":"XXXXX",
    "data":{
        "orderNo":"XXXXXX",
        "emailReceivingDate":"2024-01-05 10:54:21",
        "uniqueCode":"e4afbecfd5727817ff73a71a94a2a64d",
        "emailCategory":"Payment Success",
        "from":"donotreply@easyjet.com",
        "to":"NSDLZCQTGJTEYXOMFOD@gorn.top",
        "emailSubject":"easyJet booking reference: XXXXX",
        "emailLink":"http://order-oss-sg.oss-ap-southeast-1.aliyuncs.com/2024/01/e4afbecfd5727817ff73a71a94a2a64d.eml?Expires=1704426870&OSSAccessKeyId=LTAI5tDmTE9iwtNdsqxVXuom&Signature=zF8aNNsGgY8n2jhsW7V1gmPLw8c%3D",
        "createTime":"2024-01-05 10:54:26"
    },
    "notificationId":"20240105105430470MJMOR",
    "status":-1,
    "type":"email.all"
}

```
{% endtab %}
{% endtabs %}
