# todoアプリでデータをアーカイブとして残す方法

todoアプリで削除を押すと完全に消去されていると思いますが
過去のtodoを見返すため、削除したtodoをアーカイブとして別のリストに表示させる機能が欲しいのですが、
リスト表示の際にフィルタをして必要なものだけ表示させるようなことはできるのでしょうか。

[参考サイト]
https://docs.djangoproject.com/ja/3.0/topics/db/queries/

------------------------------------------------------------------------------
# DjangoはInstagramで使用

[質問者]

DjangoはInstagramで使用されているようなのですが、
Instagramのような何万人と利用するアプリもコースで作成した社内SNSの構成で作成可能なのでしょうか。
それとも大規模だと何か他に考慮するべきことがあるのでしょうか。

[先生]

基本的には講義の内容通りでアプリを作成すること可能ですが、セキュリティ面の設定やユーザーモデルの拡張、検索機能の導入やメールサーバーの導入など、細かい点を踏まえると本当に使えるサイトを作るという観点ではまだ沢山のステップを踏まなければいけないかと思います。

---------------------
# 社内SNSアプリの機能に追加したのですが、ユーザー別での処理

TodoアプリのレッスンでやったUpdateViewを、社内SNSアプリの機能に追加したのですが、ユーザー別での処理について質問させてください。
例えば、Aさん、Bさんがユーザーとして存在していて、それぞれ投稿をしています。

下記のように、{% if user.is_authenticated %}を使ってログイン状態のユーザーが処理を行えるようにしたのですが、Aさん（ログインしているユーザー）は自分の投稿も編集できますが、Bさんの編集もできていまします。（動画で行った< form >を少し変えてみましたが、こちらでも投稿は編集自体はできています）

Bさんの編集処理を制限したいのですが、処理が上手くできませんでした。
AさんがBさんの投稿編集をできないようにするにはどのような処理を行えば良いですか？

```html:update.html

{% if user.is_authenticated %}

      <form method="POST"　enctype="multipart/form-data">{% csrf_token %}

        <div>Title:{‌{ form.title }}</div>

        <div>Memo:{‌{ form.memo }}</div>

        <div>Image:{‌{ form.image }}</div>

        <input type="hidden" name="author" value="{‌{ user.username }}">

        <input type="submit" value="Submit">

      </form>

{% else %}

```

```python:views.py

class UpdateMessage(UpdateView):

    template_name = 'update.html'

    model = BoardModel

    fields = ('title', 'message', 'image')

    success_url = reverse_lazy('list')

```

[先生]

既読機能で使っている
post2 = request.user.get_username()
を使い、ログインしているユーザー名の情報を取れば、その情報をもとに条件分岐することによってログインしている人だけが投稿可能になるという機能を実装できるようになるかと思います。
---------------------
# Herokuを用いての公開

自分で一通り調べて実際に行ってみたところ、Buildには成功するようですが、実際の画面ではエラーが表示されており、ログを確認すると「at=error code=H10 desc="App crashed"」というエラーが出てしまっていました。

https://qiita.com/kents1002/items/e1b90c71897c55b8e870

データベースのsqlite3がHerokuに対応していないことが理由

飛んできたリクエストを受け取る、といったような設定をするファイルは、settingファイルなのでしょうか、それともurlsの方で何か設定するのでしょうか

not foundということは、Heroku自体は動いてそうですね。
そうなると、webserver→gunicorn（wsgi）→Django（urls.py）という流れになりますので、その流れのどこかで詰まっていることが原因かな、と思われます。

------------------------------------------
# todoproject、編集、アップデートしたい場合

作成した「todoproject」をVultr側からgit cloneすることで一般公開出来るように進めていきましたが、アップデートしたい場合にはどのようにするのが良いのでしょうか？

VultrにSSH接続した後に、
①：vim操作で直接編集
②：git pullコマンド または git fetch + git mergeコマンドで変更分を取り込む

などが考えられますが、②の方法で問題ないのか、より効率的な方法があるのかご教示頂きたいです。個人開発レベル、GitHub上のmasterブランチを常に最新にしている前提でアドバイス頂ければ幸いです。


はい、②の方法で全く問題ないかと思います。

------------------------------------------