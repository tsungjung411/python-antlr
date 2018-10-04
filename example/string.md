
### 測試資料：
```
 "123" "abc" "456"
  "\"xyz\"7890" ""
```

### 執行結果：
```
(start   (string "123")   (string "abc")   (string "456") \n     (string "\"xyz\"7890")   (string "") \n)
```

### ANTLR: String.g4
```g4
grammar String;

start
	: (string|ANYCHAR)*
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
[沒有定義 ANYCHAR](../001-沒有定義 ANYCHAR.md)

<br>
<hr>
<br>

### 沒有使用 greedy quantifier '?' (貪婪量詞)
```g4
grammar String;

start
	: (string|ANYCHAR)*
	;

string
	: STRING
	;

STRING
	: '"' ('\\"' | .)* '"'
	;

ANYCHAR
	: .
	;
```

執行結果：
```
warning(131): Test.g4:12:18: greedy block ()* contains wildcard; the non-greedy syntax ()*? may be preferred

(start   (string "123" "abc" "456"\n  "\"xyz\"7890") \n)
```
只辨識到一個 string


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
