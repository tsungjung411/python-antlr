
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
	: (STRING|ANYCHAR)*
	;

STRING
	: '"' ('\\"' | .)*? '"'
	;

ANYCHAR
	: .
	;
```

<hr>

### 不合文法的 String.g4
```g4
grammar String;

start
	: (STRING|.)*
	;

STRING
	: '"' ('\\"' | .)*? '"'
	;
```

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

<hr>

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
