# react-native-lightning

##[DEPRECATED]
###Please consider using either of the following libraries instead:
 - https://github.com/synonymdev/react-native-lightning
 - https://github.com/LtbLightning/rn-ltbl

:warning: This is pre-alpha software. Please use as your own risk.

### Description
This library hopes to simplify the process of adding Lightning via LND's Neutrino to any React-Native app. 

### Android Installation:

Video Walkthrough: [TODO]

If you have any trouble, please use [this commit](https://github.com/coreyphillips/photon/commit/925510f3515f6bac812d41a49a43d3a0c0981dfe) as a reference to what needs to be changed/added to your project to get everything working.

1. Install Dependencies:
   ```
    yarn add react-native-lightning buffer react-native-randombytes react-native-crypto react-native-keychain@4.0.5
    yarn add -D rn-nodeify
    yarn install
    ```
2. Start the project:
    
    `react-native run-android`
    
#### Example Usage
```
const lnd = require("react-native-lightning");
lnd.start();
```
    
### iOS Installation (In Progress)

### Manual (Android/iOS):
1. `yarn add react-native-lightning buffer react-native-randombytes`

2. Add the following to the end of your postinstall script in yourproject/package.json:
    - `cd node_modules/react-native-lightning && yarn install && ./node_modules/.bin/rn-nodeify --install buffer,stream,assert,events,crypto,vm,process --hack`
 
3. Copy react-native-lightning/src/lnd.config to the following. (Note: Create the directories if they do not exist):
     - Android - `android/app/src/main/assets/lnd.config`
     - iOS - `ios/lightning/lnd.config`
     
4. Copy necessary files over for Android & iOS respectively:
    - Android - Copy LndNativeModule.java & LndNativePackage.java to `android/app/src/main/java/com/yourproject/` and be sure to replace "com.rnlightning" at the top of each file with the name of your own project.
    - iOS - Copy LndReactModule.h & LndReactModule.m to `ios/lightning/`.
     
5. Generate the Lndmobile.aar & Lndmobile.framework files.
    - Option 1 - Generate them locally with lnd v0.9:
        - To generate these files, please follow the instructions detailed in the README of Lightning Lab's Lightning App [here.](https://github.com/lightninglabs/lightning-app/tree/master/mobile)
    - Option 2 - Download pre-generated files:
        - If you do not wish to generate these files locally you can download them [here](https://github.com/coreyphillips/photon/releases/tag/v0.0.1) instead. However, I highly recommend you opt for option 1.

6. Add the Lndmobile.aar & Lndmobile.framework files to the project:
    - Add the Lndmobile.aar file to `android/Lndmobile`
    - Add the Lndmobile.framework file to `ios/lightning`

7. Add `packages.add(new LndNativePackage());` to "getPackages" in MainApplication.java just above `return packages`"

8. For Android you'll need these additional dependencies in `YourProject/android/app/build.gradle`:
 - `implementation 'com.google.protobuf:protobuf-java:3.13.0'`
 - `implementation 'com.android.support:multidex:1.0.3'` 
 - Then Add `multiDexEnabled true` under `defaultConfig` in the same gradle file.

9. Start the project:
    - iOS: `react-native run-ios`
    - Android: `react-native run-android`
