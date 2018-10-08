
### 測試資料：
```
[123] [abc] [456]
 [\[xyz\]7890] []
```

### 執行結果：
```
(start (string [123])   (string [abc])   (string [456]) \n   (string [\[xyz\]7890])   (string []) \n <EOF>)
```

### ANTLR: String.g4
```g4
grammar String;

start
	: (string|ANYCHAR)* EOF
	;

string
	: StringBody
	;

StringBody
	: '[' ('\\[' | '\\]' | ~('[' | ']'))* ']'
	;

ANYCHAR
	: .
	;
```
- \[...\] 字串裡，可以包含巢狀 [，使用逸出序列 \\[ 表達
- \[...\] 字串裡，可以包含巢狀 ]，使用逸出序列 \\] 表達
- \[...\] 字串裡，如果遇到非 \[ 或是 \] 字元，字串可以繼續延伸下去
