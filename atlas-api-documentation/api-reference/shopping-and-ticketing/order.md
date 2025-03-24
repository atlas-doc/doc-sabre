# Order

### Dependency

`Verify` function should be called in prior to this call.

### Endpoint {% debug uid="order_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/order.do](https://sandbox.atriptech.com/order.do)

## Request

{% hint style="info" %}

The booking requirements need to be read from the "bookingRequirement" array in the "verify.do" response. The "Booking Requirements" can be different at the route level. Alternatively, you can add all the details but please note that all the fields should have actual data and not fictitious information. Please follow this approach.

{% endhint %}

{% tabs %}
{% tab title="Schema" %}
### **ifSeatOccupied**
- **Type:** String  
- **Required:** Yes  
- **Description:** Defines the seat assignment strategy if the preferred seat is already occupied.  
- **Constraints:** Must be "SIMILAR_SEAT" or another predefined strategy.  

  Valid values:

  SIMILAR_SEAT: Default, select a similar seat automatically

  STOP_SEAT: Stop seat and continue ticketing

  STOP_TICKET: Stop ticketing and cancel the order
- **Default:** SIMILAR_SEAT  
- **Example:** "SIMILAR_SEAT"  

### **sessionId**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique session identifier for the booking request.  
- **Constraints:** Must be a valid UUID.  
- **Default:** None  
- **Example:** "43c3c07e-2b05-4fc9-8832-29a71075a097"  

## **passengers** (Array)
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of passengers included in the booking. Each passenger object contains their personal details and ancillaries.  
- **Constraints:** Must contain at least one passenger object.  
- **Default:** None  
- **Example:** [{...}]  

### **passengers.name**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's full name in uppercase format.  
- **Constraints:** Must follow "LASTNAME/FIRSTNAME MIDDLENAME" format.  
- **Default:** None  
- **Example:** "TEST/ONE"  

### **passengers.passengerType**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Passenger type.  
- **Constraints:** 0 = Adult, 1 = Child, 2 = Infant.  
- **Default:** None  
- **Example:** 0  

### **passengers.birthday**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's date of birth in YYYYMMDD format.  
- **Constraints:** Must be a valid date.  
- **Default:** None  
- **Example:** "19900101"  

### **passengers.gender**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's gender.  
- **Constraints:** "M" for Male, "F" for Female.  
- **Default:** None  
- **Example:** "M"  

### **passengers.cardNum**
- **Type:** String  
- **Required:** Yes  
- **Description:** Identification card number.  
- **Constraints:** None.  
- **Default:** None  
- **Example:** "00000001"  

### **passengers.cardType**
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of identification card.  
- **Constraints:** Must be a valid card type (e.g., "PP" for passport).  

  Valid values:

  PP - Passport

  GA - Hong Kong Macau Pass for China mainland citizens

  TW - Taiwan Pass for China mainland citizens

  TB - China mainland pass for Taiwanese

  HY - International Seaman's Certificate
- **Default:** None  
- **Example:** "PP"  

### **passengers.cardIssuePlace**
- **Type:** String  
- **Required:** Yes  
- **Description:** Country where the identification card was issued.  
- **Constraints:** Must be a valid ISO country code.  
- **Default:** None  
- **Example:** "SG"  

### **passengers.cardExpired**
- **Type:** String  
- **Required:** Yes  
- **Description:** Expiration date of the identification card in YYYYMMDD format.  
- **Constraints:** Must be a future date.  
- **Default:** None  
- **Example:** "20301231"  

### **passengers.nationality**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's nationality.  
- **Constraints:** Must be a valid ISO country code.  
- **Default:** None  
- **Example:** "SG"  

### **passengers.ffpCardNo**
- **Type:** String  
- **Required:** No  
- **Description:** Frequent flyer program card number.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "123456"  

### **passengers.ffpCarrier**
- **Type:** String  
- **Required:** No  
- **Description:** Frequent flyer program carrier code.  
- **Constraints:** None  
- **Default:** None  
- **Example:** "JT"  

### **passengers.ancillaries** (Array)
- **Type:** Array  
- **Required:** No  
- **Description:** Additional services selected by the passenger.  
- **Constraints:** Can be empty if no ancillaries are selected.  
- **Default:** []  
- **Example:** [{...}]  

#### **passengers.ancillaries.productCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Code representing the ancillary service. This is received from routing element in the search/revalidation response.
- **Constraints:** Must be a valid product code.  
- **Default:** None  
- **Example:** "BAG_5J_PH-PH_1_1P_20KG"  

#### **passengers.ancillaries.segmentIndex**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Segment to which the ancillary applies.  
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** 1  

## **contact** (Object)
- **Type:** Object  
- **Required:** Yes  
- **Description:** Contact details for the booking.  
- **Constraints:** Must include at least an email or phone number.  
- **Default:** None  
- **Example:** {...}  

### **contact.name**
- **Type:** String  
- **Required:** Yes  
- **Description:** Contact person's name.  
- **Constraints:** Format : LastName/FirstName MiddleName
- **Default:** None  
- **Example:** "Way/Su"  

### **contact.email**
- **Type:** String  
- **Required:** No  
- **Description:** Contact email address.  
- **Constraints:** Must be a valid email format.  
- **Default:** None  
- **Example:** "xxxxxxxxx@xxx.com"  

