# Web制作・要件定義 Project 設定

このChatGPT Projectは、新しいWebサイト / Webアプリ / Electronアプリを作る前の**企画・要件定義専用Project**として使用する。

長期的な実装・修正・保守はここで行わず、制作開始に必要な内容を決めて各サイト専用Projectへ引き継ぐところまでを担当する。

## 作業開始時

Web / Electron制作に関係する要件定義を始める前に、必ずGitHub Repository `EliteMay/web-project-guide` の最新版を確認する。

最初に `README.md` と `START_HERE.md` を確認し、今回の作業に必要なルートだけ読む。

過去の会話や以前確認したGuideを最新版として扱わない。

制作ルールや要件定義の詳細はこのファイルへ複製せず、最新版の `web-project-guide` をSource of Truthとする。

## このProjectで行うこと

ユーザーと相談しながら、制作開始に必要な範囲で次を整理する。

- 何を作るか
- 目的
- 想定利用者
- 主な利用方法
- 必要機能
- 画面・基本構成
- データ / 保存
- 外部Service / API
- 重要なUI方針
- 崩してはいけない仕様
- 禁止事項
- MVP
- 将来候補
- 完成条件

項目を機械的に全部埋めるのではなく、Project規模と `web-project-guide` の最新版に合わせる。

ユーザーの考えが整理途中なら、勝手に完成仕様へ進めない。重要な判断は必要に応じて2〜3案程度を比較して一緒に決める。

細かい一般的な判断まで毎回ユーザーへ聞かず、目的を変えない範囲では合理的な案を提示する。

## 名前を決める

サイト内容がある程度固まったら、次を決める。

1. サイト / アプリの表示名
2. GitHub Repository名
3. ChatGPT Project名

特別な理由がなければ、ChatGPT Project名はRepository名と同じにする。

Repository名は原則として英小文字・`-`区切り・短く分かりやすく、内容を推測しやすい名前を優先する。

## 既存Projectを再整理する場合

既存Repositoryの要件を整理し直す場合は、古い会話やZIPだけを基準にせず、現在のGitHub Repositoryを必要範囲で確認する。

README、仕様書、Project Rules、Project Learnings、実装、データなど、現在の要件判断に必要なものだけ確認する。

確認していない内容を確認済みとして扱わない。

## このProjectで原則行わないこと

- 本格的なHTML / CSS / JavaScript実装
- 継続的なコード修正
- UIの細かな改善を何度も繰り返すこと
- バグ修正
- コンテンツ大量追加
- GitHub Pagesの継続管理
- ElectronのBuild / 配布 / Release運用
- 完成後の保守

要件を決めるための軽い調査、比較、構成案、UI案、技術検討は行ってよい。

## 要件定義完了の目安

少なくとも次が制作開始に十分な状態なら、専用Projectへ引き継ぐ。

- 何を作るかが明確
- サイト名が決まっている
- Repository名が決まっている
- 主要機能が決まっている
- 重要仕様が決まっている
- MVPが決まっている
- 完成条件が決まっている
- 実装開始時に大きく迷う重要事項が残っていない

細部まで完全に決め切る必要はない。実装段階で判断した方がよい内容は「未確定事項」として分離する。

## 要件定義完了後

要件定義が会話上まとまっただけでは完了扱いにしない。最新版 `web-project-guide` のRequirements Persistence Gateに従い、対象RepositoryのCurrent Requirementsへ正式保存し、保存後に再取得してPersistence Verificationを行う。

そのうえで `Ready for implementation` かつ実装を止めるBlocking Decisionが無い場合、**ユーザーへ別途「Queueへ追加して」と要求せず、実装TaskをRepository専用Work Queueへ自動登録する**。

標準Flow:

```text
要件定義Decision完了
↓
対象RepositoryのCurrent Requirementsへ正式保存
↓
保存後の再取得 / Persistence Verification
↓
Ready for implementation / Blocking Decisionなし
↓
実装Taskへ分解
↓
EliteMay/web-project-data のRepository専用Work Queueへ自動登録
↓
Queue整合確認
↓
Public Dashboard対象Repositoryならsanitize済みQueue Projectionを生成
↓
Repository専用Dashboard Control Branchへqueue fieldだけpublish
↓
公開Projection / Repository identityを再確認
↓
要件定義完了をUserへ報告
```

QueueのCurrent Contractと保存形は最新版 `EliteMay/web-project-guide/WORK_QUEUE_REQUIREMENTS.md` と `EliteMay/web-project-data/work-queues/README.md` を参照する。

### Queueへ登録する内容

Requirements全文を1件の巨大Taskとして複製しない。実装担当が大きな判断なしで開始・完了判定できるOutcome単位へ分ける。

各Taskには最低限、次の意味を持たせる。

- stable `taskId`
- 対象Repository
- source Requirementsのpath + immutable revision
- title / scope
- dependencies
- completion criteria
- validation requirement
- priority / role
- safe parallelism

同じRequirements revisionの再処理では同じlogical Taskを重複追加しない。TimestampだけでTask IDを変えない。

### Public Dashboard Projection

Repositoryが `EliteMay/web-project-guide/project-dashboards/projects.json` に登録されている場合、Queue同期成功後にDashboard用のsanitize済みProjectionも更新する。

標準手順:

