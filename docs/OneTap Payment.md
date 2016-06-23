One Tap Payment feature makes your user save the trouble of enterring the CVV of his/her card.

####Step 1. Enable the One Tap Payment
 ```java
CitrusConfig.getInstance().enableOneTapPayment(true);
 ``` 
    
    
###### Note: One Tap Payment may not work on few devices due to unsupported device architecture.
    You can check if One Tap Payment is supported by device using below method
```java
CitrusClient.getInstance(mContext).isOneTapPaymentSupported(); // returns true if supported else false
``` 
  
####Step 2. Check whether the One Tap Payment Enabled for the card.
Below method will return true if One Tap Payment is enabled for saved Credit/Debit card else return false
 ```java
 if (CitrusClient.getInstance(mContext).isOneTapPaymentEnabledForCard((CardOption) paymentOption)) {
     //do not prompt CVV from end user and continue payment
  } else {
    //prompt CVV from end user and continue payment
  }
  ``` 
####Step 3. Load Money using One Tap Payment

 ```java
 if (CitrusClient.getInstance(mContext).isOneTapPaymentEnabledForCard((CardOption) paymentOption)) {
     //do not prompt CVV from end user and Continue Load Money Payment with below method
     CitrusClient.getInstance(mContext).simpliPay((PaymentType.LoadMoney) paymentType, callback);
  } else {
    //prompt CVV from end user, udate Payment Option and continue payment
    CitrusClient.getInstance(mContext).simpliPay((PaymentType.LoadMoney) paymentType, callback);
  }
 ``` 
####Step 4. PG Payment using One Tap Payment

 ```java
 if (CitrusClient.getInstance(mContext).isOneTapPaymentEnabledForCard((CardOption) paymentOption)) {
     //do not prompt CVV from end user and continue PG Payment with below method
     CitrusClient.getInstance(mContext).simpliPay((PaymentType.PGPayment) paymentType, callback);
  } else {
    //prompt CVV from end user, udate Payment Option and continue PG Payment
     CitrusClient.getInstance(mContext).simpliPay((PaymentType.PGPayment) paymentType, callback);
  }
 ``` 
####Step 5. Make Payment using One Tap Payment

 ```java
 if (CitrusClient.getInstance(mContext).isOneTapPaymentEnabledForCard((CardOption) paymentOption)) {
     //do not prompt CVV from end user and continue Make Payment
     CitrusClient.getInstance(mContext).simpliPay((PaymentType.PGPayment) paymentType, callback);
   } else {
    //prompt CVV from end user, udate Payment Option and continue Make Payment
    CitrusClient.getInstance(mContext).simpliPay((PaymentType.PGPayment) paymentType, callback);
  }
 ``` 
  
                
    
    
