---
layout:     post
title:      Swift4.1翻译
subtitle:   第二章 Strings and Characters
date:       2018-05-31
author:     BeyoundCong
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - iOS
    - 翻译
    - Swift
---
## 字符串和字符

字符串就是由一系列的字符组成，例如：“hello，world”或者“albatross”。

Swift 中的字符串由 String 表示。字符串（包括 Character values ）可以以多种方式访问。

Swift 的字符串和字符类型提供了一种快速、符合 Unicode 的方法，可以在代码中使用文本。字符串的语法创建和操作容易，可读性强。可以使用字符串将常量、变量、文字和表达式插入到更长的字符串，这样不论是显示、存储和打印一些特定的字符串值会更加容易。

注意：

   Swift 的字符串类型与 Foundation 的 NSString 类连接。Foundation 还扩展了字符串，以暴露由 NSString 定义的方法。如果您导入 Foundation，您就可以在没有选择的情况下访问那些 NSString 方法。

```
   let string:String = "hello";
   let otherString:NSString = "world";
   print(string + (otherString as String));
```

使用字符串字面量作为常量或变量的初始值:

```
   let someString = "Some string literal value”
```

创建多行字符串:（不会以换行符开头或结尾）

   ```
   let quotation = """
   The White Rabbit put on his spectacles.  "Where shall I begin,
   please your Majesty?" he asked.
    
   "Begin at the beginning," the King said gravely, "and go on
   till you come to the end; then stop.
   """
   ```

多行字符串中如果想使用换行符让源码更容易阅读，并且不希望换行符是字符串值的一部分，可以在这些行的末尾加一个反斜杠（\）:

```
   let someString = """
   “The White Rabbit put on his spectacles.  "Where shall I begin, \
   please your Majesty?" he asked.”
   “Begin at the beginning," the King said gravely, "and go on \
   till you come to the end; then stop.”
   """
```

让一个多行字符串字面意思开始或以一个行结束，写一个空行作为第一行或者最后一行:

```
   let someString = """

   “This string starts with a line break.
   It also ends with a line break.”

   """
```

多行字符串可以缩进匹配周围的代码。在结束引号(“”)之前的空格会告诉Swift在所有其他行之前忽略哪些空白。以下俩份代码可以运行对比一下输出

```
   let someString = """
       “This string starts with a line break.
           adada
       It also ends with a line break.”

   """
```

```
       let someString = """
   “This string starts with a line break.
       adada
   It also ends with a line break.”

   """
```

### 字符串中的特殊字符

字符串值中可以包括以下特殊字符：

   > 转义符: 空字符\0、反斜杠 \\\ 、水平Tab \t、换行\n、回车\r、双引号\"和单引号\‘ 。一个任意的 Unicode 标量，写成\u{n}，其中 n 是一个 1-8位十六进制数字，其值就等于一个有效的 Unicode 编码点。例如：

```
  let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
  let dollarSign = "\u{24}"
  let blackHeart = "\u{2665}"
  let sparklingHeart = "\u{1F496}"
```

多行字符串文本使用了三个双引号而不是一个，所以在多行字符串字面上包含双引号（“），不需要转义。如果要在多行字符串中包含文本""，至少要对其中一个引号做处理。例如:

```
  let threeDoubleQuotationMarks = """
  Escaping the first quotation mark \"""
  Escaping all three quotation marks \"\"\"
  """
```

初始化一个空字符串:

```
  var emptyString = ""
  var anotherEmptyString = String()
```

检查字符串值以及 BOOL 属性是否为空

```
  var name = ""
  if name.isEmpty {
      print("Nothing to see here")
  }
```

字符串具有可变性：

  可以指定一个字符串是否可以通过将其赋值给一个变量（可修改），或者是一个常量（不可修改）

```
  var variableString = "Horse"
  variableString += " and carriage"
  // variableString is now "Horse and carriage

  let constantString = "Highlander"
  constantString += " and another Highlander"
  //this reports a compile-time error - a constant string cannot be modified
```

  可以通过 类型 NSString 和 NSMutableString 来定义字符串是否可以被修改。

#### 字符串值类型（Value Types）:

  当你创建一个新的字符串值，把它传给一个函数或方法时，或者当它被分配给一个常量或变量时，这个字符串会被复制。在以上情况下，都会创建一个现有字符串值的对象，并传递或分配新对象，而不是之前的对象。值类型在结构中描述，枚举类型为值类型。

  Swift 默认字符串确保当一个函数或方法传递给你一个字符串值时，你可以确信这个值不会被修改，除了你自己去修改它。Swift 的编译器优化了字符串的使用，必要时进行深拷贝。这就保证在使用字符串作为值类型时，性能会更好一些。

