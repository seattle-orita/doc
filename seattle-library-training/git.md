# gitに関するルール

## git ワークフロー

![git-flow](https://wac-cdn.atlassian.com/dam/jcr:34c86360-8dea-4be4-92f7-6597d4d5bfae/02%20Feature%20branches.svg?cdnVersion=1783)

参照 : https://www.atlassian.com/ja/git/tutorials/comparing-workflows/gitflow-workflow

### 各ブランチについて

|ブランチ|名称|
|-|-|
|main|メインブランチ|
|develop/yyyyMMdd|デベロップブランチ（日付ブランチ）|
|feature/issue-[0-9]|フィーチャーブランチ|

#### main

作成済み。  
直接の書き込み禁止。  
毎月実施されるデベロップブランチとのマージでのみ更新される。

#### develop

派生元はメインブランチ。  
開発リーダーが作成し、プッシュする。  
ブランチ名のサフィックスは月末の日付を指定する。  
例 : `develop/20210930`  
直接の書き込み禁止。  
フィーチャーブランチとのマージでのみ更新される。

#### feature

派生元はデベロップブランチ。  
実装者がローカルで作成し、プッシュする。  
ブランチ名のサフィックスは対象Issueの番号を指定する。  
例 : `feature/issue-1`  
直接コミット・プッシュし、プルリクエストを作成する。

### ブランチ保護について

| |直接のプッシュ|変更されるタイミング|作成者|
|-|-|-|-|
|main|×|developとのマージ|-|
|develop|×|初回プッシュ<br>featureとのマージ|開発リーダー|
|feature|○|開発作業時|実装者|

基本的に**feature以外のブランチでコミット、プッシュは禁止。**  
seattleconsulting-stockのプライベートリポジトリではブランチ保護設定ができないため、各自上記のルールを遵守すること。  

### featureブランチでの作業方法

`yyyyMMdd`, `issue-[0-9]`は読み替えること。  

```bash
# 親ブランチに移動
git checkout develop/yyyyMMdd
# 最新の状態にする
git pull origin develop/yyyyMMdd
# developを親としてfeatureを作成
git checkout -b feature/issue-[0-9]
```

### developブランチの作成

`yyyyMMdd`,は読み替えること。  

```bash
# 親ブランチに移動
git checkout main
# 最新の状態にする
git pull origin main
# mainを親としてdevelopを作成
git checkout -b develop/yyyyMMdd
# 初回コミット
git commit --allow-empty -m "start develop/yyyyMMdd"
# プッシュ
git push origin develop/yyyyMMdd
```

- 初回コミットは空
- メッセージは`start develop/yyyyMMdd`

## コミットメッセージ

- コミットメッセージと変更内容が一致していることは確認すること。
- プレフィックスにハッシュ(#)とIssue番号をつけ、変更内容を記載  

例 : `#1 javaのソースコード追加`  
参照 : https://github.com/seattleconsulting-stock/seattle-library-training/commit/27326e6f263c43db682809d6f5cd5b80a5fafde7

## Tips

### 書き込み禁止ブランチに変更を加えてプッシュしてしまった場合

**下記手順が何を実施しているか不鮮明な場合は絶対に実施せず、開発リーダーへ連絡、もしくはSlackの開発チャンネルで周知すること。**  

```bash
# gitの履歴を見て、変更を加える前のHEADを確認する
git reflog
# 変更前のHEADにリセットする（HEADが10だった場合）
git reset HEAD@{10}
# 強制プッシュ
git push --force-with-lease origin 対象ブランチ
```

### 親ブランチがマージされた場合

（例）  
マージされた親ブランチ : `develop/20210820`  
現在のデベロップブランチ ; `develop/20210903`

```bash
git rebase --onto develop/20210903 develop/20210820
```
