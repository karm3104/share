# PHPまとめ　＆　気づき　2日目

## 変数
プログラムの値をメモリの一部に確保する箱（領域）の宣言  
PHPの場合は必ず「＄」を頭につけて宣言する。

＠例    
変数strを宣言して「こんにちは」を代入。echoで呼び出し

```
<?php $str = "こんにちは";?>

<?echo $str;?>
上と下は同じ結果を出力
<? = str; ?>
```

※ほかの言語やった後とか＄を忘れやすいので注意

※変数に変数を代入することも可能

```
$const = "こんにちは"
$str = $const;
echo $str

	>>こんにちは
```

## 変数名のルール

```
$_ｘｘｘｘ    
```

**※先頭は「アルファベット」「アンダーバー」を使う。**    
**※以降は英文字、数字を使える**    
**※2つ以上の単語の場合**    
**2つ目以降の単語の頭文字を大文字にする！（ルール）**

## 文字列とは

```
123(数値)

"123"（文字列、数字）
```

### 文字列の結合

```
echo "こんにちは". "はじめまして"
echo $str. $const;
＠関数に関数を結合して代入する
$1 = $str. $const;
```

## 数値

### 型

```
文字列 ”123”    
数値 123    
論理値 true, false    
```

### 四則演算

```
+ : 足し算
- : 引き算
* : 掛け算
/ : 割り算
% : 割り算の余り

割り算の時、「０」で割ると異常終了する
変数の値の時とか注意すること！！
```

ex)
関数
```
if(is_numeric($num1)){
	$num1_1 = intval($num1);
}

is_numeric : 
intval : 
```



### 比較演算子

**出力は必ずTRUE か FALSE のどちらかになる。**

```
a { >（より大きい）,>=（以上）,<（）,<=（以下）,==（等しい）,!=（等しくない） } b

※  === : 値が等しくて型も等しい
※  !== : 値と型、どちらかが等しい
```

### 条件の組み合わせ

**条件文の出力は必ずTRUE か FALSE のどちらかになる。**

```
and => かつ = &&
or  => もしくは = ||

＠例
条件1 && 条件2 || 条件3
	>>条件1かつ条件2または条件3

```


## -if -elseif文

### if文

```
if($a = $b){
	[trueの処理]
}else{
	[falseの処理]
}
```

### -elseif文

```
if(条件1){
	[trueの処理]
}elseif(条件2){
	[条件2の処理]
}elseif(条件3){
	[条件3の処理]
}elseif(条件4){
	[条件4の処理]
}
```

### -ifif文 (基本的には使わない)

```
if(条件1){
	if(条件1){
		if(条件1){
			[]
		}
	}
}
```

### switch文
一つの変数、一つの答え（イコール文）しか書けない

```
switch($value){
	case "A":
		echo [A];
		break;
	case "B":
		echo [B];
		break;
	default:
	  echo [D];
}

```


## 繰り返し処理

### for文

```
@例
for($i=0; $i<=3; $i++){
	処理
}
```

### while文 

```
while(条件){
	処理
}

while($i <= 5){
	echo $i. "回目の繰り返し<br>";
	$i++;
}

```

### while文その他の書き方


```

@普通の書き方
		<?php
		$i = 1;
		while ( $i <= 5 ) {
			echo "<tr>";
			echo "<td>". $i. "回目の繰り返し</td>";
			echo "</tr>";
			$i++;
		}
		?>

@echoを省略した書き方（閉じタグの位置や生のHTML部分（<tr>~<tr>部分）、
echoがない書き方など使うこともあるので覚えておく！）
＠phpの構文（言語）部分を<??>で囲んでいたらOK?
		<?php
		$i = 1;
		while ( $i <= 5 ) {
		?>
			<tr><td><?= $i?>回目の繰り返し</td></tr>
		<?php
		$i++;
		}
		?>
```

### BREAKやCONTINUEで処理を止める

break

continue

```

		<?php
		for ( $i = 1; $i <= 10; $i++ ) {
			if ( $i == 5 ) {
				break;
			}
			echo $i. "回目の繰り返し<br>";
		}		
	  ?>
	＞＞5回目の処理で抜ける

		<hr>
		<?php 
		for ( $i = 1; $i <= 10; $i++ ) {
			if ( $i == 5 ) {
				continue;
			}
			echo $i. "回目の繰り返し<br>";
		}
		?>
			＞＞5回目の処理はスキップして続ける


		<?php
		$i = 0;
		while ( $i <= 5 ) {
			$i++;
			if ($i == 3){
			continue;
			}
			echo $i. "回目の繰り返し<br>";
			if ($i == 5){
				break;
			}
		}
		?>
			＞＞3回目の処理はスキップして5回目の処理で抜ける
```

## 配列

### 配列の作成 

```
$numbers = [1,2,3,4]    

これのキーは0,1,2,3    

これのバリューは1,2,3,4    
```

### 配列に追加

```
$numbers[] = 5  
```

**phpの場合、自動で空いているキー（この場合4）に5を追加してくれる**

### 配列の繰り返し取り出し

**＠for文**  
```
for ($i = 0;$i<5;$i++){
	echo $numbers [$i]
}


＠count($numbers)変数で要素数を取得できる

for ($i = 0;$i<count($numbers);$i++){
	echo $numbers [$i]
}
```

**＠foreach文　　PHPの場合は主にこっち！**  

```
＠keyとvalueの取り出し

foreach($numbers as $key =>$value){
	echo "添字". $key. "番は";
	echo $value. "です。<br>";
}


＠valueのみ取り出し

foreach($numbers as $value){
	echo $value. "です。<br>";
}

※keyだけを取り出す場合はあまりない。
両方呼び出して片方echoするでもOK。
```


## チェックボックスと配列の関係



※name = skill[ ]の[ ]部分が配列でデータを送信することを示す。逆に[ ]が入ってないとエラーになる。  
**nameは同じ配列に入れたいためすべて同一の名前にする。**  
※value = "なにがし"は送りたい情報が決まっているため既に記入されている。


```
	<div class="container padding-y-20">
		<h4>スキルをチェックしてください。（複数選択可）</h4>
		<form action="checkbox.php" method="post">
			<label><input type="checkbox" name="skill[]" value="PHP"> PHP</label>
			<label><input type="checkbox" name="skill[]" value="HTML"> HTML</label>
			<label><input type="checkbox" name="skill[]" value="CSS"> CSS</label>
			<label><input type="checkbox" name="skill[]" value="その他"> その他</label>
			<input type="submit" class="btn" value="送信">
		</form>
	</div>


＠上で入力しないとskill[]が帰ってこないのでissetで関数が帰ってきているか調べる→なければ、ありませんが出力される。
※帰ってこずにブランクで表示されるため
		<?php
		if(isset($_POST["skill"])){
		  $skill = $_POST["skill"];
		  foreach($skill as $key => $value){
			     echo $value. "<br>";
		  }
		}else{
		    echo "ありません<br>";
		}
		?>
```
チェックボックスのみ配列で送られる。  
ラジオボタンなどは一つしか選べないためvalueの値は0,1のどちらかしかない
