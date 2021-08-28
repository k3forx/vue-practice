# vue-practice

## 【Vue.js2&Vue.js3 対応】】 基礎から 【Vuetify】 を使った応用まで！

### 1.4 Vue のインストール

関数で返すようにデータをバインドするので、バリデーションに使ったりできる書く

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

## Vue の基礎

### API の違い

|                | `methods`          | `computed`                                                 | `watch`                                                              |
| -------------- | ------------------ | ---------------------------------------------------------- | -------------------------------------------------------------------- |
|                | メソッド           | 算出プロパティ                                             | 監視プロパティ                                                       |
| 使い方         | 一般的な関数と同様 | return 内に特定したい data を含める `this.xxx`             | 特定したい data 名で作成、コールバック関数を含める                   |
| キャッシュ     | キャッシュされない | キャッシュする                                             | キャッシュする                                                       |
| 実行タイミング | 再描画の度に実行   | 特定 data 変更時、特定 data を元に派生したデータを使うとき | 特定 data 変更時、特定コールバック関数を実行、非同期処理 (Ajax など) |

### `this` について

```javascript
// Following log shows window object
console.log(this);

// Following log shows "object" of `test` function
const obj = {
  test: function () {
    console.log(this);
  },
};

// Following log shows window object
const objArrow = {
  test: () => {
    console.log(this);
  },
};
```

Like this...

![image](https://user-images.githubusercontent.com/45956169/130318654-c698b24d-d53a-4a74-b7f9-fdc97323f380.png)

### リアクティブ について

https://jp.vuejs.org/v2/guide/reactivity.html

- `data` 内に定義されたオブジェクトにはそれぞれ getter と setter が定義されている

![image](https://user-images.githubusercontent.com/45956169/130337355-4b65c2ee-ec1a-4bd0-a448-4ffac86fb923.png)

> Vue では、すでに作成されたインスタンスに対して新しいルートレベルのリアクティブなプロパティを動的に追加することはできません。しかしながら、`Vue.set(object, propertyName, value)` メソッドを使ってネストしたオブジェクトにリアクティブなプロパティを追加することができます:

```JavaScript
let app = new Vue({
  el: "#app",
  data() {
    return {
      reactiveTest: {
        name: "test",
      },
    };
  },
});
```

`message` には getter や setter がつかない

![image](https://user-images.githubusercontent.com/45956169/130337525-dd385810-d15b-4c0e-aa31-94845bd0922b.png)

### created と mounted

- `created`: `data`生成のタイミング (非同期通信でデータ取得したい場合)
- `mounted`: DOM 生成のタイミング

```JavaScript
let app = new Vue({
  el: "#app",
  data() {
    return {};
  },
  created() {
    console.log("created");
    console.log(this.$el);
  },
  mounted() {
    console.log("mounted");
    console.log(this.$el);
  },
});
```

![image](https://user-images.githubusercontent.com/45956169/130337606-8093cade-3cc4-419a-9fba-a83bb008de92.png)

## Transition

### リストトランジション

> 例えば、`v-for` のように同時に描画したいリストのアイテムがある場合はどうすればよいでしょう？この場合は、`<transition-group>` コンポーネントを使うことができます。

## Form

### `v-on` と `v-bind`

- `input` タグの `@input` は `input` イベントを `v-on` を用いて監視しているということ
  - https://developer.mozilla.org/ja/docs/Web/API/HTMLElement/input_event

### `v-model`

いくつか修飾子がある。例えば、`.lazy` はフォーカスが外れた時にデータをバインドするので、バリデーションに使ったりできる

- https://jp.vuejs.org/v2/guide/forms.html#%E4%BF%AE%E9%A3%BE%E5%AD%90

### フォームのイベント/オプション

| タイミング     | 送信ボタンクリック時            | リアルタイムフォーカスが外れた時   | リアルタイム (即時)                |
| -------------- | ------------------------------- | ---------------------------------- | ---------------------------------- |
| イベント       | `@click`, `@submit`, `.prevent` | `@change`, `@blur`, `v-model.lazy` | `@input`, `v-model` (`input` タグ) |
| オプション API | `methods`                       | `computed`, `watch`                | `computed`, `watch`                |

### 非同期処理と非同期通信

- Promise の正体

  - プロパティ
  - メソッド
  - 状態 (ok/ng)
  - 結果の値

- async / await

非同期通信 (Ajax) 簡易表
| タイミング | 画面表示時 | クリック時 | リアルタイム |
| --- | --- | --- | --- |
| イベント | `created`, `mounted` (`$nextTick`) | `@click`, `@submit` | `@input` |
| オプション API | `methods` | `methods` | `watch` |

## コンポーネント

### グローバルコンポーネント

お約束

- インスタンス化の前に書く
- template 内は ```
- 単一ルートが必須 (`div`タグなど)

```vue
Vue.component("my-component", { template: `
<div>aaa</div>
` }) let app = new Vue({})
```

### ローカルコンポーネント

- 変数で作成
- インスタンス内に components で追加する

```vue
let myComponent = {} let app = new Vue({ components: { 'my-component':
myComponent } })
```

### props

- html の属性のようなもの
- 基本的には親コンポーネントからの受け渡されるオブジェクトなので、子コンポーネントでは `data` に渡して使う

- props 名はケバブケース
- Type が Object か Array で default 設定を行うならば、関数で定義する

### emit

子のコンポーネント

```javascript
...
<... @click="method_in_child" ...>
...
methods: {
  method_in_child() {
    this.$emit("custom-event", value)
  }
}
...
```

親のコンポーネント

```javascript
...
<... @custom-event="method_in_parent" ...>
...
methods: {
  method_in_parent(e) {
    console.log(e)
  }
}
...
```

### eventbus

- 子 <-> 子や親 <-> 孫同士でデータ連携をするには EventBus や Vuex などを用いる

## Vuetify

### Grid

以下の grid は md 以上なら 4 つ分使用し、それ以下は 12 使うということを示している

```JavaScript
<v-col cols="12" md="4">
```

## Spacing

- `m`: margin
- `p`: padding
- `t`op/`b`ottom/`l`eft/`r`ight
- `x` (left and right)/`y` (top and bottom)/`a` (left, right, top, and bottom)

size

- 1: 4px (i.e. 5 -> 5\*4 = 20px)

ex.)

margin, top and bottom, 20px

```javascript
<div class="my-5">
```
