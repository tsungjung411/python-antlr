
### input.txt
```
 "123" "abc" "456"
  "\"xyz\"7890"
```

### ANTLR: String.g4
```g4
grammar String;

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

### Results:
```
(start   (string "123")   (string "abc")   (string "456") \n     (string "\"xyz\"7890") \n)
```
