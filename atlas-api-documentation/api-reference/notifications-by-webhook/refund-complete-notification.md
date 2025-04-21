# Refund Complete Notification

### Refund Complete Notification Webhook

When a ticket or ancillary service is cancelled, you will receive the `order.refundComplete` notification on your server.

EndPoint ： The URL you configured to receive notifications

Method : Post

{% tabs %}
{% tab title="Schema" %}

#### `cid`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Unique identifier for the client or system invoking the refund process.  
- **Default:** `null`  
- **Example:** `"XXXXXXXX"`

#### `orderNo`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Unique identifier of the original order being refunded.  
- **Default:** `null`  
- **Example:** `"ZNMKU20220119160129691"`

#### `currency`
- **Type:** `string`  
- **Required:** Yes  
- **Description:** Currency used for fare and refund calculations.  
- **Constraints:** ISO 4217 3-letter currency code  
- **Default:** `"USD"`  
- **Example:** `"USD"`

#### `originalTotalFare`
- **Type:** `number`  
- **Required:** Yes  
- **Description:** Total base fare (excluding ancillaries) originally paid.  
- **Default:** `0.0`  
- **Example:** `37.32`

#### `originalTotalAncillaryAmount`
- **Type:** `number`  
- **Required:** Yes  
- **Description:** Total amount originally paid for ancillary services.  
- **Default:** `0.0`  
- **Example:** `10.0`

#### `originalTotalAmount`
- **Type:** `number`  
- **Required:** Yes  
- **Description:** Combined total of fare + ancillaries originally paid.  
- **Default:** `0.0`  
- **Example:** `47.32`

#### `airlinePenaltyAmountForFare`
- **Type:** `number`  
- **Required:** Yes  
- **Description:** Penalty charged by airline for fare cancellation or refund.  
- **Default:** `0.0`  
- **Example:** `5.0`

#### `airlinePenaltyAmountForAncillaries`
- **Type:** `number`  
- **Required:** Yes  
- **Description:** Penalty charged by airline for cancelling ancillary services.  
- **Default:** `0.0`  
- **Example:** `0.0`

#### `airlinePenaltyAmount`
- **Type:** `number`  
- **Required:** Yes  
- **Description:** Total penalty imposed by the airline (fare + ancillaries).  
- **Default:** `0.0`  
- **Example:** `0.0`

#### `finalRefundAmount`
- **Type:** `number`  
- **Required:** Yes  
- **Description:** Net refund amount returned to the user after penalties and fees. Calculated as:  
  `(originalTotalAmount - airlinePenaltyAmount - transactionFee)`   
- **Default:** `0.0`  
- **Example:** `37.32`

#### `transactionFee`
- **Type:** `number`  
- **Required:** Yes  
- **Description:** Platform or processing fee deducted from refund.  
- **Default:** `0.0`  
- **Example:** `2.0`

#### `refundStatus`
- **Type:** Integer  
- **Required:** Yes  
- **Description:** The present status of the refund process. If the ticket is paid by deposit: the status can be 0,1,2,3,4. If the ticket is paid by VCC pass through: the status can be 0,1,4,5,6. Withdrew is only in the refund claim.
  Valid values:
  - `0`: Atlas Processing
  - `1`: Airline Processing (Submitted to airline by Atlas)
  - `2`: Refunded
  - `3`: Airline Refunding
  - `4`: Rejected
  - `5`: Fulfillment Done
  - `6`: Withdrew  
- **Default:** None  
- **Example:** `2`

{% endtab %}

{% tab title="Samples" %}
```
{
    "cid": "XXXXXXXX",
    "orderNo": "ZNMKU20220119160129691",
    "currency": "USD",
    "originalTotalFare": 37.32,
    "originalTotalAncillaryAmount": 10,
    "originalTotalAmount": 47.32,
    "airlinePenaltyAmountForFare": 5,
    "airlinePenaltyAmountForAncillaries": 0,
    "airlinePenaltyAmount":0,
    "finalRefundAmount":37.32,
    "transactionFee": 2,
    "refundStatus": 2
}
```
{% endtab %}
{% endtabs %}
