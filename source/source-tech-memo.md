# Actionsデモ②: 技術メモからのナレッジ抽出

## 実行方法（3つのいずれか）

### 方法A: GitHub Web UI（非エンジニア向け）
1. https://github.com/kadota05/team-knowledge にアクセス
2. `source/` フォルダを開く
3. 「Add file」→「Create new file」
4. ファイル名を `tech-memo-api-design.md` にする
5. 下の「投入ファイル」の内容を貼り付け
6. 「Commit changes」をクリック

### 方法B: gh CLI（ターミナルから）
```bash
gh api repos/kadota05/team-knowledge/contents/source/tech-memo-api-design.md \
  -X PUT \
  -f message="add: API設計ガイドライン" \
  -f content="$(base64 < 投入ファイルのパス)"
```

### 方法C: git clone（開発者向け）
```bash
cd team-knowledge
# source/にファイルを作成
git add source/tech-memo-api-design.md
git commit -m "add: API設計ガイドライン"
git push
```

## 投入ファイル

```markdown
# API設計ガイドライン（佐藤メモ）

最近のプロジェクトで学んだAPI設計のベストプラクティスをまとめる。

## エンドポイント命名
- リソース名は複数形: /users, /posts, /comments
- ネストは2階層まで: /users/:id/posts はOK、/users/:id/posts/:id/comments はNG
- アクションが必要な場合は動詞を使う: /users/:id/activate

## レスポンス形式
- 必ず統一したエンベロープを使う:
  { "data": ..., "meta": { "page": 1, "total": 100 } }
- エラー時:
  { "error": { "code": "NOT_FOUND", "message": "..." } }
- 日時はISO 8601形式（UTC）

## バージョニング
- URLにバージョンを含める: /api/v1/users
- 破壊的変更はメジャーバージョンアップ
- 非推奨APIは最低3ヶ月間の猶予期間を設ける

## 認証
- Bearer tokenを使用
- トークンの有効期限は1時間
- リフレッシュトークンは30日
```