#### 通过循环遍历字符串来输出单个字符的值：

  ```
  for character in "Dog" {
      print(character)
  }
  ```

  又或者单个字符串创建字符串常量或变量:

  ```
  let exclamationMark: Character = "1"
  ```

  传递一个字符值数组来当字符串值初始值的参数创建:

  ```
  let catCharacters: [Character] = ["C", "a", "t", "!", "🐱"]
  let catString = String(catCharacters)
  ```

  可以将字符串值用” + “连接创建一个新的字符串值：

  ```
  let string1 = "hello"
  let string2 = " there"
  var welcome = string1 + string2
  ```

  或者利用 ”+=“ 来把值加到现有的字符串中:

  ```
  var instruction = "look over"
  instruction += string2
  ```

  使用 String 类型的 append() 方法也可以将字符值追加到字符串变量:

  ```
  let exclamationMark: Character = "!"
  welcome.append(exclamationMark)
  ```

  注意：不能将字符串或字符加到现有的字符变量中，因为字符值只包含一个字符 !!!

  想让多行字符串文本构建更长的字符串行，并且希望符串中的每一行都以换行符结束，包括最后一行：

  ```
  let badStart = """
  one
  two
  """
  let end = """
  three
  """
  print(badStart + end)
  /*
   one
   twothree
   */

  let goodStart = """
  one
  two

  """
  print(goodStart + end)
  /*
   one
   two
   three
  */
  ```

### 字符串插值

  在单行或多行字符串文本中使用字符串插值，在其中插入的每一项都包在括号中，由反斜杠（\）前缀。这是一种从常量、变量、文字和表达式混合中构造一个新的字符串值的方法:

  ```
  let multiplier = 3
  let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
  ```

  注意：
  被插入的字符串括号内不能包含未转义的反斜杠（\）、回车或换行，可以包含其他字符串文本。

#### Unicode

  Unicode是一种国际标准，用于在不同的书写系统中编码、表示和处理文本。它使您能够从任何语言中以标准化的形式表示几乎任何字符，并从外部源(如文本文件或web页面)读取和写入这些字符。Swift的字符串和字符类型完全符合unicode。

#### Unicode标量

  Swift 原生字符串类型是有 Unicode 标量值创建的。Unicode 标量是一个字符或修饰语的唯一21位“数字”，例如拉丁语小写字母A(“A”)的U+0061。Unicode 标量是在U+0000到U+D7FF的范围内的任何Unicode编码点

  请注意，并不是所有的21位Unicode标量都被分配给一个字符，一些标量是为将来的赋值预留的。被分配给一个角色的标量通常也有一个名字，比如上面例子中的拉丁字母a或者表情。

#### 扩展字母集（Extended Grapheme Clusters）

   Swift 的字符类型的每个实例都表示一个扩展的 字母集。可扩展的字母集是一个或多个 Unicode 标量的序列(当组合起来时)产生一个人可读的字符。比如:

  ```
  let eAcute: Character = "\u{E9}"    
  let combinedEAcute: Character = "\u{65}\u{301}"
  ```

   从输出可以看出来结果是一样的。第一种是单一的 Unicode 标量e （U+00E9）第二种是一对标量 小写字母e（U+0065） + 重音标量（U+0301）组合。

  扩展字母集是一种灵活的方式，可将复杂的脚本字符表示为单个字符值。例如 韩语字母表中的韩语音节可以被表示成一个预先组成的或分解的序列。这两种表述都符合Swift的单个字符值:

  ```
  let precomposed: Character = "\u{D55C}"
  let decomposed: Character = "\u{1112}\u{1161}\u{11AB}"
  ```

  扩展的字符集标量也可以用来封装标记，将其他 Unicode 标量作为单个字符值的一部分括起来：

  ```
  let enclosedEAcute: Character = "\u{E9}\u{20DD}"
  ```

  区域符号 Unicode 标量也可以组合成对出现组成单个字符值：

  ```
  let regionalIndicatorForUS: Character = "\u{1F1FA}\u{1F1F8}"
  ```

### 计数字符

  检索字符串中字符值的计算（count 属性）

  ```
  let unusualMenagerie = "Koala 🐨, Snail 🐌, Penguin 🐧, Dromedary 🐪"
  print("unusualMenagerie has \(unusualMenagerie.count) characters")
  ```

  如果在字符值使用扩展字符集，字符串连接和修改可能并不会影响字符串的字符计算，例如下面将重音标量加到字符串末尾，字符计数并没有改变：

  ```
  var word = "cafe"
  print("the number of characters in \(word) is \(word.count)")
  word += "\u{301}"
  print("the number of characters in \(word) is \(word.count)")
  ```

 注意：
