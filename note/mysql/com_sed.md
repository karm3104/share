# 検索・抽出・表示・複数TABLE利用　コマンド集


## ページ内リンク

|中項目|小項目|
|:---|:---|
|[表示系コマンド](#表示系コマンド)|[エイリアス ( as ) ](#エイリアス)/  [四則演算](#四則演算)|
|[条件指定検索](#条件指定検索)|[条件検索 ( WHERE ) ](#WHERE条件検索/)/  [比較演算子 ](#比較演算子)/  [文字列検索 ( LIKE検索 ) ](#文字列検索)/ [ワイルドカード ( %, _ ) ](#ワイルドカード)/ [NULLを利用した検索( IS NULL ) ](#NULLを利用した検索)/  [複数条件の組み合わせ検索 ( AND, OR ) ](#複数条件の組み合わせ検索)/  [並べ替え出力 ( asc, desc ) ](#並べ替え出力)|
|[グループ毎に表示](#グループ毎に表示)|[グループ検索( GROUP BY ) ](#グループ検索)/ [条件付きグループ検索(HAVING ) ](#条件付きグループ検索)|
|[複数TABLEの利用](#複数TABLEの利用)|[内部結合・外部結合 ( INNER JOIN, OUTER JOIN ) ](#内部結合・外部結合)|




## 一連の流れ

||コマンド|役割|備考|
|:---|:---|:---|:---|
||mysql -u root -p|ログインコマンド（-u:ユーザー指定、-p:パスワード…ここブランクエンターで次で入力）||
||show database();|DATABASEの中身確認||
||use DB名|対象DATABASEに移動||
||show tables;|TABLEの中身確認||
||desc TABLE名;|TABLEの型、FIELD項目、名前の確認||
|※|set names cp932;|日本語使うときは入れるときも出すときも必須！(文字化けを防ぐ)|※|
||select * from TABLE名|TABLEの中身の確認||



## 表示系コマンド

||コマンド|役割|備考|
|:---|:---|:---|:---|
||select FIELD名2,FIELD名3,FIELD名1 from TB名;|FIELDを入れ替えて表示する||
||select FIELD名2,FIELD名3,FIELD名2,…,from TB名 from TB名;|連続して表示も可能||

### エイリアス

||コマンド|役割|備考|
|:---|:---|:---|:---|
||select FIELD名 as 置換後FIELD名 from TB名;|出力時にFIELD名を置き換える||
||select FIELD名*1000 as 置換後FIELD名 from TB名;|出力時にFIELDのデータを*1000した上でFIELD名を置き換える||

### 四則演算

||コマンド|役割|備考|
|:---|:---|:---|:---|
||select FIELD名1+FIELD名2 from TB名;|TB名のFIELD1とFIELD2を足す|+|
||select FIELD名1-FIELD名2 from TB名;|TB名のFIELD1とFIELD2を引く|-|
||select FIELD名1*FIELD名2 from TB名;|TB名のFIELD1とFIELD2をカケル|*|
||select FIELD名1/FIELD名2 from TB名;|TB名のFIELD1とFIELD2を割る|/|

### 関数

||コマンド|役割|備考|
|:---|:---|:---|:---|
||select avg(FIELD名) from TB名;|FIELD名の平均値を表示|**avg**|
||select sum(FIELD名) from TB名;|FIELD名の合計値を表示|**sum**|
||select count(FIELD名) from TB名;|FIELD名の件数を表示|**count**|
||select min(FIELD名) from TB名;|FIELD名の最小値を表示|**min**|
||select max(FIELD名) from TB名;|FIELD名の最大値を表示|**max**|
||select FIELD名1,FIELD名2,FIELD名3, concat(FIELD名1,FIELD名2) from TB名;|FIELD1,2,3からFIELD1,2を結合して表示|**concat**|
||select FIELD名1,FIELD名2,FIELD名3, substring(FIELD名1, 2, 3) from TB名;|FIELD1のデータの２桁目から３桁分を取り出して表示|**substring**|
||insert into TB名(FIELD名) values(now());|日時の取得|**now()**|



## 条件指定検索

||コマンド|役割|備考|
|:---|:---|:---|:---|
||select FIELD名 from TB名 limit 3;|TB名のFIELDの先頭のデータから3つ取り出し||
||select FIELD名 from TB名 limit 3 offset 4;|TB名のFIELDの4つ目のデータから3つ取り出し||

### WHERE条件検索

||コマンド|役割|備考|
|:---|:---|:---|:---|
||select * from TB名 where FIELD名>=100;|TB全てのデータから「FIELDのデータが100以上」のものを抽出||

### 比較演算子

||コマンド|役割|備考|
|:---|:---|:---|:---|
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

### 文字列検索

||コマンド|役割|備考|
|:---|:---|:---|:---|
||where FIELD名 **like** 条件|あいまい検索|**like**|
||select * from TB名 where FIELD名 like 条件 |TB全てのデータからFIELD内で条件に合うもの||
||'%a'|文字列'a'で終わる||
||'a%'|文字列'a'で始まる||
||'%a%'|文字列'a'がどこかに含まれる||
||'%%'|文字列なんでもOK|?|

### ワイルドカード

||コマンド|役割|備考|
|:---|:---|:---|:---|
||%|任意の文字列||
|Ex|%県|埼玉県、廃藩置県、…||
||＿|任意の1文字が該当||
|Ex|長_県|長崎県、長い県、…||

### NULLを利用した検索

||コマンド|役割|備考|
|:---|:---|:---|:---|
||select * from TB名 where FIELD名 is null;|TB全てのデータからFIELD内でNULLの項目を表示(**isは必ず入力**)||
||select * from TB名 where FIELD名 is not null;|TB全てのデータからFIELD内でNULLではない項目を表示(**isは必ず入力**)||

### 複数条件の組み合わせ検索

||コマンド|役割|備考|
|:---|:---|:---|:---|
||select * from TB名 where 条件 比較演算子 条件|||
|Ex|select * from TB名 where FIELD名>=50 and FIELD名<=100|FIELDのデータが50以上かつ100以下のものを検索||
|※|※ORとANDの優先順位|※ANDが優先されるためOR優先したい場合はカッコで囲って先に処理させる|※|

### 並べ替え出力

||コマンド|役割|備考|
|:---|:---|:---|:---|
||select * from TB名 order by FIELD名 asc;|TB全てのデータからFIELD内データを昇順で表示||
||select * from TB名 order by FIELD名 desc;|TB全てのデータからFIELD内データを降順で表示||
|※|**指定なしでも昇順で表示される**|**降順の際は必ず「desc」をつける。limit指定で上位○個表示も可能**|※|



## グループ毎に表示

### グループ検索

||コマンド|役割|備考|
|:---|:---|:---|:---|
||select FIELD名 from TB名 group by FIELD名|FIRLDデータの重複分をまとめて表示。他項目はテキトーなものを表示||
|*|**件数**|*|*|
||select FIELD名 count(*) as 件数 from TB名 group by FIELD名|TBのFIELD名をまとめて、FIELDごとのcount数を件数として表示||
|*|**合計値**|*|*|
||select FIELD名 sum(FIELD2) as 合計 from TB名 group by FIELD名|TBのFIELD名のデータ重複をまとめて、FIELD2のsum値を合計として表示||
|*|**平均値**|*|*|
||select FIELD名 avg(FIELD2) as 平均 from TB名 group by FIELD名|TBのFIELD名のデータ重複をまとめて、FIELD2のavg値を平均として表示||
|*|**件数・合計・平均値**|*|*|
||select FIELD名 count(*) as 件数 sum(FIELD2) as 合計 avg(FIELD2) as 平均 from TB名 group by FIELD名|TBのFIELD名のデータ重複をまとめて、重複分をcountとして件数に出力して、FIELD2のsum値を合計、avg値を平均としてそれぞれ表示||
|※|**group byを使うときにselectで指定できる項目は**|**group byで指定したFIELDか、関数で呼び出して計算したFIELDのみ可能！**|※|

### 条件付きグループ検索

||コマンド|役割|備考|
|:---|:---|:---|:---|
||select FIELD名,sum(FIELD2) from TB名 group by **having sum(FIELD2)>=200**;|FIELDデータ毎にまとめるが、表示するのはFIELD2の合計が200以上のみ||
|Ex|select FIELD名 avg(FIELD2) as 平均 from TB名 where FIELD2>=50 **group by FIELD名** habving avg(FIELD2)>=100 **order by avg(FIELD2) desc FIELD名;**|FIELDデータ毎にまとめるが、表示するのは、FIELD2が50以上のもので→**FIELD名データをwhereで集約**→かつFIELD2が100以上のデータをhavingでまとめたものを→**avg値を平均とした上で大きい順にFIELD名のデータとして出力**||
|※|where→group by→havingの順番は覚える|where(で絞った条件の結果を)group by(でグループ内重複があったらまとめて)having(でグループ内を条件で検索する)|※|




## 複数TABLEの利用

||コマンド|役割|備考|
|:---|:---|:---|:---|
||select * from TB1 union select from TB2|TB1とTB2を単純に合わせて出力する||

### 内部結合・外部結合

||コマンド|役割|備考|
|:---|:---|:---|:---|
|*|**内部結合**|*|*|
||INNER JOIN|内部結合||
|Ex|select * from TB1 inner join TB2 on TB1.bang = TB2.bang|TB1とTB2を結合して、TB1.bangとTB2.bangが一致するものだけを、全FIELD分出力||
|Ex|select TB1.bang, TB2.nama, from TB1 inner join TB2 on TB1.bang = TB2.bang|TB1とTB2を結合して、TB1.bangとTB2.bangが一致するものだけを、TB1.bangとTB2.namaのFIELDデータ分出力||
|*|**外部結合**|*|*|
||LEFT OUTER JOIN|一致したレコード及び下の例のTB1(左側)の全データを表示||
||RIGHT OUTER JOIN|一致したレコード及び下の例のTB2(右側)の全データを表示||
|Ex|select * from TB1 left outer join TB2 on TB1.bang = TB2.bang|TB1とTB2を結合して、TB1.bangとTB2.bangが一致するものとTB1の全データを、全FIELD分出力|||||

<!-- ## 雛形

||コマンド|役割|備考|
|:---|:---|:---|:---|
|||||
|||||
|||||
|||||
||||| -->
