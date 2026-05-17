# Journal App — Claude Code 引き継ぎ

## プロジェクト概要
個人向けAI日記アプリ。非エンジニアがClaudeとの対話のみで設計・開発。

## 技術構成
- **単一ファイル**: `index.html`（React + Babel CDN、インストール不要）
- **環境自動判定**: `IS_CLAUDE`フラグ（`window.storage`の有無で判定）
  - Claude artifact内 → `window.storage`
  - ローカル → File System Access API / localStorage
- **AIモデル**: Claude / Gemini 2.5 Flash / GPT-4o（切り替え可能）

## 実装済み機能
- チャット（ルーティンチップ + 感情アラートセンサー）
- カレンダー・ログ・タグ検索
- 週次/月次分析（AIによるパターン抽出）
- インポート: Claude JSON / ChatGPT JSON / Gemini HTML（マイアクティビティ）
- エクスポート: JSON / Markdown / テキスト
- Markdown自動同期（ローカル保存時、Obsidian連携）
- バイアス分析（感情語検出時に自動実行）
- PWA対応（manifest.json + sw.js）

## データ構造（session オブジェクト）
```json
{
  "id": "s_xxx",
  "date": "ISO8601",
  "title": "15文字以内",
  "summary": "80文字以内",
  "tags": ["タグ1", "タグ2"],
  "insights": ["気づき1"],
  "bias": {
    "trigger": "不快感のトリガー",
    "raw_reaction": "野生の反応",
    "value_exposed": "露わになった価値観",
    "bias_pattern": "思考の癖",
    "debug_question": "掘り下げる問い"
  },
  "messages": [{"role": "user|assistant", "content": "..."}],
  "source": "Journal|Claude|ChatGPT|Gemini|Review",
  "model": "claude|gemini|gpt"
}
```

## 既知の課題・今後の実装候補
- 感情タグの時系列可視化（分析タブの拡張）
- 記録が50件超えたらメタデータ拡張（category, reuseLevel等）
- 月次レポートの強化

## ファイル構成
```
journal-app/
  ├ index.html   ← 全機能が入った単一ファイル
  ├ manifest.json
  └ sw.js
```

## Claude Codeへの指示
`index.html` を開いて続きの開発をお願いします。
コードは1ファイル完結のReact（Babel CDN）です。
