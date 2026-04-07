# Actionsデモ①: 会議議事録からのナレッジ抽出

## 実行方法（3つのいずれか）

### 方法A: GitHub Web UI（非エンジニア向け）
1. https://github.com/kadota05/team-knowledge にアクセス
2. `source/` フォルダを開く
3. 「Add file」→「Create new file」
4. ファイル名を `meeting-notes-20260407.md` にする
5. 下の「投入ファイル」の内容を貼り付け
6. 「Commit changes」をクリック

### 方法B: gh CLI（ターミナルから）
```bash
gh api repos/kadota05/team-knowledge/contents/source/meeting-notes-20260407.md \
  -X PUT \
  -f message="add: 技術定例議事録 2026/04/07" \
  -f content="$(base64 < 投入ファイルのパス)"
```

### 方法C: git clone（開発者向け）
```bash
git clone https://github.com/kadota05/team-knowledge.git
cd team-knowledge
# source/にファイルを作成
git add source/meeting-notes-20260407.md
git commit -m "add: 技術定例議事録 2026/04/07"
git push
```

## 投入ファイル

```markdown
# 技術定例 2026/04/07 議事録

## 参加者
田中、鈴木、佐藤、山田

## 決定事項

### デプロイフロー変更
- 今後すべてのデプロイはステージング環境での確認を必須とする
- ステージングでの確認は最低30分間行うこと
- 本番デプロイは毎週火曜・木曜の14:00-16:00のみ
- 緊急デプロイはCTOの承認があれば時間外も可

### コードレビュー規約
- PRは作成後24時間以内にレビューすること
- approveは最低2名必要
- 500行を超えるPRは分割を推奨

### セキュリティ
- APIキーは必ずSecrets Managerを使用する
- .envファイルは絶対にコミットしない
- 新しいAPIエンドポイントには必ず認証を入れること

## TODO
- 田中: ステージング環境のモニタリングダッシュボード作成
- 鈴木: CIにデプロイ時間チェックを追加
```
