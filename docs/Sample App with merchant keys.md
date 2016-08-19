* You can check sample App provided with your keys and URL 

 Following changes are required
 
  
  1.Load Money Redirect URL Changes
  
    strings.xml file
    
    change prefs_load_money_return_url_default_value attribut. Replace this url with your Load Money Redirect URL.
    
  2.SDK Init Keys 
  
    Utils.java file 
    
    change MerchantConfigParameters.SANDBOX - change values with your keys and BillGenerator URL for sandbox environment.
    
    change MerchantConfigParameters.PRODUCTION - change values with your keys and BillGenerator URL for production environment.
    
    
  
     
