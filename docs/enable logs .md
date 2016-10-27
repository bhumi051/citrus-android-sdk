<b> How to enable Logs? </b>

```groovy
      citrusClient.setLogLevel(CitrusLogger.LogLevel.DEBUG); 
```      

   1. Logs can be used while debugging any issue.
   2. Loglevel is set to OFF by default. Only Warning and Errors will be displayed by default.
   3. Make sure you are turning off the logs when you are using Production Environment. 
   
<b> Note </b>
  * Below method is deprecated and will be removed in next release.
  
   ~~citrusClient.enableLog(true);~~
   


