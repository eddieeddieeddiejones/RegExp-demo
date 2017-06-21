
# 正则表达式学习技巧

## Demo01：03_replace_04_去掉.html

sublime编辑器中`ctrl + F`打开搜索功能，按照下图操作，能直观的看到正则表达式匹配到的内容

![如何用sublime匹配正则表达式](readme_img/03_replace_04_去掉符号.png "如何用sublime匹配正则表达式")

sublime编辑器中`ctrl + H`,打开查找替换功能

![查找替换](readme_img/09_书_正则表达式必知必会_07_查找替换回溯引用.png "查找替换")

## 一个网站直观看正则表达式是什么意思的网站[regexper](https://regexper.com/?#https%3F%3A%5C%2F%5C%2F%5B-%5Cw.%5D%2B(%3A%5Cd%2B)%3F(%5C%2F(%5B%5Cw%2F_.%5D*)%3F)%3F%0A)

# 代码摘抄

把demo中重要的代码片段摘抄出来，方便查阅(`ctrl + F`搜索这个页面)

## 03_replace_03.html

```javascript
// \w+ 匹配到一段字符串
// \s 空格
var re = /(\w+)\s(\w+)/;
var str = 'John Smith';
// $1表示正则表达式中第一个括号中的内容，依次类推
var newstr = str.replace(re, '$2 hahaha $1');
console.log(newstr);  // Smith hahaha John
```

## 03_replace_04_去掉符号.html

```javascript
var username = 'J;ohnSmith;@%';
username = username.replace(/[^A-Za-z\d_-]+/g, '');
alert(username); // JohnSmith
```

## 05_splitMyTry.html

```javascript
var names = 'aa ; sdf; sdf ; sdf ;sdf'
var re = /\s*;\s*/
var nameList = names.split(re)
console.log(nameList) // ["aa", "sdf", "sdf", "sdf", "sdf"]
```

## 06_test.html

```javascript
var username = 'johnsmith';
console.log(/[a-zA-Z_-]+/.test(username)); // true;
```

## 07_JS权威指南_01_基础知识.html

```javascript
# JS权威指南，10章 正则表达式部分
- 正则表达式中特殊含义的字符有：
  ^ $ . * + ? = ! : | \ / ( ) [ ] { }
  正则表达式中遇到这些字符，要用\转义

# 正则表达式的字符类
- [^...]： 不在方括号内任意字符
- . ：除换行之外的任意字符
- \w ： 等价于[a-zA-Z0-9]
- \W ：等价于[^a-zA-Z0-9]
- \s : 空白符
- \S : 任何非Unicode空白符的字符
- \d : 等价于 [0-9]
- \D : 等价于[^0-9]

# 正则表达式的重复字符语法
- {n, m} : 匹配至少n次，但是不能超过m次
- {n,} : n或者更多
- {n} : 匹配n次
- ? ：等价于{0，1}
- + ： 等价于 {1,}
- * :  等价于 {0,},0个或者多个

# 修饰符
- g： 全局
- m: 多行匹配
- i: 不区分大小写
```

## 07_JS权威指南_02_exec与match的区别.html

```javascript
// exec与match有什么不同
// match方法的参数是一个全局正则表达式（含有修饰符g）时，
// 会返回由所有匹配结果组成的一个数组，而exec无论有没有修饰符g，
// 都只是返回一个匹配结果
console.log(/\w{3}\d?/.test('aaa')) // true
console.log('aa java '.match(/\s+java\s+/)) // [" java ", index: 2, input: "aa java "]
console.log('aa java a java '.match(/\s+java\s+/g)) // [" java ", " java "]
console.log(/\s+java\s+/g.exec('aa java a java ')) // [" java ", index: 2, input: "aa java a java "]
console.log(/\s+java\s+/.exec('aa java a java ')) // [" java ", index: 2, input: "aa java a java "]
```

## 07_JS权威指南_03_零宽断言与负向先行断言.html

```javascript
// console.log(/[^(]*/.exec('asdf (sadfasd')) // ["asdf ", index: 0, input: "asdf (sadfasd"]
// console.log('abcdcd ef abcd'.match(/(ab|cd)+|ef/g)) // ["abcdcd", "ef", "abcd"]

// (?=),零宽断言，(?=xxx) 后面必须有xxx，\ 转义
console.log('abc:sdfabc'.match(/abc?(?=\:)/g)) // ["abc"]
// (?!),负向先行断言，(?!xxx)后面不能有xxx。可以使用sublime编辑器 ctrl + f测试
console.log('abcxxxdef'.match(/(abc|def)(?!xxx)/g))  // ["def"]
```

