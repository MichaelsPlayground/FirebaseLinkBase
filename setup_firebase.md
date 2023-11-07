# Setup Firebase

To run Firebase project it is necessary to setup your project in the Firebase console. Follow the link
https://console.firebase.google.com/ and **login with your Google account**.

This are the steps I used to setup the project for the **Firebase Quickstart Android** project.

**Recommendation**: In the first time you will setup a lot of projects but the number of projects is limited
(about 10 projects are allowed) and I strongly recommend to **use a second, "test" account** for the setups and 
not your regular Google account. This is because you cannot delete projects no longer in use and reuse the 
project space again - you have to wait some weeks before the console accepts new projects.

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
7)  
