https://sinyblog.com/django/django-allauth/


ビジネス
 ホームDjango爆速で作れるDjangoユーザ認証機能【django-allauth】


目次 [hide]

1 Django-allauthとは？
2 今回django-allauthで作った認証機能アプリ
3 django-allauthによるユーザ認証機能実装手順
 ①django-allauthモジュールのインポート
 ②アプリケーションの作成
 ③settings.pyの設定
 ③urls.pyの設定
 ④マイグレーションの実行
 ⑤django-authテンプレートのカスタマイズ
こんにちは。sinyです。

最近、改めてDjango認証回りの勉強をしているのですが、Django標準である程度認証機能が付属しているとはいえ、1つ1つ画面機能を作りこんでいくのはちょっと手間がかかって大変だと思います。
特に入門者に取ってはとっつきにくい部分の1つだと思います。

今回は、そんなDjangoのユーザ認証周りの基本的な機能をdjango-allauthというモジュールを使って爆速で簡単に実装する手順を紹介します。

また、「デフォルトのままだと画面デザインがしょぼい、画面遷移が微妙」というのもあるので、その辺も少し整えた形で実装してみました。

Django-allauthとは？
Django-allauthとはDjangoパッケージで、以下のようなユーザ認証系の機能を備えているモジュールになっています。

django-allauth機能
ユーザログオン機能
ユーザログアウト機能
パスワード変更
パスワード再設定
ユーザ登録
上記以外にもソーシャル連携認証（Twitter等のユーザ認証を使ってログオンするやつ）などの機能も備わっています。

今回django-allauthで作った認証機能アプリ
今回は、django-allauthを使って以下の機能を実装してみました。

ユーザログオン機能
ユーザログアウト機能
パスワード再設定
ユーザ登録
django-allauthで実際に作った簡単なユーザ認証機能アプリのデモ動画です。


 

django-allauthによるユーザ認証機能実装手順
では実際に、django-allauthを使ったユーザ認証機能の実装手順を説明していきます。
細かい部分は一旦おいておいて、入門者でも簡単に実装できる手順にしました。

事前準備として、以下の作業は終わっている前提とします。

