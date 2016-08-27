
SDK provides facility to make payment using Payment JSON. You can juse this feature if you want to generate few parameters required 
for payment inside app instead of server. You can also use this feature if your bill generator url accepts post method parameters.
If your bill generator url supports post method, you can request the api response from the app and pass the json to SDK.
Expected JSON is as below
```json
{"merchantTxnId":"147089657626491",
"amount":{"value":"10.00","currency":"INR"},
"requestSignature":"e5d22d7c55d398ff0f103bb8d6d413aaabaf2ff7",
"merchantAccessKey":"F2VZD1HBS2VVXJPMWO77",
"returnUrl":"https:\/\/salty-plateau-1529.herokuapp.com\/redirectURL.sandbox.php",
"notifyUrl":"https:\/\/salty-plateau-1529.herokuapp.com\/notifyUrl.sandbox.php",
"customParameters":{"param1":"1000","param2":"CitrusTestSDK"},
"alteredAmout":{"value":null,"currency":"INR"},
"dpSignature":"554beb58c77f208e03704ef961a8b36b34dbefc8"}//dpSignature and alteredAmout is optional. 
//Required only for Dynamic pricing feature
//merchantTxnId - should be different for every transaction
//merchantTxnId - should be max 24 characters
```
Citrus Cash Payment Using JSON Bill
```java
   try {
                PaymentType.CitrusCash citrusCash = new PaymentType.CitrusCash(amount, Constants.BILL_URL);
                //PaymentType can be of any type(Credit , Debit, BetBanking).
                String paymentJSON = "{\"merchantTxnId\":\"147089657626491\",\"amount\":{\"value\":\"10.00\",\"currency\":\"INR\"},\"requestSignature\":\"e5d22d7c55d398ff0f103bb8d6d413aaabaf2ff7\"," +
                        "\"merchantAccessKey\":\"F2VZD1HBS2VVXJPMWO77\",\"returnUrl\":\"https:\\/\\/salty-plateau-1529.herokuapp.com\\/redirectURL.sandbox.php\"," +
                        "\"notifyUrl\":\"https:\\/\\/salty-plateau-1529.herokuapp.com\\/notifyUrl.sandbox.php\"," +
                        "\"customParameters\":{\"param1\":\"1000\",\"param2\":\"CitrusTestSDK\"},\"alteredAmout\":{\"value\":null,\"currency\":\"INR\"},\"dpSignature\":\"554beb58c77f208e03704ef961a8b36b34dbefc8\"}";
                PaymentType.CitrusCash citrusCash1 = new PaymentType.CitrusCash(PaymentBill.fromJSON(paymentJSON));
                citrusClient.simpliPay(citrusCash, new Callback<TransactionResponse>() {
                    @Override
                    public void success(TransactionResponse transactionResponse) {
                        if (getApplicationContext() != null) {
                            showSnackBar(transactionResponse.getMessage());
                        }
                    }

                    @Override
                    public void error(CitrusError error) {
                        if (getApplicationContext() != null) {
                            showSnackBar(error.getMessage());
                        }
                    }
                });
    } catch (CitrusException e) {
          e.printStackTrace();
          showSnackBar(e.getMessage());
    }
```


<h4>Pay using Debit Card using JSON Bill</h4>

```java
  CitrusClient citrusClient = CitrusClient.getInstance(context); // Activity Context
  // No need to call init on CitrusClient if already done.

  DebitCardOption debitCardOption = new DebitCardOption("Card Holder Name", "4111111111111111", "123", Month.getMonth("12"), Year.getYear("18"));

      String paymentJSON = "{\"merchantTxnId\":\"147089657626491\",\"amount\":{\"value\":\"10.00\",\"currency\":\"INR\"},\"requestSignature\":\"e5d22d7c55d398ff0f103bb8d6d413aaabaf2ff7\"," +
                        "\"merchantAccessKey\":\"F2VZD1HBS2VVXJPMWO77\",\"returnUrl\":\"https:\\/\\/salty-plateau-1529.herokuapp.com\\/redirectURL.sandbox.php\"," +
                        "\"notifyUrl\":\"https:\\/\\/salty-plateau-1529.herokuapp.com\\/notifyUrl.sandbox.php\"," +
                        "\"customParameters\":{\"param1\":\"1000\",\"param2\":\"CitrusTestSDK\"},\"alteredAmout\":{\"value\":null,\"currency\":\"INR\"},\"dpSignature\":\"554beb58c77f208e03704ef961a8b36b34dbefc8\"}";
  // Init PaymentType     
  PaymentType.PGPayment pgPayment = new PaymentType.PGPayment(PaymentBill.fromJSON(paymentJSON), debitCardOption, new CitrusUser("developercitrus@gmail.com","9876543210"));

  citrusClient.simpliPay(pgPayment, new Callback<TransactionResponse>() {

     @Override
     public void success(TransactionResponse transactionResponse) { }

     @Override
     public void error(CitrusError error) { }
  });
  ```
