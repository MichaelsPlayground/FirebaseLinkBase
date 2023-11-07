# Get the SHA-1 hash of your application

Link: https://developers.google.com/android/guides/client-auth

I'm using the "signing report way" here:

1) open your project in Android Studio
2) on the right sidebar you find the Gradle "button"
3) click on the "play symbol" meaning "Execute Gradle Task"
4) in the opening window type **signingReport** and press the "enter" button
5) at the bottom the "Run" window opens with this (much longer) report:
```plaintext
> Task :analytics:app:signingReport
Variant: debug
Config: debug
Store: /Users/xxx/.android/debug.keystore
Alias: AndroidDebugKey
MD5: 4D:1E:D7:91:56:67:73:EA:54:73:BC:EC:D7:E5:9B:F5
SHA1: 19:22:A4:D7:01:A8:3D:09:8F:04:93:E9:8E:21:92:2D:5A:5F:B0:54
SHA-256: A7:A8:66:27:C7:76:6D:C3:3C:9E:3F:89:99:88:3E:A1:7B:ED:34:69:19:83:B6:EA:72:04:C9:13:8E:84:E0:90
Valid until: Samstag, 30. September 2051
----------
...
```
6) The important part ist the **SHA1** value - just copy **YOUR** data:

**19:22:A4:D7:01:A8:3D:09:8F:04:93:E9:8E:21:92:2D:5A:5F:B0:54**

The value is a sample for MY SHA1 value, don't use it for your project !
