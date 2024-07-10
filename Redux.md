# Reduxついて
## ライブラリ Redux

- JavaScriptアプリケーションで予測可能な状態管理を行うためのライブラリ
- 主にReactと組み合わせて使用されるが、他のJavaScriptフレームワークやライブラリとも統合可能
- Reduxの設計は、**アプリケーションの状態を一貫性を持って管理し、デバッグやテストを容易にすることを目指している**

## 特徴
1. 単一の状態ツリー
- アプリケーション全体の状態を一つのJavaScriptオブジェクト（状態ツリー）として管理
    - 状態の管理と追跡が容易になる

2. 読み取り専用の状態
- Reduxの状態は読み取り専用
- 状態を変更するためには、アクションというオブジェクトをディスパッチ（送信）する必要があります。

3. 純粋なリデューサ関数
- 状態の変更は、リデューサと呼ばれる純粋関数によって行われる
    - リデューサは現在の状態とアクションを受け取り、新しい状態を返す関数

4. ミドルウェアのサポート
- Reduxはミドルウェアをサポートしており、アクションのディスパッチ時に追加のロジックを挿入することが可能
    - 非同期アクションやロギング、エラーハンドリングなどを容易に行うことが可能

5. デバッグツール
- Reduxには強力なデバッグツールがある
    - 状態の変更履歴を視覚化したり、アクションの流れを追跡したりすることが可能

> 簡単にまとめると...
>- ストア: 状態を保存する箱
>- アクション: 状態を変えたい時の「指示書」
>- リデューサ: アクションを受け取って状態をどう変えるか決める関数
>- Provider: ストアをアプリ全体に渡すためのもの



## コード例
1. Reduxのセットアップ
2. アクションの定義
3. Reducerの定義
4. ストアの作成
5. Reactコンポーネントの作成
6. アプリケーションのセットアップ

- 状態管理のためのアクション、リデューサ、ストアを定義し、Reactコンポーネントでその状態を利用
- `Provider`コンポーネントを使ってアプリケーション全体にストアを提供しています。
Reduxの基本的な機能を使ってカウンターアプリを実装

### 1. Reduxのセットアップ
```sh
$ npm install redux react-redux
```

### 2. アクションの定義
状態を変えたい時はアクションという「指示書」を使う

※ オブジェクトで定義
```js
// actions.js
export const increment = () => ({
  // カウントを増やアクション（指示）
  type: 'INCREMENT'
});

```
### 3. Reducerの定義
状態を変更するためには、アクションという「変更のリクエスト」を送る

このリクエストを受け取るのがリデューサ関数
```js
// reducers.js
const initialState = { count: 0 };

const counterReducer = (state = initialState, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    default:
      return state;
  }
};

export default counterReducer;
```
### 4. ストアの作成
```js
// store.js
import { createStore } from 'redux';
import counterReducer from './reducers';

const store = createStore(counterReducer);

export default store;

```
### 5. Reactコンポーネントの作成
```js
// Counter.js
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { increment } from './actions';

function Counter() {
  const count = useSelector(state => state.count);
  const dispatch = useDispatch();

  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => dispatch(increment())}>Increment</button>
    </div>
  );
}

export default Counter;

```


6. アプリケーションのセットアップ
```js
// App.js
import React from 'react';
import { Provider } from 'react-redux';
import store from './store';
import Counter from './Counter';

function App() {
  return (
    // Proviferコンポーネントを使ってアプリケーション全体にストアを提供
    <Provider store={store}>
      <Counter />
    </Provider>
  );
}

export default App;

```
