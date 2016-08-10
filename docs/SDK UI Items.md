##SDK UI Items
###SDK provides few UI items which can be used in app while accepting payment details.

###CardNumberEditText
This UI item can be used to accept card number details. This edittext shows the card icon as soon as first few digits are entered as well as aligns card number.
You can add this widget in your layout xml file as below

```
    <com.citrus.widgets.CardNumberEditText
                   
                    /** add other properties as required**/        
    />
```
You can refer **fragment_credit_debit_card.xml** and **CreditDebitCardFragment** in Example app for usage.

###CardExpiry
This UI item can be used to accept expiry date. It will automatically append / in between month and expiry
You can add this widget in your layout xml file as below

```
    <com.citrus.widgets.ExpiryDate
                
                    /** add other properties as required**/        
    />
```

You can refer **fragment_credit_debit_card.xml** and **CreditDebitCardFragment** in Example app for usage.
