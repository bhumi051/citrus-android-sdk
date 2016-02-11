One Tap Payment will enable the payment without entering CVV for Card Payments. 
If enabled we will save a the CVV of the card if the transaction is successful and the user does not need to enter CVV while making payment next time.

####Step 1. Enable the One Tap Payment
 ```java
CitrusConfig.getInstance().enableOneTapPayment(true);
 ``` 
    
    
###### Note: One Tap Payment may not work on few devices due to unsupported device architecture.
    You can check if One Tap Payment is supported by device using below method
```java
CitrusClient.getInstance(mContext).isOneTapPaymentSupported(); // returns true if supported else false
``` 
  //
####Step 2. Check whether the One Tap Payment Enabled for the card.
Below method will return true if One Tap Payment is enabled for saved credit/debit card else return false
 ```java
 if (citrusClient.isOneTapPaymentEnabledForCard((CardOption) paymentOption)) {
     //do not prompt CVV from end user and continue payment
  } else {
    //prompt CVV from end user and continue payment
  }
  ``` 
                
    
    
