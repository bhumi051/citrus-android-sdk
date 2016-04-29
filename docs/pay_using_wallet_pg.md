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
Amount amount = new Amount("100");
PaymentType.CitrusCash paymentType = new PaymentType.CitrusCash(amount,Constants.BILL_URL);
citrusClient.smartPay(paymentType,callback);

//or

Amount amount = new Amount("100");
boolean useCitrusCash = true;
boolean useMVC = false;
PaymentType.SplitPayment paymentType = new PaymentType.SplitPayment(amount, Constants.BILL_URL, null,useCitrusCash, useMVC);
citrusClient.smartPay(paymentType , callback);
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
boolean useCitrusCash = false;
boolean useMVC = false;
PaymentType.SplitPayment paymentType = new PaymentType.SplitPayment(amount, Constants.BILL_URL, netbankingOption,useCitrusCash, useMVC);
citrusClient.smartPay( paymentType , callback);

```

### Payment Using Debit Card
```java
Amount amount = new Amount("100");

CardOption debitCardOption =new DebitCardOption("Salil", "411111111111111", "123", Month.getMonth("12"), Year.getYear("2020"));

boolean useCitrusCash = false;
boolean useMVC = false;
PaymentType.SplitPayment paymentType = new PaymentType.SplitPayment(amount, Constants.BILL_URL, debitCardOption,useCitrusCash, useMVC);
citrusClient.smartPay( paymentType , callback);


```

### Payment Using Credit Card
```java
Amount amount = new Amount("100");

// Get the MVC payment mode from the payment options list returned by the getwallet api
CardOption creditCardOption =new CreditCardOption("Salil", "411111111111111", "123", Month.getMonth("12"), Year.getYear("2020"));

boolean useCitrusCash = false;
boolean useMVC = false;
PaymentType.SplitPayment paymentType = new PaymentType.SplitPayment(amount, Constants.BILL_URL, creditCardOption,useCitrusCash, useMVC);
citrusClient.smartPay( paymentType , callback);
```

### Payment Using Netbanking
```java
Amount amount = new Amount("100");

NetbankingOption netbankingOption = new NetbankingOption("ICICI Bank", "CID001");

boolean useCitrusCash = false;
boolean useMVC = false;
PaymentType.SplitPayment paymentType = new PaymentType.SplitPayment(amount, Constants.BILL_URL, netbankingOption,useCitrusCash, useMVC);
citrusClient.smartPay( paymentType , callback);
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

boolean useMVC = true;
boolean useCitrusCash = false;
PaymentOption paymentOption = null;

//Netbanking
paymentOption = new NetbankingOption("ICICI Bank", "CID001");
// Or CreditCard
paymentOption = new CreditCardOption("Salil", "411111111111111", "123", Month.getMonth("12"), Year.getYear("2020"));
// Or DebitCard
paymentOption = new DebitCardOption("Salil", "411111111111111", "123", Month.getMonth("12"), Year.getYear("2020"));
PaymentType.SplitPayment paymentType = new PaymentType.SplitPayment(amount, Constants.BILL_URL, paymentOption,useCitrusCash, useMVC);
citrusClient.smartPay( paymentType , callback);
```
----

## Split Payments using Citrus Cash + Other Payment Option

```java
Amount totalAmount = new Amount("100");
boolean useMVC = false;
boolean useCitrusCash = true;
PaymentOption paymentOption = null;
```
##### Netbanking

``` java
paymentOption = new NetbankingOption("ICICI Bank", "CID001");
```

##### Or CreditCard
``` java
paymentOption = new CreditCardOption("Salil", "411111111111111", "123", Month.getMonth("12"), Year.getYear("2020"));
```

##### Or DebitCard
``` java
paymentOption = new DebitCardOption("Salil", "411111111111111", "123", Month.getMonth("12"), Year.getYear("2020"));
```

```java
PaymentType.SplitPayment paymentType = new PaymentType.SplitPayment(amount, Constants.BILL_URL, paymentOption,useCitrusCash, useMVC);
citrusClient.smartPay( paymentType , callback);
```
----

## Split Payments using MVC + Citrus Cash + Other Payment Option

```java
Amount totalAmount = new Amount("100");

boolean useMVC = true;
boolean useCitrusCash = true;
PaymentOption paymentOption = null;

```
##### Netbanking

``` java
paymentOption = new NetbankingOption("ICICI Bank", "CID001");
```

##### Or CreditCard
``` java
paymentOption = new CreditCardOption("Salil", "411111111111111", "123", Month.getMonth("12"), Year.getYear("2020"));
```

##### Or DebitCard
``` java
paymentOption = new DebitCardOption("Salil", "411111111111111", "123", Month.getMonth("12"), Year.getYear("2020"));
```

```java
PaymentType.SplitPayment paymentType = new PaymentType.SplitPayment(amount, Constants.BILL_URL, paymentOption,useCitrusCash, useMVC);
citrusClient.smartPay( paymentType , callback);
```