### **contact.mobile**
- **Type:** String  
- **Required:** Yes  
- **Description:** Contact phone number.  
- **Constraints:** Must include country code. Format: XXXX(digital country code)-XXXXXXXX(phone number). Example: 0001-87291810, 0086-13928109091, 0971-19201998  
- **Default:** None  
- **Example:** "0065-81234567"  

### **requestSource**
- **Type:** String  
- **Required:** No  
- **Description:** The tag to identify which channel does this traffic come from. (e.g., website, mobile app).  
- **Default:** ""  
- **Example:** "Organic"  

### **allowGenerateMultipleOrders**
- **Type:** Boolean  
- **Required:** No  
- **Description:** Allows multiple orders to be generated if a cheaper fare is found.  
- **Default:** false  
- **Example:** false  

### **useAtlasMailForContact**
- **Type:** Boolean  
- **Required:** No  
- **Description:** The tag denoting whether to use Atlas email id for contact information. true: Use Atlas email as contact email; false: Use customer email as contact email.
- **Default:** false  
- **Example:** false  
    
{% endtab %}

{% tab title="Samples" %}
```
{
  "sessionId": "2ef08340-d311-41e0-9078-b7589dafbd59",
  "offerId": null,
  "orderNo": null,
  "passengers": [
    {
      "name": "LATIFI/KARIM",
      "passengerType": 0,
      "birthday": "19980102",
      "gender": "M",
      "cardNum": null,
      "cardType": null,
      "cardIssuePlace": null,
      "cardExpired": null,
      "nationality": null,
      "paxRecordId": null,
      "ffpCardNo": null,
      "ffpCarrier": null,
      "ancillaries": [
        {
          "productCode": "SCI_BAG_1PC_20KG",
          "segmentIndex": 1
        }
      ]
    }
  ],
  "contact": {
    "name": "LATIFI/KARIM",
    "address": null,
    "postcode": null,
    "email": "KARIM.LATIFI2016@GMAIL.COM",
    "mobile": "0046-771407000"
  },
  "baggagePiece": 0,
  "baggageWeight": 0,
  "passengerBaggages": null,
  "useAtlasMailForContact": false,
  "allowGenerateMultipleOrders": false,
  "locale": null,
  "ifSeatOccupied": null,
  "skipDuplicateCheck": false,
  "cid": "ttxzp62405",
  "requestSource": null,
  "channel": null,
  "mainChannel": null,
  "subChannelID": null,
  "requestOwner": null,
  "isSourceReliable": null,
  "requestIp": "34.69.44.134"
}
```
{% endtab %}
{% endtabs %}


{% hint style="info" %}
**VCC can also be used on round-trip itineraries combining 2 one-way fares. Check our FAQs for <mark style="color:blue;">**[Atlas API Order](../../faqs/atlas-order-api.md)**<mark style="color:blue;"></mark>**


{% endhint %}


## Response

{% tabs %}
{% tab title="Schema" %}
### **ifSeatOccupied**
- **Type:** String  
- **Required:** Yes  
- **Description:** Defines the seat assignment strategy if the preferred seat is already occupied.  
- **Constraints:** Must be "SIMILAR_SEAT" or another predefined strategy.  

  Valid values:

  SIMILAR_SEAT: Default, select a similar seat automatically

  STOP_SEAT: Stop seat and continue ticketing

  STOP_TICKET: Stop ticketing and cancel the order
- **Default:** SIMILAR_SEAT  
- **Example:** "SIMILAR_SEAT"  

### **sessionId**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique session identifier for tracking the booking response.  
- **Constraints:** Must be a valid UUID.  
- **Default:** None  
- **Example:** "1b7712ae-a94e-44b2-b4e9-574c07d2f3dc"  

### **offerId**
- **Type:** String  
- **Required:** No  
- **Description:** Unique identifier for the offer associated with the booking.  
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** null  

### **orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique order number assigned to the booking.  
- **Constraints:** Must be a valid alphanumeric string.  
- **Default:** None  
- **Example:** "AXWKQ20250324134909925"  

### **originalOrderNo**
- **Type:** String  
- **Required:** No  
- **Description:** Original order number if applicable.  
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** null  

### **ticketOrderNo**
- **Type:** String  
- **Required:** No  
- **Description:** Ticket order number assigned after booking confirmation.  
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** null  

### **totalPrice**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Total price of the booking.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 110.8  

### **totalTransactionFee**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Total transaction fee applied to the booking.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 1  

### **currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency in which the total price is displayed.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** "USD"  

### **vendorTotalPrice**
- **Type:** Float  
- **Required:** Yes  
- **Description:** The total price charged by the vendor.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 102  

### **vendorCurrency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency in which the vendor price is charged.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** "EUR"  

### **tktLimitTime**
- **Type:** String  
- **Required:** Yes  
- **Description:** Ticketing deadline time for completing the booking. This time will be displayed in SGT (GMT +8).
- **Constraints:** Must be in "YYYY-MM-DD HH:MM:SS" format.  
- **Default:** None  
- **Example:** "2025-03-24 14:19:10"  

