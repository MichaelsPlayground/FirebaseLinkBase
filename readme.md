# Firebase Link Base

Please note: This is not an app but "just" my link repository for all themes around **Firebase**.

## Start point and console

Start point: https://firebase.google.com/

Link to Firebase console: https://console.firebase.google.com/

## Basic information

Base information about Firebase: https://firebase.google.com/docs/guides

Add Firebase to your Android project: https://firebase.google.com/docs/android/setup

Learn about using and managing API keys for Firebase: https://firebase.google.com/docs/projects/api-keys

Learn more about Android and Firebase: https://firebase.google.com/docs/android/learn-more

## Firebase Quickstarts for Android

Firebase Quickstarts for Android: https://firebaseopensource.com/projects/firebase/quickstart-android/

GitHub repository with all (Android) Java and Kotlin code: https://github.com/firebase/quickstart-android

Themes: Admob, Analytics, App Distribution, App Indexing, Authentication, Remote Config, Crashlytics, 
Realtime Database, Dynamic Links, Firestore, Cloud Functions, In App Messaging, Cloud Messaging, 
ML Kit, Performance Monitoring, Cloud Storage

### Authentication Quickstart

Link: https://firebaseopensource.com/projects/firebase/quickstart-android/auth/readme

Auth setup for Email/Password authentication: 
- Go to the Firebase Console and navigate to your project:
- Select the Auth panel and then click the Sign In Method tab.
- Click Email/Password and turn on the Enable switch, then click Save.
- Under Authorized Domains click Add Domain and add auth.example.com.
- Run the app on your device or emulator.
- Select EmailPasswordActivity from the main screen.
- Fill in your desired email and password and click Create Account to begin.

### Firebase Database Quickstart

Link: https://firebaseopensource.com/projects/firebase/quickstart-android/database/readme

Database Rules - Below are some samples rules that limit access and validate data:
```plaintext
{
  "rules": {
    // User profiles are only readable/writable by the user who owns it
    "users": {
      "$UID": {
        ".read": "auth.uid == $UID",
        ".write": "auth.uid == $UID"
      }
    },

    // Posts can be read by anyone but only written by logged-in users.
    "posts": {
      ".read": true,
      ".write": "auth.uid != null",

      "$POSTID": {
        // UID must match logged in user and is fixed once set
        "uid": {
          ".validate": "(data.exists() && data.val() == newData.val()) || newData.val() == auth.uid"
        },

        // User can only update own stars
        "stars": {
          "$UID": {
              ".validate": "auth.uid == $UID"
          }
        }
      }
    },

    // User posts can be read by anyone but only written by the user that owns it,
    // and with a matching UID
    "user-posts": {
      ".read": true,

      "$UID": {
        "$POSTID": {
          ".write": "auth.uid == $UID",
            ".validate": "data.exists() || newData.child('uid').val() == auth.uid"
        }
      }
    },


    // Comments can be read by anyone but only written by a logged in user
    "post-comments": {
      ".read": true,
      ".write": "auth.uid != null",

      "$POSTID": {
        "$COMMENTID": {
          // UID must match logged in user and is fixed once set
          "uid": {
              ".validate": "(data.exists() && data.val() == newData.val()) || newData.val() == auth.uid"
          }
        }
      }
    }
  }
}
```

### Firestore Quickstart

Link: https://firebaseopensource.com/projects/firebase/quickstart-android/firestore/readme

Security Rules - Add the following security rules to your project in the: rules tab:

```plaintext
service cloud.firestore {  
  match /databases/{database}/documents {
    // Anyone can read a restaurant, only authorized
    // users can create or update. Deletes are not allowed.
       match /restaurants/{restaurantId} {
         allow read: if true;
         allow create, update: if request.auth.uid != null;
    }

    // Anyone can read a rating. Only the user who made the rating
    // can delete it. Ratings can never be updated.
    match /restaurants/{restaurantId}/ratings/{ratingId} {
         allow read: if true;
      allow create: if request.auth.uid != null;
         allow delete: if request.resource.data.userId == request.auth.uid;
         allow update: if false;
    }
  }
}
```

### Cloud Storage for Firebase Quickstart

Link: https://firebaseopensource.com/projects/firebase/quickstart-android/storage/readme

## Other repositories from Firebase

Snippets for Android: https://github.com/firebase/snippets-android
(This repository holds code snippets used in Android documentation on firebase.google.com.)

FirebaseUI for Android: https://github.com/firebase/FirebaseUI-Android
(FirebaseUI is an open-source library for Android that allows you to quickly connect common UI elements to Firebase APIs.)

Samples: https://firebase.google.com/docs/samples?hl=en

Codelab FriendlyChat (Kotlin): https://firebase.google.com/codelabs/firebase-android/#0

Codelab FriendlyChat (Kotlin): https://github.com/firebase/codelab-friendlychat-android

# Third party tutorials

## JavaTPoint Firebase Tutorial

Link: https://www.javatpoint.com/firebase

Themes: Introduction, Firebase Authentication, Firebase UI, Firebase SDK, Firebase Real-time database, Firestore Database, 
Firebase Cloud Storage, Firebase Hosting, Firebase Cloud Function, Firebase Crashlytics, Clud Messaging, In-App-Messaging, 
Dynamic Link, AdMob

complete sourcecodes for several examples

## hackernoon.com User authentication in android using firebase (Java)

User Authentication in Android using Firebase (Java): https://hackernoon.com/user-authentication-in-android-using-firebase-java 
with Source code and setup Firebase project using the assistant

used Fonts: https://github.com/Temmarie/Fonts



End of documemt
