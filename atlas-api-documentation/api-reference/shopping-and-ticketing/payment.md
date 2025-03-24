# Payment

### Dependency

`Order` function should be called in prior to this call.

### Endpoint {% debug uid="pay_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/pay.do](https://sandbox.atriptech.com/pay.do)

{% hint style="info" %}
- Atlas provides the information from the search.do API response itself whether VCC can be accepted as a mode of payment for an order. Please read the "supportCreditTransPayment" field in the search.do and verify.do responses. When this field is equal to "0" (zero), it means that only "deposit" mode of payment can be used and when this field is equal to "1" (one), it means that both the "deposit" as well as the "VCC" mode of payment can be used.
- For VCC payment, you can use any fictitious card number.

{% endhint %}

## Request

{% tabs %}
{% tab title="Schema" %}

### Deposit Mode of Payment

### **orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the flight booking order. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.
- **Constraints:** Must be a valid alphanumeric string.  
- **Default:** None  
- **Example:** "TESTT20250324162613982"  
    

### VCC Mode of Payment 

### **orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the flight booking order. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different. 
- **Constraints:** Must be a valid alphanumeric string.  
- **Default:** None  
- **Example:** "TESTF20250324204900551"  

### **supportCreditTransPayment**
- **Type:** String  
- **Required:** Yes  
- **Description:** Indicates whether credit transfer payment is supported.  
- **Constraints:** "0" = Payment with Deposit, "1" = Payment with credit card pass through to the airline.  
- **Default:** "1"  
- **Example:** "1"  

### **creditCard** (Object)
- **Type:** Object  
- **Required:** Yes  
- **Description:** Contains credit card details for the payment.  
- **Constraints:** Must contain valid credit card information.  
- **Default:** None  
- **Example:** {...}  

#### **creditCard.cardNumber**
- **Type:** String  
- **Required:** Yes  
- **Description:** Masked credit card number.  
- **Constraints:** Must be a valid credit card number format.  
- **Default:** None  
- **Example:** "XXXXXXXXXXXXXXXX"  

#### **creditCard.cardExpireMonth**
- **Type:** String  
- **Required:** Yes  
- **Description:** Expiry month of the credit card.  
- **Constraints:** Must be a valid two-digit month (01-12).  
- **Default:** None  
- **Example:** "09"  

#### **creditCard.cardExpireYear**
- **Type:** String  
- **Required:** Yes  
- **Description:** Expiry year of the credit card.  
- **Constraints:** Must be a valid two-digit year (e.g., 26 for 2026).  
- **Default:** None  
- **Example:** "26"  

#### **creditCard.cardCVV**
- **Type:** String  
- **Required:** Yes  
- **Description:** Masked CVV security code.  
- **Constraints:** Must be a valid three-digit or four-digit CVV.  
- **Default:** None  
- **Example:** "***"  

#### **creditCard.cardHolderLastName**
- **Type:** String  
- **Required:** Yes  
- **Description:** Last name of the cardholder.  
- **Constraints:** Must be a valid name.  
- **Default:** None  
- **Example:** "T*****"  

#### **creditCard.cardHolderFirstName**
- **Type:** String  
- **Required:** Yes  
- **Description:** First name of the cardholder.  
- **Constraints:** Must be a valid name.  
- **Default:** None  
- **Example:** "A**"  

#### **creditCard.cardHolderCountry**
- **Type:** String  
- **Required:** Yes  
- **Description:** Country of the cardholder.  
- **Constraints:** Must be a valid country code.  
- **Default:** None  
- **Example:** "S*"  

#### **creditCard.cardHolderProvince**
- **Type:** String  
- **Required:** No  
- **Description:** The province or state of the card holder. This field is mandatory for US addresses. For addresses outside the US, this field can be left "blank". Only use 2-letter US state codes and not full names. For example; use "CA" and not "California".
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** ""  

#### **creditCard.cardHolderCity**
- **Type:** String  
- **Required:** Yes  
- **Description:** City of the cardholder.  
- **Constraints:** Must be a valid city name.  
- **Default:** None  
- **Example:** "HOUSTON"  

