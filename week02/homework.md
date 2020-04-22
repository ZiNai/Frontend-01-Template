# 本周作业

## 写一个正则表达式 匹配所有 Number 直接量

````js
 /^-?\d+$|^(-?\d+)(\.\d+)?$|^0[bB][01]+$|^0[oO][0-7]+$|^0[xX][0-9a-fA-F]+$/g;
````

- 整数

```js
/^-?[0-9]+$/g
```

- 浮点数

```js
/^[-+]?[0-9]*\.?[0-9]+$/g
```

- 二进制数

```js
/^[01]+$/
```

- 八进制数

```js
/^[0-7]+\$/
```

- 十六进制数

```js
/(^0x[a-f0-9]{1,2}$)|(^0X[A-F0-9]{1,2}$)|(^[A-F0-9]{1,2}$)|(^[a-f0-9]{1,2}$)/g
```

## 写一个 UTF-8 Encoding 的函数

````js
function utf8Encode(unicodeString) {
    if (typeof unicodeString != 'string') throw new TypeError('parameter ‘unicodeString’ is not a string');
    const utf8String = unicodeString.replace(
        /[\u0080-\u07ff]/g,  // U+0080 - U+07FF => 2 bytes 110yyyyy, 10zzzzzz
        function(c) {
            var cc = c.charCodeAt(0);
            return String.fromCharCode(0xc0 | cc>>6, 0x80 | cc&0x3f); }
    ).replace(
        /[\u0800-\uffff]/g,  // U+0800 - U+FFFF => 3 bytes 1110xxxx, 10yyyyyy, 10zzzzzz
        function(c) {
            var cc = c.charCodeAt(0);
            return String.fromCharCode(0xe0 | cc>>12, 0x80 | cc>>6&0x3F, 0x80 | cc&0x3f); }
    );
    return utf8String;
}
````

## 写一个正则表达式，匹配所有的字符串直接量，单引号和双引号

````js
/[\u0021-\u007E]{6,16}|[\x21-\x7E]{6,16}|(['"])(?:(?!\1).)*?\1/g
````
