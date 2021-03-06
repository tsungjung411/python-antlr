
### 不合文法的 [String.g4](../example/001-String.md)

```g4
grammar String;

start
	: (string|.)* EOF
	;

string
	: STRING
	;

STRING
	: '"' ('\\"' | .)*? '"'
	;
```
* ```start``` parser rule 使用了萬用字元
* i.e. 沒有定義 ANYCHA

<br>

**編譯訊息：**
```
warning(131): String.g4:4:13: greedy block ()* contains wildcard; 
    the non-greedy syntax ()*? may be preferred
```
 - 即使將 ```(string|.)*``` 改成 ```(string|.)*?```，錯誤結果仍一樣

<br>

**執行結果：**
```
line 1:5 token recognition error at: ' '
line 1:11 token recognition error at: ' '
line 1:17 token recognition error at: '\n'
line 2:0 token recognition error at: ' '
line 2:14 token recognition error at: ' '
line 2:17 token recognition error at: '\n'
(start (string "123") (string "abc") (string "456") (string "\"xyz\"7890") (string "") <EOF>)
```

- parser 除了處理 變數(parser-rule identifier) 和 字元(char) (e.g. '"', '[', ']')
- 並**不處理萬用字元(wildcard)**，所以會直接丟出 error

<br>

```g4
grammar String;

start
	: (string|ANYCHAR)* EOF
	;

string
	: stringBody
	;

stringBody
	: '"' ('\\"' | .)*? '"'
	;

ANYCHAR
	: .
	;
```
- 取自  [String.g4](../example/001-String.md)
- 把 STRING 改名成 stringBody
- stringBody 雖然有萬用字元，但是它是搭配 reluctant quantifier，這樣好像就 OK
