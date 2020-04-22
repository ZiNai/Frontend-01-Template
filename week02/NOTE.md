# JavaScript 计算机语言基础

我的这块知识基本是空白，现在换个角度来学习前端，感觉非常不错

# 计算机语言通识

### 分类整理
1. - 非形式语言
     - 中文, 英文
   - 形式语言(乔姆斯基谱系)
     - 0型 无限制文法
      - \?::=?
     - 1型 上下文相关文法
      - \?\<A>\?::=?\<B>?
       - 2型 上下文无关文法
      - \<A>::=?
     - 3型 正则文法
      - \<A>::=\<A>?
      - \<A>::=?\<A> (不允许)
2. -  图灵完备性        
     - 命令式(图灵机)
       - goto
       - if 和 while
     - 声明式(lambada)
       - 递归
3. -类型系统
    - 动态类型系统与静态类型系统
   - 强类型与弱类型
   - 复合类型
     - 结构体
     - 函数签名
   - 子类型
     - 逆变/协变
   
### 产生式(BNF)
- 尖括号括起来的名称来表示语法结构名
- 语法结构分成基础结构和需要用其他语法结构定义的复合结构
  - 基础结构称终结符
  - 复合结构称非终结符
- 引号和中间的字符表示终结符
- 可以有括号
- *表示重复多次
- |表示或
- +表示至少一次
> 终结符: 不会变的字(关键字,字面量,符号等等不会变的东西)  
非终结符: 会变的字(变量)

> 其他产生式: EBNF ABNF ...

```bash
# 四则运算BNF
<Number> :: = "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"

<DecimalNumber> :: = "0" | (("1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9") <Number>*)

<PrimaryExpression> :: =
   <DecimalNumber> |
  "(" <LogicExpression> ")"

<MultiplicationExpression> :: =
  <PrimaryExpression> |
  <Multiplication> "*" <PrimaryExpression> |
  <Multiplication> "/" <PrimaryExpression>

<AdditionExpression> :: =
  <MultiplicationExpression> |
  <AdditionExpression> "+" <MultiplicationExpression> |
  <AdditionExpression> "-" <MultiplicationExpression>

<LogicExpression> :: =
  <AdditionExpression> |
  <LogicExpression> "||" <AdditionExpression> |
  <LogicExpression> "&&" <AdditionExpression>
```

### 图灵完备性
- 图灵完备性
  - 命令式(图灵机)
    - goto
    - if 和 while
  - 声明式(lambada)
    - 递归
> 简单的来说可编程的称之为图灵完备性,反之则不能,例如html,css

### 动态语言与静态语言
- 动态
> 运行时才知道数据类型
- 静态
> 编译时就知道数据类型

### 类型系统
- 动态类型系统与静态类型系统
- 强类型与弱类型
> 强类型指数据类型不能隐式转换,弱类型则可以.
- 复合类型
  - 结构体
  - 函数签名
- 子类型
  - 逆变/协变

# ECMAScript Language

### 一般命令式编程语言构成
  1. Atom
     - Identifier
     - Literal
  2. Expression
     - Atom
     - Operator
     - Punctuator
  3. Statement
     - Expression
     - Keyword
     - Punctuator
  4. Structure
     - Function
     - Class
     - Process
     - Namespace
  5. Program
     - Program
     - Mould
     - Package
     - Library

#### Atom Identifier & Literal

  - WhiteSpace
    - \<TAB\>：`\t`
    - \<VT\>： `\v`
    - \<FF\>：`\f` 
    - \<SP\>：`\s`
    - \<NBSP\>：NO-BREAK SPACE
    - \<ZWNBSP\>：ZERO WIDTH NO-BREAK SPACE
    - \<USP\>
  - LineTerminator
    - \<LF\>：`\n`
    - \<CR\>：`\r`
    - \<LS\>
    - \<PS\>
  - Comment
    - // comment
    - /* comment */
  - CommonToken
    - IdentifierName
    - Punctuator
    - NumericLiteral
    - StringLiteral
    - Template

### JS 词法、类型

### 预备知识：[unicode](https://www.fileformat.info/info/unicode/) 字符集

- [Blocks](https://www.fileformat.info/info/unicode/block/index.htm) 编码组

  - 0 ~ U+007F：常用拉丁字符
    - `String.fromCharCode(num)`
  - U+4E00 ~ U+9FFF：CJK ChineseJapaneseKorean三合一
    - 有一些增补区域（extension）
  -  U+0000 - U+FFFF：[BMP]([https://zh.wikipedia.org/wiki/Unicode%E5%AD%97%E7%AC%A6%E5%B9%B3%E9%9D%A2%E6%98%A0%E5%B0%84](https://zh.wikipedia.org/wiki/Unicode字符平面映射)) 基本平面

- [Categories](https://www.fileformat.info/info/unicode/category/index.htm)

  - [space空格系列](https://www.fileformat.info/info/unicode/category/Zs/list.htm)

- 实践
- 中文变量名

    因涉及到文件的编码保存方式，使用 `\u十六进制unicode`转译（`'中文'.codeCodeAt().toString(16)`）

### Atom 词

#### InputElement

- whiteSpace

  可查阅 unicode [space列表](https://www.fileformat.info/info/unicode/category/Zs/list.htm)

  - Tab：制表符（打字机时代：制表时隔开数字很方便）
  - VT：纵向制表符 `\v`
  - FF: FormFeed
  - SP: Space
  - NBSP: NO-BREAK SPACE（和 SP 的区别在于不会断开、不会合并）
  - ...

- LineTerminator 换行符

  - LF: Line Feed `\n`
  - CR: Carriage Return `\r`
  - LS: LINE SEPARATOR 分行
  - PS: PARAGRAPH SEPARATOR 分段

- Comment 注释

- Token 记号：一切有效的东西

  - Punctuator: 符号 比如 `> = < }`
  - Keywords：比如 `await`、`break`... 不能用作变量名，但像 getter 里的 `get`就是个例外
    - Future reserved Keywords: `eum`
  - IdentifierName：标识符，可以以字母、_ 或者 $ 开头，代码中用来标识**[变量](https://developer.mozilla.org/en-US/docs/Glossary/variable)、[函数](https://developer.mozilla.org/en-US/docs/Glossary/function)、或[属性](https://developer.mozilla.org/en-US/docs/Glossary/property)**的字符序列
    - 变量名：不能用 Keywords
    - 属性：可以用 Keywords
  - Literal: 直接量
    - Number
      - 存储 Uint8Array、Float64Array
      - 各种进制的写法
        - 二进制0b
        - 八进制0o
        - 十进制0x
      - 实践
        - 比较浮点是否相等：Math.abs(0.1 + 0.2 - 0.3) <= Number.EPSILON
        - 如何快捷查看一个数字的二进制：(97).toString(2)
    - String
      - Character
      - Code Point
      - Encoding
        - unicode编码 - utf
          - utf-8 可变长度 （控制位的用处）
      - Grammar
        - `''`、`""`、``` `
    - Boolean
    - Null
    - Undefind
