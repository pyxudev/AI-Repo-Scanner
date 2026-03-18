# 🚀 AI Repo Scanner

<p align="center">
  <b>Scan recent GitHub repositories and detect AI-generated projects</b><br>
  <i>GitHubの最新リポジトリを収集し、AI生成の可能性を判定</i><br>
  <i>自动扫描 GitHub 最新仓库并检测 AI 生成项目</i>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Frontend-HTML%2FCSS-blue">
  <img src="https://img.shields.io/badge/AI-Claude%20%7C%20Ollama-purple">
  <img src="https://img.shields.io/badge/API-GitHub-green">
  <img src="https://img.shields.io/badge/License-MIT-lightgrey">
</p>

---

## 📖 Overview / 概要 / 概述

- 🇯🇵 GitHub上の直近24時間のリポジトリを収集し、AI生成の可能性を分析  
- 🇺🇸 Collects repositories from the last 24 hours and detects AI-generated projects  
- 🇨🇳 收集最近24小时的GitHub仓库并检测AI生成项目  

---

## 🧩 Architecture / 構成 / 架构

```
Browser (index.html)
  │
  ├─ GitHub Search API → Fetch repositories
  │
  └─ AI (Claude / Ollama) → Analyze & score
```

- 🇯🇵 サーバーレスで動作可能  
- 🇺🇸 Runs fully serverless (Anthropic API)  
- 🇨🇳 支持无服务器运行  

---

## ⚙️ Setup / セットアップ / 安装

### Requirements

| Item | JP | EN | CN |
|------|----|----|----|
| Ollama | AI判定 | AI analysis | AI判断 |
| Anthropic API Key | AI判定 | AI analysis | AI判断 |
| GitHub PAT | レート制限緩和 | Rate limit | 提高限额 |

---

## ▶️ Run / 起動 / 启动

### Option A

- 🇯🇵 index.html を開く  
- 🇺🇸 Open index.html  
- 🇨🇳 打开 index.html  

### Option B (Recommended)

```bash
python -m http.server 8080
```

---

## 🧠 Usage / 使い方 / 使用方法

1. 🇯🇵 APIキー入力 / 🇺🇸 Enter API key / 🇨🇳 输入 API Key  
2. 🇯🇵 スキャン開始 / 🇺🇸 Start scan / 🇨🇳 开始扫描  
3. 🇯🇵 結果表示 / 🇺🇸 View results / 🇨🇳 查看结果  

---

## 📊 Scoring / スコア / 评分

| Score | JP | EN | CN |
|------|----|----|----|
| 80–100 | 高確度 | High | 高概率 |
| 60–79 | 中確度 | Medium | 中等 |
| 40–59 | 低確度 | Low | 低 |

---

## ⚠️ Notes / 注意 / 注意事项

- 🇯🇵 APIキーは公開しないこと  
- 🇺🇸 Do NOT expose API keys  
- 🇨🇳 不要暴露 API Key  

---

## ☁️ Deploy / デプロイ / 部署

```bash
npm install -g vercel
vercel deploy
```

---

## 📁 Structure / 構成 / 结构

```
ai-repo-scanner/
└── index.html
```

---

## ⭐ Features

- 🔍 GitHub 最新リポジトリ取得 / Fetch latest repos / 获取最新仓库  
- 🤖 AIスコアリング / AI scoring / AI评分  
- ⚡ サーバーレス / Serverless / 无服务器  

---

<p align="center">
  Made with ❤️ using Claude & Ollama
</p>
