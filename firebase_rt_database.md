# Firebase Real Time Database

Talking about a database is usually the second step in the development of a Firebase app. When you are going to check the Firebase console 
website you will find 3 products that are suitable to store data:

**Real Time Database**: Real Time Database (RT Database) is Firebase's original database. It's an efficient, low-latency solution for mobile apps that 
require synced states across clients in realtime.

**Firestore Database**: Cloud Firestore is Firebase's newest database for mobile app development. It builds on the successes of the Realtime 
Database with a new, more intuitive data model. Cloud Firestore also features richer, faster queries and scales further than the Realtime Database.

If you should need to decide between RT Database and Firebase I recommend to check the link https://firebase.google.com/docs/database/rtdb-vs-firestore?hl=en.

I will not conceal that the usage of the newer Firestore database may be more expensive as the "old" Real Time Database.

**Storage**: This is not a database but a storage solution, so it good to store user data like images, video, audio files or documents and PDF's.

This document is about the setup of a Real Time Database. We start with the product choice in the Firebase console.

1) click on the product "Database"
2) click on "create database"
3) The next step is important for your database performance: you need to choose the server location for your database: choose between a location in 
the United States of America, Europe or in Asia. As I'm located in Germany I have chosen for "Belgium". Please note that it is not possible to change 
this setting at a later time.
4) The second step is about **Security rules** and I don't realy like the two possible options:
- start in **locked mode**: means a "unusable database" because no data can get appended, deleted or even read. Choose this option if you know what 
individual rules need to get setup in a following step.
- start in **test mode**: means the database will allow an unlimited read and write access without any limitations. As this setup is **unsecure** 
the database has a time limit of 1 month. This option is good for testing purposes but there is high risk that you forget about the time limit and 
are surprised when your application stops to work properly.

I'm choosing the locked mode here as the sample app provides some prepared database rules in the readme.md document:

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
5) press the "Enable" button to setup the Realtime Database (wait some seconds)
6) At this time the database is empty, but you should click on the "Rules" tab to edit the "locked mode":
```plaintext
{
  "rules": {
    ".read": false,
    ".write": false
  }
}
```
Copy and paste the sample rules from step 4 into the rules editor and press the "Publish" button.

Note: If you would like to "play" a little bit try the Rules Playground.
7) We should not forget to think about "pricing". Click on the "Usage" tab to get an idea about possible billing parameters. 
An overview about pricing can be found here: https://firebase.google.com/pricing. As you can see you can start with most products without 
generating any bills (at "no cost") but there are limitations on the the free "Spark" plan.
8) The last step is to move to "Project Overview" - "Project settings"
9) Think about the changes we made in the build.gradle file: edit the (module) build.gradle file for the database module:
```plaintext
old data:
  applicationId = "com.google.firebase.quickstart.database"
new data:
  applicationId = "de.androidcrypto.firebase.quickstart.database"   
```
This is necessary to avoid any "double package entry" errors.
10) click on "Add app" to append the database module to our Firebase project
11) choose the Android icon
12) register your "app" = database module by entering the applicationId (see step 9): "de.androidcrypto.firebase.quickstart.database"
13) enter an apps nickname
14) enter the SHA1 fingerprint (is the same as for the first app): 19:22:a4:d7:01:a8:3d:09:8f:04:93:e9:8e:21:92:2d:5a:5f:b0:54
15) press "Register app" and wait for some seconds
16) Now download the (appended/changed) google-services.json file. **Don't forget to move the file to the database/app folder**.




