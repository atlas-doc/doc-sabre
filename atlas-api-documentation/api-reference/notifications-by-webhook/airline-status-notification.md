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
- **Constraints:** Must be a valid JSON object.  
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
- **Constraints:** Each item must be a valid airline code (IATA or ICAO).  
- **Default:** None  
- **Example:** `["TO", "HV"]`  

#### **data.airlineStatus**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Indicates the operational status of the airline(s).  

  Valid values:

  Active = Online

  Maintenance = Airline is under maintenance

  Inactive = Offline
- **Constraints:** Can be "Active" or "Inactive".  
- **Default:** None  
- **Example:** `"Active"`

#### **status**  
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Indicates the response status.  
- **Constraints:** -1 indicates an error or inactive status.  
- **Default:** None  
- **Example:** `-1`  

#### **type**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Specifies the type of response message. 

  Valid value:

  airline.status 
- **Constraints:** Must be a valid response type string.  
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


