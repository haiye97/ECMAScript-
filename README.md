ECMAScript 6入门（http://es6.ruanyifeng.com/#docs/intro）


一、ECMAScript 6简介
1、ECMAScript 和 JavaScript 的关系
ECMAScript 和 JavaScript 的关系是，前者是后者的规格，后者是前者的一种实现（另外的 ECMAScript 方言还有 Jscript 和 ActionScript）。日常场合，这两个词是可以互换的.
2、ES6 和 ECMAScript2015 的关系 
ES6 既是一个历史名词，也是一个泛指，含义是5.1版以后的 JavaScript 的下一代标准，涵盖了ES2015、ES2016、ES2017等等，而ES2015 则是正式名称，特指该年发布的正式版本的语言标准。本书中提到 ES6 的地方，一般是指 ES2015 标准，但有时也是泛指“下一代 JavaScript 语言”。
3、Babel转码器
4、Traceur转码器





二、let 和 const 命令
1、let命令
ES6 新增了let命令，用来声明变量。它的用法类似于var，但是所声明的变量，只在let命令所在的代码块内有效。for循环还有一个特别之处，就是设置循环变量的那部分是一个父作用域，而循环体内部是一个单独的子作用域。

上面代码正确运行，输出了3次abc。这表明函数内部的变量i与循环变量i不在同一个作用域，有各自单独的作用域。
let特性：不存在变量提升（变量一定在声明之后使用）、暂时性死区（ 存在全局变量tmp，但是块级作用域内let又声明了一个局部变量tmp，导致后者绑定这个块级作用域，所以在let声明变量前，对tmp赋值会报错。）、不能重复声明（ 不允许在相同作用域内，重复声明同一个变量。 不能在函数内部重新声明参数。）

2、块级作用域
3、const命令
const声明一个只读的常量。一旦声明，常量的值就不能改变。
const特性：不提升、不可重复声明、只在声明所在的块级作用域内有效
const实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址不得改动， const只能保证这个指针是固定的，至于它指向的数据结构是不是可变的，就完全不能控制了。
4、顶层对象的属性
顶层对象，在浏览器环境指的是window对象，在Node指的是global对象。ES5之中，顶层对象的属性与全局变量是等价的。
ES6为了改变这一点，一方面规定，为了保持兼容性，var命令和function命令声明的全局变量，依旧是顶层对象的属性；另一方面规定，let命令、const命令、class命令声明的全局变量，不属于顶层对象的属性。也就是说，从ES6开始，全局变量将逐步与顶层对象的属性脱钩。
5、global对象





三、变量的解构赋值
1、数组的解构赋值
本质上，这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值。
事实上，只要某种数据结构具有 Iterator 接口，都可以采用数组形式的解构赋值。
默认值： ES6 内部使用严格相等运算符（===），判断一个位置是否有值。所以，如果一个数组成员不严格等于undefined，默认值是不会生效的。 默认值是一个表达式，那么这个表达式是惰性求值的，即只有在用到的时候，才会求值。

2、对象的解构赋值
数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。
对象的解构赋值的内部机制，是先找到同名属性，然后再赋给对应的变量。真正被赋值的是后者，而不是前者。

上面代码中，foo是匹配的模式，baz才是变量。真正被赋值的是变量baz，而不是模式foo。
由于数组本质是特殊的对象，因此可以对数组进行对象属性的解构。

3、字符串的解构赋值
字符串也可以解构赋值。这是因为此时，字符串被转换成了一个类似数组的对象。
4、数值和布尔值的解构赋值
解构赋值时，如果等号右边是数值和布尔值，则会先转为对象。 由于undefined和null无法转为对象，所以对它们进行解构赋值，都会报错。
5、函数参数的解构赋值

函数参数的解构也可以使用默认值。（对比下面二段代码）

6、圆括号问题
可以使用圆括号：情况只有一种：赋值语句的非模式部分，可以使用圆括号。

7、用途
交换变量的值、 从函数返回多个值、 函数参数的定义、 提取JSON数据、 函数参数的默认值、 遍历Map结构、 输入模块的指定方法




