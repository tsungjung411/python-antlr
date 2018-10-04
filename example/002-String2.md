
### [001-String.md] 的加強版

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
	: '"' ('\\"' | ~["])* '"'
	;

ANYCHAR
	: .
	;
```


STRING
- 從 ```'"' ('\\"' | .)*? '"'```
- 變更
- 為 ```'"' ('\\"' | ~["])* '"'```

說明：
- 不需要「勉強量詞(reluctant quantifier)」
- 「wildcard」 改成 「只要不是 " 的字元，我就一直吃，直到遇到 " 就跳出」
