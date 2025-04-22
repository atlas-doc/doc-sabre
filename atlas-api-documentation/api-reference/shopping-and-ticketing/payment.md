# Payment

### Dependency

`Order` function should be called in prior to this call.

### Endpoint {% debug uid="pay_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/pay.do](https://sandbox.atriptech.com/pay.do)

{% hint style="info" %}
- Atlas provides the information from the search.do API response itself whether VCC can be accepted as a mode of payment for an order. Please read the "supportCreditTransPayment" field in the search.do and verify.do responses. When this field is equal to "0" (zero), it means that only "deposit" mode of payment can be used and when this field is equal to "1" (one), it means that both the "deposit" as well as the "VCC" mode of payment can be used.
- For VCC payments, the Test Cards to be used for testing in SANDBOX:

    Visa
    - 4532015112830366
    - 4916931584764308
    - 4485275742308327
    - 4556737586899855
    - 4532644189324563

    Mastercard
    - 5555555555554444
    - 5105105105105100
    - 5223456789012346
    - 5301250070000191
    - 5454545454545454

    American Express
    - 378282246310005
    - 371449635398431
    - 340000000000009
    - 370000000000002
    - 375987654321001

    Discover 
    - 6011111111111117 
    - 6011000990139424 
    - 6011987612345678

    JCB
    - 3566002020360505

{% endhint %}

## Request

{% tabs %}
{% tab title="Schema" %}

### Deposit Mode of Payment

### **orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the flight booking order. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.
- **Default:** None  
- **Example:** "TESTT20250324162613982"  
    

### VCC Mode of Payment 

Cardholder country, province, city, postcode and address are required only for a select few airlines as per the table provided below: 

| Airline Code | Airline Name | cardHolderCountry | cardHoldProvince | cardHolderCity | cardHolderPostCode | cardHolderAddress |
| ---- | -------- | -----------------| ----------------- | ------------- | ----------------- | ------------------ |
| 4N | Air North | Required| Required | Required | Required | Required |
| 5J | Cebu Pacific Air | Required| Required | Required | Required | Required |
| 8P | Pacific Coastal | Required| Required | Not Required | Required | Required |
| 9M | Central Mountain Air | Required| Required | Not Required | Required | Required |
| A3 | Aegean Airlines | Required| Required | Required | Required | Required |
| AN | Advanced Airlines | Required| Required | Required | Required | Required |
| AS | Alaska Airlines | Not Required| Required | Required | Required | Required |
| BT | Air Baltic | Required| Not Required | Required | Required | Required |
| BV | TOKI AIR | Required| Required | Required | Required | Required |
| D8 | Norwegian Air Sweden | Required| Not Required | Required | Required | Required |
| DE | Condor | Not Required| Not Required | Required | Not Required | Not Required |
| DG | Cebgo | Required| Required | Required | Required | Required |
| DI | Cebu Pacific Air | Not Required| Not Required | Required | Not Required | Not Required |
| DM | Arajet | Required| Required | Required | Required | Required |
| DY | Norwegian Air Shuttle ASA | Not Required| Required | Required | Required | Required |
| E6 | Eurowings Europe | Required| Required | Required | Required | Required |
| EI | Aer Lingus | Required| Required | Required | Required | Required |
| EW | Eurowings | Required| Required | Required | Required | Required |
| F9 | Frontier Airlines (US Address) | Required | Not Required | Required | Required | Required |
| F9 | Frontier Airlines (Non-US Address) | Not Required | Not Required | Not Required | Not Required | Not Required |
| FA | Fly Safair | Required| Required | Required | Required | Required |
| G4 | Allegiant Air | Required| Required | Required | Required | Required |
| GE | Lift Airline | Required| Required | Required | Required | Required |
| GQ | Skyexpress | Required| Required | Required | Required | Required |
| H4 | HiSky | Required| Not Required | Not Required | Not Required | Not Required |
| H7 | HiSky | Required| Not Required | Not Required | Not Required | Not Required |
| JV | Perimeter | Required| Required | Required | Not Required | Not Required |
| KM | AirMalta | Required| Not Required | Required | Not Required | Required |
| LJ | Jin Air | Required| Required | Not Required | Required | Required |
| MM | Peach Aviation | Not Required| Not Required | Required | Required | Required |
| MO | Calm Air | Not Required| Not Required | Not Required | Not Required | Required |
| NK | Spirit Airlines | Required| Required | Required | Required | Required |
| OA | Olympic Air | Required| Required | Required | Required | Required |
| OG | PLAY | Required| Required | Required | Required | Required |
| P6 | Pascan | Required| Required | Required | Required | Required |
| PB | PAL Airlines | Required| Required | Required | Required | Required |
| RW | Royal Air Philippines | Not Required| Not Required | Not Required | Not Required | Required |
| SY | Sun Country Airlines | Required| Required | Required | Required | Required |
| TR | Scoot Tiger Air | Required| Not Required | Required | Required | Required |
| VY | Vueling Airlines | Required| Not Required | Required | Required | Required |

