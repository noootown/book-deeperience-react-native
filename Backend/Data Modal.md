# Data Model

## 前言

在 ```mongodb``` 這類的 ```NoSQL```，以及他的 ODM 例如 ```Mongoose``` 都會提供一個 Model 的功能，方便程式設計師定義資料的形式。由於 firebase 沒有 model，為了資料的好看，我們也實作了一個簡單的 model，事先定義好資料的格式。

注意！這個功能還在評估階段，目前也沒有看到有專案有實作類似的功能。

## 結構

關於 model ，我們把它放在 ```src/model``` 底下。抽出一個 UserModel 來解釋我們設計的原則，程式碼如下：

```
import ModelInterface from './ModelInterface'

type idType = string
type userDataType = {
  email: string,
  username: ?string,
  avatar: ?string,
}

const PATH = '/users/'

export default class UserModel extends ModelInterface {
  constructor(id: idType, userData : userDataType) {
    super(userData)
    this.id = id
    this.data = userData
  }
  getPath() {
    return `${PATH}${this.id}`
  }
  getData() {
    return this.data
  }
}
```

在上面的程式碼，我們繼承了 ```ModeInterface```。ModelInterface裡，定義了 ```getPath``` 和 ```getData``` 兩個 function，代表我們要實作它。getPath 代表的是在 firebase 裡面儲存的路徑，而 getData 則是取得這個 record 的 data 部分。

另外，我們還使用了 ```flow``` 這們 ```Facebook``` 開源的套件來做型別的檢查，關於 flow 這個套件，會在之後的章節做講解。

操作方法如下

```
const user = new UserModel(uid, { email, username })
user.getPath() // 取得 path
user.getData() // 取得 data
```