#### **creditCard.cardHolderPostCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Postal code of the cardholder.  
- **Constraints:** Must be a valid postal code.  
- **Default:** None  
- **Example:** "20001"  

#### **creditCard.cardHolderAddress**
- **Type:** String  
- **Required:** Yes  
- **Description:** Address of the cardholder.  
- **Constraints:** Must be a valid address.  
- **Default:** None  
- **Example:** "BASKET STREET"  

#### **creditCard.cardHolderPhone**
- **Type:** String  
- **Required:** No  
- **Description:** Phone number of the cardholder.  
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** 0065-4578278254  

#### **creditCard.cardHolderEmail**
- **Type:** String  
- **Required:** No  
- **Description:** Email address of the cardholder.  
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** test@ai.com  

#### **creditCard.maxAcceptedAmount**
- **Type:** Float  
- **Required:** No  
- **Description:** Maximum accepted transaction amount. Certain airlines may experience fare change after payment submission due to their inability to hold seat reservations. You can use this parameter to set a maximum acceptable payment amount threshold. This is the maximum amount which can be used to create the booking using a VCC.

  If this parameter is 'null', our system will automatically set the maximum acceptable amount as the greater of either 5% of the order price or 5 USD (converted to the transacting currency) per 
  passenger. When the amount entered by the customer is lower than 5% of the order price or 5 USD (converted to the transacting currency) per passenger, the information sent to Atlas by the 
  customer will be used.  
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** null  

{% endtab %}

{% tab title="Samples" %}
* Pay with prepayment

```json
{
   "orderNo": "PSTEV20220119165629057"
}
```

* Pay with credit card pass through

```json
{
  "orderNo": "APOGF20250324204900551",
  "supportCreditTransPayment": "1",
  "creditCard": {
    "cardNumber": "439576******3827",
    "cardExpireMonth": "09",
    "cardExpireYear": "26",
    "cardCVV": "***",
    "cardHolderLastName": "T*****",
    "cardHolderFirstName": "A**",
    "cardHolderCountry": "S*",
    "cardHolderProvince": "",
    "cardHolderCity": "H*********",
    "cardHolderPostCode": "2****",
    "cardHolderAddress": "B******************",
    "cardHolderPhone": null,
    "cardHolderEmail": null,
    "maxAcceptedAmount": null,
    "threeDS": null
  },
  "paymentMethod": null,
  "clientOrderNo": null,
  "cid": "ttxzp62405",
  "requestSource": null,
  "channel": null,
  "mainChannel": null,
  "subChannelID": null,
  "requestOwner": null,
  "isSourceReliable": null,
  "requestIp": "34.132.184.222"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %} 
      

### **orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the flight booking order.  
- **Constraints:** Must be a valid alphanumeric string.  
- **Default:** None  
- **Example:** "TESTX20250324195425088"  

### **pnrCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** The pnrCode is the single reference for the booking. This is the Atlas PNR.  
- **Constraints:** Must be a valid alphanumeric string.  
- **Default:** None  
- **Example:** "QVWFIN"  

### **paymentMethod**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Payment method used for booking.  

  Valid values:

  1: Pre-payment

  3: VCC

  5: MOR
- **Constraints:** Must be a valid payment method identifier.  
- **Default:** None  
- **Example:** 1  

### **airlines** (Array)
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of airline codes associated with the booking.  
- **Constraints:** Must contain at least one airline code.  
- **Default:** None  
- **Example:** ["JM"]  

### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Response status code.  
- **Constraints:** 0 indicates success.  
- **Default:** 0  
- **Example:** 0  

### **msg**
- **Type:** String  
- **Required:** Yes  
- **Description:** Response message. The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result. 
- **Constraints:** Must be a valid string.  
- **Default:** "success"  
- **Example:** "success"  
{% endtab %}

{% tab title="Samples" %}
```
{
  "orderNo": "ANRUE20230906141814490",
  "pnrCode": "ZMPB8O",
  "paymentMethod": 1,
  "airlines": [
    "5W"
  ],
  "status": 0,
  "msg": null
}
```
{% endtab %}
{% endtabs %}
