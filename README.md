# AndroidGradleTest
A test for multiple builds of an Android project including/excluding Google Ads

This project is a test to see how to configure build.gradle and the Android project in order to create various builds of the same app.

App name:
  1. Games News (Content will be customised to have News for games, but otherwise be the same app)
  2. Regular News

App Versions:
  1. Lite Version (Free, Ad Supported)
  2. Pro Version (For sale at price)
  
Build Types:
  1. Debug
  2. Release
  
 The Lite version will contain google Ads, the Pro Version will have none.
 This makes for 8 Build Variants.

This was done in build.gradle by having 2 Build Flavours and 4 Built Types.

```

buildTypes {
        liteDebug {
            ...
        }
        liteRelease {
            ...
        }
        proDebug {
            ...
        }
        proRelease {
            ...
        }
        ...
    }

    productFlavors {
        gamesnews {
            ...
        }
        regularnews {
            ...
        }
    }

```


The pro versions of the app will contain no adds, so 'com.google.firebase:firebase-ads:10.0.1' dependancy was included only in the lite builds:

```

dependencies {
    
    ...
    
    liteDebugCompile 'com.google.firebase:firebase-ads:10.0.1'
    liteReleaseCompile 'com.google.firebase:firebase-ads:10.0.1'

    ...
}

```

However, the layout and java code relies on these dependancies, therefore a customised Activity java file and layout was created for both pro and lite versions (each in their own folder) However, to link each of the 4 build types to the corresponding source folder, customised source folders had to be set

```

sourceSets {
        proDebug {
            res.srcDirs = ['src/pro/res']
            java.srcDirs = ['src/pro/java']
        }
        proRelease {
            res.srcDirs = ['src/pro/res']
            java.srcDirs = ['src/pro/java']
        }
        liteDebug {
            res.srcDirs = ['src/lite/res']
            java.srcDirs = ['src/lite/java']
        }
        liteRelease {
            res.srcDirs = ['src/lite/res']
            java.srcDirs = ['src/lite/java']
        }
    }
 
 ```
 
 The final result is 8 build variants selectable. Adding a new app version (i.e. Sports News) is trivial and will create the relevant Build Types for that app
