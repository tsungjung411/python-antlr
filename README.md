Here we provide some simple ANTLR examples.
<br>在這邊我們提供一些簡單的 ANTLR 範例。

使用版本：antlr-4.7.1-complete.jar

<br>

基本認知：
- 特性：
  - 使用 regex / reg-exp / regular expression 基本語法
  - 與上下文無關的文法
    - 意思是結構當下就決定，不會因為前後關係而產生結構變化
    - 全台大停電："全台/大/停電", "全/台大/停電"
    - 當天才知道："當天/才/知道", "當/天才/知道"
    - 漁民捕魚的地方：
      - (漁民 n.)/(捕魚 v.) -> 打中 adj = n. + v. + '的' (形容詞規則)
      - (漁民 n.)/(捕魚 n.) -> 打中 n. = n. + n (複合名詞規則) -> 執行沒有意義
      - 從字面上無法決定結構，必須要在根據詞彙意義才能進行組裝
      - 所以 ANTLR 並無法處理「上下文有關」的語法

- 檔案：
  - 檔名：```Xxx.g4```
  - 內部的 grammer 宣告為：```Grammar Xxx;```  （概念同 Java, 主 class 名稱與檔名必須一致）
  
- 變數：
  - parser 變數
    - 小寫開頭的識別字，表示 parser (語法分析器)
    - 例如 number, string, classBody, xABC
    - 語法分析器 syntactic analyzer，以 parser 來稱呼
    - parser 所定義的規則稱為 parser rule
    - parser rule 不可以是純字元，否則會有編譯錯誤，此時應該當作 lexer<br><br>
    
  - lexer 變數
    - 大寫開頭的識別字，表示 lexer (詞法分析器)
    - 例如 Number, NUMBER, String, STRING, ANY_CHAR, AnyChar, WS (表示 WhiteSpace)
    - 詞法分析器 lexical analyzer，簡稱 lexer
    - lexer 所定義的規則稱為 lexer rule
    - lexer rule 不可以含有 parser (不可以含有變數)，否則會有編譯錯誤，此時應該當作 parser<br><br>
  
- 串流(stream)
  - char stream -> lexer -> token stream -> parser -> tree
  - 輸入字元(char) -> lexer(詞法分析器) -> 輸出標記(token)
  - 輸入標記(token) -> psrser(語法分析器) -> 輸出標記的結構樹(token tree)

- 正規表達式 (Regex)
  - 預設模式：
    - 貪婪量詞(greedy quantifier)
  - 有支援：
    - 勉強量詞(reluctant quantifier)
    - 亦即，非貪婪模式 -> the non-greedy syntax ```()*?```
  - 不支援：
    - 獨占模式(possessive quantifier)
    - 不支援字元否定[^]，改用 ~ (not 運算子)<br>(~x operator matches anything but x)
<br>

### 參考資料
 - [[wiki] 詞法分析](https://zh.wikipedia.org/zh-tw/%E8%AF%8D%E6%B3%95%E5%88%86%E6%9E%90)
 - [[wiki] 語法分析器](https://zh.wikipedia.org/wiki/%E8%AA%9E%E6%B3%95%E5%88%86%E6%9E%90%E5%99%A8)
 - [ANTLR Examples for Python](https://github.com/jszheng/py3antlr4book)

### 正規表達式
 - [貪婪、勉強、獨占量詞的差別](https://www.cnblogs.com/ggicci/archive/2012/09/18/2690804.html)
 - [Java 正規表達式](https://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html)
