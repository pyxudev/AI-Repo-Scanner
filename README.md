# AI Repo Scanner

## Overview

本アプリは GitHub 上の直近 24 時間内に更新または作成されたリポジトリを自動収集し、
AI によって生成された**可能性のある**プロジェクトを検出・収集・表示します。

## コンポーネント

- HTML/CSS
- Anthropic API
- Ollama
- GitHub Search API

```
ブラウザ (index.html 1ファイル)
  │
  ├─ GitHub Search API     ──→  直近24h のリポジトリ取得
  │
  └─ Ollama/Anthropic API  ──→  Claude が各リポジトリを分析しスコアリング
```

Anthropic API 利用の場合はサーバー不要。`index.html` をブラウザで開くだけで動作します。


# セットアップガイド

## 必要なもの

| 項目 | 必須 | 用途 |
|------|------|------|
| Ollama | ↓とどちらか必須 | リポジトリの AI 判定 |
| Anthropic API Key | ↑とどちらか必須 | リポジトリの AI 判定 |
| GitHub PAT | 任意 | レート制限の緩和 (60→5000 req/h) |

---

## STEP 1 — AI 連携設定

### Ollama を使う場合 

- Ollama のインストール

```bash
# Windows の場合
https://ollama.com/download からインストーラーをダウンロードして実行します。

# macOS / Linux の場合
curl -fsSL https://ollama.com/install.sh | sh
```

- モデルのダウンロード

```bash
# おすすめ（バランス型・JSON出力安定）
ollama pull llama3.2

# 言語処理が得意なモデル
ollama pull qwen2.5

# コード理解に特化
ollama pull qwen2.5-coder
```

- Ollama を CORS 許可つきで起動

```bash
# macOS / Linux
OLLAMA_ORIGINS="*" ollama serve

# Windows (PowerShell)
$env:OLLAMA_ORIGINS="*"; ollama serve
```

### Anthropic API の場合 — Anthropic API Key の取得

1. https://console.anthropic.com/settings/keys を開く
2. **「Create Key」** をクリック
3. 任意の名前を入力して **「Create Key」**
4. 表示された `sk-ant-api03-...` をコピー（一度しか表示されません）

> 💡 料金: Claude Sonnet の場合 input $3/MTok・output $15/MTok  
> 20件のリポジトリ分析で概ね $0.05〜$0.15 程度

---

## STEP 2 — GitHub Personal Access Token の取得（任意・推奨）

トークンなしでも動きますが、1時間60リクエストの制限があります。

1. https://github.com/settings/tokens を開く
2. **「Generate new token (classic)」** をクリック
3. スコープで **`public_repo`** にチェック
4. **「Generate token」** → 表示された `ghp_...` をコピー

---

## STEP 3 — アプリの起動

### 方法A: ダブルクリックで開く（最も簡単）

`index.html` をブラウザにドラッグ＆ドロップ、またはダブルクリック。

> ⚠️ CORS の関係で Chrome はローカルファイルに制限がかかることがあります。  
> その場合は方法 B を使ってください。

---

### 方法B: ローカルサーバーで起動（推奨）

**Python がある場合（macOS/Linux/Windows デフォルト）:**

```bash
# index.html があるディレクトリで実行
python -m http.server 8080
```

ブラウザで http://localhost:8080 を開く。

---

**Node.js がある場合:**

```bash
npx serve .
```

ブラウザで http://localhost:3000 を開く。

---

**VS Code がある場合:**

拡張機能 **Live Server** をインストール →  
`index.html` を右クリック → **「Open with Live Server」**

---

## STEP 4 — 使い方

1. ブラウザで起動すると「セットアップ」フォームが表示されます
2. **Anthropic API Key**（必須）と **GitHub PAT**（任意）を入力
3. **「スキャン開始」** をクリック
4. 直近24時間の GitHub リポジトリを20件取得・分析します
5. AI スコア 40 以上のリポジトリがカード形式で表示されます
6. カードをクリックすると詳細モーダルが開きます
7. **「再スキャン」** ボタンでいつでも再取得できます

---

## スコアの見方

| スコア | 判定 | 意味 |
|--------|------|------|
| 80〜100 | 🔴 高確度 | AI 生成の強い証拠あり |
| 60〜79  | 🟡 中確度 | 中程度の証拠あり |
| 40〜59  | 🟢 低確度 | 弱い証拠あり |
| 0〜39   | 非表示 | 人間が書いた可能性が高い |

---

## トラブルシューティング

### 「スキャン中にエラーが発生しました」が出る

- Anthropic API Key が正しいか確認してください
- コンソール（F12）でエラー詳細を確認してください
- Anthropic の残高が不足していないか確認してください

### GitHub API のレート制限エラー

- GitHub PAT を設定してください（60→5000 req/h に増加）
- すでに PAT を設定している場合は `public_repo` スコープがあるか確認

### CORS エラーが出る

- ローカルサーバー（`python -m http.server 8080`）で起動してください
- `file://` プロトコルでは一部ブラウザで CORS 制限がかかります

---

## Vercel へのデプロイ（公開する場合）

```bash
# Vercel CLI をインストール
npm install -g vercel

# デプロイ
vercel deploy
```

> ⚠️ Anthropic API Key をブラウザに直接入力する構成のため、  
> 公開サーバーにデプロイする場合は API Key をサーバーサイドで管理することを推奨します。

---

## ファイル構成

```
ai-repo-scanner/
└── index.html   ← アプリ本体（これ1ファイルのみ）
```

依存ライブラリは CDN から読み込むため、追加インストール不要です。
