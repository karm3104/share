# Djangoアプリ作成(Anaconda 環境下)


## 作業前準備（作成済みの場合）

### Anaconda仮想環境のアクティベーション（有効化）

djangoの仮想化関連DIR(venv)に移動

```
cd c:xxxxxxxx\django\venv
```

djangoの仮想化関連DIR（cd c:xxxxxxxx\django\venv）内で
仮想環境の有効化（アクティベーション）

```
.\[仮想環境名]\Scripts\activate
```

### 無効化

```
deactivate
```

### 開発サーバ起動（プロジェクト内manage. py）

```
cd c:xxxxxxxx\django\[プロジェクト名]
python manage.py runserver
```


## 初回起動時

Anaconda仮想環境を作るフォルダの作成

```
mkdir c:xxxxxxxx\django\venv
```

作成したフォルダに移動

```
cd c:xxxxxxxx\django\venv
```

仮想環境の作成

```
python -m venv [仮想環境名]
```

django対象ディレクトリに移動
```
cd c:xxxxxxxx\django\venv
```

django対象ディレクトリ（cd c:xxxxxxxx\django\venv）内で
仮想環境の有効化（アクティベーション）

```
.\[仮想環境名]\Scripts\activate
```

無効化

```
deactivate
```

最新のdjangoをインストール

```
pip install django
```

バージョンを絞りたいとき

```
pip install django==x.x.x
```

インストール時にpipに怒られたとき

```
pip install --upgrade pip
```

更に怒られたら

```
python -m pip install --upgrade pip
```
（ 参考：https://www.curict.com/item/5a/5ac72d2.html ）

インストールされているモジュールを確認

```
pip list
```

## プロジェクトの作成
対象フォルダに移動（django内、venvは仮想環境用ファイルなのでには入らない！）
```
cd c:xxxxxxxx\django
django-admin startproject [プロジェクト名]
```
（→完了すると[プロジェクト名]のフォルダとファイルが出来上がる。）


## 開発サーバ起動（プロジェクト内のmanage　.py ）
```
cd c:xxxxxxxx\django\[プロジェクト名]
python manage.py runserver
```

### 日本語化(初回のみ)

```
C:xxxxxxxx\django\[プロジェクト名]\[プロジェクト名]\settings.py
LANGUAGE_CODE = 'en-us'
TIME_ZONE = 'UTC'
↓　↓
LANGUAGE_CODE = 'ja'
TIME_ZONE = 'Asia/Tokyo'
```

### データベースの設定

割愛

## アプリケーションの作成

新たなCP画面を立ち上げてdjango対象ディレクトリに移動(サーバー用CPとアプリケーション用CPを分けとくため)

```
cd c:xxxxxxxx\django\venv
```

django対象ディレクトリ（cd c:xxxxxxxx\django\venv）内で
仮想環境の有効化（アクティベーション）

```
.\[仮想環境名]\Scripts\activate
```

### アプリケーションの作成

```
cd c:xxxxxxxx\django\[プロジェクト名]
python manage.py startapp [アプリケーション名]
```


## 2回目以降（作成済みの場合）

### Anaconda仮想環境のアクティベーション（有効化）

djangoの仮想化関連DIR(venv)に移動

```
cd c:xxxxxxxx\django\venv
```

djangoの仮想化関連DIR（cd c:xxxxxxxx\django\venv）内で
仮想環境の有効化（アクティベーション）

```
.\[仮想環境名]\Scripts\activate
```

### 無効化

```
deactivate
```

### 開発サーバ起動（プロジェクト内manage. py）

```
cd c:xxxxxxxx\django\[プロジェクト名]
python manage.py runserver
```




















