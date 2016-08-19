
SDK provides facility to make payment using Payment JSON. You can juse this feature if you want to generate few parameters required 
for payment inside app instead of server. You can also use this feature if your bill generator url accepts post method parameters.
If your bill generator url supports post method, you can request the api response from the app and pass the json to SDK.
Expected JSON is as below
```
{"merchantTxnId":"147089657626491","amount":{"value":"10.00","currency":"INR"},
"requestSignature":"e5d22d7c55d398ff0f103bb8d6d413aaabaf2ff7","merchantAccessKey":"F2VZD1HBS2VVXJPMWO77",
"returnUrl":"https:\/\/salty-plateau-1529.herokuapp.com\/redirectURL.sandbox.php",
"notifyUrl":"https:\/\/salty-plateau-1529.herokuapp.com\/notifyUrl.sandbox.php",
"customParameters":{"param1":"1000","param2":"CitrusTestSDK"},
"alteredAmout":{"value":null,"currency":"INR"},
"dpSignature":"554beb58c77f208e03704ef961a8b36b34dbefc8"}//dpSignature and alteredAmout is optional. 
//Required only for Dynamic pricing feature
//merchantTxnId - should be different for every transaction
//merchantTxnId - should be max 24 characters
```
Payment Using JSON Bill
```
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
