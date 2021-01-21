# 追加・削除・変更コマンド集

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


## 追加系コマンド

||コマンド|役割|備考|
|:---|:---|:---|:---|
|*|set names cp932;|文字化けを防ぐ|日本語使うときは入出力時に必須！|
||create|作成|database,table|
||create database DB名|データベースの新規作成||
||create table TB名 (FIELD名 型(桁数),…);|field、型を指定してテーブルを作成||
||insert|入力|table|
||insert into TB名(FIELD名1,…) values ('データ'…);|レコードとしてデータの中身を追加||
||→|(FIELD名)は全項目入力の際は不要||
|*|desc TB名;|テーブルの型、フィールド項目、名前の確認|テーブル作ったら必ず確認！|
|||||
|*|テーブルやレコードのコピー|*|*|
||create table 新TB名 select * from コピー元TB名|テーブルの完全コピー|FIELDも中身も取ってくる|
||create table 新TB名 like コピー元TB名|コピー元のフィールド構造だけをコピー|主キーなど属性もコピー|
||insert into 既存TB名 select * from コピー元TB名|他テーブルのレコードをコピー|構造が互いに同じであること|
||insert into 既存TB名 select * from コピー元TB名|特定のフィールドのデータをコピー||
|||||


## キーの設定

||コマンド|役割|備考|
|:---|:---|:---|:---|
|*|プライマリキーの設定|*|*|
||create table TB名(FIELD名 型(桁) primary key,FIELD名 型(桁),…|1つの主キーを設定する際||
||create table TB名(FIELD名 型(桁),FIELD名 型(桁),…,primary key(FIELD名1,FIELD名2)|複数の主キーを設定する際使用（現場ではこっち）||
|||||
|*|ユニークキーの設定|*|*|
||create table TB名(FIELD名1 型 unique,FIELD名2)|重複できない制限をかけるだけでNULLの入力は可能||
|||||
|*|連続採番されるフィールドの設定|*|*|
||create table TB名(FIELD名1 型 auto_increment primary key,FIELD名2)|自動採番||
|||||
|*|自動採番初期値の設定|*|*|
||alter table TB名 auto_increment = xx;|xx番から採番される。但し、現在登録されている数字より大きくなくてはならない||
|||||
|*|最初からデータが入っているフィールドの設定|*|*|
||alter table TB名 modify FIELD名 型(桁) default '初期値';|対象のフィールドには初期値がデフォルトで入る||
|||||


## 確認系コマンド

||コマンド|役割|備考|
|:---|:---|:---|:---|
||show database();|データベースの中身確認||
||show tables;|テーブルの中身確認||
||desc TB名;|指定したテーブルの型、フィールド項目、名前の確認||
||select * from TB名|テーブルの中身の確認||
|||||

## 改造系コマンド

||コマンド|役割|備考|
|:---|:---|:---|:---|
||alter table TB名 modify 変更値;|フィールドの定義を変更||
||alter table TB名 add 変更値;|フィールドを追加||
||alter table TB名 change 変更値;|フィールドの名前と定義を変更||
||alter table TB名 drop FIELD名;|フィールドの削除||
|||||
|*|フィールド位置の変更|*|*|
||alter table TB名 add 変更値 first;|先頭にフィールドを追加||
||alter table TB名 add 変更値 after FIELD名;|指定したフィールドの後にフィールドを追加||
||alter table TB名 modify FIELD名 型 first等 ;|first等の位置にフィールドを変更する||
||alter table TB名 change 元FIELD名 新FIELD名 新型|フィールドの名前とデータ型を変更||
||alter table TB名 drop FIELD名|フィールドを削除||
|||||

## 削除系コマンド

||コマンド|役割|備考|
|:---|:---|:---|:---|
||drop|削除||
||drop databasee DB名;|指定したデータベース全体を削除||
||drop table TB名;|指定したテーブル全体を削除||
||drop table if exists TB名;|指定したテーブルが存在すれば対象を削除||
||delete from TB名;|テーブルのレコードだけを削除||
||alter table TB名 drop FIELD名|指定したテーブルの指定したフィールドを削除||
|||||
