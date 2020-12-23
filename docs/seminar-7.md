# 大前端内部技术交流会期数未定（时间未定）  
## 1、js 基础知识  
- ### 1.1、JavaScript 数据类型和数据结构  
  - JavaScript 是一种弱类型或者说动态语言。
  - 这意味着你不用提前声明变量的类型，在程序运行过程中，类型会被自动确定。
  - 这也意味着你可以使用同一个变量保存不同类型的数据：
  ```javascript
  var foo = 42; // foo is a Number now
  foo = "bar"; // foo is a String now
  foo = true; // foo is a Boolean now
  ```
  - 最新的 ECMAScript 标准定义了 8 种数据类型:
  - 原始类型：Boolean、Null、Undefined、Number、BigInt、String、Symbol
  - 引用类型：Object
  - 除 Object 以外的所有类型都是不可变的（值本身无法被改变）。
  ```javascript
  const foo = [1, 2];
  const bar = foo;
  bar[0] = 9;
  console.log(foo[0], bar[0]); // => 9, 9
  ```

- ### 1.2、Boolean
  #### 描述
  - Boolean 对象是一个布尔值的对象包装器。  

  - 如果需要，作为第一个参数传递的值将转换为布尔值。如果省略或值 0，-0，null，false，NaN，undefined，或空字符串（""），该对象具有的初始值 false。所有其他值，包括任何对象，空数组（[]）或字符串"false"，都会创建一个初始值为 true 的对象。  

  #### 语法
  ```javascript
  const isShow = true;
  console.log(isShow); //true
  const isDelete = false;
  console.log(isDelete); //false
  const isView = Boolean(true);
  console.log(isView); //true
  ```
  #### 实例方法
  - Boolean.prototype.toString()
  - 根据对象的值返回字符串"true"或"false"。  
    重写 Object.prototype.toString()方法。

  - Boolean.prototype.valueOf()  
    返回 Boolean 对象的原始值。  
    重写 Object.prototype.valueOf()方法。
  
  ```javascript
  console.log(isView.toString()); //'true'
  console.log(typeof isView.toString()); //String
  console.log(isView.toString()); //true
  console.log(isView.valueOf()); //true
  ```

- ### 1.3、Null
  #### 描述
  - 值 null 是一个字面量，不像 undefined，它不是全局对象的一个属性。null 是表示缺少的标识，指示变量未指向任何对象。把 null 作为尚未创建的对象，也许更好理解。在 API 中，null 常在返回类型应是一个对象，但没有关联的值的地方使用。

  #### null 与 undefined 的不同点：
  - 当检测 null 或 undefined 时，注意相等（==）与全等（===）两个操作符的区别 ，前者会执行类型转换：

  ```javascript
  typeof null // "object" (因为一些以前的原因而不是'null')
  typeof undefined // "undefined"
  null === undefined // false
  null == undefined // true
  null === null // true
  null == null // true
  !null //true
  isNaN(1 + null) // false
  isNaN(1 + undefined) // true
  ```

- ### 1.4、undefined
  #### 描述
  - 一个声明未定义的变量的初始值，或没有实际参数的形式参数。
  ```javascript
  var x; //创建一个变量，但并没有赋值
  console.log("X 的值是", x) //返回 X 的值是 undefined
  ```

- ### 1.5、Number
  #### 描述
  - JavaScript 的 Number 对象是经过封装的能让你处理数字值的对象。Number 对象由 Number() 构造器创建。
  - JavaScript 的 Number 类型为双精度 IEEE 754 64 位浮点类型。
  
  #### Number 对象主要用于：
  - 如果参数无法被转换为数字，则返回 NaN。
  - 在非构造器上下文中 (如：没有 new 操作符)，Number 能被用来执行类型转换。

  #### 语法
  ```javascript
    new Number(value);
    var a = new Number('123'); // a === 123 is false
    var b = Number('123'); // b === 123 is true
    a instanceof Number; // is true
    b instanceof Number; // is false
  ```
  #### 属性
  - Number.EPSILON  
    两个可表示(representable)数之间的最小间隔。  
    `console.log(Number.EPSILON); //2.220446049250313e-16`
  
  - Number.MAX_SAFE_INTEGER  
    JavaScript 中最大的安全整数 (253 - 1)。   
    `console.log(Number.MAX_SAFE_INTEGER); //9007199254740991`
  
  - Number.MAX_VALUE  
    能表示的最大正数。最小的负数是 -MAX_VALUE。  
    `console.log(Number.MAX_VALUE); //1.7976931348623157e+308`
  
  - Number.MIN_SAFE_INTEGER  
    JavaScript 中最小的安全整数 (-(253 - 1)).  
    `console.log(Number.MIN_SAFE_INTEGER); //-9007199254740991`
    
  - Number.MIN_VALUE  
    能表示的最小正数即最接近 0 的正数 (实际上不会变成 0)。  
    最大的负数是 -MIN_VALUE。  
    `console.log(Number.MIN_VALUE); //5e-324`

  - Number.NaN  
    特殊的“非数字”值。  
    `console.log(Number.NaN); //NaN`

  - Number.NEGATIVE_INFINITY  
    特殊的负无穷大值，在溢出时返回该值。  
    `console.log(Number.NEGATIVE_INFINITY); //-Infinity`

  - Number.POSITIVE_INFINITY  
    特殊的正无穷大值，在溢出时返回该值。  
    `console.log(Number.POSITIVE_INFINITY); //Infinity`
    
  - Number.prototype  
    Number 对象上允许的额外属性。 
    ```javascript
    const num1 = 2;
    console.log(num1.toExponential()); //2e+0
    console.log(num1.toFixed(2)); //2.00

    const num2 = 100.09;
    console.log(num2.toLocaleString("zh-Hans-CN", {style: "currency",currency:"CNY"})); //¥100.09
    console.log(num2.toLocaleString("en-Us", { style: "currency", currency: "USD" })); //$100.09
    console.log(num2.toLocaleString("de-DE", { style: "currency", currency:"EUR" })); //100,09 €
    console.log(num2.toLocaleString("ja-JP", { style: "currency", currency:"YEN" })); //YEN 100.09

    const num3 = 13.3714;
    console.log(num3.toPrecision(2)); //13
    console.log(num3.toString()); //"13.3714"
    console.log(typeof num3.toString()); //string
    console.log(num3.valueOf()); //13.3714

    ```
  #### 方法
  - Number.isNaN()  
    确定传递的值是否是 NaN。
    ```javascript
    const num4 = 0;
    const nan = NaN;
    console.log(Number.isNaN(num4)); //false
    console.log(Number.isNaN(nan)); //true
    ```

  - Number.isFinite()  
    确定传递的值类型及本身是否是有限数。
    ```javascript
    const num5 = 9007199254740991;
    console.log(Number.isFinite(num5)); //true
    console.log(Number.isFinite(Infinity)); //false
    console.log(Number.isFinite(NaN)); //false
    console.log(Number.isFinite(-Infinity)); //false
    console.log(Number.isFinite(2e100)); //true
    console.log(Number.isFinite("0")); //false
    ```

  - Number.isInteger()  
    确定传递的值类型是“number”，且是整数。
    ```javascript
    console.log(Number.isInteger(1)); // true
    console.log(Number.isInteger(0)); // true
    console.log(Number.isInteger("2")); // false
    console.log(Number.isInteger(NaN)); // false
    console.log(Number.isInteger([])); // false
    console.log(Number.isInteger([1])); // false
    console.log(Number.isInteger({})); // false
    console.log(Number.isInteger(Infinity)); // false
    ```
  
  - Number.isSafeInteger()  
    确定传递的值是否为安全整数 ( -(253 - 1) 至 253 - 1 之间)。
    ```javascript
    console.log(Number.isSafeInteger(3)); // true
    console.log(Number.isSafeInteger(Math.pow(2, 53))); // false
    console.log(Number.isSafeInteger(Math.pow(2, 53) - 1)); // true
    console.log(Number.isSafeInteger(NaN)); // false
    console.log(Number.isSafeInteger(Infinity)); // false
    console.log(Number.isSafeInteger("3")); // false
    console.log(Number.isSafeInteger(3.1)); // false
    console.log(Number.isSafeInteger(3.0)); // true
    ```

  - Number.toInteger()  
    计算传递的值并将其转换为整数 (或无穷大)。
    ```javascript
    Number.toInteger(0.1); // 0
    Number.toInteger(1); // 1
    Number.toInteger(Math.PI); // 3
    Number.toInteger(null); // 0
    ```
  
  - Number.parseFloat()  
    和全局对象 parseFloat() 一样。
    ```javascript
    //下面的例子都返回 3.14
    Number.parseFloat(3.14);
    Number.parseFloat('3.14');
    Number.parseFloat(' 3.14 ');
    Number.parseFloat('314e-2');
    Number.parseFloat('0.0314E+2');
    Number.parseFloat('3.14some non-digit characters');
    Number.parseFloat({ toString: function() { return "3.14" } });

    Number.parseFloat("FF2");//NaN
    Number.parseFloat(900719925474099267n);//900719925474099300
    Number.parseFloat('900719925474099267n');//900719925474099300
    ```

  - Number.parseInt()  
    和全局对象 parseInt() 一样。
    ```javascript
    //以下例子均返回 15:
    parseInt("0xF", 16);
    parseInt("F", 16);
    parseInt("17", 8);
    parseInt(021, 8);
    parseInt("015", 10); // parseInt(015, 8); 返回 13
    parseInt(15.99, 10);
    parseInt("15,123", 10);
    parseInt("FXX123", 16);
    parseInt("1111", 2);
    parseInt("15 \* 3", 10);
    parseInt("15e2", 10);
    parseInt("15px", 10);
    parseInt("12", 13);
    //以下例子均返回 NaN:
    parseInt("Hello", 8); // 根本就不是数值
    parseInt("546", 2); // 除了“0、1”外，其它数字都不是有效二进制数字
    //以下例子均返回 -15：
    parseInt("-F", 16);
    parseInt("-0F", 16);
    parseInt("-0XF", 16);
    parseInt(-15.1, 10);
    parseInt(" -17", 8);
    parseInt(" -15", 10);
    parseInt("-1111", 2);
    parseInt("-15e1", 10);
    parseInt("-12", 13);
    //下例中全部返回 4:
    parseInt(4.7, 10);
    parseInt(4.7 \* 1e22, 10); // 非常大的数值变成 4
    parseInt(0.00000000000434, 10); // 非常小的数值变成 4
    //下面的例子返回 224
    parseInt("0e0",16);
    ```

- ### 1.6、BigInt
  #### 描述
  - 可以用在一个整数字面量后面加 n 的方式定义一个 BigInt ，如：10n，或者调用函数 BigInt()。

  - BigInt 是一种内置对象，它提供了一种方法来表示大于 253 - 1 的整数。这原本是 Javascript 中可以用 Number 表示的最大数字。BigInt 可以表示任意大的整数。

  - 它在某些方面类似于 Number ，但是也有几个关键的不同点：不能用于 Math 对象中的方法；不能和任何 Number 实例混合运算，两者必须转换成同一种类型。在两种类型来回转换时要小心，因为 BigInt 变量在转换成 Number 变量时可能会丢失精度。

  #### 语法
  ```javascript
  const theBiggestInt = 9007199254740991n;
  const alsoHuge = BigInt(9007199254740991);// ↪ 9007199254740991n
  ```
  #### 类型信息
  - 使用 typeof 测试时， BigInt 对象返回 "bigint" ：
  ```javascript
  typeof 1n === 'bigint'; // true
  typeof BigInt('1') === 'bigint'; // true
  ```
  - 使用 Object 包装后， BigInt 被认为是一个普通 "object" ：
  ```javascript
  typeof Object(1n) === 'object'; // true
  ```

  #### 运算
  - 以下操作符可以和 BigInt 一起使用： +、`*`、`-`、`**`、`%` 。除 >>> （无符号右移）之外的 位操作 也可以支持。因为 BigInt 都是有符号的， >>> （无符号右移）不能用于 BigInt。为了兼容 asm.js ，BigInt 不支持单目 (+) 运算符。
  ```javascript
  const previousMaxSafe = BigInt(Number.MAX_SAFE_INTEGER);
  // ↪ 9007199254740991n
  
  const maxPlusOne = previousMaxSafe + 1n;
  // ↪ 9007199254740992n
  
  const theFuture = previousMaxSafe + 2n;
  // ↪ 9007199254740993n, this works now!
  
  const multi = previousMaxSafe \* 2n;
  // ↪ 18014398509481982n
  
  const subtr = multi – 10n;
  // ↪ 18014398509481972n
  
  const mod = multi % 10n;
  // ↪ 2n
  
  const bigN = 2n \*\* 54n;
  // ↪ 18014398509481984n
  
  bigN \* -1n
  // ↪ –18014398509481984n

  ```
  #### 静态方法
  - BigInt.asIntN()  
  将 BigInt 值转换为一个 -2width-1 与 2width-1-1 之间的有符号整数。
  
  - BigInt.asUintN()  
  将一个 BigInt 值转换为 0 与 2width-1 之间的无符号整数。

  #### 实例方法
  - BigInt.prototype.toLocaleString()  
  返回此数字的 language-sensitive 形式的字符串。覆盖 Object.prototype.
  
  - toLocaleString() 方法。  
  BigInt.prototype.toString()  
  返回以指定基数(base)表示指定数字的字符串。覆盖 Object.prototype.toString() 方法。
  
  - BigInt.prototype.valueOf()  
  返回指定对象的基元值。 覆盖 Object.prototype.valueOf() 方法。

