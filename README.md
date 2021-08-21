# vue-practice

## 【Vue.js2&Vue.js3 対応】】 基礎から 【Vuetify】 を使った応用まで！

### 1.4 Vue のインストール

関数で返すように書く

```javascript
...
data: function () {
    return {
    	message: "Hello Vue!",
    };
},
...
```

Vue インスタンスのプロパティは以下のドキュメントを参照

- https://jp.vuejs.org/v2/api/#%E3%82%A4%E3%83%B3%E3%82%B9%E3%82%BF%E3%83%B3%E3%82%B9%E3%83%97%E3%83%AD%E3%83%91%E3%83%86%E3%82%A3

メモ

- `Vue` インスタンスを作成する必要がある
- `el`: 仮想 DOM
- `data`

# 公式ドキュメント

## ディレクティブ

ディレクティブは `v-` から始まる特別な属性です。ディレクティブ属性値は、**単一の JavaScript 式**を期待します。

### 引数

ディレクティブの中には “引数” を取るものもあります。これはディレクティブ名の後にコロンで表記します。例えば、`v-bind` ディレクティブは、リアクティブに HTML 属性を更新します:

```html
<a v-bind:href="url"> ... </a>
```

- `v-bind`: HTML 要素に使用すると、属性を動的に設定できる。コンポーネントに使用すると、コンポーネントのプロパティを動的に設定できる。

### 修飾子

修飾子 (Modifier) は、ドットで表記された特別な接尾語で、ディレクティブが特別な方法で束縛されるべきということを示します。例えば、`.prevent` 修飾子は `v-on` ディレクティブに、イベントがトリガされた際 `event.preventDefault()` を呼ぶように伝えます:

```HTML
<form v-on:submit.prevent="onSubmit"> ... </form>
```

## 算出プロパティとウォッチャ

### 算出プロパティ

#### 基本的な例

```HTML
<div id="example">
  <p>Original message: "{{ message }}"</p>
  <p>Computed reversed message: "{{ reversedMessage }}"</p>
</div>
```

```JavaScript
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // 算出 getter 関数
    reversedMessage: function () {
      // `this` は vm インスタンスを指します
      return this.message.split('').reverse().join('')
    }
  }
})
```

## リストレンダリング

### `v-for` で配列に要素をマッピングする

```HTML
<ul id="example-1">
  <li v-for="item in items" :key="item.message">
    {{ item.message }}
  </li>
</ul>
```

```JavaScript
var example1 = new Vue({
  el: '#example-1',
  data: {
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```

結果:

```
* Foo
* Bar
```

- バブリングとキャプチャリング

API の違い

|                | `methods`          | `computed`                                                 | `watch`                                                              |
| -------------- | ------------------ | ---------------------------------------------------------- | -------------------------------------------------------------------- |
|                | メソッド           | 算出プロパティ                                             | 監視プロパティ                                                       |
| 使い方         | 一般的な関数と同様 | return 内に特定したい data を含める `this.xxx`             | 特定したい data 名で作成、コールバック関数を含める                   |
| キャッシュ     | キャッシュされない | キャッシュする                                             | キャッシュする                                                       |
| 実行タイミング | 再描画の度に実行   | 特定 data 変更時、特定 data を元に派生したデータを使うとき | 特定 data 変更時、特定コールバック関数を実行、非同期処理 (Ajax など) |
