# Web / Electron制作 Project 共通設定

このChatGPT Projectは、1つのWebサイト / Webアプリ / Electronアプリを継続して制作・改善するために使用する。

各サイト固有の詳細仕様はこの共通設定へ書かず、対象GitHub RepositoryのCurrent Requirements / Current RepositoryをSource of Truthとして扱う。

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

## Work Queue / Current Assignment

対象RepositoryにRepository専用Work Queueが存在する場合、実装開始前に `EliteMay/web-project-data/work-queues/<owner>--<repository>/` のCurrent Queueを必要範囲で確認する。

Queueは実装計画 / assignment coordinationであり、対象RepositoryのCurrent Requirementsを上書きしない。

作業開始時の優先順:

```text
対象RepositoryのCurrent Requirements / Current Repository
↓
Work QueueのCurrent requirements revisionとの一致確認
↓
自分のWorker Lane / Current Assignment確認
↓
依存関係・Scope・Completion Criteria確認
↓
作業開始
```

Queue Itemのsource Requirements revisionがCurrent Repositoryと一致しない場合、古いTaskをそのまま実行せず`needs_reconcile`相当として扱う。

A/B/C/D等のWorker Laneは固定の仕事名ではない。前Taskの成果物・Validation・CompletionがDurableになった後、Queue / Coordinatorが正式に次Taskを割り当てた場合だけ同じLaneを次の仕事へ切り替える。

Worker自身がQueue外の次Taskを勝手に発明しない。

### Public DashboardはAssignment Authorityではない

Repository専用Dashboardに表示されるWork Queueは、Private Queueから生成したsanitize済みProjectionである。

- Dashboardの`現在の仕事` / `次の仕事`は人間向け表示として利用できる。
- `次の仕事`が`正式割当前の候補`の場合、その表示だけを根拠に作業開始しない。
- Workerが正式に作業開始する根拠はPrivate QueueのLane / Current AssignmentとCurrent Requirementsである。
- Dashboard表示とPrivate Queueが食い違う場合はPrivate Queueを再取得し、DashboardをCurrent Stateへ再publishする。
- DashboardからPrivate Task本文、Requirements revision、holder identity等を推測しない。

### Task完了時

Queue管理が有効な作業では、意味のあるTask完了時に次を確認する。

- 成果物が保存済み
- 必要Validationが保存済み
- Completion / Handoff状態が確定
- Queue Item / assignment stateをCurrent Evidenceへ合わせる
- 前TaskをHistoryとして残す
- 次のeligible Taskがある場合は正式Assignmentを確認
- 無い場合はLaneを`次の割当待ち`として扱う

Taskが終わっただけで前Taskの100%やblockerを次Taskへ引き継がない。

### 完了後の同一Lane自動切替

Current Taskが`ready_for_apply`まで到達し、成果物と必要ValidationをCurrent Evidenceから確認できた場合、**Userへ毎回「次へ進めて」「Aを更新して」と要求せず**、Current Queueから次のeligible TaskをCoordinatorが選び、最新版のQueue advance contractで同じLaneへ切り替える。

標準Flow:

```text
A: Current Task 作業完了
↓
成果物 / Validation / Handoff確認
↓
Current TaskをcompletedとしてHistory確定
↓
Current Queue / Requirements / dependency / parallel safety再確認
↓
次のeligible Taskがある
  → Aへ正式AssignmentしてCurrent Taskを切替
次のeligible Taskがない
  → Aをwaiting（次の割当待ち）へ変更
↓
sanitize済みPublic Queue Projectionを再生成
↓
Repository Dashboardへpublish
```

切替時の原則:

- Dashboardの候補表示だけから次Taskを決めない。
- `safeParallel=true`だけから意味的に安全と決めつけない。
- Current Requirements revision / Queue generation / dependency / lane assignment revisionを再確認する。
- `blocked` / `needs_reconcile`等を完了扱いして次Taskへ進めない。
- Current Taskの成果物・Validationが未確定ならLaneを上書きしない。
- 次Taskが無ければ新しいTaskをWorker自身で発明しない。
- Retryで同じ完了・切替を二重適用しない。

この「自動切替」は**Queue状態とDashboard表示を次の仕事へ進めること**を指す。新しいChatGPT会話の自動起動は別Policyであり、この処理だけでWorkerが実行開始した扱いにしない。

Authoritative QueueのTask / Lane / sync stateが変わった場合、対象RepositoryがCurrent Project Dashboard registryに登録されていれば、最新版のPublic Queue Projection contractに従ってsanitize済みProjectionも更新する。Control Branchの既存Run / Worker情報を壊さず`queue` fieldだけを同期する。

Public Dashboard publishに失敗しても、既に確定した成果物やPrivate Queue stateを巻き戻さない。DashboardをAuthorityにせず、publishだけ安全にretry / recoveryする。

Queue登録済みであっても、Workerの自動起動は別Policyとする。新しいChatへStart Promptを貼る方式なら、Dashboard / Queueに次のCurrent Assignmentを出し、Userが開始できる状態にする。

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
→ 対象Project RepositoryのCurrent Requirements

実装Task / Worker割当のcoordination
→ EliteMay/web-project-data/work-queues/<owner>--<repository>/

Public Dashboard表示
→ Private Queue / Run Stateから生成したsanitize済みProjection

実コード・データ・現行仕様
→ 対象Project Repository
```

Queueや開始プロンプトへ各サイト固有Requirements全文を複製せず、同じ情報を複数の場所へ不必要に持たない。Public DashboardもCurrent AssignmentのAuthorityとして扱わない。
