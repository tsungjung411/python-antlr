
### 測試資料：
```
|123| |abc| |456|
 |\|xyz\|7890| ||
```

### 執行結果：
```
(start (string |123|)   (string |abc|)   (string |456|) \n   (string |\|xyz\|7890|)   (string ||) \n <EOF>)
```

### ANTLR: String.g4 (第一種解法)
```g4
grammar String;

start
	: (string|ANYCHAR)* EOF
	;

string
	: STRING
	;

STRING
	: '|' ('\\|' | .)*? '|'
	;

ANYCHAR
	: .
	;
```
- 同 [001-String.md](../example/001-String.md)

<br>

### ANTLR: String.g4 (第二種解法)
```g4
grammar String;

start
	: (string|ANYCHAR)* EOF
	;

string
	: STRING
	;

STRING
	: '|' ('\\|' | ~[|])*? '|'
	;

ANYCHAR
	: .
	;
```
- 同 [002-String.md](../example/002-String.md)
- 將 ```.``` 換成 ```~[|]```

