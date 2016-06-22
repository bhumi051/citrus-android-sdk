<h3>What is Auto Load?</h3>
<h4>You can choose Auto Load to save time and hassle.Basically we will credit your account with chosen amount(currently with 500rs) when the balance in your wallet falls below 500rs. </h4>
* Auto Load feature is available only for Credit Card Load Money Transaction.
* Auto load feature is available only for Master and VISA Card.
* You can create only one auto load subscription.
* Minimum threshold amount is 500rs.
* Minimum auto load amount is 500rs.
* You can deactivate as well as update auto load subscription.
* Actual credit card number is required for auto load subscription.

##Check if Active Auto Load Subscription Exists 
 Before creating any auto load subscription, check if active subscription exists. If active subscription does not exist, you can create auto load subscription.Use this method before creating subscription, deactivating subscription, updating existing subscription.

```java
   citrusClient.isActiveSubscriptionPresent(new Callback<Boolean>() {
            @Override
            public void success(Boolean isSubscriptionAvailable) {
                if (isSubscriptionAvailable)
                //active subscription exists 
                else
                //active subscription does not exists 
            }

            @Override
            public void error(CitrusError error) {
                Toast.makeText(getActivity(), error.getMessage(), Toast.LENGTH_SHORT).show();
            }
   });
  ```
##How to create auto load subscription?
###1. Initiate as auto load transaction 
 You can create a auto load transaction by below method. **Please make sure  the cardoption is Master or Visa Credit-Card only.**


```java
   Callback<SubscriptionResponse> callback = new Callback<SubscriptionResponse>() {
		    @Override
		    public void success(SubscriptionResponse subscriptionResponse) {

		    }

		    @Override
		    public void error(CitrusError error) {
		       
		    }
		};
	CreditCardOption cardOption = new CreditCardOption("", cardNumber, cardCVV, cardExpiryMonth(), cardExpiryYear()); //use this for new card
	//or
	CreditCardOption cardOption = new CreditCardOption(token, cvv);//use this for saved card
	PaymentType paymentType = new PaymentType.LoadMoney(amout, Constants.RETURN_URL_LOAD_MONEY, cardOption);
	try { 
	  citrusClient.autoLoadMoney((PaymentType.LoadMoney) paymentType, thresholdAmount, autoLoadAmount, callback);//call this method to initiate auto load subscription
	} catch (CitrusException e) {
	    e.printStackTrace();
	}
```
###2. Lazy Auto Load
You can create auto load subscription after load money transaction. First check if existing load money transaction is eligible for auto-load or not. If yes then you can create auto-load subscription using card details used in earlier load money transaction.
         
```java
    //call below method after load money successful transaction
    citrusClient.isAutoLoadAvailable(new Callback<Boolean>() { //first check if auto load is available
        @Override
        public void success(Boolean isAvailable) {
            if (isAvailable) {
               citrusClient.autoLoadMoney(new Amount(thresholdAmount, autoLoadAmount,callback);//call this method for lazy auto load
            }
        }

        @Override
        public void error(CitrusError error) {

        }
    });
```
### Deactivate Auto Load Subscription -
use below method to deactivate existing auto load subscription.
```java
    citrusClient.deActivateSubscription(new Callback<SubscriptionResponse>() {
            @Override
            public void success(SubscriptionResponse subscriptionResponse) {
              
            }

            @Override
            public void error(CitrusError error) {
          
            }
    });
```
### Get Active Subscription
```java
    citrusClient.getActiveSubscriptions(new Callback<SubscriptionResponse>() {
            @Override
            public void success(SubscriptionResponse subscriptionResponses) {
             //subscriptionResponses - will be null if no active subscription exists.
            }

            @Override
            public void error(CitrusError error) {
               
            }
    });
```
###  Update Subscription to lower value
You can update threshold and auto-load amount to lower value than current threshold and auto-load amount.
```java
    citrusClient.updateSubScriptiontoLoweValue(thresholdAmount, loadAmount, new Callback<SubscriptionResponse>() {
        @Override
        public void success(SubscriptionResponse subscriptionResponse) {
            //updated subscriptionResponse
        }

        @Override
        public void error(CitrusError error) {
            //error
        }
    });
```
###  Update Subscription to Higher Value
Update subscription to higher value requires auto load transaction.
```java
   Callback<SubscriptionResponse> callback = new Callback<SubscriptionResponse>() {
		    @Override
		    public void success(SubscriptionResponse subscriptionResponse) {

		    }

		    @Override
		    public void error(CitrusError error) {
		       
		    }
		};
	CreditCardOption cardOption = new CreditCardOption("", cardNumber, cardCVV, cardExpiryMonth(), cardExpiryYear()); //use this for new card
	//or
	CreditCardOption cardOption = new CreditCardOption(token, cvv);//use this for saved card
	PaymentType paymentType = new PaymentType.LoadMoney(amout, Constants.RETURN_URL_LOAD_MONEY, cardOption);
	try { 
	  citrusClient.updateSubscriptiontoHigherValue((PaymentType.LoadMoney) paymentType, thresholdAmount, autoLoadAmount, callback);//call this method to update auto load subscription.
	} catch (CitrusException e) {
	    e.printStackTrace();
	}
```
    