count属性必须遍历整个字符串中的Unicode标量，以确定该字符串的字符。因为扩展的字符集可以由多个 Unicode 标量组成。不同的字符、相同字符的不同表示，可能需要不同的内存存储。count属性返回的字符的计数并不总是与包含相同字符的NSString的length属性相同。NSString的长度基于字符串中UTF-16表示的16位代码单元的数量，而不是字符串中Unicode扩展字符集的数量。

### 访问和修改字符串

  通过方法、属性、下标语法访问和修改一个字符串。

  每个字符串值都有一个关联的索引类型，字符串。索引，它对应于字符串中每个字符的位置。

  不同的字符可以要求不同的内存存储，因此为了确定哪个字符处于特定的位置，您必须从该字符串的开始或结束迭代每个Unicode标量。由于这个原因，Swift字符串不能按整数值进行索引。

  用startIndex属性访问字符串的第一个字符的位置。endIndex属性是字符串中最后一个字符后的位置。因此，endIndex属性对于字符串的下标不是有效的参数。如果一个字符串是空的，那么startIndex和endIndex是相等的。

  ```
  let greeting = "Guten Tag!"
  greeting[greeting.startIndex]
  // G
  print(greeting[greeting.startIndex])
  greeting[greeting.index(before: greeting.endIndex)]
  // !
   print(greeting[greeting.index(before: greeting.endIndex)])
  greeting[greeting.index(after: greeting.startIndex)]
  // u
   print(greeting[greeting.index(after: greeting.startIndex)])
  let index = greeting.index(greeting.startIndex, offsetBy: 7)
  greeting[index]
  // a”
   print(greeting[index])
  ```

  访问字符串范围外的索引或在字符串范围外的索引访问一个字符或报错！

  ```
  let greeting = ""
  greeting[greeting.endIndex] // Error
  greeting.index(after: greeting.endIndex) // Error”
  ```

  使用索引访问字符串中单个字符的所有索引：

  ```
  let greeting = "Dog is !"
  for index in greeting.indices {
      print("\(greeting[index]) ", terminator: "")
  }
  ```

 注意:
您可以使用startIndex和endIndex属性和索引(before:)、索引(after:)和索引(_:offsetBy:)方法对任何符合集合协议的类型的方法。(字符串、集合类型：数组、字典和集合)。

