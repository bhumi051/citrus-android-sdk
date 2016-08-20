<b>Passing user details in Payment</b>

1. SDK provides a different constructor to pass user details in Payment.

2. Atleast email and mobile number should be passed.

3. Dummy user details passed to payment may cause unexpected result as its difficult to trace the transaction of specific user.

4. If no user details are passed, SDK will fecth email and mobile set against the user from profile and will be sent for payment.

5. If no user details are found in profile, SDK will send dummy data for the transaction.

Please refer below sample code for passing user details
```java
  CitrusClient citrusClient = CitrusClient.getInstance(context); // Activity Context
  CardOption cardOption = new DebitCardOption(cardHolderName, cardNumber, cardCVV, month, year);//can be credit card, saved card, NetBanking Option
  CitrusUser citrusUser = new CitrusUser(email,mobile);//pass user details 
  PaymentType.PGPayment pgPayment = new PaymentType.PGPayment(amount, BILL_URL, cardOption, citrusUser);

  citrusClient.simpliPay(pgPayment, new Callback<TransactionResponse>() { //can be pgPayment, CitrusCash

     @Override
     public void success(TransactionResponse transactionResponse) { }

     @Override
     public void error(CitrusError error) { }
  });
 ```
