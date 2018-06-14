---
layout:     post
title:      Swift4.1翻译
subtitle:   第一章
date:       2018-06-01
author:     shavekevin
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - iOS
    - 翻译
    - Swift
---
# 欢迎使用Swift

## 关于Swift

用swift来写代码是一种很棒的方式，不管是手机、电脑客户端服务端或者是其他别的都可以用swift代码来运行。她是一种安全快速 交互式的编程语言，结合了现代优秀编程语言的最佳思维，从更加广泛的苹果工程文化和开源社区中汲取更多的智慧。编译器对性能做了很大的优化，并且她的语言也为开发者做了优化，也就是说在性能和语言优化上，它没有做出妥协。



swift是一门极其友好的新语言。她是一种具有工业品质的一门编程语言，和脚本语言一样具富有表现力和愉悦感。用playground来写swift语言能给你所见即所得的体验，当你写完一段代码的时候，你不需要重新去编译也不需要重新运行一个app就可以看到代码执行的结果。

Swift采用了现代的编程模式来定义大量的常见编程错误

例如：

1.变量在使用之前必须要先初始化

2.数组在越界的时候发生错误

3.整形类型需要检查是否溢出

4.可选类型的变量要确保进行过判断nil处理

5.内存是系统自己管理的

6.对错误的处理允许从意外故障中恢复

为了充分利用现代的硬件，swift代码在不断被编译和优化。语法和标准库的设计基于指导库的原则，这很显然使我们的代码表现的更好。速度和安全的结合使得swift成为从hello world 到整个操作系统实现的最佳选择。

Swift将强大的类型推断和模式匹配与现代化的轻量级的语法相结合，使得我们可以用清晰的表达式来表达复杂的想法。因此，代码不仅仅是容易写，而且易于阅读和维护。

Swift的发展已经有一些年了，并且随着新特性的发展在不断的改进。我们swift的目标是雄心勃勃的。我们迫不及待的看看你用swfit能创造出来什么。


## 版本兼容性
这本书主要讲的是Swift 4.1,默认的版本的Swift是基于Xcode 9.2 版本。不论语言是Swift4 或者Swift3你都可以用Xcode9.2来进行编译。

注意：
> 当你在Swift4 环境下使用swift3的代码的时候，语言的标识应该是3.2.因此，你可以使用像#if swift(>=3.2)这样的条件编译代码块来编写与多个版本兼容的swift代码。

当你使用Xcode9.2来编译Swift3代码的时候，大部分Swift4的功能是可用的。但是下面的一些特性只在Swift4下是可用的。

    子串的操作返回值只能是子串的类型，不能是父串的类型
    @objc 这些隐式的属性被用在更少的地方。
    同一个文件中某个类型的延展，可以访问该类型的私有成员变量。  
一个用Swift4编写的工程可以依赖用Swift3写的代码，反之用Swift3写的工程也可以依赖Swift4的代码。
如果你有一个大的工程是由多个framework组成的，那么将你可以一次性的将代码从Swift3移植到Swift4框架中。


## Swift之旅

大多数人在开始学习一门新的语言的时候，按照惯例都要在打印这句单词`Hello, world!`在Swift中我们同样也可以用一句单独的话来表达。
```
print("Hello, world!")
```
如果你之前用C语言或者`Objective-C`语言写过代码的话，`swift`中的这个语法对你来说应该是很熟悉的，这一行代码就是一个完整的程序。你不需要引入另外一个框架来实现输入和输出一个字符串的操作。我们在使用一个实体的时候都是在全局作用域中使用的，因此这里我们不需要main函数。当然你也不必在每一个声明之后添加分号来结束。
这个旅行的小册子给你足够的信息关于怎么用swift来完成一系列的编程任务。如果你对一些不明白的话，也不要担心。在剩下的这本书里将会为你详细的介绍关于swift的所有东西。

注意：
使用mac下载这个playground，双击文件在Xcode 中打开 下载地址： https://developer.apple.com/go/?id=swift-tour

## 值的使用
用`let`来定义一个常量，用`var`来定义变量。常量不需要在编译期就暴露出来，你必须一次性给它赋一个特别明确的值。这就意味着你可以使用一个常量来代表一个值。这个值只被赋值一次但是可以被很多地方使用。

```
var myVariable = 42
myVariable = 50
let myConstant = 42
```

