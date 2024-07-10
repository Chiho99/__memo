# React Jotaiについて
## Reactライブラリ Jotai
- Reactアプリケーションで状態管理をシンプルかつ効率的に行うためのライブラリ
- 「Jotai」という名前は、日本語の「一粒」から由来しており、一つ一つの状態（atom）を扱うことができるという意味を持つ

## 特徴
### 1. シンプルなAPI
- Jotaiは、非常にシンプルなAPIを提供し、状態の定義と利用が簡単
- 状態を定義するための`atom`関数と、状態を取得・更新するためのフック`useAtom`が主な構成要素

### 2. グローバルな状態管理
- ReactのコンテキストAPIを使ってグローバルな状態管理を行うことが可能
    - どのコンポーネントからでも状態にアクセスすることが可能です。

### 3. 軽量で高速
- 非常に軽量であり、依存関係も少ないため、パフォーマンスが良好
- 必要な部分のみを更新することで、高速な状態管理が可能

### 4. 再レンダリングの最小化
- 必要な部分だけが再レンダリングされるため、効率的に状態管理を行うことが可能
    - パフォーマンスの最適化が図られている

### 5. Reactのフックとシームレスな統合
- JotaiはReactのフックと統合されているため、既存のReactコードに簡単に組み込むことが可能

## コード例
1. countAtomという状態を定義
2. Counterコンポーネントでその状態を利用してカウンターを実装

ボタンをクリックすると、カウントが増加する仕組み
```js
import React from 'react';
import { atom, useAtom } from 'jotai';

// カウンターの状態を定義
const countAtom = atom(0);

function Counter() {
  const [count, setCount] = useAtom(countAtom);
  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default Counter;

```