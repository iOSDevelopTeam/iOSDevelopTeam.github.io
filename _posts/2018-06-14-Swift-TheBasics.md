---
layout:     post
title:      Swift4.1翻译
subtitle:   第二章 The Basics
date:       2018-06-14
author:     shavekevin
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - iOS
    - 翻译
    - Swift
---
# Swift语言开发指南
## 基础部分
Swift是一门新的开发语言，它可以在iOS、macOS watchOS以及tvOS系统环境下进行应用的开发。

Swift提供了它自己的`C`和`Objective-C`语言的所有基本数据类型。包括用于描述整数的Int，描述浮点型的`Double`和`Float`，描述布尔值的`Bool`以及描述文本数据的`String`。Swift也提供了三个主要的集合类型。比如集合类型中描述的的数组、集合、和字典。

和C语言一样，Swift用变量来存储和引用一个已经被声明过名字的值。Swift同样能够使用不可变数据类型的值。这些不能改变的值被称为常量，它比C语言中的常量更加强大。当你在使用不可变的值的时候，常量能够使你的代码变得安全整洁。

除了一些熟悉的类型之外，Swift还提供了`Objective-C`没有的高级类型，比如说：元组。元组能够让你创创建和传递一组数据。函数中返回多个值的时候你可以用元组作为单个复合值来接收。

Swift也提供了一些可选类型，它能够处理值缺失的情况。可选值的意思是说：这里有一个值，它等于`X`或者`它没有值`。使用可选类型的之后就像使用`Objective-C`中的空指针一样，但是它的使用不仅仅局限于类，可以是任意类型。和`Objective-C`中的空指针相比来说，可选类型可不仅仅是安全和更具表现力那么简单，它们是Swift最强大功能中的核心。

Swift是一门安全类型的语言。这意味着这门语言可以帮你弄明白你所使用的值是什么类型的。如果你的代码中需要的是`String`,当你用`Int`来给它赋值的时候，类型安全会阻止你这么做。同样的，如果你意外的将可选字符串传递给非可选字符串那么类型安全会阻止你这么做。类型安全可以帮你在开发过程中尽早的捕获和修正错误。

###  常量和变量

常量和变量都需要用一个别名(比如说`maximumNumberOfLoginAttempts`或者`welcomeMessage`)以及一个特殊的数据类型的值(比如说数字`10`和字符串`hello`)来来进行关联.常量的值一旦被初始化设置了之后就不能发生改变了，而变量则可以在未来给它赋不同的值。
### 常量和变量的声明
常量和变量在使用之前都是要经过声明的。你可以用关键词`let`来修饰一个常量，用`var`关键词来修饰一个变量。下面的例子是通过对常量和变量的使用来模拟一个用户尝试登录次数的场景。
```
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempts  = 0
```
这段代码可以被解读为：
声明一个新的名字为`maximumNumberOfLoginAttempts`的常量，它的值为10。然后声明一个新的名为`currentLoginAttempts`的变量，它的初始值为0.
在这个例子中，最大允许尝试登录次数被声明为一个常量，因为最大的尝试登录次数不能被修改。当前的尝试登录次数被声明为一个变量，因为这个次值会随着尝试登录失败的次数的增加而增加。
你可以连续声明几个常量或者变量在同一行中，他们之间用逗号隔开。
```
var x = 0.0,y = 0.0,z = 0.0
```
注意：
如果你的代码中使用的值是不会发生改变的那么用`let`关键字来声明。如果声明的值是需要发生改变的那么用`var`关键字来声明。
### 类型标注
在声明常量和变量的时候你可以为它提供一个类型标注，它可以很清楚的告诉编辑器常量和变量以什么样的数据类型被存储。在常量和变量添加类型标注的时候在命名之后加一个冒号以以及空格，然后加上类型的名称。

下面的这个例子里给出一个叫做`welcomeMessage`变量的类型标注，它表明了这个变量被存储为一个`String`类型的值。
```
var welcomeMessage: String
```
在声明的时候冒号的意思是“...类型的”，因此上面的代码可以这样来理解：

声明一个类型为`String`的变量`welcomeMessage`。

类型字符串的意思是可以存储任意值的字符串，可以把它理解为有存储功能的"事物类型"。

变量`welcomeMessage`可以被赋值为任意的字符串而不报错。
```
welcomeMessage = "Hello"
```
你可以在一行定义多个同一种类型的变量，用逗号隔开在最后一个变量后面添加冒号和类型标注。
```
var red,green,blue:Double
```
注意：
在实际开发中我们很少需要给常量/变量来写类型标注，如果在定义常量/变量的时候给了一个初始值，那么Swift可以帮我们推断出常量/变量的类型。具体请参考`类型和安全判断`。在上面定义的变量`welcomeMessage`中，我们没有给它赋初值，因此变量`welcomeMessage`的类型是从类型标注里判断的，而不是从它初始值判断的。
### 常量和变量的命名
常量和变量的名字可以包含任意字符串，当然也包括了`Unicode`
字符。
```
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐂 = "dogcow"
```
常量和变量的命名不能包含空格字符，数学符号，箭头，保留的(或者非法的)Unicode码位，连线与制表符。也不能够用数字开头，尽管数字可能在名称的其他地方可以使用。

