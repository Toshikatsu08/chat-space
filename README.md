# chat-space DB設計
## usersテーブル
|Column|Type|Options|
|------|----|-------|
|username|string|null: false|
|email|string|null: false|
|password|string|null: false|
### Association
- has_many :messages
- has_many :users_groups
- has_many :groups, through: users_groups

## messagesテーブル
|Column|Type|Options|
|------|----|-------|
|body|text|null: false|
|image|string|
|user_id|integer|null: false, foreign_key: true|
|group_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :user
- has_many :groups

## groupsテーブル
|Column|Type|Options|
|------|----|-------|
|group_name|string|null: false|
|user_id|integer|null: false, foreign_key: true, add_index :users, :username|
### Association
- belongs_to :user
- has_many :groups_tags
- has_many :tags, through: :groups_tags
- has_many :users_groups
- has_many :users, through: users_groups

## tagsテーブル
|Column|Type|Options|
|------|----|-------|
|text|text|null: false|
### Association
- has_many :groups_tags
- has_many :groups, through: :groups_tags

## groups_tagsテーブル
|Column|Type|Options|
|------|----|-------|
|group_id|integer|null: false, foreign key: true|
|tag_id|integer|null: false, foreign key: true|
### Association
- belongs_to :group
- belongs_to :tag

### users_groupsテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign key: true|
|group_id|integer|null: false, foreign key: true|
### Association
- belongs_to :user
- belongs_to :group