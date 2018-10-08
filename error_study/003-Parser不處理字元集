
### 不合文法的 [String2.g4](../example/002-String2.md)

```g4
grammar String;

start
	: (string|ANYCHAR)* EOF
	;

string
	: stringBody
	;

stringBody
	: '"' ('\\"' | ~["])* '"'
	;

ANYCHAR
	: .
	;
```
STRING 改名為 stringBody

<br>

**編譯訊息：**
```
error(50): String.g4::: syntax error: mismatched character '<EOF>' expecting '''
error(50): String.g4:18:0: syntax error: '<EOF>' came as a complete surprise to me while looking for rule element
```
- 字元集(charset)類似萬用字元(wildcard)的概念，只是限定或排除了一些字元
- parser 除了處理 變數(parser-rule identifier) 和 字元(char) (e.g. '"', '[', ']')
- 並不處理字元集(charset)、萬用字元(wildcard)，所以會直接丟出 error