一旦你为常量和变量声明一个确定的类型之后，你不能够再声明一个相同名字类型的常量/变量，并且也不能够改变它所存储的类型，当然你也不能够对常量和变量的互换操作。

注意：
如果你需要使用和Swift保留关键字相同的名称作为常量和变量名。你可以使用关键字反引号(`)将关键字包起来作为它的名字，不到万不得已的时候，建议你不要使用关键字来作为常量和变量的名字。

你可以改变一个变量的值为另外一种相同类型的值，在下面的例子中，`friendWelcome`的值从`hello！`变为`Bonjour!`。
```
var friendWelcome = "hello !"
friendWelcome = "Bonjour ！"
// friendWelcome  is now "Bonjour！"
```
和变量不同的是常量在初始化设置以后就不能够发生改变了。当你改变常量值的时候，编译器会报错。
```
let languageName = "Swift"
languageName = "c++"
//Cannot assign to value: 'languageName' is a 'let' constant
// 这里是一个编译错误，languageName 不能够被改变.
```
### 打印出常量和变量

你可以用`print(_:separator:terminator:) `这个函数打印出常量和变量的当前值。
```
print(friendWelcome)
// 打印出 friendWelcome 的值
```
` print(_:separator:terminator:)`函数是一个在全局的指定区域打印出一个甚至更多值的的函数。例如在Xcode里面，`print(_:separator:terminator:)`是在xcode的控制台输出的。`separator`和`terminator`参数都有默认值，因此你当你调用函数的时候可以省略掉它们。函数默认通过换行符来结束当前行。如果不想换行，可以默认添加一个空的字符串来代替，例如：`print(someValue, terminator: "").`如果想了解更多关于参数的信息，可以查看[默认参数](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/Functions.html#//apple_ref/doc/uid/TP40014097-CH10-ID169)。

Swift用字符串插值的方式把常量名和变量名当做占位符加入到长字符串中，Swift会把常量和变量的值替换掉这些占位符。把常量和变量名放到括号里面,并在括号前面加上反斜杠来转义。

```
print("The currenct value of firendlyWelcome is \(friendWelcome)")
// 打印出当前firendlyWelcome的值
```
注意：
字符串插值所有能用的选项在[这里](https://docs.swift.org/swift-book/LanguageGuide/StringsAndCharacters.html#ID292)能找到。
### 注释

把你代码里不用执行的文本用打上注释作为注解或者一个标记来提醒你自己。在swift中，编译器会忽略掉注释的编译。

在swift中注释和在c语言的注释十分相似。单行的注释用`//`来表示。
```
// This is a comment.
```
多行注释以`/*`开始，以`*/`结尾。

```
/*
 This is also a comment.
 but is written over multiple lines. 
 */
```
和C语言中多行注释不同的是，swift中多行注释是可以进行嵌套的。你可以写一个嵌套的多行注释用`/*`开始 ，然后添加第二个多行注释以`/*`开始以`*/`结束。最后用`*/`来结束第一个多行注释。
```
/* This is the start of the first multiline comment.
 /* This is the second,nested multiline comment. */
 This is the end of the first mulitiline comment.*/
```

注释的多行嵌套使得你在注释大量代码块的时候更加便捷和容易，即使代码里已经存在多行注释也没有影响。

### 分号
和其他编程语言不同的是，在swift中，在代码的结尾，不需要你写分号(;)当然，你也可以按照你的习惯来添加分号。有一种情况是必须要添加分号的，那就是在一行中执行多个语句

```
let cat = "🐱";print(cat)
// print "🐱"
```
### 整数
整数就是没有小数的数字，比如说：42和-23.整数可以是有符号的类型(正数，负数和0)，也可以是无符号的类型(正数和0)。

`swift`为我们提供了8位，16位，32位，以及64位的无符号和有符号的整数。这些整数的命名规则和c语言类似。比如说：有无符号的8位整数`UInt8`和有符号的32位整数`Int32`。像`swift`中的其他类型一样,整数类的命名都是大写字母开头。
#### 整数的范围
你可以通过访问整数的最大值属性和最小值属性在确定他们的范围。
```
let minValue = UInt8.min // UInt8的最小值为0
let maxValue = UInt8.max // UInt8的最大值为2
print("minValue of UInt8 is \(minValue) and maxValue of UInt8 is \(maxValue)。")
```
这些属性的值表明了这种类型数据只能在规定范围内进行操作(就像上面`UInt8`的例子),因此同种类型的数据可以在表达式中一起使用。
#### Int
在大多数情况下，在写代码的过程中我们并不需要指定一个长度给`Integer`。`Swift`提供了另外一个整数类型的数据`Int`，它的长度和原生平台的字节数相同。
1. 在32位的平台上，`Int`的长度和`Int32`一致。
2. 在64位的平台上，`Int`的长度和`Int64`一致。

如果你不需要为整型添加特殊的长度处理，用默认的`Int`来实现代码就行。这可以提高代码的一致性和可复用性。甚至是在32位的平台上，他能够储存在`-2`，`147`，`483`，`648`和`2`，`147`，`483`，`647`范围之间的数据，在很多时候这个范围内的数据已经很大了。
#### UInt
`swift`也为我们提供了无符号类型的整型数据。`UInt`和原生平台有着相同长度的字节数。
1. 在32位的平台上，`UInt`的长度和`UInt32`一致。
2. 在64位的平台上，`UInt`的长度和`UInt64`一致。

注意：
尽量不要使用`UInt`,除非你真的需要存储一个和当前原生平台长度相同的字节数的无符号整数时候，如果不是这种情况，建议你最好使用`Int`，即使你要存储的对象已知是非负的。统一使用`Int`提高了代码的一致性和可复用性。避免在不同的数据类型进行转换，并且匹配数字的类型进行判断，具体请参考[类型安全和类型推断](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html#ID322)。
#### 浮点型数据
所谓浮点型数据就是带有小数部分的数据。比如：`3.14258`，`0.1`和`-273.15`。

浮点型所代表值得范围要比整型要更大，它能够储存比整型更小或者更大的值。Swift提供了两种有符号的浮点数类型。
1. `Double`类型代表的64位浮点型数据。
2. `Float`类型代表的32位浮点型数据。

注意：
`Double`类型精度至少为小数点后15位，`Float`类型的精确度仅仅是小数点后6位。
你可以根据自己编程的需要值的范围选择是`Double`类型还是`Float`类型，如果两种条件都满足，优先选择`Double`。
### 类型安全和类型判断

Swift是一个类型安全的语言，类型安全的语言可以让你清楚的知道你所处理的代码值的类型。如果你代码中需要的是`String`,那么。你如果给它赋值为`Int`类型的数据，那么编译器就会报错。

因为`Swift`是类型安全的语言，所以它在编译的时候会对代码进行类型的检查。这在开发过程中能够帮助你尽可能早的发现和解决问题。

当你在处理不同类型数据的时候，类型检查能够帮助避免一些问题。然而，这并不意味着你在每次声明常量或者变量的时候都需要显示指定类型。如果你没有指定显示类型，那么swift会使用类型判断来为你选择合适的类型。类型判断确保了编译器在编译代码的时候通过检查你赋的值自动推断出表达式的类型。

因为有了类型判断，和c或者c++相比来说，swift很少需要你进行类型声明。常量和变量虽然需要来明确类型，但是大部分工作并不需要你来完成，编译器已经为你完成了。

当你声明一个常量或者变量赋初值的时候类型判断变非常有用。在你声明常量或者变量的时候，赋给它们一个字面量(`literal value`或者`literal`)就能够让编译器自己来进行类型判断。(所谓字面量就是直接出现在代码中的值，比如下面例子中的`42`和`3.14159`。)

例如：如果你给一个新的常量用字面量的形式给它赋值为`42`没有声明它的数据类型，Swift能推断出你要给常量赋一个`Int`类型的数据，因为你在初始化的时候给它赋值了一个像整型的数字。
```
let meaningOfLife = 42
// meaningOfLife will be inferred to be of  type Int  这里常量meaningOfLife 会被便以及推断为一个整型
```
同理，如果你没有给浮点类型的数据标记类型，那么`Swift`会默认类型的`Double`
```
let  pi = 3.14159
// pi will be inferred to be of type Double 这里常量pi会被默认推断为DoubleL类型的数据。
```
当swift在推断浮点型数据的时候，它会默认推断为`Double`类型而不是`Float`类型。

如果你在一个表达式中用整型和浮点型混合计算的时候,在上下文中会被`swift`推断为`Double`类型。
```
let anotherPi = 3 + 0.14159
// anotherPi will be inferred of type Double 这里常量anotherPi会被swift推断为Double类型的数据。
```
初始值3没有给显式声明类型，并且在表达式中出现了一个浮点类型的字面量，所以表达式被推断为`Double`类型。
### 数值型字面量
整数类型的字面量可以被写作：
1. 一个十进制数，没有前缀
2. 一个二进制数，前缀是`0b`
3. 一个八进制数，前缀是`0o`
4. 一个十六进制数，前缀是`0X`
下面所有的整数型字面量都是代表十进制的值`17`
```
let decimalInteger = 17
let binaryInteger  = 0b10001// 二进制的17 2*2*2*2+1
let octalInteger = 0o21 // 八进制的17 2*8+1*1
let hexadecimalInteger = 0x11 // 十六进制的17 16*1+1
```
浮点型的字面量可以是十进制(没有前缀)，也可以是十六进制的(带有前缀)。在小数的两遍必须是十进制的值值(或者十六进制有前缀的值)。十进制的浮点数可以有一个可选的指数(exponent)。通常用大写的或者小写的e来表示，十六进制的浮点数，通常用大写或者小写的`p`来表示。

如果一个十进制的指数为`exp`，那么这个数相当于基数和`10^exp`的乘积.
例如：
`1.25e2`表示的是`1.25*10^2`或者`125.0`。
`1.25e-2`表示的是`1.25*10^-2`或者`0.0125`。
如果一个有前缀的十六进制的指数为`exp`，那么这个数相当于基数和`2^exp`的乘积。
例如：
`0xFp2`表示的是`15*2^2`或者`60.0`。
`0xFp-2`表示的是`15*2^-2`或者`3.75`。
下面的浮点型的字面量都等价于十进制的值`12.1875`。
```
//浮点类型的十进制的12.1875
let decimalDouble = 12.1875
let exponentDouble = 1.21875e1
let hexadecimalDouble = 0xC.3p0
//计算方式：0x代表16进制C代表12后面.3代表小数 所以整数部分应该是应该是12*(16^0)+0.3*(16^-1) 
后面的p代表指数，以2为底。所以完整表达式为（12*(16^0)+0.3*(16^-1)）*(2^0)
```
数字类型的字面量添加额外的标记能够使它们看起来更容易阅读。整数和浮点型都可以添加额外的零加上下划线来增强可阅读性，并且不会影响字面量的值。

```
let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_000_1
```
### 数值类型转换
即使常量和变量你已经知道它们是非负的，你也可以在代码中用`Int`类型来修饰它们。使用默认整数数据类型保证了常量和变量可以被复用并且能用来匹配整数字面量的类型推断。

当我们做特殊的任务时候才会对整型类型做类型指定，比如：需要处理的外部的长度明确了数据或者为了性能优化、内存占用等等。使用显式指定长度的类型可以及时的发现值的溢出并且还能标记我们在处理的是特殊的数据。

#### 整数类型转换
不同类型的整数可以保存不同范围的常量和变量。Int8类型的整数可以存储数据的范围是`-128`到`127`。无符号整型的可以存储常量和变量的范围是`0`到`255`。如果数字超出了常量和变量对应值的范围，编译的时候会报错。
```
let cannotBeNegative:UInt8 = -1 //不在UInt8值范围内报错
let tooBig:Int8 = Int8.max + 1  //超出Int8值范围内报错
```
因为不同数据类型能够存储数据的范围是不一样的，在进行类型转换的时候你必须选择一个合适的数据类型进行转换。这种转换方式能够让你的代码的意图更明显，并且能够防止你在隐式转换中遇到的错误。

在转换一个特殊的数字类型到另一个类型的时候，你需要重新初始化一个你需要的目标数据。在下面的例子中，常量`twoThousand`是一个`UInt16`类型的数据，和它一起需要转换的数据类型是`UInt8`,它们两个不能够直接相加，因为他们两个类型不一样。
我们可以用`UInt16(one)`来创建一个`UInt`类型的数据用`one`的值进行初始化。用初始化的数据类代替原始数据。
```
let twoThousand:UInt16 = 2_000
let one:UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
```

因为等式两边的类型都是`UInt16`，所以两者等式操作是被允许的。输出的常量`(twoThousandAndOne)`的数据类型被`swift`推断为`UInt16`，因为它是两个UInt16的常量相加而来的。

`SomeType(ofInitialValue)`调用的是`swift`构造器并传入一个初始值的默认方法。在语言的内部，UInt16有一个构造器可以接收一个`UInt8`类型的数据。这个构造的作用是通过已经存在的`UInt8`类型的数据初始化一个`UInt16`类型的数据。需要注意的是：你并不能任意的传入值，只有在传入`UInt16`内部有对应构造器的值。不过你可以扩展现有的类型，让它来接收其他类型的值(包括自定义的类型),具体请参考[扩展](https://docs.swift.org/swift-book/LanguageGuide/Extensions.html)。

#### 整数和浮点数转换
在进行整数和浮点数类型转换的时候一定要指定类型。
```
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
// pi等于3.14159，被Swift推断为double类型
```
在这里，常量`three`被当做一个`Double`类型的数据来创建，因此`+`两边应为相同的类型。如果这里没有进行转化，那么`+`(加号运算符)是不被允许使用的。
浮点型的数据和整型一样可以互相转换。整型可以使用`Double`和`Float`进行初始化。
```
let integerPi = Int(pi)
//这里integerPi等于3，被Swift推断为Int类型。
```
上面我们使用浮点型数据进行初始化一个整型数据的时候，我们发现浮点值被截断了。这意味着4.75变成了4，-3.9被截断为-3。
注意：
结合数字型的常量和变量的规则和数字字面量的规则是不同的，在字面量3可以和直接和字面量0.14159相加，因为数字型的字面量他们本身值是没有特定类型的。它们的类型只有在编译需要计算值的时候才会被推断。
### 类型别名
类型别名是给已经存在的一个数据类型添加一个可选的名字。你可以用关键字`typealias`来定义这是一个类型别名。

当你想给现有的类型添加一个有意义的名字的时候，类型别名显得特别的有用。我们假设你正在处理特定长度的外部资源的数据的时候：
```
typealias AudioSample = UInt16
```
当你定义过一个类型别名的时候，你可以在任意一个地方像使用原始名一样来使用这个别名。
```
var maxAmplitudeFound = AudioSample.min
//  maxAmplitudeFound 现在的值是0
```
在这里，`AudioSample`被定义成一个值为`UInt16`的别名。正因为这是一个别名，所以我们调用`AudioSample.min`实际上就是调用`UInt16.min`这个函数，这样为变量`maxAmplitudeFound`提供了一个初始值`0`。
### 布尔值
`Swift` 有一个基础的布尔类型叫做`Bool`，布尔的值是逻辑上的值，因此只有真和假。`Swift`为我们提供了两个bool常量`true` 和`false`。
```
let  ornagesAndOrange = true
let  turnipsAndDelicious = false
```
`ornagesAndOrange`和`turnipsAndDelicious`被推断为`Bool`因为他们是由`Bool`字面量初始化来的。就像上面提到的`Int`和`Double`类型，当在声明的时候你只需要设置一下他们的值`true	`或`false`不需要声明常量或者变量的类型。当初始化常量或者变量的时候如果要赋值的类型是已知的，就可以触发便以及的类型推断，这使得Swift的代码更加简洁和易读。

当你在写条件语句比如`if`语句的时候，布尔值显得更加有用。
```
if turnipsAndDelicious {
    print("Mmm, tasty turnips!")
} else {
    print("Eww, turnips are horrible.")
}
// 这里打印的是:Eww, turnips are horrible.
```
关于条件语句，比如`if`语句，可以参考[控制流](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html)
如果你在使用Bool值的时候赋了其他类型的值，那么swift因为类型安全就会报错。下面的例子中就会报编译的错误。
```
let i= 1
if i {
// 这个例子不会编译成功，会报错（报错原因是 判断的值不是bool类型）
}
```
然而，下面的例子是合法的：
```
let i = 1
if i == 1 {
    // 这个例子能编译成功不报错。因为这里i == 1 是一个判断语句
}
```
因为等式`i == 1`的结果是一个`Bool`类型的值，所以第二个例子能够通过类型检查。像`i == 1`这样类型的比较，参考 [基本操作符](https://docs.swift.org/swift-book/LanguageGuide/BasicOperators.html)。
和swift中其他类型安全的例子一样，这个方法避免了一些偶然的错误并且保证了代码的目的总是清晰的。

### 元组
元组(Truples)就是把多个值组合成一个复合值。元组中的成员并不一定是相同类型的数据，它们可以是任意类型的数据。
在这个例子中`(404,"Not Found")`就是一个代表`HTTP`状态码的元组。`HTTP`状态码是当你请求网页的时候，web服务器返回的一个特殊值。如果请求的网页不存在就会返回状态码`404 NOT Found`。
```
let http404Error = (404,"Not Found")
// http404Error的类型是(Int,String)的元组，值是(404, "Not Found")
```
` (404,"Not Found")	`这个元组把`Int`和`String`的值放到一起组合起来表示`HTTP`请求的状态码的两部分：一个数组和另外一个可读的描述。它被描述为一个类型为`(Int,String)`的元组。

你可以把任意顺序的类型组合为一个元组，这个元组可以你需要的任意类型的数据。你可以创建一个类型为`(Int,Int,Int)`或者`(String,Bool)`或者其他的任何你想创建任意组合的元组。

你可以将元组的内容分解为单独的常量或者变量，然后你就可以正常使用它们了。
```
let (statusCode, statusMessage) = http404Error
print("The status code is \(statusCode)")
//输出的状态码为 404
print("The status message is \(statusMessage)")
// 输出的状态描述为 Not Found
```
如果你只需要元组中的其中一个值，那么分解的时候你可以用`_`将不需要的部分省略掉。
```
let  (justTheStatusCode,_) =  http404Error
print("The status code is \(justTheStatusCode)")
// 输出的状态码为 404
```
此外，你还可以用下标来访问元组中的某个值，元组中的下标从0开始。

```
print("The status code is \(http404Error.0)")
//输出的状态码为 404
print("The status message is \(http404Error.1)")
// 输出的状态描述为 Not Found
```
你可以在定义元组的时候给单个元组进行命名

```
let http200Status = (statusCode:200,description:"OK")

```
当元组中的元素命名后，你可以通过名字来获取对应的元素的值。

```
print("The status code is \(http200Status.statusCode)")
////输出的状态码为 200
print("The status message is \(http200Status.description)")
// 输出的状态描述为 OK
```
元组在用作函数返回值的时候显得尤为重要。已给获取网页请求状态地方函数可以会返回一个`(Int,String)`元组来描述网络请求的状态。这和只能返回一个值进行比较来说。一个包含两个不同类型值的元组返回地方信息更有用。了解更多请参考[函数与返回值](https://docs.swift.org/swift-book/LanguageGuide/Functions.html#ID164)。

注意：

元组在组织临时值的时候很有用，它们并不适合用到复杂的数据结构里。如果你的数据结构不是临时的使用，那么请使用类或者结构体而不是用元组。了解更多，请参考[类与结构体](https://docs.swift.org/swift-book/LanguageGuide/ClassesAndStructures.html)。
### 可选类型

当处理值缺失情况的时候，你可以用可选类型来表示。可选类型表明有两种可能性：或者有值，你可以解析这个可选类型来访问这个值。或者这个值不存在。
注意：
在`C`语言和`Objective-C`语言中不存在可选类型这个概念。在`Objective-C`语言中最接近的是一个方法中不要么返回一个对象，要么返回`nil`，`nil`表示缺少一个合法的对象。然而，这只对对象起作用，对于结构体，基本的C数据类型以及枚举值都不起作用。对于这些类型，`Objective-C`方法中一般会返回一个特殊值(比如NSNotFound)来暗示值的缺失。这种方法假设方法的调用者知道并对这些特殊值进行判断。然而，Swift的可选类型让你明白任意类型额值缺失，并不需要一个特殊的常量。

这里有一个关于可选值是怎么被用作当做缺省值的例子，Swift中整型中有一个构造器，作用是将一个`String`类型的值转换成一个`Int`类型的值。然而，并不是所有的字符串都能够转化为整型。字符串`123`可以被转化为整型`123`，但是字符串`Hello,world`不能被转化为整型。

下面的例子中使用这种便利构造器将`String`转换成`Int`类型。
```
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)
//这里的convertedNumber 被编译器推断为'Int'类型，或者类型 ‘optional Int’
```

因为这个构造器也可能失败，所以它的返回了一个可选类型的`(optional)Int`而不是一个整型。一个可选的`Int`类型写作`Int?`而不是`Int`。这里的问号包含的值是可选类型，也就是说可能包含Int;类型的值也可能不包含。(不能包含其他的类型，比如说`Bool`类型的值或者String类型的值，它只能是`Int`类型，或者不存在这个类型。)

### nil

你可以给一个不存在的可选类型的变量赋值为`nil`：
```
var serverResponseCode:Int? = 404
// serverResponseCode中包含了一个可选的Int类型的值404
serverResponseCode = nil
// 这里serverResponseCode的值为nil(值不存在)
```
注意：
你不能够把`nil`用在非可选的变量和常量上。如果你的代码中存在常量或者变量值缺省的情况，那么在声明的时候就声明为可选变量或者常量。

如果你不提供可选类型的变量的初始值，那么变量会自动设置为`nil`。
```
var surveyAnswer:String?
//这里surveyAnswer将会被自动设置为nil
```
注意：
`Swift`中的`nil`和`Objective-C`中的`nil`意义不一样。在`Objective-C`中，nil是一个指向不存在对象的一个指针。在`Swift`中，`nil`不是一个指针，它是一个确定类型的值。任何类型的可选状态都可以被设置为`nil`，不仅仅是对象类型的数据。

### if语句以及强制解析

你可以使用if语句和nil来判断比较已给可选值是否包含值。你可以使用(`==`)以及(`!=`)等于以及不等于两个操作符来判断一个可选值是否包含值。

如果一个可选类型是有值的，那么它被认为不等于`nil`。
```
if convertedNumber != nil {
    print("convertedNumber contains some integer value.")
}
// 输出convertedNumber contains some integer value.
```
当你确定这个可选值确实包含值的时候，你可以在可选的名字后面加一个`!`来获取值。
这个感叹号表示我知道这个值有可选值，请使用它。这种被称为可选值的强制类型解析。
```
if convertedNumber != nil {
    print("convertedNumber has an integer value of \(convertedNumber).")
}
//输出的是 convertedNumber has an integer value of 123.
```
更多关于`if`条件语句的介绍，请参考[控制流](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html)。

注意:
使用`！`来获取一个不存在的值可能会导致运行时的错误。在进行强制类型解析`!`的时候要注意,确保可选类型一定要包含一个不为`nil`的值。

### 可选绑定

使用可选绑定来找出一个可选类型是否包含值，如果包含，如果包含就把值赋给一个临时变量或者常量。可选绑定可以用在if和while等条件语句中，这条语句不仅仅可以判断可选类型中是否有值，同时也可以将可选类型中的值赋给一个常量或者变量。关于if和while 语句，。请参考[控制流](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html)。

像下面一样用if语句写一个可选绑定：
```
if let constantName = someOptional {
    statements
}
```
你可以像上面那样使用可选绑定来重写在例子[可选类型](http://wiki.jikexueyuan.com/project/swift/chapter2/01_The_Basics.html#optionals)中列举的`possibleNumber`例子。
```
if let actualNumber = Int(possibleNumber) {
    print("\'\(possibleNumber)\' has an integer value of \(actualNumber)")
} else {
    print("\'\(possibleNumber)\'  could not be converted to an integer")
}
// 输出 123 has an integer value of 123
```
这段代码可以被这样来解读：
如果`Int(possibleNumber) `返回的可选`Int`包含的一个值，创建一个新的叫做`actualNumber`的常量并将包含的值赋给它。

如果转换成功，那么`actualNumber`常量可以在`if`语句的第一个分支中使用。它已经被可选类型包含的值初始化过，这里就不需要再变量的后面添加！来进行强制解析获取它的值了。在这个例子中，`actualNumber`只是被用来输出转换的结果。

常量和变量都可以使用可选类型绑定。如果你想在`if`的第一个分支语句中使用`actualNumber`,那么你可以把判断条件改为`if  var actualNumber` 这里就把可选类型中包含的值就被赋值给一个变量而不是一个常量。
你可以在`if`语句中使用多个可选绑定或者`Bool`类型来作为条件判断，它们之前用逗号隔开。如果可选类型中任意一个值为`nil`或者`Bool`类型中判断结果为`false`，那么整个if语句的条件判断就会被认为是`false`。下面例子中的`if`语句是等价的：

```
if let firstNumber = Int("4"),let secondNumber = Int("42"),firstNumber < secondNumber && secondNumber < 100 {
    print("\(firstNumber) < \(secondNumber) < 100")
}
// 打印的结果是：4 < 42 < 100
if let firstnumber = Int("4") {
    if  let  secondnumber = Int("42") {
        if firstnumber < secondnumber && secondnumber < 100 {
            print("\(firstnumber) < \(secondnumber) < 100")
        }
    }
}
// 打印的结果是：4 < 42 < 100
```
注意：
在if语句中创建的常量和变量的可选绑定，只能在body中使用。相反，在guard语句中创建的常量和变量的可选绑定，只有在guard语句之外能够取到值，请参参考[提前退出](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID525)。

### 隐式解析可选类型

就像上面描述的一样，可选类型暗示了常量和变量可以没有值，可选类型通过if语句来判断是否有值，如果有值的话可以通过可选绑定来进行值的解析。

有时候在程序的结构中，在第一次被赋值以后，可以确定一个可选的类型总是有值。在这种情况下，每次都进行判断和解析可选值是很低效的，因为可以确定这个值是总是存在的。
这种类型的可选状态被定义为隐式解析可选类型`implicitly unwrapped optionals`。把可选类型(`String?`)后面的问号改为(`String!`)叹号来声明一个隐式解析可选类型。

当可选类型在第一次被赋值以后就可以确定一直有值的时候，隐式解析可选类型显得很有用。隐式解析可选类型主要被用在Swift中类的构造器中，请参考[无主引用以及隐式解析可选属性](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html#ID55)。

一个隐式解析可选类型实际上就是一个普通的可选类型，但是可以被当做非可选类型来使用，并不需要每次都是用解析来获取可选值。下面的例子中展示了可选类型`String`和隐式解析可选类型`String`行为之间的区别。
```
let  possibleString:String? = "An optional string."
let forcedString:String = possibleString!
//需要用感叹号来获取值
let  assumedString:String! = "An implicitly unwrapped optional string."
let implicitString:String = assumedString
// 不需要用感叹号就能获取值
```
你可以把隐式解析可选类型当做一个可以自动解析的可选类型。你要做的就是在声明的时候把感叹号放到类型的结尾，而不是放到每次取值的可选名字的结尾。

注意：
如果你在隐式可选类型中没有值的时候尝试取值，那么会触发运行时的错误。这和你在没有值的普通可选类型后面添加一个叹号一样。

你仍然可以把隐式解析可选类型当做普通的可选类型来判断它是否包含值:
```
if assumedString != nil {
    print(assumedString!)
}
// 打印出 An implicitly unwrapped optional string.
```
你可以在单个语句的可选绑定类型中使用隐式解析可选类型来检查分析它的值：
```
if let definiteString = assumedString {
    print(definiteString)
}
// 打印出 An implicitly unwrapped optional string.
```
注意：

如果一个变量在之后可能会是`nil`的时候，不要使用隐式解析可选类型。如果你需要在变量的声明周期中判断是否为`nil`的时候，使用普通可选类型。

### 错误处理

你可以使用错误处理(`error handling`)来应对程序运行过程中可能会出现的错误情况。

与可选值不一样的是，运用值的存在与缺失来表达函数执行的成功与失败，错误处理可以推断出失败的原因。并可以传播到程序的其他地方。

当一个函数遇到出现错误条件的时候，它能抛出错误。调用函数方法的地方能抛出异常并合理的响应。

```
func canThrowAnError () throws {
    // this function may or may not throw an error
}
```
一个函数在声明中添加一个`throws`关键字是的时候来抛出错误消息。当一个函数可能会抛出异常的时候，你应该在表达式中使用前置`try`关键词。

`Swift`会自动将错误传播到当前的范围直到它们被`catch`句子来处理。

```
do {
    try canThrowAnError()
    // no error was thrown
} catch  {
    // an error was thrown
}
```
一个`do`语句创建了一个新的作用域，它允许错误被传递到一个或者多个`catch`语句中。
这是一个如何运用错误处理来应对不同错误情况的例子：
```
do {
    try makeASandwich()
    eatASandwich()
} catch SandwichError.outOfCleardishes {
    washDishes()
} catch SandwichError.missingTngredients(let ingredients) {
    buyGroceries(ingredients)
}
```
在这个例子中，`makeASandwich()`函数会抛出一个错误消息条件是如果没有干净的盘子或者某个原料的缺失。由于`makeASandwich()`可能会抛出错误，所以函数调用被包在了`try`语句中。将函数包在一个`do`语句中，那么任何被抛出的错误都会被传播到`catch`语句中。
如果没有错误被抛出，那么`eatASandwich()`函数会被调用。如果一个匹配`SandwichError.outOfCleardishes`的错误被抛出，那么会执行`washDishes()`这个函数，如果异常`SandwichError.missingTngredients`被捕获到，那么`buyGroceries(_:)`函数将会被调用，并且会使用`catch`所捕获到的关联值`String`作为参数。
抛出，捕获以及传播错误等，会在[错误处理](http://wiki.jikexueyuan.com/project/swift/chapter2/17_Error_Handling.html)的章节中说明。


### 断言和先决条件

断言和先决条件是在运行时进行检查的。你可以用它们来检查在执行后面代码的之前是否一个必要的条件已经满足了。如果断言或者先决条件中的`bool`值是`true`的时候，那么代码会像往常一样执行。如果条件判断为`false`，当前程序的状态是无效的，代码的执行会结束，你的app会被终止。


你使用断言和先决条件来表达你做的假设和你在编码时候的希望执行的方式。你可以将这些包含在代码中。断言帮助你在开发阶段找到错误和不正确的假设，先决条件帮助你在在生产环境中发现存在的问题。

除了在运行时验证你的期望值，断言和先决条件也变成了你代码中一种有用的文档形式。和上面讨论的[错误处理](http://wiki.jikexueyuan.com/project/swift/chapter2/17_Error_Handling.html)不同，断言和先决条件不是用来处理可以恢复或者可以预期的错误。因为一个断言失败表明了程序正在处于一个无效的状态，没有办法来捕获一个失败的断言。

使用断言和先决条件不是一个能够避免出现程序无效状态的编码方法。然而，如果一个无效状态的程序产生快了。断言可以强制检查你的数据和程序状态，使程序按照预测中的被终止，并帮助我们更简单的对这个问题进行调试。一旦遇到无效的状态，程序就会被终止，防止无效的状态对程序造成进一步的伤害。

断言和先决条件的不同之处在于它们什么时候进行检测。断言仅仅在调试的时候运行，但是先决条件不仅仅在调试的时候能运行在生产环境下也能运行。在生产环境下，断言条件不会被评估。这意味着你可以在开发阶段多使用断言，这些断言在生产条件下不会造成影响。

### 使用断言进行调试

你可以用Swift标准库的函数`assert(_:_:file:line:)`来编写一个断言。
你向这个函数传入一个判断结果为true和false的表达式以及一条错误情况下展示的信息。例如：
```
let age = -3
assert(age >= 0,"A person's age can't be less than zero.")
// 这个断言会失败 因为一个人的年龄不可能小于0（把断言中的语句变为age <= 0,就不会走这个断言）
```
在这个例子中，只有`age >= 0`为`true`也就是说`age`的值为非负数的时候，代码才会继续执行。如果age的值为负数，就像上面代码中的一样，那么，`age >= 0` 为`false`,断言失败，使得应用被终止运行。

你也可以省略掉断言的提示信息，例如：当断言条件可能会重复执行的时候
```
assert(age >= 0)
```
如果代码已经被检查过，你可以使用函数`assertionFailure(_:file:line:)`来表明断言失败了。例如：
```
if age > 10 {
    print("You can ride the roller-coaster or the ferris wheel.")
} else if age > 0 {
    print("You can ride the ferris wheel.")
} else {
    assertionFailure("A person's age can't be less than zero.")
}
```
### 强制执行先决条件
当一个条件可能为假，但是继续执行下去要求条件必须为真的时候，需要使用先决条件。例如:使用先决条件来判断下标有没有越界，或者来检查是否将一个正确的参数传给了函数。

你可以使用函数`precondition(_:_:file:line:)`来写一个先决条件。向这个函数传入一个结构为true或者false的表达式以及一条错误条件下显示信息。例如：
```
// 下标的实现
precondition(index > 0, "Index must be greater than zero.")
```
你可以调用函数[preconditionFailure(_:file:line:)](https://developer.apple.com/documentation/swift/1539374-preconditionfailure)来表明出现了一个错误,例如：`switch`的进入了`default`分支，所有的有效输入数据都应该被其他分支所处理而不是默认的`default`分支。
注意：
如果你使用不检查的模式（-Ounchecked）进行编译，先决条件将不会进行检查。编译器会假设所有的先决条件都是`true`，这将优化你的代码。然而致命的错误函数`(_:file:line:)`总是中断执行，无论你进行什么样的优化设置。

在设计原型和早期的开发阶段你可以使用致命的错误函数`(_:file:line:)`，这个阶段只是对方法的声明，
但是没有具体的实现。你可以在方法`fatalError("Unimplemented")`进行具体实现。因为`fatalError`不会像断言和先决条件那样可以被优化，所以你可以确保当代码执行到一个没有实现的方法是的时候，程序会被中断。

更多swift4.1翻译请查看[github](https://github.com/iOSDevelopShareTeam/SwiftTourv4.1)。

QQ技术交流群：214541576 

微信公众号：shavekevin

开发者头条：![](http://ww1.sinaimg.cn/large/006mQyr2ly1fqgrkt5gurj30qo1bcq53.jpg)

热爱生活，分享快乐。好记性不如烂笔头。多写，多记，多实践，多思考。

