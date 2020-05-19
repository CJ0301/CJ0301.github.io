---
layout: 		post
title: 			"JavaScript基础"
subtitle: 		'正则表达式'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
tags:
  - JavaScript
---
## 创建
JS中的正则表达式都用RegExp对象表示，可以使用RegExp()构造函数来创建RegExp对象。不过通常RegExp对象都用直接量语法来创建，和字符串差不多，区别在于字符串用""包裹，而正则用//包裹，🌰：
```javascript
//匹配所有以s结尾的字符串。
//直接量创建
var pattern = /s$/;
//构造函数创建
var pattern = new RegExp("s$");
```
注意：ECMAScript5规范中正则表达式直接量运算都会新对象，与ECMAScript3规范不同。多数新浏览器已经使用ECMAScript5。🌰：
```javascript
function getRE(){
	var re = /[a-z]/;
	re.foo = "bar";
	return re;
}

var reg = getRE();
re2 = getRE();
console.log(reg === re2)//ECMAScript3返回true，ECMAScript5返回false
console.log(re2.foo)//ECMAScript3返回baz，ECMAScript5返回bar
```
## 正则规则
#### 字符类
<table>
	<tr>
		<td>字符</td>
		<td>匹配</td>
	</tr>
	<tr>
		<td>[...]</td>
		<td>方括号内的任意字符</td>
	</tr>
	<tr>
		<td>[^...]</td>
		<td>不在方括号内的任意字符</td>
	</tr>
	<tr>
		<td>.</td>
		<td>除换行符和其他Unicode行终止符以外的任意字符</td>
	</tr>
	<tr>
		<td>\w</td>
		<td>任何ASCII字符组成的单词，等价于[1-zA-Z0-9]</td>
	</tr>
	<tr>
		<td>\W</td>
		<td>任何不是ASCII字符组成的单词，等价于[^1-zA-Z0-9]</td>
	</tr>
	<tr>
		<td>\s</td>
		<td>任何Unicode空白符</td>
	</tr>
	<tr>
		<td>\S</td>
		<td>任何非Unicode空白符的字符</td>
	</tr>
	<tr>
		<td>\d</td>
		<td>任何ASCII数字，等价于[0-9]</td>
	</tr>
	<tr>
		<td>\D</td>
		<td>除了ASCII数字以外的任何字符，等价于[^0-9]</td>
	</tr>
	<tr>
		<td>[\b]</td>
		<td>退格直接量(特例)</td>
	</tr>
</table>

转义字符可组合使用,如/[\s\d]/可匹配任意空白符或数字。

#### 重复
<table>
	<tr>
		<td>字符</td>
		<td>含义</td>
	</tr>
	<tr>
		<td>{n,m}</td>
		<td>匹配前一项至少n次但不能超过m次</td>
	</tr>
	<tr>
		<td>{n,}</td>
		<td>匹配n次或更多次</td>
	</tr>
	<tr>
		<td>{n}</td>
		<td>匹配前一项n次</td>
	</tr>
	<tr>
		<td>?</td>
		<td>匹配前一项0次或1次，意思是这一项可存在可不存在，等价于{0,1}</td>
	</tr>
	<tr>
		<td>+</td>
		<td>匹配前一项1次或多次，等价于{1,}</td>
	</tr>
	<tr>
		<td>*</td>
		<td>匹配前一项0次或多次，等价于{0,}</td>
	</tr>
</table>

