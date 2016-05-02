<h4>Payment using Debit Card Token</h4>
```java
  CitrusClient citrusClient = CitrusClient.getInstance(context); // Activity Context
  // No need to call init on CitrusClient if already done.

// Get the Saved Card Option from the payment options list returned by the getwallet api
DebitCardOption cardOption = null;
for (PaymentOption paymentOption : paymentOptionsList) {
      if (paymentOption instanceOf CardOption) {
            cardOption = (CardOption) paymentOption;
            break;
      }
}
// Set the CVV for cardOption
cardOption.setCardCVV(cvv); //set the CVV 


  

  // Init Net Banking PaymentType     
  PaymentType.PGPayment pgPayment = new PaymentType.PGPayment(amount, BILL_URL, cardOption, new CitrusUser("developercitrus@gmail.com","9876543210"));

  citrusClient.pgPayment(pgPayment, new Callback<TransactionResponse>() {

     @Override
     public void success(TransactionResponse transactionResponse) { }

     @Override
     public void error(CitrusError error) { }
  });
  ```
  
 <h4>Payment using Credit Card Token</h4>
```java
  CitrusClient citrusClient = CitrusClient.getInstance(context); // Activity Context
  // No need to call init on CitrusClient if already done.

  CreditCardOption creditCardOption = new CreditCardOption("d7505f22bca20a97f8d8f305530e88a9", "123");

  // Init Net Banking PaymentType     
  PaymentType.PGPayment pgPayment = new PaymentType.PGPayment(amount, BILL_URL, creditCardOption, new CitrusUser("developercitrus@gmail.com","9876543210"));

  citrusClient.pgPayment(pgPayment, new Callback<TransactionResponse>() {

     @Override
     public void success(TransactionResponse transactionResponse) { }

     @Override
     public void error(CitrusError error) { }
  });
  ```
  
<h4>Payment using Bank Token</h4>
```java
   CitrusClient citrusClient = CitrusClient.getInstance(context); // Activity Context
  // No need to call init on CitrusClient if already done.

  NetbankingOption netbankingOption = new NetbankingOption("b66352b2d465699d6fa7cfb520ba27b5");

  // Init Net Banking PaymentType     
  PaymentType.PGPayment pgPayment = new PaymentType.PGPayment(amount, BILL_URL, ne, netbankingOption CitrusUser("developercitrus@gmail.com","9876543210"));

  citrusClient.pgPayment(pgPayment, new Callback<TransactionResponse>() {

     @Override
     public void success(TransactionResponse transactionResponse) { }

     @Override
     public void error(CitrusError error) { }
  });
  ```
