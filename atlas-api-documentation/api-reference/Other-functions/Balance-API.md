# Get Balance

The "Balance API" is used to fetch the deposit balance from the ATRIP credentials of the customer.

The customer will need to send the header information and the response will be received with the ATRIP deposit balance.

## Dependency

There is no dependency for this call.

## Endpoint

[https://sandbox.atriptech.com/balance.do](https://sandbox.atriptech.com/balance.do)

## Request

The "request" has to be only the header information consisting of 'x-atlas-client-id' and 'x-atlas-client-secret'

## Response

{% tabs %}
{% tab title="Schema" %}

### **accountBalance**
- **Type:** Object  
- **Required:** Yes  
- **Description:** Object containing the current account balance and its associated currency.  
- **Constraints:** Must include both `amount` and `currency`.  
- **Default:** None  
- **Example:**
  ```json
  {
    "amount": 12308007.89,
    "currency": "USD"
  }
  ```

### **accountBalance.amount**
- **Type:** Number (Float)  
- **Required:** Yes  
- **Description:** Current available balance in the account.  
- **Constraints:** Must be ≥ 0  
- **Default:** `0.00`  
- **Example:** `12308007.89`

### **accountBalance.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** The currency in which Atlas settles transactions with you.  
- **Constraints:** Must be a valid 3-letter ISO 4217 currency code.  
- **Default:** None  
- **Example:** `"USD"`

### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Status of the request indicating success or failure.  

  Valid values:

  0: success

  9999: error (an error message will be displayed with the issue)
- **Constraints:**  
- **Default:** None  
- **Example:** `0`
{% endtab %}

{% tab title="Samples" %}
```
{
    "accountBalance": {
        "amount": 12308007.89,
        "currency": "USD"
    },
    "status": 0
}
```
{% endtab %}
{% endtabs %}
