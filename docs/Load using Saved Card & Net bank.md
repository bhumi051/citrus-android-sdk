<h4>Load/Add Money using Debit/Credit Card Token</h4>
```java
     CitrusClient citrusClient = CitrusClient.getInstance(context); // Activity Context
  // No need to call init on CitrusClient if already done.

// Step 1 - Get All the saved instruments.(getWallet method of SDK).
// Step 2 - Display List on the UI.
// Step 3 - If option selected by user is CardOption , call setCardCVV method and send payment option to SDK.
// Set the CVV for cardOption
  cardOption.setCardCVV(cvv); //cardOption is the option selected by user on UI.

  // Init PaymentType     
  PaymentType.LoadMoney loadMoney = new PaymentType.LoadMoney(amount, LOAD_MONEY_RETURN_URL, debitCardOption);

  citrusClient.simpliPay(loadMoney, new Callback<TransactionResponse>() {

     @Override
     public void success(TransactionResponse transactionResponse) { }

     @Override
     public void error(CitrusError error) { }
  });

  ```

<h4>Load/Add Money using Bank Token</h4>
```java
     CitrusClient citrusClient = CitrusClient.getInstance(context); // Activity Context
  // No need to call init on CitrusClient if already done.

// Step 1 - Get All the saved instruments.(getWallet method of SDK).
// Step 2 - Display List on the UI.
// Step 3 - If option selected by user is NetBanking Option ,  send payment option to SDK.

  // Init PaymentType     
  PaymentType.LoadMoney loadMoney = new PaymentType.LoadMoney(amount, LOAD_MONEY_RETURN_URL, netBankingOption);
//netBankingOption is the option selected by user on the UI.
  citrusClient.simpliPay(loadMoney, new Callback<TransactionResponse>() {

     @Override
     public void success(TransactionResponse transactionResponse) { }

     @Override
     public void error(CitrusError error) { }
  });
  ```
