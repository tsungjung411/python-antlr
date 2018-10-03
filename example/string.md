
### 測試資料
```
 "123" "abc" "456"
  "\"xyz\"7890"
```

### ANTLR: Test.g4
```g4
grammar Test;

start : (string|ANYCHAR)*;


string
	: String
	;

String
	: '"' ('\\"' | .)*? '"'
	;

ANYCHAR
	: .
	;

```
