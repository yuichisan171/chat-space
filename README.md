# Chatspace

## 概要
---
カリキュラムからChatspaceのトップ画面を実装。

## 詳細
---

### 構造
コーディングしたトップ画面の構造は以下の通り。

- サイドバー
  - サイドヘッダー
    - nameやボタン等のボックス
  - グループ一覧
    - グループ名,最新のメッセージ

- メイン画面
  - メインヘッダー
    - 現在のグループ,編集ボタン等
  - メッセージ
    - name,時間,メッセージ
  - 投稿フォーム
    - 入力フォーム,画像貼り付け機能,送信ボタン

[全体イメージ](https://gyazo.com/7281855aafaae516a6444cb2bef60d30)
使用言語:haml,scss

### DB

#### usersテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false, index: true|
|email|string|null: false|
|password|string|null: false|

##### Association
- has_many :group_users
- has_many :groups, through: :groups_users
- has_many :messages

#### groupsテーブル
|Column|Type|Options|
|------|----|-------|
|name|text|null: false|

##### Association
- has_many :group_users
- has_many :users, through: :groups_users
- has_many :messages

#### groups_usersテーブル

|Column|Type|Options|
|------|----|-------|
|user_id|references|null: false, foreign_key: true|
|group_id|references|null: false, foreign_key: true|

##### Association
- belongs_to :group
- belongs_to :user

#### messagesテーブル
|Column|Type|Options|
|------|----|-------|
|text|text||
|image|string||
|user_id|references|null: false, foreign_key: true|
|group_id|references|null: false, foreign_key: true|

##### Association
- belongs_to :user
- belongs_to :group

### 苦戦したこと
主にメイン画面。ネストやプロパティをどう書くのか大変だったこと。