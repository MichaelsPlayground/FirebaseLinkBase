# Firebase Cloud Storage

This page is about the setup of a **Firebase Cloud Storage** product in Firebase console. We start with the product choice in the Firebase console.

1) click on the product "Storage"
2) click on "Get started"
3) This step is about **Security rules** and I don't really like the two possible options:
- start in **production mode**: means a "unusable database" because no data can get appended, deleted or even read. Choose this option if you know what
  individual rules need to get setup in a following step.
- start in **test mode**: means the database will allow an unlimited read and write access without any limitations. As this setup is **unsecure**
  the database has a time limit of 1 month. This option is good for testing purposes but there is high risk that you forget about the time limit and
  are surprised when your application stops to work properly.
I'm choosing the production mode here - don't forget to change it in step 6.
4) The next step is important for your database performance: you need to choose the server location for your database: choose between a location in 
the United States of America, Europe or in Asia. The are choices for "multi region" or "single region". As I'm located in Germany I have chosen for "Europe West". Please note that it is not possible to change
this setting at a later time: "*After you set this location, you cannot change it later. This location setting will also be the default location for Cloud Firestore.*"
5) The Firebase server creates a bucket after pressing "Done", just wait for up to a minute.
6) At this time the database is empty, but you should click on the "Rules" tab to edit the "production mode":
```plaintext
rules_version = '2';
// Craft rules based on data in your Firestore database
// allow write: if firestore.get(
//    /databases/(default)/documents/users/$(request.auth.uid)).data.isAdmin;
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read, write: if false;
    }
  }
}
```
You find more information about Security Rules here: https://firebase.google.com/docs/storage/security, but for this project I'm using a very simplified 
security role - this allows reading and writing of all files when the user is authenticated with Firebase Authentication:
```plaintext
rules_version = '2';

// Craft rules based on data in your Firestore database
// allow write: if firestore.get(
//    /databases/(default)/documents/users/$(request.auth.uid)).data.isAdmin;
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```
7) press "Publish" to get the new rules setting active
8) We should not forget to think about "pricing". Click on the "Usage" tab to get an idea about possible billing parameters. 
An overview about pricing can be found here: https://firebase.google.com/pricing. As you can see you can start with most products without 
generating any bills (at "no cost") but there are limitations on the the free "Spark" plan.
9) The last step is to move to "Project Overview" - "Project settings"
10) Think about the changes we made in the build.gradle file: edit the (module) build.gradle file for the storage module:
```plaintext
old data:
  applicationId = "com.google.firebase.quickstart.firebasestorage"
new data:
  applicationId = "de.androidcrypto.firebase.quickstart.firebasestorage"   
```
This is necessary to avoid any "double package entry" errors.
11) click on "Add app" to append the storage module to our Firebase project
12) choose the Android icon
13) register your "app" = storage module by entering the applicationId (see step 9): "de.androidcrypto.firebase.quickstart.firebasestorage"
14) enter an apps nickname
15) enter the SHA1 fingerprint (is the same as for the first app): 19:22:a4:d7:01:a8:3d:09:8f:04:93:e9:8e:21:92:2d:5a:5f:b0:54
16) press "Register app" and wait for some seconds
17) Now download the (appended/changed) google-services.json file. **Don't forget to move the file to the database/app folder**.






