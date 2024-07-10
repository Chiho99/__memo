# SWRついて
## Reactライブラリ SWR

- Next.jsの開発元であるVercelが開発したReact用のデータフェッチングライブラリ
- `stale-while-revalidate（古いデータを使いつつ、新しいデータを再フェッチする）`の略
- データのキャッシング、リフェッチング、リアルタイム更新などを簡単に実現できる

## 特徴
1. 簡単なデータフェッチ
- SWRは、簡単にデータをフェッチしてReactコンポーネントで利用することが可能
- 内部的にはfetch関数を使っているが、他のHTTPクライアントとも統合可能

2. キャッシング
- SWRはデータをキャッシュして、同じデータを再度フェッチする際に無駄なリクエストを減らす

3. リアルタイム更新
- データがバックグラウンドで自動的に更新されるため、常に最新のデータを表示可能

4. エラー処理
- データフェッチ中のエラー処理が簡単に行える

5. リファクタリングのサポート
- シンプルなAPIを持ち、コードのリファクタリングが容易


## コード例
1. インストール
2. データフェッチの実装

### 1. インストール
```sh
$ npm install swr
```
### 2. データフェッチの実装

- `fetcher`関数
    - 指定されたURLからデータを取得し、JSON形式で返す関数
- `useSWR`フック
    - データのフェッチを行うために利用
        - `useSWR('エンドポイントのURL',fetcher関数)`
- 状態のハンドリング
    - `useSWR`は`data`と`error`を返す
        - `data`がまだ取得できていない場合はローディング状態を表示
        - エラーが発生した場合はエラーメッセージを表示

```js
import useSWR from 'swr';

// フェッチャー関数
const fetcher = (url) => fetch(url).then((res) => res.json());

function Profile() {
  const { data, error } = useSWR('/api/user', fetcher);

  if (error) return <div>Failed to load</div>;
  if (!data) return <div>Loading...</div>;

  return (
    <div>
      <h1>{data.name}</h1>
      <p>{data.email}</p>
    </div>
  );
}

export default Profile;
```

## SWRの便利な機能
### リアルタイム更新
データをリアルタイムで更新するための機能も持つ

以下はポーリングを使ったリアルタイム更新の例
```js
const { data, error } = useSWR('/api/user', fetcher, {
  refreshInterval: 1000, // 1秒ごとにデータを再フェッチ
});
```
### キャッシングと再利用
データをキャッシュして、同じデータを必要とする他のコンポーネントでも再利用
```js
import useSWR from 'swr';

const fetcher = (url) => fetch(url).then((res) => res.json());

function Profile() {
  const { data, error } = useSWR('/api/user', fetcher);
  // 同じURLを使った別のSWRフック
  const { data: data2 } = useSWR('/api/user', fetcher);

  // dataとdata2は同じキャッシュを参照する
  if (error) return <div>Failed to load</div>;
  if (!data) return <div>Loading...</div>;

  return (
    <div>
      <h1>{data.name}</h1>
      <p>{data.email}</p>
    </div>
  );
}

export default Profile;
```