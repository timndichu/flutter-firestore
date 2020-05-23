# flutter-firestore
How to connect your flutter app to firebase

## Step 1: Creating your Flutter App
Create your flutter app within VS-Code: ```Ctrl+Shift+P``` Then from the infobox that appears, ```>Flutter: New Project``` </br>
Then wait for everything to be load in

## Step 2: Create a Firebase Project
1. In the Firebase console: https://console.firebase.google.com, click Add project, then select or enter a Project name. </br>
If you have an existing Google Cloud Platform (GCP) project, you can select the project from the dropdown menu to add Firebase resources to that project. </br>
2. Click Continue. </br>
3. Click Create project (or Add Firebase, if you're using an existing GCP project).

## Step 3: Register your app with Firebase
1. In the center of the Firebase console's project overview page, click the Android icon to launch the setup workflow. </br>
2. Enter your app's package name in the Android package name field. <br>
**This is important: Make sure to use a ```com.companyname.appname``` setup and not ```com.example.appname```. So choose an appropriate name** </br>
*Find this package name in your module (app-level) Gradle file, usually app/build.gradle (example package name: com.yourcompany.yourproject). </br>
Make sure to find all occurrences of that package name in your project and replace all of them > from com.example.yourprojectname > to what you want it named <br>*
3. Click Register app.

## Step 4: Add a Firebase configuration file

1. Click Download google-services.json to obtain your Firebase Android config file (google-services.json).
 *You can download your Firebase Android config file again at any time.
 Make sure the config file is not appended with additional characters, like (2).* <br>

2. Move your config file into the android/app directory of your Flutter app. <br>

3. To enable Firebase services in your Android app, add the google-services plugin to your Gradle files, as follows: <br>
  a) In your root-level (project-level) Gradle file (android/build.gradle), add rules to include the Google Services Gradle plugin. Check that you have Google’s Maven repository, as well. 
  ```
  buildscript {

    repositories {
      // Check that you have the following line (if not, add it):
      google()  // Google's Maven repository
    }

    // ...

    dependencies {
      // ...

      // Add the following line:
      classpath 'com.google.gms:google-services:4.3.3'  // Google Services plugin
    }
}

allprojects {
    // ...

    repositories {
      // Check that you have following line (if not, add it):
      google()  // Google's Maven repository
      // ...
    }
}
 ```

  <br>
  
 b) In your module (app-level) Gradle file (usually android/app/build.gradle), apply the Google Services Gradle plugin. <br>
  ```
      // Add the following line:
    apply plugin: 'com.google.gms.google-services'  // Google Services plugin

    android {
      // ...
    }

    // ...

  ```
  <br>

4. Run flutter packages get in VS CODE.


5. Back in the Firebase console setup workflow, click Next to skip the remaining steps.


## Step 5: Add FlutterFire Plugins

1. Ensure that your app is not currently running in your emulator or on your device. <br>

2. From the root directory of your Flutter app, open your pubspec.yaml file.

3. Add the FlutterFire plugins for the Firebase Core Flutter SDK.
      ```
      dependencies:
        flutter:
          sdk: flutter
        # Add the dependency for the Firebase Core Flutter SDK
        firebase_core: 

      ```
      
4. Add the other Flutter Fire plugins you want to use <br>
     ```
     dependencies:
       flutter:
         sdk: flutter
       # Check that you have this dependency (added in the previous step)
       firebase_core:

       # Add the dependency for the FlutterFire plugin for Google Analytics
       firebase_analytics: 

       # Add the dependencies for any other Firebase products you want to use in your app
       # For example, to use Firebase Authentication and Cloud Firestore
       firebase_auth: 
       cloud_firestore:

     ```
     <br>

5. Run flutter packages get.
<br>


## The most important steps (If your app fails to build after adding the FlutterFire Plugins)

1. Enable multidex.
<br>

Open android/app/build.gradle and add the following lines.
    ```
    defaultConfig {
        ...
        multiDexEnabled true
    }
    ```
    
<br>

and

```
dependencies {
    ...

    implementation 'com.android.support:multidex:1.0.3'
}
```


If you have migrated to AndroidX, you'll want this instead:
```
dependencies {
    ...
    implementation 'androidx.multidex:multidex:2.0.1'
}
```

<br>

