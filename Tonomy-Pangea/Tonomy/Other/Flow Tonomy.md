Needs more testing - Needs more Flow marketing

- Forgot to put in the general foundation strategy



Flow for revoke

SSO flow normal

SSO Flow with their own Identity app - Takeover


SSO flow adapted to use cases 
- Revoking authority
- Getting access to multipule apps at the same time

Design Flow:
- Overview Dashboard - See what is happening in the idenity
- Overview Dashboard - Login into multipule apps
- 


Normal flow SSO - Normal SSO using the application as is. Revoke from the User side.

New application SSO - Use the ID to be able to login to multipule apps.
(With a while-labeld application)



Here is a possible flow for an SSO login app that keeps the user's information at all times:

1.  User opens the app and is presented with a login screen.
    
2.  User enters their credentials (email and password) and clicks the "Log In" button. Or biometic information. 
3. Upon entering, the user is presented with information on what request is being made, what will be stored and what information is required. On the Top there is a message with "new Connection". On the top there is a slider, with which the user could terminate this connection later on. 
4. The User clicks, Proceed with this Login.
    
3.  The app sends the credentials to the SSO server for verification. 
  
4.  If the credentials are valid, the SSO server sends a token to the app. Otherwise, it sends an error message.
5. The screen on the userside is update with new information on who's authority the access is given and what kind of premissions this entails.
    
5.  The app stores the token on the user's device, encrypted with a key that only the user knows.
    
6.  The app uses the token to authenticate the user and access protected resources on the device.
    
7.  The user can access their personal information and update it as needed.
    
8.  The user can also log out of the app by revoking the token.
    
9.  If the user closes the app, the token will remain on the device, allowing for faster login the next time the user opens the app.
    
10.  The user will also be able to use the same token to authenticate on other apps that use the same SSO service.
    

1.  User opens the app and is presented with a login screen.
2.  User enters their credentials (email and password) and clicks the "Log In" button.
3.  The app sends a request to the SSO server with the credentials for verification.
4.  If the credentials are valid, the SSO server sends a token to the app, otherwise, it sends an error message.
5.  The app stores the token on the user's device, encrypted with a key that only the user knows.
6.  The app uses the token to authenticate the user and access protected resources on the device.
7.  The user can access their personal information and update it as needed.
8.  The user can also log out of the app by revoking the token.
9.  If the user closes the app, the token will remain on the device, allowing for faster login the next time the user opens the app.
10.  The user will also be able to use the same token to authenticate on other apps that use the same SSO service.


Note:

-   The encryption key should be created during the first login and should be stored securely.
-   The device should be secured with a passcode or biometric authentication to prevent unauthorized access to the token.
-   The token should be revoked if it is compromised or when the user wants to log out.
-   The app should have a mechanism to detect if the token is expired or revoked, and ask the user to login again if that happens.