# 追加・削除・変更・レコード編集・ビュー・トランザクション　コマンド集


## ページ内リンク

|中項目|小項目|
|:---|:---|
|[追加系コマンド](#追加系コマンド)|[TABLEやRECORD、DBの作成、追加 ( CREATE, INSERT ) ](#TABLEやRECORDのコピー) / [TABLEやRECORDのコピー ( CREATE, INSERT ) ](#TABLEやRECORDのコピー) / [ビューの追加 ( view ) ](#ビューの追加)|
|[キーの設定](#キーの設定)|主キー ( primary key ) / ユニークキー ( unique ) / 自動採番関連 ( auto_increment ) / FIELD初期値 ( default ) |
|[確認系コマンド](#確認系コマンド)|確認 ( show, desc, select * from ) |
|[改造系コマンド](#改造系コマンド)|[FIELDの値を変更 ( alter table ) ](#FIELDの値を変更)/  [FIELD位置の変更 ( alter table … first等 ) ](#FIELD位置の変更)|
|[削除系コマンド](#削除系コマンド)|DB,TABLE削除 ( drop ) / RECORD全削除 ( delete from ) / FIELD削除 ( alter table … drop … ) |
|[RECORD編集](#RECORD編集)|[RECORD追加 ( insert into ... value ... ) ](#RECORD追加)/  [RECORD変更 ( update ... set ...'' ) ](#RECORD変更)/  [RECORD削除 ( delete from ... where ... ) ](#RECORD削除)|
|[トランザクション](#トランザクション)|開始 ( start transaction ) / 戻す ( rollback ) / 確定 ( commit ) |




## 一連の流れ

||コマンド|役割|備考|
|:---|:---|:---|:---|
||mysql -u root -p|ログインコマンド（-u:ユーザー指定、-p:パスワード…ここブランクエンターで次で入力）||
||show database();|DATABASEの中身確認||
||use DB名|対象DATABASEに移動||
||show tables;|TABLEの中身確認||
||desc TABLE名;|TABLEの型、FIELD項目、名前の確認||
||set names cp932;|日本語使うときは入れるときも出すときも必須！(文字化けを防ぐ)||
||select * from TABLE名|TABLEの中身の確認||



## 追加系コマンド

### TABLEやRECORDの作成

||コマンド|役割|備考|
|:---|:---|:---|:---|
|*|set names cp932;|文字化けを防ぐ|日本語使うときは入出力時に必須！|
||create|作成|database,table|
||create database DB名|DATABASEの新規作成||
||create table TB名 (FIELD名 型(桁数),…);|field、型を指定してTABLEを作成||
||insert|入力|table|
||insert into TB名(FIELD名1,…) values ('データ'…);|RECORDとしてデータの中身を追加||
||→|(FIELD名)は全項目入力の際は不要||
|*|desc TB名;|TABLEの型、FIELD項目、名前の確認|TABLE作ったら必ず確認！|

### TABLEやRECORDのコピー

||コマンド|役割|備考|
|:---|:---|:---|:---|
||create table 新TB名 select * from コピー元TB名|TABLEの完全コピー|FIELDも中身も取ってくる|
||create table 新TB名 like コピー元TB名|コピー元のFIELD構造だけをコピー|主キーなど属性もコピー|
||insert into 既存TB名 select * from コピー元TB名|他TABLEのRECORDをコピー|構造が互いに同じであること|
||insert into 既存TB名 select * from コピー元TB名|特定のFIELDのデータをコピー||

### ビューの追加

||コマンド|役割|備考|
|:---|:---|:---|:---|
||create or replace view VIEW名 as select… |selectで検索したSQLで抜き出した情報を、VIEW名で保存する||




## キーの設定

||コマンド|役割|備考|
|:---|:---|:---|:---|
|*|プライマリキーの設定|*|*|
||create table TB名(FIELD名 型(桁) primary key,FIELD名 型(桁),…|1つの主キーを設定する際||
||create table TB名(FIELD名 型(桁),FIELD名 型(桁),…,primary key(FIELD名1,FIELD名2)|複数の主キーを設定する際使用（現場ではこっち）||
|*|ユニークキーの設定|*|*|
||create table TB名(FIELD名1 型 unique,FIELD名2)|重複できない制限をかけるだけでNULLの入力は可能||
|*|連続採番されるFIELDの設定|*|*|
||create table TB名(FIELD名1 型 auto_increment primary key,FIELD名2)|自動採番||
|*|自動採番初期値の設定|*|*|
||alter table TB名 auto_increment = xx;|xx番から採番される。但し、現在登録されている数字より大きくなくてはならない||
|*|最初からデータが入っているFIELDの設定|*|*|
||alter table TB名 modify FIELD名 型(桁) default '初期値';|対象のFIELDには初期値がデフォルトで入る||



## 確認系コマンド

||コマンド|役割|備考|
|:---|:---|:---|:---|
||show database();|DATABASEの中身確認||
||show tables;|TABLEの中身確認||
||desc TB名;|指定したTABLEの型、FIELD項目、名前の確認||
||select * from TB名|TABLEの中身の確認||



## 改造系コマンド

### FIELDの値を変更

||コマンド|役割|備考|
|:---|:---|:---|:---|
||alter table TB名 modify 変更値;|FIELDの定義を変更||
||alter table TB名 add 変更値;|FIELDを追加||
||alter table TB名 change 変更値;|FIELDの名前と定義を変更||
|Ex|alter table TB名 change 元FIELD名 新FIELD名 新データ型|FIELDの名前とデータ型を変更||
||alter table TB名 drop FIELD名;|FIELDの削除||

### FIELD位置の変更

||コマンド|役割|備考|
|:---|:---|:---|:---|
||alter table TB名 add 変更値 first;|先頭にFIELDを追加||
||alter table TB名 add 変更値 after FIELD名;|指定したFIELDの後にFIELDを追加||
||alter table TB名 modify FIELD名 型 first等 ;|first等の位置にFIELDを変更する||



## 削除系コマンド

||コマンド|役割|備考|
|:---|:---|:---|:---|
||drop|削除||
||drop databasee DB名;|指定したDATABASE全体を削除||
||drop table TB名;|指定したTABLE全体を削除||
||drop table if exists TB名;|指定したTABLEが存在すれば対象を削除||
||delete from TB名;|TABLEのRECORDだけを削除||
||alter table TB名 drop FIELD名|指定したTABLEの指定したFIELDを削除||



## RECORD編集

### RECORD追加

||コマンド|役割|備考|
|:---|:---|:---|:---|
||insert into TB名 values(,入力値,入力値,…);|RECORD一括挿入、全項目入力時のみFIELD名が不要||
||insert into TB名(FIELD1, FIELD3,FIELD5) values(FIELD1入力値, FIELD3入力値, FIELD5入力値);|指定したFIELDのみにRECORDを挿入||

### RECORD変更

||コマンド|役割|備考|
|:---|:---|:---|:---|
|*|全件変更|*|*|
||update TB名 set FIELD名 = '変更値'|FIELD名のデータ値を全件変更値に変更する||
|*|該当データのみ変更|*|*|
||update TB名 set FIELD名 = '変更値' where 条件|FIELD名のデータ値を条件に該当するデータのみ変更値に変更する||
|Ex|update customer set birthday = '19750501' where birthday = '19650501';|customerTABLEのbirthdayFIELDのデータが19650501に該当するデータのみ19750501に変更する||

### RECORD削除
### （1RECORD分、1行分、1件分）

||コマンド|役割|備考|
|:---|:---|:---|:---|
||delete from TB名 where 条件;|条件に該当するデータを削除する||



## トランザクション

||コマンド|役割|備考|
|:---|:---|:---|:---|
||start transaction;|トランザクションを有効にする||
||rollback; |条件に該当するデータを削除する||
||commit;|条件に該当するデータを削除する||
|※|イメージとして|start transactionを宣言してその時のデータを抜き出す。rollbackは抜き出したデータを破棄する。commitで抜き出したデータを格納する。|※|