IamService Account file is relative to cordova root directory

cordova plugin -d add cordova-plugin-play-deploy --no-registry --variable IAM_SERVICE_ACCOUNT_JSON_FILE_LOCATION='Google Play Android Developer-07b05227da33.json'

you need to add com.github.triplet.gradle:play-publisher:1.2.0 to the classpath (because of a weird gradle plugin classloading issue) to platforms/android/build.gradle

buildscript {
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
}