🌰:  
/\d{2,4}/  		//匹配2~4个数字
/\w{3}\d?/ 		//精确匹配三个单词和一个可选的数字
/\s+java\s+/ 	//匹配前后带有一个或多个空格的字符串"java"
/[^(]*/ 		//匹配一个或多个非左括号的字符

#### 选择、分组与引用
<table>
	<tr>
		<td>字符</td>
		<td>含义</td>
	</tr>
	<tr>
		<td>|</td>
		<td>表示选择</td>
	</tr>
	<tr>
		<td>(...)</td>
		<td>表示分组，将几个项合为一个单元，这个单元可通过*+?|等符号加以修饰，同时可以被\n引用。</td>
	</tr>
	<tr>
		<td>(?:...)</td>
		<td>只组合，把项组合到一个单元，但不记忆与该组相匹配的字符。</td>
	</tr>
	<tr>
		<td>?</td>
		<td>匹配前一项0次或1次，意思是这一项可存在可不存在，等价于{0,1}</td>
	</tr>
	<tr>
		<td>\n</td>
		<td>和第n个分组第一次匹配的字符相匹配，组是圆括号中的子表达式(也可能是嵌套的)，组索引是从左到右的左括号数量，(?:形式除外。</td>
	</tr>
</table>

🌰:  
/ab|cd|ef/ 		//匹配字符串"ab"，"cd"或者"ef"
/([a-z]+)(\d+)\1/   //匹配字符串前面是a-z中的字母，中间是数字，最后是a-z中的字母。

#### 指定匹配位置
<table>
	<tr>
		<td>字符</td>
		<td>含义</td>
	</tr>
	<tr>
		<td>^</td>
		<td>匹配字符串的开头，在多行检索中，匹配一行的开头</td>
	</tr>
	<tr>
		<td>$</td>
		<td>匹配字符串的结尾，在多行检索中，匹配一行的结尾</td>
	</tr>
	<tr>
		<td>\b</td>
		<td>匹配一个单词的边界，简言之就是单词与空格之间的位置</td>
	</tr>
	<tr>
		<td>\B</td>
		<td>匹配非单词边界</td>
	</tr>
	<tr>
		<td>(?=...)</td>
		<td>正向肯定断言，圆括号内必须正确匹配。</td>
	</tr>
	<tr>
		<td>(?!...)</td>
		<td>正向否定断言，圆括号内必须不匹配。</td>
	</tr>
	<tr>
		<td>(?<=...)</td>
		<td>反向肯定断言，就是和上面的正向方向不太一样，用起来一样</td>
	</tr>
	<tr>
		<td>(?<!...)</td>
		<td>反向否定断言，就是上面那个匹配变成不匹配</td>
	</tr>
</table>

🌰: 
/Java(?! Script)/

#### 修饰符
修饰符号是放在第二个/之外的
<table>
	<tr>
		<td>字符</td>
		<td>含义</td>
	</tr>
	<tr>
		<td>i</td>
		<td>执行不区分大小写的匹配。</td>
	</tr>
	<tr>
		<td>g</td>
		<td>执行一个全局匹配。</td>
	</tr>
	<tr>
		<td>m</td>
		<td>多行匹配，^匹配一行的开头和字符串的开头，$匹配行的结束和字符串的结束。</td>
	</tr>
</table>

#### 用于模式匹配的string方法
<table>
	<tr>
		<td>方法</td>
		<td>功能</td>
	</tr>
	<tr>
		<td>search()</td>
		<td>返回第一个与之匹配的子串的起始位置，找不到则返回-1，无法进行全局搜索</td>
	</tr>
	<tr>
		<td>replace()</td>
		<td>第一个参数为正则表达式，第二个参数是要进行替换的字符串</td>
	</tr>
	<tr>
		<td>match()</td>
		<td>最常用的正则表达式方法，返回一个由匹配结果组成的数组</td>
	</tr>
	<tr>
		<td>split()</td>
		<td>对指定规则进行分割</td>
	</tr>
</table>

## RegExp对象
RegExp()有两种创建形式，第二种的构造创建形式有两个参数，第二个参数是可选的。🌰：
```javascript
var pattern = new RegExp("\\d{5}","g");
```
需要注意的是，在构造里\必须都被替换成\\进行转义。

#### RegExp属性
每个RegExp对象都包含5个属性。
- source：一个只读的字符串，包含正则表达式的文本
- global：一个只读的布尔值，是否包含g
- ignoreCase：一个只读布尔值，是否包含i
- multiline：一个只读的布尔值，是否包含m
- lastIndex：可读写的整数，如果匹配模式带有g，这个属性存储整个字符串下一次检索的开始位置，属性会被exec()和test()方法用到。

#### RegExp方法
RegExp对象有两个执行用于执行模式匹配操作的方法。最主要的匹配方法是exec()

exec()的每一次调用都会记录一次下标，并在查找不到之后将该值赋值为0。
```
function getRE(string){
	re = /\d+/g;
	var s;
	while((s = re.exec(string))!=null)
		document.write(s+"  ");      
}
```

另外一种监测方法是test()，只返回匹配结果的布尔值。