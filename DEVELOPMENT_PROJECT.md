# Web / Electron制作 Project 共通設定

このChatGPT Projectは、1つのWebサイト / Webアプリ / Electronアプリを継続して制作・改善するために使用する。

各サイト固有の詳細仕様はこの共通設定へ書かず、開始プロンプトと対象GitHub RepositoryをSource of Truthとして扱う。

## 作業開始時

Web / Electron制作に関係する作業では、最初にGitHub Repository `EliteMay/web-project-guide` の最新版を確認する。

まず `README.md` と `START_HERE.md` を確認し、今回の作業種類に必要なドキュメントだけ読む。

過去の会話や以前確認したGuideを最新版として扱わない。

制作ルール、品質基準、GitHub運用、UI / UX、保存、性能、Security、Testing、Electron、完成条件などの詳細はこのファイルへ複製せず、最新版の `web-project-guide` をSource of Truthとする。

## 対象Repository

1つのChatGPT Projectには、原則として1つのGitHub Repositoryだけを対応させる。

対象Repositoryは、開始プロンプトまたはProject内の既存情報から特定する。

既存Repositoryを変更する場合は、古い会話・古いZIP・記憶だけを基準にせず、現在のGitHub上の状態を確認する。

必要に応じて、README、仕様書、Project Rules、Project Learnings、Work Report、コード、データ、Tests、Deployment設定など、今回の変更に関係するものだけ確認する。

確認できていない内容や実行結果を、確認済みとして扱わない。

## GitHub中心

ChatGPTからGitHubを直接扱える作業では、可能な限りGitHub上の現在状態を確認し、そのまま安全に作業する。

単純なHTML / CSS / JavaScript / JSON等の作成・修正で、毎回ZIPやCodexを前提にしない。

まずChatGPTで可能な調査、相談、設計、GitHub確認、ファイル作成・修正、コード修正、データ修正、文書更新、確認を行う。

ChatGPTだけでは十分に検証できない項目が残る場合のみ、Codexまたはユーザー側で確認する項目を具体的に示す。

Codexを固定担当として扱わない。

## 仕様と変更

現在の要件、Repository内の仕様、実装、README等と新しいユーザー指示が衝突する場合は、重要な矛盾を示す。

現在の明確なユーザー指示を優先するが、データ互換性、崩してはいけない仕様、主要機能削除、大きな仕様変更などへ影響する場合は勝手に破壊的変更を確定しない。

仕様変更が確定した場合は、必要な関連文書も現行実装と一致させる。

## UI / 見た目

UI変更も最新版の `web-project-guide` に従う。

意味のある見た目変更では、現在UI、ユーザーフィードバック、必要なDomain Researchを確認してから変更する。

過去に成功した別サイトのデザインを、そのまま最初の正解として適用しない。

## 会話の分離

同じChatGPT Project内でも、作業目的が大きく違う場合は会話を分ける。

基本名:

- `Repository名（実装）`
- `Repository名（UI・見た目）`
- `Repository名（不具合・改善）`
- `Repository名（相談・調査）`

必要な場合のみ:

- `Repository名（データ・コンテンツ）`
- `Repository名（GitHub・公開）`

同じ目的の作業なら、無理に新しい会話を増やさない。

## 公開URL

GitHub Pages等で公開しているWebサイトでは、公開状態を確認できる場合、作業完了時に実際の公開URLを提示する。

確認できていないURLを推測で「公開済み」として扱わない。

## 完成判定

「コードを書いた」「Commitした」だけで完成扱いにしない。

完成条件、Testing、Validation、Documentation更新、最終状態確認は最新版の `web-project-guide` に従う。

ChatGPTから確認できない実機・OS依存項目が残る場合は、未確認事項として明記する。

## Source of Truth

```text
Web制作の共通ルール
→ EliteMay/web-project-guide

ChatGPT制作Projectの共通運用
→ このDEVELOPMENT_PROJECT.md

今回のサイト固有要件
→ 開始プロンプト / 対象Project Repository

実コード・データ・現行仕様
→ 対象Project Repository
```

共通設定へ各サイト固有仕様を増やさず、同じ情報を複数の場所へ不必要に複製しない。
