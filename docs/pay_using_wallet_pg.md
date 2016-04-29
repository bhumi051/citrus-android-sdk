### Pay Using Wallet PG

#### Paying through Wallet will enable the user using any of the payment instrument like Citrus Cash and/or MVC and/or Cards and/or Netbanking.
The user can choose to pay using just one or a combination of above payment modes.

Following are the steps to implement wallet payments.
* Get Wallet
```java
List<PaymentOption> paymentOptionsList = null;

CitrusClient.getWallet(new Callback<List<PaymentOption>>() {
            @Override
            public void success(List<PaymentOption> paymentOptions) {
                paymentOptionsList = paymentOptions;
            }

            @Override
            public void error(CitrusError error) {
               
            }
        });
```

This will return the list of payment options for the logged in user.
The list includes all the saved payment instruments as well as Citrus Cash and MVC as payment modes.

You need to present user with the UI to decide to the user using which payment instrument the user wants to make the payment.

### Initiate Payment (For total transaction amount &#8377; 100

### Payment Using CitrusCash (If the citrusCash balance is sufficient)
```java
PaymentType.CitrusCash paymentType = new PaymentType.CitrusCash(new Amount("5"),"BILL_URL");
citrusClient.smartPay(paymentType,callback);
```

### Payment Using MVC(Merchant Virtual Currency) (If the MVC balance is sufficient)
```java
Amount amount = new Amount("100");
boolean useCitrusCash = false;
boolean useMVC = true;
PaymentType.SplitPayment paymentType = new PaymentType.SplitPayment(amount, Constants.BILL_URL, null,useCitrusCash, useMVC);
citrusClient.smartPay(paymentType , callback);
```

### Payment Using Saved Cards
```java
Amount amount = new Amount("100");
// Get the Saved Card Option from the payment options list returned by the getwallet api
CardOption cardOption = null;
for (PaymentOption paymentOption : paymentOptionsList) {
      if (paymentOption instanceOf CardOption) {
            cardOption = (CardOption) paymentOption;
            break;
      }
}
// Set the CVV for cardOption
cardOption.setCardCVV(cvv);
boolean useCitrusCash = false;
boolean useMVC = false;
PaymentType.SplitPayment paymentType = new PaymentType.SplitPayment(amount, Constants.BILL_URL, cardOption,useCitrusCash, useMVC);
citrusClient.smartPay( paymentType , callback);

```

### Payment Using Saved Netbanking
```java
Amount amount = new Amount("100");

// Get the Saved Netbaking payment mode from the payment options list returned by the getwallet api
NetbankingOption netbankingOption = null;
for (PaymentOption paymentOption : paymentOptionsList) {
      if (paymentOption instanceOf NetbankingOption) {
            netbankingOption = (NetbankingOption) paymentOption;
            break;
      }
}
// Set the transaction amount for the particular payment option.
netbankingOption.setTransactionAmount(amount);

List<PaymentOption> walletPaymentOptionsList = new ArrayList<>();
// Add the payment option in the list.
walletPaymentOptionsList.add(netbankingOption);

PaymentType.WalletPGPayment paymentType = new PaymentType.WalletPGPayment(amount, Constants.BILL_URL, walletPaymentOptionsList);
citrusClient.walletPGCharge( paymentType, callback);
```

### Payment Using Debit Card
```java
Amount amount = new Amount("100");

CardOption debitCardOption =new DebitCardOption("Salil", "411111111111111", "123", Month.getMonth("12"), Year.getYear("2020"));

// Set the transaction amount for the particular payment option.
debitCardOption.setTransactionAmount(amount);

List<PaymentOption> walletPaymentOptionsList = new ArrayList<>();
// Add the payment option in the list.
walletPaymentOptionsList.add(debitCardOption);

PaymentType.WalletPGPayment paymentType = new PaymentType.WalletPGPayment(amount, Constants.BILL_URL, walletPaymentOptionsList);
citrusClient.walletPGCharge(paymentType, callback);
```

### Payment Using Credit Card
```java
Amount amount = new Amount("100");

// Get the MVC payment mode from the payment options list returned by the getwallet api
CardOption creditCardOption =new CreditCardOption("Salil", "411111111111111", "123", Month.getMonth("12"), Year.getYear("2020"));

// Set the transaction amount for the particular payment option.
creditCardOption.setTransactionAmount(amount);

List<PaymentOption> walletPaymentOptionsList = new ArrayList<>();
// Add the payment option in the list.
walletPaymentOptionsList.add(creditCardOption);

PaymentType.WalletPGPayment paymentType = new PaymentType.WalletPGPayment(amount, Constants.BILL_URL, walletPaymentOptionsList);
citrusClient.walletPGCharge(paymentType, callback);
```

### Payment Using Netbanking
```java
Amount amount = new Amount("100");

NetbankingOption netbankingOption = new NetbankingOption("ICICI Bank", "CID001");
// Set the transaction amount for the particular payment option.
netbankingOption.setTransactionAmount(amount);

List<PaymentOption> walletPaymentOptionsList = new ArrayList<>();
// Add the payment option in the list.
walletPaymentOptionsList.add(netbankingOption);

PaymentType.WalletPGPayment paymentType = new PaymentType.WalletPGPayment(amount, Constants.BILL_URL, walletPaymentOptionsList);
citrusClient.walletPGCharge( paymentType, callback);
```
----

## Split Payments
Split Payments allow the users to pay partial amount using the wallet and remaining amount using other payment options such as Credit Card, Debit Card or Netbanking.

Suppose: Total Transaction Amount is &#8377; 100.
Citrus Cash Balance: &#8377; 50
MVC Balance: &#8377; 30

## Split Payments using MVC + Other Payment Option