### **orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the flight booking order. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different. 
- **Default:** None  
- **Example:** "TESTF20250324204900551"  

### **supportCreditTransPayment**
- **Type:** String  
- **Required:** Yes  
- **Description:** Indicates whether credit transfer payment is supported.

  Valid values:
  - "0" = Payment with Deposit
  - "1" = Payment with credit card pass through to the airline.  
- **Default:** "1"  
- **Example:** "1"  

### **creditCard** (Object)
- **Type:** Object  
- **Required:** Yes  
- **Description:** Contains credit card details for the payment.  
- **Default:** None  
- **Example:** {...}  

#### **creditCard.cardNumber**
- **Type:** String  
- **Required:** Yes  
- **Description:** Masked credit card number.  
- **Default:** None  
- **Example:** "XXXXXXXXXXXXXXXX"  

#### **creditCard.cardExpireMonth**
- **Type:** String  
- **Required:** Yes  
- **Description:** Expiry month of the credit card. Must be a valid two-digit month (01-12).   
- **Default:** None  
- **Example:** "09"  

#### **creditCard.cardExpireYear**
- **Type:** String  
- **Required:** Yes  
- **Description:** Expiry year of the credit card. Must be a valid two-digit year (e.g., 26 for 2026).    
- **Default:** None  
- **Example:** "26"  

#### **creditCard.cardCVV**
- **Type:** String  
- **Required:** Yes  
- **Description:** Masked CVV security code. Must be a valid three-digit or four-digit CVV.    
- **Default:** None  
- **Example:** "***"  

#### **creditCard.cardHolderLastName**
- **Type:** String  
- **Required:** Yes  
- **Description:** Last name of the cardholder.  
- **Default:** None  
- **Example:** "T*****"  

#### **creditCard.cardHolderFirstName**
- **Type:** String  
- **Required:** Yes  
- **Description:** First name of the cardholder.  
- **Default:** None  
- **Example:** "A**"  

#### **creditCard.cardHolderCountry**
- **Type:** String  
- **Required:** Yes  
- **Description:** Country of the cardholder.  
- **Default:** None  
- **Example:** "S*"  

#### **creditCard.cardHolderProvince**
- **Type:** String  
- **Required:** No  
- **Description:** The province or state of the card holder. For example; use "CA" and not "California".
- **Default:** null  
- **Example:** ""  

#### **creditCard.cardHolderCity**
- **Type:** String  
- **Required:** Yes  
- **Description:** City of the cardholder.  
- **Default:** None  
- **Example:** "HOUSTON"  

#### **creditCard.cardHolderPostCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Postal code of the cardholder.  
- **Default:** None  
- **Example:** "20001"  

#### **creditCard.cardHolderAddress**
- **Type:** String  
- **Required:** Yes  
- **Description:** Address of the cardholder.  
- **Default:** None  
- **Example:** "BASKET STREET"  

#### **creditCard.cardHolderPhone**
- **Type:** String  
- **Required:** No  
- **Description:** Phone number of the cardholder.  
- **Default:** null  
- **Example:** 0065-4578278254  

#### **creditCard.cardHolderEmail**
- **Type:** String  
- **Required:** No  
- **Description:** Email address of the cardholder.  
- **Default:** null  
- **Example:** test@ai.com  

#### **creditCard.maxAcceptedAmount**
- **Type:** Number  
- **Required:** No  
- **Description:** Maximum accepted transaction amount. Certain airlines may experience fare change after payment submission due to their inability to hold seat reservations. You can use this parameter to set a maximum acceptable payment amount threshold. This is the maximum amount which can be used to create the booking using a VCC.

  If this parameter is 'null', our system will automatically set the maximum acceptable amount as the greater of either 5% of the order price or 5 USD (converted to the transacting currency) per 
  passenger. When the amount entered by the customer is lower than 5% of the order price or 5 USD (converted to the transacting currency) per passenger, the information sent to Atlas by the 
  customer will be used.  
- **Default:** null  
- **Example:** null  

#### **paymentMethod**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Method of payment selected by the user. For MoR, the card type must be same as that in order.do RQ.

  Valid values:
  - 1 = Deposit
  - 3 = VCC Passthrough
  - 5 = MoR
- **Default:** Deposit  
- **Example:** `3`  
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
  "paymentMethod": 5,    
  "clientOrderNo": null,
  "cid": "xxxxxxxxxx",
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
- **Default:** None  
- **Example:** "TESTX20250324195425088"  

### **pnrCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** The pnrCode is the single reference for the booking. This is the Atlas PNR.  
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
- **Default:** None  
- **Example:** 1  

### **airlines** (Array)
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of airline codes associated with the booking.  
- **Default:** None  
- **Example:** ["JM"]  

### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Response status code.  
  Valid values:
  - 0: success
  - 2: system error
- **Default:** 0  
- **Example:** 0  

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
