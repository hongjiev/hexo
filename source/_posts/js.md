---
title: js
---
### 严格模式 ###
	function doSomething(){		"use strict";		//函数体 
	}
严格模式下,JavaScript 的执行结果会有很大不同。支持严格模式的浏览器包括 IE10+、Firefox 4+、Safari 5.1+、Opera 12+和 Chrome。

<!--more-->
##数据类型

ECMAScript 中有 5 种简单数据类型(也称为基本数据类型):`Undefined`、`Null`、`Boolean`、`Number` 和 `String`。还有 1 种复杂数据类型——`Object`，Object 本质上是由一组无序的名值对组成的。

鉴于 ECMAScript 是松散类型的,因此需要有一种手段来检测给定变量的数据类型——typeof 就 是负责提供这方面信息的操作符。对一个值使用 typeof 操作符可能返回下列某个字符串: 12

###typeof操作符
*  "undefined"——如果这个值未定义; 
*  "boolean"——如果这个值是布尔值; 
*  "string"——如果这个值是字符串;*  "number"——如果这个值是数值;*  "object"——如果这个值是对象或 null; 
*  "function"——如果这个值是函数。var message = "some string";
alert(typeof message);// "string"

alert(typeof(message));//"string"

这几个例子说明,typeof 操作符的操作数可以是变量(message),也可以是数值字面量。注意, typeof 是一个操作符而不是函数,因此例子中的圆括号尽管可以使用,但不是必需的。

有些时候,typeof 操作符会返回一些令人迷惑但技术上却正确的值。比如,调用 typeof null 会返回"object",因为特殊值 null 被认为是一个空的对象引用。Safari 5 及之前版本、Chrome 7 及之 前版本在对正则表达式调用 typeof 操作符时会返回"function",而其他浏览器在这种情况下会返回 "object"。

###Undefined类型

Undefined 类型只有一个值,即特殊的 undefined。在使用 var 声明变量但未对其加以初始化时,这个变量的值就是 undefined,例如:

var message;

alert(message == undefined); //true

// 下面这个变量并没有声明
// var age

alert(age); // 产生错误

对于尚未声明过的变量,只 4 能执行一项操作,即使用 typeof 操作符检测其数据类型(对未经声明的变量调用 delete 不会导致错 误,但这样做没什么实际意义,而且在严格模式下确实会导致错误)

###Null类型

Null 类型是第二个只有一个值的数据类型,这个特殊的值是 null。从逻辑角度来看,null 值表 示一个空对象指针,而这也正是使用 typeof 操作符检测 null 值时会返回"object"的原因,如下面 的例子所示:
var car = null;
alert(typeof car); // "object"

