# Deploy

## 前言

30天系列要進入尾聲了，在倒數第二天的這時候，要來講開發產品流程的最後一步 —— 部署。不過這篇的部署目前只會提到 Android 的部分，因為我手邊沒有 iOS 的手機可以做測試，日後把這個部分完成後，會一併補上。

## 部署流程

#### Android

關於 android 的部署流程，其實網路上都說的蠻好的，在這邊我會引用一些資料，然後提示一些比較需要注意的地方。首先，先參考 [這篇](https://facebook.github.io/react-native/docs/signed-apk-android.html) ，總共分為以下幾個步驟：

1. 第一步是先產生一個簽名的 key 。因為 Google Play 上所有的 APP 在上架前，都被要求先簽署，確保軟體是 OK 沒問題，而不是惡意的。

```
keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
```

要注意的是，這邊要根據自己的習慣，調整 keystore 的名字，並妥善保存，例如發到 bitbucket 或者 gitlab 等private repo。app 在發部之後，如果需要做調整的話，都需要再簽上同一個 keystore，如果這個 keystore 弄丟的話，那麼就只能再重新發佈另一個 app ，那麼對產品是一個重大的損失。

2. 設定 ```~/.gradle/gradle.properties``` 的資料。（參閱 [連結](https://facebook.github.io/react-native/docs/signed-apk-android.html#setting-up-gradle-variables) ）

3. 改變 ```android/app/build.gradle``` 的 config。（參閱 [連結](https://facebook.github.io/react-native/docs/signed-apk-android.html#adding-signing-config-to-your-app-s-gradle-config) ）

4. ```./gradlew assembleRelease``` 產生 release 版的 app。要注意的是，之前的 ```react-native run-android``` 所發佈的版本都是 debug 版本的，使用是預設的 debug.keystore。產生後的 apk ，不管是 release 或者 debug，都是放在 ```/android/app/build/outputs/apk```內。

#### iOS

(略，待補充）