<h4>Pay using Credit Card using JSON Bill</h4>

```java
  CitrusClient citrusClient = CitrusClient.getInstance(context); // Activity Context
  // No need to call init on CitrusClient if already done.

  CreditCardOption creditCardOption = new CreditCardOption("Card Holder Name", "4111111111111111", "123", Month.getMonth("12"), Year.getYear("18"));

        String paymentJSON = "{\"merchantTxnId\":\"147089657626491\",\"amount\":{\"value\":\"10.00\",\"currency\":\"INR\"},\"requestSignature\":\"e5d22d7c55d398ff0f103bb8d6d413aaabaf2ff7\"," +
                        "\"merchantAccessKey\":\"F2VZD1HBS2VVXJPMWO77\",\"returnUrl\":\"https:\\/\\/salty-plateau-1529.herokuapp.com\\/redirectURL.sandbox.php\"," +
                        "\"notifyUrl\":\"https:\\/\\/salty-plateau-1529.herokuapp.com\\/notifyUrl.sandbox.php\"," +
                        "\"customParameters\":{\"param1\":\"1000\",\"param2\":\"CitrusTestSDK\"},\"alteredAmout\":{\"value\":null,\"currency\":\"INR\"},\"dpSignature\":\"554beb58c77f208e03704ef961a8b36b34dbefc8\"}";
  // Init PaymentType     
  PaymentType.PGPayment pgPayment = new PaymentType.PGPayment(PaymentBill.fromJSON(paymentJSON), creditCardOption, new CitrusUser("developercitrus@gmail.com","9876543210"));

  citrusClient.simpliPay(pgPayment, new Callback<TransactionResponse>() {

     @Override
     public void success(TransactionResponse transactionResponse) { }

     @Override
     public void error(CitrusError error) { }
  });
  ```
  
  <h4>Pay using Net Banking Option using JSON Bill</h4>
  
  ```java
  CitrusClient citrusClient = CitrusClient.getInstance(context); // Activity Context
  // No need to call init on CitrusClient if already done.

  NetbankingOption netbankingOption = new NetbankingOption("ICICI Bank","CID001");
         String paymentJSON = "{\"merchantTxnId\":\"147089657626491\",\"amount\":{\"value\":\"10.00\",\"currency\":\"INR\"},\"requestSignature\":\"e5d22d7c55d398ff0f103bb8d6d413aaabaf2ff7\"," +
                        "\"merchantAccessKey\":\"F2VZD1HBS2VVXJPMWO77\",\"returnUrl\":\"https:\\/\\/salty-plateau-1529.herokuapp.com\\/redirectURL.sandbox.php\"," +
                        "\"notifyUrl\":\"https:\\/\\/salty-plateau-1529.herokuapp.com\\/notifyUrl.sandbox.php\"," +
                        "\"customParameters\":{\"param1\":\"1000\",\"param2\":\"CitrusTestSDK\"},\"alteredAmout\":{\"value\":null,\"currency\":\"INR\"},\"dpSignature\":\"554beb58c77f208e03704ef961a8b36b34dbefc8\"}";
  // Init Net Banking PaymentType     
  PaymentType.PGPayment pgPayment = new PaymentType.PGPayment(PaymentBill.fromJSON(paymentJSON), netbankingOption, new CitrusUser("developercitrus@gmail.com","9876543210"));

  citrusClient.simpliPay(pgPayment, new Callback<TransactionResponse>() {

     @Override
     public void success(TransactionResponse transactionResponse) { }

     @Override
     public void error(CitrusError error) { }
  });
  ```