```java
Amount totalAmount = new Amount("100");

// Get the MVC payment mode from the payment options list returned by the getwallet api
MVCOption mvcOption = null;
for (PaymentOption paymentOption : paymentOptionsList) {
      if (paymentOption instanceOf MVCOption) {
            mvcOption = (MVCOption) paymentOption;
            break;
      }
}
// Set the transaction amount for the particular payment option.
mvcOption.setTransactionAmount(mvcOption.getMaxBalance());

// Remaing amount to be paid using other payment option is 80.
Amount remainingAmount = new Amount("80");
PaymentOption paymentOption = null;

```
##### Netbanking

``` java
paymentOption = new NetbankingOption("ICICI Bank", "CID001");
// Set the transaction amount for the particular payment option.
paymentOption.setTransactionAmount(remainingAmount);
```

##### Or CreditCard
``` java
paymentOption = new CreditCardOption("Salil", "411111111111111", "123", Month.getMonth("12"), Year.getYear("2020"));
// Set the transaction amount for the particular payment option.
paymentOption.setTransactionAmount(remainingAmount);
```

##### Or DebitCard
``` java
paymentOption = new DebitCardOption("Salil", "411111111111111", "123", Month.getMonth("12"), Year.getYear("2020"));
// Set the transaction amount for the particular payment option.
paymentOption.setTransactionAmount(remainingAmount);
```

```java
List<PaymentOption> walletPaymentOptionsList = new ArrayList<>();
// Add the payment option in the list.
walletPaymentOptionsList.add(paymentOption);

PaymentType.WalletPGPayment paymentType = new PaymentType.WalletPGPayment(totalAmount, Constants.BILL_URL, walletPaymentOptionsList);
citrusClient.walletPGCharge( paymentType, callback);
```
----

## Split Payments using Citrus Cash + Other Payment Option

```java
Amount totalAmount = new Amount("100");

// Get the MVC payment mode from the payment options list returned by the getwallet api
CitrusCash citrusCash = null;
for (PaymentOption paymentOption : paymentOptionsList) {
      if (paymentOption instanceOf CitrusCash) {
            citrusCash = (CitrusCash) paymentOption;
            break;
      }
}
// Set the transaction amount for the particular payment option.
citrusCash.setTransactionAmount(citrusCash.getMaxBalance());

// Remaing amount to be paid using other payment option is 50.
Amount remainingAmount = new Amount("50");
PaymentOption paymentOption = null;

```
##### Netbanking

``` java
paymentOption = new NetbankingOption("ICICI Bank", "CID001");
// Set the transaction amount for the particular payment option.
paymentOption.setTransactionAmount(remainingAmount);
```

##### Or CreditCard
``` java
paymentOption = new CreditCardOption("Salil", "411111111111111", "123", Month.getMonth("12"), Year.getYear("2020"));
// Set the transaction amount for the particular payment option.
paymentOption.setTransactionAmount(remainingAmount);
```

##### Or DebitCard
``` java
paymentOption = new DebitCardOption("Salil", "411111111111111", "123", Month.getMonth("12"), Year.getYear("2020"));
// Set the transaction amount for the particular payment option.
paymentOption.setTransactionAmount(remainingAmount);
```

```java
List<PaymentOption> walletPaymentOptionsList = new ArrayList<>();
// Add the payment option in the list.
walletPaymentOptionsList.add(paymentOption);

PaymentType.WalletPGPayment paymentType = new PaymentType.WalletPGPayment(totalAmount, Constants.BILL_URL, walletPaymentOptionsList);
citrusClient.walletPGCharge( paymentType, callback);
```
----

## Split Payments using MVC + Citrus Cash + Other Payment Option

```java
Amount totalAmount = new Amount("100");

// Get the MVC payment mode from the payment options list returned by the getwallet api
CitrusCash citrusCash = null;
MVCOption mvcOption = null;
for (PaymentOption paymentOption : paymentOptionsList) {
      if (paymentOption instanceOf MVCOption) {
            mvcOption = (MVCOption) paymentOption;
            break;
      }
}

for (PaymentOption paymentOption : paymentOptionsList) {
      if (paymentOption instanceOf CitrusCash) {
            citrusCash = (CitrusCash) paymentOption;
            break;
      }
}

// Set the transaction amount for the particular payment option.
citrusCash.setTransactionAmount(citrusCash.getMaxBalance()); // Rs. 50

// Set the transaction amount for the particular payment option.
mvcOption.setTransactionAmount(mvcOption.getMaxBalance()); // Rs. 30

// Remaing amount to be paid using other payment option is 20.
Amount remainingAmount = new Amount("20");
PaymentOption paymentOption = null;

```
##### Netbanking

``` java
paymentOption = new NetbankingOption("ICICI Bank", "CID001");
// Set the transaction amount for the particular payment option.
paymentOption.setTransactionAmount(remainingAmount);
```

##### Or CreditCard
``` java
paymentOption = new CreditCardOption("Salil", "411111111111111", "123", Month.getMonth("12"), Year.getYear("2020"));
// Set the transaction amount for the particular payment option.
paymentOption.setTransactionAmount(remainingAmount);
```

##### Or DebitCard
``` java
paymentOption = new DebitCardOption("Salil", "411111111111111", "123", Month.getMonth("12"), Year.getYear("2020"));
// Set the transaction amount for the particular payment option.
paymentOption.setTransactionAmount(remainingAmount);
```

```java
List<PaymentOption> walletPaymentOptionsList = new ArrayList<>();
// Add the payment option in the list.
walletPaymentOptionsList.add(paymentOption);

PaymentType.WalletPGPayment paymentType = new PaymentType.WalletPGPayment(totalAmount, Constants.BILL_URL, walletPaymentOptionsList);
citrusClient.walletPGCharge( paymentType, callback);
```
