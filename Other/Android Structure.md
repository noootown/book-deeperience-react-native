# Android Structure

## 前言

提完了 iOS 的架構，接下來就要提 Android 的部分囉。設定 Android 時，相比 iOS 起來，稍微方便一些。讓我們看下去。

## 架構

Android 的檔案架構大致如下：

```
/android
	/.gradle
	/app
		/build
		/src
			/assets
			/main
				/java/com/deeperience/
					MainActivity.java
					MainApplication.java
		build.gradle
	/gradle
	/keystores
```
其中對我們來說，較為重要的是 ```/app``` 和 ```/keystores```。因為前者記錄著我們使用的 library，而後者放著我們的 keystore ，是為了 deploy 用的。

那麼我們就直接來看看如何引入一個呼叫 Android 原生 API 的 react native library 吧！

第一步和第二步：

MainApplication.java:

```
package com.deeperience;

import android.app.Application;
import android.util.Log;

// 這邊是 import 我們所有會用到的 library (第一步)

import com.facebook.react.ReactApplication;
import com.burnweb.rnsimplealertdialog.RNSimpleAlertDialogPackage;
import com.facebook.react.ReactInstanceManager;
import com.facebook.react.ReactNativeHost;
import com.facebook.react.ReactPackage;
import com.facebook.react.shell.MainReactPackage;
import com.magus.fblogin.FacebookLoginPackage;
import com.oblador.vectoricons.VectorIconsPackage;
import com.burnweb.rnsimplealertdialog.RNSimpleAlertDialogPackage;
import com.i18n.reactnativei18n.ReactNativeI18n;

import java.util.Arrays;
import java.util.List;


public class MainApplication extends Application implements ReactApplication {

  private final ReactNativeHost mReactNativeHost = new ReactNativeHost(this) {
    @Override
    protected boolean getUseDeveloperSupport() {
      return BuildConfig.DEBUG;
    }

   // 把所有要用的 package 塞在這裡 (第二步)
    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
                                         new MainReactPackage(), 
                                         new RNSimpleAlertDialogPackage(),
                                         new VectorIconsPackage(),
                                         new ReactNativeI18n(),
                                         new FacebookLoginPackage()
                                         );
    }
  };

  @Override
  public ReactNativeHost getReactNativeHost() {
      return mReactNativeHost;
  }
}
```

接著還有第三步，看到 ```/android/app/build.gradle```，注意，有兩個 ```build.gradle```。

```
.....
dependencies {
	// 有一些 library 會需要在這邊也加上。
    compile project(':react-native-simpledialog-android')

    compile fileTree(dir: "libs", include: ["*.jar"])
    compile "com.android.support:appcompat-v7:23.0.1"
    compile "com.facebook.react:react-native:+"  // From node_modules

    compile project(':react-native-vector-icons')
    compile project(':react-native-i18n')
    compile project(':react-native-facebook-login')
}
.....
```
到這裡就大功告成了，不過一樣，其實使用 ```react-native link``` 就可以解決了。然而，了解這些的話，我們在之後有遇到奇怪問題的時候就可以有工具解決囉！
