# Todoアプリ

CRUD機能のtodoアプリ(IPアドレスで接続)
# 使い方

## [Web接続]

1. vultrに接続し、スナップショットからインスタンスを作成、https://my.vultr.com/


2. トップページに接続 or 管理ユーザーとして接続
	- http://<独自ドメイン>/list
	- ex) http://45.77.22.104/list

	- http://<独自ドメイン>/admin
	- ex) http://45.77.22.104/admin


(注)
スナップショットからインスタンス作成でIPアドレスが変更になる



## [ローカル接続]

1. カレントディレクトリに移動


	`cd /Users/user/Dropbox/iCollections/Folder2/PF/django/todoproject1`

	`python manage.py runserver`

2. http://<IPアドレス>:<ポート番号>/が表示されるのでコピーし、ブラウザーに接続

---------------------
# URL

- 管理画面:	http://<独自ドメイン>/admin

- トップページ:	http://<独自ドメイン>/list

- 新規作成: http://<独自ドメイン>/create

- 詳細画面: http://<独自ドメイン>/detail/<id番号>

- 削除: http://<独自ドメイン>/delete/<id番号>

- 編集画面: http://<独自ドメイン>/update/<id番号>

# 使用技術・サーバー

- python3

- Django

- postgresql

- nginx

- gunicorn

- Git

- html/CSS

- Bootstrap

- vultr(サーバー)

- DNS

# 機能一覧

- 新しいtodoリストを作成

- 作成したtodoリストの中身を読込表示

- 作成したtodoリストを更新

- todoリストの中身を削除