一个常量或者变量要想对它进行赋值的时候，你必须得知道需要赋什么类型的值给它们。然而，并不是所有的变量都需要直接定义类型的。当你声明一个变量或者常量的时候给他们一个类型的值，让编译器自己去判断你所定义值的类型。在上面的例子中，编译器会自己判断myVariable 是一个`integer`类型的常量，因为它是被一个`integer`类型初始化的。
常量或者变量初始化的值并不一定能提供给我们太多的信息(也可能这个常量或者变量没有赋初始值)，你可以给变量或者常量进行类型的绑定设置，用一个冒号隔开。

```
let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble:Double = 70
```

小测试：
创建一个值为4 的浮点型常量

```
let floatValue:Float = 4
```

一个值不能够直接被转化为另外一种类型(隐式转换)，如果真的需要把当前值转化为一个不同的类型，我们需要通过显式转换来获得目标值的类型。

```
let label = "The width is"
let width = 94
let widthLabel = label + String(width)
```

小测试：
如果去掉最后一行将width 转化为String的代码，将会出现什么错误呢？
结果：`Binary operator '+' cannot be applied to operands of type 'String' and 'Int'`

还有一种简单的方式可以把值转化为字符串：将你所要转化的值用圆括号括起来，然后放一个斜杠`\`到圆括号的前面，例如：

```
let apples = 3
let orange = 5
let appSummary = "I have \(apples) apples. "
let fruitSummary = "I have \(apples + orange) pieces of fruit. "
```

小测试:
在一句欢迎语中，将一个浮点型的值和一个人名用\（）拼接到一起。

```
let floatValue = 70.0
let stringName = "Kevin"
let stringValue = "My name is " +stringName+ "The Tencent rock price is \(floatValue)"
```

用三个双引号"""来定义一个多行的字符串，引号的缩进规则是相同的，例如：

```
let quotation = """
I said "I have \(apples) apples." And then I said "I have \(apples+orange) pieces of fruit."
"""
```

用`[]`创建一个数组或者字典，用	`[]`获取数组的某一个元素或者字典的某一个key，最后一个元素可以用`，`隔开。

```
var shoppingList = ["catfish","water","tulips","bluePrint"]
shoppingList[1] = "bottle of water"
var occupations = [
"malcolm":"Caption",
"Kaylee":"Mechanic",
]
occupations["Jayne"] = "Public Relations"
```


用初始化方法创建一个空的数组或者字典

```
let emptyArray = [String]()
let emptyDictonary = [String:Float]()
```

假设给出值的类型能够被编译器推测出来，你可以像这样写一个空的数组[]或者是一个空的字典[:]-- 例如：你可以像给一个变量赋值或者传递参数一样。

```
shoppingList = []
occupations = [:]
```

## 控制流程

用`if`或者`switch`来处理一些条件判断，用`for-in while` 和`repeat-while` 做循环。判断条件之间的圆括号可以省略，但是语句之间的大括号是不可以省略的。

```
let individualScores = [75,43,103,87,12]
var teamScore = 0
for score in individualScores {
    if score > 50 {
        teamScore += 3
    }else {
        teamScore += 1
    }
}
print(teamScore)
```

在一个	`if`条件语句中，判断的条件必须是一个bool类型的值，这就是说像 `if score {...}`这样写的代码是错误的，因为编译器不会隐式的与零值做比较。
你可以会用`if`和`let`这个组合来处理赋值中变量值为空的情况，这些值代表是可选类型的值。一个可选类型的值可能包含一个值或者包含一个nil来表示这个值是空的。在定义值类型后面添加一个？表示这个值是可选类型。

小测试：
```
var optionalString: String? = "hello"
print(optionalString == nil)
var optionalName: String? = "john appleseed"
var greeting = "hello"
if let name = optionalName {
    greeting = "hello,\(name)"
}