### **pnrCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** The pnrCode is the single reference for the booking. This is the Atlas PNR.
- **Constraints:** Must be a valid alphanumeric string.  
- **Default:** None  
- **Example:** "AZQB6O"  

### **includeExtraBaggage**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Indicates whether extra baggage is included in the booking.  
- **Constraints:** 0 = No, 1 = Yes.  
- **Default:** 0  
- **Example:** 0  

### **paxTicketInfos** (Array)
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of passenger details including tickets and ancillaries.  
- **Constraints:** Must contain at least one passenger object.  
- **Default:** None  
- **Example:** [{...}]  

#### **paxTicketInfos.name**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's full name.  
- **Constraints:** Must follow "LASTNAME/FIRSTNAME MIDDLENAME" format.  
- **Default:** None  
- **Example:** "LATIFI/KARIM"  

#### **paxTicketInfos.passengerType**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Passenger type.  
- **Constraints:** 0 = Adult, 1 = Child, 2 = Infant.  
- **Default:** None  
- **Example:** 0  

#### **paxTicketInfos.birthday**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's date of birth in YYYYMMDD format.  
- **Constraints:** Must be a valid date.  
- **Default:** None  
- **Example:** "19980102"  

#### **paxTicketInfos.gender**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's gender.  
- **Constraints:** "M" for Male, "F" for Female.  
- **Default:** None  
- **Example:** "M"  

#### **paxTicketInfos.cardNum**
- **Type:** String  
- **Required:** No  
- **Description:** Identification card number.  
- **Constraints:** Can be empty or null.  
- **Default:** None  
- **Example:** ""  

### **paxTicketInfos.cardType**
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of identification card.  
- **Constraints:** Must be a valid card type (e.g., "PP" for passport).  

  Valid values:

  PP - Passport

  GA - Hong Kong Macau Pass for China mainland citizens

  TW - Taiwan Pass for China mainland citizens

  TB - China mainland pass for Taiwanese

  HY - International Seaman's Certificate
- **Default:** None  
- **Example:** "PP"  

### **paxTicketInfos.cardIssuePlace**
- **Type:** String  
- **Required:** Yes  
- **Description:** Country where the identification card was issued.  
- **Constraints:** Must be a valid ISO country code.  
- **Default:** None  
- **Example:** "SG"  

### **paxTicketInfos.cardExpired**
- **Type:** String  
- **Required:** Yes  
- **Description:** Expiration date of the identification card in YYYYMMDD format.  
- **Constraints:** Must be a future date.  
- **Default:** None  
- **Example:** "20301231"  

### **paxTicketInfos.nationality**
- **Type:** String  
- **Required:** Yes  
- **Description:** Passenger's nationality.  
- **Constraints:** Must be a valid ISO country code.  
- **Default:** None  
- **Example:** "SG"  

#### **paxTicketInfos.contactEmails**
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of passenger contact email addresses.  
- **Constraints:** Must contain valid email format.  
- **Default:** None  
- **Example:** ["KARIM.LATIFI2016@GMAIL.COM"]  

#### **paxTicketInfos.contactPhones**
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of passenger contact phone numbers.  
- **Constraints:** Must be a valid phone number format with country code.  
- **Default:** None  
- **Example:** ["0046-771407000"]  

## **Ancillaries** (Array)
- **Type:** Array  
- **Required:** No  
- **Description:** Additional services purchased by the passenger, such as baggage and seat selection.  
- **Constraints:** Can be empty if no ancillaries are selected.  
- **Default:** []  
- **Example:** [{...}]  

### **ancillaries.productCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Code representing the ancillary service. This is received from routing element in the search/revalidation response.
- **Constraints:** Must be a valid product code.  
- **Default:** None  
- **Example:** "BAG_5J_PH-PH_1_1P_20KG"  

### **ancillaries.segmentIndex**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Segment to which the ancillary applies.  
- **Constraints:** Must be a positive integer.  
- **Default:** None  
- **Example:** 1  

### **ancillaries.offerId**
- **Type:** String  
- **Required:** No  
- **Description:** Offer identifier for the ancillary service.  
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** AXOG123845861644119681  

### **ancillaries.buyMethod**
- **Type:** String  
- **Required:** Yes  
- **Description:** Purchase method for the ancillary service.  
- **Constraints:** Must be a valid string representation.  
- **Default:** None  
- **Example:** "0"  

### **ancillaries.ancillaryPrice**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Price of the ancillary product.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 38.02  

### **ancillaries.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency of the ancillary price.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** "USD"  

### **ancillaries.vendorPrice**
- **Type:** Float  
- **Required:** No  
- **Description:** Vendor's price for the ancillary product.  
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** null  

### **ancillaries.vendorCurrency**
- **Type:** String  
- **Required:** No  
- **Description:** Currency used by the vendor for the ancillary.  
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** null  

### **ancillaries.productType**
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of ancillary product.  

  Valid values:

  1: Standard Check-in baggage

  2: Cabin Baggage Overhead Locker

  6: Seat
- **Constraints:** Must be a valid string representation.  
- **Default:** None  
- **Example:** "1"  

### **ancillaries.displayCurrency**
- **Type:** String  
- **Required:** No  
- **Description:** Display currency for the ancillary price.  
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** null  

### **ancillaries.displayPrice**
- **Type:** Float  
- **Required:** No  
- **Description:** Price for the ancillary in display currency .  
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** null  

