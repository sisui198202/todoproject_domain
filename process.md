# 接続

http://portfolio7716.work/

# 独自ドメイン設定から接続まで

1 https://my.vultr.com/に接続し、サーバを追加する。

[追加内容]
1.1: Cloud Compute

1.2: Tokyo

1.3: Ubuntu

1.4: $5/mo

1.5: Deploy Nowを選択

1.6: [vultr]
vultrにログインしてコントロールパネルよりDNSという場所を選択しドメインを追加

1.7: スナップショットを取り込む

2 [お名前.comにネームサーバ名を追加]
ns1.vultr.com
ns2.vultr.com


(参考)
[vultrのドメイン設定方法]
https://asamesimae.com/vultr_set_domain/

[Vultr DNSの概要]
https://cloudo3.com/ja/%E3%82%AF%E3%83%A9%E3%82%A6%E3%83%88%E3%82%99%E3%82%B3%E3%83%B3%E3%83%92%E3%82%9A%E3%83%A5%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%AF%E3%82%99/vultr-dns%E3%81%AE%E6%A6%82%E8%A6%81/2202

3 ＜ローカル側での作業＞

3.1
{‌{ ローカルのディレクトリ }}/todoproject/todo/urls.py

の

urlpatterns = [

path('list/', TodoList.as_view(), name='list'),

を

urlpatterns = [

    path('', TodoList.as_view(), name='list'),

へと変更


3.2 ＜サーバへgit cloneした後のサーバ側での作業＞

変更点②

手順の「4-1. settings.pyファイルの設定」内の

vim ~/todoproject/todoproject/settings.pyで

ALLOWED_HOSTS = ['VPSのIP', ‘localhost’’]

を

ALLOWED_HOSTS = ['VPSのIP', 'VPSのIPと紐付けたドメイン名', ‘localhost’’]

へと変更



3.3 手順の「6-1. Nginxの繋ぎこみの設定」内の

sudo vim /etc/nginx/sites-available/todoprojectで

server_name VPSのIP;

を

server_name VPSのIPと紐付けたドメイン名 VPSのIP;

へと変更

4 todoenvの仮想環境に入る。

cd ​todoproject
source ​todoenv​/bin/activate

5
gunicorn --bind 0.0.0.0:8000 todoproject.wsgi

(gunicorn socketの実行)
sudo systemctl start gunicorn.socket

sudo systemctl enable gunicorn.socket

6 Nginxの再起動
sudo systemctl restart nginx

7. 独自ドメインで、ブラウザーでアクセス。

                                      以上
---------------------
# スナップショットからlistページ接続までの処理

0. サーバを作成(ubuntu,スナップショットで作成)

    0.1
    https://my.vultr.com/subs/?id=70dd6645-1f1f-4fb6-92bd-383177c88319#subsoverview

    0.2
    https://my.vultr.com/subs/?id=70dd6645-1f1f-4fb6-92bd-383177c88319#subssnapshots


1. vultrにログインし、IPアドレス入力

    1.1
    ssh nanairo@<IPアドレス>
    パスワード: nanairo1982

    ex)
    ssh nanairo@45.77.177.147


    1.2: IPアドレス入力
    vim ~/todoproject/todoproject/settings.py

    [settings.py]
    ALLOWED_HOSTS = ['VPSのIP', ‘localhost’’]

2.
    2.1
    cd ​todoproject

    2.2
    source ​todoenv​/bin/activate

3. (todoenv)で入った状態で下記を実行すること
    3.1
    python3 manage.py makemigrations

    3.2
    python3 manege.py migrate

    3.3
    python3 manage.py collectstatic

4.

    4.1
    sudo ufw allow 8000

    4.2
    gunicorn --bind 0.0.0.0:8000 todoproject.wsgi

    * 45.77.177.147:8000/listを、クロームに入力

    4.3
    deactivate


5.

    5.1
    sudo systemctl start gunicorn.socket

    5.2
    sudo systemctl enable gunicorn.socket


6. VPSのIP​を入力他

    6.1
    sudo vim /etc/nginx/sites-available/​todoproject

    [todoproject]

    server { listen 80;
    server_name ​VPSのIP​;
    location = /favicon.ico { access_log off; log_not_found off; } location /static/ {
    root /home/​ryota​/​todoproject​; }

    6.2
    sudo systemctl restart nginx

    6.3
    sudo ufw allow 'Nginx Full'

(ブラウザークロームでlistページに接続)
7. 45.77.177.147/list

---------------------
# ipアドレス入力(2つ)

1. vim ~/todoproject/todoproject/settings.py

＋＋＋ここから
ALLOWED_HOSTS = ['VPSのIP', ‘localhost’’]
DATABASES = {
 'default': {
 'ENGINE': 'django.db.backends.postgresql_psycopg2',
 'NAME': 'myproject',
 'USER': 'myprojectuser',
 'PASSWORD': 'password',
 'HOST': 'localhost',
 'PORT': '',
 }
}


2. sudo vim /etc/nginx/sites-available/todoproject

＋＋＋ここから
server {
 listen 80;
 server_name VPSのIP;
 location = /favicon.ico { access_log off; log_not_found off; }
 location /static/ {
 root /home/ryota/todoproject;
 }
 location / {
 include proxy_params;
 proxy_pass http://unix:/run/gunicorn.sock;
 }
}