```
小测试：
将`optionalName`的值改为nil。那么`greeting `的值应该是什么呢？将`optionalName`的值改为nil并在`if`语句之后添加一个`else` 此时输出`greeting` 语句。

```
var optionalString1: String? = "hello"
print(optionalString1 == nil)
var optionalName1: String? = nil
var greeting1 = "hello"
if let name1 = optionalName1 {
    greeting1 = "hello,\(name1)"
}else {
    greeting1 = "this is an errorCode!"
}
```

输出结果为：`"this is an errorCode!"` 如果`optionalName` 为空的时候`if`判断中的代码就不会执行，此时执行是`else`语句.


如果可选类型 值为nil，因为判断条件为false不满足那么代码就会被跳过。反之如果可选类型的值就会被解包并复制给`let` 声明的常量，解包的值就能够在代码块中（花括号中）使用了。

另外一种处理可选类型的方式是用？？操作符提供一个默认的值。如果可选类型的值为空的时候，默认值就会用来替换可选类型的值。

```
let nickName: String? = nil
let fullName:String = "john Appleseed"
let informalGreeting = "hi \(nickName ?? fullName)"
```

Switches 语句支持任意类型数据的比较操作-他们不局限于基本数据类型的比较，还能用于等式的比较。

```

let vegetable = "red papper"
switch vegetable {
case "celery":
    print("Add some raisins and make ants on a log.")
case "cucumber","watrcress":
    print("that would make a good tea sandwich")
case let x where x.hasSuffix("papper"):
    print("Is it a spicy \(x)?")
default:
    print("Everything tastes good in soup.")
}

```

小测试：
试着移除switch的default case 。出现什么错误了？
```
Switch must be exhaustive
```

通过上面的操作你可以看到，`let`被用于接收可变值，然后对常量`let`进行等式判断。
执行完`switch`中对应的`case`之后，程序会结束`switch`语句的执行，因此，不用像OC一样写完一个`switch`之后紧跟一个`break`来结束	`switch`语句。
你可以用`for - in`这个语句遍历字典中的键值对。由于字典是无序的，因此他们键值对也是无序的。

```
let interestingNumbers = [
    "Prime":[2,3,5,7,11,13],
    "Fibonacci":[1, 1, 2, 3, 5, 8],
    "Square":[1, 4, 9, 16, 25],
]
var largest = 0
for (_,numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
        }
    }
}
print(largest)