事前準備
仮想環境作成(python -m venv tutorial)
プロジェクト作成(django-admin startproject tutorial)
言語設定(英語→日本語）
管理者ユーザの作成(python manage.py createsuperuser)
もし、事前準備の手順がよくわからないという方は、以下の記事でDjangoの基礎タスクについて勉強してみてください。


さて、django-allauthの実装手順に入っていきます。
なお、以下の環境で動作確認しています。

モジュール	バージョン
Django	 2.1.4
Python	3.6.5
django-allauth	0.38.0

①django-allauthモジュールのインポート
まず最初にdjango-allauthモジュールを以下の手順でインポートします。
```
pip install django-allauth
```

※Django本体をインストールしてない場合はpip instlal djangoでインストールしておいてください。

②アプリケーションの作成
　
今回は、以下のコマンドでユーザ認証用のアプリケーション「accounts」を作成します。

python manage.py startapp accounts

③settings.pyの設定
settings.pyのINSTALLED_APPSに以下5個(#追加の部分）を追加します。


```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'accounts',                #追加
    'django.contrib.sites',    #追加
    'allauth',                 #追加
    'allauth.account',         #追加
    'allauth.socialaccount',   #追加
]

```


作成したアプリケーション「accounts」と、allauth関連の設定を４つ追加しています。
続いて、settings.pyの最終行に以下のエントリーを追加します。

```
SITE_ID = 1
LOGIN_REDIRECT_URL = 'home'
ACCOUNT_LOGOUT_REDIRECT_URL = '/accounts/login/'

EMAIL_HOST = 'smtp.gmail.com'
EMAIL_PORT = 587
EMAIL_HOST_USER = '自分nogmailアドレス'
EMAIL_HOST_PASSWORD = 'gmailのパスワード'
EMAIL_USE_TLS = True
```

----------
各パラメータの説明
SITE_ID：動かしているサイトを識別するID
LOGIN_REDIRECT_URL：ログオン後に遷移するURLの指定
ACCOUNT_LOGOUT_REDIRECT_URL ： ログアウト後に遷移するURLの指定
EMAIL_HOST ：メールサーバの指定（今回はGmailを使うのでsmtp.gmail.comとしています）
EMAIL_PORT ：ポート番号の指定
EMAIL_HOST_USER ：Emailサーバの認証ユーザ名
EMAIL_HOST_PASSWORD：認証パスワード
EMAIL_USE_TLS ：TLSの設定（TRUE,FALSE)
なお、今回はGmailメールサーバでパスワードリセットメールを送る設定にしていますが、
Gmailを使う場合は「安全性の低いアプリのアクセス」を「有効」にしておく必要がありますので注意してください。（設定方法はググればすぐでてきます）
----------



③urls.pyの設定
プロジェクト直下のurls.pyを以下の通り設定します。

```
from django.contrib import admin
from django.urls import include, path　　　#includeを追加
from django.views.generic import TemplateView　　　#追加
 
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', TemplateView.as_view(template_name='home.html'), name='home'),　　#追加
    path('accounts/', include('allauth.urls')),　　　#追加
]
``` 
 
```
path('', TemplateView.as_view(template_name='home.html'), name='home'),
```

これは、ログオン後のTOP画面の定義です。
単純にTemplateView汎用ビューを使って、home.htmlにレンダリングしてるだけです。

```
path('accounts/', include('allauth.urls')),
```

上記は、allauthのurls.pyの設定をインクルードするための設定です。

ちなみに、allauthのurls.pyは有効化した仮想環境フォルダ内の以下に存在しています。

「\venv\<仮想環境名>\Lib\site-packages\allauth\accounts\urls.py」に存在しています。

④マイグレーションの実行
python manage.py migrateを実行しておきます。
※特にモデルの定義などしていないので、ユーザ認証系のテーブルだけが生成されます。

python manage.py runserverを実行して以下のURL(http://127.0.0.1:8000/accounts/login/)にアクセスして以下の画面が表示されればとりあえずOKです。



基本的にはこれでユーザ認証系機能の実装自体は終わっています。
1つ1つ機能を定義していくのに比べたらめちゃくちゃ簡単に実装できることがわかると思います。

ただ、上記画面を見てもわかるように画面デザインがいけていなかったり、ログオン画面に戻るボタンがところどころついていなかったりするのでちょっとカスタマイズします。

⑤django-authテンプレートのカスタマイズ
上記で実装されたユーザ認証系のテンプレートファイルは、
「\venv\<仮想環境名>\Lib\site-packages\allauth\templates」に存在しているので、基本的にこのテンプレートファイルを自分好みのデザインにカスタマイズしていけばOKです。

とはいえ、入門者にとっては

「どうやってカスタマイズすればいいかまだ分からない・・・」

っていう人もいるかもしれないので、とりあえず、見た目と画面遷移をそれなりにしたテンプレートを作ってみました。

以下のGithubサイトからテンプレートファイルをダウンロードして、\site-packages\allauth\templates\accountフォルダ配下に上書きコピーしてください。

https://github.com/sinjorjob/django-allauth-templates

以上で、最初にお見せしたデモ動画のようなデザイン（下記図）のユーザ認証アプリが完成します。



今回は、django-allauthテンプレートの以下を少しカスタマイズしてみました。

カスタマイズしたテンプレート一覧
signup.html（ユーザ登録画面用）
login.html（ログオン画面用）
password_reset.html（パスワードリセット画面用）
password_reset_from_key.html(パスワードリセット画面用）
password_reset_from_key_done.html（パスワードリセット完了画面用）
logout.html（ログアウト画面用）
base.html(共通テンプレート）
カスタマイズした内容ですが、実はたいしたことはしていなくて、それなりに見た目をよくするために以下を追加、修正しただけです。

Bootstrap4を利用するようにコードを追加(base.html)
ボタンデザインに「class="btn btn-primary"」をつけてデザインを変更
bootstratpのclassを使って画面全体のデザインを微修正
（content-wrapper/container-fluid/card-bodyあたり）
ログオン画面に戻るリンクボタンを追加

```
<a class="btn btn-primary" href="{% url 'account_login' %}" role="button">ログオン画面</a>
```

フォームの表示方法を変更(form.as_p→form.as_table)
 

以上、django-allauthを使った「爆速で作れるDjangoユーザ認証機能【django-allauth】」でした。
少しでも参考になれば幸いです。