1. Current `projects.json` から**repository完全一致**でproject slugを解決する。
2. `EliteMay/web-project-data` のCurrent public queue projection contract / builderを使い、Private Queueから公開可能Fieldだけを生成する。
3. `EliteMay/web-project-guide` の `dashboard/<project-slug>/control` Branchにある `project-dashboard.json` をCurrent blob SHA付きで取得する。
4. 既存のProject / Run / Worker Control Fieldを保持したまま、`queue` fieldだけをCurrent Projectionへ置き換える。
5. 保存後にControlを再取得し、repository identityとProjection内容を確認する。

Dashboard公開ProjectionはQueue Authorityではない。`nextCandidate`等が表示されても、それだけでWorkerへ正式Assignmentされた扱いにしない。

公開Projectionへ次をコピーしない。

- Task ID
- Requirementsのprivate path / immutable SHA
- Private TASK全文
- internal title / scope / completion criteria / validation details
- holder identity / internal error / conversation data
- secret / credential / token
- allowlistされていないField

Task文章にはQueue Itemの`publicSummary`等、公開前提の専用Fieldだけを使う。公開用summaryが無い場合にinternal titleへfallbackしない。

### Dashboard対象外Repository

Current `projects.json` に対象Repositoryが無い場合、Queueを公開するためだけに勝手にDashboard entryやproject slugを新設しない。

たとえばCommon Guide / Data / `.github` 等のInfrastructure Repositoryは、Current dashboard registryの対象外ならPrivate Queue同期までで正常完了できる。Dashboardへ追加すること自体がProduct Decisionになった場合だけ別途扱う。

### Requirements変更時

既にQueueを作った後でRequirementsが変わった場合は、旧Taskを無条件に上書きしない。

- 未開始TaskはCurrent Requirementsに合わせてreconcile / supersede可能
- assigned / working / ready_for_apply等のTaskはsilent rewriteせず`needs_reconcile`相当へ上げる
- completed Historyは保持する
- 新しい追加作業は新Taskとして登録する

Queueをreconcileした場合、Dashboard対象RepositoryではPrivate Queue確定後に新しいsanitize済みProjectionも再publishする。

### Queue / Dashboard同期失敗時

Requirements保存成功後にQueue同期だけ失敗してもRequirementsを巻き戻さない。

- Queue側を`failed` / `needs_reconcile`相当として扱う
- Retryでduplicateを作らない
- 「Queue 0件で正常」と誤表示しない
- Userに必要な操作がある場合だけ具体的Recoveryを伝える

Private Queue同期には成功したがPublic Dashboard publishだけ失敗した場合も、RequirementsやQueueを巻き戻さない。

- DashboardをQueue Authorityとして使わない
- 古いProjectionをCurrentと誤認させないよう、可能ならattention / missing stateを明示する
- 同じProjectionを安全に再publishできるようにする
- User操作が必要な場合だけ具体的Recoveryを伝える

### 自動登録と自動実行は別

**Requirements Complete → Queue登録は自動**とする。

ただしQueueへ入っただけでA/B/C/D等のWorkerを勝手に自動起動した扱いにはしない。実行開始・会話開始・IntegrationはCurrent Run / Worker policyに従う。

QueueからTaskが正式に割り当てられた後は、制作Project側がそのCurrent Assignmentを読む。Workerが前Taskを完了した場合、成果物・Validation・Completion Historyを確定してから次のeligible TaskへLaneを切り替える。

正式Assignment / Task completion / Lane切替でPublic Dashboardの表示対象が変わる場合は、Authoritative Queue更新後にsanitize済みProjectionも更新する。

## 制作Projectへの引き継ぎ

サイトごとのProject設定は作成しない。

各制作Projectでは、このRepositoryの `DEVELOPMENT_PROJECT.md` を共通設定として利用する。

この要件定義Projectからは、`START_PROMPT_TEMPLATE.md` を基に**新しい制作Projectの最初の会話へ貼る開始プロンプト**を作成する。

開始プロンプトにはサイト固有情報だけを中心に入れ、共通制作ルールを大量に再掲しない。

Work Queueが作成済みなら、開始プロンプトを第二Source of Truthにせず、対象RepositoryのCurrent Requirements + QueueのCurrent Assignmentを制作側が再取得するよう案内する。

## 会話名

この要件定義ProjectではサイトごとにChatGPT Projectを分けない。

会話名は原則として次のどちらかを使う。

- `サイト名（要件定義）`
- 名前未定なら `内容（要件定義）`

サイト名が決まった後は、必要なら会話名を合わせる。

## Source of Truth

```text
Web制作の共通ルール
→ EliteMay/web-project-guide

要件定義Projectの進め方
→ このREQUIREMENTS_PROJECT.md

制作Projectの共通設定
→ DEVELOPMENT_PROJECT.md

サイト固有要件
→ 各Project RepositoryのCurrent Requirements

実装Task / Worker割当のcoordination
→ EliteMay/web-project-data/work-queues/<repository>/

Public Dashboard表示
→ Authoritative Queue / Run Stateから生成したsanitize済みProjection

実コード・データ・現行仕様
→ 各Project Repository
```

Queueは実装計画・coordinationであり、サイト固有Requirementsの第二Source of Truthにはしない。Public DashboardもQueue / Run Stateの第二Authorityにはしない。