```
小测试：
添加另外一个变量来找到number中的最大值，同时记录下最大的number是哪个？

```
var largestTest = 0
var largestNumber = ""
for (kindTest,numbersTest) in interestingNumbers {
    for numberTest in numbersTest {
        if numberTest > largestTest {
            largestTest = numberTest
            largestNumber = kindTest
        }
    }
}
print("the largest is \(largestTest),the lastNumber is \(largestNumber).")
```

用while来重复一段代码，直到条件满足。如果把循环条件写在结尾的话，至少要保证循环走一遍。
```
var n = 2
while n < 100 {
    n *= 2
}
print("the result of n is \(n)")
var m = 2
repeat {
    m *= 2
} while m < 100
print("the result of m is \(m)")
```

你可以使用`..<`来完成一个在一定范围内循环。

```
var total = 0
for i in0 ..<4 {
total += i
}
print(total)
```
用`..<` 来进行循环处理的时候，不包括边界的值。如果你想包括边界的值 那么用`...`来表达。

## 函数和闭包

用`func`来声明一个函数。函数调用的时候直接使用函数的名字,如果函数有参数的时候要带上参数。用`->`来分割参数名和函数返回值类型。
```
func greet (person:String,day:String) ->String {
return "Hello \(person),today is \(day)."
}
greet(person: "Bob", day: "Tuesday")
```

小测试：
去掉函数的参数`day`，然后添加另外一个参数今天午饭到问候语中。

```
func greetPre (person:String,meal:String) ->String {
    return "Hello,\(person),what will you  have on  \(meal)?"
}
greetPre(person: "Kevin", meal: "Supper")
```
一般来说，函数用它们的形参作为实参的标签。实参可以写在形参前面的标签做自定义，或者用_ 来表示没有实参标签。

```
func greetAdd(_ person:String, on day:String) ->String {
return "Hello \(person),today is \(day).
}
greetAdd("John", on:"Wednesday")
```

我们可以用一个元组来处理返回多个值的情况（复合值），比如:一个函数中有多个返回值。元组中的每一个元素可以用它们的名字或者它们的编号来表示。
```
func calculateStatistics (scores:[Int]) -> (min: Int, max:Int, sum:Int) {
    var min = scores[0]
    var max = scores[0]
    var sum = 0
    for score in scores {
        if score > max {
            max = score
        } else if score < min {
            min = score
        }
        sum += score
    }
    return (min, max, sum)

}
let statistics = calculateStatistics(scores: [5,3,100,3,9])
print(statistics.sum)
print(statistics.2)
```

函数是可以进行嵌套的，嵌套函数可以对声明在外层函数的参数进行访问。你可以在一个既长又复杂的函数中用函数嵌套来进行组织代码。

```
func returnFifteen() ->Int {
    var y = 10
    func add() {
        y += 5
    }
    add()
    return y
}
returnFifteen()
```

函数是第一类对象，这意味着一个函数可以用另外一个函数的返回值作为自己的返回值。

```
func makeIncrementer() -> ((Int) ->Int) {
    func addOne(number : Int) ->Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()
increment(7)

```
函数也可以用另外一个函数作为它的参数。
```
func hasAnyMatches(list:[Int], condition:(Int) ->Bool) ->Bool {
    for item in list {
        if condition(item) {
            return true
        }
    }
    return false
}
func lessThanTen(number: Int) ->Bool {
    return number < 10
}
var numbers = [20, 9, 7, 12]
hasAnyMatches(list: numbers, condition: lessThanTen)

```
函数是一种特殊的闭包：`block`内部的代码会延时执行。当闭包创建的时候，闭包中的代码可以对闭包中的变量和函数进行访问，就像之前的嵌套函数一样，闭包也可以在其他不同的空间中执行。你可以定义一个用`{}`包围起来但是没有名字的闭包，用`in`来分割函数名和函数的返回值。
```
numbers.map ({(number:Int) ->Int in
let result = 3 * number
return result
})
```
小测试：
重写闭包，当值为奇数时返回0

```
numbers.map ({(number:Int) ->Int in
if number % 2 == 0 {
return 0
}
return number
})
```
如果你想更简单的写一个闭包，那么下面几种方式。如果一个包的类型已经确定，比如说一个代理的回调，你可以省略参数的类型，它的返回类型或者两者都省略。单语句的闭包隐式返回执行的结果。
```
let mappedNumbers = numbers.map({number in 3 * number})
print(mappedNumbers)
```
当你使用参数的时候，你可以用参数所在位置来替代参数的名字，这在短的闭包中特别有高效。当闭包作为函数的最后个参数时，它可以直接跟在圆括号之后。如果闭包是函数仅有的一个参数，你可以直接省略掉圆括号。 
```
let sortedNumbers = numbers.sorted { $0 > $1 }
print(sortedNumbers)

```
## 类与对象
用`class`加类名来创建一个类。一个类中属性的声明常量和变量方式是相同，只不过它被声明在一个类的上下文中。同样的，方法和函数的声明写法是一样的。
```
class Shape {
    var numberOfSides = 0
    func simpleDescription() ->String {
        return "A shape with \(numberOfSides) sides."
    }
}
```
小测试：
用`let`定义一个常量并定义一个带有参数的方法。

```
let letConstrant = 5
func letConstant(parame:Int) ->String {
    return "B shape with\(letConstrant) sides."
}
```
通过在类名后面添加 一个`()`来创建一个类的实例。使用点语法访问这个实例的属性和方法。
```
var shape = Shape()
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription()
print(shape.simpleDescription(),"\n",shape.letConstant(parame:5))
```
上面这个版本的`Shape`类少了一些重要的东西：当一个实例创建的时候应该有一个初始化方法用`init`方法来创建一个。

```
class NamedShape {   
    var numberOfSides:Int = 0
    var name:String
    init(name:String) {
        self.name = name
    }
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }    
}
```
注意观察在初始化方法中是怎么用`self`来区分出调用的`name`是参数还是属性。当你创建一个了类的实例的时候，初始化参数就能像函数一样被传递使用了。每一个属性就需要被分配一个值，不管它是声明中(比如说上面的变量`numberOfSides`)或者是初始化的时候(像上面的`name`)。
如果你想在对象被销毁前做一些处理工作，可以用`deinit`来创建一个析构器。
在每个子类的后面往往都跟着它所继承的父类，用冒号隔开。一个类对于继承任何标准的基类并不是必须的，所以你可以选择引用或者省略掉父类。
子类重写父类定义的方法的时候用关键词`override`来标记。这是为了防止意外被重写。如果没有`override`关键字，编译器会报错。编译器也会检测在子类override的方法是不是真的重写了父类的某个方法。

```
class Square:NamedShape {
    
