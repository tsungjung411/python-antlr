Here we provide some easy ANTLR examples.
在這邊我們提供一些簡單的 ANTLR 範例。

基本認知：
- 檔案：
  - 檔名：```Xxx.g4```
  - 內部的 grammer 宣告為：```Grammar Xxx;```  （概念同 Java, 主 class 名稱與檔名必須一致）
  
- 變數：
  - 小寫開頭的識別字，表示 parser(語法分析器)，例如 number, string, classBody
  - 語法分析器 syntactic analyzer，簡稱 parser
  - parser 所定義的規則稱為 parser rule
  - parser rule 不可以是純字元，否則會有編譯錯誤，此時應該當作 lexer<br><br>
  
  - 大寫開頭的識別字，表示 lexer(詞法分析器)，例如 Number, NUMBER, String, STRING, ANYCHAR, WS (表示 WhiteSpace)
  - 詞法分析器 lexical analyzer，簡稱 lexer
  - lexer 所定義的規則稱為 lexer rule
  - lexer rule 不可以含有 parser (不可以含有變數)，否則會有編譯錯誤，此時應該當作 parser<br><br>
  
- 串流(stream)
  - char stream -> lexer -> token stream -> parser -> tree
  - 輸入字元(char) -> lexer(詞法分析器) -> 輸出標記(token)
  - 輸入標記(token) -> psrser(語法分析器) -> 輸出標記的結構樹(tree)
