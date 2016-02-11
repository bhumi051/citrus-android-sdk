
This new Link User Extended API is written to ease up the process of on-boarding for users. 

To perform this, a two step approach is followed as explained below,

####Step 1. (Linking the user)
 - Grab the user entered credentials (email id, mobile number) and call the Link User Extended API with these credentials, as below,
 
 ```java
 citrusClient.linkUserExtended(emailId, mobileNo, new Callback<LinkUserExtendedResponse>(){
       @Override
            public void success(LinkUserExtendedResponse linkUserExtendedResponse) {
                // User Linked!
            }
       @Override
            public void error(CitrusError error) {
                // Error case
                String errorMessasge = error.getMessage();
            }
 });
 ``` 
 - The above API call, will perform all the required calculations on these credentials and give you 'success/error' callback based on its result. Success callback will give a <b>'linkUserExtendedResponse'</b> object which you should maintain for future reference.
 
 

####Step 2. (Signing the user based on response of Step 1)
 - Step 1 will also give you the type of Sign In, that should be performed for the current user. This type falls under 5 categories, and you can get it by calling the below method,
 
 ```java
 LinkUserSignInType linkUserSignInType = linkUserExtendedResponse.getLinkUserSignInType();
 ```
  - The above method will give you a enum and its 5 categories are,
  ```java
                1. SignInTypeMOtpOrPassword (Sign-in using mobile OTP or Password)
                2. SignInTypeMOtp (Sign-in using mobile OTP)
                3. SignInTypeEOtpOrPassword (Sign-in using email OTP or Password)
                4. SignInTypeEOtp (Sign-in using email OTP)
                5. None (Error case)
   ```

- Using the above sign in type you can manage your UI to display either OTP/Password editfields or both. Also for above cases, you can display a particular message to user. Call the below method to get the message,

 ```java
 String linkUserMessage = linkUserExtendedResponse.getLinkUserMessage();
 ``` 
- Next, once user enters the OTP/Password, you need to set a enum value which is the PasswordType, as below,
```java
      LinkUserPasswordType linkUserPasswordType = LinkUserPasswordType.None;
      if("OTP entered by user"){
           // Set PasswordType as OTP
           linkUserPasswordType = LinkUserPasswordType.Otp;
      }else if("Password entered by user"){
           // Set PasswordType as Password
           linkUserPasswordType = LinkUserPasswordType.Password;
      }
```
 - Finally call the below method to Sign in user, which takes 3 main parameters and a callback,
 ```java
            1. linkUserExtended (Previous LinkUserExtended Response Object)
            2. linkUserPasswordType (LinkUser PasswordType calculated above)
            3. linkUserPassword (OTP/Password entered by user)
  
 citrusClient.linkUserExtendedSignIn(linkUserExtended,linkUserPasswordType,linkUserPassword, new Callback<CitrusResponse>(){
      @Override
            public void success(CitrusResponse citrusResponse) {
                // User Signed In!
            }
      @Override
            public void error(CitrusError error) {
                // Error case
                String errorMessasge = error.getMessage();
            }
});
```

#### Notes:
 - In case, if after performing Step 1, the OTP is not received, you can have a resend functionality for users. This basically should just perform Step 1 again with the already entered user credentials.
 - Email ID is not mandatory in Step 1.
 - If user enters both email and mobile number in Step 1, make sure that he/she is unable to edit those values during Step 2 after Step 1 is completed.
