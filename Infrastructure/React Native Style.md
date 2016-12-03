# React Native Style

## 前言
```Style```，是整個架構很重要的一個元素。除了component 之外，我們也需要 style 去裝飾整個畫面。這個章節，我將會解釋，在 Deeperience-react-native ，我們如何抽出 style 讓整個專案會更好寫的。

## Style 的架構

#### 各個component

關於各個 component 的 style，我把它放在各個 js 檔同個目錄下的 styles.js。至於 React Native style 的寫法，詳細可以參考 [這一篇](https://facebook.github.io/react-native/docs/stylesheet.html) 和 [這一篇](https://facebook.github.io/react-native/docs/style.html) 。

#### 共用的 style

首先，我們要先抽出整個專案會共用的 style，這部分我們把它們放在 ```/src/styles/origin/index.js```。之所以會命名成 origin，是因為這是最原始的 theme。如果之後有要再更改 theme 的話，那我們就再複製一個資料夾，設定這個部分即可。

#### 平台特定的 style 呢？

因為 Android 和 iOS 平台對於 style render 出來的結果還是有一些不一樣。例如行高、字距⋯⋯。此外，Android 和 iOS 的用戶體驗不一樣，有時候，我們需要針對各個平台設計不同的style。於是我們便參考網路寫法，寫了一個加強版的 stylesheet。

```
import { StyleSheet as RNStyleSheet, Platform } from 'react-native'

class StyleSheet {
  static create(styles: Object): {[name: string]: number} {
    const platformStyles = {}
    Object.keys(styles).forEach((name) => {
      const { ios, android, ...style } = { ...styles[name] }
      let outputStyle = style
      if (ios && Platform.OS === 'ios') outputStyle = { ...style, ...ios }
      if (android && Platform.OS === 'android') outputStyle = { ...style, ...android }
      platformStyles[name] = outputStyle
    })
    return RNStyleSheet.create(platformStyles)
  }
}

export default StyleSheet
```

大致上的意思，就把把原來 object 中 ios attribute 和 android attribute 的部分抽出來，然後判定平台是什麼，最後 render。

於是我們就可以寫出下面這樣的 code ：

```
export default StyleSheet.create({
  container: {
    flex: 1,
    paddingLeft: 20,
    paddingRight: 20,
    ios: {
      paddingTop: 15,
      paddingBottom: 15,
    },
    android: {
      paddingTop: 10,
      paddingBottom: 10,
    },
    backgroundColor: 'white',
  },
)}
```