## 07_JS权威指南_04_单词边界.html

```javascript
// 匹配单词java。\b 单词边界 就是\w 和\W 之外
// 的东西。 /\sjava\s/ 有bug ,匹配不到一行开头的java,
// 而且匹配到的单词前后带有空格，这不是我们想要的
// \sjava\s sublime搜索
//java java
// console.log('javahaha:sadf java script'.match(/\bjava\b/ig)) // ["java"]
// console.log('java haha:sadf java script'.match(/\sjava\s/ig)) // [" java "]
```

## 07_JS权威指南_05_SearchandReplace.html

```javascript
// search方法，没找到的返回-1,不支持全局搜索，因为忽略了正则表达式中的g关键字
console.log('JavaScript'.search(/script/i)) // 4

const text = 'ac Ac aC'
const newText = text.replace(/ac/gi, 'AC')
console.log(newText) // AC AC AC
```

## 07_JS权威指南_06_将英文引号转为中文引号.html

```javascript
// 将英文 引号转化为中文引号
var quote = /"([^"]*)"/g
var str = '"sadf""sdfs"'
// $1 指的是括号中的内容
var newStr = str.replace(quote, "“$1”")
console.log(newStr) // “sadf”“sdfs”
```

## 07_JS权威指南_07_匹配url.html

```javascript
var text = 'visit my blog at http://www.a.com/b'
var url = /(\w+)\:\/\/([\w.]+)\/(\w+)/
var matches = text.match(url)
if(matches !== null) {
  var fullUrl = matches[0]
  var protocol = matches[1]
  var host = matches[2]
  var path = matches[3]
}
console.log(fullUrl) // http://www.a.com/b
console.log(protocol) // http
console.log(host) // www.a.com
console.log(path) // b
```

## 07_JS权威指南_07_匹配urlMyTry_02_全局匹配.html

```javascript
var text = 'visit my blog at http://www.a.com/b  http://www.ac.com/b'
var url = /(\w+)\:\/\/([\w.]+)\/(\w+)/g
var matches = text.match(url)
// ["http://www.a.com/b", "http://www.ac.com/b"]
console.log(matches)
```

## 07_JS权威指南_08_以逗号分割字符串.html

```javascript
// split
// 以逗号分割字符串
var returnStr = '1, 2, 3, 4, 5'.split(/\s*,\s*/)
console.log(returnStr) // ["1", "2", "3", "4", "5"]
```

## 07_JS权威指南_09_match方法.html

```javascript
// match方法
var matches = '1 plus 2 plus 3'.match(/\d+/g)
console.log(matches) // ["1", "2", "3"]
```

## 08_exec.html

```javascript
// var matches = /(hello \S+)/.exec('This is a hello world!');
// 没找到返回null，不管正则表达式有没有g修饰符，都会返回相同的一个数组
// console.log(matches)  //  ["hello world!", "hello world!", index: 10, input: "This is a hello world!"]
// console.log(matches.input) // This is a hello world!
// console.log(matches[1]); // hello world!

// 没找到返回null，不管正则表达式有没有g修饰符，都会返回相同的一个数组，不识别全局变量
// ["hello world!", "hello world!", index: 10, input: "This is a hello world! hello asdf"]
// console.log(/(hello \S+)/g.exec('This is a hello world! hello asdf'));
```

## 09_书_正则表达式必知必会_01_匹配IP.html