如果定义的变量准备在将来用于保存对象,那么最好将该变量初始化为 null 而不是其他值。这样 一来,只要直接检查 null 值就可以知道相应的变量是否已经保存了一个对象的引用,如下面的例子 所示:
	if (car != null){		// 对 car 对象执行某些操作	}实际上,undefined 值是派生自 null 值的,因此 ECMA-262 规定对它们的相等性测试要返回 true:     `alert(null == undefined);    //true`

尽管 null 和 undefined 有这样的关系,但它们的用途完全不同。如前所述,无论在什么情况下 都没有必要把一个变量的值显式地设置为 undefined,可是同样的规则对 null 却不适用。换句话说, 只要意在保存对象的变量还没有真正保存对象,就应该明确地让该变量保存 null 值。这样做不仅可以 体现 null 作为空对象指针的惯例,而且也有助于进一步区分 null 和 undefined。

###Boolean类型

要将一个值转换为其对应的 Boolean 值,可以调用转型函数 Boolean()

     var message = "Hello world!";     var messageAsBoolean = Boolean(message);

###Number类型
ECMAScript 能够表示的最小数值保 存在 `Number.MIN_VALUE` 中——在大多数浏览器中,这个值是 `5e-324`;能够表示的最大数值保存在 `Number.MAX_VALUE` 中——在大多数浏览器中,这个值是 `1.7976931348623157e+308`。如果某次计算的 结果得到了一个超出 JavaScript 数值范围的值,那么这个数值将被自动转换成特殊的 `Infinity` 值。具 体来说,如果这个数值是负数,则会被转换成`-Infinity`(负无穷),如果这个数值是正数,则会被转 换成 Infinity(正无穷)。

NaN,即非数值(Not a Number)是一个特殊的数值,这个数值用于表示一个本来要返回数值的操作数未返回数值的情况(这样就不会抛出错误了)。

NaN 本身有两个非同寻常的特点。首先,任何涉及 NaN 的操作(例如 NaN/10)都会返回 NaN,这 个特点在多步计算中有可能导致问题。其次,NaN 与任何值都不相等,包括 NaN 本身。例如,下面的代 码会返回 false:

	alert(NaN == NaN); //false
	
针对 NaN 的这两个特点,ECMAScript 定义了 isNaN()函数。这个函数接受一个参数,该参数可以 是任何类型,而函数会帮我们确定这个参数是否“不是数值”。

	alert(isNaN(NaN)); 	//true    alert(isNaN(10));	//false    alert(isNaN("10"));		//false    alert(isNaN("blue"));	//true    alert(isNaN(true));		//false(可以被转换成数值 1)尽管有点儿不可思议,但 isNaN()确实也适用于对象。在基于对象调用 isNaN() 函数时,会首先调用对象的 valueOf()方法,然后确定该方法返回的值是否可以转 换为数值。如果不能,则基于这个返回值再调用 toString()方法,再测试返回值。

Number()函数的转换规则如下：
		*  如果是 Boolean 值,true 和 false 将分别被转换为 1 和 0。
	*  如果是数字值,只是简单的传入和返回。	*  如果是 null 值,返回 0。	*  如果是 undefined,返回 NaN。	*  如果是字符串,遵循下列规则:	*  如果字符串中只包含数字(包括前面带正号或负号的情况),则将其转换为十进制数值,即"1" 会变成 1,"123"会变成 123,而"011"会变成 11(注意:前导的零被忽略了);	*  如果字符串中包含有效的浮点格式,如"1.1",则将其转换为对应的浮点数值(同样,也会忽 略前导零);	*  如果字符串中包含有效的十六进制格式,例如"0xf",则将其转换为相同大小的十进制整 数值;	*  如果字符串是空的(不包含任何字符),则将其转换为 0;	*  如果字符串中包含除上述格式之外的字符,则将其转换为 NaN。	*  如果是对象,则调用对象的 valueOf()方法,然后依照前面的规则转换返回的值。如果转换的结果是 NaN,则调用对象的 toString()方法,然后再次依照前面的规则转换返回的字符串值。
```
var num1 = Number("Hello world!"); //NaN var num2 = Number(""); //0var num3 = Number("000011"); //11var num4 = Number(true); //1
```
由于 Number()函数在转换字符串时比较复杂而且不够合理,因此在处理整数的时候更常用的是 parseInt()函数。parseInt()函数在转换字符串时,更多的是看其是否符合数值模式。它会忽略字 符串前面的空格,直至找到第一个非空格字符。如果第一个字符不是数字字符或者负号,parseInt() 就会返回 NaN;也就是说,用 parseInt()转换空字符串会返回 NaN(Number()对空字符返回 0)。如 果第一个字符是数字字符,parseInt()会继续解析第二个字符,直到解析完所有后续字符或者遇到了 一个非数字字符。例如,"1234blue"会被转换为 1234,因为"blue"会被完全忽略。类似地,"22.5" 4 会被转换为 22,因为小数点并不是有效的数字字符。

与 parseInt()函数类似,parseFloat()也是从第一个字符(位置 0)开始解析每个字符。而且 也是一直解析到字符串末尾,或者解析到遇见一个无效的浮点数字字符为止。也就是说,字符串中的第 一个小数点是有效的,而第二个小数点就是无效的了,因此它后面的字符串将被忽略。举例来说, "22.34.5"将会被转换为 22.34。

###String类型

###Object类型

var o = new Object();

Object 的每个实例都具有下列属性和方法。
* constructor:保存着用于创建当前对象的函数。对于前面的例子而言,构造函数(constructor) 8 就是 Object()。* hasOwnProperty(propertyName):用于检查给定的属性在当前对象实例中(而不是在实例 的原型中)是否存在。其中,作为参数的属性名(propertyName)必须以字符串形式指定(例 如:o.hasOwnProperty("name"))。* isPrototypeOf(object):用于检查传入的对象是否是传入对象的原型(第 5 章将讨论原 型)。* propertyIsEnumerable(propertyName):用于检查给定的属性是否能够使用 for-in 语句 (本章后面将会讨论)来枚举。与 hasOwnProperty()方法一样,作为参数的属性名必须以字符串形式指定。* toLocaleString():返回对象的字符串表示,该字符串与执行环境的地区对应。* toString():返回对象的字符串表示。 valueOf():返回对象的字符串、数值或布尔值表示。通常与 toString()方法的返回值相同。

##函数
	function functionName(arg0, arg1,...,argN) {    	statements	}以下是一个函数示例:
	function sayHi(name, message) {   		alert("Hello " + name + "," + message);	}
	
在函数体内可以通过 arguments 对象来 访问这个参数数组,从而获取传递给函数的每一个参数。

其实,arguments 对象只是与数组类似(它并不是 Array 的实例),因为可以使用方括号语法访 问它的每一个元素(即第一个元素是 arguments[0],第二个元素是 argumetns[1],以此类推),使 用 length 属性来确定传递进来多少个参数。在前面的例子中,sayHi()函数的第一个参数的名字叫 name,而该参数的值也可以通过访问 arguments[0]来获取。因此,那个函数也可以像下面这样重写, 即不显式地使用命名参数:

	function sayHi() {   		alert("Hello " + arguments[0] + "," + arguments[1]);	}
	
	function howManyArgs() {   		alert(arguments.length);	}	howManyArgs("string", 45);  //2	howManyArgs();              //0	howManyArgs(12);            //1