### 字符串插入及删除

  将单个字符插入到指定位置的字符串中:insert(_:at:)

  在指定的索引中插入另外一个字符串的内容：inset(contentsOf:at:）

  ```
  var welcome:String = "hello"
  welcome.insert("!", at: welcome.endIndex)
  print(welcome)
  // welcome now equals "hello!"
  welcome.insert(contentsOf: " there", at: welcome.index(before: welcome.endIndex))
  print(welcome)
  // welcome now equals "hello there!”
  ```

  从指定索引中的字符串删除单个字符，使用 remove(at:)

  指定范围内删除子字符串，使用 removeSubrange(_:)

  ```
  var welcome = "hello there!"
  welcome.remove(at: welcome.index(before: welcome.endIndex))
  // welcome now equals "hello there"

  let range = welcome.index(welcome.endIndex, offsetBy: -6)..<welcome.endIndex
  welcome.removeSubrange(range)
  // welcome now equals "hello”
  ```

### 子字符串

  从字符串获取子字符串的实例，然后用方法处理子字符串，可以短时间使用子字符串，如果想长时间使用就需要把子字符串转化为字符串实例。例如：

  ```
  let greeting = "Hello, world!"
  let index = greeting.index(of: ",") ?? greeting.endIndex
  let beginning = greeting[..<index]
  // beginning is "Hello"
  print(beginning)
  // Convert the result to a String for long-term storage.
  let newString = String(beginning)
  print(newString)
  ```

  跟字符串一样，每个子字符串都有一个内存区域，组成子字符串的字符被存储其中。字符串和子字符串之间的区别是，作为性能优化，子字符串可以重用用于存储原始字符串的部分内存，或者用于存储另一个子字符串的部分内存。(字符串有类似的优化，但是如果两个字符串共享内存，它们是相等的。)意味着，在修改字符串或子字符串之前，不必担心会有复制内存的性能成本。子字符串不适合长期存储，因为它们重用原始字符串的存储，只要使用它的任何子字符串，就必须将整个原始字符串保存在内存中。

  在上面的示例中，greeting是一个字符串，这意味着它有一个内存区域，其中组成字符串的字符被存储在其中。因为开始是一种问候的子串，它重新使用了问候使用的记忆。相反，newString是一个字符串，当它从子字符串创建时，它有自己的存储。下图显示了这些关系:

  ![](http://ww1.sinaimg.cn/large/006hs9KEgy1frqvn9884kj30ow0i4js3.jpg)

  ​

注意:
字符串和子字符串都符合StringProtocol协议，字符串处理函数通常接受StringProtocol值。您可以使用字符串或子字符串值调用这些函数。

### 字符串的比较

  Swift 提供了三种方法比较：符串和字符相等、前缀相等和后缀相等。

  字符串和字符串使用 相等(==) 和 不相等(!=)进行比较：

  ```
  let quotation = "We're a lot alike, you and I."
  let sameQuotation = "We're a lot alike, you and I."
  if quotation == sameQuotation {
      print("These two strings are considered equal")
  }
  // Prints "These two strings are considered equal 
  ```

  两个字符串值相等，如果他们的扩展字符集等同（具有相同的语言意义和外形），那么它们也是相等的。

  ```
  // "Voulez-vous un café?" using LATIN SMALL LETTER E WITH ACUTE
  let eAcuteQuestion = "Voulez-vous un caf\u{E9}?"
  // "Voulez-vous un café?" using LATIN SMALL LETTER E and COMBINING ACUTE ACCENT
  let combinedEAcuteQuestion = "Voulez-vous un caf\u{65}\u{301}?"
  if eAcuteQuestion == combinedEAcuteQuestion {
      print("These two strings are considered equal")
  }
  // Prints "These two strings are considered equal
  ```

  但是、英语的字母A 并不等于西里尔字母A，尽管在视觉上相似，但是没有相同的语言含义:

  ```
  let latinCapitalLetterA: Character = "\u{41}"
  let cyrillicCapitalLetterA: Character = "\u{0410}"
  if latinCapitalLetterA != cyrillicCapitalLetterA {
      print("These two characters are not equivalent.")
  }
  // Prints "These two characters are not equivalent.
  ```

注意：
在 Swift 中，字符串和字符并不区分低于（not locale-sensitive）

### 检查前后缀是否相等

  要检查字符串是否具有特定的字符串前缀或后缀，请调用字符串的hasPrefix(_:)和hasSuffix(_:)方法，这两种方法都接受一个字符串类型的参数并返回一个布尔值。

  使用 hasPrefix(_:) 方法计算出第1幕场景的数量：

  ```
  let romeoAndJuliet = [
      "Act 1 Scene 1: Verona, A public place",
      "Act 1 Scene 2: Capulet's mansion",
      "Act 1 Scene 3: A room in Capulet's mansion",
      "Act 1 Scene 4: A street outside Capulet's mansion",
      "Act 1 Scene 5: The Great Hall in Capulet's mansion",
      "Act 2 Scene 1: Outside Capulet's mansion",
      "Act 2 Scene 2: Capulet's orchard",
      "Act 2 Scene 3: Outside Friar Lawrence's cell",
      "Act 2 Scene 4: A street in Verona",
      "Act 2 Scene 5: Capulet's mansion",
      "Act 2 Scene 6: Friar Lawrence's cell"
  ]
  var act1SceneCount = 0
  for scene in romeoAndJuliet {
      if scene.hasPrefix("Act 1 ") {
          act1SceneCount += 1
      }
  }
  print("There are \(act1SceneCount) scenes in Act 1")
  // Prints "There are 5 scenes in Act 1
  ```

  使用hasSuffix(_:)方法计算 Capulet's mansion 和 Friar Lawrence's cell 数量

  ```
  var mansionCount = 0
  var cellCount = 0
  for scene in romeoAndJuliet {
      if scene.hasSuffix("Capulet's mansion") {
          mansionCount += 1
      } else if scene.hasSuffix("Friar Lawrence's cell") {
          cellCount += 1
      }
  }
  print("\(mansionCount) mansion scenes; \(cellCount) cell scenes")
  // Prints "6 mansion scenes; 2 cell scenes
  ```

### Unicode 字符串展示

  将 Unicode 字符串写入文本或存储时，该字符串中的 Unicode 标量会存在这个 Unicode 定义的编码表单中。字符串会被编码成小块，称为代码单元。UTF-8编码格式(它将字符串编码为8位代码单元)、UTF-16编码格式(将字符串编码为16位代码单元)和UTF-32编码表单(将字符串编码为32位代码单元)。

  Swift 提供了几种方式来访问字符串的 Unicode。可以使用 for in 遍历字符串，访问它的单个字符值作为 Unicode 扩展字符集。

  另外一种方法，在符合三个条件的 unicode 中，访问一个字符串值:

  - UTF-8代码单元的集合(用字符串的utf8属性访问)
  - UTF-16代码单元的集合(使用字符串的utf16属性访问)
  - 一个21位的 Unicode标 量值集合，等价于字符串的UTF-32编码表单(使用字符串的unicodeScalars属性访问)

  举个例子: 

  ```
  let dogString = "Dog‼🐶"
  ```

  上面的字符串是由 Dog + 感叹号(Unicode 标量U+203C) + 🐶字符(Unicode 标量U+1F436)

#### UTF-8 展示

  通过遍历 UTF-8 属性来访问字符串的 UTF-8 展示。属性是 String 类型，视图如下:

  ![](http://ww1.sinaimg.cn/large/006hs9KEgy1frr34f1bhlj30he0a0wey.jpg)

  ```
  let dogString = "Dog‼🐶"
  for codeUnit in dogString.utf8 {
      print("\(codeUnit) ", terminator: "")
  }
  print("")
  // Prints "68 111 103 226 128 188 240 159 144 182
  ```

  解释：前三个十进制码单元值（68 111 103）表示字符D、o和g，它们的 UTF-8 表示与它们的 ASCII 表示相同。接下来的三个十进制代码单元值(226,128,188)是一个3字节的 UTF-8 表示双感叹号字符。最后四个 codeUnit 值(240、159、144、182)是 DOG FACE 字符的4字节 UTF-8 表示。

#### UTF-16 展示

  通过遍历 UTF-16 属性来访问字符串的 UTF-16 展示。属性是 String 类型，视图如下:

  ![](http://ww1.sinaimg.cn/large/006hs9KEgy1frr3jkcj4mj30iw0a474o.jpg)

  ```
  let dogString = "Dog‼🐶"
  for codeUnit in dogString.utf16 {
      print("\(codeUnit) ", terminator: "")
  }
  print("")
  // Prints "68 111 103 8252 55357 56374
  ```

  同样，前三个codeUnit值(68、111、103)表示字符D、o和g，其UTF-16代码单元的值与字符串的UTF-8表示相同(因为这些Unicode标量表示ASCII字符)。

  第四个codeUnit值(8252)是十六进制值203C的十进制等价物，它表示双感叹号字符的Unicode标量U+203C。该字符可以表示为UTF-16中的单个代码单元。

  第五个和第6个codeUnit值(55357和56374)是一个UTF-16代理对狗脸字符的表示。这些值是U+D83D (decimal值55357)的高代理值，以及U+DC36 (decimal值56374)的一个低代理值。

#### Unicode 标量表示

  遍历 unicodeScalars 属性，访问字符串值的 Unicode 标量。

  ![](http://ww1.sinaimg.cn/large/006hs9KEgy1frr3ru8i9yj30i20a40t6.jpg)

  ```
  let dogString = "Dog‼🐶"
  for scalar in dogString.unicodeScalars {
      print("\(scalar.value) ", terminator: "")
  }
  print("")
  // Prints "68 111 103 8252 128054
  ```

  前三个UnicodeScalar值(68、111、103)的值属性再次表示字符D、o和g。

  第四个codeUnit值(8252)又相当于十六进制值203C，它表示双感叹号字符的Unicode标量U+203C。

  第五个和最后一个UnicodeScalar(128054)的值属性是一个十进制等价的十六进制值1F436，它代表了狗脸字符的Unicode标量U+1F436。

  除了查询其值属性之外，还可以使用每个UnicodeScalar值来构造一个新的字符串值，比如字符串插值:

  ```
  let dogString = "Dog‼🐶"
  for scalar in dogString.unicodeScalars {
      print("\(scalar) ")
  }
  // D
  // o
  // g
  // ‼
  // 🐶
  ```
  
  更多swift4.1翻译请查看[github](https://github.com/iOSDevelopShareTeam/SwiftTourv4.1)。

QQ技术交流群：214541576 

微信公众号：shavekevin

开发者头条：![](http://ww1.sinaimg.cn/large/006mQyr2ly1fqgrkt5gurj30qo1bcq53.jpg)

热爱生活，分享快乐。好记性不如烂笔头。多写，多记，多实践，多思考。






  ​