```javascript
// 匹配IP
256.212.1.1
12.234.234.23
\b((\d{1, 2}|1\d{2}|2[0-4]\d|25[0-5])\.){3}(\d{1, 2}|1\d{2}|2[0-4]\d|25[0-5]\.)\b
\d{1, 2} // 匹配0-9，或者0-99
1\d{2}  // 100 - 199  
2[0-4]\d // sublime搜索 201 244 249 2499
25[0-5]  // 250 -
 255
(1.){3} // 1.1.1.
// “\b”一般应用在需要匹配某一单词字符组成的子串，
// 但这一字符不能包含在同样由单词字符组成的更长的子串中。
// 比如要替换掉一段英文中的单词“to”，而“today”显然不在替换的范围内，
// 所以正则可以用“\bto\b”来限定。
\b2\b //sublime搜索 2 2 22 234 2//，\b单词边界

// 优化
// 这是IP 0.0.0.0  
// 这这不是 1.01.01.01，排除这种情况
// (((25[0-4]|2[0-4]\d|1\d{2})|([1-9]?\d))，三位数的情况
// ([1-9]?\d) 2位或者1位数字的情况
\b(((25[0-4]|2[0-4]\d|1\d{2})|([1-9]?\d))\.){3}((25[0-4]|2[0-4]\d|1\d{2})|([1-9]?\d))\b
```

## 09_书_正则表达式必知必会_03_回溯引用.html

```javascript
// 回溯引用
// of of asd and and and  and
// \1指的是(\w+)
\s+(\w+)\s+\1  // sublime 搜索这个这则表达式
```

## 09_书_正则表达式必知必会_04_匹配数字0-254.html

```javascript
// 1位或者2位数字
// 0 12 2 34
[1-9]?\d // 贪婪匹配

0-254
254 251
249 241
178
23
0 1
25[0-4]|24\d|1\d{2}|[1-9]?\d
```

## 09_书_正则表达式必知必会_04_匹配数字0-254.html

```javascript
// aaaaaaaa
// 在*+等后面加上?，表示非贪婪模式，就是尽可能少的去匹配
// aaa+?  // sublime搜索查看匹配结果
// *+等是贪婪模式，就是尽可能多的去匹配
// aaa+  // sublime搜索查看匹配结果

// 实际应用。
// sublime搜索查看匹配结果
// <\!-{2,}(.*?)-{2,}>
// <\!-{2,}(.*)-{2,}>
// var str = '<!-- sadf --><!-- sdfa -->'
// var newStr = str.replace(/<\!-{2,}(.*?)-{2,}>/g, '<!-- haha$1-->')
// console.log(newStr)  // <!-- haha sadf --><!-- haha sdfa -->

// var str1 = '<!-- sadf --><!-- sdfa -->'
// var newStr1 = str1.replace(/<\!-{2,}(.*)-{2,}>/g, '<!-- haha$1-->')
// console.log(newStr1) // <!-- haha sadf --><!-- sdfa -->
```

## 09_书_正则表达式必知必会_06_回溯引用.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
  </head>
  <body>
    <h1>sdf</h1><h3>dfg</h3>
    <h2>sdf</h2>
    <script>
    // 回溯索引，\1代表的就是正则表达式中第一个括号中的内容，就是([1-6])
    // <[Hh]([1-6])>.*?</[Hh]\1>  // sublime搜索查看匹配结果

    var str
     = '<h1>sdf</h1><h3>dfg</h3>'
    var re = /<[Hh]([1-6])>.*?<\/[Hh]\1>/g
    console.log(str.match(re)) // ["<h1>sdf</h1>", "<h3>dfg</h3>"]

    var str1 = 'aa'
    var re1 = /(a)\1/
    console.log(str1.match(re1))  // ["aa", "a", index: 0, input: "aa"]
    </script>
  </body>
</html>
```

## 09_书_正则表达式必知必会_07_查找替换回溯引用.html

```javascript
// sublime ctrl+h 查找替换
// 000-1111-2222
// (000)-1111-2222 // 结果
// (\d{3})-(\d{4})-(\d{4})
// ($1)-$2-$3

var str = '000-1111-2222'
var re = /(\d{3})-(\d{4})-(\d{4})/
var newStr = str.replace(re, '($1)-$2-$3')
// var newStr = str.replace(/re/, '(\1)-\2-\3')
console.log(newStr) // (000)-1111-2222
```

## 09_书_正则表达式必知必会_08_大小写转换元字符.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
  </head>
  <body>  
      <h1>WELCOME</h1><h1>hahaha</h1>
      <h1>welcome</h1><h1>hahaha</h1>
    <script>
      // 大小写转换元字符
      
      // \Uxxx\E,将xxx转换为大写的XXX
      // \LXXX\E,将XXX转换为小写的xxx
      
      // <h1>welcome</h1>
      // =>
      // <h1>WELCOME</h1>
      // ctrl+ h，查找替换
      // (<[Hh]1>)(.*?)(</[Hh]1>)
      // $1\U$2\E$3
      
      // <h1>WELCOME</h1>
      // =>
      // <h1>welcome</h1>
      // ctrl+ h，查找替换
      // (<[Hh]1>)(.*?)(</[Hh]1>)
      // $1\L$2\E$3

      var str = '<h1>welcome</h1>'
      var re = /(<[Hh]1>)(.*?)(<\/[Hh]1>)/
      var newStr = str.replace(re, '$1\U$2\E$3')
      // js好像是不支持
      console.log(newStr)  // <h1>UwelcomeE</h1>
    </script>
  </body>
</html>
```

