# 新規制作Project 開始プロンプト Template

このTemplateは、要件定義完了後に新しいChatGPT制作Projectの最初の会話へ貼る開始プロンプトを作るために使用する。

共通制作ルールはここへ全文複製しない。制作Projectでは `EliteMay/web-project-workflow` の `DEVELOPMENT_PROJECT.md` と `EliteMay/web-project-guide` の最新版を参照する。

---

# {SITE_NAME} 制作開始

## 基本情報

サイト / アプリ名：
`{SITE_NAME}`

GitHub Repository：
`EliteMay/{REPOSITORY_NAME}`

ChatGPT Project：
`{REPOSITORY_NAME}`

## Project概要

{このサイト / アプリが何をするものか}

## 目的

{何のために作るか}

## 想定利用者

{誰が使うか。必要な場合のみ}

## 確定要件

詳細なCurrent Requirementsは対象RepositoryをSource of Truthとする。

- {要件1}
- {要件2}
- {要件3}

## 主な機能

- {主要機能1}
- {主要機能2}
- {主要機能3}

## 重要仕様 / 崩してはいけないこと

- {重要仕様1}
- {重要仕様2}

## 禁止事項

- {避ける仕様・実装1}
- {必要な場合のみ追加}

## MVP

最初に完成させる範囲：

- {MVP1}
- {MVP2}

## 将来候補

- {MVP後に追加可能な機能1}
- {必要な場合のみ追加}

## 完成条件

- {完成条件1}
- {完成条件2}
- {完成条件3}

## 未確定事項

- {実装段階で判断してよい内容、または残っている未確定事項}

未確定事項がなければ「特になし」とする。

## Work Queue

要件定義完了時にRepository専用Queueが作成済みなら、次を確認する。

`EliteMay/web-project-data/work-queues/EliteMay--{REPOSITORY_NAME}/`

Queueは実装Task / Worker Assignmentのcoordinationであり、要件のSource of Truthではない。

制作開始時は:

1. 対象RepositoryのCurrent Requirementsを読む
2. Queueが指すRequirements revisionとの一致を確認する
3. Current Assignmentがある場合はそのTaskのScope / Dependencies / Completion Criteriaを読む
4. staleなAssignmentなら勝手に実行せずreconcileする

開始プロンプト本文をCurrent Assignmentの代わりにしない。

## 制作開始時

このChatGPT Projectでは、GitHub Repository `EliteMay/web-project-workflow` の最新 `DEVELOPMENT_PROJECT.md` を共通Project設定の正本として扱う。

Web / Electron制作ルールは `EliteMay/web-project-guide` の最新版をSource of Truthとする。

制作開始時に必要な最新ルールを確認し、対象Repositoryが既に存在する場合は現在のGitHub上の状態を確認してから作業する。

Repository専用Work Queueが存在する場合はCurrent Assignmentも確認する。

古い会話、古いZIP、以前確認したルール、古いStart Promptだけを現在状態として扱わない。
