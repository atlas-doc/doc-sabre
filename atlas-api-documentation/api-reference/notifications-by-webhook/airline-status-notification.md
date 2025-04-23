# Airline Status Update Notification

### Airline Status Update Webhook

Once an airline's status is changed, an `airline.status` notification will be received on your server. You can process it and take action as required. For example; you could adjust your search caching strategy as per the status of the airline.

### EndPoint

The URL you configured to receive notifications

Method : Post

{% tabs %}
{% tab title="Schema" %}

#### **data**  
- **Type:** Object  
- **Required:** Yes  
- **Description:** Contains airline information including the airline codes and their status.  
- **Default:** None  
- **Example:**  
  ```json
  {
    "airline": ["TO", "HV"],
    "airlineStatus": "Active"
  }
  ```

#### **data.airline**  
- **Type:** Array of Strings  
- **Required:** Yes  
- **Description:** List of airline codes associated with the response.  
- **Default:** None  
- **Example:** `["TO", "HV"]`  

#### **data.airlineStatus**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Indicates the operational status of the airline(s).  

  Valid values:
  - Active = Online
  - Maintenance = Airline is under maintenance
  - Inactive = Offline
- **Default:** None  
- **Example:** `"Active"`

#### **status**  
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Indicates the response status. Only for internal use by Atlas.  
- **Default:** None  
- **Example:** `-1`  

#### **type**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Specifies the type of response message. 

  Valid value:
  - airline.status 
- **Default:** None  
- **Example:** `"airline.status"`  

{% endtab %}
{% tab title="Samples" %}
```
{
  "data":{
     "airline":["TO","HV"],
     "airlineStatus":"Active"},
  "status":-1,
  "type":"airline.status"
}
```
{% endtab %}
{% endtabs %}