- ### 1.7、String  
  #### 描述  
  - 字符串对于保存可以以文本形式表示的数据非常有用。 一些常用的字符串操作有：查询字符串长度，使用 + 和 += 运算符来构建和连接字符串，使用 indexOf 方法检查某一子字符串在父字符串中的位置，又或是使用 substring 方法提取从父字符串中提取子字符串。

  #### 语法
  - 字符串字面量采取以下形式：
  ```javascript
  'string text'
  "string text"
  "中文/汉语"
  "español"
  "English "
  ```
  - 你也能使用 String 函数将其他值生成或转换成字符串：
  ```javascript
  String(thing)
  new String(thing)
  ```
  #### 方法
  - String.fromCharCode()  
  通过一串 Unicode 创建字符串。
  ```javascript
  String.fromCharCode(65, 66, 67); // 返回 "ABC"
  String.fromCharCode(0x2014); // 返回 "—"
  String.fromCharCode(0x12014); // 也是返回 "—"; 数字 1 被剔除并忽略
  String.fromCharCode(8212); // 也是返回 "—"; 8212 是 0x2014 的十进制表示
  ```

  - String.fromCodePoint()  
    通过一串 码点 创建字符串。  
  ```javascript
  String.fromCodePoint(42); // "\*"
  String.fromCodePoint(65, 90); // "AZ"
  String.fromCodePoint(0x404); // "\u0404"
  String.fromCodePoint(0x2F804); // "\uD87E\uDC04"
  String.fromCodePoint(194564); // "\uD87E\uDC04"
  String.fromCodePoint(0x1D306, 0x61, 0x1D307) // "\uD834\uDF06a\uD834\uDF07"
  ```
  
  - String.raw()  
  通过模板字符串创建字符串。
  ```javascript
  String.raw`Hi\n${2+3}!`;
  // 'Hi\n5!'，Hi 后面的字符不是换行符，\ 和 n 是两个不同的字符\
  
  String.raw `Hi\u000A!`;
  // "Hi\u000A!"，同上，这里得到的会是 \、u、0、0、0、A 6 个字符，
  // 任何类型的转义形式都会失效，保留原样输出，不信你试试.length
  
  let name = "Bob";
  String.raw `Hi\n${name}!`;
  // "Hi\nBob!"，内插表达式还可以正常运行
  
  // 正常情况下，你也许不需要将 String.raw() 当作函数调用。
  // 但是为了模拟 `t${0}e${1}s${2}t` 你可以这样做:
  String.raw({ raw: 'test' }, 0, 1, 2); // 't0e1s2t'
  // 注意这个测试, 传入一个 string, 和一个类似数组的对象
  // 下面这个函数和 `foo${2 + 3}bar${'Java' + 'Script'}baz` 是相等的.
  String.raw({
      raw: ['foo', 'bar', 'baz']
      }, 2 + 3, 'Java' + 'Script'); // 'foo5barJavaScriptbaz'

  ```
  #### 字符串泛型方法 
  - String.prototype.constructor  
  用于创造对象的原型对象的特定的函数。

  - String.prototype.length  
  返回了字符串的长度。
  ```javascript
  const str1 = "我们都是中国人";
  console.log(str1.length); //7
  ```
  - String.prototype.charAt()  
  返回特定位置的字符。
  ```javascript
  console.log(str1.charAt(0)); //我
  console.log(str1.charAt(3)); //是
  console.log(str1.charAt(4)); //中
  console.log(str1.charAt(5)); //国
  console.log(str1.charAt(6)); //人
  ```
  - String.prototype.charCodeAt()  
  返回表示给定索引的字符的 Unicode 的值。
  ```javascript
  "ABC".charCodeAt(0) // returns 65:"A"
  "ABC".charCodeAt(1) // returns 66:"B"
  "ABC".charCodeAt(2) // returns 67:"C"
  "ABC".charCodeAt(3) // returns NaN
  ```
  - String.prototype.codePointAt()
  返回使用 UTF-16 编码的给定位置的值的非负整数。
  ```javascript
  'ABC'.codePointAt(1); // 66
  '\uD800\uDC00'.codePointAt(0); // 65536
  'XYZ'.codePointAt(42); // undefined
  ```

  - String.prototype.concat()  
  连接两个字符串文本，并返回一个新的字符串。
  ```javascript
  let hello = 'Hello, '
  console.log(hello.concat('Kevin', '. Have a nice day.'))// Hello, Kevin. Have a nice day.
  let greetList = ['Hello', ' ', 'Venkat', '!']
  "".concat(...greetList) // "Hello Venkat!"
  "".concat({}) // [object Object]
  "".concat([]) // ""
  "".concat(null) // "null"
  "".concat(true) // "true"
  "".concat(4, 5) // "45"
  ```

  - String.prototype.includes()  
  判断一个字符串里是否包含其他字符串。
  ```javascript
  var str = 'To be, or not to be, that is the question.';
  console.log(str.includes('To be')); // true
  console.log(str.includes('question')); // true
  console.log(str.includes('nonexistent')); // false
  console.log(str.includes('To be', 1)); // false
  console.log(str.includes('TO BE')); // false
  ```

  -String.prototype.endsWith()  
  判断一个字符串的是否以给定字符串结尾，结果返回布尔值。
  ```javascript
  var str = "To be, or not to be, that is the question.";
  console.log( str.endsWith("question.") ); // true
  console.log( str.endsWith("to be") ); // false
  console.log( str.endsWith("to be", 19) ); // true
  ```
  
  - String.prototype.indexOf()  
  从字符串对象中返回首个被发现的给定值的索引值，如果没有找到则返回-1。  
  字符串中的字符被从左向右索引。第一个字符的索引（index）是 0，变量名为 stringName 的字符串的最后一个字符的索引是 stringName.length - 1 。  
  indexOf 方法是区分大小写的。例如，下面的表达式将返回 -1：  
  `"Blue Whale".indexOf("blue") // 返回 -1`

  ```javascript
  var anyString = "Brave new world";
  
  console.log("The index of the first w from the beginning is " + anyString.indexOf("w"));// logs 8
  
  console.log("The index of the first w from the end is " + anyString.lastIndexOf("w"));// logs 10
  
  console.log("The index of 'new' from the beginning is " + anyString.indexOf("new"));// logs 6
  
  console.log("The index of 'new' from the end is " + anyString.lastIndexOf("new"));// logs 6

  ```
  - String.prototype.lastIndexOf()  
  1. 从字符串对象中返回最后一个被发现的给定值的索引值，如果没有找到则返回-1。 

  2. lastIndexOf() 方法返回调用 String 对象的指定值最后一次出现的索引，在一个字符串中的指定位置 fromIndex 处从后向前搜索。如果没找到这个特定值则返回-1 。  

  3. 该方法将从尾到头地检索字符串 str，看它是否含有子串 searchValue。开始检索的位置在字符串的 fromIndex 处或字符串的结尾（没有指定 fromIndex 时）。如果找到一个 searchValue，则返回 searchValue 的第一个字符在 str 中的位置。str 中的字符位置是从 0 开始的。

  ```javascript
  'canal'.lastIndexOf('a'); // returns 3 （没有指明 fromIndex 则从末尾 l 处开始反向检索到的第一个 a 出现在 l 的后面，即 index 为 3 的位置）
  'canal'.lastIndexOf('a', 2); // returns 1（指明 fromIndex 为 2 则从 n 处反向向回检索到其后面就是 a，即 index 为 1 的位置）
  'canal'.lastIndexOf('a', 0); // returns -1(指明 fromIndex 为 0 则从 c 处向左回向检索 a 发现没有，故返回-1)
  'canal'.lastIndexOf('x'); // returns -1
  'canal'.lastIndexOf('c', -5); // returns 0（指明 fromIndex 为-5 则视同 0，从 c 处向左回向查找发现自己就是，故返回 0）
  'canal'.lastIndexOf('c', 0); // returns 0（指明 fromIndex 为 0 则从 c 处向左回向查找 c 发现自己就是，故返回自己的索引 0）
  'canal'.lastIndexOf(''); // returns 5
  'canal'.lastIndexOf('', 2); // returns 2
  console.log("The index of the first w from the beginning is " + anyString.indexOf("w"));
  // Displays 8
  console.log("The index of the first w from the end is " + anyString.lastIndexOf("w"));
  // Displays 10
  console.log("The index of 'new' from the beginning is " + anyString.indexOf("new"));
  // Displays 6
  console.log("The index of 'new' from the end is " + anyString.lastIndexOf("new"));
  ```
  - String.prototype.localeCompare()  
  返回一个数字表示是否引用字符串在排序中位于比较字符串的前面，后面，或者二者相同。

  - String.prototype.match()  
  使用正则表达式与字符串相比较。
  ```javascript
  var str = 'For more information, see Chapter 3.4.5.1';
  var re = /see (chapter \d+(\.\d)\*)/i;
  var found = str.match(re);
  console.log(found);
  // logs [ 'see Chapter 3.4.5.1',
  // 'Chapter 3.4.5.1',
  // '.1',
  // index: 22,
  // input: 'For more information, see Chapter 3.4.5.1' ]
  
  // 'see Chapter 3.4.5.1' 是整个匹配。
  // 'Chapter 3.4.5.1' 被'(chapter \d+(\.\d)\*)'捕获。
  // '.1' 是被'(\.\d)'捕获的最后一个值。
  // 'index' 属性(22) 是整个匹配从零开始的索引。
  // 'input' 属性是被解析的原始字符串。

  var str = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
  var regexp = /[A-E]/gi;
  var matches_array = str.match(regexp);
  console.log(matches_array);
  // ['A', 'B', 'C', 'D', 'E', 'a', 'b', 'c', 'd', 'e']

  ```

  - String.prototype.replace()  
  被用来在正则表达式和字符串直接比较，然后用新的子串来替换被匹配的子串
  ```javascript
  var str = 'Twas the night before Xmas...';
  var newstr = str.replace(/xmas/i, 'Christmas');
  console.log(newstr); // Twas the night before Christmas...

  ```
  - String.prototype.search()  
    - 对正则表达式和指定字符串进行匹配搜索，返回第一个出现的匹配项的下标。  
    - 如果匹配成功，则 search() 返回正则表达式在字符串中首次匹配项的索引;否则，返回 -1。
    - 如果传入一个非正则表达式对象 regexp，则会使用 new RegExp(regexp) 隐式地将其转换为正则表达式对象。
  
  ```javascript
  var str = "hey JudE";
  var re = /[A-Z]/g;
  var re2 = /[.]/g;
  console.log(str.search(re)); // returns 4, which is the index of the first capital letter "J"
  console.log(str.search(re2)); // returns -1 cannot find '.' dot punctuation
  ```
  - String.prototype.slice()  
    - 摘取一个字符串区域，返回一个新的字符串。  
    - slice() 从一个字符串中提取字符串并返回新字符串。在一个字符串中的改变不会影响另一个字符串。也就是说，slice 不会修改原字符串（只会返回一个包含了原字符串中部分字符的新字符串）。
  ```javascript
  var str1 = 'The morning is upon us.', // str1 的长度 length 是 23。

  str2 = str1.slice(1, 8),
  str3 = str1.slice(4, -2),
  str4 = str1.slice(12),
  str5 = str1.slice(30);
  console.log(str2); // 输出：he morn
  console.log(str3); // 输出：morning is upon u
  console.log(str4); // 输出：is upon us.
  console.log(str5); // 输出：""
  ```
  - String.prototype.split()  
    - split() 方法使用指定的分隔符字符串将一个 String 对象分割成子字符串数组，以一个指定的分割字串来决定每个拆分的位置。
    - 找到分隔符后，将其从字符串中删除，并将子字符串的数组返回。如果没有找到或者省略了分隔符，则该数组包含一个由整个字符串组成的元素。如果分隔符为空字符串，则将 str 转换为字符数组。如果分隔符出现在字符串的开始或结尾，或两者都分开，分别以空字符串开头，结尾或两者开始和结束。因此，如果字符串仅由一个分隔符实例组成，则该数组由两个空字符串组成。
    - 如果分隔符是包含捕获括号的正则表达式，则每次分隔符匹配时，捕获括号的结果（包括任何未定义的结果）将被拼接到输出数组中。但是，并不是所有浏览器都支持此功能。
  ```javascript
  //用 split 取出一个字符串的：年月日 时分秒，当然也可以用 new Date()转换
  let splitStr = "2020-12-21 11:14:51";
  splitStr = splitStr.split(" ");
  console.log(splitStr); //["2020-12-21", "11:14:51"]
  const nyr = splitStr[0].split("-");
  console.log(nyr); //["2020", "12", "21"]
  const sfm = splitStr[1].split(":");
  console.log(sfm); //["11", "14", "51"]
  console.log("year:" + nyr[0] + " month:" + nyr[1] + " day:" + nyr[2] + " hour:" + sfm[0] + " minute:" + sfm[1] + " second:" + sfm[2] ); //year:2020 month:12 day:21 hour:11 minute:14 second:51
  ```

  - String.prototype.substr()  
    - substr() 方法返回一个字符串中从指定位置开始到指定字符数的字符。
    - start 是一个字符的索引。首字符的索引为 0，最后一个字符的索引为 字符串的长度减去 1。substr 从 start 位置开始提取字符，提取 length 个字符（或直到字符串的末尾）。
    - 如果 start 为正值，且大于或等于字符串的长度，则 substr 返回一个空字符串。
    - 如果 start 为负值，则 substr 把它作为从字符串末尾开始的一个字符索引。如果 start 为负值且 abs(start) 大于字符串的长度，则 substr 使用 0 作为开始提取的索引。注意负的 start 参数不被 Microsoft JScript 所支持。
    - 如果 length 为 0 或负值，则 substr 返回一个空字符串。如果忽略 length，则 substr 提取字符，直到字符串末尾。
  ```javascript
  //用 substr 取出歌词“天青色等烟雨，而我在等你！”两句。
  const substrStr = "天青色等烟雨，而我在等你！";
  console.log(substrStr.substr(0, 7)); //天青色等烟雨，
  console.log(substrStr.substr(7, 6)); //而我在等你！
  ```

  - String.prototype.substring()
    - substring() 方法返回一个字符串在开始索引到结束索引之间的一个子集, 或从开始索引直到字符串的末尾的一个子集。
    - substring 提取从 indexStart 到 indexEnd（不包括）之间的字符。特别地：
      + 如果 indexStart 等于 indexEnd，substring 返回一个空字符串。
      + 如果省略 indexEnd，substring 提取字符一直到字符串末尾。
      + 如果任一参数小于 0 或为 NaN，则被当作 0。
      + 如果任一参数大于 stringName.length，则被当作 stringName.length。
      + 如果 indexStart 大于 indexEnd，则 substring 的执行效果就像两个参数调换了一样。见下面的例子。
  ```javascript
  //substring 操作 where are you?
  const substringStr = "where are you?";
  console.log(substringStr.substring(0)); //where are you?
  console.log(substringStr.substring(0, 5)); //where
  console.log(substringStr.substring(6, 9)); //where
  console.log(substringStr.substring(100, 0)); //where are you?
  console.log(substringStr.substring(substringStr.length - 1, 3)); //re are you
  ```
  
  - String.prototype.toLocaleLowerCase()
    - toLocaleLowerCase()方法根据任何指定区域语言环境设置的大小写映射，返回调用字符串被转换为小写的格式。
    - toLocaleLowerCase() 方法返回根据任意区域语言大小写映射集而转换成小写格式的字符串。toLocaleLowerCase() 并不会影响字符串原本的值。在大多数情况下，该方法和调用 toLowerCase()的结果相同，但是在某些区域环境中，比如土耳其语，它的大小写映射并不遵循在 Unicode 中的默认的大小写映射，因此会有一个不同的结果。
  ```javascript
  'ALPHABET'.toLocaleLowerCase(); // 'alphabet'
  '\u0130'.toLocaleLowerCase('tr') === 'i'; // true
  '\u0130'.toLocaleLowerCase('en-US') === 'i'; // false
  let locales = ['tr', 'TR', 'tr-TR', 'tr-u-co-search', 'tr-x-turkish'];
  '\u0130'.toLocaleLowerCase(locales) === 'i'; // true
  ```

  - String.prototype.toLocaleUpperCase()  
    - toLocaleUpperCase() 方法根据本地主机语言环境把字符串转换为大写格式，并返回转换后的字符串。
  ```javascript
  'alphabet'.toLocaleUpperCase(); // 'ALPHABET'
  'Gesäß'.toLocaleUpperCase(); // 'GESÄSS'
  'i\u0307'.toLocaleUpperCase('lt-LT'); // 'I'
  let locales = ['lt', 'LT', 'lt-LT', 'lt-u-co-phonebk', 'lt-x-lietuva'];
  'i\u0307'.toLocaleUpperCase(locales); // 'I'
  ```

  - String.prototype.toString()  
    - toString() 方法返回指定对象的字符串形式。
    - String 对象覆盖了 Object 对象的 toString 方法；并没有继承 Object.toString()。对于 String 对象，toString 方法返回该对象的字符串形式，和 String.prototype.valueOf() 方法返回值一样。
  ```javascript
  var x = new String("Hello world");
  console.log(x.toString()) // 输出 "Hello world"
  ```

  - String.prototype.trim()  
    - trim() 方法会从一个字符串的两端删除空白字符。在这个上下文中的空白字符是所有的空白字符 (space, tab, no-break space 等) 以及所有行终止符字符（如 LF，CR 等）。
    - trim() 方法返回一个从两头去掉空白字符的字符串，并不影响原字符串本身。
  ```javascript
  //trim 处理前后空格
  let trimStr = "   Why are there spaces?    ";
  console.log(trimStr.trim()); //Why are there spaces?
  trimStr = "Why are there spaces?    ";
  console.log(trimStr.trim()); //Why are there spaces?
  ```
  - String.prototype.trimStart()
  - String.prototype.trimLeft()
    - trimStart() 方法从字符串的开头删除空格。trimLeft() 是此方法的别名。  

  - String.prototype.trimEnd()  
  - String.prototype.trimRight()
    - trimEnd() 方法从一个字符串的末端移除空白字符。trimRight() 是这个方法的别名。
  
  - String.prototype.valueOf()
    - valueOf() 方法返回 String 对象的原始值
  ```javascript
  const stringObj = new String('foo');
  console.log(stringObj);
  // expected output: String { "foo" }
  console.log(stringObj.valueOf());
  // expected output: "foo"
  ```