## **Ancillaries: Baggage Details**

### **auxBaggageElement** (Object)
- **Type:** Object  
- **Required:** Yes  
- **Description:** Details about the baggage included in the ancillary.  
- **Constraints:** None  
- **Default:** None  
- **Example:** {...}  

#### **auxBaggageElement.piece**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of baggage pieces allowed.  
- **Constraints:** Must be a non-negative integer.  
- **Default:** None  
- **Example:** 1  

#### **auxBaggageElement.weight**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Weight allowance per baggage piece in kg.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 20  

#### **auxBaggageElement.isAllWeight**
- **Type:** Boolean  
- **Required:** Yes  
- **Description:** Indicates whether the total weight is distributed among all pieces.  
- **Constraints:** true or false.  
- **Default:** true  
- **Example:** true  

#### **auxBaggageElement.size**
- **Type:** String  
- **Required:** No  
- **Description:** Dimensions of the baggage, if applicable.  
- **Constraints:** Can be empty.  
- **Default:** ""  
- **Example:** ""  

### **auxSeatElement** (Object)
- **Type:** Object  
- **Required:** Yes  
- **Description:** Details about the seat selection included in the ancillary.  
- **Constraints:** None  
- **Default:** None  
- **Example:** {...}  

#### **auxSeatElement.row**
- **Type:** String  
- **Required:** Yes  
- **Description:** Row number of the selected seat.  
- **Constraints:** Must be a valid row number.  
- **Default:** None  
- **Example:** "8"  

#### **auxSeatElement.column**
- **Type:** String  
- **Required:** Yes  
- **Description:** Column identifier of the selected seat.  
- **Constraints:** Must be a valid column designator.  
- **Default:** None  
- **Example:** "A"  


### **vendorFare** (Object)
- **Type:** Object  
- **Required:** Yes  
- **Description:** Details of vendor-specific pricing for different passenger types.  
- **Constraints:** Must contain valid pricing details.  
- **Default:** None  
- **Example:** {...}  

#### **vendorFare.vendorAdultPrice**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Price for an adult passenger.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 44.88  

#### **vendorFare.vendorAdultTax**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Tax applied for an adult passenger.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 0.12  

#### **vendorFare.vendorChildPrice**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Price for a child passenger.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 44.88  

#### **vendorFare.vendorChildTax**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Tax applied for a child passenger.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 0.12  

#### **vendorFare.vendorInfantPrice**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Price for an infant passenger.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 30  

#### **vendorFare.vendorInfantTax**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Tax applied for an infant passenger.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 0  

#### **vendorFare.vendorCurrency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency in which vendor pricing is displayed.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** "EUR"  

### **bundleOptions** (Array)
- **Type:** Array  
- **Required:** No  
- **Description:** Available fare bundles for selection.  
- **Constraints:** Can be empty.  
- **Default:** []  
- **Example:** []  

### **links** (Array)
- **Type:** Array  
- **Required:** No  
- **Description:** List of additional resources like terms and conditions.  
- **Constraints:** Can contain null values.  
- **Default:** []  
- **Example:** [{...}]  

#### **links.carrier**
- **Type:** String  
- **Required:** No  
- **Description:** Carrier associated with the link.  
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** null  

#### **links.kind**
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of link provided.  
- **Constraints:** Must be a valid string.  
- **Default:** None  
- **Example:** "terms"  

#### **links.link**
- **Type:** String  
- **Required:** No  
- **Description:** URL of the resource.  
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** null  

#### **links.description**
- **Type:** String  
- **Required:** Yes  
- **Description:** Description of the linked resource.  
- **Constraints:** Must be a valid string.  
- **Default:** None  
- **Example:** "Carrier terms and conditions"  

### **separateBookings**
- **Type:** Boolean  
- **Required:** Yes  
- **Description:** Indicates whether the bookings are processed separately.  
- **Constraints:** true or false.  
- **Default:** false  
- **Example:** false  

### **displayFare** (Object)
- **Type:** Object  
- **Required:** Yes  
- **Description:** Breakdown of the total fare in the display currency to the user.  
- **Constraints:** Must contain valid pricing details.  
- **Default:** None  
- **Example:** {...}  

#### **displayFare.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** The currency used for display fare.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** "EUR"  

#### **displayFare.exchangeRate**
- **Type:** Float  
- **Required:** Yes  
- **Description:** The exchange rate applied to convert the fare to the display currency.  
- **Constraints:** Must be a positive float value.  
- **Default:** 1  
- **Example:** 1  

#### **displayFare.adultPrice**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Price for an adult passenger in display currency.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 44.88  

#### **displayFare.adultTax**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Tax applied for an adult passenger in display currency.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 0.12  

#### **displayFare.childPrice**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Price for a child passenger in display currency.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 44.88  

#### **displayFare.childTax**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Tax applied for a child passenger in display currency.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 0.12  

#### **displayFare.infantPrice**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Price for an infant passenger in display currency.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 30  

#### **displayFare.infantTax**
- **Type:** Float  
- **Required:** Yes  
- **Description:** Tax applied for an infant passenger in display currency.  
- **Constraints:** Must be a positive float value.  
- **Default:** None  
- **Example:** 0  

