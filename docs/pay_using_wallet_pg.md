### Pay Using Wallet PG

#### Paying through Wallet will enable the user using any of the payment instrument like Citrus Cash and/or MVC and/or Cards and/or Netbanking.
The user can choose to pay using just one or a combination of above payment modes.

Following are the steps to implement wallet payments.
* Get Wallet
```java
      CitrusClient.getWallet(callback);

This will return the list of payment options for the logged in user.
The list includes all the saved payment instruments as well as Citrus Cash and MVC as payment modes.

You need to present user with the UI to decide to the user using which payment instrument the user wants to make the payment.

### Initiate Payment

#### Initialize the paymentoptions list.
```java
  List<PaymentOption> paymentOptionList = new ArrayList<>();
  // Set the transaction amount for the particular payment option.
  paymentOption.setTransactionAmount(amount);
  // Add the payment option in the list.
  paymentOptionList.add(paymentOption);
  
  PaymentType.WalletPGPayment paymentType = new PaymentType.WalletPGPayment(amount, Constants.BILL_URL, paymentOptionList);
  citrusClient.walletPGCharge((PaymentType.WalletPGPayment) paymentType, callback);
 
