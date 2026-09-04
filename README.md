# Web Project Workflow

ChatGPTで新しいWebサイト / Webアプリ / Electronアプリを企画し、各専用Projectへ安全に引き継ぐための**Project運用ルールのSource of Truth**です。

このRepositoryはWeb制作そのものの設計・品質ルールを管理しません。制作ルールの正本は [`EliteMay/web-project-guide`](https://github.com/EliteMay/web-project-guide) です。

## 役割分担

```text
web-project-workflow
= ChatGPT Projectの役割 / 要件定義から制作Projectへの引き継ぎ方法

web-project-guide
= Web / Electron制作の共通ルール / 品質基準 / 判断基準

各Project Repository
= サイト固有の要件 / 仕様 / コード / データ / Test / 履歴
```

同じルールやサイト固有情報を複数の場所へ全文複製しません。

## ファイル

- [`REQUIREMENTS_PROJECT.md`](REQUIREMENTS_PROJECT.md) — 共通の「Web制作・要件定義」ChatGPT Project設定
- [`DEVELOPMENT_PROJECT.md`](DEVELOPMENT_PROJECT.md) — 各サイト専用ChatGPT Projectで共通利用する設定
- [`START_PROMPT_TEMPLATE.md`](START_PROMPT_TEMPLATE.md) — 要件定義完了後に新しい制作Projectへ渡す開始プロンプトのTemplate

## 基本フロー

```text
Web制作・要件定義 Project
↓
サイト内容を相談
↓
サイト名 / Repository名 / 要件を確定
↓
START_PROMPT_TEMPLATE.mdを基に開始プロンプトを作成
↓
Repository名と同名のChatGPT Projectを作成
↓
そのProjectではDEVELOPMENT_PROJECT.mdを共通設定として利用
↓
実装 / UI改善 / 不具合修正 / 保守
```

## 名前の基本

特別な理由がなければ次を基本とします。

- 表示名: サイト・アプリに適した名前
- GitHub Repository: 英小文字 + `-` 区切りの短く分かりやすい名前
- ChatGPT Project: GitHub Repository名と同じ

例:

```text
Site: Home Workout Guide
Repository: home-workout-guide
ChatGPT Project: home-workout-guide
```

## このRepositoryへ置かないもの

- Web制作の詳細ルール
- 各サイト固有の機能仕様
- 各サイト固有の保存Schema
- 各サイト固有のTest / Release Contract
- 各サイトの長期的な要件本文

それぞれ `web-project-guide` または対象Project Repositoryを正本とします。
