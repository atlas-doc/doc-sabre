# Addon Complete Notification

### Addon Complete Notification Webhook

When your customer books an ancillary service post booking their ticket, you will receive the `order.addonComplete` notification.

EndPoint ： The URL you configured to receive notifications

Method : Post

{% tabs %}
{% tab title="Schema" %}

#### `cid`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Unique client identifier.  
- **Default:** `null`  
- **Example:** `"rggat40831"`

#### `type`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Type of notification event. Must be `"order.addonComplete"`   
- **Default:** `null`  
- **Example:** `"order.addonComplete"`

#### `data.addonOrderNo`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Unique identifier for the add-on order.  
- **Default:** `null`  
- **Example:** `"BCNQL20201031184148568KLDKS"`

#### `data.originalOrderNo`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Original main order number associated with the add-on.  
- **Default:** `null`  
- **Example:** `"BCNQL20201031184148568"`

#### `data.orderStatus`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Status of the add-on order.  

  Valid values: 
  - `"0"` = Unpaid  
  - `"1"` = Ticketing-in-Process  
  - `"2"` = Ticketed  
  - `"-3"` = Cancelled  
- **Default:** `"0"`  
- **Example:** `"2"`

### `data.paxTicketInfos[]`

#### `paxTicketInfos[].name`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Passenger name in `LastName/FirstName MiddleName` format.  
- **Default:** `null`  
- **Example:** `"MOREL/JEROME"`

#### `paxTicketInfos[].passengerType`
- **Type:** `integer`  
- **Required:** Yes  
- **Description:** Passenger type.  

  Valid values: 
  - `0` = Adult  
  - `1` = Child  
  - `2` = Infant  
- **Default:** `0`  
- **Example:** `0`

#### `paxTicketInfos[].birthday`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Passenger birth date in `yyyyMMdd` format.  
- **Default:** `null`  
- **Example:** `"19661118"`

#### `paxTicketInfos[].gender`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Passenger gender.  

  Valid values:
  - `"M"`: Male
  - `"F"`: Female  
- **Default:** `null`  
- **Example:** `"M"`

#### `paxTicketInfos[].cardNum`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Document number (e.g. passport).  
- **Default:** `null`  
- **Example:** `"G000000000"`

#### `paxTicketInfos[].cardType`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Type of ID document.  

  Valid values:
  - PP - Passport
  - GA - Hong Kong Macau Pass for China mainland citizens
  - TW - Taiwan Pass for China mainland citizens
  - TB - China mainland pass for Taiwanese
  - HY - International Seaman's Certificate 
- **Default:** `null`  
- **Example:** `"PP"`

#### `paxTicketInfos[].cardIssuePlace`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Country that issued the document.  
- **Default:** `null`  
- **Example:** `"FR"`

#### `paxTicketInfos[].cardExpired`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Expiry date of the document. Must be a future-valid date.  Format: `yyyyMMdd`.  
- **Default:** `null`  
- **Example:** `"20320118"`

#### `paxTicketInfos[].nationality`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Passenger nationality.  
- **Default:** `null`  
- **Example:** `"FR"`

#### `paxTicketInfos[].ticketNos`
- **Type:** `array of string`  
- **Required:** Yes  
- **Description:** Ticket numbers issued to the passenger.  
- **Default:** `[]`  
- **Example:** `["EDVLRZ"]`

#### `paxTicketInfos[].airlinePNRs`
- **Type:** `array of string`  
- **Required:** Yes  
- **Description:** Airline PNR codes associated with the passenger.  
- **Default:** `[]`  
- **Example:** `["EDVLRZ"]`

### `paxTicketInfos[].ancillaries[]`

#### `ancillaries[].productCode`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Unique product code for the ancillary item.  
- **Default:** `null`  
- **Example:** `"SCI_BAG_ID_25KG_AABBBB"`

#### `ancillaries[].segmentIndex`
- **Type:** `integer`  
- **Required:** Yes  
- **Description:** Segment index to which the ancillary applies.  
- **Default:** `1`  
- **Example:** `1`

{% endtab %}

{% tab title="Sample" %}
```
{
    "cid": "rggat40831",
    "type": "order.addonComplete",
    "data":
    {
        "addonOrderNo": "BCNQL20201031184148568KLDKS",
        "originalOrderNo": "BCNQL20201031184148568",
        "orderStatus": "2",
        "paxTicketInfos": [
            {
                "name": "MOREL/JEROME",
                "passengerType": 0,
                "birthday": "19661118",
                "gender": "M",
                "cardNum": "G000000000",
                "cardType": "PP",
                "cardIssuePlace": "FR",
                "cardExpired": "20320118",
                "nationality": "FR",
                "ticketNos": [
                    "EDVLRZ"
                ],
                "airlinePNRs": [
                    "EDVLRZ"
                ],
                "ancillaries": [
                    {
                        "productCode": "SCI_BAG_ID_25KG_AABBBB",
                        "segmentIndex": 1
                    }
                ]
            }
        ]
    }  
}
```
{% endtab %}
{% endtabs %}
