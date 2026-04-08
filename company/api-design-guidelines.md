REST APIの設計に関するベストプラクティスをまとめたガイドライン。

## エンドポイント命名

- リソース名は複数形: `/users`, `/posts`, `/comments`
- ネストは2階層まで: `/users/:id/posts` はOK、`/users/:id/posts/:id/comments` はNG
- アクションが必要な場合は動詞を使う: `/users/:id/activate`

## レスポンス形式

- 必ず統一したエンベロープを使う:
  ```json
  { "data": ..., "meta": { "page": 1, "total": 100 } }
  ```
- エラー時:
  ```json
  { "error": { "code": "NOT_FOUND", "message": "..." } }
  ```
- 日時はISO 8601形式（UTC）

## バージョニング

- URLにバージョンを含める: `/api/v1/users`
- 破壊的変更はメジャーバージョンアップ
- 非推奨APIは最低3ヶ月間の猶予期間を設ける

## 認証

- Bearer tokenを使用
- トークンの有効期限は1時間
- リフレッシュトークンは30日