四、字符串的扩展
1、字符的Unicode表示法
2、codePointAt()
JavaScript内部，字符以UTF-16的格式储存，每个字符固定为2个字节。对于那些需要4个字节储存的字符（Unicode码点大于0xFFFF的字符），JavaScript会认为它们是两个字符。
ES6提供了codePointAt方法，能够正确处理4个字节储存的字符，返回一个字符的码点。
3、 String.fromCharCode()
ES5提供String.fromCharCode方法，用于从码点返回对应字符，但是这个方法不能识别32位的UTF-16字符（Unicode编号大于0xFFFF）。
ES6提供了String.fromCodePoint方法，可以识别大于0xFFFF的字符，弥补了String.fromCharCode方法的不足。在作用上，正好与codePointAt方法相反。
4、字符串遍历接口（for...of...）
5、at()
ES5对字符串对象提供charAt方法，返回字符串给定位置的字符。该方法不能识别码点大于0xFFFF的字符。
有一个提案，提出字符串实例的at方法，可以识别Unicode编号大于0xFFFF的字符，返回正确的字符。
6、normalize()
ES6提供字符串实例的normalize()方法，用来将字符的不同表示方法统一为同样的形式，这称为Unicode正规化。
7、includes()、startsWith()、endsWith()
JavaScript只有indexOf方法，可以用来确定一个字符串是否包含在另一个字符串中。ES6又提供了三种新方法。
includes()：返回布尔值，表示是否找到了参数字符串。
startsWith()：返回布尔值，表示参数字符串是否在源字符串的头部。
endsWith()：返回布尔值，表示参数字符串是否在源字符串的尾部。（ 针对前n个字符）
这三个方法都支持第二个参数，表示开始搜索的位置。
8、 repeat()
返回一个新字符串，表示将原字符串重复n次。
9、 padStart()、 padEnd()
ES2017 引入了字符串补全长度的功能。如果某个字符串不够指定长度，会在头部或尾部补全。
10、模板字符串
模板字符串（template string）是增强版的字符串，用反引号（`）标识。
11、实例：模板编译
(?)12、标签模板
13、String.raw()
String.raw方法，往往用来充当模板字符串的处理函数，返回一个斜杠都被转义（即斜杠前面再加一个斜杠）的字符串，对应于替换变量后的模板字符串。

14、模板字符串的限制（提案）







五、正则的扩展
1、RegExp构造函数
在 ES5 中，RegExp构造函数的参数有两种情况。但当第一个参数正则对象中有修饰符则不能有第二个参数， ES6 改变了这种行为。如果RegExp构造函数第一个参数是一个正则对象，那么可以使用第二个参数指定修饰符。而且，返回的正则表达式会忽略原有的正则表达式的修饰符，只使用新指定的修饰符。

2、字符串的正则方法
字符串对象共有4个方法，可以使用正则表达式：match()、replace()、search()和split()。
ES6 将这4个方法，在语言内部全部调用RegExp的实例方法，从而做到所有与正则相关的方法，全都定义在RegExp对象上。

String.prototype.match 调用 RegExp.prototype[Symbol.match]
String.prototype.replace 调用 RegExp.prototype[Symbol.replace]
String.prototype.search 调用 RegExp.prototype[Symbol.search]
String.prototype.split 调用 RegExp.prototype[Symbol.split]
3、u修饰符
ES6 对正则表达式添加了u修饰符，含义为“Unicode模式”，用来正确处理大于\uFFFF的 Unicode 字符。也就是说，会正确处理四个字节的 UTF-16 编码。
一旦加上u修饰符号，就会修改下面这些正则表达式的行为：点字符、 Unicode 字符表示法、 量词、 预定义模式、 i 修饰符
4、y修饰符
y修饰符的作用与g修饰符类似，也是全局匹配，后一次匹配都从上一次匹配成功的下一个位置开始。不同之处在于，g修饰符只要剩余位置中存在匹配就可，而y修饰符确保匹配必须从剩余的第一个位置开始，这也就是“粘连”的涵义。

5、sticky属性
与y修饰符相匹配，ES6 的正则对象多了sticky属性，表示是否设置了y修饰符。

6、flags属性
ES6 为正则表达式新增了flags属性，会返回正则表达式的修饰符。

7、s修饰符：dotAll修饰符（提案）
引入/s修饰符，使得.可以匹配任意单个字符。
8、后行断言（提案）
9、Unicode属性类（提案）
10、具名组匹配（提案）
正则表达式使用圆括号进行组匹配。组匹配的一个问题是，每一组的匹配含义不容易看出来，而且只能用数字序号引用，要是组的顺序变了，引用的时候就必须修改序号。现在有一个“具名组匹配”（Named Capture Groups）的提案，允许为每一个组匹配指定一个名字，既便于阅读代码，又便于引用。

上面代码中，“具名组匹配”在圆括号内部，模式的头部添加“问号 + 尖括号 + 组名”（?<year>），然后就可以在exec方法返回结果的groups属性上引用该组名。同时，数字序号（matchObj[1]）依然有效。
如果要在正则表达式内部引用某个“具名组匹配”，可以使用\k<组名>的写法。









六、数值的扩展
1、二进制和八进制表示法
ES6 提供了二进制和八进制数值的新的写法，分别用前缀0b（或0B）和0o（或0O）表示。 从 ES5 开始，在严格模式之中，八进制就不再允许使用前缀0表示。
2、Number.isFinite(),Number.isNaN()
它们与传统的全局方法isFinite()和isNaN()的区别在于，传统方法先调用Number()将非数值的值转为数值，再进行判断，而这两个新方法只对数值有效，Number.isFinite()对于非数值一律返回false, Number.isNaN()只有对于NaN才返回true，非NaN一律返回false。
3、Number.parseInt(),Number.parseFloat()
ES6 将全局方法parseInt()和parseFloat()，移植到Number对象上面，行为完全保持不变。
4、Number.inInteger()
需要注意的是，在 JavaScript 内部，整数和浮点数是同样的储存方法，所以3和3.0被视为同一个值。
5、Number.EPSILON
ES6在Number对象上面，新增一个极小的常量Number.EPSILON。 Number.EPSILON的实质是一个可以接受的误差范围。
6、安全整数和Number.inSafeInteger()
JavaScript能够准确表示的整数范围在-2^53到2^53之间（不含两个端点），超过这个范围 ，无法精确表示这个值。 ES6引入了Number.MAX_SAFE_INTEGER和Number.MIN_SAFE_INTEGER这两个常量，用来表示这个范围的上下限。
7、Math对象的扩展
ES6在Math对象上新增了17个与数学相关的方法。所有这些方法都是静态方法，只能在Math对象上调用。
Math.trunc()、 Math.trunc()。。。。。。。。
8、Math.signbit()
Math.sign()用来判断一个值的正负，但是如果参数是-0，它会返回-0。 Math.signbit()方法判断一个数的符号位是否设置了。
9、指数运算符
注意，在 V8 引擎中，指数运算符与Math.pow的实现不相同，对于特别大的运算结果，两者会有细微的差异。

10、Integer数据类型（提案）
引入了新的数据类型 Interger（整数） ，来解决大于 53个二进制位的整数，JavaScript 是无法精确表示的，这使得 JavaScript 不适合进行科学和金融方面的精确计算。











七、函数的扩展
1、函数参数的默认值
参数变量是默认声明的，所以不能用let或const再次声明。 使用参数默认值时，函数不能有同名参数。 一个容易忽略的地方是，参数默认值不是传值的，而是每次都重新计算默认值表达式的值。也就是说，参数默认值是惰性求值的。

与解构赋值默认值结合使用



上面两种写法都对函数的参数设定了默认值，区别是写法一函数参数的默认值是空对象，但是设置了对象解构赋值的默认值；写法二函数参数的默认值是一个有具体属性的对象，但是没有设置对象解构赋值的默认值。
函数的length属性：将返回没有指定默认值的参数个数。 如果设置了默认值的参数不是尾参数，那么length属性也不再计入后面的参数了。
作用域： 一旦设置了参数的默认值，函数进行声明初始化时，参数会形成一个单独的作用域（context）。

函数f调用时，参数y = x形成一个单独的作用域。这个作用域里面，变量x本身没有定义，所以指向外层的全局变量x。函数调用时，函数体内部的局部变量x影响不到默认值变量x。

函数foo的参数形成一个单独作用域。这个作用域里面，首先声明了变量x，然后声明了变量y，y的默认值是一个匿名函数。这个匿名函数内部的变量x，指向同一个作用域的第一个参数x。函数foo内部又声明了一个内部变量x，该变量与第一个参数x由于不是同一个作用域，所以不是同一个变量，因此执行y后，内部变量x和外部全局变量x的值都没变。

如果将var x = 3的var去除，函数foo的内部变量x就指向第一个参数x，与匿名函数内部的x是一致的，所以最后输出的就是2，而外层的全局变量x依然不受影响。
2、rest参数
ES6 引入 rest 参数（形式为...变量名），用于获取函数的多余参数，这样就不需要使用arguments对象了， rest 参数之后不能再有其他参数（即只能是最后一个参数），否则会报错。 函数的length属性，不包括 rest 参数。
3、严格模式
从 ES5 开始，函数内部可以设定为严格模式（'use strict';）。 ES2016 做了一点修改，规定只要函数参数使用了默认值、解构赋值、或者扩展运算符，那么函数内部就不能显式设定为严格模式，否则会报错。
4、name属性
函数的name属性，返回该函数的函数名。 需要注意的是，ES6 对这个属性的行为做出了一些修改。如果将一个匿名函数赋值给一个变量，ES5 的name属性，会返回空字符串，而 ES6 的name属性会返回实际的函数名。
5、箭头函数

箭头函数有几个使用注意点。
（1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
（2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
（3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。
（4）不可以使用yield命令，因此箭头函数不能用作 Generator 函数。
上面四点中，第一点尤其值得注意。this对象的指向是可变的，但是在箭头函数中，它是固定的。
6、绑定this（ES7提案）
箭头函数可以绑定this对象，大大减少了显式绑定this对象的写法（call、apply、bind）
7、尾调用优化
指某个函数的最后一步是调用另一个函数。 “尾调用优化”对递归操作意义重大， ES6 中只要使用尾递归，就不会发生栈溢出，相对节省内存。 ES6 的尾调用优化只在严格模式下开启，正常模式是无效的。
8、函数参数的尾逗号
ES2017 允许函数的最后一个参数有尾逗号（trailing comma）。






八、数组的扩展
1、扩展运算符
扩展运算符（spread）是三个点（...）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列。array.push(...items)和add(...numbers)这两行，都是函数的调用，它们的都使用了扩展运算符。该运算符将一个数组，变为参数序列。
替代数组的apply方法

应用：合并数组、与解构赋值结合（放到最后一位）、函数的返回值、字符串、实现了Iterator接口的对象、Map和Set结构，Generator函数

2、Array.form()
Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括ES6新增的数据结构Set和Map）。 所谓类似数组的对象，本质特征只有一点，即必须有length属性。因此，任何有length属性的对象，都可以通过Array.from方法转为数组，而此时扩展运算符就无法转换。
3、Array.of()
Array.of方法用于将一组值，转换为数组。
4、数组实例的copyWithin()
数组实例的copyWithin方法，在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。也就是说，使用这个方法，会修改当前数组。
5、数组实例的find()和findIndex()
数组实例的find方法，用于找出第一个符合条件的数组成员。 indexOf方法无法识别数组的NaN成员，但是findIndex方法可以借助Object.is方法做到。
6、数组实例的fill()
fill方法使用给定值，填充一个数组。
7、数组实例的entries()、keys()和values()
ES6 提供三个新的方法——entries()，keys()和values()——用于遍历数组。 可以用for...of循环进行遍历，唯一的区别是keys()是对键名的遍历、values()是对键值的遍历，entries()是对键值对的遍历。
8、数组实例的includes()
Array.prototype.includes方法返回一个布尔值，表示某个数组是否包含给定的值，与字符串的includes方法类似。
9、数组的空位
数组的空位指，数组的某一个位置没有任何值。 ES6 则是明确将空位转为undefined。







九、对象的扩展
1、属性的简洁表示法
ES6 允许直接写入变量和函数，作为对象的属性和方法。 ES6 允许在对象之中，直接写变量。这时，属性名为变量名, 属性值为变量的值。

除了属性简写，方法也可以简写。

2、属性名表示法
表达式还可以用于定义方法名。

注意，属性名表达式与简洁表示法，不能同时使用，会报错。
属性名表达式如果是一个对象，默认情况下会自动将对象转为字符串[object Object]，这一点要特别小心。

上面代码中，[keyA]和[keyB]得到的都是[object Object]，所以[keyB]会把[keyA]覆盖掉，而myObject最后只有一个[object Object]属性。
3、方法的name属性
分情况获取
4、Object.is()
ES6提出“Same-value equality”（同值相等）算法，它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。 不同之处只有两个：一是+0不等于-0，二是NaN等于自身。
5、Object.assign()
Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。 由于undefined和null无法转成对象，所以如果它们作为唯一参数，就会报错， 如果undefined和null不在首参数，就不会报错。注意字符串、布尔值和数值情况。 Object.assign方法实行的是浅拷贝，而不是深拷贝。也就是说，如果源对象某个属性的值是对象，那么目标对象拷贝得到的是这个对象的引用。 对于嵌套的对象，一旦遇到同名属性，Object.assign的处理方法是替换，而不是添加。
常用用途：为对象添加属性、为对象添加方法、克隆对象、合并多个对象、为属性指定默认值
6、属性的可枚举性
7、属性的遍历
ES6 一共有5种方法可以遍历对象的属性。
（1）for...in
for...in循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。
（2）Object.keys(obj)
Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）。
（3）Object.getOwnPropertyNames(obj)
Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）。
（4）Object.getOwnPropertySymbols(obj)
Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有 Symbol 属性。
（5）Reflect.ownKeys(obj)
Reflect.ownKeys返回一个数组，包含对象自身的所有属性，不管属性名是 Symbol 或字符串，也不管是否可枚举。
以上的5种方法遍历对象的属性，都遵守同样的属性遍历的次序规则。
首先遍历所有属性名为数值的属性，按照数字排序。
其次遍历所有属性名为字符串的属性，按照生成时间排序。
最后遍历所有属性名为 Symbol 值的属性，按照生成时间排序。
8、__proto__属性，Object.setPrototypeOf()，Object.getPrototypeOf()
9、Object.keys()，Object.values()，Object.entries()
10、对象的扩展运算符
11、Object.getOwnPropertyDescriptors()
ES5 一个Object.getOwnPropertyDescriptor方法，返回某个对象属性的描述对象（descriptor）。
ES2017 引入了Object.getOwnPropertyDescriptors方法，返回指定对象所有自身属性（非继承属性）的描述对象。
12、Null传导运算符（提案）
引入了“Null 传导运算符”（null propagation operator）?.，简化上面的写法。






十、Symbol（新数据类型）
1、概述
ES5 的对象属性名都是字符串，这容易造成属性名的冲突。 ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值。它是 JavaScript 语言的第七种数据类型。不要使用new来实例化。
2、作为属性名的Symbol
3、实例：消除魔术字符串
4、属性名的遍历
Symbol 作为属性名，该属性不会出现在for...in、for...of循环中，也不会被Object.keys()、Object.getOwnPropertyNames()、JSON.stringify()返回。但是，它也不是私有属性，有一个个Object.getOwnPropertySymbols方法，可以获取指定对象的所有 Symbol 属性名。 Reflect.ownKeys方法可以返回所有类型的键名，包括常规键名和 Symbol 键名。
以 Symbol 值作为名称的属性，不会被常规方法遍历得到。我们可以利用这个特性，为对象定义一些非私有的、但又希望只用于内部的方法。
5、Symbol.for()，Symbol.keyFor()
重新使用同一个Symbol值，Symbol.for方法可以做到这一点。

Symbol.keyFor方法返回一个已登记的 Symbol 类型值的key。如上面代码第一行，返回的是“bar”，第二行代码返回“undefined”
6、实例：模板的Singleton模式
Singleton模式指的是调用一个类，任何时候返回的都是同一个实例。
7、内置的Symbol值
ES6还提供了11个内置的Symbol值，指向语言内部使用的方法。











十一、Set和Map数据结构（新数据结构）

1、Set（与数组之间的转换，数组去重）
ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。 Set 本身是一个构造函数，用来生成 Set 数据结构。（===）基本相同，但Set认为NaN等于NaN，空对象不等于空对象。
Set的属性和方法
Set 结构的实例有以下属性。
Set.prototype.constructor：构造函数，默认就是Set函数。
Set.prototype.size：返回Set实例的成员总数。
Set 实例的方法分为两大类：操作方法（用于操作数据）和遍历方法（用于遍历成员）。下面先介绍四个操作方法。
add(value)：添加某个值，返回Set结构本身。
delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
has(value)：返回一个布尔值，表示该值是否为Set的成员。
clear()：清除所有成员，没有返回值。
Set 结构的实例有四个遍历方法，可以用于遍历成员。
keys()：返回键名的遍历器
values()：返回键值的遍历器
entries()：返回键值对的遍历器
forEach()：使用回调函数遍历每个成员
需要特别指出的是，Set的遍历顺序就是插入顺序。这个特性有时非常有用，比如使用Set保存一个回调函数列表，调用时就能保证按照添加顺序调用。
2、WeakSet
WeakSet 结构与 Set 类似，也是不重复的值的集合。但是，它与 Set 有两个区别。
首先，WeakSet 的成员只能是对象，而不能是其他类型的值。
其次，WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用，也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 WeakSet 之中。

上面代码中，a是一个数组，它有两个成员，也都是数组。将a作为 WeakSet 构造函数的参数，a的成员会自动成为 WeakSet 的成员。

上面代码中，数组b的成员不是对象，加入 WeaKSet 就会报错。
WeakSet 结构有以下三个方法。

WeakSet.prototype.add(value)：向 WeakSet 实例添加一个新成员。
WeakSet.prototype.delete(value)：清除 WeakSet 实例的指定成员。
WeakSet.prototype.has(value)：返回一个布尔值，表示某个值是否在 WeakSet 实例之中。
WeakSet 不能遍历，是因为成员都是弱引用，随时可能消失，遍历机制无法保证成员的存在，很可能刚刚遍历结束，成员就取不到了。WeakSet 的一个用处，是储存 DOM 节点，而不用担心这些节点从文档移除时，会引发内存泄漏。
3、Map
ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。
注意，只有对同一个对象的引用，Map 结构才将其视为同一个键。这一点要非常小心。 Map 的键实际上是跟内存地址绑定的，只要内存地址不一样，就视为两个键。
实例的属性和操作方法
size属性
set(key,value)
get(key)
has(key)
delete(key)
clear()
遍历方法
keys()：返回键名的遍历器。
values()：返回键值的遍历器。
entries()：返回所有成员的遍历器。
forEach()：遍历 Map 的所有成员。
与JSON、数组、对象间的相互转化
4、WeakMap
WeakMap结构与Map结构类似，也是用于生成键值对的集合。
WeakMap与Map的区别有两点。 首先，WeakMap只接受对象作为键名（null除外），不接受其他类型的值作为键名。 其次，WeakMap的键名所指向的对象，不计入垃圾回收机制。 注意，WeakMap 弱引用的只是键名，而不是键值。键值依然是正常引用， 即使在 WeakMap 外部消除了键值的引用，WeakMap 内部的引用依然存在。
实例的属性和方法： WeakMap只有四个方法可用：get()、set()、has()、delete()。











十二、Proxy（为操作对象提供的新API）
1、概述
Proxy 用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种“元编程”（meta programming），即对编程语言进行编程。
Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。Proxy 这个词的原意是代理，用在这里表示由它来“代理”某些操作，可以译为“代理器”。
对于可以设置、但没有设置拦截的操作，则直接落在目标对象上，按照原先的方式产生结果。
（1）get(target, propKey, receiver)
拦截对象属性的读取，比如proxy.foo和proxy['foo']。
最后一个参数receiver是一个对象，可选，参见下面Reflect.get的部分。
（2）set(target, propKey, value, receiver)
拦截对象属性的设置，比如proxy.foo = v或proxy['foo'] = v，返回一个布尔值。
（3）has(target, propKey)
拦截propKey in proxy的操作，返回一个布尔值。
（4）deleteProperty(target, propKey)
拦截delete proxy[propKey]的操作，返回一个布尔值。
（5）ownKeys(target)
拦截Object.getOwnPropertyNames(proxy)、Object.getOwnPropertySymbols(proxy)、Object.keys(proxy)，返回一个数组。该方法返回目标对所有自身的属性的属性名，而Object.keys()的返回结果仅包括目标对象自身的可遍历属性。
（6）getOwnPropertyDescriptor(target, propKey)
拦截Object.getOwnPropertyDescriptor(proxy, propKey)，返回属性的描述对象。
（7）defineProperty(target, propKey, propDesc)
拦截Object.defineProperty(proxy, propKey, propDesc）、Object.defineProperties(proxy, propDescs)，返回一个布尔值。
（8）preventExtensions(target)
拦截Object.preventExtensions(proxy)，返回一个布尔值。
（9）getPrototypeOf(target)
拦截Object.getPrototypeOf(proxy)，返回一个对象。
（10）isExtensible(target)
拦截Object.isExtensible(proxy)，返回一个布尔值。
（11）setPrototypeOf(target, proto)
拦截Object.setPrototypeOf(proxy, proto)，返回一个布尔值。
如果目标对象是函数，那么还有两种额外操作可以拦截。
（12）apply(target, object, args)
拦截 Proxy 实例作为函数调用的操作，比如proxy(...args)、proxy.call(object, ...args)、proxy.apply(...)。
（13）construct(target, args)
拦截 Proxy 实例作为构造函数调用的操作，比如new proxy(...args)。
2、Proxy实例的方法
3、Proxy.revocable
Proxy.revocable方法返回一个可取消的 Proxy 实例。
4、this问题
目标对象内部的this关键字会指向 Proxy 代理。
5、实例：Web服务的客户端









十三、Reflect（为操作对象提供的新API ）
1、概述
Reflect对象的设计目的有这样几个。
（1） 将Object对象的一些明显属于语言内部的方法（比如Object.defineProperty），放到Reflect对象上。现阶段，某些方法同时在Object和Reflect对象上部署，未来的新方法将只部署在Reflect对象上。也就是说，从Reflect对象上可以拿到语言内部的方法。
（2） 修改某些Object方法的返回结果，让其变得更合理。比如，Object.defineProperty(obj, name, desc)在无法定义属性时，会抛出一个错误，而Reflect.defineProperty(obj, name, desc)则会返回false。
（3） 让Object操作都变成函数行为。某些Object操作是命令式，比如name in obj和delete obj[name]，而Reflect.has(obj, name)和Reflect.deleteProperty(obj, name)让它们变成了函数行为。
（4）Reflect对象的方法与Proxy对象的方法一一对应，只要是Proxy对象的方法，就能在Reflect对象上找到对应的方法。这就让Proxy对象可以方便地调用对应的Reflect方法，完成默认行为，作为修改行为的基础。也就是说，不管Proxy怎么修改默认行为，你总可以在Reflect上获取默认行为。
2、静态方法
Reflect对象一共有13个静态方法。
Reflect.apply(target,thisArg,args)
Reflect.construct(target,args)
Reflect.get(target,name,receiver)
Reflect.set(target,name,value,receiver)
Reflect.defineProperty(target,name,desc)
Reflect.deleteProperty(target,name)
Reflect.has(target,name)
Reflect.ownKeys(target)
Reflect.isExtensible(target)
Reflect.preventExtensions(target)
Reflect.getOwnPropertyDescriptor(target, name)
Reflect.getPrototypeOf(target)
Reflect.setPrototypeOf(target, prototype)
上面这些方法的作用，大部分与Object对象的同名方法的作用都是相同的，而且它与Proxy对象的方法是一一对应的。
3、实例：使用Proxy实现观察者模式
观察者模式（Observer mode）指的是函数自动观察数据对象，一旦对象有变化，函数就会自动执行。










十四、Promise 对象
1、Promise的含义
Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。 所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。
Promise对象有以下两个特点。
（1）对象的状态不受外界影响。Promise对象代表一个异步操作，有三种状态：Pending（进行中）、Resolved（已完成，又称 Fulfilled）和Rejected（已失败）。
（2）一旦状态改变，就不会再变，任何时候都可以得到这个结果。 这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。
有了Promise对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，Promise对象提供统一的接口，使得控制异步操作更加容易。
Promise也有一些缺点。首先，无法取消Promise，一旦新建它就会立即执行，无法中途取消。其次，如果不设置回调函数，Promise内部抛出的错误，不会反应到外部。第三，当处于Pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。
如果某些事件不断地反复发生，一般来说，使用 Stream 模式是比部署Promise更好的选择。
2、基本用法
Promise 新建后就会立即执行。

上面代码中，Promise 新建后立即执行，所以首先输出的是Promise。然后，then方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行，所以Resolved最后输出。
异步加载图片

Ajax 操作

3、Promise.prototype.then()
它的作用是为 Promise 实例添加状态改变时的回调函数。前面说过，then方法的第一个参数是Resolved状态的回调函数，第二个参数（可选）是Rejected状态的回调函数。 then方法返回的是一个新的Promise实例（注意，不是原来那个Promise实例）。因此可以采用链式写法，即then方法后面再调用另一个then方法。
4、Promise.prototype.catch()
Promise.prototype.catch方法是.then(null, rejection)的别名，用于指定发生错误时的回调函数。 如果Promise状态已经变成Resolved，再抛出错误是无效的。 一般来说，不要在then方法里面定义Reject状态的回调函数（即then的第二个参数），总是使用catch方法。
5、Promise.all()
Promise.all方法用于将多个 Promise 实例，包装成一个新的 Promise 实例。
6、Promise.race()
Promise.race方法同样是将多个Promise实例，包装成一个新的Promise实例。
7、Promise.resolve()
有时需要将现有对象转为Promise对象，Promise.resolve方法就起到这个作用。
8、Promise.reject()
Promise.reject(reason)方法也会返回一个新的 Promise 实例，该实例的状态为rejected。
9、两个有用的附加方法
done()
Promise对象的回调链，不管以then方法或catch方法结尾，要是最后一个方法抛出错误，都有可能无法捕捉到（因为Promise内部的错误不会冒泡到全局）。因此，我
们可以提供一个done方法，总是处于回调链的尾端，保证抛出任何可能出现的错误。
finally()
finally方法用于指定不管Promise对象最后状态如何，都会执行的操作。它与done方法的最大区别，它接受一个普通的回调函数作为参数，该函数不管怎样都必须执行。
10、应用
加载图片、Generator函数与Promise的结合
11、Promise.try()（提案）
Promise.try就是模拟try代码块，就像promise.catch模拟的是catch代码块。










十五、Iterator 和 for...of 循环
1、Iterator（遍历器）的概念
遍历器（Iterator）就是这样一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署Iterator接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。
Iterator 的作用有三个：一是为各种数据结构，提供一个统一的、简便的访问接口；二是使得数据结构的成员能够按某种次序排列；三是ES6创造了一种新的遍历命令for...of循环，Iterator接口主要供for...of消费。
2、默认Iterator接口
ES6 规定，默认的 Iterator 接口部署在数据结构的Symbol.iterator属性，或者说，一个数据结构只要具有Symbol.iterator属性，就可以认为是“可遍历的”（iterable）。
原生具备 Iterator 接口的数据结构如下。
Array
Map
Set
String
TypedArray
函数的 arguments 对象
对象（Object）之所以没有默认部署 Iterator 接口，是因为对象的哪个属性先遍历，哪个属性后遍历是不确定的，需要开发者手动指定。本质上，遍历器是一种线性处理，对于任何非线性的数据结构，部署遍历器接口，就等于部署一种线性转换。不过，严格地说，对象部署遍历器接口并不是很必要，因为这时对象实际上被当作Map结构使用，ES5 没有 Map 结构，而 ES6 原生提供了。
3、调用Iterator接口的场合
解构赋值
扩展运算符（只要某个数据结构部署了 Iterator 接口，就可以对它使用扩展运算符，将其转为数组。）、
yield*（ yield*后面跟的是一个可遍历的结构，它会调用该结构的遍历器接口。）
4、字符串的Iterator接口
字符串是一个类似数组的对象，也原生具有 Iterator 接口。
5、Iterator接口和Generator函数
6、遍历器对象的return()，throw()
return方法的使用场合是，如果for...of循环提前退出（通常是因为出错，或者有break语句或continue语句），就会调用return方法。如果一个对象在完成遍历前，需要清理或释放资源，就可以部署return方法。
throw方法主要是配合Generator函数使用，一般的遍历器对象用不到这个方法。
7、for...of循环
数组(for...of循环可以代替数组实例的forEach方法。 JavaScript 原有的for...in循环，只能获得对象的键名，不能直接获取键值。ES6 提供for...of循环，允许遍历获得键值。)
Set和Map结构
类似数组的对象(for...of循环用于字符串、DOM NodeList 对象、arguments对象等, 并不是所有类似数组的对象都具有 Iterator 接口，一个简便的解决方法，就是使用Array.from方法将其转为数组。)
对象( 对于普通的对象，for...in循环可以遍历键名，for...of循环会报错。 一种解决方法是，使用Object.keys方法将对象的键名生成一个数组，然后遍历这个数组。 另一个方法是使用 Generator 函数将对象重新包装一下。)











十六、Generator 函数的语法
1、简介
基本概念 Generator 函数是 ES6 提供的一种异步编程解决方案，语法行为与传统函数完全不同。 执行 Generator 函数会返回一个遍历器对象，也就是说，Generator 函数除了状态机，还是一个遍历器对象生成函数。返回的遍历器对象，可以依次遍历 Generator 函数内部的每一个状态。 形式上，Generator 函数是一个普通函数，但是有两个特征。一是，function关键字与函数名之间有一个星号；二是，函数体内部使用yield表达式，定义不同的内部状态（yield在英语里的意思就是“产出”）。 Generator 函数的调用方法与普通函数一样，也是在函数名后面加上一对圆括号。不同的是，调用 Generator 函数后，该函数并不执行，返回的也不是函数运行结果，而是一个指向内部状态的指针对象，也就是上一章介绍的遍历器对象（Iterator Object）。
yield表达式 由于 Generator 函数返回的遍历器对象，只有调用next方法才会遍历下一个内部状态，所以其实提供了一种可以暂停执行的函数。yield表达式就是暂停标志。Generator 函数可以不用yield表达式，这时就变成了一个单纯的暂缓执行函数。 另外需要注意，yield表达式只能用在 Generator 函数里面，用在其他地方都会报错。
与Iterator关系 由于 Generator 函数就是遍历器生成函数，因此可以把 Generator 赋值给对象的Symbol.iterator属性，从而使得该对象具有 Iterator 接口。
2、next方法的参数
yield表达式本身没有返回值，或者说总是返回undefined。next方法可以带一个参数，该参数就会被当作上一个yield表达式的返回值。

注意，由于next方法的参数表示上一个yield表达式的返回值，所以第一次使用next方法时，不能带有参数。V8 引擎直接忽略第一次使用next方法时的参数，只有从第二次使用next方法开始，参数才是有效的。从语义上讲，第一个next方法用来启动遍历器对象，所以不用带有参数。
3、for...of循环
for...of循环可以自动遍历 Generator 函数时生成的Iterator对象，且此时不再需要调用next方法。
利用for...of循环，可以写出遍历任意对象（object）的方法。原生的 JavaScript 对象没有遍历接口，无法使用for...of循环，通过 Generator 函数为它加上这个接口，就可以用了。

4、Generator.prototype.throw()
Generator 函数返回的遍历器对象，都有一个throw方法，可以在函数体外抛出错误，然后在 Generator 函数体内捕获。

上面代码中，遍历器对象i连续抛出两个错误。第一个错误被 Generator 函数体内的catch语句捕获。i第二次抛出错误，由于 Generator 函数内部的catch语句已经执行过了，不会再捕捉到这个错误了，所以这个错误就被抛出了 Generator 函数体，被函数体外的catch语句捕获。
5、Generator.prototype.return()
Generator函数返回的遍历器对象，还有一个return方法，可以返回给定的值，并且终结遍历Generator函数。

如果 Generator 函数内部有try...finally代码块，那么return方法会推迟到finally代码块执行完再执行。
6、yield*表达式
如果在 Generator 函数内部，调用另一个 Generator 函数，默认情况下是没有效果的。 这个就需要用到yield*表达式，用来在一个 Generator 函数里面执行另一个 Generator 函数。 任何数据结构只要有 Iterator 接口，就可以被yield*遍历。
yield*命令可以很方便地取出嵌套数组的所有成员。 使用yield*语句遍历完全二叉树。

7、作为对象属性的Generator函数
如果一个对象的属性是 Generator 函数， 属性前面有一个星号，表示这个属性是一个 Generator 函数。
8、Generator函数的this
Generator 函数g返回的遍历器obj，是g的实例，而且继承了g.prototype。但是，如果把g当作普通的构造函数，并不会生效，因为g返回的总是遍历器对象，而不是this对象。 Generator函数也不能跟new命令一起用，会报错。

解决方法： 第一种方法：生成一个空对象，使用call方法绑定 Generator 函数内部的this
第二种方法： var f = F.call(F.prototype);
9、含义
Generator 是实现状态机的最佳结构
Generator与协程
10、应用
Generator 可以暂停函数执行，返回任意表达式的值。这种特点使得 Generator 有多种应用场景。
异步操作的同步化表达、控制流管理、部署Iterator接口、作为数据结构













十七、Generator 函数的异步应用
1、传统方法
ES6 诞生以前，异步编程的方法，大概有下面四种。
回调函数
事件监听
发布/订阅
Promise 对象
Generator 函数将 JavaScript 异步编程带入了一个全新的阶段。
2、基本概念
异步、回调函数、Promise
3、Generator函数
协程： 多个线程互相协作，完成异步任务。
协程的Generator函数实现： Generator 函数是协程在 ES6 的实现，最大特点就是可以交出函数的执行权（即暂停执行）。
Generator函数的数据交换和错误处理： Generator 函数可以暂停执行和恢复执行，这是它能封装异步任务的根本原因。除此之外，它还有两个特性，使它可以作为异步编程的完整解决方案：函数体内外的数据交换和错误处理机制。
异步任务的封装
4、Thunk函数
Thunk 函数是自动执行 Generator 函数的一种方法。
参数的求值策略： 传值调用和传名调用
Thunk函数的含义： 编译器的“传名调用”实现，往往是将参数放到一个临时函数之中，再将这个临时函数传入函数体。这个临时函数就叫做 Thunk 函数。
JavaScript语言的Thunk函数： 在 JavaScript 语言中，Thunk 函数替换的不是表达式，而是多参数函数，将其替换成一个只接受回调函数作为参数的单参数函数。
Thunkify模块： 生产环境的转换器，建议使用 Thunkify 模块。
Generator函数的流程管理
Thunk函数的自动流程管理： Thunk 函数真正的威力，在于可以自动执行 Generator 函数。
5、co模块
用于 Generator 函数的自动执行， co函数返回一个Promise对象，因此可以用then方法添加回调函数。
co函数的原理： co 模块其实就是将两种自动执行器（Thunk 函数和 Promise 对象），包装成一个模块。使用 co 的前提条件是，Generator 函数的yield命令后面，只能是 Thunk 函数或 Promise 对象。如果数组或对象的成员，全部都是 Promise 对象。
基于Promise对象的自动执行
co模块的源码： co 函数接受 Generator 函数作为参数，返回一个 Promise 对象。
处理并发的异步操作















十八、async 函数
1、含义
ES2017 标准引入了 async 函数，使得异步操作变得更加方便，是 Generator 函数的语法糖。
async函数对 Generator 函数的改进，体现在以下四点。 （1）内置执行器。 （2）更好的语义。 （3）更广的适用性。 （4）返回值是 Promise。
2、用法
3、语法
async函数的语法规则总体上比较简单，难点是错误处理机制。
4、async函数的实现原理
5、与其他异步处理方法的比较
6、按顺序完成异步操作
7、异步遍历器






十九、Class 的基本语法
1、简介
2、严格模式
类和模块的内部，默认就是严格模式，所以不需要使用use strict指定运行模式。只要你的代码写在类或模块之中，就只有严格模式可用。
考虑到未来所有的代码，其实都是运行在模块之中，所以 ES6 实际上把整个语言升级到了严格模式。
3、constructor方法
constructor方法是类的默认方法，通过new命令生成对象实例时，自动调用该方法。
constructor方法默认返回实例对象（即this），完全可以指定返回另外一个对象。

上面代码中，constructor函数返回一个全新的对象，结果导致实例对象不是Foo类的实例。
类必须使用new调用，否则会报错。这是它跟普通构造函数的一个主要区别，后者不用new也可以执行。
4、类的实例对象
5、Class表达式
6、不存在变量提升
7、私有方法
8、私有属性
9、this的指向
10、name属性
11、Class的取值函数（getter）和存值函数（setter）
存值函数和取值函数是设置在属性的 Descriptor 对象上的。
12、Class的Generator方法
13、Class的静态方法
类相当于实例的原型，所有在类中定义的方法，都会被实例继承。如果在一个方法前，加上static关键字，就表示该方法不会被实例继承，而是直接通过类来调用，这就称为“静态方法”。
父类的静态方法，可以被子类继承。
14、Class的静态属性和实例属性
静态属性指的是 Class 本身的属性，即Class.propName，而不是定义在实例对象（this）上的属性。 目前，只有这种写法可行，因为 ES6 明确规定，Class 内部只有静态方法，没有静态属性。
15、new.target属性
ES6 为new命令引入了一个new.target属性，该属性一般用在在构造函数之中，返回new命令作用于的那个构造函数。如果构造函数不是通过new命令调用的，new.target会返回undefined，因此这个属性可以用来确定构造函数是怎么调用的。
需要注意的是，子类继承父类时，new.target会返回子类。 利用这个特点，可以写出不能独立使用、必须继承后才能使用的类。












二十、Class 的继承
1、简介
子类必须在constructor方法中调用super方法，否则新建实例时会报错。这是因为子类没有自己的this对象，而是继承父类的this对象，然后对其进行加工。如果不调用super方法，子类就得不到this对象。
ES5 的继承，实质是先创造子类的实例对象this，然后再将父类的方法添加到this上面（Parent.apply(this)）。ES6 的继承机制完全不同，实质是先创造父类的实例对象this（所以必须先调用super方法），然后再用子类的构造函数修改this。
另一个需要注意的地方是，在子类的构造函数中，只有调用super之后，才可以使用this关键字，否则会报错。这是因为子类实例的构建，是基于对父类实例加工，只有super方法才能返回父类实例。

2、Object.getPrototypeOf()
Object.getPrototypeOf方法可以用来从子类上获取父类。可以使用这个方法判断，一个类是否继承了另一个类。
3、super关键字
第一种情况，super作为函数调用时，代表父类的构造函数。 注意，super虽然代表了父类A的构造函数，但是返回的是子类B的实例，即super内部的this指的是B，因此super()在这里相当于A.prototype.constructor.call(this)。 super()只能用在子类的构造函数之中，用在其他地方就会报错。
第二种情况，super作为对象时，在普通方法中，指向父类的原型对象； 由于super指向父类的原型对象，所以定义在父类实例上的方法或属性，是无法通过super调用的。 ES6 规定，通过super调用父类的方法时，super会绑定子类的this。 由于绑定子类的this，所以如果通过super对某个属性赋值，这时super就是this，赋值的属性会变成子类实例的属性。

用在静态方法之中，这时super将指向父类，而不是父类的原型对象。
4、类的prototype属性和__proto__属性
大多数浏览器的 ES5 实现之中，每一个对象都有__proto__属性，指向对应的构造函数的prototype属性。
（1）子类的__proto__属性，表示构造函数的继承，总是指向父类。
（2）子类prototype属性的__proto__属性，表示方法的继承，总是指向父类的prototype属性。
5、原生构造函数的继承
ECMAScript 的原生构造函数大致有下面这些。
Boolean()
Number()
String()
Array()
Date()
Function()
RegExp()
Error()
Object()
以前，这些原生构造函数是无法继承的，比如，不能自己定义一个Array的子类。 原生构造函数会忽略apply方法传入的this，也就是说，原生构造函数的this无法绑定，导致拿不到内部属性。
注意，继承Object的子类，有一个行为差异。

上面代码中，NewObj继承了Object，但是无法通过super方法向父类Object传参。这是因为 ES6 改变了Object构造函数的行为，一旦发现Object方法不是通过new Object()这种形式调用，ES6 规定Object构造函数会忽略参数。
6、Mixin模式的实现
Mixin 模式指的是，将多个类的接口“混入”（mix in）另一个类。










二十一、Decorator修饰器
1、类的装饰
修饰器（Decorator）是一个函数，用来修改类的行为。ES2017 引入了这项功能，目前 Babel 转码器已经支持。

注意，修饰器对类的行为的改变，是代码编译时发生的，而不是在运行时。这意味着，修饰器能在编译阶段运行代码。也就是说，修饰器本质就是编译时执行的函数。
前面的例子是为类添加一个静态属性，如果想添加实例属性，可以通过目标类的prototype对象操作。

上面代码通过修饰器mixins，把Foo类的方法添加到了MyClass的实例上面，传参。
2、方法的装饰
修饰器函数一共可以接受三个参数，第一个参数是所要修饰的目标对象，第二个参数是所要修饰的属性名，第三个参数是该属性的描述对象。

修改属性描述对象的enumerable属性，使得该属性不可遍历。
如果同一个方法有多个修饰器，会像剥洋葱一样，先从外到内进入，然后由内向外执行。

上面代码中，外层修饰器@dec(1)先进入，但是内层修饰器@dec(2)先执行。
3、为什么装饰器不能用于函数？
修饰器只能用于类和类的方法，不能用于函数，因为存在函数提升。
4、core-decorators.js
core-decorators.js是一个第三方模块，提供了几个常见的修饰器，通过它可以更好地理解修饰器。
（1）@autobind：autobind修饰器使得方法中的this对象，绑定原始对象。
（2）@readonly： readonly修饰器使得属性或方法不可写。
（3）@override： override修饰器检查子类的方法，是否正确覆盖了父类的同名方法，如果不正确会报错。
（4）@deprecate (别名@deprecated)： deprecate或deprecated修饰器在控制台显示一条警告，表示该方法将废除。
（5）@suppressWarnings： suppressWarnings修饰器抑制decorated修饰器导致的console.warn()调用。但是，异步代码发出的调用除外。
5、使用装饰器实现自动发布事件
6、Mixin
在修饰器的基础上，可以实现Mixin模式。所谓Mixin模式，就是对象继承的一种替代方案，中文译为“混入”（mix in），意为在一个对象之中混入另外一个对象的方法。
7、Trait
Trait也是一种修饰器，效果与Mixin类似，但是提供更多功能，比如防止同名方法的冲突、排除混入某些方法、为混入的方法起别名等等。
8、Babel转码器的支持










二十二、Module 的语法
1、概述
在 ES6 之前，社区制定了一些模块加载方案，最主要的有 CommonJS 和 AMD 两种。前者用于服务器，后者用于浏览器。
ES6 模块的设计思想，是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。

上面代码的实质是从fs模块加载3个方法，其他方法不加载。这种加载称为“编译时加载”或者静态加载，即 ES6 可以在编译时就完成模块加载，效率要比 CommonJS 模块的加载方式高。commonJs 实质是整体加载模块（即加载模块的所有方法），生成一个对象，然后再从这个对象上面读取方法。
2、严格模式
ES6 模块之中，顶层的this指向undefined，即不应该在顶层代码使用this。
3、export命令
模块功能主要由两个命令构成：export和import。export命令用于规定模块的对外接口，import命令用于输入其他模块提供的功能。
通常情况下，export输出的变量就是本来的名字，但是可以使用as关键字重命名。
export语句输出的接口，与其对应的值是动态绑定关系，即通过该接口，可以取到模块内部实时的值， 这一点与 CommonJS 规范完全不同。CommonJS 模块输出是值的缓存，不存在动态更新。
export命令可以出现在模块的任何位置，只要处于模块顶层就可以，如果处于块级作用域内，就会报错。
4、import命令
注意，import命令具有提升效果，会提升到整个模块的头部，首先执行。
由于import是静态执行，所以不能使用表达式和变量，这些只有在运行时才能得到结果的语法结构。
5、模块的整体加载
除了指定加载某个输出值，还可以使用整体加载，即用星号（*）指定一个对象，所有输出值都加载在这个对象上面。
6、export default命令
为模块指定默认输出。

export default命令用于指定模块的默认输出。显然，一个模块只能有一个默认输出，因此export default命令只能使用一次。所以，import命令后面才不用加大括号，因为只可能对应一个方法。
正是因为export default命令其实只是输出一个叫做default的变量，所以它后面不能跟变量声明语句。
export default也可以用来输出类。
7、export与import的复合写法
8、模块的继承
9、跨模块常量
本书介绍const命令的时候说过，const声明的常量只在当前代码块有效。
10、import()（提案）
import命令会被 JavaScript 引擎静态分析，先于模块内的其他模块执行（叫做”连接“更合适） ，import和export命令只能在模块的顶层，不能在代码块之中（比如，在if代码块之中，或在函数之中）。 这样的设计，固然有利于编译器提高效率，但也导致无法在运行时加载模块。
建议引入import()函数，完成动态加载。 import()返回一个 Promise 对象。 import()类似于 Node 的require方法，区别主要是前者是异步加载，后者是同步加载。
适用场合
（1）按需加载。
（2）条件加载。
（3）动态的模块路径。







二十三、Module 的加载实现
1、浏览器加载
默认情况下，浏览器是同步加载 JavaScript 脚本，即渲染引擎遇到<script>标签就会停下来，等到执行完脚本，再继续向下渲染。如果是外部脚本，还必须加入脚本下载的时间。 <script>标签打开defer或async属性，脚本就会异步加载。
defer与async的区别是：前者要等到整个页面正常渲染结束，才会执行；后者一旦下载完，渲染引擎就会中断渲染，执行这个脚本以后，再继续渲染。一句话，defer是“渲染完再执行”，async是“下载完就执行”。另外，如果有多个defer脚本，会按照它们在页面出现的顺序加载，而多个async脚本是不能保证加载顺序的。
加载规则： 浏览器加载 ES6 模块，也使用<script>标签，但是要加入type="module"属性， 等同于打开了<script>标签的defer属性。
利用顶层的this等于undefined这个语法点，可以侦测当前代码是否在 ES6 模块之中。
2、ES6模块与CommonJs模块的差异
两个重大差异
CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。
CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。
由于 ES6 输入的模块变量，只是一个“符号连接”，所以这个变量是只读的，对它进行重新赋值会报错。 最后，export通过接口，输出的是同一个值。不同的脚本加载这个接口，得到的都是同样的实例。
第二个差异是因为 CommonJS 加载的是一个对象（即module.exports属性），该对象只有在脚本运行完才会生成。而 ES6 模块不是对象，它的对外接口只是一种静态定义，在代码静态解析阶段就会生成。
3、Node加载
Node 对 ES6 模块的处理比较麻烦，因为它有自己的 CommonJS 模块格式，与 ES6 模块格式是不兼容的。目前的解决方案是，将两者分开，ES6 模块和 CommonJS 采用各自的加载方案。在静态分析阶段，一个模块脚本只要有一行import或export语句，Node 就会认为该脚本为 ES6 模块，否则就为 CommonJS 模块。如果不输出任何接口，但是希望被 Node 认为是 ES6 模块，可以在脚本中加一行语句export {};
ES6 模块之中，顶层的this指向undefined；CommonJS 模块的顶层this指向当前模块，这是两者的一个重大差异。
import命令加载CommonJs模块： 默认输出、 整体输入
require命令加载ES6模块： 采用require命令加载 ES6 模块时，ES6 模块的所有输出接口，会成为输入对象的属性。
4、循环加载
“循环加载”（circular dependency）指的是，a脚本的执行依赖b脚本，而b脚本的执行又依赖a脚本。
CommonJs模块的加载原理： CommonJS模块无论加载多少次，都只会在第一次加载时运行一次，以后再加载，就返回第一次运行的结果，除非手动清除系统缓存。
CommonJs模块的循环加载：由于CommonJS模块遇到循环加载时，返回的是当前已经执行的部分的值，而不是代码全部执行后的值，两者可能会有差异。所以，输入变量的时候，必须非常小心。
ES6模块的循环加载
5、ES6模块的转码
ES6 module transpiler是 square 公司开源的一个转码器，可以将 ES6 模块转为 CommonJS 模块或 AMD 模块的写法，从而在浏览器中使用。
另一种解决方法是使用 SystemJS。它是一个垫片库（polyfill），可以在浏览器内加载 ES6 模块、AMD 模块和 CommonJS 模块，将其转为 ES5 格式。它在后台调用的是 Google 的 Traceur 转码器。







二十四、编程风格
1、块级作用域
（1）let 取代 var：ES6提出了两个新的声明变量的命令：let和const。
（2）全局常量和线程安全： 在let和const之间，建议优先使用const，尤其是在全局环境，不应该设置变量，只应设置常量。
let和const的本质区别，其实是编译器内部的处理不同。
2、字符串
静态字符串一律使用单引号或反引号，不使用双引号。动态字符串使用反引号。
3、解构赋值
使用数组成员对变量赋值时，优先使用解构赋值。
函数的参数如果是对象的成员，优先使用解构赋值。
如果函数返回多个值，优先使用对象的解构赋值，而不是数组的解构赋值。这样便于以后添加返回值，以及更改返回值的顺序。
4、对象
单行定义的对象，最后一个成员不以逗号结尾。多行定义的对象，最后一个成员以逗号结尾。
对象尽量静态化，一旦定义，就不得随意添加新的属性。如果添加属性不可避免，要使用Object.assign方法。
如果对象的属性名是动态的，可以在创造对象的时候，使用属性表达式定义。
对象的属性和方法，尽量采用简洁表达法，这样易于描述和书写。
5、数组
使用扩展运算符（...）拷贝数组。
使用Array.from方法，将类似数组的对象转为数组。
6、函数
立即执行函数可以写成箭头函数的形式。
那些需要使用函数表达式的场合，尽量用箭头函数代替。因为这样更简洁，而且绑定了this。 箭头函数取代Function.prototype.bind，不应再用self/_this/that绑定 this。
不要在函数体内使用arguments变量，使用rest运算符（...）代替。
使用默认值语法设置函数参数的默认值。
7、Map结构
注意区分Object和Map，只有模拟现实世界的实体对象时，才使用Object。如果只是需要key: value的数据结构，使用Map结构。因为Map有内建的遍历机制。
8、Class
总是用Class，取代需要prototype的操作。因为Class的写法更简洁，更易于理解。
使用extends实现继承，因为这样更简单，不会有破坏instanceof运算的危险。
9、模块
首先，Module语法是JavaScript模块的标准写法，坚持使用这种写法。使用import取代require。
使用export取代module.exports。
如果模块只有一个输出值，就使用export default，如果模块有多个输出值，就不使用export default，export default与普通的export不要同时使用。
不要在模块输入中使用通配符。因为这样可以确保你的模块之中，有一个默认输出（export default）。
如果模块默认输出一个函数，函数名的首字母应该小写。
如果模块默认输出一个对象，对象名的首字母应该大写。
10、ESLint的使用
ESLint是一个语法规则和代码风格的检查工具，可以用来保证写出语法正确、风格统一的代码。









二十五、读懂 ECMAScript 规格
1、概述
2、相等运算符
3、数组的空位
4、数组的map方法