### **paymentOptions** (Array)
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of available payment methods and associated fees.  
- **Constraints:** Must contain at least one valid payment option.  
- **Default:** None  
- **Example:** [{...}]  

#### **paymentOptions.paymentMethod**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Payment method identifier. 

  Valid values:

  1: Pre-payment

  3: VCC

  5: MOR
- **Constraints:** Must be a valid payment method.  
- **Default:** None  
- **Example:** 1  

#### **paymentOptions.serviceFee** (Object)
- **Type:** Object  
- **Required:** Yes  
- **Description:** Atlas transaction fee associated with the payment method.  
- **Constraints:** Must contain valid fee details.  
- **Default:** None  
- **Example:** {...}  

#### **paymentOptions.ticketFare** (Object)
- **Type:** Object  
- **Required:** No  
- **Description:** Fare amount deducted from a specific payment source.  
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** {...}  

#### **paymentOptions.paymentFee** (Object)
- **Type:** Object  
- **Required:** No  
- **Description:** Additional payment fee charged for that payment option. Example: VCC surcharge.
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** {...}  

### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Response status code.  
- **Constraints:** 0 indicates success.  
- **Default:** 0  
- **Example:** 0  

### **msg**
- **Type:** String  
- **Required:** No  
- **Description:** Response message.  
- **Constraints:** Can be null.  
- **Default:** null  
- **Example:** null  

*   #### **routing** (Object)

    Route and fare details. The structure is also Routing Elements, same as search response
{% endtab %}

