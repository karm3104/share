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
|||||
|*|**エイリアス**|*|*|
||select FIELD名 as 置換後FIELD名 from TB名;|出力時にフィールド名を置き換える||
||select FIELD名*1000 as 置換後FIELD名 from TB名;|出力時にフィールドのデータを*1000した上でFIELD名を置き換える||
|||||
|*|**四則演算**|*|*|
||select FIELD名1+FIELD名2 from TB名;|TB名のFIELD1とFIELD2を足す||
||select FIELD名1-FIELD名2 from TB名;|TB名のFIELD1とFIELD2を引く||
||select FIELD名1*FIELD名2 from TB名;|TB名のFIELD1とFIELD2をカケル||
||select FIELD名1/FIELD名2 from TB名;|TB名のFIELD1とFIELD2を割る||
|||||
|*|**関数**|*|*|
||select avg(FIELD名) from TB名;|FIELD名の平均値を表示|**avg**|
||select sum(FIELD名) from TB名;|FIELD名の合計値を表示|**sum**|
||select count(FIELD名) from TB名;|FIELD名の件数を表示|**count**|
||select min(FIELD名) from TB名;|FIELD名の最小値を表示|**min**|
||select max(FIELD名) from TB名;|FIELD名の最大値を表示|**max**|
||select FIELD名1,FIELD名2,FIELD名3, concat(FIELD名1,FIELD名2) from TB名;|FIELD1,2,3からFIELD1,2を結合して表示|**concat**|
||select FIELD名1,FIELD名2,FIELD名3, substring(FIELD名1, 2, 3) from TB名;|FIELD1のデータの２桁目から３桁分を取り出して表示|**substring**|
||insert into TB名(FIELD名) values(now());|日時の取得|**now()**|
|||||
|||||


## 条件指定検索

||コマンド|役割|備考|
|:---|:---|:---|:---|
||select FIELD名 from TB名 limit 3;|TB名のFIELDの先頭のデータから3つ取り出し||
||select FIELD名 from TB名 limit 3 offset 4;|TB名のFIELDの4つ目のデータから3つ取り出し||
|||||
|*|**WHERE条件選択**|*|*|
||select * from TB名 where FIELD名>=100;|TB全てのデータから「FIELDのデータが100以上」のものを抽出||
|||||
|*|**比較演算子**|*|*|
||=|等しい||
||>|より大きい||
||>=|以上||
||<|より小さい||
||=<|以下||
||<>|とは異なる||
||in(O,O,...)|oかoのいずれかと等しい||
||not in(O,O,...)|oかoのいずれも等しくない||
||between a and b|aからbの範囲内||
||not between a and b|aからbの範囲内外||
|||||
|*|**文字列検索**|*|*|
||select * from TB名 where FIELD名 like 条件 |TB全てのデータからFIELD内で条件に合うもの||
||'%a'|文字列'a'で終わる||
||'a%'|文字列'a'で始まる||
||'%a%'|文字列'a'がどこかに含まれる||
||'%%'|文字列なんでもOK|?|
|||||
|*|**ワイルドカード**|*|*|
||%|任意の文字列||
|Ex|%県|埼玉県、廃藩置県、…||
||＿|任意の1文字が該当||
|Ex|長_県|長崎県、長い県、…||
|||||
|*|**NULLを利用した検索**|*|*|
||select * from TB名 where FIELD名 is null;|TB全てのデータからFIELD内でNULLの項目を表示(**isは必ず入力**)||
||select * from TB名 where FIELD名 is not null;|TB全てのデータからFIELD内でNULLではない項目を表示(**isは必ず入力**)|||*|**複数条件の組み合わせ検索**|*|*|
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