    var sideLength:Double
    init(sideLength:Double, name:String) {
        self.sideLength = sideLength
        super .init(name: name)
        numberOfSides = 4
    }
    func area() -> Double {
        return sideLength * sideLength
    }
    
    override func simpleDescription() -> String {
        return "A square with sides of length\(sideLength)."
    }
    
}
let test  = Square(sideLength: 5.2, name: "my test square")
test.area()
test.simpleDescription()
```
小测试：
再定义一个继承自NamedShape的类Circle,在它的初始化方法中有一个半径和name的两个参数。在这个类中实现area和simpleDescription两个方法。

```
class Circle:NamedShape {
    
    var radius:Double
    init(radius:Double,name:String) {
        self.radius = radius
        super.init(name: name)
        numberOfSides = 6
    }
    func area() -> Double {
        return Double.pi * radius * radius
    }
    override func simpleDescription() -> String {
        return "The radius of the circle is \(radius)."
    }
    
}
let testCircle = Circle(radius: 2, name: "the circle")
testCircle.area()
testCircle.simpleDescription()
```
属性除了能够做简单的存储之外，还能够添加`getter`和`setter`方法。
```
class EquilateralTriangle:NamedShape {
    
    var sideLength:Double = 0.0
    init(sideLength:Double,name:String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }
    var perimter:Double {
        get {
            return 3.0 * sideLength
        }
        set {
            sideLength = newValue / 3.0
        }
    }
    override func simpleDescription() -> String {
        return "An equilteral Triangle with sides of length\(sideLength)."
    }
}
var triangle = EquilateralTriangle (sideLength: 3.1, name: "a triangle")
print(triangle.perimter)
triangle.perimter = 9.9
print(triangle.sideLength)
```
在`perimter`的`setter`方法中，新值被隐式的命名为`newValue`,你可以在`setter`方法的圆括号内为新值重新命名。
我们注意到对`EquilateralTriangle`进行初始化的时候有以下三个步骤，

*  对父类声明的属性进行赋值
*  初始化的时候调用父类的初始化方法
*  改变在父类定义的属性的值，一些额外的设置工作在调用方法以及 `getter`和`setter`方法的时候也会完成。
如果你并不是真的要计算一个属性的值，但是仍然需要添加相应的代码，用willset和didset来操作新值。这段代码会在初始化之外属性值发生任意改变的时候执行。例如：下面的类保证了三角形的每一条边的长度和正方形的每一条边的长度都相等。

```
class TriangleAndSquare {
    var  triangle:EquilateralTriangle {
        willSet {
            square.sideLength = newValue.sideLength
        }
    }
    var  square:Square {
        willSet {
            triangle.sideLength = newValue.sideLength
        }
    }
    init(size:Double,name:String) {
        square = Square(sideLength: size, name: name)
        triangle = EquilateralTriangle(sideLength: size, name: name)
    }
}

var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
print(triangleAndSquare.square.sideLength)
print(triangleAndSquare.triangle.sideLength)
triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
print(triangleAndSquare.triangle.sideLength)

