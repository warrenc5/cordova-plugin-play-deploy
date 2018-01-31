Create your IamService Account file is relative to cordova root directory.

`cordova plugin -d add cordova-plugin-play-deploy --no-registry --variable IAM_SERVICE_ACCOUNT_JSON_FILE_LOCATION='Google Play Android Developer-07b05227da33.json'`

Then you need to add `com.github.triplet.gradle:play-publisher:1.2.0` to the classpath (because of a weird gradle plugin classloading issue) to `platforms/android/build.gradle`

Which gets overwritten after every clean - I know this is hacky -- I tried to add it as a framework in plugin but that didn't work.

``` buildscript {
        repositories {
                jcenter()
                        maven {
                                url "https://maven.google.com"
                        }
        }
        dependencies {

                // NOTE: Do not place your application dependencies here; they belong
                // in the individual module build.gradle files
                classpath 'com.android.tools.build:gradle:3.0.0'
                classpath 'com.github.triplet.gradle:play-publisher:1.2.0'
        }
```}


Then you can send up the Apk.

`cordova build android --browserify --release -- --gradleArg=--stacktrace --gradleArg=--info --gradleArg publishApkArmv7Release`

To see a list of all the tasks

`cordova clean android --gradleArg=--stacktrace --gradleArg=--info --gradleArg tasks`

Troubleshooting

The first APK must be uploaded manually.

401 Unauthorized, go into Play Console users & permission, you will see the IAM account has been trying to access the app. Grant permission and try again.


