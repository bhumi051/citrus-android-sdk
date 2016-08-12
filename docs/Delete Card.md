<b>SDK allows you to delete the saved card against your account</b>
Below is the sample piece of code
```
    citrusClient.deletePaymentOption(paymentOption, new Callback<CitrusResponse>() { 
        @Override
        public void success(CitrusResponse citrusResponse) {
            
        }
  
        @Override
        public void error(CitrusError citrusError) {
  
        }
    });
    //paymentOption is receieved in getWallet which is nothing but saved payment.
```

