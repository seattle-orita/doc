# GitHubに関するルール

## Issue

|項目|入力値|
|-|-|
|Title|タスクの内容が分かる文言|
|Comment|新規機能開発 : `新規機能の概要・対応方針・内容など`<br>バグ対応 : `調査結果・ログ・発生箇所・環境・対応内容など`|
|Assignees|タスクの担当者|
|Labels|[GitHub公式ドキュメント](https://docs.github.com/ja/issues/using-labels-and-milestones-to-track-work/managing-labels#about-default-labels)に準ずる|
|Projects|存在するProjectsを選択|
|Milestone|-|

### クローズ

PRがマージされた・ドキュメントが承認されたタイミングでクローズする。  
Issue作成者がクローズすること。  

### リオープン

基本的になし。  
追加対応の場合は新規Issueを作成して、説明欄に記載する。

## Pull Request

|項目|入力値|
|-|-|
|Title|feature -> develop : `対象Issueのタイトルをコピー`<br>develop -> main : `merge develop/yyyyMMdd into main`|
|Comment|feature -> develop : `Issueのリンク(ハッシュとIssue番号)・変更内容・レビュー時に補足したい箇所`<br>develop -> main : `-`|
|Reviewers|開発リーダー|
|Assignees|実装担当者|
|Labels|-|
|Projects|-|
|Milestone|-|

### クローズ

基本的にはしなくて良い。  
クローズする場合はコメントを記載してクローズすること。

### マージ

レビュー終了後、**開発リーダーが行う。**  
ブランチ保護と同様、マージの権限を変更できないため上記ルールを遵守すること。

## Projects

**開発リーダーが作成する。**  
基本的に**管理するのはIssueのみ。**  
ゆくゆくは自動化したい。。

|項目|入力値|
|-|-|
|Project Board Name|マージ予定日 `yyyy/MM/dd`|
|Description|-|
|Project template|Template: None|

### カラム

以下4つを作成。  
- Todo
- in Progress
- in Review
- Done

### フロー

![project-flow](https://user-images.githubusercontent.com/85621608/131568052-dcd6acb0-1d75-40af-9d0e-734c555e0ea3.png)

|カラム名|状態|
|-|-|
|Todo|Issueがオープンしている・着手はしていない|
|in Progress|実装中・着手中|
|in Review|プルリクエストやドキュメントのレビュー中・レビュー指摘反映中|
|Done|プルリクエストがマージされた・ドキュメントが承認された|
