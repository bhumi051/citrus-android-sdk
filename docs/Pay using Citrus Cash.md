<h2>Pay using Citrus Cash</h2>

<li>You can perform a transaction using Citrus cash.</li>  

```java
 try {
          mCitrusClient.prepaidPay(new PaymentType.CitrusCash(new Amount("5"),"BILL_URL"),new Callback<PaymentResponse>() {
              @Override
              public void success(PaymentResponse paymentResponse) {
                  
              }

              @Override
              public void error(CitrusError citrusError) {

              }
          });
        } catch (CitrusException e) {
            e.printStackTrace();
        }
  ```
