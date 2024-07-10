# React Jotaiについて
## Reactライブラリ Recoil
- Reactアプリケーションで状態管理を行うためのライブラリ
- RecoilはFacebookによって開発されており、ReactのコンテキストAPIを拡張して、複雑な状態管理をシンプルかつ効率的に行うことが可能

## 特徴
### 1. シンプルで宣言的なAPI
- 状態を定義するための`atom`、派生状態を作成するための`selector`、状態にアクセスするための`useRecoilState`や`useRecoilValue`などのフックを提供

### 2. グローバルな状態管理
- グローバルな状態管理をサポートし、Reactコンポーネント間で状態を簡単に共有することが可能

### 3. 依存関係の管理
- `Recoilのselector`を使うことで、状態の依存関係を管理
- 状態が変化した際に必要な部分だけが再計算されるようにできている

### 4. パフォーマンスの最適化
- Reactのレンダリングの特性を活かして、最小限の再レンダリングで状態を管理
    - パフォーマンスの最適化が図られる

### 5. 非同期状態のサポート
- Recoilは非同期状態もサポートしており、非同期操作の結果を状態に反映させることが可能


## コード例
1. `countState`という`atom`を定義
2. `Counter`コンポーネントでその状態を利用してカウンターを実装
3. `RecoilRoot`でラップすることで、Recoilの状態管理を利用可能になる

ボタンをクリックすると、カウントが増加する仕組み
```js
import React from 'react';
import { RecoilRoot, atom, useRecoilState } from 'recoil';

// カウンターの状態を定義
const countState = atom({
  key: 'countState', // このキーは状態の識別子
  default: 0, // 初期値
});

function Counter() {
  const [count, setCount] = useRecoilState(countState);
  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

function App() {
  return (
    <RecoilRoot>
      <Counter />
    </RecoilRoot>
  );
}

export default App;
```