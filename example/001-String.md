
### 測試資料：
```
"123" "abc" "456"
 "\"xyz\"7890" ""
```

### 執行結果：
```
(start (string "123")   (string "abc")   (string "456") \n   (string "\"xyz\"7890")   (string "") \n <EOF>)
```

### ANTLR: String.g4
```g4
grammar String;

start
	: (string|ANYCHAR)* EOF
	;

string
	: STRING
	;

STRING
	: '"' ('\\"' | .)*? '"'
	;

ANYCHAR
	: .
	;
```

### Error Study
 - [parser不處理萬用字元](../error_study/001-parser不處理萬用字元.md)
 - [沒有使用貪婪量詞'?'](../error_study/002-沒有使用貪婪量詞'%3F'.md)
 

<br>
<hr>
<br>

### 字串不能是以 'a' 開始
```g4
grammar String;

start
	: (string|ANYCHAR)*
	;

string
	: STRING
	;

STRING
	: '"' ('\\"' | ~[a])* '"'
	;

ANYCHAR
	: .
	;
```

執行結果：
```
(start   (string "123")   " a b c (string " ") 4 5 6 (string "\n  ") \ (string "xyz\"7890") \n)
```
"abc 被跳過，導致後面都錯位
```
 "123" "abc" "456"
 ^^^^^     ^^^   ^

  "\"xyz\"7890"
  ^ ^^^^^^^^^^^
```
