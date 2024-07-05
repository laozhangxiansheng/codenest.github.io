---
title: JS中字符串的属性及方法
tags: JS
index_img: https://cdn.houdemingxin.com/image/default/CF4AFA8A497C42D382680A794A40BE26-6-2.png
banner_img: https://cdn.houdemingxin.com/image/default/CF4AFA8A497C42D382680A794A40BE26-6-2.png
date: 2024-07-05 15:53:39
---

# JS 中字符串的属性及方法

## 属性

### 1. length

字符串的长度，即字符串中字符的个数。

```javascript
let str = "hello world";
console.log(str.length); // 11
```

## 方法

### 2. charAt(index)

返回指定位置的字符，index 为字符串中的索引，从 0 开始。

```javascript
let str = "hello world";
console.log(str.charAt(0)); // h
console.log(str.charAt(1)); // e
```

### 3. charCodeAt(index)

返回指定位置的字符的 Unicode 编码，index 为字符串中的索引，从 0 开始。

```javascript
let str = "hello world";
console.log(str.charCodeAt(0)); // 104
console.log(str.charCodeAt(1)); // 101
```

### 4. indexOf(searchValue, fromIndex)

返回指定子字符串在原字符串中首次出现的位置，返回索引。未找到时返回 -1。可选参数 fromIndex 指定起始搜索位置。

```javascript
let str = "hello world";
console.log(str.indexOf("o")); // 4
console.log(str.indexOf("o", 5)); // 7
```

### 5. lastIndexOf(searchValue, fromIndex)

返回指定字符在字符串中最后一次出现的位置，fromIndex 为开始查找的位置，默认为字符串的长度。

```javascript
let str = "hello world";
console.log(str.lastIndexOf("o")); // 7
console.log(str.lastIndexOf("o", 5)); // 4
```

### 6. slice(start, end)

返回从 start 到 end（不包括 end）之间的字符串，start 和 end 为字符串中的索引，从 0 开始。

```javascript
let str = "hello world";
console.log(str.slice(0, 5)); // hello
console.log(str.slice(6, 11)); // world
```

### 7. substring(start, end)

返回从 start 到 end（不包括 end）之间的字符串，start 和 end 为字符串中的索引，从 0 开始。

```javascript
let str = "hello world";
console.log(str.substring(0, 5)); // hello
console.log(str.substring(6, 11)); // world
```

### 8. substr(start, length)

返回从 start 开始的 length 个字符，start 为字符串中的索引，从 0 开始。

```javascript
let str = "hello world";
console.log(str.substr(0, 5)); // hello
console.log(str.substr(6, 5)); // world
```

### 9. split(separator, limit)

将字符串分割成数组，separator 为分割符，limit 为返回数组的最大长度。

```javascript
let str = "hello world";
console.log(str.split(" ")); // ["hello", "world"]
console.log(str.split(" ", 1)); // ["hello"]
```

### 10. toLowerCase()

将字符串转换为小写。

```javascript
let str = "Hello World";
console.log(str.toLowerCase()); // hello world
```

### 11. toUpperCase()

将字符串转换为大写。

```javascript
let str = "Hello World";
console.log(str.toUpperCase()); // HELLO WORLD
```

### 12. trim()

去除字符串两端的空格。

```javascript
let str = "  hello world  ";
console.log(str.trim()); // hello world
```

### 13. replace(searchValue, replaceValue)

将字符串中的 searchValue 替换为 replaceValue。

```javascript
let str = "hello world";
console.log(str.replace("world", "JavaScript")); // hello JavaScript
console.log(str.replace(/o/g, "a")); // hella warld
```

### 14. match(regexp)

返回一个数组，包含字符串中与正则表达式匹配的子串。

```javascript
let str = "hello world";
console.log(str.match(/o/g)); // ["o", "o"]
```

### 15. search(regexp)

返回字符串中第一个与正则表达式匹配的子串的索引。

```javascript
let str = "hello world";
console.log(str.search(/o/)); // 4
```

### 16. trimLeft()

去除字符串左端的空白字符。

```javascript
let str = "  hello world  ";
console.log(str.trimLeft()); // hello world
```

### 17. trimRight()

去除字符串右端的空白字符。

```javascript
let str = "  hello world  ";
console.log(str.trimRight()); //   hello world
```

### 18. includes(searchValue, fromIndex)

判断字符串是否包含 searchValue，fromIndex 为开始搜索的位置。

```javascript
let str = "hello world";
console.log(str.includes("o")); // true
console.log(str.includes("o", 5)); // true
console.log(str.includes("o", 8)); // false
```

### 19. startsWith(searchValue, fromIndex)

判断字符串是否以 searchValue 开头，fromIndex 为开始搜索的位置。

```javascript
let str = "hello world";
console.log(str.startsWith("h")); // true
console.log(str.startsWith("h", 1)); // false
```

### 20. endsWith(searchValue, fromIndex)

判断字符串是否以 searchValue 结尾，fromIndex 为开始搜索的位置。

```javascript
let str = "hello world";
console.log(str.endsWith("d")); // true
console.log(str.endsWith("d", 5)); // false
```

### 21. repeat(count)

返回一个新字符串，该字符串包含 count 个 str 的副本。

```javascript
let str = "hello";
console.log(str.repeat(3)); // hellohellohello
```

### 22. concat('hole', 'world')

将一个或多个字符串与原字符串连接合并，形成一个新的字符串并返回。

```javascript
let str = "hello";
console.log(str.concat("world")); // helloworld
console.log(str.concat("world", "!", "!!!")); // helloworld!!!
```

### 23. at(index)

返回指定位置的字符，支持负索引。

```javascript
let str = "hello world";
console.log(str.at(0)); // h
console.log(str.at(-1)); // d
```

### 24. padStart(targetLength, padString)

用 padString 填充字符串，使字符串达到 targetLength 的长度，从字符串的头部开始填充。

```javascript
let str = "hello";
console.log(str.padStart(10, " ")); //     hello
console.log(str.padStart(10, "0")); // 00000hello
```

### 25. padEnd(targetLength, padString)

用 padString 填充字符串，使字符串达到 targetLength 的长度，从字符串的尾部开始填充。

```javascript
let str = "hello";
console.log(str.padEnd(10, " ")); // hello
console.log(str.padEnd(10, "0")); // hello00000
```
