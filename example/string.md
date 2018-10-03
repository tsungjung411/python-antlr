
### 測試資料：
```
 "123" "abc" "456"
  "\"xyz\"7890"
```

### 執行結果：
```
(start   (string "123")   (string "abc")   (string "456") \n     (string "\"xyz\"7890") \n)
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

<br>
<hr>
<br>

### 不合文法的 String.g4
```g4
grammar String;

start
	: (string|.)*
	;

string
	: STRING
	;

STRING
	: '"' ('\\"' | .)*? '"'
	;
```
沒有定義 ANYCHAR

<br>

執行結果：
```
line 1:0 token recognition error at: ' '
line 1:6 token recognition error at: ' '
line 1:12 token recognition error at: ' '
line 1:18 token recognition error at: '\n'
line 2:0 token recognition error at: ' '
line 2:1 token recognition error at: ' '
line 2:15 token recognition error at: '\n'
(start "123" "abc" "456" "\"xyz\"7890")
```

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
