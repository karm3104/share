# 検索・抽出・表示コマンド集

## 一連の流れ

||コマンド|役割|備考|
|:---|:---|:---|:---|
||mysql -u root -p|ログインコマンド（-u:ユーザー指定、-p:パスワード…ここブランクエンターで次で入力）||
||show database();|データベースの中身確認||
||use DB名|対象データベースに移動||
||show tables;|テーブルの中身確認||
||desc テーブル名;|テーブルの型、フィールド項目、名前の確認||
||set names cp932;|日本語使うときは入れるときも出すときも必須！(文字化けを防ぐ)||
||select * from テーブル名|テーブルの中身の確認||
|||||


## 表示系コマンド

||コマンド|役割|備考|
|:---|:---|:---|:---|
||select FIELD名2,FIELD名3,FIELD名1 from TB名;|フィールドを入れ替えて表示する||
||select FIELD名2,FIELD名3,FIELD名2,…,from TB名 from TB名;|連続して表示も可能||
|*|エイリアス|*|*|
||select FIELD名 as 置換後FIELD名 from TB名;|出力時にフィールド名を置き換える||
||select FIELD名*1000 as 置換後FIELD名 from TB名;|出力時にフィールドのデータを*1000した上でFIELD名を置き換える||
|*|四則演算|*|*|
||select FIELD名1+FIELD名2 from TB名;|TB名のFIELD1とFIELD2を足す||
||select FIELD名1-FIELD名2 from TB名;|TB名のFIELD1とFIELD2を引く||
||select FIELD名1*FIELD名2 from TB名;|TB名のFIELD1とFIELD2をカケル||
||select FIELD名1/FIELD名2 from TB名;|TB名のFIELD1とFIELD2を割る||
|*|関数|*|*|
||select avg(FIELD名) from TB名;|FIELD名の平均値を表示|avg|
||select sum(FIELD名) from TB名;|FIELD名の合計値を表示|sum|
||select count(FIELD名) from TB名;|FIELD名の件数を表示|count|
||select min(FIELD名) from TB名;|FIELD名の最小値を表示|min|
||select max(FIELD名) from TB名;|FIELD名の最大値を表示|max|
|||||




## キーの設定

||コマンド|役割|備考|
|:---|:---|:---|:---|
|||||
|||||
|||||
|||||
|||||


## 確認系コマンド

||コマンド|役割|備考|
|:---|:---|:---|:---|
|||||
|||||
|||||
|||||
|||||

## 改造系コマンド

||コマンド|役割|備考|
|:---|:---|:---|:---|
|||||
|||||
|||||
|||||
|||||

## 削除系コマンド

||コマンド|役割|備考|
|:---|:---|:---|:---|
|||||
|||||
|||||
|||||
|||||