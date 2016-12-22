# Promise & Generator Function & Async Await

## 前言

這篇文章，想要探討的是javascript最有魅力的一個部分，非同步 (asynchronous)。 為什麼會說它是javascript最有魅力的一個部分呢？那是因為javascript本身應用的環境就充滿了各種非同步。打個比方好了，如果前端要和後端抓個資料，總不能送出request後，就block住吧，那如果資料沒回傳回來，不就GG了？其它事情都不用做了。所以，最正確的解，一定是送完request後，就繼續去做其它事，等待回來的結果，再根據結果做事。

我想如果有耳聞promise, ES6 yield, ES7 async/await 的朋友，應該不會錯過網路上有關於它們的文章和比較。不過說實話，有認真把它們都抓起來做一個完整比較和推演的文章，其實沒有很多，希望今天這一篇可以給想要了解這部分的人一個很完整的啟發，了解關於非同步這一塊，js是怎麼演進的。

## Callback

首先，我們要先講一下，到底什麼是callback。callback 是 javascript 很常用到的一種寫法，要熟悉js的話，就絕對不能不理解 callback 是什麼。

簡單來說，callback就是把A function傳進另一個 B function，當B function做完事後，就 call A function，做它該做的事。通常的用法是在讀資料庫的時候，或者call api的時候會使用到。因為這些動作都是非同步的，當做完事後，就要使用一個callback，來接這個資料，做該做的事。

要想像一下的話，大概就是今天你媽要炒菜，發現沒有醬油。剛好覺得在旁邊看電視的你太廢了，就叫你出去買罐醬油。你出去買的同時，媽媽還是在炒菜，只是沒有加醬油，沒辦法上菜罷了。於是為了省時，她就先切盤水果。

```
function 媽媽叫(跑腿完工作＝ 醬油買回來){
    叫你買醬油().done(醬油買回來(醬油){
        炒菜(醬油)
        上菜囉()
    })
    切水果()
}
```
大概就是這麼一個情況吧，醬油買回來就是一個callback ，也就是買醬油這個非同步的動作做完之後，會有相對應的callback 去 handle 該做的事。

如果有用過jquery的人，應該會有用過一個$.ajax的函式。這個函式是直接實現AJAX技術的，雖然$.ajax這個函式和這個jquery函式庫現在已經明日黃花了，我還是要稍微提一下它，因為方便我們做解釋。

假設政府提供一個查颱風即時動態的API好了，然後拿回資料後，我們可以在網頁上把它的位置畫出來。那麼程式碼如下：

程式碼如下：

```
$.ajax("www.president.gov.tw/api/typhoon",{})
  .done(function(result){
    draw(result)
  })
```

但如果我們希望每次做的事情不一樣，可以選擇的話，那我們就要考慮把它用一個 wrapper function 包起來，程式碼如下，功能是畫一個藍色和紅色的颱風（什麼鬼XD）

```
function drawRedTyphoon(result) {
  draw(result, 'red')
}

function drawBlueTyphoon(result) {
  draw(result, 'blue')
}

function manipulateTyphoon(func) {
  $.ajax("www.president.gov.tw/api/typhoon",{})
    .done(func(result))
}

manipulateTyphoon(drawBlueTyphoon)
```

這邊傳進去的func就是一個callback function，根據不同的callback，我們可以做不同的事。

喔對，我們還可以把上面的程式改寫成如下，ES6的形式，之後的教學都會使用ES6函式，算是一個語法糖吧，有興趣的可以研究一下。喔對，因為我超討厭寫ES5的表示方法，不太優雅XD。

```
const drawRedTyphoon = result => draw(result, 'red')
const drawBlueTyphoon = result => draw(result, 'blue')
const manipulateTyphoon = func =>
  $.ajax("www.president.gov.tw/api/typhoon",{})
    .done(func(result))
```

## Promise

Promise 是一個泛指的類，也就是說有不同類的 promise，定義著不同的標準，例如A+, ES6，之類的。其實我們上面用到的ajax，也是一個promise的類似概念，只是不屬於A+或ES6就是了。

總而言之，Promise就是把一個一個的動作，像在串香腸一樣，把它給串起來。怎麼說呢？請看下面的程式碼。

```
const p = new Promise(
  (resolve, reject) => {
    $.ajax("www.president.gov.tw/api/typhoon",{})
      .done(result => resolve(result))
   }).then(result => decorate(result,'blue'))
   .then(result => console.log(result))
```

這段程式碼的意思是當ajax成功拿到資料後，就會把資料經由resolve function 傳到下一個 then。也就是說，第一個 then 會接 promise 傳來的資料。而後面的 then 都會接上一個 then return的值，然後一層一層接下去。

上面這段程式碼的概念就是把拿到的颱風資料，裝飾一下藍色（什麼概念XD），然後再印出來。看到好處了嗎，我們把一行一行的邏輯定義在每一個then裡面，更方便我們釐清發生了什麼事。正因為如此，越來越多的api 直接都訂為回傳一個 promise，好處呢，就是可以在回傳的東西後面，直接接個then，做想要做的事情！

現行最通行的 promise，就是 ES6 定義的 promise。只要 new 一個 promise，馬上就可以處理很多非同步指令。最後，關於promise的部分，因為有很多複雜而且好用的用法，也有很多不一樣的 library 包裝起來，可以參照相關資料，學更多。

## 你怎麼還在 $.ajax？用fetch吧！

