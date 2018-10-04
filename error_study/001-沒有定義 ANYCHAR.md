
### 不合文法的 [String.g4](../example/string.md)

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
沒有定義 ANYCHA

<br>

**編譯訊息：**
```
warning(131): Test.g4:4:13: greedy block ()* contains wildcard; 
    the non-greedy syntax ()*? may be preferred
```
 - 即使將 ```string|.)*``` 改成 ```string|.)*?```，錯誤結果仍一樣

<br>

**執行結果：**
```
line 1:0 token recognition error at: ' '
line 1:6 token recognition error at: ' '
line 1:12 token recognition error at: ' '
line 1:18 token recognition error at: '\n'
line 2:0 token recognition error at: ' '
line 2:1 token recognition error at: ' '
line 2:15 token recognition error at: ' '
line 2:18 token recognition error at: '\n'
(start (string "123") (string "abc") (string "456") (string "\"xyz\"7890") (string ""))
```

- parser 除了處理 變數(parser rule) 和 字元(char) (e.g. '"', '[', ']')
- 並不處理萬用字元(wildcard)，所以會直接丟出 error
