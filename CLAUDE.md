# CLAUDE.md — Task Board Project

## プロジェクト概要

SAMURAI SPRINT用のタスクボードアプリケーション。

## 開発スタイル

- コードはシンプルに保つ。不要な抽象化・将来の要件への先回り実装はしない。
- コメントは「なぜそうしているか」が非自明な場合のみ記述する。説明的なコメントは書かない。
- UI変更を加えた場合は、ブラウザで動作確認してから完了とする。

## Git 運用ルール

**コードを変更するたびに、必ずGitHubへプッシュすること。**

具体的な手順：

1. 変更をステージングする
   ```
   git add <変更ファイル>
   ```

2. コミットメッセージは変更の「なぜ」を簡潔に記述する（1〜2文）
   ```
   git commit -m "コミットメッセージ"
   ```

3. **毎回プッシュする**
   ```
   git push origin <ブランチ名>
   ```

### ブランチ戦略

- `main` — 本番相当の安定ブランチ。直接コミットしない。
- `develop` — 開発の統合ブランチ。
- `feature/<機能名>` — 機能単位の作業ブランチ。

### コミットの注意事項

- `.env` や認証情報を含むファイルは絶対にコミットしない。
- `--no-verify` や `--force` は原則使用禁止。必要な場合はユーザーに確認を取る。
- `main` へのforce pushは絶対に行わない。

## デプロイ先

| 種別 | URL |
|------|-----|
| GitHub リポジトリ | https://github.com/kirohi-boy/task-board |
| GitHub Pages (本番) | https://kirohi-boy.github.io/task-board/ |

`main` ブランチへのプッシュで GitHub Actions が自動ビルド・デプロイする。

## 技術スタック

| 役割 | 技術 |
|------|------|
| UI ライブラリ | React 18 |
| ビルドツール | Vite 5 |
| 言語 | JavaScript (JSX) |
| スタイリング | CSS Modules なし / グローバル CSS |
| 状態管理 | React useState（外部ライブラリなし） |
| 永続化 | localStorage |
| デプロイ | GitHub Actions + GitHub Pages |

## コンポーネント命名規約

- ファイル名・コンポーネント名はともに **PascalCase**（例: `App.jsx`、`TaskItem.jsx`）
- 1ファイル1コンポーネントを原則とする
- CSSファイルはコンポーネントと同名にする（例: `App.jsx` → `App.css`）
- イベントハンドラは `handle` プレフィックス（例: `handleKeyDown`、`handleSubmit`）
- state の setter は `set` プレフィックス（例: `setTasks`、`setInput`）

## ファイル構成

```
task-board/
├── CLAUDE.md
├── index.html
├── package.json
├── package-lock.json
├── vite.config.js
├── .gitignore
├── .github/
│   └── workflows/
│       └── deploy.yml      # GitHub Pages 自動デプロイ
└── src/
    ├── main.jsx            # エントリーポイント
    ├── index.css           # グローバルスタイル
    ├── App.jsx             # タスクボード本体
    └── App.css             # App コンポーネントのスタイル
```

## その他のルール

- 破壊的操作（ファイル削除、ブランチ削除、DBリセットなど）の前は必ずユーザーに確認する。
- 外部サービスへのデータ送信・公開操作の前も確認を取る。