fetch是定義在前端的一個函式，也就是window.fetch，是一個目前實驗中的函式。雖然是實驗中，但多數瀏覽器都已經實作了。此外，考慮到$.ajax不是那麼的簡潔，而且又要import一整個jquery包，不如就使用fetch吧。

fetch的用法如下：

```
fetch(
  "www.president.gov.tw/api/typhoon",
  { method: 'GET' }
).then(result => result.json()) //有些回傳值會需要做json的轉換。
```

基本只要設定好domain和傳的method，就可以用來傳送request了。最大的好處就是它回傳的就是一個 ES6 promise，也就是說你愛多少個then就多少個，而且還直接相容ES6。

這邊要釐清一個重點，除了fetch之外，還有很多的AJAX library 可以實現回傳 promise 這個功能的。例如 superAgent，他的回傳值也可以直接接上then。換句話說，所有 promise 類的回傳，都一定要實作可以接上 then 這個功能，這也是當初 promise 標準制定時的一個條件。

## Callback hell

會叫做callback hell，就是因為寫它真的很痛苦，維護也很痛苦、大家都痛苦。譬如剛從氣象局拿回颱風的資料，然後要把它丟到server存到database，然後完之後，看後端api server的反應，決定我要不要更新畫面。那麼程式碼會長什麼樣子？

```
fetch(
  "www.president.gov.tw/api/typhoon",
  {method: 'GET'}
).then(result => {
    fetch("xxx.xxx.xx.x/api/storeTyphoon",
      {method: 'POST'}
    ).then(result => {
      if(result.error) {
        // do something, may be another ajax
      } else {
        // do something
      }
    })
  })
```

兩層的callback大致上就是這個樣子。那如果三層呢？像是result.error裡面要再重新request一次。抱歉，再加一層。如果是千層蛋糕，那該有多好，但不好意思，這是JS，非常的不好。所以勢必要有解決辦法。

So, do yield and generator function come to our rescue?

yield是ES6發佈的一個很重要的feature，他提供了一個很方便，但又不是那麼直覺的功能。

```
function * gen() {
  yield "沒";
  yield "一";
  yield "村";
}
let g = gen();
let a = g.next()
console.log(a.value) // “沒”
a = g.next()
console.log(a.value) // “一”
a = g.next()
console.log(a.value) // “村”
```

上面這一段是generator function的最簡單用法。詳細解釋如下。當我們呼叫gen()的時候，會生成一個generator function實體。Generator function 都是有一個 * 字號的，代表它和一般的function不一樣。

接著我們每call一次next() ，程式碼就會跑到yield的地方暫停。注意！真的是暫停，必須要等到下次呼叫next () 時，才會把yield右邊的資料丟給左邊的變數。這個階段其實也可以在next () 裡頭指定一個數，類似像next(assign)，來把assign變數指定給左邊的變數。接著如果要得到這個值，可以直接呼叫g.next().value。

你可能會覺得這是很普通的功能嘛。就只是迭代，然後一直呼叫next()。如果這麼理解yield的話，那就大錯特錯了。yield最強大的功能就是可以記錄目前函式進行到哪裡，一步一步做，而不會嘩啦啦一次作完。

也因為他有暫停這個特性，所以有人拿它來解決callback hell。但在這裡，沒一村非常不建議這麼做，因為可讀性和可維護性不會因此而變好，反而可能更難讀。

以下有一個關於generator function的介紹，我覺得寫的很棒。裡面有出一個範例為了解決callback hell。不過仔細推敲程式碼，就會發現超難懂！那我還不如寫callback hell。這就是拿yield來解決callback hell會產生的問題，太hacky了！而且事實上 yield 和 generator function本來就不是拿來處理這樣的情況。這是一個anti-pattern！

要非常注意的點是，如果你的yield右邊放一個promise，他是把整個promise丟給左邊的變數喔，不是丟回傳值！

[generator function詳細介紹](http://www.codedata.com.tw/javascript/es6-3-generator/)

## async 和 await，終於盼到你們兄弟倆了

終於來到了ES7，也終於盼到這兩位的幫忙了。Async await的用法很簡單，程式碼如下，一看就會懂了！

```
const getData = async () => {
  const a = await fetch(“xxx.xxx.xx.x”)
  const b = await fetch(“xxx.xxx.xx.x”)
}
```

這邊的a和b就真的是回傳的結果喔！

## 結語

說了這麼一大長串，不是指越後面提到的技術就越重要，這點非常重要！要了解的是，這是一個演化的過程，但有些東西還是會在它該出現的地方出現，只是對於我們現在想要達到的目的，不是個好方法就是了。

能全都用熟，然後自然而然的使用各個語法，那才是重點，沒有誰優於誰！

## 延伸閱讀

1. 這篇文章主要擷自我的另一篇 [文章](https://noootown.wordpress.com/2016/11/13/callback-promise-fetch-yield-async-await/)

2. [promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)

3. [JavaScript Promise API](https://davidwalsh.name/promises)

4. [fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)

不過fetch在有一些瀏覽器沒有支援，所以可以使用github的polyfill。這部分感謝網友Willy Hsu和朋友詹致遠提醒XD
5. [Github fetch](https://github.com/github/fetch)

6. [promise 和yield的用法（不過這篇的用法有一點anti pattern，可以參照留言一樓的說法）](http://huli.logdown.com/posts/292655-javascript-promise-generator-async-es6)

7. [generator function](http://www.codedata.com.tw/javascript/es6-3-generator/)

