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

```groovy
	compile 'com.citruspay.sdk:payment-sdk:4.0.0'
```

<b>Note</b>

* Remove these library's only if you have added those for earlier version of Citrus SDK.
* In case if any of above library is used in your app as well, keep that library in build.gradle.
* Following are the librarys and versions internally used in 4.0.0 version(no need to add in your build.gradle. Taken care by   Citrus SDK compile dependency).

<table border="1" width="100%">
   <col width="20">
   <col width="20">
    <col width="60">

  <tr align="center">
    <th>Library Name</th>
    <th>Library Version</th>
    <th>Compile Dependency</th>
  </tr>
  <tr align="center">
    <th>appcompat-v7</th>
    <th>23.1.0</th>
    <th>compile 'com.android.support:appcompat-v7:23.1.0'</th>
  </tr>
  <tr align="center">
    <th>logger</th>
    <th>1.8</th>
    <th>compile 'com.orhanobut:logger:1.8'</th>
  </tr>
  <tr align="center">
    <th>conceal</th>
    <th>1.0.1</th>
    <th>compile 'com.facebook.conceal:conceal:1.0.1@aar'</th>
  </tr>
  <tr align="center">
    <th>volley</th>
    <th>1.0.0</th>
    <th>compile 'com.android.volley:volley:1.0.0'</th>
  </tr>
   <tr align="center">
    <th>gson</th>
    <th>2.6.2</th>
    <th>compile 'com.google.code.gson:gson:2.6.2'</th>
  </tr>
</table> 


  
