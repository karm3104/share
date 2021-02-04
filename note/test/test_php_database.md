# テスト

## データベースの正規化

非正規型  
  ↓  
  ↓   繰返し項目をそれぞれ別レコードとして独立させること  
  ↓   
第1正規形  
  ↓   
  ↓ 部分従属している部分を別テーブルとする（主キーの項目の一部により決定する項目の関係）  
  ↓ ※リレーションと呼ぶ  
第2正規形  
  ↓   
  ↓ 推移従属している項目を別項目とする  
  ↓   
第3正規形

## データベースとは

ひとつのデータベースに様々な関連するテーブルが一つにまとまっている物を指す  

MYSQLはリレーショナルデータベース管理システム（RDBMS）であり表形式である。

列 = フィールド（項目） = カラム
行 = レコード = タプル
※1レコードで一件となる

## リレーショナルデータベースの表操作

### 選択
行の抽出（全ての列の情報を、選択した行に合致する中身だけ取り出す）  
射影（表の中から必要な列だけ指定して、表から取り出す操作。行の内容は入ってこない）
結合（複数の表（テーブル）から1つの表にする操作：where innerjoin a.c = b.cなど）

## SQLコマンド

### インサート文
```

※追加系
insert into TB名 values(,入力値,入力値,…);    
        RECORD一括挿入、全項目入力時のみFIELD名が不要
create database DB名
        DATABASEの新規作成
create table TB名 (FIELD名 型(桁数),…);	
        field、型を指定してTABLEを作成
desc TB名;
    	TABLEの型、FIELD項目、名前の確認

※削除系
drop databasee DB名;
    	指定したDATABASE全体を削除	 
drop table TB名;
        指定したTABLE全体を削除	 
drop table if exists TB名; 
        指定したTABLEが存在すれば対象を削除	 
delete from TB名;   
    	TABLEのRECORDだけを削除	 
alter table TB名 drop FIELD名  
     	指定したTABLEの指定したFIELDを削除

※コピー系
create table 新TB名 select * from コピー元TB名
        TABLEの完全コピー	FIELDも中身も取ってくる
create table 新TB名 like コピー元TB名
    	コピー元のFIELD構造だけをコピー	主キーなど属性もコピー
insert into 既存TB名 select * from コピー元TB名
    	他TABLEのRECORDをコピー	構造が互いに同じであること
insert into 既存TB名 select * from コピー元TB名
    	特定のFIELDのデータをコピー	 
```

```
主キーの設定
        createttableのときに、FIELD名のところでprimary keyを指定する。
ユニークキー
        unique。重複できない制限をかける（nullの入力は可能）
結合
union => 大量のデータを処理する際使う。単純にデータをくっつける。
inner join =>内部結合。一致するレコードを取り出すような結合

```

```
where句

select * from TB名 where FIELD名>=100;
    	TB全てのデータから「FIELDのデータが100以上」のものを抽出

	=	等しい	 
 	>	より大きい	 
 	>=	以上	 
 	<	より小さい	 
 	=<	以下	 
 	<>	とは異なる	 
 	in(O,O,…)	oかoのいずれかと等しい	 
 	not in(O,O,…)	oかoのいずれも等しくない	 
 	between a and b	aからbの範囲内	 
 	not between a and b	aからbの範囲内外


 	where FIELD名 like 条件	あいまい検索	like
 	select * from TB名 where FIELD名 like 条件	
        TB全てのデータからFIELD内で条件に合うもの	 
 	‘%a’	文字列’a’で終わる	 
 	‘a%’	文字列’a’で始まる	 
 	‘%a%’	文字列’a’がどこかに含まれる	 
 	’%%’	文字列なんでもOK	?
ワイルドカード
 	コマンド	役割	備考
 	%	任意の文字列	 
Ex	%県	埼玉県、廃藩置県、…	 
 	＿	任意の1文字が該当	 
Ex	長_県	長崎県、長い県、…	
```

セレクトの中にセレクト
ビュー場面

トランザクション
ロールバック
コミット