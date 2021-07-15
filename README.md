# Todoアプリ

CRUD機能のtodoアプリ(独自ドメインで接続)
# 使い方

## 新しいTodoを作成

1. トップページの左上にある新規作成ボタンをクリック

2. 入力・選択項目(4つ)

	1. Title

	2. Memo

	3. Priority(優先度)
		1. high
		2. normal
		3. low

	4. Duedate(期限)

3. createボタンをクリック

## 作成したTodoを編集

各Todoリストにある、「編集画面へ」を選択


## 作成したTodoを削除

各Todoリストにある、「削除画面へ」を選択

## 作成したTodoの詳細内容を見る

各Todoリストにある、「詳細画面へ」を選択

---------------------
# URL

- トップページ:		http://portfolio7716.work

- 管理画面:            http://portfolio7716.work/admin

- 新規作成:            http://portfolio7716.work/create

- 詳細画面:            http://portfolio7716.work/detail/<id番号>

- 削除:               http://portfolio7716.work/delete/<id番号>

- 編集画面:            http://portfolio7716.work/update/<id番号>

# 使用技術・サーバー

- python3

- Django

- postgresql

- nginx

- gunicorn

- Git

- html/CSS

- Bootstrap

- vultr

- DNS

# 機能一覧

- 新しいtodoリスト作成

	- Title
	- Memo
	- Priority(優先度3つ)
	- Duedate(期限)

- 作成したtodoリストの詳細表示

- 作成したtodoリストを更新

- todoリストの中身を削除