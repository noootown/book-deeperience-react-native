# Flexbox

## 前言

我們一直反覆強調 React Native 的核心價值，就是 ```Learn once, Write anywhere```。接著這一張，我要提到react native style 的核心 —— flexbox。

## Container 和 Items

#### 分類

Flexbox 把所有DOM分成 Container 和 Items，指的是 CSS style 這部分的相依關係。包在外面的就是 container，而內部被包起來的就是 items 

所有的 attribute ，都分為 container attribute 或 item attribute。接下來會依依講解如何完成一個簡單的 flexbox版面設計。請搭配這篇 [CheatSheet](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) ，以及這篇 [Layout with Flexbox](https://facebook.github.io/react-native/docs/flexbox.html) 服用。

####  注意

這邊接下來提到的 Flexbox，都是依照 React Native 上的 Flexbox 舉例，和瀏覽器的屬性會有些許的不同。這點要注意。真正的 React Native Flexbox，請參考後面那篇的，而前面那篇的 Cheatsheet ，雖然是適用瀏覽器的，但還是有很大的參考價值。

#### 步驟

1. 由於 react native 都是以 flexbox 做排版，所以我們不需要加上 ```display: flex```這項屬性。

2. 接著我們要決定我們的 layout 是要橫在排或者直著排，前者請使用 ```flexDirection: row```，後者請使用 ```flexDirection: 'column'```。要注意的是，在react native 裡面，所有的 style都是寫在一個object  裡面，而object的key是沒有 ```-```的，所以要全部變成camel 表示。

3. 再來，我們要排上一步設定那個方向的排列方式，請使用  ```justifyContent``` 屬性來做排列，通常最常用的是置中對齊，那我們就使用 ```justifyContent: 'center'```。其它使用方式，可以參照 Cheatsheet。

4. 接著來排另一個方向的排列方式，這時我們要使用 ```alignItems```。通常會使用 ```center``` 來置中，也可以使用```stretch```來撐滿整個版面。

5. 到了這一步，我們算是把所有的 container attribute 都設定完了，接著我們就要設定 items 的 attribute。 items 的 attribute 相對好理解，我們會使用 ```order``` 來定義每個 items 在排列方向上，該佔多少比例的空間，否則就是依照原始 items 的寬度。或者我們也可以使用 ```flex``` 來縮寫很多個屬性。

6. 最後，我們可以在用alignSelf 來調整比較特別的 item。

## 結語

CSS3 的 Flexbox 是 RN 預設的排法，需要常練習，也請務必非常熟悉。

## 延伸閱讀

1. [react-native 之布局篇](https://segmentfault.com/a/1190000002658374)