<h4>Payment using Debit/Credit Card Token</h4>
```java
  CitrusClient citrusClient = CitrusClient.getInstance(context); // Activity Context
  // No need to call init on CitrusClient if already done.

// Step 1 - Get All the saved instruments.(getWallet method of SDK).
// Step 2 - Display List on the UI.
// Step 3 - If option selected by user is CardOption , call setCardCVV method and send payment option to SDK.
// Set the CVV for cardOption
cardOption.setCardCVV(cvv); //cardOption is the option selected by user on UI.
  // Init Net Banking PaymentType     
  PaymentType.PGPayment pgPayment = new PaymentType.PGPayment(amount, BILL_URL, cardOption, new CitrusUser("developercitrus@gmail.com","9876543210"));

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
  
// Step 1 - Get All the saved instruments.(getWallet method of SDK).
// Step 2 - Display List on the UI.
// Step 3 - If option selected by user is NetbankingOption , send NetbankingOption to SDK.

  // Init Net Banking PaymentType     
  PaymentType.PGPayment pgPayment = new PaymentType.PGPayment(amount, BILL_URL, ne, netbankingOption CitrusUser("developercitrus@gmail.com","9876543210"));

  citrusClient.pgPayment(pgPayment, new Callback<TransactionResponse>() {

     @Override
     public void success(TransactionResponse transactionResponse) { }

     @Override
     public void error(CitrusError error) { }
  });
  ```
