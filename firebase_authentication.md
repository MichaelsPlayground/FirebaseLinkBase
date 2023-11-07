# Firebase Authentication

This is usually the first step to setup a Firebase based application as we talk about sensitive data 
that is stored by your app users within the Firebase database and storage.

## Authentication with Email and Password

After you deployed your app (here on an emulator) you press the "EmailPasswordFragment" entry:

Type in any Email address (does not need to exist, but an existing one of you gives an additional option) 
and enter a password (I'm using always "123456" for my test accounts as there is no way to recover the 
password, just an reset by Email is possible). Then press "Create account":

At this time the user was created using it's (internal) Firebase UID. As you can see in the screenshot the 
user's Email address is not verified yet ("verified: false"):

If you are using an existing Email press the "Verify" button to receive an Email verification Email:

Open your Email account, find a mail from "noreply@quickstart..." and click on the link within the mail. 
You get a note in your browser that "Your email has been verified" and when "reloading" your Quickstart app
(press the "Reload" button) you see this information in your app as well (verified: true). This is an 
**optional feature**, again - depending on your app needs. If you don't use this option the user is active 
without the Email verification, otherwise you will prohibit the  usage of your app until the Email address 
is verified.

Now we are moving back to the Firebase console - press the "Authentication" product on the left side and get 
a list of users that signed up so far:

There are some other tabs available like "Templates", "Usage" and "Settings" - I'm not going deeper to these 
settings but you should keep in mind that this setup is running on a "no cost base" some some settings are 
limited, e.g. the number of sign-ups is fixed to a maximum of 100 - for higher numbers you may need to upgrade  
your payment plan.

## Anonymous Authentication 

Please press the AnonymousAuthFragment" entry for this authentication option.

If you are still signed in from the previous step press the "Sign out" button and then "Sign in" - there is a 
new User ID and the "Email: null" shows that no Email was used.

The Firebase console shows an anonymous user and the numbr will raise until an anonymous user decides to 
"sign out", so this may litter your account...

## Authentication with a Google account

Please press the "GoogleSignInFragment" and find a "spartan" desktop - there is just a Google Sign in button available. 
After pressing this button the device will present you the "system" Google account or you can choose another account.

Depending on your tests you may get notices from Google to accept the usage of this account but after this you are 
signed in with you Google account number and the Firebase UID that is unique to this Email address.

Visit the Firebase console /  Authentication to see the new user.

## Authentication with FirebaseUI

All Firebase UI modules are build on top of the regular SDK modules, so FirebaseUIAuth is a module that help to 
manage the  user authentication with a minimum of code, but unfortunately this type of authentication failed during 
my tests of the Quickstart sample, sorry.
