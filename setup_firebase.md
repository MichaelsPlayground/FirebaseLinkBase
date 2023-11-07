# Setup Firebase

To run Firebase project it is necessary to setup your project in the Firebase console. Follow the link
https://console.firebase.google.com/ and **login with your Google account**.

This are the steps I used to setup the project for the **Firebase Quickstart Android** project using the "**Authentication**" module. 
For other modules there are additional steps necessary.

**Recommendation**: In the first time you will setup a lot of projects but the number of projects is limited
(about 10 projects are allowed) and I strongly recommend to **use a second, "test" account** for the setups and 
not your regular Google account. This is because you cannot delete projects no longer in use and reuse the 
project space again - you have to wait some weeks before the console accepts new projects.

**Error note**: If you are using the given (default) "applicationId" = "com.google.firebase.quickstart.auth" you 
will run into the problem that the Google authentication will fail, see step 3 action 9. If you want to avoid this 
you should better rename the applicationId (find it in the modules/apps build.gradle file for the "auth" module) to 
a unique one. I have chosen "de.androidcrypto.firebase.quickstart.auth". Please keep in mind that you need to change 
the applicationId on all further modules as well !

## step 1: get your project data

Your Firebase project is bundled with your Java (Kotlin) project in Android Studio AND with the local keystore 
that is in use on your developing machine. 

1) get the package name of your project: simply open the MainActivity.java file, scroll to the top and copy 
the package name: **com.google.firebase.quickstart.auth.java**
2) get the SHA1-value of your keystore - as there are several ways to get it I'm recommending the 
"signingReport" way - follow the steps in my get_sha1.md document or https://developers.google.com/android/guides/client-auth

## step 2: Add Firebase using the Firebase console

I'm describing option 1 to add Firebase to the project using the Firebase console (for more information 
see https://firebase.google.com/docs/android/setup?hl=en).

As the Firebase Quickstart Android app offers tests for all Firebase modules we will need to setup all data if you want to run 
all modules. For a quick start I'm showing the setup for the "**Authentication**" module only:

1) click on "add project"
2) enter a project name - make sure the data is correct because for some data it is difficult to change later. The name should 
reflect your Android Studio project name, because with a rising number of projects you won't know what projects match... For 
my project I'm using "QuickstartAndroid" and press "Continue"
3) For this project I'm **disabling Google Analytics** - if we need it later it's no problem to add it. Press "Create project"
4) The project get created... wait about a minute and press "Continue"
5) "Now it's time to add an app to get started" - press the Android symbol
**Special note on using the FirebaseQuickstartAndroid application**: usually you have an app with one package name but this sample 
project allows for testing several Firebase modules like Authentication, Realtime Database and so on. For this reason you have to 
check the individual **applicationId** you find in the specific "build.gradle.build.kts" file for the "module :auth:app". For that reason 
I'm using the value "**com.google.firebase.quickstart.auth**" as data ! 
6) Register your app by providing the package name (see step 1), in my example it's **com.google.firebase.quickstart.auth** (see above note)
7) Entering an apps "nickname" is optional, I'm using "Quickstart Android" 
8) Please enter the "Debug signing certificate SHA-1" because we will need this for minimum obe module later (see step 1 part 2 above), again: 
please your OWN SHA1 value
9) press "Register app" and wait some seconds
10) your setup is complete, click on "Download google-services.json" and save this file locally on your device.
11) Press "Next" button to get the data for the actual dependencies you need to app to your Gradle and setting files
12) In the  "plugins" section of your **root build.gradle** file (project-level) add this dependency and press "Sync now":
```plaintext
// Add the dependency for the Google services Gradle plugin
id 'com.google.gms.google-services' version '4.4.0' apply false
```
13) In the  **module build.gradle** file (app-level) add these modules and dependencies and press "Sync now":
```plaintext
plugins {
  id 'com.android.application'
  // Add the Google services Gradle plugin
  id 'com.google.gms.google-services'
  ...
}
...
dependencies {
  // Import the Firebase BoM
  implementation platform('com.google.firebase:firebase-bom:32.5.0')
  // TODO: Add the dependencies for Firebase products you want to use
  // When using the BoM, don't specify versions in Firebase dependencies
  // https://firebase.google.com/docs/android/setup#available-libraries
  
  // Firebase Authentication
    implementation("com.google.firebase:firebase-auth")
    // Google Identity Services SDK (only required for Auth with Google)
    implementation("com.google.android.gms:play-services-auth:20.7.0")
    // Firebase UI
    // Used in FirebaseUIActivity.
    implementation("com.firebaseui:firebase-ui-auth:8.0.2")
    ...
}
```
Please note that I'm adding dependencies for "Google Identity Service SDK" and "Firebase UI" as they are necessary for 
this module as well.
14) Press "Next" and "Continue to console" to finish your project setup... but you are not ready so far !
15) In step 10 we downloaded the "google-services.json" file, please move this file to your "app" folder. As the 
Firebase Quickstart Android project contains several modules please move the "google-services.json" file to the 
"auth/app" folder. If you start your app and the file is missing or at the wrong place you find a note in your Logcat 
file and your app won't work.

