
<b>Additonal Parameters in Bill URL</b>
* SDK allows you to send any additonal parameters apart from amount in BillURL.
  e.g if you want to generate transaction ID in app and send it to BillURL.
* You have to append the parameter in your BillURL (which you will be passing to SDK) 
 e.g  https://salty-plateau-1529.herokuapp.com/billGenerator.sandbox.php?merchantTxnId=1234
 
 //You need to update your BilURL logic to handle this parameter and construct the json.
 Below is the JSON generated based on parameter sent in BillURL.
 ```
 {"merchantTxnId":"1234","amount":{"value":"10.00","currency":"INR"},
 "requestSignature":"ddfcf1fe7049ec238f3c53bb4db76d2fb5ffb71e","merchantAccessKey":"F2VZD1HBS2VVXJPMWO77",
 "returnUrl":"https:\/\/salty-plateau-1529.herokuapp.com\/redirectURL.sandbox.php",
 "notifyUrl":"https:\/\/salty-plateau-1529.herokuapp.com\/notifyUrl.sandbox.php",
 "customParameters":{"param1":"1000","param2":"CitrusTestSDK"},"alteredAmout":{"value":null,"currency":"INR"},
 "dpSignature":"554beb58c77f208e03704ef961a8b36b34dbefc8"}
 ```
 * You can append more than 1 parameters in BillURL. You have to append your BillURL logic accordingly.
 
   e.g
   http://yoururl/test/demo_form.asp?name1=value1&name2=value2
 
