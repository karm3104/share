# PHPまとめ　＆　気づき　1日目


## PHPの基本

### プロジェクトの作成

プロジェクト名：php
使用IDE：eclipse

新規project作成
ファイル→新規→phpプロジェクト

>プロジェクト名にプログラム名は入れないほうがいい    
>プログラム名を変えるときに全て変えなくてはいけなくなるので困る

### 言語の分類
* phpはインタプリンタ言語、スクリプト言語
* JAJAはコンパイラ言語

### サーバーとクライアントの関係    
クライアントからのリクエストにサーバー側がレスポンスを返すことで成り立っている。

### phpの書き方

ファイル名: ファイル名.php
```
<?php
{php記述内容};
?>
```

### 出力

```
echo '...'...;
print '...'...;
```

### コメント

|||
|---|---|
|//...|ここから行の最後までコメント|
|/**/|スラッシュアスターアスタースラッシュの間がコメント|


### ローカルホスト=自分自身
```
127.0.0.1
```

---

## GETでのデータ受け渡し   

---


### GET送信の書式    

```
…/送信先.php?キー = 値    

@例

…/anser.php?favorite = 和食
```

### 複数のGET送信の書式    

```
…/送信先.php?キー = 値    
```

### PHP側の処理(受信)   

```
echo $_GET["値"]    

＠例    

echo $_GET["和食"]    
```

## POSTでのデータ受け渡し   

### POST送信の書式    

```
<form action = "..." method= "POST">
    (input等)
</form>

＠例

<form action="answer.php" method="post">
	<input type="text" class="form-control" name="name">
	<input type="submit" class="btn" value="送信">
</form>
```

### PHP側の処理（受信）   
```
echo $_POST["値"]    

＠例    

echo $_POST["name"]   
```

### REQUESTでのPHP側の処理（受信）    
どちらでも受け取れる！    

```
$_REQUEST["name"]
```