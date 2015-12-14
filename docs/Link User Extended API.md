
This new Link User Extended API is written to ease up the process of on-boarding for users. 

To perform this, a two step approach is followed as explained below,

####Step 1. (Linking the user)
 - Grab the user entered credentials (email id, mobile number) and call the Link User Extended API with the necessary parameters, as below,
 
 ```java
      citrusClient.linkUserExtended(emailId, mobileNo, new Callback<LinkUserExtendedResponse>(){
       @Override
            public void success(LinkUserExtendedResponse linkUserExtendedResponse) {
            }
       @Override
            public void error(CitrusError error) {
        });
 ``` 
 - The above API call, will perform all the required calculations and give you 'success/error' callback based on its result. Success callback will give a <b>'linkUserExtendedResponse'</b> object which you should maintain for future reference.
 
####Step 2. (Signing the user based on response of Step 1)
 - Step 1 will also give you the type of Sign In, which should be performed for the current user. This type falls under 5 categories, which you can get by calling the below method,
 
 ```java
 LinkUserSignInType linkUserSignInType = linkUserExtendedResponse.getLinkUserSignInType();
 ```
  - The above method will give you a enum and the 5 categories are,
  ```java
                1. SignInTypeMOtpOrPassword (Sign-in using mobile OTP or Password)
                2. SignInTypeMOtp (Sign-in using mobile OTP)
                3. SignInTypeEOtpOrPassword (Sign-in using email OTP or Password)
                4. SignInTypeEOtp (Sign-in using email OTP)
                5. None (Error case)
   ```

- Using the above sign in type you can manage your UI to display either OTP/Password editfields or both. Also for above cases, you can display a particular message to user, call the below method to get the message,

 ```java
 String linkUserMessage = linkUserExtendedResponse.getLinkUserMessage();
 ``` 
- Next, once user enters the OTP/Password, you need to set one enum value as below,
```java
      LinkUserPasswordType linkUserPasswordType = LinkUserPasswordType.None;
      if("OTP entered by user"){
           linkUserPasswordType = LinkUserPasswordType.Otp;
      }else if("Password entered by user"){
           linkUserPasswordType = LinkUserPasswordType.Password;
      }
```
 - Finally call the below method to Signin user,
 ```java
 citrusClient.linkUserExtendedSignIn(emailId,linkUserPassword,linkUserExtended,linkUserPasswordType, new Callback<CitrusResponse>() {
            @Override
            public void success(CitrusResponse citrusResponse) {
            }
            @Override
            public void error(CitrusError error) {
                
            }
        });