```
当值是可选的时候，你可以在一些操作之前添加`？`例如：使用方法、属性、下标的时候。如果在`?`之前值已经是`nil`，那么在`？`之后的所有操作都可以被忽视掉,整个表达式的结果就是`nil`。相反的，可选值将被展开(也就是说可选值是有值的)，那么在`？`之后的代码将会按照展开的值执行。综合以上两种情况，表达式的值是可选值。

```
let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
let sideWidth = optionalSquare?.sideLength
```
## 枚举和结构体
使用enum关键字来创建一个枚举，创建方式就像我们创建类和其他数据类型的数据一样，枚举里面可能会包含一些和枚举值相关的方法。

```
enum Rank:Int {
    case ace = 1
    case two,three,four,five,six,seven,eight,nine,ten
    case jack,queen,king
    func simpleDescription() -> String {
        switch self {
        case .ace:
            return "ace"
        case .jack:
            return "jack"
        case .queen:
            return "queen"
        case .king:
            return "king"
        default:
            return String(self.rawValue)
        }
    }
}
let  ace = Rank.ace
let aceRawValue = ace.rawValue
```
小测试：
写一个函数从枚举`Rank`中取出两个枚举值比下他们的`rawValue`

```
func compareFromRang(_ a:Rank,_ b:Rank) -> String{
    if a.rawValue > b.rawValue {
        return "\(a.simpleDescription())'s rawValue is the max than \(b.simpleDescription())'s"
    }else {
        return "\(a.simpleDescription())'s rawValue is the max than \(b.simpleDescription())'s"
    }
}
compareFromRang(Rank.jack,Rank.king)
```
在swift中，枚举的默认值是从0开始，枚举中成员的值是自增的，但是你可以给成员自定义值。在上面的例子中，Ace就被明确的赋值为1，它之后的成员就是按照顺序自增的。你可以使用字符串或者浮点类型的值作为枚举的初始值。使用`rawValue`这个属性来访问枚举中成员变量的值。
你可以使用`init?(rawValue:)`这个初始化方法来获取枚举中某个成员的值。如果在`Rank`这个枚举中能够找到的话，返回相对应的值。如果找不到那么就返回`nil`。

```
if  let convertedRank = Rank (rawValue: 3) {
    let threeDescription = convertedRank.simpleDescription()
    print(threeDescription)
    
}
```
枚举中的每个case值都是实际的值，另外一种写法是给他们自己定义值。事实上，如果这个值没有特殊的意义，你没有必要重新为他们赋值。

```
enum  Suit {
    case spades,hearts,diamonds,clubs
    func simpleDescription() ->String {
        switch self {
        case .spades:
            return "spades"
        case .hearts:
            return "hearts"
        case .diamonds:
            return "diamonds"
        case .clubs:
            return "clubs"
        }
    }
}

let hearts = Suit.hearts
let heartsDescription = hearts.simpleDescription()
```
小练习：
为上面的`Suit`枚举添加一个`color()`方法，使得 `spades`和`clubs` 返回`black` `hearts`和`diamonds`返回`red`。
```
    func colorDescription()->UIColor {
        switch self {
        case .spades,.clubs:
            return UIColor.black
        case .hearts,.diamonds:
            return UIColor.red
        }
    }
```
在枚举外面调用
```
let heartsColorDescription = hearts.colorDescription()

```
上面我们可以看出用两种方式引用了`hearts`这个枚举成员，当我们`hearts`这个从常量赋值的时候，枚举中的`Suit.hearts`需要用全名来引用(也就是说先找到枚举所属，然后使用它的成员变量)，因为常量没有显式的指定类型。在switch中，枚举成员使用它的缩写`.hearts`来引用，因在`suit`这个枚举中`self`是已知的类型。如果值的类型是已知的话可以使用缩写。
如果一个枚举有自己的初始值，这些值在他们声明的时候就已经确定了。那就意味着：不同枚举实例中相同成员变量都有一个相同的值。另外一种为枚举成员变量的值进行关联，那就是在创建枚举成员变量的时候确定的。这意味着枚举成员的关联值可能会不同。你可以把关联值理解为枚举成员的寄存属性。例如：可以考虑一下从服务端来获取日出和日落时间情况的请求。服务端会返回你正确的结果或者错误的描述信息。

```
enum ServerResponse {
    case result(String, String)
    case failure(String)
}
let success = ServerResponse.result("6:00 am", "8:09 pm")
let failure = ServerResponse.failure("Out of cheese.")
switch success {
case let .result(sunrise, sunset):
    print("Sunrise is at \(sunrise) and sunset is at \(sunset).")
case let .failure(message):
    print("Failure ... \(message)")
}
```
小练习：
为上面的枚举`ServerResponse`添加第三个成员变量,并添加相应的`switch`语句。
注意一下日出和日落的时间是怎么从`ServerResponse`中获取到并且和`switch`中的`case` 相匹配的。
用`struct`创建一个结构体，结构体和类有很多相似之处，比如说方法和构造器。他们之间最大的区别就是结构体是用来传值的，而类是传的是引用。

```
struct Card {
    var rank:Rank
    var suit:Suit
    func simpleDescription() -> String {
        return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
    }
    
}
let threeOfSpades = Card(rank: .three, suit: .spades)
let threeOfSpadesDescription = threeOfSpades.simpleDescription()
```
小练习：
给`Crad`添加一个方法，创建一副完整的扑克牌并把`rank`和`suit`对应起来。

## 协议和扩展
用`protocol`来声明一个协议
```
protocol ExampleProtocol {
    var simpleDescription:String{get}
    mutating func adjust()
}
```
类、枚举和结构体都能够遵循并实现协议。

```
class SimpleClass:ExampleProtocol {
    var simpleDescription: String = "A very simple class."
    var anotherProperty:Int = 69105
    func  adjust() {
        simpleDescription += " Now 100% adjusted."
    }
    
}
var a  = SimpleClass()
a.adjust()
let aDescription = a.simpleDescription
struct SimpleStructure:ExampleProtocol {
    var simpleDescription: String = "A simple structure"
    mutating func adjust() {
        simpleDescription += "(adjusted)"
    }
    
}
var b = SimpleStructure ()
b.adjust()
let bDescription = b.simpleDescription
```
小练习：写一个枚举遵守上面的这个协议。
```
enum SimpleEnum:Int,ExampleProtocol {
    case type,title
    var simpleDescription:String {
        switch self {
        case .type:
            return "A simple  enum  about  type"
        case .title:
            return "A simple  enum  about  title"
        }
    }
    func adjust() {
        print("this is enum")
    }
}
var c = SimpleEnum.type
c.simpleDescription
c.adjust()
```
注意在声明`SimpleStructure`的时候使用关键字`mutating`来标记一个能改变结构体值的方法。`SimpleClass`的声明不需要用关键字来标记修改它的方法，因为类里的方法是可以一直发生改变的。
用`extension`延展来为现有的类添加功能，比如添加一些新的方法和可以用来计算的属性。你可以用延展来添加一个协议给一个在其他地方创建的类，甚至添加的类型可能是引用的一个library或者框架。
```
extension Int:ExampleProtocol {
    