- ### 1.8、Symbol
  #### 概述
  - ES6 引入了一种新的原始数据类型 Symbol，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，前六种是：undefined、null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。
  - Symbol 值通过 Symbol 函数生成。这就是说，对象的属性名现在可以有两种类型，一种是原来就有的字符串，另一种就是新增的 Symbol 类型。凡是属性名属于 Symbol 类型，就都是独一无二的，可以保证不会与其他属性名产生冲突。
  ```javascript
  const pid = Symbol("pid");
  const cid = Symbol("cid");
  console.log(pid.toString()); //Symbol(pid)
  console.log(cid.toString()); //Symbol("cid")
  const obj = {
    [pid]: 20201125668899774465,
    [Symbol("cid")]: "2020336655889974"
  };
  console.log(obj);
  //'{Symbol(cid): "2020336655889974" Symbol(pid): 20201125668899774000}'
  console.log(obj[pid]); //20201125668899774000
  console.log(obj[Symbol("cid")]); //undefined
  ```

- ### 1.9、Object
  #### 描述
  在JavaScript中，几乎所有的对象都是Object类型的实例，它们都会从Object.prototype 继承属性和方法。Object构造函数为给定值创建一个对象包装器。Object构造函数，会根据给定的参数创建对象，具体有以下情况：
  - 如果给定值是 null 或 undefined，将会创建并返回一个空对象
  - 如果传进去的是一个基本类型的值，则会构造其包装类型的对象
  - 如果传进去的是引用类型的值，仍然会返回这个值，经他们复制的变量保有和源对象相同的引用地址  

  当以非构造函数形式被调用时，Object 的行为等同于 new Object()。

  #### 语法
  ``` javascript
  // 对象初始化器（Object initialiser）或对象字面量（literal）
  { [ nameValuePair1[, nameValuePair2[, ...nameValuePairN] ] ] }
  // 以构造函数形式来调用
  new Object([value])
  ```

  #### Object 构造函数的方法
  - Object.assign()  
      - Object.assign() 方法用于将所有可枚举属性的值从一个或多个源对象分配到目标对象。它将返回目标对象。  
      - 针对深拷贝，需要使用其他办法，因为 Object.assign()拷贝的是（可枚举）属性值。
  ```javascript
  const target = { a: 1, b: 2 };
  const source = { b: 4, c: 5 };
  console.log(Object.assign({}, target, source)); // "{a: 1, b: 4, c: 5}"
  console.log(Object.assign({}, source, target)); // "{b: 2, c: 5, a: 1}"
  ```

  - Object.create()  
  Object.create()方法创建一个新对象，使用现有的对象来提供新创建的对象__proto__。
  ```javascript
  const person = {
    isHuman: false,
    printIntroduction: function() {
      console.log(`My name is ${this.name}. Am I human? ${this.isHuman}`);
    }
  };
  const me = Object.create(person);
  me.name = 'Matthew'; // "name" is a property set on "me", but not on "person"
  me.isHuman = true; // inherited properties can be overwritten
  me.printIntroduction();
  // expected output: "My name is Matthew. Am I human? true"
  ```

  - Object.defineProperty()  
  Object.defineProperty() 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。
  ```javascript
  const object1 = {};
  Object.defineProperty(object1, 'property1', {
    value: 42,
    writable: false
  });
  object1.property1 = 77;// throws an error in strict mode
  console.log(object1.property1);// expected output: 42
  const obj1 = { _name: "" };
  Object.defineProperty(obj1, "name", {
    get: function() {
      return this._name;
    },
    set: function(val) {
      this._name = val + " & jolin Tasi";
    }
    });
    obj1.name = "jay chou";
    console.log(obj1.name); //jay chou & jolin Tasi
  ```

  - Object.defineProperties()  
    - Object.defineProperties() 方法直接在一个对象上定义新的属性或修改现有属性，并返回该对象。
    - Object.defineProperties 本质上定义了 obj 对象上 props 的可枚举属性相对应的所有属性。
  ```javascript
  var obj = {};
  Object.defineProperties(obj, {'property1': {
      value: true,
      writable: true
    },
    'property2': {
      value: 'Hello',
      writable: false
    }
    // etc. etc.
  });
  ```

  - Object.entries()  
  Object.entries()方法返回一个给定对象自身可枚举属性的键值对数组，其排列与使用 for...in 循环遍历该对象时返回的顺序一致（区别在于 for-in 循环还会枚举原型链中的属性）。
  ```javascript
  //Object.entries
  const obj2 = {
  1: "待审核",
  2: "待提交",
  3: "审核通过",
  4: "已公示"
  };
  console.log(Object.entries(obj2));
  //[
  // 0:["1", "待审核"]
  // 1:["2", "待提交"]
  // 2:["3", "审核通过"]
  // 3:["4", "已公示"]
  //]
  for (const [key, value] of Object.entries(obj2)) {
  console.log(`${key}:${value}`);
  }
  //1:待审核
  //2:待提交
  //3:审核通过
  //4:已公示
  ```

  - Object.getPrototypeOf()  
  Object.getPrototypeOf() 方法返回指定对象的原型（内部[[Prototype]]属性的值）。
  ```javascript
  var proto = {};
  var obj = Object.create(proto);
  Object.getPrototypeOf(obj) === proto; // true
  var reg = /a/;
  Object.getPrototypeOf(reg) === RegExp.prototype; // true
  ```  

  - Object.is()  
  Object.is()方法判断两个值是否为同一个值。
  ```javascript
  Object.is('foo', 'foo'); // true
  Object.is(window, window); // true

  Object.is('foo', 'bar'); // false
  Object.is([], []); // false

  var foo = { a: 1 };
  var bar = { a: 1 };
  Object.is(foo, foo); // true
  Object.is(foo, bar); // false

  Object.is(null, null); // true

  // 特例
  Object.is(0, -0); // false
  Object.is(0, +0); // true
  Object.is(-0, -0); // true
  Object.is(NaN, 0/0); // true
  ```
  - Object.keys()  
  Object.keys() 方法会返回一个由一个给定对象的自身可枚举属性组成的数组，数组中属性名的排列顺序和正常循环遍历该对象时返回的顺序一致 。
  ```javascript
  // simple array
  var arr = ['a', 'b', 'c'];
  console.log(Object.keys(arr)); // console: ['0', '1', '2']

  // array like object
  var obj = { 0: 'a', 1: 'b', 2: 'c' };
  console.log(Object.keys(obj)); // console: ['0', '1', '2']

  // array like object with random key ordering
  var anObj = { 100: 'a', 2: 'b', 7: 'c' };
  console.log(Object.keys(anObj)); // console: ['2', '7', '100']

  // getFoo is a property which isn't enumerable
  var myObj = Object.create({}, {
    getFoo: {
      value: function () { return this.foo; }
    }
  });
  myObj.foo = 1;
  console.log(Object.keys(myObj)); // console: ['foo']
  ```

  - Object.setPrototypeOf()  
  Object.setPrototypeOf() 方法设置一个指定的对象的原型 ( 即, 内部[[Prototype]]属性）到另一个对象或 null。
    - 如果对象的[[Prototype]]被修改成不可扩展(通过 Object.isExtensible()查看)，就会抛出 TypeError 异常。如果 prototype 参数不是一个对象或者 null(例如，数字，字符串，boolean，或者 undefined)，则什么都不做。否则，该方法将 obj 的[[Prototype]]修改为新的值。  
    - Object.setPrototypeOf()是 ECMAScript 6 最新草案中的方法，相对于 Object.prototype.__proto__ ，它被认为是修改对象原型更合适的方法
  ```javascript
  //Object.setPrototypeOf
  const obj3 = {
    name: "jay chou",
    getName: function() {
      return this.name + " 很好啊！";
    }
  };
  const obj4 = Object.setPrototypeOf({}, obj3);
  obj4.name = "Jolin Tasi";
  console.log(obj3.getName()); //jay chou 很好啊！
  console.log(obj4.getName()); //Jolin Tasi 很好啊！
  ```

  - Object.values()  
  Object.values()方法返回一个给定对象自身的所有可枚举属性值的数组，值的顺序与使用 for...in 循环的顺序相同 ( 区别在于 for-in 循环枚举原型链中的属性 )。
  ```javascript
  var obj = { foo: 'bar', baz: 42 };
  console.log(Object.values(obj)); // ['bar', 42]

  // array like object
  var obj = { 0: 'a', 1: 'b', 2: 'c' };
  console.log(Object.values(obj)); // ['a', 'b', 'c']

  // array like object with random key ordering
  // when we use numeric keys, the value returned in a numerical order according to the keys
  var an_obj = { 100: 'a', 2: 'b', 7: 'c' };
  console.log(Object.values(an_obj)); // ['b', 'c', 'a']

  // getFoo is property which isn't enumerable
  var my_obj = Object.create({}, { getFoo: { value: function() { return this.foo; } } });
  my_obj.foo = 'bar';
  console.log(Object.values(my_obj)); // ['bar']

  // non-object argument will be coerced to an object
  console.log(Object.values('foo')); // ['f', 'o', 'o']

  ```

- ### 1.10、Array
  #### 描述
  数组是一种类列表对象，它的原型中提供了遍历和修改元素的相关操作。JavaScript 数组的长度和元素类型都是非固定的。因为数组的长度可随时改变，并且其数据在内存中也可以不连续，所以 JavaScript 数组不一定是密集型的，这取决于它的使用方式。一般来说，数组的这些特性会给使用带来方便，但如果这些特性不适用于你的特定使用场景的话，可以考虑使用类型数组 TypedArray。  

  只能用整数作为数组元素的索引，而不能用字符串。后者称为关联数组。使用非整数并通过方括号或点号来访问或设置数组元素时，所操作的并不是数组列表中的元素，而是数组对象的属性集合上的变量。数组对象的属性和数组元素列表是分开存储的，并且数组的遍历和修改操作也不能作用于这些命名属性。

  #### 语法
  ```javascript
  [element0, element1, ..., elementN]
  new Array(element0, element1[, ...[, elementN]])
  new Array(arrayLength)
  
  //创建数组
  var fruits = ['Apple', 'Banana'];
  console.log(fruits.length);// 2

  //通过索引访问数组元素
  var first = fruits[0];// Apple
  var last = fruits[fruits.length - 1]; // Banana

  //遍历数组
  fruits.forEach(function (item, index, array) {
    console.log(item, index);
  });
  // Apple 0
  // Banana 1

  //添加元素到数组的末尾
  var newLength = fruits.push('Orange');
  //newLength:3; fruits: ["Apple", "Banana", "Orange"]

  //删除数组末尾的元素
  var last = fruits.pop(); // remove Orange (from the end)
  // last: "Orange"; fruits: ["Apple", "Banana"];

  //删除数组最前面（头部）的元素
  var first = fruits.shift(); // remove Apple from the front
  // first: "Apple"; fruits: ["Banana"];

  //添加元素到数组的头部
  var newLength = fruits.unshift('Strawberry') // add to the front
  // ["Strawberry", "Banana"];

  //找出某个元素在数组中的索引
  fruits.push('Mango');// ["Strawberry", "Banana", "Mango"]
  var pos = fruits.indexOf('Banana');// 1

  //通过索引删除某个元素
  var removedItem = fruits.splice(pos, 1); // this is how to remove an item
  // ["Strawberry", "Mango"]

  //从一个索引位置删除多个元素
  var vegetables = ['Cabbage', 'Turnip', 'Radish', 'Carrot'];
  console.log(vegetables);
  // ["Cabbage", "Turnip", "Radish", "Carrot"]

  var pos = 1, n = 2;

  var removedItems = vegetables.splice(pos, n);
  // this is how to remove items, n defines the number of items to be removed,
  // from that position(pos) onward to the end of array.

  console.log(vegetables);
  // ["Cabbage", "Carrot"] (the original array is changed)

  console.log(removedItems);
  // ["Turnip", "Radish"]

  //复制一个数组
  var shallowCopy = fruits.slice(); // this is how to make a copy
  // ["Strawberry", "Mango"]
  ```

  #### 方法
  - Array.from()  
  Array.from() 方法从一个类似数组或可迭代对象创建一个新的，浅拷贝的数组实例。
  ```javascript
  Array.from('foo');
  // [ "f", "o", "o" ]

  const set = new Set(['foo', 'bar', 'baz', 'foo']);
  Array.from(set);// [ "foo", "bar", "baz" ]

  const map = new Map([[1, 2], [2, 4], [4, 8]]);
  Array.from(map);// [[1, 2], [2, 4], [4, 8]]

  function f() {
    return Array.from(arguments);
  }
  f(1, 2, 3);// [ 1, 2, 3 ]
  
  Array.from([1, 2, 3], x => x + x);// [2, 4, 6]
  Array.from({length: 5}, (v, i) => i);// [0, 1, 2, 3, 4]

  //创建一个 100 个元素的数组并设定默认值为 1
  const arr1 = Array.from(new Array(100)).map(item => {
  return 1;
  });
  console.log(arr1); //[1,...98 个 1...,1]
  ```

  - Array.isArray()  
    - Array.isArray() 用于确定传递的值是否是一个 Array。
    - 当检测Array实例时, Array.isArray优于instanceof,因为 Array.isArray 能检测iframes.
    ```javascript
    // 下面的函数调用都返回 true
    Array.isArray([]);
    Array.isArray([1]);
    Array.isArray(new Array());
    Array.isArray(new Array('a', 'b', 'c', 'd'))
    // 鲜为人知的事实：其实 Array.prototype 也是一个数组。
    Array.isArray(Array.prototype);

    // 下面的函数调用都返回 false
    Array.isArray();
    Array.isArray({});
    Array.isArray(null);
    Array.isArray(undefined);
    Array.isArray(17);
    Array.isArray('Array');
    Array.isArray(true);
    Array.isArray(false);
    Array.isArray(new Uint8Array(32))
    Array.isArray({ __proto__: Array.prototype });
    ```

  - Array.of()   
    - Array.of() 方法创建一个具有可变数量参数的新数组实例，而不考虑参数的数量或类型。
    - Array.of() 和 Array 构造函数之间的区别在于处理整数参数：Array.of(7) 创建一个具有单个元素 7 的数组，而 Array(7) 创建一个长度为 7 的空数组（注意：这是指一个有 7 个空位(empty)的数组，而不是由 7 个 undefined 组成的数组）。
    ```javascript
    Array.of(1); // [1]
    Array.of(1, 2, 3); // [1, 2, 3]
    Array.of(undefined); // [undefined]
    ```

  - Array.prototype.copyWithin()  
  copyWithin() 方法浅复制数组的一部分到同一数组中的另一个位置，并返回它，不会改变原数组的长度。
  ```javascript
  [1, 2, 3, 4, 5].copyWithin(-2)
  // [1, 2, 3, 1, 2]

  [1, 2, 3, 4, 5].copyWithin(0, 3)
  // [4, 5, 3, 4, 5]

  [1, 2, 3, 4, 5].copyWithin(0, 3, 4)
  // [4, 2, 3, 4, 5]

  [1, 2, 3, 4, 5].copyWithin(-2, -3, -1)
  // [1, 2, 3, 3, 4]
  ```

  - Array.prototype.fill()
    - fill() 方法用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。不包括终止索引。
    - fill 方法接受三个参数 value, start 以及 end. start 和 end 参数是可选的, 其默认值分别为 0 和 this 对象的 length 属性值。
    ```javascript
    console.log(new Array(100).fill(1)); //[1,...98 个 1...,1]
    [1, 2, 3].fill(4);               // [4, 4, 4]
    [1, 2, 3].fill(4, 1);            // [1, 4, 4]
    [1, 2, 3].fill(4, 1, 2);         // [1, 4, 3]
    [1, 2, 3].fill(4, 1, 1);         // [1, 2, 3]
    [1, 2, 3].fill(4, 3, 3);         // [1, 2, 3]
    [1, 2, 3].fill(4, -3, -2);       // [4, 2, 3]
    [1, 2, 3].fill(4, NaN, NaN);     // [1, 2, 3]
    [1, 2, 3].fill(4, 3, 5);         // [1, 2, 3]
    Array(3).fill(4);                // [4, 4, 4]
    [].fill.call({ length: 3 }, 4);  // {0: 4, 1: 4, 2: 4, length: 3}
    ```

  - Array.prototype.pop()  
    - pop()方法从数组中删除最后一个元素，并返回该元素的值。此方法更改数组的长度。
    - pop 方法有意具有通用性。该方法和 call() 或 apply() 一起使用时，可应用在类似数组的对象上。pop 方法根据 length 属性来确定最后一个元素的位置。如果不包含 length 属性或 length 属性不能被转成一个数值，会将 length 置为 0，并返回 undefined。
    - 如果你在一个空数组上调用 pop()，它返回 undefined。
    ```javascript
    let myFish = ["angel", "clown", "mandarin", "surgeon"];

    let popped = myFish.pop();

    console.log(myFish);
    // ["angel", "clown", "mandarin"]

    console.log(popped);
    // surgeon
    ```
  
  - Array.prototype.push()  
    - push() 方法将一个或多个元素添加到数组的末尾，并返回该数组的新长度。
    - push 方法具有通用性。该方法和 call() 或 apply() 一起使用时，可应用在类似数组的对象上。push 方法根据 length 属性来决定从哪里开始插入给定的值。如果 length 不能被转成一个数值，则插入的元素索引为 0，包括 length 不存在时。当 length 不存在时，将会创建它。
    ```javascript
    var sports = ["soccer", "baseball"];
    var total = sports.push("football", "swimming");
    console.log(sports);
    // ["soccer", "baseball", "football", "swimming"]
    console.log(total);// 4
    ```
  
  - Array.prototype.reverse()  
  reverse() 方法将数组中元素的位置颠倒，并返回该数组。数组的第一个元素会变成最后一个，数组的最后一个元素变成第一个。该方法会改变原数组。
  ```javascript
  const a = [1, 2, 3];
  console.log(a); // [1, 2, 3]
  a.reverse();
  console.log(a); // [3, 2, 1]
  ```

  - Array.prototype.shift()  
    - shift() 方法从数组中删除第一个元素，并返回该元素的值。此方法更改数组的长度。
    - shift 方法并不局限于数组：这个方法能够通过 call 或 apply 方法作用于类似数组的对象上。但是对于没有 length 属性（从 0 开始的一系列连续的数字属性的最后一个）的对象，调用该方法可能没有任何意义。
    ```javascript
    let myFish = ['angel', 'clown', 'mandarin', 'surgeon'];

    console.log('调用 shift 之前: ' + myFish);
    // "调用 shift 之前: angel,clown,mandarin,surgeon"

    var shifted = myFish.shift();

    console.log('调用 shift 之后: ' + myFish);
    // "调用 shift 之后: clown,mandarin,surgeon"

    console.log('被删除的元素: ' + shifted);
    // "被删除的元素: angel"
    ```
  
  - Array.prototype.sort()  
  sort() 方法用原地算法对数组的元素进行排序，并返回数组。默认排序顺序是在将元素转换为字符串，然后比较它们的 UTF-16 代码单元值序列时构建的
  ```javascript
  const arr2 = ["Blue", "Humpback", "Beluga"];
  console.log(arr2.sort()); //["Beluga", "Blue", "Humpback"]
  const arr3 = ["A", "D", "O", "P", "Y", "T"];
  console.log(arr3.sort()); //["A", "D", "O", "P", "T", "Y"]
  const arr4 = [
  { name: "jay chou", age: 40 },
  { name: "Patty Hou", age: 41 },
  { name: "tom", age: 56 },
  { name: "green", age: 21 },
  { name: "aobama", age: 65 }
  ];
  console.log(
    arr4.sort((a, b) => {
      return a.age - b.age;
    })
  );
  //0: {name: "green", age: 21}
  //1: {name: "jay chou", age: 40}
  //2: {name: "Patty Hou", age: 41}
  //3: {name: "tom", age: 56}
  //4: {name: "aobama", age: 65}
  ```

  - Array.prototype.splice()  
  splice() 方法通过删除或替换现有元素或者原地添加新的元素来修改数组,并以数组形式返回被修改的内容。此方法会改变原数组。
  ```javascript
  var myFish = ["angel", "clown", "mandarin", "sturgeon"];
  var removed = myFish.splice(2, 0, "drum");
  // 运算后的 myFish: ["angel", "clown", "drum", "mandarin", "sturgeon"]
  // 被删除的元素: [], 没有元素被删除

  var myFish = ['angel', 'clown', 'drum', 'mandarin', 'sturgeon'];
  var removed = myFish.splice(3, 1);
  // 运算后的 myFish: ["angel", "clown", "drum", "sturgeon"]
  // 被删除的元素: ["mandarin"]
  ```

  - Array.prototype.unshift()  
  unshift() 方法将一个或多个元素添加到数组的开头，并返回该数组的新长度(该方法修改原有数组)。
  ```javascript
  let arr = [1, 2];

  arr.unshift(0); // result of the call is 3, which is the new array length
  // arr is [0, 1, 2]

  arr.unshift(-2, -1); // the new array length is 5
  // arr is [-2, -1, 0, 1, 2]

  arr.unshift([-4, -3]); // the new array length is 6
  // arr is [[-4, -3], -2, -1, 0, 1, 2]

  arr.unshift([-7, -6], [-5]); // the new array length is 8
  // arr is [ [-7, -6], [-5], [-4, -3], -2, -1, 0, 1, 2 ]
  ```

  - Array.prototype.concat()  
    - concat() 方法用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组。
    - concat 方法创建一个新的数组，它由被调用的对象中的元素组成，每个参数的顺序依次是该参数的元素（如果参数是数组）或参数本身（如果参数不是数组）。它不会递归到嵌套数组参数中。
    ```javascript
    var alpha = ['a', 'b', 'c'];
    var numeric = [1, 2, 3];
    alpha.concat(numeric);
    // result in ['a', 'b', 'c', 1, 2, 3]
    ```
  
  - Array.prototype.includes()  
  includes() 方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回 false。
  ```javascript
  [1, 2, 3].includes(2); // true
  [1, 2, 3].includes(4); // false
  [1, 2, 3].includes(3, 3); // false
  [1, 2, 3].includes(3, -1); // true
  [1, 2, NaN].includes(NaN); // true
  ```

  - Array.prototype.join()   
  join() 方法将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串。如果数组只有一个项目，那么将返回该项目而不使用分隔符。
  ```javascript
  var a = ['Wind', 'Rain', 'Fire'];
  var myVar1 = a.join(); // myVar1 的值变为"Wind,Rain,Fire"
  var myVar2 = a.join(', '); // myVar2 的值变为"Wind, Rain, Fire"
  var myVar3 = a.join(' + '); // myVar3 的值变为"Wind + Rain + Fire"
  var myVar4 = a.join(''); // myVar4 的值变为"WindRainFire"
  ```

  - Array.prototype.slice()  
  slice() 方法返回一个新的数组对象，这一对象是一个由 begin 和 end 决定的原数组的浅拷贝（包括 begin，不包括 end）。原始数组不会被改变。
  ```javascript
  var fruits = ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango'];
  var citrus = fruits.slice(1, 3);

  // fruits contains ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango']
  // citrus contains ['Orange','Lemon']
  ```

  - Array.prototype.toString()  
  Array 对象覆盖了 Object 的 toString 方法。对于数组对象，toString 方法连接数组并返回一个字符串，其中包含用逗号分隔的每个数组元素。
  ```javascript
  const array1 = [1, 2, 'a', '1a'];
  console.log(array1.toString());
  // expected output: "1,2,a,1a"
  ```

  - Array.prototype.indexOf()  
  indexOf()方法返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。
  ```javascript
  var array = [2, 5, 9];
  array.indexOf(2); // 0
  array.indexOf(7); // -1
  array.indexOf(9, 2); // 2
  array.indexOf(2, -1); // -1
  array.indexOf(2, -3); // 0
  ```

  - Array.prototype.lastIndexOf()  
  lastIndexOf() 方法返回指定元素（也即有效的 JavaScript 值或变量）在数组中的最后一个的索引，如果不存在则返回 -1。从数组的后面向前查找，从 fromIndex 处开始。
  ```javascript
  var array = [2, 5, 9, 2];
  var index = array.lastIndexOf(2);
  // index is 3
  index = array.lastIndexOf(7);
  // index is -1
  index = array.lastIndexOf(2, 3);
  // index is 3
  index = array.lastIndexOf(2, 2);
  // index is 0
  index = array.lastIndexOf(2, -2);
  // index is 0
  index = array.lastIndexOf(2, -1);
  // index is 3
  ```

  - Array.prototype.forEach()  
  forEach() 方法按升序为数组中含有效值的每一项执行一次 callback 函数，那些已删除或者未初始化的项将被跳过（例如在稀疏数组上）。
  ```javascript
  const array1 = ['a', 'b', 'c'];
  array1.forEach(element => console.log(element));
  // expected output: "a"
  // expected output: "b"
  // expected output: "c"
  ```

  - Array.prototype.entries()  
  entries() 方法返回一个新的 Array Iterator 对象，该对象包含数组中每个索引的键/值对。
  ```javascript
  const array1 = ['a', 'b', 'c'];

  const iterator1 = array1.entries();

  console.log(iterator1.next().value);
  // expected output: Array [0, "a"]

  console.log(iterator1.next().value);
  // expected output: Array [1, "b"]
  ```

  - Array.prototype.every()  
  every() 方法测试一个数组内的所有元素是否都能通过某个指定函数的测试。它返回一个布尔值。
  ```javascript
  function isBigEnough(element, index, array) {
    return element >= 10;
    }
    [12, 5, 8, 130, 44].every(isBigEnough); // false
    [12, 54, 18, 130, 44].every(isBigEnough); // true
  ```

  - Array.prototype.some()  
  some() 方法测试数组中是不是至少有 1 个元素通过了被提供的函数测试。它返回的是一个 Boolean 类型的值。
  ```javascript
  function isBiggerThan10(element, index, array) {
    return element > 10;
  }
  [2, 5, 8, 1, 4].some(isBiggerThan10); // false
  [12, 5, 8, 1, 4].some(isBiggerThan10); // true
  ```

  - Array.prototype.filter()  
  filter() 方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。
  ```javascript
  function isBigEnough(element) {
    return element >= 10;
  }
  var filtered = [12, 5, 8, 130, 44].filter(isBigEnough);
  // filtered is [12, 130, 44]
  ```

  - Array.prototype.find()  
  find() 方法返回数组中满足提供的测试函数的第一个元素的值。否则返回 undefined。
  ```javascript
  var inventory = [
    {name: 'apples', quantity: 2},
    {name: 'bananas', quantity: 0},
    {name: 'cherries', quantity: 5}
    ];
  function findCherries(fruit) {
    return fruit.name === 'cherries';
  }
  console.log(inventory.find(findCherries)); 
  // { name: 'cherries', quantity: 5 }
  ```

  - Array.prototype.findIndex()  
  findIndex()方法返回数组中满足提供的测试函数的第一个元素的索引。若没有找到对应元素则返回-1。
  ```javascript
  function isPrime(element, index, array) {
  var start = 2;
  while (start <= Math.sqrt(element)) {
    if (element % start++ < 1) {
      return false;
      }
    }
    return element > 1;
  }
  console.log([4, 6, 8, 12].findIndex(isPrime)); // -1, not found
  console.log([4, 6, 7, 12].findIndex(isPrime)); // 2
  ```

  - Array.prototype.keys()  
  keys() 方法返回一个包含数组中每个索引键的 Array Iterator 对象。
  ```javascript
  const array1 = ['a', 'b', 'c'];
  const iterator = array1.keys();
  for (const key of iterator) {
  console.log(key);
  }
  // expected output: 0
  // expected output: 1
  // expected output: 2
  ```

  - Array.prototype.map()  
  map() 方法创建一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值。
  ```javascript
  let arr5 = [
  { name: "jay chou", age: 40 },
  { name: "Patty Hou", age: 41 },
  { name: "tom", age: 56 },
  { name: "green", age: 21 },
  { name: "aobama", age: 65 }
  ];
  arr5 = arr5.map((item, index) => {
    return { ...item, id: index };
  });
  console.log(arr5);
  //0: {name: "jay chou", age: 40, id: 0}
  //1: {name: "Patty Hou", age: 41, id: 1}
  //2: {name: "tom", age: 56, id: 2}
  //3: {name: "green", age: 21, id: 3}
  //4: {name: "aobama", age: 65, id: 4}
  ```
  
  - Array.prototype.reduce()  
  reduce() 方法对数组中的每个元素执行一个由您提供的 reducer 函数(升序执行)，将其结果汇总为单个返回值。
  ```javascript
  var sum = [0, 1, 2, 3].reduce(function (accumulator, currentValue) {
    return accumulator + currentValue;
  }, 0);// 和为 6

  var initialValue = 0;
  var sum = [{x: 1}, {x:2}, {x:3}].reduce(function (accumulator, currentValue) {
    return accumulator + currentValue.x;
  },initialValue)
  console.log(sum) // logs 6
  ```
  - Array.prototype.reduceRight()  
  reduceRight() 方法接受一个函数作为累加器（accumulator）和数组的每个值（从右到左）将其减少为单个值。
  ```javascript
  //求一个数组中所有值的和
  var sum = [0, 1, 2, 3].reduceRight(function(a, b) {
    return a + b;
    });// sum is 6
  
  //扁平化（flatten）一个二维数组
  var flattened = [[0, 1], [2, 3], [4, 5]].reduceRight(function(a, b) {
    return a.concat(b);
  }, []);// flattened is [4, 5, 2, 3, 0, 1]
  ```

  - Array.prototype.values()  
  values() 方法返回一个新的 Array Iterator 对象，该对象包含数组每个索引的值
  ```javascript
  let arr = ['w', 'y', 'k', 'o', 'p'];
  let eArr = arr.values();
  for (let letter of eArr) {
    console.log(letter);
  } //"w" "y "k" "o" "p"
  ```

## 2、css 基础知识
- ### 2.1、什么是 CSS？  
CSS（层叠样式表）是一种样式语言，对于 HTML 元素来说足够简单。 它在网页设计中非常流行，其应用在 XHTML 中也很常见。

- ### 2.2、CSS 样式的组成部分是什么？  
   一个样式规则由三部分组成：
   - 选择器–选择器是 HTML 标记，用于选择要设置样式的内容。 它根据其 ID，类和名称选择 HTML 元素。
   - 属性–属性是 HTML 标签的一种属性。 简而言之，所有 HTML 属性都转换为 CSS 属性。
   - 值– CSS 中的值定义 CSS 属性的一组有效值。

- ### 2.3、CSS3 有哪些新特性？
   - 选择器;
   - 圆角（border-raduis）;
   - 多列布局（multi-column layout）;
   - 阴影（shadow）和反射（reflect）;
   - 文字特效（text-shadow）;
   - 文字渲染（text-decoration）;
   - 线性渐变（gradient）;
   - 旋转（rotate）/缩放（scale）/倾斜（skew）/移动（translate）;
   - 媒体查询（@media）;
   - RGBA 和透明度 ;
   - @font-face 属性;
   - 多背景图 ;
   - 盒子大小;
   - 语音;

- ### 2.4、什么是BFC  
  1. BFC的概念：块级格式化上下文
  2. BFC的原理：属于同一个BFC区域的相邻元素垂直方向边距重叠；BFC区域不会跟浮动元素重叠；BFC是一个独立的容器；不影响外面也不被外面影响；BFC容器计算高度时会计算子元素浮动元素的高度。
  3. 如何创建BFC：html根元素就是一个BFC；float不为none的元素；position为abslote、fixed的元素；display为inline-block、table-cell、table-caption；overflow不为visible。
  4. BFC的使用场景：两栏布局，左边固定，右边自适应；清楚浮动；上下边距重叠的时候

- ### 2.5、移动端1px解决方案
  - 移动端 web 项目越来越多，设计师对于 UI 的要求也越来越高，比如 1px 的边框。在高清屏下，移动端的 1px 会很粗。 比如，这个是假的 1 像素 

  1. 产生原因  
  那么为什么会产生这个问题呢？主要是跟一个东西有关，DPR(devicePixelRatio) 设备像素比，它是默认缩放为 100%的情况下，设备像素和 CSS 像素的比值。  
  `
  window.devicePixelRatio=物理像素 /CSS 像素
  `   
  目前主流的屏幕 DPR=2 （iPhone 8）,或者 3 （iPhone 8 Plus）。拿 2 倍屏来说，设备的物理像素要实现 1 像素，而 DPR=2，所以 css 像素只能是 0.5。一般设计稿是按照 750 来设计的，它上面的 1px 是以 750 来参照的，而我们写 css 样式是以设备 375 为参照的，所以我们应该写的 0.5px 就好了啊！ 试过了就知道，iOS 8+系统支持，安卓系统不支持。

  2. 推荐解决方案
      - 使用伪元素
      这个方法是我使用最多的，做出来的效果也是非常棒的，直接上代码。
      ```css
      .setOnePx{
        position: relative;
        &::after{
        position: absolute;
        content: '';
        background-color: #e5e5e5;
        display: block;
        width: 100%;
        height: 1px; /_no_/
        transform: scale(1, 0.5);
        top: 0;
        left: 0;
        }
      }
      ```
- ### 2.6、Flex 布局
  1. Flex 布局是什么？  
  Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。  
  任何一个容器都可以指定为 Flex 布局。
    ```css
    .box{
      display: flex;
    }
    .box{
      display: inline-flex;
    }  
    ```  
    注意，设为 Flex 布局以后，子元素的 float、clear 和 vertical-align 属性将失效。  
     
  2. 基本概念  
  采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。  
  容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做 main start，结束位置叫做 main end；交叉轴的开始位置叫做 cross start，结束位置叫做 cross end。  
  项目默认沿主轴排列。单个项目占据的主轴空间叫做 main size，占据的交叉轴空间叫做 cross size。

  3. 容器的属性
      - flex-direction
      - flex-wrap
      - flex-flow
      - justify-content
      - align-items
      - align-content  

     3.1 flex-direction属性  
     flex-direction 属性决定主轴的方向（即项目的排列方向）。
     ```css
     .box {
       flex-direction: row | row-reverse | column | column-reverse;
      }
     ```
     - row（默认值）：主轴为水平方向，起点在左端。  
     - row-reverse：主轴为水平方向，起点在右端。  
     - column：主轴为垂直方向，起点在上沿。  
     - column-reverse：主轴为垂直方向，起点在下沿。

     3.2 flex-wrap属性  
     默认情况下，项目都排在一条线（又称"轴线"）上。flex-wrap 属性定义，如果一条轴线排不下，如何换行。
     ```css
     .box{
       flex-wrap: nowrap | wrap | wrap-reverse;
      }
     ```
     - （1）nowrap（默认）：不换行。
     - （2）wrap：换行，第一行在上方。
     - （3）wrap-reverse：换行，第一行在下方

     3.3 flex-flow  
     flex-flow 属性是 flex-direction 属性和 flex-wrap 属性的简写形式，默认值为 row nowrap。
     ```css
     .box {
       flex-flow: <flex-direction> || <flex-wrap>;
      }
     ```

     3.4 justify-content 属性  
     justify-content 属性定义了项目在主轴上的对齐方式。
     ```css
     .box {
       justify-content: flex-start | flex-end | center | space-between | space-around;
      }
     ```
     - flex-start（默认值）：左对齐
     - flex-end：右对齐
     - center： 居中
     - space-between：两端对齐，项目之间的间隔都相等。
     - space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

     3.5 align-items 属性  
     align-items 属性定义项目在交叉轴上如何对齐。
     ```css
     .box {
       align-items: flex-start | flex-end | center | baseline | stretch;
      }
     ```
     - flex-start：交叉轴的起点对齐。
     - flex-end：交叉轴的终点对齐。
     - center：交叉轴的中点对齐。
     - baseline: 项目的第一行文字的基线对齐。
     - stretch（默认值）：如果项目未设置高度或设为 auto，将占满整个容器的高度。

     3.6 align-content 属性  
     align-content 属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
     ```css
     .box {
       align-content: flex-start | flex-end | center | space-between | space-around | stretch;
      }
     ```
     - flex-start：与交叉轴的起点对齐。
     - flex-end：与交叉轴的终点对齐。
     - center：与交叉轴的中点对齐。
     - space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
     - space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
     - stretch（默认值）：轴线占满整个交叉轴。

  四、项目的属性  
    以下6个属性设置在项目上。  
     - order  
     - flex-grow  
     - flex-shrink  
     - flex-basis  
     - flex  
     - align-self    

    4.1 order 属性  
     order 属性定义项目的排列顺序。数值越小，排列越靠前，默认为 0。   

     ```css
     .item {
       order: <integer>;
      }
     ```

    4.2 flex-grow 属性  
     flex-grow 属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。  

     ```css
     .item {
       flex-grow: <number>; /*default 0 */
      }
     ```  
     如果所有项目的 flex-grow 属性都为 1，则它们将等分剩余空间（如果有的话）。如果一个项目的 flex-grow 属性为 2，其他项目都为 1，则前者占据的剩余空间将比其他项多一倍。

    4.3 flex-shrink 属性  
     flex-shrink 属性定义了项目的缩小比例，默认为 1，即如果空间不足，该项目将缩小。 
     ```css
     .item {
       flex-shrink: <number>; /*default 1 */
     }
     ```
     如果所有项目的 flex-shrink 属性都为 1，当空间不足时，都将等比例缩小。如果一个项目的 flex-shrink 属性为 0，其他项目都为 1，则空间不足时，前者不缩小。  
      负值对该属性无效。 

    4.4 flex-basis 属性  
     flex-basis 属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为 auto，即项目的本来大小。
     ```css
     .item {
       flex-basis: <length> | auto; /*default auto*/
      }
     ```
     它可以设为跟 width 或 height 属性一样的值（比如 350px），则项目将占据固定空间。
    
    4.5 flex属性
     flex 属性是 flex-grow, flex-shrink 和 flex-basis 的简写，默认值为 0 1 auto。后两个属性可选。  
     ```css
     .item {
       flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
      }
     ```
     该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。  
     建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。  
    
    4.6 align-self属性  
     align-self 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖 align-items 属性。默认值为 auto，表示继承父元素的 align-items 属性，如果没有父元素，则等同于 stretch。
     ```css
     .item {
       align-self: auto | flex-start | flex-end | center | baseline | stretch;
      }
     ```
     该属性可能取 6 个值，除了 auto，其他都与 align-items 属性完全一致。
  
- ### 2.7、重绘和回流
  1. 浏览器渲染机制  
     - 浏览器采用流式布局模型（Flow Based Layout）  
     - 浏览器会把 HTML 解析成 DOM，把 CSS 解析成 CSSOM，DOM 和 CSSOM 合并就产生了渲染树（Render Tree）。  
     - 有了 RenderTree，我们就知道了所有节点的样式，然后计算他们在页面上的大小和位置，最后把节点绘制到页面上。  
     - 由于浏览器使用流式布局，对 Render Tree 的计算通常只需要遍历一次就可以完成，但 table 及其内部元素除外，他们可能需要多次计算，通常要花 3 倍于同等元素的时间，这也是为什么要避免使用 table 布局的原因之一。
  
  2. 重绘  
     由于节点的几何属性发生改变或者由于样式发生改变而不会影响布局的，称为重绘，例如 outline, visibility, color、background-color 等，重绘的代价是高昂的，因为浏览器必须验证 DOM 树上其他节点元素的可见性。
  
  3. 回流  
     回流是布局或者几何属性需要改变就称为回流。回流是影响浏览器性能的关键因素，因为其变化涉及到部分页面（或是整个页面）的布局更新。一个元素的回流可能会导致了其所有子元素以及 DOM 中紧随其后的节点、祖先节点元素的随后的回流。
     ```html
     <body>
      <div class="error">
          <h4>我的组件</h4>
          <p><strong>错误：</strong>错误的描述…</p>
          <h5>错误纠正</h5>
          <ol>
              <li>第一步</li>
              <li>第二步</li>
          </ol>
      </div>
      </body>
     ```
     在上面的 HTML 片段中，对该段落(`<p>`标签)回流将会引发强烈的回流，因为它是一个子节点。这也导致了祖先的回流（div.error 和 body – 视浏览器而定）。此外，`<h5>`和`<ol>`也会有简单的回流，因为其在 DOM 中在回流元素之后。大部分的回流将导致页面的重新渲染。  

     - 回流必定会发生重绘，重绘不一定会引发回流。
  
  4. 浏览器优化  
     现代浏览器大多都是通过队列机制来批量更新布局，浏览器会把修改操作放在队列中，至少一个浏览器刷新（即 16.6ms）才会清空队列，但当你获取布局信息的时候，队列中可能有会影响这些属性或方法返回值的操作，即使没有，浏览器也会强制清空队列，触发回流与重绘来确保返回正确的值。  

     主要包括以下属性或方法：
     - offsetTop、offsetLeft、offsetWidth、offsetHeight
     - scrollTop、scrollLeft、scrollWidth、scrollHeight
     - clientTop、clientLeft、clientWidth、clientHeight
     - width、height
     - getComputedStyle()
     - getBoundingClientRect()  

     所以，我们应该避免频繁的使用上述的属性，他们都会强制渲染刷新队列。
  
  5. 减少重绘与回流  
     1. CSS
     - 使用 transform 替代 top
     - 使用 visibility 替换 display: none ，因为前者只会引起重绘，后者会引发回流（改变了布局）
     - 避免使用 table 布局，可能很小的一个小改动会造成整个 table 的重新布局。
     - 尽可能在 DOM 树的最末端改变 class，回流是不可避免的，但可以减少其影响。尽可能在 DOM 树的最末端改变 class，可以限制了回流的范围，使其影响尽可能少的节点。
     - 避免设置多层内联样式，CSS 选择符从右往左匹配查找，避免节点层级过多。
     ```html
     <div>
      <a> <span></span> </a>
     </div>
     <style>
      span {
        color: red;
      }
      div > a > span {
        color: red;
      }
     </style>
     ```
     对于第一种设置样式的方式来说，浏览器只需要找到页面中所有的 span 标签然后设置颜色，但是对于第二种设置样式的方式来说，浏览器首先需要找到所有的 span 标签，然后找到 span 标签上的 a 标签，最后再去找到 div 标签，然后给符合这种条件的 span 标签设置颜色，这样的递归过程就很复杂。所以我们应该尽可能的避免写过于具体的 CSS 选择器，然后对于 HTML 来说也尽量少的添加无意义标签，保证层级扁平。  
     - 将动画效果应用到 position 属性为 absolute 或 fixed 的元素上，避免影响其他元素的布局，这样只是一个重绘，而不是回流，同时，控制动画速度可以选择 requestAnimationFrame。
     - 避免使用 CSS 表达式，可能会引发回流。
     - 将频繁重绘或者回流的节点设置为图层，图层能够阻止该节点的渲染行为影响别的节点，例如 will-change、video、iframe 等标签，浏览器会自动将该节点变为图层。
     - CSS3 硬件加速（GPU 加速），使用 css3 硬件加速，可以让 transform、opacity、filters 这些动画不会引起回流重绘 。但是对于动画的其它属性，比如 background-color 这些，还是会引起回流重绘的，不过它还是可以提升这些动画的性能。

     2. JavaScript
     - 避免频繁操作样式，最好一次性重写 style 属性，或者将样式列表定义为 class 并一次性更改 class 属性。
     - 避免频繁操作 DOM，创建一个 documentFragment，在它上面应用所有 DOM 操作，最后再把它添加到文档中。
     - 避免频繁读取会引发回流/重绘的属性，如果确实需要多次使用，就用一个变量缓存起来。
     - 对具有复杂动画的元素使用绝对定位，使它脱离文档流，否则会引起父元素及后续元素频繁回流。

- ### 2.8、几种常见的 CSS 布局  
  一、单列布局   
     常见的单列布局有两种：
     - header,content 和 footer 等宽的单列布局
     - header 与 footer 等宽,content 略窄的单列布局

     1. 第一种  
     对于第一种，先通过对 header,content,footer 统一设置 width：1000px;或者 max-width：1000px(这两者的区别是当屏幕小于 1000px 时，前者会出现滚动条，后者则不会，显示出实际宽度);然后设置 margin:auto 实现居中即可得到。
     ``` html
     <div class="header"></div>
     <div class="content"></div>
     <div class="footer"></div>
     ```
     ```css
     .header{
        margin:0 auto;
        max-width: 960px;
        height:100px;
        background-color: blue;
      }
      .content{
        margin: 0 auto;
        max-width: 960px;
        height: 400px;
        background-color: aquamarine;
      }
      .footer{
        margin: 0 auto;
        max-width: 960px;
        height: 100px;
        background-color: aqua;
      }
     ```
     2. 第二种  
     对于第二种，header、footer 的内容宽度不设置，块级元素充满整个屏幕，但 header、content 和 footer 的内容区设置同一个 width，并通过 margin:auto 实现居中。
     ```html
     <div class="header">
      <div class="nav"></div>
     </div>
     <div class="content"></div>
     <div class="footer"></div>
     ```
     ```css
     .header{
        margin:0 auto;
        max-width: 960px;
        height:100px;
        background-color: blue;
      }
      .nav{
        margin: 0 auto;
        max-width: 800px;
        background-color: darkgray;
        height: 50px;
      }
      .content{
        margin: 0 auto;
        max-width: 800px;
        height: 400px;
        background-color: aquamarine;
      }
      .footer{
        margin: 0 auto;
        max-width: 960px;
        height: 100px;
        background-color: aqua;
      }
     ```
  二、两列自适应布局  
  两列自适应布局是指一列由内容撑开，另一列撑满剩余宽度的布局方式  
  1. float+overflow:hidden  
  如果是普通的两列布局，浮动+普通元素的 margin 便可以实现，但如果是自适应的两列布局，利用 float+overflow:hidden 便可以实现，这种办法主要通过 overflow 触发 BFC,而 BFC 不会重叠浮动元素。由于设置 overflow:hidden 并不会触发 IE6-浏览器的 haslayout 属性，所以需要设置 zoom:1 来兼容 IE6-浏览器。具体代码如下：
  ```html
  <div class="parent" style="background-color: lightgrey;">
    <div class="left" style="background-color: lightblue;">
        <p>left</p>
    </div>
    <div class="right"  style="background-color: lightgreen;">
        <p>right</p>
        <p>right</p>
    </div>        
  </div>
  ```
  ```css
  .parent {
    overflow: hidden;
    zoom: 1;
  }
  .left {
    float: left;
    margin-right: 20px;
  }
  .right {
    overflow: hidden;
    zoom: 1;
  }
  ```
  2. Flex布局  
  Flex 布局，也叫弹性盒子布局，区区简单几行代码就可以实现各种页面的的布局。
  ```css
  /*html 部分同上*/
  .parent {
    display:flex;
  }  
  .right {
    margin-left:20px;
    flex:1;
  }
  ```
  3. grid 布局  
  Grid 布局，是一个基于网格的二维布局系统，目的是用来优化用户界面设计。
  ```css
  /*html 部分同上*/
  .parent {
    display:grid;
    grid-template-columns:auto 1fr;
    grid-gap:20px
  }
  ```
- ### 2.9 CSS 盒模型介绍  
  - 当对一个文档进行布局（lay out）的时候，浏览器的渲染引擎会根据标准之一的 CSS 基础框盒模型（CSS basic box model），将所有元素表示为一个个矩形的盒子（box）。CSS 决定这些盒子的大小、位置以及属性（例如颜色、背景、边框尺寸…）。  

  - 每个盒子由四个部分（或称区域）组成，其效用由它们各自的边界（Edge）所定义（原文：defined by their respective edges，可能意指容纳、包含、限制等）。如图，与盒子的四个组成区域相对应，每个盒子有四个边界：内容边界 Content edge、内边距边界 Padding Edge、边框边界 Border Edge、外边框边界 Margin Edge。

  - 内容区域 content area ，由内容边界限制，容纳着元素的“真实”内容，例如文本、图像，或是一个视频播放器。它的尺寸为内容宽度（或称 content-box 宽度）和内容高度（或称 content-box 高度）。它通常含有一个背景颜色（默认颜色为透明）或背景图像。

  - 如果 `box-sizing` 为 `content-box`（默认），则内容区域的大小可明确地通过 `width`、`min-width`、`max-width`、`height`、`min-height`，和 `max-height` 控制。

  - 内边距区域 padding area 由内边距边界限制，扩展自内容区域，负责延伸内容区域的背景，填充元素中内容与边框的间距。它的尺寸是 padding-box 宽度 和 padding-box 高度。
  
  - 内边距的粗细可以由 `padding-top`、`padding-right`、`padding-bottom`、`padding-left`，和简写属性 `padding` 控制。

  - 边框区域 border area 由边框边界限制，扩展自内边距区域，是容纳边框的区域。其尺寸为 border-box 宽度 和 border-box 高度。
  
  - 边框的粗细由 `border-width` 和简写的 `border` 属性控制。如果 `box-sizing` 属性被设为 `border-box`，那么边框区域的大小可明确地通过 `width`、`min-width`, `max-width`、`height`、`min-height`，和 `max-height` 属性控制。假如框盒上设有背景（`background-color` 或 `background-image`），背景将会一直延伸至边框的外沿（默认为在边框下层延伸，边框会盖在背景上）。此默认表现可通过 CSS 属性 `background-clip` 来改变。

  - 外边距区域 margin area 由外边距边界限制，用空白区域扩展边框区域，以分开相邻的元素。它的尺寸为 margin-box 宽度 和 margin-box 高度。
  
  - 外边距区域的大小由 `margin-top`、`margin-right`、`margin-bottom`、`margin-left`，和简写属性 `margin` 控制。在发生外边距合并的情况下，由于盒之间共享外边距，外边距不容易弄清楚。
  
  - 最后，请注意，除可替换元素外，对于行内元素来说，尽管内容周围存在内边距与边框，但其占用空间（每一行文字的高度）则由 line-height 属性决定，即使边框和内边距仍会显示在内容周围。

- ### 2.10、水平垂直居中的布局
  1. 定宽高  
  一、绝对定位和负 magin 值
     ```html
     <template>
        <div id="app">
          <div class="box">
            <div class="children-box"></div>
          </div>
        </div>
      </template>
      <style type="text/css">
      .box {
        width: 200px;
        height: 200px;
        border: 1px solid red;
        position: relative;
      }
      .children-box {
          position: absolute;
          width: 100px;
          height: 100px;
          background: yellow;
          left: 50%;
          top: 50%;
          margin-left: -50px;
          margin-top: -50px; 
        }
     </style>
     ```
  二、绝对定位 + transform
     ```html
        <template>
        <div id="app">
            <div class="box">
                <div class="children-box"></div>
            </div>
        </div>
        </template>
        <style type="text/css">
        .box {
            width: 200px;
            height: 200px;
            border: 1px solid red;
            position: relative;
        }
        .children-box {
            position: absolute;
            width: 100px;
            height: 100px;
            background: yellow;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%); 
        }
     </style>
     ```
  
  三、绝对定位 + left/right/bottom/top + margin
     ```html
      <template>
        <div id="app">
            <div class="box">
                <div class="children-box"></div>
            </div>
        </div>
      </template>
      <style type="text/css">
      .box {
          width: 200px;
          height: 200px;
          border: 1px solid red;
          position: relative;
      }
      .children-box {
          position: absolute;
          display: inline;
          top: 0;
          left: 0;
          right: 0;
          bottom: 0px;
          background: yellow;
          margin: auto;
          height: 100px;
          width: 100px;
      }
      </style>
     ```
  四、flex 布局
     ```html
        <template>
          <div id="app">
              <div class="box">
                  <div class="children-box"></div>
              </div>
          </div>
      </template>
      <style type="text/css">
      .box {
          width: 200px;
          height: 200px;
          border: 1px solid red;
          display: flex;
          justify-content: center;
          align-items: center;
      }
      .children-box {
          background: yellow;
          height: 100px;
          width: 100px;
      }
      </style>
     ```
  五、grid 布局  
     ```html
      <template>
      <div id="app">
          <div class="box">
              <div class="children-box"></div>
          </div>
      </div>
      </template>
      <style type="text/css">
      .box {
          width: 200px;
          height: 200px;
          border: 1px solid red;
          display: grid;
      }
      .children-box {
          width: 100px;
          height: 100px;
          background: yellow;
          margin: auto;
      }
      </style>
     ```
  
  2. 不定宽高  
  一、绝对定位 + transform
     ```html
     <template>
        <div id="app">
            <div class="box">
                <div class="children-box">111111</div>
            </div>
        </div>
      </template>
      <style type="text/css">
      .box {
          width: 200px;
          height: 200px;
          border: 1px solid red;
          position: relative;
      }
      .children-box {
        position: absolute;
        background: yellow;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
      }
      </style>
     ```
  二、table-cell
     ```html
      <template>
        <div id="app">
            <div class="box">
                <div class="children-box">111111</div>
            </div>
        </div>
      </template>
      <style type="text/css">
        .box {
            width: 200px;
            height: 200px;
            border: 1px solid red;
            display: table-cell;
            text-align: center;
            vertical-align: middle;
        }
        .children-box {
          background: yellow;
          display: inline-block;
        }
      </style>
     ```
  三、flex 布局
     ```html
     <template>
      <div id="app">
          <div class="box">
              <div class="children-box">11111111</div>
          </div>
      </div>
      </template>
      <style type="text/css">
      .box {
          width: 200px;
          height: 200px;
          border: 1px solid red;
          display: flex;
          justify-content: center;
          align-items: center;
      }
      .children-box {
          background: yellow;
      }
      </style>
     ```

## 3、vue 组件通信方式
- ### 3.1、props/@on+\$emit
   用于实现父子组件间通信。通过 props 可以把父组件的消息传递给子组件：  
   
   ```html
   // parent.vue  
   <child :title="title"></child>
   ```
   ```javascript
   // child.vue
   props: {
     title: {
       type: String,
       default: '',
      }
    }
   ```
   这样一来 this.title 就直接拿到从父组件中传过来的 title 的值了。注意，你不应该在子组件内部直接改变 prop。  
   > 单向数据流   
   所有的 prop 都使得其父子 prop 之间形成了一个单向下行绑定：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外变更父级组件的状态，从而导致你的应用的数据流向难以理解。  
   额外的，每次父级组件发生变更时，子组件中所有的 prop 都将会刷新为最新的值。这意味着你不应该在一个子组件内部改变 prop。如果你这样做了，Vue 会在浏览器的控制台中发出警告。  

   而通过 @on+\$emit 组合可以实现子组件给父组件传递信息：
   ```html
   // parent.vue
   <child @changeTitle="changeTitle"></child>
   ```
   ```javascript
   // child.vue
   this.$emit('changeTitle', '我们都是中国人')
   ```
- ### 3.2、attrs和listeners  
   Vue_2.4 中新增的 $attrs/$listeners 可以进行跨级的组件通信。\$attrs 包含了父级作用域中不作为 prop 的属性绑定（class 和 style 除外），好像听起来有些不好理解？没事，看下代码就知道是什么意思了： 
   ```html
   // 父组件 index.vue
   <list class="list-box" title="标题" desc="描述" :list="list"></list>
   ```
   ```javascript
   // 子组件 list.vue
    props: {
      list: [],
    },
    mounted() {
      console.log(this.$attrs) // {title: "标题", desc: "描述"}
    }
   ```
   在上面的父组件 index.vue 中我们给子组件 list.vue 传递了 4 个参数，但是在子组件内部 props 里只定义了一个 list，那么此时 this.\$attrs 的值是什么呢？首先要去除 props 中已经绑定了的，然后再去除 class 和 style，最后剩下 title 和 desc 结果和打印的是一致的。基于上面代码的基础上，我们在给 list.vue 中加一个子组件：
   ```html
   // 子组件 list.vue
   <detail v-bind="$attrs"></detial>
   ```
   ```javascript
    // 孙子组件 detail.vue
    // 不定义 props，直接打印 $attrs
    mounted() {
        console.log(this.$attrs) // {title: "标题", desc: "描述"}
    }
   ```
   在子组件中我们定义了一个 v-bind="$attrs" 可以把父级传过来的参数，去除 props、class 和 style 之后剩下的继续往下级传递，这样就实现了跨级的组件通信。  
   $attrs 是可以进行跨级的参数传递，实现父到子的通信；同样的，通过 $listeners 用类似的操作方式可以进行跨级的事件传递，实现子到父的通信。$listeners 包含了父作用域中不含 .native 修饰的 v-on 事件监听器，通过 v-on="$listeners" 传递到子组件内部。
   ```html
   // 父组件 index.vue
   <list @change="change" @update.native="update"></list>
   // 子组件 list.vue
   <detail v-on="$listeners"></detail>
   ```
   ```javascript
   // 孙子组件 detail.vue
   mounted() {
     this.$listeners.change()
     this.$listeners.update() 
     // TypeError: this.\$listeners.update is not a function
    }
   ```
- ### 3.3、provide/inject 组合拳  
   provide/inject 组合以允许一个祖先组件向其所有子孙后代注入一个依赖，可以注入属性和方法，从而实现跨级父子组件通信。在开发高阶组件和组件库的时候尤其好用。
   ```javascript
   // 父组件 index.vue
   data() {
     return {
       title: 'bubuzou.com',
      }
    }
   provide() {
    return {
      detail: {
        title: this.title,
        change: (val) => {
          console.log( val )
        }
      }
    }
   }
   // 孙子组件 detail.vue
   inject: ['detail'],
   mounted() {
     console.log(this.detail.title) // bubuzou.com
     this.detail.title = 'hello world' // 虽然值被改变了，但是父组件中 title 并不会重新渲染
     this.detail.change('改变后的值') // 执行这句后将打印：改变后的值
     }
   ```
   > provide 和 inject 的绑定对于原始类型来说并不是可响应的。这是刻意为之的。然而，如果你传入了一个可监听的对象，那么其对象的 property 还是可响应的。这也就是为什么在孙子组件中改变了 title，但是父组件不会重新渲染的原因。

- ### 3.4 EventBus  
   以上三种方式都是只能从父到子方向或者子到父方向进行组件的通信，而我就比较牛逼了，我还能进行兄弟组件之间的通信，甚至任意 2 个组件间通信。利用 Vue 实例实现一个 EventBus 进行信息的发布和订阅，可以实现在任意 2 个组件之间通信。有两种写法都可以初始化一个 eventBus 对象：  
   1、通过导出一个 Vue 实例，然后再需要的地方引入：
   ```javascript
   // eventBus.js
   import Vue from 'vue'
   export const EventBus = new Vue()
   ```
   使用 EventBus 订阅和发布消息：
   ```javascript
   import {EventBus} from '../utils/eventBus.js'
   // 订阅处
   EventBus.$on('update', val => {})
   // 发布处
   EventBus.$emit('update', '更新信息')
   ```
   2、在 main.js 中初始化一个全局的事件总线：
   ```javascript
   // main.js
   Vue.prototype.\$eventBus = new Vue()
   ```
   使用：
   ```javascript
   // 需要订阅的地方
   this.$eventBus.$on('update', val => {})
   
   // 需要发布信息的地方
   this.$eventBus.$emit('update', '更新信息')
   ```
   如果想要移除事件监听，可以这样来：
   ```javascript
   this.$eventBus.$off('update', {})
   ```
  上面介绍了两种写法，推荐使用第二种全局定义的方式，可以避免在多处导入 EventBus 对象。这种组件通信方式只要订阅和发布的顺序得当，且事件名称保持唯一性，理论上可以在任何 2 个组件之间进行通信，相当的强大。但是方法虽好，可不要滥用，建议只用于简单、少量业务的项目中，如果在一个大型繁杂的项目中无休止的使用该方法，将会导致项目难以维护。

- ### 3.5 Vuex 进行全局的数据管理  
   Vuex 是一个专门服务于 Vue.js 应用的状态管理工具。适用于中大型应用。Vuex 中有一些专有概念需要先了解下：  
   - State：用于数据的存储，是 store 中的唯一数据源；
   - Getter：类似于计算属性，就是对 State 中的数据进行二次的处理，比如筛选和对多个数据进行求值等；
   - Mutation：类似事件，是改变 Store 中数据的唯一途径，只能进行同步操作；
   - Action：类似 Mutation，通过提交 Mutation 来改变数据，而不直接操作 State，可以进行异步操作；
   - Module：当业务复杂的时候，可以把 store 分成多个模块，便于维护；
   对于这几个概念有各种对应的 map 辅助函数用来简化操作，比如 mapState，如下三种写法其实是一个意思，都是为了从 state 中获取数据，并且通过计算属性返回给组件使用。
   ```javascript
   computed: {
    count() {
      return this.$store.state.count
    },
    ...mapState({
      count: state => state.count
    }),
    ...mapState(['count']),
   },
   ```
   又比如 mapMutations， 以下两种函数的定义方式要实现的功能是一样的，都是要提交一个 mutation 去改变 state 中的数据： 
   ```javascript
      methods: {
        increment() {
          this.$store.commit('increment')
        },
      ...mapMutations(['increment']),
    }
   ```
   接下来就用一个极简的例子来展示 Vuex 中任意 2 个组件间的状态管理。  
   1、 新建 store.js
   ```javascript
   import Vue from 'vue'
   import Vuex from 'vuex'
   Vue.use(Vuex)
   export default new Vuex.Store({
     state: {
       count: 0,
      },
    mutations: {
      increment(state) {
        state.count++
      },
      decrement(state) {
        state.count--
      }
      },
    })
   ```
   2、 创建一个带 store 的 Vue 实例
   ```javascript
   import Vue from 'vue'
   import App from './App.vue'
   import router from './router'
   import store from './utils/store'
   new Vue({
     router,
     store,
     render: h => h(App)
    }).$mount('#app')
   ```
   3、 任意组件 A 实现点击递增
   ```html
   <template>
    <p @click="increment">click to increment：{{count}}</p>
   </template>
   <script>
   import {mapState, mapMutations} from 'vuex'
   export default {
      computed: {
          ...mapState(['count'])
      },
      methods: {
          ...mapMutations(['increment'])
      },
    }
   </script>
   ```
   4、 任意组件 B 实现点击递减 
   ```html
   <template>
    <p @click="decrement">click to decrement：{{count}}</p>
   </template>
   <script>
    import {mapState, mapMutations} from 'vuex'
    export default {
      computed: {
          ...mapState(['count'])
      },
      methods: {
          ...mapMutations(['decrement'])
      },
    }
   </script>
   ```
   以上只是用最简单的 vuex 配置去实现组件通信，当然真实项目中的配置肯定会更复杂，比如需要对 State 数据进行二次筛选会用到 Getter，然后如果需要异步的提交那么需要使用 Action，再比如如果模块很多，可以将 store 分模块进行状态管理。对于 Vuex 更多复杂的操作还是建议去看 Vuex 官方文档，然后多写例子。

- ### 3.6 Vue.observable 实现 mini vuex  
   这是一个 Vue2.6 中新增的 API，用来让一个对象可以响应。我们可以利用这个特点来实现一个小型的状态管理器。
   ```javascript
   // store.js
   import Vue from 'vue'
   export const state = Vue.observable({
     count: 0,
    })
   export const mutations = {
    increment() {
       state.count++
      }
    decrement() {
      state.count--
    }
   }
   ```
   ```html
    // parent.vue
    <template>
      <p>{{ count }}</p>
    </template>
    <script>
      import { state } from '../store'
      export default {
      computed: {
          count() {
              return state.count
          }
      }
      }
    </script>
   ```
   ```javascript
   // child.vue
   import { mutations } from '../store'
   export default {
     methods: {
       handleClick() {
         mutations.increment()
        }
      }
    }
   ```

- ### 3.7、$refs、children、parent、root  
   通过给子组件定义 ref 属性可以使用 \$refs 来直接操作子组件的方法和属性。
   ```html
   <child ref="list"></child>
   ```
   比如子组件有一个 getList 方法，可以通过如下方式进行调用，实现父到子的通信：
   ```javascript
   this.$refs.list.getList()
   ```
   除了 $refs 外，其他 3 个都是自 Vue 实例创建后就会自动包含的属性，使用和上面的类似。