{% tab title="Samples" %}
```
{
  "sessionId": "o_412ae4b089b54a7eae80e10a99c6b956",
  "offerId": "o_412ae4b089b54a7eae80e10a99c6b956_1",
  "orderNo": "AJZWC20250324144008152",
  "originalOrderNo": null,
  "ticketOrderNo": null,
  "totalPrice": 26.19,
  "totalTransactionFee": 0.5,
  "currency": "EUR",
  "vendorTotalPrice": 511.44,
  "vendorCurrency": "ZAR",
  "tktLimitTime": "2025-03-24 15:10:08",
  "pnrCode": "EGZOT3",
  "includeExtraBaggage": 0,
  "paxTicketInfos": [
    {
      "name": "Chamapiwa/Sailus",
      "passengerType": 0,
      "birthday": "19820211",
      "gender": "M",
      "cardNum": "8202116215181",
      "cardType": "PP",
      "cardIssuePlace": null,
      "cardExpired": "",
      "nationality": null,
      "ticketNos": [],
      "airlinePNRs": [],
      "contactEmails": [
        "sailus.chamapiwa@transnet.net"
      ],
      "contactPhones": [
        "0027-794177059"
      ],
      "ancillaries": [
        {
          "productCode": "SCI_SEAT_8A_FA_DUR_HLA",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 2.56,
          "currency": "EUR",
          "vendorPrice": null,
          "vendorCurrency": null,
          "productType": "6",
          "displayCurrency": null,
          "displayPrice": null,
          "auxBaggageElement": null,
          "auxSeatElement": {
            "row": "8",
            "column": "A"
          }
        }
      ]
    }
  ],
  "routing": {
    "fid": "qMUoH_0WrD8T-59gLuWpYQyRW461p0M0_OBiOR5ubboLmevgV4dL_w..",
    "routingIdentifier": "RFVSX0pOQl8xXzIwMjUwMzI3X18xXzBfMHxDWkUyNTk0NF9hcGlfMnwxfDIzLjYzXzIzLjYzXzQuNzNfMC41MF81Mi40OV9FVVJ8RFVSX0pOQl8xXzIwMjUwMzI3X18xXzBfMF5EVVItRkE0NzMtLUhMQS0yMDI1MDMyNzA3NTAtMjAyNTAzMjcwOTA1LVRBLTEtXjIzLjYzXzIzLjYzXzQuNzNfMC41MF81Mi40OV5BRkFBUElfQUZBQVBJXl5eWkFSXjQ2MS40NF40NjEuNDReOTIuMjl8MHwyMDI1MDMyNDE0NDAwOHwwfDE3NDI3OTg0MDg2OTdnRzBQdXx8fEdldE9mZmVyfHwwLjUwfDR8MHw=.kgVr8o1Cv+yM1rkf3iof08DAAhSjQdGOKhD1tetzZV0=",
    "supportCreditTransPayment": "0",
    "supportPaymentMethods": [
      1
    ],
    "currency": "EUR",
    "adultPrice": 14.42,
    "adultTax": 9.21,
    "childPrice": 14.42,
    "childTax": 9.21,
    "infantPrice": 4.73,
    "infantTax": 0,
    "infantAllowed": true,
    "transactionFeePerPax": 0.5,
    "transactionFee": 0.5,
    "transactionFeeMode": "PER_BOOKING",
    "nationalityType": 0,
    "nationality": "",
    "suitAge": "",
    "PaxType": "ADT",
    "fromSegments": [
      {
        "segmentIndex": 1,
        "carrier": "FA",
        "flightNumber": "FA473",
        "depAirport": "DUR",
        "depTime": "202503270750",
        "arrAirport": "HLA",
        "arrTime": "202503270905",
        "stopCities": "",
        "duration": 75,
        "codeShare": false,
        "cabin": "",
        "cabinClass": 1,
        "seatCount": 9,
        "aircraftCode": "738",
        "depTerminal": "",
        "arrTerminal": "",
        "operatingCarrier": "",
        "operatingFlightnumber": "",
        "fareFamily": "TA"
      }
    ],
    "retSegments": [],
    "combineIndexs": [],
    "rule": {
      "hasBaggage": 1,
      "baggageElements": [
        {
          "segmentNo": 1,
          "baggageType": "StandardCheckInBaggage",
          "passengerType": 0,
          "baggagePiece": 0,
          "baggageWeight": 0,
          "baggageSize": ""
        },
        {
          "segmentNo": 1,
          "baggageType": "StandardCheckInBaggage",
          "passengerType": 1,
          "baggagePiece": 0,
          "baggageWeight": 0,
          "baggageSize": ""
        },
        {
          "segmentNo": 1,
          "baggageType": "StandardCheckInBaggage",
          "passengerType": 2,
          "baggagePiece": 0,
          "baggageWeight": 0,
          "baggageSize": ""
        },
        {
          "segmentNo": 1,
          "baggageType": "CabinBaggageOverheadLocker",
          "passengerType": 0,
          "baggagePiece": 1,
          "baggageWeight": 7,
          "baggageSize": "56*36*25cm"
        },
        {
          "segmentNo": 1,
          "baggageType": "CabinBaggageOverheadLocker",
          "passengerType": 1,
          "baggagePiece": 1,
          "baggageWeight": 7,
          "baggageSize": "56*36*25cm"
        },
        {
          "segmentNo": 1,
          "baggageType": "CabinBaggageOverheadLocker",
          "passengerType": 2,
          "baggagePiece": 0,
          "baggageWeight": 0,
          "baggageSize": "56*36*25cm"
        }
      ],
      "refundRules": [
        {
          "refundType": 0,
          "refundStatus": "T",
          "refundFee": 0,
          "currency": "ZAR",
          "refNoshow": "T",
          "refNoShowCondition": 0,
          "refNoshowFee": 0,
          "ruleDetailList": [
            {
              "ruleId": 31911,
              "status": "H",
              "startMinute": 525600,
              "endMinute": 64800,
              "amount": 230.72,
              "currency": "ZAR"
            },
            {
              "ruleId": 31912,
              "status": "T",
              "startMinute": 64800,
              "endMinute": 0,
              "amount": 0,
              "currency": "ZAR"
            },
            {
              "ruleId": 31913,
              "status": "T",
              "startMinute": 0,
              "endMinute": -525600,
              "amount": 0,
              "currency": "ZAR"
            }
          ],
          "ruleList": [
            {
              "rowId": 31911,
              "gmtCreate": "Jun 24, 2024 11:41:45 AM",
              "gmtModified": "Jun 24, 2024 11:41:45 AM",
              "creator": null,
              "modifier": null,
              "isDeleted": "N",
              "airline": "FA",
              "ruleType": "self_refund",
              "ruleName": "self_refund_FA_1_vtgba0",
              "ruleKey": "self_refund_FA_202406241141441",
              "priority": 10,
              "validBeginTime": "Oct 8, 2019 12:00:00 AM",
              "validEndTime": "Jun 9, 2333 11:59:59 PM",
              "depCity": null,
              "arrCity": null,
              "depCountry": null,
              "arrCountry": null,
              "bookingCode": null,
              "fareFamily": null,
              "cabinClass": null,
              "timingMode": "depTime",
              "timeLeft": null,
              "timeRight": -64800,
              "travelBeginDate": null,
              "travelEndDate": null,
              "productType": null,
              "ruleExtend": {
                "ruleKey": "self_refund_FA_202406241141441",
                "canRefund": "Y",
                "canChange": null,
                "canRefundTax": "Y",
                "canRefundPkg": null,
                "canRefundCoupon": null,
                "canMakeUpDiff": null,
                "canNoShowRefund": null,
                "amount": null,
                "amountCurrency": null,
                "pricePercent": "0.5",
                "priceItem": "fare+tax",
                "taxItem": null,
                "charge": null,
                "chargeCurrency": null,
                "canExemptSameDay": null,
                "exemptDuration": null,
                "ticketBeginTime": null,
                "ticketEndTime": null,
                "applyBeginTime": null,
                "applyEndTime": null,
                "travelBeginTime": null,
                "travelEndTime": null
              }
            },
            {
              "rowId": 31912,
              "gmtCreate": "Jun 24, 2024 11:41:45 AM",
              "gmtModified": "Jun 24, 2024 11:41:45 AM",
              "creator": null,
              "modifier": null,
              "isDeleted": "N",
              "airline": "FA",
              "ruleType": "self_refund",
              "ruleName": "self_refund_FA_2_iQPszP",
              "ruleKey": "self_refund_FA_202406241141442",
              "priority": 10,
              "validBeginTime": "Oct 8, 2019 12:00:00 AM",
              "validEndTime": "Jun 9, 2333 11:59:59 PM",
              "depCity": null,
              "arrCity": null,
              "depCountry": null,
              "arrCountry": null,
              "bookingCode": null,
              "fareFamily": null,
              "cabinClass": null,
              "timingMode": "depTime",
              "timeLeft": -64800,
              "timeRight": 0,
              "travelBeginDate": null,
              "travelEndDate": null,
              "productType": null,
              "ruleExtend": {
                "ruleKey": "self_refund_FA_202406241141442",
                "canRefund": "N",
                "canChange": null,
                "canRefundTax": "N",
                "canRefundPkg": null,
                "canRefundCoupon": null,
                "canMakeUpDiff": null,
                "canNoShowRefund": null,
                "amount": null,
                "amountCurrency": null,
                "pricePercent": null,
                "priceItem": "fare+tax",
                "taxItem": null,
                "charge": null,
                "chargeCurrency": null,
                "canExemptSameDay": null,
                "exemptDuration": null,
                "ticketBeginTime": null,
                "ticketEndTime": null,
                "applyBeginTime": null,
                "applyEndTime": null,
                "travelBeginTime": null,
                "travelEndTime": null
              }
            },
            {
              "rowId": 31913,
              "gmtCreate": "Jun 24, 2024 11:41:45 AM",
              "gmtModified": "Jun 24, 2024 11:41:45 AM",
              "creator": null,
              "modifier": null,
              "isDeleted": "N",
              "airline": "FA",
              "ruleType": "self_refund",
              "ruleName": "self_refund_FA_3_m03oLw",
              "ruleKey": "self_refund_FA_202406241141443",
              "priority": 10,
              "validBeginTime": "Oct 8, 2019 12:00:00 AM",
              "validEndTime": "Jun 9, 2333 11:59:59 PM",
              "depCity": null,
              "arrCity": null,
              "depCountry": null,
              "arrCountry": null,
              "bookingCode": null,
              "fareFamily": null,
              "cabinClass": null,
              "timingMode": "depTime",
              "timeLeft": 0,
              "timeRight": null,
              "travelBeginDate": null,
              "travelEndDate": null,
              "productType": null,
              "ruleExtend": {
                "ruleKey": "self_refund_FA_202406241141443",
                "canRefund": "N",
                "canChange": null,
                "canRefundTax": "N",
                "canRefundPkg": null,
                "canRefundCoupon": null,
                "canMakeUpDiff": null,
                "canNoShowRefund": null,
                "amount": null,
                "amountCurrency": null,
                "pricePercent": null,
                "priceItem": "fare+tax",
                "taxItem": null,
                "charge": null,
                "chargeCurrency": null,
                "canExemptSameDay": null,
                "exemptDuration": null,
                "ticketBeginTime": null,
                "ticketEndTime": null,
                "applyBeginTime": null,
                "applyEndTime": null,
                "travelBeginTime": null,
                "travelEndTime": null
              }
            }
          ]
        }
      ],
      "changesRules": [
        {
          "changesType": 0,
          "changesStatus": "T",
          "changesFee": 0,
          "currency": "ZAR",
          "revNoshow": "T",
          "revNoShowCondition": 0,
          "revNoshowFee": 0,
          "ruleList": [
            {
              "rowId": 31914,
              "gmtCreate": "Jun 24, 2024 11:41:57 AM",
              "gmtModified": "Jun 24, 2024 11:41:57 AM",
              "creator": null,
              "modifier": null,
              "isDeleted": "N",
              "airline": "FA",
              "ruleType": "self_change",
              "ruleName": "self_change_FA_1_XrDAyc",
              "ruleKey": "self_change_FA_202406241141571",
              "priority": 10,
              "validBeginTime": "Oct 8, 2019 12:00:00 AM",
              "validEndTime": "Jun 9, 2333 11:59:59 PM",
              "depCity": null,
              "arrCity": null,
              "depCountry": null,
              "arrCountry": null,
              "bookingCode": null,
              "fareFamily": null,
              "cabinClass": null,
              "timingMode": "depTime",
              "timeLeft": null,
              "timeRight": -240,
              "travelBeginDate": null,
              "travelEndDate": null,
              "productType": null,
              "ruleExtend": {
                "ruleKey": "self_change_FA_202406241141571",
                "canRefund": "Y",
                "canChange": null,
                "canRefundTax": "N",
                "canRefundPkg": null,
                "canRefundCoupon": null,
                "canMakeUpDiff": null,
                "canNoShowRefund": null,
                "amount": 300,
                "amountCurrency": "ZAR",
                "pricePercent": null,
                "priceItem": "fare+tax",
                "taxItem": null,
                "charge": null,
                "chargeCurrency": null,
                "canExemptSameDay": null,
                "exemptDuration": null,
                "ticketBeginTime": null,
                "ticketEndTime": null,
                "applyBeginTime": null,
                "applyEndTime": null,
                "travelBeginTime": null,
                "travelEndTime": null
              }
            },
            {
              "rowId": 31915,
              "gmtCreate": "Jun 24, 2024 11:41:57 AM",
              "gmtModified": "Jun 24, 2024 11:41:57 AM",
              "creator": null,
              "modifier": null,
              "isDeleted": "N",
              "airline": "FA",
              "ruleType": "self_change",
              "ruleName": "self_change_FA_2_tlSdPH",
              "ruleKey": "self_change_FA_202406241141572",
              "priority": 10,
              "validBeginTime": "Oct 8, 2019 12:00:00 AM",
              "validEndTime": "Jun 9, 2333 11:59:59 PM",
              "depCity": null,
              "arrCity": null,
              "depCountry": null,
              "arrCountry": null,
              "bookingCode": null,
              "fareFamily": null,
              "cabinClass": null,
              "timingMode": "depTime",
              "timeLeft": -240,
              "timeRight": 0,
              "travelBeginDate": null,
              "travelEndDate": null,
              "productType": null,
              "ruleExtend": {
                "ruleKey": "self_change_FA_202406241141572",
                "canRefund": "N",
                "canChange": null,
                "canRefundTax": "N",
                "canRefundPkg": null,
                "canRefundCoupon": null,
                "canMakeUpDiff": null,
                "canNoShowRefund": null,
                "amount": null,
                "amountCurrency": null,
                "pricePercent": null,
                "priceItem": "fare+tax",
                "taxItem": null,
                "charge": null,
                "chargeCurrency": null,
                "canExemptSameDay": null,
                "exemptDuration": null,
                "ticketBeginTime": null,
                "ticketEndTime": null,
                "applyBeginTime": null,
                "applyEndTime": null,
                "travelBeginTime": null,
                "travelEndTime": null
              }
            },
            {
              "rowId": 31916,
              "gmtCreate": "Jun 24, 2024 11:41:57 AM",
              "gmtModified": "Jun 24, 2024 11:41:57 AM",
              "creator": null,
              "modifier": null,
              "isDeleted": "N",
              "airline": "FA",
              "ruleType": "self_change",
              "ruleName": "self_change_FA_3_zvwPU0",
              "ruleKey": "self_change_FA_202406241141573",
              "priority": 10,
              "validBeginTime": "Oct 8, 2019 12:00:00 AM",
              "validEndTime": "Jun 9, 2333 11:59:59 PM",
              "depCity": null,
              "arrCity": null,
              "depCountry": null,
              "arrCountry": null,
              "bookingCode": null,
              "fareFamily": null,
              "cabinClass": null,
              "timingMode": "depTime",
              "timeLeft": 0,
              "timeRight": null,
              "travelBeginDate": null,
              "travelEndDate": null,
              "productType": null,
              "ruleExtend": {
                "ruleKey": "self_change_FA_202406241141573",
                "canRefund": "N",
                "canChange": null,
                "canRefundTax": "N",
                "canRefundPkg": null,
                "canRefundCoupon": null,
                "canMakeUpDiff": null,
                "canNoShowRefund": null,
                "amount": null,
                "amountCurrency": null,
                "pricePercent": null,
                "priceItem": "fare+tax",
                "taxItem": null,
                "charge": null,
                "chargeCurrency": null,
                "canExemptSameDay": null,
                "exemptDuration": null,
                "ticketBeginTime": null,
                "ticketEndTime": null,
                "applyBeginTime": null,
                "applyEndTime": null,
                "travelBeginTime": null,
                "travelEndTime": null
              }
            }
          ],
          "ruleDetailList": [
            {
              "ruleId": 31914,
              "status": "H",
              "startMinute": 525600,
              "endMinute": 240,
              "amount": 300,
              "currency": "ZAR"
            },
            {
              "ruleId": 31915,
              "status": "T",
              "startMinute": 240,
              "endMinute": 0,
              "amount": 0,
              "currency": "ZAR"
            },
            {
              "ruleId": 31916,
              "status": "T",
              "startMinute": 0,
              "endMinute": -525600,
              "amount": 0,
              "currency": "ZAR"
            }
          ]
        }
      ],
      "serviceElements": [
        {
          "hasFreeSeat": 0,
          "hasFreeMeal": 0
        }
      ]
    },
    "ancillaryProductElements": [
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_1PC_20KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 1,
        "price": 7.94,
        "currency": "EUR",
        "vendorPrice": 155,
        "vendorCurrency": "ZAR",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 20,
          "isAllWeight": true,
          "size": ""
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_BAG_1PC_20KG",
        "auxSeatElement": null,
        "displayPrice": null,
        "displayCurrency": null
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_2PC_40KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 1,
        "price": 20.74,
        "currency": "EUR",
        "vendorPrice": 405,
        "vendorCurrency": "ZAR",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 2,
          "weight": 40,
          "isAllWeight": true,
          "size": ""
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_BAG_2PC_40KG",
        "auxSeatElement": null,
        "displayPrice": null,
        "displayCurrency": null
      }
    ],
    "vendorFare": null,
    "bundleOptions": [],
    "links": [
      {
        "carrier": null,
        "kind": "terms",
        "link": null,
        "description": "Carrier terms and conditions"
      }
    ],
    "separateBookings": false,
    "refreshTime": null,
    "displayFare": null,
    "ancillarySupported": [
      "seat",
      "luggage"
    ]
  },
  "duplicateOrders": null,
  "paymentOptions": [
    {
      "paymentMethod": 1,
      "serviceFee": {
        "amount": 0.5,
        "currency": "EUR",
        "deductFrom": "DEPOSIT"
      },
      "ticketFare": {
        "amount": 26.19,
        "currency": "EUR",
        "deductFrom": "DEPOSIT"
      },
      "paymentFee": null
    }
  ],
  "status": 0,
  "msg": null
}
```
{% endtab %}
{% endtabs %}