## step 3 configure the Authenticate options

All steps above were necessary to get a connection between your app and the Firebase servers, now we need to define which 
authentification options we are going to accept for our project. The Firebase Quickstart Android code contains e.g. the 
authentication with a Facebook account - as I'm not having one I cannot test or use this option. For my sample app I'm 
using the following authentications:
- authenticate with an email address and password
- authenticate with a Google account
- authenticate anonymously (without any account)

Please keep in mind that it depends on your specific needs what kind of authentication options you are using.

In step 2 the final action was to return to the Firebase's console and now it's the right time to **choose a product**, in this  
case I'm adding the **Authentication** product - simply press on the large button "Authentication".
1) click on "Get started" and wait some seconds
2) we need to choose one or more "Sign-in provider", as a start we use the native provider "Email/password" and click on the button
3) Enable "Email/Password" but leave "Email link (passwordless sign-in)" disabled a this requires some more steps to setup. Press "save".
4) That was easy - the "Email/Password" is enabled now. Now press the button "Add new provider" for another provider
5) Press "Anonymous" in the overview
6) Enable the switch for the "Anonymous" provider and click on "Save"
7) As a last example press "Add new Provider" and press the "Google" button
8) Enable the switch for the "Google" provider and choose the Email address of your Google account as "Support email for project".
9) Press "Save" and we should be ready now, but a message appears: "Can't enable Google sign-in. An identical OAuth client already exists." 
** This a serious warning because it means: A package name needs to be UNIQUE when using Google authentication.** In the end you won't be 
able to use Google authentication within your project and the only chance is a change of your application package to a unique one.
I changed it to "de.androidcrypto.firebase.quickstart.auth", deleted the old "app" in Firebase console and added the changed one. There are some 
additional clicks and deletion steps to go but in the end you get a running client accepting the Google authentication. 

10) This is accompanied by the note that we need to run some more steps:
```plaintext
Enabling Google sign-in for the first time creates new OAuth clients, which are automatically added to the config files for your apps.

Download and replace the configuration files in your apps so that you can use Google sign-in for your apps.

After replacing your config files, finish setting up Google sign-in for Android and Apple apps. 
```
See: Authenticate with Google on Android, Link: https://firebase.google.com/docs/auth/android/google-signin

See: Authenticate with Google on Android, Link: https://firebase.google.com/docs/auth/android/google-signin?hl=en&authuser=0&_gl=1*1fbtazb*_ga*MjAwMDk1NjQyMy4xNjk5MTg0MjU1*_ga_CW55HF8NVT*MTY5OTM1MjgxNy44LjEuMTY5OTM1Njc2Ni4xMy4wLjA.

In the console go to "Project overview" and "Project settings" and download the new generated "google-services.json" file 
(**don't forget to move the file to the auth/app folder**) and add the Google Play services library dependency to you app/module 
"build.gradle" file (here all dependencies are shown):
```plaintext
dependencies {
    // Import the BoM for the Firebase platform
    implementation(platform("com.google.firebase:firebase-bom:32.5.0"))
    // Add the dependency for the Firebase Authentication library
    // When using the BoM, you don't specify versions in Firebase library dependencies
    implementation("com.google.firebase:firebase-auth")
    // Also add the dependency for the Google Play services library and specify its version
    implementation("com.google.android.gms:play-services-auth:20.7.0")
}
```

Now we are ready to start the auth app within Android Studio - it is running on a real device or an emulator.