## 09_书_正则表达式必知必会_09_向前匹配向后匹配.html

```javascript
// 向前查找
(?=xxx),匹配xxx之前内容
https://www.a.com
.+(?=:) // sublime 正则搜索
.+(=:) // sublime 搜索对比，看有什么不同

2yuan
3yuan
22
// 负向前查找
[0-9]+(?!(yuan))


$2.12
$1.12
213
// 向后查找
(?<=\$)[0-9.]+ // sublime 正则搜索
```
![向前匹配向后匹配](readme_img/09_书_正则表达式必知必会_09_向前匹配向后匹配.png "向前匹配向后匹配")

## 09_书_正则表达式必知必会_10_条件表达式.html

```javascript
// 匹配北美电话号码
(020)2222-1234  // 真的北美电话号码
003-2345-1243  // 真的北美电话号码

(020)-0203-2032 // 假的北美电话号码

// (\()? // 有一个或者没有(
// (?(1)\)|-) ,假如有(那么匹配),或者直接匹配-
(\()?\d{3}(?(1)\)|-)\d{4}-\d{4}

[a]sadf]sdf[sadf]]sadf[]sadf[
// ?(1) ，假如有那么匹配
// 假如有(\[)， 那么匹配\]
(\[)\w*(?(1)\]) // 
```

## 11_书正则表达式必知必会_常见问题_01_北美电话号码.html

```javascript
J. Doe: 248-555-1234
sdf: (313) 555-1234
sadf: (810)555-1234
sadf: (810555-1234

// 这两个不是北美电话号码
sadf: 810)555-1234
sadf: 734.555.9999
// 打开搜索，alt+r切换正则匹配，输入正则表达式可以搜索，比如`\d`搜索数字
var regExp1 = /\(?[2-9]\d\d\)?[ -]?[2-9]\d\d-\d{4}/
\(?[2-9]\d\d\)?[ -]?[2-9]\d\d-\d{4}
(\()?[2-9]\d\d(?(1)\))[ -]?[2-9]\d\d-\d{4}

// 这个正则表达式是最好的
// (?(1)\)) 意思是如果有(，那么匹配)。这里(1)指开头的(\()
(\()?[2-9]\d\d(?(1)\))[ -]?[2-9]\d\d-\d{4}
```

## 11_书正则表达式必知必会_常见问题_03_匹配网址.html

```javascript
http://wwww.sdf:80/blog
https://wwww.sdf:80/blog/index.cfm
http://wwww.sdf.com
http://ben:waerwa@www.forta.com/
http://localhost/index.php?ab=1&c=2
http://localhost:8500/

var regExp = /https?:\/\/[\w.-]+(:\d+)?(\/([\w.-]*))?/
```

# 其他

- 推荐pdf阅读软件，福昕阅读器，可以高亮、框选、文本标记

![福昕阅读器](readme_img/10_福昕阅读器.png "福昕阅读器")

- chrome浏览器， `ctrl + f` 可以将网页保存为pdf文件
- 推荐有道词典，可以划句子翻译、选中单词查看意思、设置快捷键快速呼出小窗口查看单词意思

![划词翻译](readme_img/11_有道词典_1_划词翻译.png "划词翻译")

![查看单词意思](readme_img/11_有道词典_2_查看单词意思.png "查看单词意思")

![快捷键呼出小窗口](readme_img/11_有道词典_3_快捷键呼出小窗口.png "快捷键呼出小窗口")

- API查询网站，[devdocs](http://devdocs.io/)。把各个框架库的文档集中到一个网站中，查询起来要方便些。

## License

MIT