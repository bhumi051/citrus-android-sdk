<b>Updating to SDK version 4.0.0 from previous version</b>
* SDK Version 4.0.0 is major release where Network layer of SDK has been changed from Retrofit to Volley.
* If you are upgrading SDK to 4.0.0 following dependencies should be removed from your build.gradle

  <b>for Retrofit 1.9</b>
  
        compile 'com.squareup.retrofit:retrofit:1.9.0' 
        compile 'com.squareup.okhttp:okhttp:2.3.0' 
        compile 'com.squareup.okhttp:okhttp-urlconnection:2.3.0'
        compile 'com.squareup.okio:okio:1.3.0' 
        compile 'com.orhanobut:logger:1.8' 
        compile 'com.facebook.conceal:conceal:1.0.1@aar'
  
   <b>for Retrofit 2.0</b>
   
        compile('com.squareup.retrofit:retrofit:2.0.0-beta2') { 
            exclude module: 'okhttp'
        }
   
        compile 'com.squareup.okhttp:okhttp:2.5.0' 
        compile 'com.squareup.retrofit:converter-gson:2.0.0-beta2' 
        compile 'com.squareup.okhttp:logging-interceptor:2.6.0' //to enable logging 
        compile 'com.squareup.okhttp:okhttp-urlconnection:2.3.0' 
        compile 'com.squareup.okio:okio:1.3.0' 
        compile 'com.orhanobut:logger:1.8'
        compile 'com.facebook.conceal:conceal:1.0.1@aar'
        
* We have also changed domain name from *citrus* to **citruspay**. Please make sure you are copying following dependency 
  and is used in your build.gradle instead of just changing version.
  
	      compile 'com.citruspay.sdk:payment-sdk:4.0.0'
  