    var simpleDescription:String {
        return "The number \(self)"
    }
    mutating func adjust() {
        self += 42
    }
}
print(7.simpleDescription)
```
小练习：
给`Double`类型的数据添加一个`absoluteValue`属性

```
extension Double {
    var absoluteValue:String {
        return "The Double number is \(self)"
    }
}
print(2.0.absoluteValue)
```
你可以像使用其他命名类型一样来使用协议名，例如：创建一个具有不同类型的数据的集合，这些不同类型的数据都遵循同一个协议。当你要处理的类型是协议的值的时候，协议之外定义的方法是不可用的。
```
let protocolValue:ExampleProtocol = a
print(protocolValue.simpleDescription)
// 打开注释你就会发现报错信息
//print(protocolValue.anotherProperty)
//Value of type 'ExampleProtocol' has no member 'anotherProperty'
```
尽管`protocolValue`这个变量在运行时的时候类型是`SimpleClass`,编辑器在编译的时候仍然把它的类型当`ExampleProtocol`。这就意味着你不能访问类在协议方法之外的属性或者方法。
## 错误处理
你可以用任何遵循`Error`协议类型来表示错误。
```
enum PrinterError:Error {
    case outOfPaper
    case noToner
    case onFire
}
```
用`throw`这个关键字来抛出一个错误，并且用`throw`来标记一个可以抛出错误的一个函数。如果你在一个方法里抛出了一个错误，函数会立即返回并且会调用函数的代码进行处理错误。
处理error的方式有很多种，一种方式是用`do-catch`。在`do`这个代码块里面，在你需要标记的抛出错误的代码之前添加`try`。在`catch`的代码块里，错误会自动被命名`error`，当然除非你给错误指定一个新的名字。
```
do {
    let printerResponse = try send(job: 1040, toPrinter: "Bi sheng")
    print(printerResponse)
} catch  {
    print(error)
}
```
小练习：
改变打印者的名字为“Never Has Toner”,让`send(job:Toner)`抛出一个错误。
```
do {
    let printerResponse = try send(job: 1040, toPrinter: "Never Has Toner")
    print(printerResponse)
} catch  {
    print(error)
}
```
你可以自己定义多个`catch`代码块来处理错误。你可以在`catch`之后添加一种模式，用法可以和`switch`中使用成员变量`case`一样。
```
do {
    let printerResponse = try send(job: 1440, toPrinter: "Gutenberg")
    print(printerResponse)
} catch PrinterError.onFire {
    print("I'll just put this over here,with the rest of the fire")
} catch let printferError as PrinterError {
    print("Printer error:\(printferError)。")
} catch {
    print(error)
}
```
小练习：
在`do`代码块中添加抛异常的代码。你要抛出什么样的错误才能让第一个catch接收并处理？第二个 第三个呢？
对`send(job:Int,toPrinter printerName:String)`作补充就可以得到问题的答案了
```
func send(job:Int,toPrinter printerName:String) throws-> String {
    if printerName == "Never Has Toner" {
        throw PrinterError.noToner
    } else if printerName == "Out Of Paper"
    {
        throw PrinterError.outOfPaper
    }
    else if printerName == "On fire" {
        throw PrinterError.onFire
    }
    return "Job sent"
}
```
另外一种处理错误的方式是使用`try?`关键字来转换结果为可选项。如果函数抛出了一个错误，错误将被忽略并且结果会被置为nil。
否则，结果就是一个包含了函数返回值的可选项。(这就是说如果抛出异常那么结果就是nil，如果不抛出异常那么结果就是一个带有一个返回值的可选项。)
```
let printerSuccess = try?send(job: 1884, toPrinter: "Mergenthaler")
let printerFailure = try?send(job: 1885, toPrinter:"Never Has Toner")
```
使用`defer`代码块来表示在函数返回之前，函数执行的代码。这段代码会执行不管函数是否抛出错误。使用`defer`你可以将设置和清除的代码写在里面，尽管它们执行的时机可能完全不同。
```
var fridgeIsOpen = false
let fridgeContent = ["milk","eggs","leftovers"]
func fridgeContains(_ food:String) -> Bool {
    fridgeIsOpen = true
    defer {
        fridgeIsOpen = false
    }
    let result = fridgeContent.contains(food)
    return result
    
}
fridgeContains("banana")
print(fridgeIsOpen)
```
## 泛型
 在尖括号里写一个名字来创建一个泛型函数或者泛型的类型。
```
func makeArray<Item>(repeating item:Item, numberOfTimes:Int) -> [Item] {
    var result = [Item]()
    for _ in 0 ..< numberOfTimes {
        result.append(item)
    }
    return result
}
makeArray(repeating: "knock", numberOfTimes: 4)
```
你也可以创建泛型的函数和方法，在类、枚举和结构体里都可以使用。
```
// Reimplement the Swift standard library's optional type
enum OptionalValue<Wrapped> {
    case none
    case some(Wrapped)
}
var possibleInteger:OptionalValue<Int> = .none
possibleInteger = .some(100)
```
在类型名字的后面使用`where`来指定对类型的一系列的需求，例如：限定一个类型来执行一个协议，限定两个类型是相同的,指定一个类有一个特定的父类。
```
func anyCommonElements<T:Sequence,U:Sequence>(_ lhs:T,_ rhs:U)->Bool
    where T.Iterator.Element:Equatable,
    T.Iterator.Element ==
    U.Iterator.Element {
        for lhsItem in lhs {
            for rhsItem in rhs {
                if lhsItem == rhsItem {
                    return true
                }
            }
    }
    return false
}
anyCommonElements([1,2,3], [3])
```
小练习：
修改`anyCommonElements(:)`函数来创建一个函数，返回一个数组。内容是两个序列里的公共元素。
```
func anyCommonArrayElements<T:Sequence,U:Sequence>(_ lhs:T,_ rhs:U)->Array<Any>
    where T.Iterator.Element:Equatable,
    T.Iterator.Element ==
    U.Iterator.Element {
        var  array = Array<Any>()
        for lhsItem in lhs {
            for rhsItem in rhs {
                if lhsItem == rhsItem {
                   array.append(lhsItem)
                }
            }
        }
        return array
}
anyCommonArrayElements([1,2,3], [2,3,4,5])
```
上面我们所写的`<T:Equatable>`和`<T>...where T:Equatable` 是等价的。

更多swift4.1翻译请查看[github](https://github.com/iOSDevelopShareTeam/SwiftTourv4.1)。

QQ技术交流群：214541576 

微信公众号：shavekevin

开发者头条：![](http://ww1.sinaimg.cn/large/006mQyr2ly1fqgrkt5gurj30qo1bcq53.jpg)

热爱生活，分享快乐。好记性不如烂笔头。多写，多记，多实践，多思考。


