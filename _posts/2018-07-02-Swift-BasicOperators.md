---
layout:     post
title:      Swift4.1翻译
subtitle:   第二章 Basic Operators
date:       2018-07-02
author:     shavekevin
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - iOS
    - 翻译
    - Swift
---
## 基本运算符

一个运算符是一个特殊的字符或短语，你可以用它来检查，改变，合并值。例如：加号(`+`)表示两个数相加,例如`let i = 1 + 2`。还有逻辑运算符 `AND (&&)`用来关联两个布尔值，例如：`if enteredDoorCode && passedRetinaScan`。

`Swift`支持大多数标准的`C`语言的操作符，并且改进了许多特性用来减少常规的编译错误。操作符`=`不意味着返回一个值，这是为了和赋值运算符`==`进行区分，避免因为错写为`=`出现错误。算数运算符(`+,-,*,/ `等)会检测并不允许值的溢出，这主要是用来避免因为值过大或者过小而超出它的类型所承载的范围导致异常的结果。你可以使用swift溢出的运算符来实现溢出，具体请参照[溢出运算符](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html#ID37)。

`Swift`和`c`语言不同的是，swift提供了区间运算符。例如：`a..<b`和`a...b`，这方便我们表达一个区间内的数值。

这个小节描述了`Swift`中的基本操作符，[高级运算符](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html)会包含Swift中的高级运算符，以及如何进行自定义运算符和如何用你自己的方式来实现标准的操作符。

### 术语
 
 运算符分为一元，二元和三元运算符。
 * 一元运算符是对单一目标进行操作的(例如`-a`)。一元运算符有前缀和或追之分，前缀运算符往往出现在操作对象的前面(例如`!b`),后缀运算符往往出现在操作对象的后面 (例如：`c!`)
 * 二元运算符是操作对象是两个目标，运算符的位置在操作对象的中间(例如：`a+b`)。
 * 三元运算符的操作对象是三个目标，和`c`语言一样，swift只有一个三元运算符，就是三目运算符(`a?b:c`)。
   
   受操作符影响的值叫操作者。在表达式`1+2`中，操作符`+`是一个二元运算符，它的两个操作者的值是`1`和`2`。
   
### 赋值运算符
赋值运算符用于初始化和更新`a`和`b`的值(例：`a=b`)。
```
let b = 10
var a = 5
a = b
// 现在a的值为10
```
如果赋值运算符的右边是一个具有多值的元组，那么它的成员可以被立即分解成多个常量和变量。

```
let (x, y) = (1,2)
//  x的值为1  y的值为2
```
赋值运算符在swift中和在Objective-C以及C语言中是不同的，赋值运算符在`swift`中不会返回一个值。下面的语句是不合法的：
```
if x = y {
    // 这是不合法的，因为等式 x = y没有返回值。
}
```
`Swift`中的这个特性避免了在使用等式运算符(`==`)中因为误用赋值运算符(`=`)而导致的错误。当语句`if x = y `不合法的时候，`swift`会在你的代码中提示你避免出现这样的错误。
### 算术运算符

swift为所有的数字类型提供了四种标准的算术运算符。
 * 加号运算符(`+`)
 * 减号运算符(`-`)
 * 乘号运算符(`*`)
 * 除号运算符(`/`)
```
1 + 2 // 等于3
5 - 3 // 等于2
2 * 3 // 等于6
10.0 / 2.5 // 等于4.0
```
和`Objective-C`和`C`语言不同的是，`Swift`的算术运算符不允许值超出默认范围。但是你可以使用`Swift`的溢出运算符来进行值溢出的运算。(例：`a &+ b`),具体请参见[溢出运算符](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html#ID37)。
加号运算符同样使用于字符串的拼接：
``` 
"hello," + “world” // 等价于hello,world
```
#### 求余运算符
求余运算符(`a%b`)是计算`b`的多少倍刚好可以放下`a`，然后返回一个多出来的值（也就是求余数）。(比如：4%2 余数为0，3%2 余数为1)。

注意：
求余运算符(`%`)在其他语言中也就做求模运算符。然而严格来说，在swift中这个操作符是对于负数来说的，这里叫做求余比求模更加贴切。

这里给大家讲一下求余运算符是怎么工作的。计算`9%4`，首先你要计算出`4`的多少倍能够放得下`9`：

![求余运算](http://ww1.sinaimg.cn/large/006mQyr2ly1fsoa8b5kn4j30iq03p0sm.jpg)

你可以发现4的多少倍能够放得下`9`，余数为`1`(橘色展示的就是)

在Swift中，求余是这样写的：
```
9 % 4 // 等于1
```
为了计算出`a%b`的值，操作符`%`用下面的等式来计算并返回了余数作为输出。
```
a = (b * 倍数) + 余数
```
当`倍数`是b的一个很大的倍数的时候，能够放的下`a`。

把 `9` 和`4` 带入等式以后：
```
9 = (4 * 2) + 1
```
当a的值为负数的时候，计算余数的方法同样适应：
```
-9 % 4 // 等于1
```
余数的值为`-1`。
在对`b`求余的时候，`b`的符号可以被忽略掉，这就是说`a % b`和`a % -b` 结果是一样的。

#### 一元负号运算符

数值类型正负可以用在前面加`-`来进行转换，这就是所谓的一元负号运算符。
```
let three = 3
let minusThree  = -three// 等价于 -3
let plusThree = -minusThree // 等价于3
```
一元负号运算符在使用的时候，直接加载常量和变量之后，他们之间不需要添加空格。
#### 一元加号运算符

当一元加号运算符使用的时候，操作符返回的值是他本身，没有发生任何改变。
```
let minusSix = -6
let  alsoMinusSix = +minusSix
//alsoMinusSix 的值仍为-6
```
尽管一元加号运算符在使用的时候没有什么实际意义，但是在你使用一元负号来表示负数的时候，可以用一元加号来表示一个正数，这样会使你的代码看起来对称。
### 组合运算符
和C语言一样，Swift也提供了组合运算符用(`=`)和其他操作符的组合。下面是一个加号的组合运算符：
```
var a = 1
a += 2 // 这里a的值为3
print("aa value is \(a)")
```
表达式`a += 2` 是表达式`a = a + 2`的缩写，一个组合加号运算符就是把加号运算和赋值运算符组合成一个，同时完成两个运算任务。

注意：
组合运算符不会返回一个值，例如：你不能这样写：`let  b = a += 2`。

关于更多swift标准操作符的问题，请查看[运算符声明](https://developer.apple.com/documentation/swift/swift_standard_library/operator_declarations)。
### 比较运算符
`Swift`支持所有标准的C语言比较符。
* 相等(`a == b`)
* 不相等(`a != b`)
* 大于(`a > b`)
* 小于(`a < b`)
* 大于等于(`a >= b`)
* 小于等于(`a <= b`)

注意：
Swift也提供了两个操作符 恒等和不恒等(`===` and `!==`)用这两个操作符你可以判断两个对象是否引用同一个实体实例。了解更多请参照[类与结构体](https://docs.swift.org/swift-book/LanguageGuide/ClassesAndStructures.html)。

每一个比表运算符都会返回一个布尔值表示这个表达式是不是对的。
```
1 == 1 // true 因为1和1 相等
2 != 1 // true 因为2 不等于1
2 > 1 // true 因为2 大于 1
1 < 2 // true 因为1 小于2
1 >= 1 // true 因为1 等于1 满足1 大于等于1
2 <= 1 // false 因为2 小于等于1
```
比较运算符也经常用在条件语句中，比如说`if`语句：
```
let  name = "world"
if name == "world" {
    print("Hello world")
} else {
    print("I'm sorry \(name),but I don't recognize you")
}
// 打印的结果是 Hello world 因为name 等于“world”
```
更多关于`if`语句的用法，请参看[控制流](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html)

如果两个元组的类型相同并且有相同个数的子元素，那么这两个元组可以用来比较。元组从左到右一个值一个值的进行比较，直到发现有两个不同的值为止。在进行比较的过程中，如果元组中每个元素都相同，那么我们可以说这两个元组相等。例如：
```
(1,"zebra") < (2,"apple") //返回true 因为1比2小，"zebra"和"apple"是不能被比较的
(3,"apple") < (3,"bird") // 返回true 因为3 等于 3，"apple" 比"bird"少
(4,"dog") < (4,"dog") // 返回true，因为4 等于4 “dog”和“dog”相同。
```
在上面的这个例子中，你可以看到从左到右的比较行为出现在第一行。因为`1`比`2`小，`(1,"zebra")`已经被认为比`(2,"apple")`小了，不管元组的其他值，所以`"zebra">"apple"`对结果没有影响,因为在比较的时候元组的第一个元素就已经把结果定了。不过当第一个元素相等的时候，就会对第二个第三个元素进行比较了。

当元素的每个元素都能够用操作符进行比较的时候，我们可以对元组进行比较。例如：在下面的代码中你可以对两个`(String，Int)`类型的元组进行比较，因为`String`和`Int`都可以用操作符`<`进行比较。相反，`(String,Bool)`类型的元组不能用操作符`<`进行比较，因为Bool不能用操作符`<`进行比较。

```
("blue",-1) < ("purple",1)// OK ，返回结果为true
("blue",false) < ("purple",true)//Binary operator '<' cannot be applied to two '(String, Bool)' operands 布尔类型的值不能进行比较(本身比较已经是true和false了。。再进行比较，过分了啊)
```
注意：
`Swift`标准库里是包含元素小于7个的元组之间的比较的。如果要比较超过7个元素的元组的话，你必须自己实现比较的操作符。

### 三元运算符

三元运算符是一个特殊的操作符是由三个操作数组成，比如：`question？answer1：answer2`这种形式。这个是基于`question`是`true`还是`false`的一种表达。如果`question`是`true`那么它的返回`answer1`的值，否则，返回`answer2`的值。

三元运算符的简写如下：
```
//let  question = true
//let answer1 = "333"
//let answer2 = "333"
//print("the answer is \(question ? answer1:answer2)")
if question {
    answer1
} else {
    answer2
}
```

这里有一个计算表格行的高度的例子。题意大概是这样的，内容的高度是固定的，当这一行有表头的话高度加50如果没有表头的话加20。

```
let contentHeight = 40
let hasHeader = true
let rowHeight = contentHeight + (hasHeader ? 50:20)// 结果为90
```

上面的这个语句是下面的语句的简写:

```
let contentHeight = 40
let hasHeader = true
let rowHeight:Int
if hasHeader {
    rowHeight = contentHeight + 50
} else {
    rowHeight = contentHeight + 20
}
// rowHeight 结果为90
```

在第一个例子中，用的是三元操作运算符意味着`rowHeight`一行低吗就能得到正确的值，这比第二个例子的代码更加简洁。

三元条件运算符提供了一个高效的判断两个参数表达式的标准，需要注意的是，过度的使用三元运算符会使简洁的代码看的不容易懂。我们应该避免在一个组合的语句中使用多个三元运算符。

### 合并空值运算符

合并空值运算符(`a ?? b`)对可选类型`a`如果包含一个值的时候被打开，或者当`a`的值为空(`nil`)的时候返回一个默认的值`b`。表达式`a`也是一个可选类型。默认值b的类型必须要和a所存储的值的类型保持一致(也就是说既然`b`是`a`的默认值，那么`b`的值的类型就必须和`a`保持一致，这才是默认值的意义所在，如果`a`没值那么默认值就顶上来)。

合并空值运算符最简单的代码表达式这样的：
```
a != nil ? a!  : b

```
上面的示例代码中使用了三元运算符，当可选类型`a`不为空的时候，强制打开a(`a!`)，访问`a`的值，反之，返回默认值`b`。合并空值运算符提供了一个更加优雅的方式来对条件进行判断和封装，这增加了代码的简洁性和易读性。

注意：
如果a的值是非空的时候，b的值永远不会被使用。这也就是所谓的短路求值。

下面的例子采用的合并空值运算符实现了在默认颜色和可选自定义颜色中进行选择。
```
let defaultColorName = "red"
var userDefinedColorName: String?//默认值是nil
var colorNameToUse = userDefinedColorName ?? defaultColorName
// 因为userDefinedColorName是nil，所以colorNameToUse被设置为默认值"red"
```
变量`userDefinedColorName`定义的是默认值为`nil`的可选的变量，因为变量`userDefinedColorName`是可选的类型，因此你可以使用合并空值运算符来空值它的值。在上面的例子中，操作符被用来决定一个字符串变量`colorNameToUse`的默认值。因为`userDefinedColorName`的值为空，表达式`userDefinedColorName ?? defaultColorName`返回了`defaultColorName`也就是`"red"`。

如果你给`userDefinedColorName`赋一个非空的值，然后让合并空值运算符来检查一下，那么`userDefinedColorName`的值就会替换掉默认值。
```
userDefinedColorName = "green"
var colorNameToUse = userDefinedColorName ?? defaultColorName // 因为userDefinedColorName 不为空，所以colorNameToUse的值为"green"。
```
### 区间运算符
Swift包含了几个区间运算符，他们表示了一个范围的值的便捷方式。
#### 闭区间运算符
闭区间运算符(`a...b`)定义了一个只能在`a`和`b`之间的运行范围，它包括边界a和b。`a`的值必须必`b`小。
如果你想在某个范围内的值被使用，那么闭区间操作符很有用。比如说`for-in`循环。
```
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}
// 打印的结果是
//1 times 5 is 5
//2 times 5 is 10
//3 times 5 is 15
//4 times 5 is 20
//5 times 5 is 25
```
了解更多关于`for-in`信息，请参看[控制流](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html)。

#### 半开区间运算符
半开区间运算符(`a ..< b`)定义了一个能在`a`和`b`之间运行的范围，但是不包括`b`。也就是说，半开区间包括了它的首值，但不包括尾值(也就是说是半开半闭区间)。和闭区间操作符一样，`a`的值总是小于`b`的。如果a的值和b的值相同，那么结果区间就是空的。

当你在处理从0开始的数组的时候，半开运算符显得很有用，它从0开始遍历到数组的长度(但是不包含数组的长度)。

```
let names = ["Anna","Alex","Brian","Jack"]
let count = names.count
for i in 0 ..< count {
    print("Person \(i + 1) is called \(names[i])")
}
// 打印结果是：
//Person 1 is called Anna
//Person 2 is called Alex
//Person 3 is called Brian
//Person 4 is called Jack
```
我们可以观察到，数组包括四个元素，但是`0 ..< count`仅包括到3(数组的最后一个元素的索引)，因为这是半开半闭区间。关于更多数组相关信息，请查看[数组](https://docs.swift.org/swift-book/LanguageGuide/CollectionTypes.html#ID107)。

#### 单侧运算符

闭区间有另外一种形式让区间朝着一个方向尽可能长的延伸。例如：一个包含所有数组元素的区间，从索引为2的地方开始到数组的结束。在这种情况下，你可以省略掉操作符一边的值。因为操作符仅一边有值，所以它叫做单侧区间。例如：
```
for name in names[2...] {
    print("\(name)")
}
// 打印结果是：
//  Brian
// Jack
for name in names[...2] {
    print("\(name)")
}
// 打印结果是：
//  Anna
//  Alex
// Brian
```
半开区间范围操作符也有单侧的形式，只需要你写下末值即可。和半开区间中两侧都包含值一样，末值都不是区间的一部分。例如：
```
for name in names[..<2] {
    print("\(name)")
}
// 打印结果是：
//Anna
//Alex
```
单侧区间可以在其他上下文中使用，不仅仅作为下标使用。你不能够省略区间的首值，因为区间遍历的开端是不明显的，你可以省略掉一个区间中的尾值，因为区间本身具有延伸的特性，确保你在循环里有一个结束循环的条件。你可以检查一下某个单侧区间是否包含一个特殊值，就像下面的代码一样。

```
let range = ...5
range.contains(7) //false
range.contains(4) //true
range.contains(-1) //true
```

### 逻辑运算符

逻辑运算符的操作对象是逻辑布尔值(`true or false`)，Swift基于C语言的三种逻辑表达式。
* 逻辑非(`!a`)
* 逻辑与(`a && b`)
* 逻辑或 (`a || b`)

#### 逻辑非运算符

逻辑非运算符是对一个布尔值取反，就是让`true`变成`false`，让`false`变成`true`。
逻辑非运算符是一个前置运算符，它往往出现在操作值的前面，不需要添加空格。它可以被读作`非a`，下面是一个例子：
```
let  allowedEntry = false
if !allowedEntry {
    print("ACCESS DENIED")
}

//打印结果是ACCESS DENIED
```
表达语句`if !allowedEntry`可以被读作“如果不允许进入”。下面一行代码只有在“不允许进入”是`true`，也就是说只有在`allowedEntry`是`false`的时候执行。

在这个例子中，小心的选择布尔常量和变量有助于我们保持代码的可读性，并且避免了双重逻辑非运算符，或者混乱的逻辑语句。

#### 逻辑与运算符

逻辑表达式与运算(`a && b`)表示的是只有等式两边同时为`true`的时候，才为`true`，否则就是`false`。
如果有任意一个为`false`，那么整个表达式就是`false`。事实上，如果第一个表达式为`false`的时候，第二个表达式就不执行了，因为这个时候已经不能保证整个表达式是`true`了，这被称为短路计算。
下面的例子中，只有当两个判断是中的值都为`true`的时候，`if`语句才会执行。

```
let enterDoorCode = true
let passedRetainScan = false
if enterDoorCode && passedRetainScan {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
//打印结果是ACCESS DENIED
```

#### 逻辑或运算符

逻辑或运算符是由两个内置运算符`|`组成。你可以用它来表达两个表达式中任意一个为`true`，那么整个表达式都是`true`。

和上面的逻辑与运算符一样，逻辑运算符或也有一个短路的计算。当左边的表达式的值为`true`的时候，运算符右边的值就不被计算了，因为不论它是`true`或者`false`都不会影响真个表达式的值。

在下面的例子中，第一个布尔值(`hasDoorKey`)是`false`，但是第二个值`knowsOverridePassword`是`true`。因为其中一个值为`true`，那么整个表达时的值就是`true`，通道是被允许的。

```
let hasDoorKey = false
let knowsOverridePassword = true
if hasDoorKey || knowsOverridePassword {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
//打印结果是Welcome!
```
#### 混合逻辑运算

你可以把多个逻辑运算符放到一起，创建一个混合逻辑表达式。

```
if enterDoorCode && passedRetainScan || hasDoorKey || passedRetainScan {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
//打印结果是Welcome!
```
上面的这个例子中使用了多个逻辑运算符`&& `和 `||`创建了一个混合逻辑运算符。然而，表达式`&& `和 `||`都只能操作两个值，所以这实际上是三个简单的逻辑表达式连续执行的结果，这个例子可以被解读为：

如果我们输入了正确的密码并且通过了视网膜的扫描，或者我们有一把有效的钥匙，或者我们知道怎么在紧急情况下重置密码，那么就被允许进入。

在`enterDoorCode`和`passedRetainScan` 以及`hasDoorKey` 因为 enterDoorCode 和 passedRetainScan的值都是false,固逻辑运算符`&` 值为`false` 逻辑运算符`||` `hasDoorKey`也为`false`。但是紧急情况重置密码的权限是`true`。所以整个混合表达式的值就是`true`。

注意：
`swift`的逻辑运算符`&&`和 `||`都是左结合式，它意味着混合表达式是由多个逻辑表达式以及计算的。他们在计算的时候优先计算左边的表达式。

### 显式括号

为了使表达式易读懂，我们有时候会在合适的地方用括号来包含一个逻辑，当然这个括号可能是非必要的。在上个关于门权限的例子中，我们把第一部分用括号括起来了，这样看起来逻辑更加明确：

```
if (enterDoorCode && passedRetainScan) || hasDoorKey || knowsOverridePassword {
    print("Welcome!")
} else {
    print("ACCESS DENIED")
}
//打印结果是Welcome!
```

通过这个括号我们能清楚的看到在整个逻辑表达式中前两个值是逻辑表达式中独立的一部分。虽然最终的输出结果没有变化，但是整个逻辑表达式显得更容易读懂。可读性有时候比简洁性更加重要，为了使你的代码逻辑更加清晰在合适的地方加上括号吧。

更多swift4.1翻译请查看[github](https://github.com/iOSDevelopShareTeam/SwiftTourv4.1)。

QQ技术交流群：214541576 

微信公众号：shavekevin

开发者头条：![](http://ww1.sinaimg.cn/large/006mQyr2ly1fqgrkt5gurj30qo1bcq53.jpg)

热爱生活，分享快乐。好记性不如烂笔头。多写，多记，多实践，多思考。




