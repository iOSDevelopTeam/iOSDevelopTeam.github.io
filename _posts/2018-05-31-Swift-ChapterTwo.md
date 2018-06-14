---
layout:     post
title:      Swift4.1翻译
subtitle:   第二章
date:       2018-05-31
author:     BeyoundCong
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - iOS
    - 翻译
    - Swift
---
# 字符串和字符

-  字符串就是由一系列的字符组成，例如：“hello，world”或者“albatross”。

   Swift 中的字符串由 String 表示。字符串（包括 Character values ）可以以多种方式访问。

-  Swift 的字符串和字符类型提供了一种快速、符合 Unicode 的方法，可以在代码中使用文本。字符串的语法创建和操作容易，可读性强。可以使用字符串将常量、变量、文字和表达式插入到更长的字符串，这样不论是显示、存储和打印一些特定的字符串值会更加容易。

-  注意：

   Swift 的字符串类型与 Foundation 的 NSString 类连接。Foundation 还扩展了字符串，以暴露由 NSString 定义的方法。如果您导入 Foundation，您就可以在没有选择的情况下访问那些 NSString 方法。

   ```
   let string:String = "hello";
   let otherString:NSString = "world";
   print(string + (otherString as String));
   ```

-  使用字符串字面量作为常量或变量的初始值:

   ```
   let someString = "Some string literal value”
   ```

-  创建多行字符串:（不会以换行符开头或结尾）

   ```
   let quotation = """
   The White Rabbit put on his spectacles.  "Where shall I begin,
   please your Majesty?" he asked.
    
   "Begin at the beginning," the King said gravely, "and go on
   till you come to the end; then stop.
   """
   ```

-  多行字符串中如果想使用换行符让源码更容易阅读，并且不希望换行符是字符串值的一部分，可以在这些行的末尾加一个反斜杠（\）:

   ```
   let someString = """
   “The White Rabbit put on his spectacles.  "Where shall I begin, \
   please your Majesty?" he asked.”
   “Begin at the beginning," the King said gravely, "and go on \
   till you come to the end; then stop.”
   """
   ```

-  让一个多行字符串字面意思开始或以一个行结束，写一个空行作为第一行或者最后一行:

   ```
   let someString = """

   “This string starts with a line break.
   It also ends with a line break.”

   """
   ```

-  多行字符串可以缩进匹配周围的代码。在结束引号(“”)之前的空格会告诉Swift在所有其他行之前忽略哪些空白。以下俩份代码可以运行对比一下输出

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

-  字符串中的特殊字符

   字符串值中可以包括以下特殊字符：

   > 转义符: 空字符\0、反斜杠 \\\ 、水平Tab \t、换行\n、回车\r、双引号\"和单引号\‘ 。一个任意的 Unicode 标量，写成\u{n}，其中 n 是一个 1-8位十六进制数字，其值就等于一个有效的 Unicode 编码点。例如：

  ```
  let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
  let dollarSign = "\u{24}"
  let blackHeart = "\u{2665}"
  let sparklingHeart = "\u{1F496}"
  ```

- 多行字符串文本使用了三个双引号而不是一个，所以在多行字符串字面上包含双引号（“），不需要转义。如果要在多行字符串中包含文本""，至少要对其中一个引号做处理。例如:

  ```
  let threeDoubleQuotationMarks = """
  Escaping the first quotation mark \"""
  Escaping all three quotation marks \"\"\"
  """
  ```

- 初始化一个空字符串:

  ```
  var emptyString = ""
  var anotherEmptyString = String()
  ```

- 检查字符串值以及 BOOL 属性是否为空

  ```
  var name = ""
  if name.isEmpty {
      print("Nothing to see here")
  }
  ```

- 字符串具有可变性：

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

- 字符串值类型（Value Types）:

  当你创建一个新的字符串值，把它传给一个函数或方法时，或者当它被分配给一个常量或变量时，这个字符串会被复制。在以上情况下，都会创建一个现有字符串值的对象，并传递或分配新对象，而不是之前的对象。值类型在结构中描述，枚举类型为值类型。

  Swift 默认字符串确保当一个函数或方法传递给你一个字符串值时，你可以确信这个值不会被修改，除了你自己去修改它。Swift 的编译器优化了字符串的使用，必要时进行深拷贝。这就保证在使用字符串作为值类型时，性能会更好一些。

- 通过循环遍历字符串来输出单个字符的值：

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

  #### 注意：不能将字符串或字符加到现有的字符变量中，因为字符值只包含一个字符 !!!

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

- 字符串插值

  在单行或多行字符串文本中使用字符串插值，在其中插入的每一项都包在括号中，由反斜杠（\）前缀。这是一种从常量、变量、文字和表达式混合中构造一个新的字符串值的方法:

  ```
  let multiplier = 3
  let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
  ```

  #### 注意：被插入的字符串括号内不能包含未转义的反斜杠（\）、回车或换行，可以包含其他字符串文本。

- Unicode

  Unicode是一种国际标准，用于在不同的书写系统中编码、表示和处理文本。它使您能够从任何语言中以标准化的形式表示几乎任何字符，并从外部源(如文本文件或web页面)读取和写入这些字符。Swift的字符串和字符类型完全符合unicode。

- Unicode标量

  Swift 原生字符串类型是有 Unicode 标量值创建的。Unicode 标量是一个字符或修饰语的唯一21位“数字”，例如拉丁语小写字母A(“A”)的U+0061。Unicode 标量是在U+0000到U+D7FF的范围内的任何Unicode编码点

  请注意，并不是所有的21位Unicode标量都被分配给一个字符，一些标量是为将来的赋值预留的。被分配给一个角色的标量通常也有一个名字，比如上面例子中的拉丁字母a或者表情。

- 扩展字母集（Extended Grapheme Clusters）

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

- 计数字符

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

  #### 注意：count属性必须遍历整个字符串中的Unicode标量，以确定该字符串的字符。因为扩展的字符集可以由多个 Unicode 标量组成。不同的字符、相同字符的不同表示，可能需要不同的内存存储。count属性返回的字符的计数并不总是与包含相同字符的NSString的length属性相同。NSString的长度基于字符串中UTF-16表示的16位代码单元的数量，而不是字符串中Unicode扩展字符集的数量。

- 访问和修改字符串

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

  #### 注意:您可以使用startIndex和endIndex属性和索引(before:)、索引(after:)和索引(_:offsetBy:)方法对任何符合集合协议的类型的方法。(字符串、集合类型：数组、字典和集合)。

- 字符串插入及删除

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

- 子字符串

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

  #### 注意:字符串和子字符串都符合StringProtocol协议，字符串处理函数通常接受StringProtocol值。您可以使用字符串或子字符串值调用这些函数。

- 字符串的比较

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

  #### 注意：在 Swift 中，字符串和字符并不区分低于（not locale-sensitive）

- 检查前后缀是否相等

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

- Unicode 字符串展示

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

- UTF-8 展示

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

- UTF-16 展示

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

- Unicode 标量表示

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

- 集合类型（Collection Types）

  Swift 提供了 三个 主要的集合类型：数组、集合和字典，用于存储值集合。数组是有序的值集合。集合是唯一值的无序集合。字典是键值关联的无序集合。

  ![](http://ww1.sinaimg.cn/large/006hs9KEgy1frr4nd4jppj30jm09wq3k.jpg)

  Swift中，数组、集合和字典对存储的值和键的类型都有要求，说明您不能错误的将错误类型的值插入集合中。

  #### 注意：Swift 的数组、集合和字典类型 实现被称为泛型集合。

- 可变集合

  创建的一个数组、一个集合或一个字典，然后分配给变量，这个创建的集合是可变的（可以添加、删除或更改）。

  创建的一个数组、一个集合或一个字典，然后分配给常量，这个创建的集合是不可变的（不可以添加、删除或更改）。

  #### 注意：如果不需要更改集合，最好创建不可变集合。这样方便对代码进行推理，Swift 编译器优化您创建的集合的性能。

- 数组（Arrays）

  数组在有序列表中存储相同类型的值。相同的值可以多次出现在不同位置的数组中。

  #### 注意：Swift 的数组类型可以桥接到 Objective-C 中的 NSArray 类。

- 数组类型的缩写语法（Array Type Shorthand Syntax）

  Swift 数组的类型是以 数组<元素> 的形式写入，元素就是数组允许存储的值类型。还可以将数组的类型以简写的形式 [元素] 编写。虽然这两种形式在功能上是相同的，但是在引用数组的类型时，使用了简写形式，是推荐使用的。

- 创建一个空数组

  可以用使用初始化语法创建特定类型的空数组

  ```
  var someInts = [Int]()
  print("someInts is of type [Int] with \(someInts.count) items.")
  // Prints "someInts is of type [Int] with 0 items.
  ```

  #### 注意：someInts 变量的类型推断为 [Int]

  如果已有类型信息，例如函数参数或已经输入的变量或常量，您可以创建一个空数组，其中包含一个空数组文本，可以写 一个空的方括号 []:

  ```
  var someInts = [Int]()
  someInts.append(3)
  // someInts now contains 1 value of type Int
  someInts = []
  // someInts is now an empty array, but is still of type [Int]
  ```

- 创建默认值的数组

  Swift的数组类型还提供了一个初始化器，用于创建特定大小的数组，并将其所有值设置为相同的默认值。

  ```
  var threeDoubles = Array(repeating: 0.0, count: 3)
  // threeDoubles is of type [Double], and equals [0.0, 0.0, 0.0]
  ```

- 两个数组相加创建一个新数组

  通过加法运算符（+）兼容类型的现有数组创建新数组。新数组的类型是从两个数组的类型中推断出来的。

  ```
  var threeDoubles = Array(repeating: 0.0, count: 3)
  // threeDoubles is of type [Double], and equals [0.0, 0.0, 0.0]

  var anotherThreeDoubles = Array(repeating: 2.5, count: 3)
  // anotherThreeDoubles is of type [Double], and equals [2.5, 2.5, 2.5]

  var sixDoubles = threeDoubles + anotherThreeDoubles
  // sixDoubles is inferred as [Double], and equals [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]
  ```

- 数组文字创建数组

  直接数组文本初始化数组，逗号分隔将一个或多个值作为数组集合写入的一种简写方式。

  > [value 1, value 2, value 3]

  ```
  var shoppingList: [String] = ["Eggs", "Milk"]
  // shoppingList has been initialized with two initial items
  ```

  shoppingList变量”被声明为“字符串值数组”，以[string]表示。因为这个特定的数组指定了字符串的值类型，所以只允许存储字符串值。然后用两个字符串值(“Eggs”和“Milk”)初始化。

  Swift 有类型推断，所以不必编写数组的类型。

  ```
  var shoppingList = ["Eggs", "Milk"]
  ```

  因为数组中所有的值类型相同的文字，Swift 可以推断 String 是用于 shoppingList 变量的类型。

- 访问和修改数组

  查找数组中的项数:

  ```
  print("The shopping list contains \(shoppingList.count) items.")
  // Prints "The shopping list contains 2 items.
  ```

  使用 isEmpty 检查 count 属性是否为0

  ```
  if shoppingList.isEmpty {
      print("The shopping list is empty.")
  } else {
      print("The shopping list is not empty.")
  }
  // Prints "The shopping list is not empty.
  ```

  通过 append 添加数据

  ``` 
  shoppingList.append("Flour")
  // shoppingList now contains 3 items, and someone is making pancakes
  ```

  或 通过 （+=）添加一个值类型相同的数据

  ```
  shoppingList += ["Baking Powder"]
  // shoppingList now contains 4 items
  shoppingList += ["Chocolate Spread", "Cheese", "Butter"]
  // shoppingList now contains 7 items
  ```

  通过在数组后面括号中添加索引获得想要的值

  ```
  var firstItem = shoppingList[0]
  // firstItem is equal to "Eggs
  ```

  #### 注意，数组中的第一线索引为0，不是1。注意数组越界问题

  使用索引修改值

  ```
  shoppingList[0] = "Six eggs"
  // the first item in the list is now equal to "Six eggs" rather than "Eggs
  ```

  通过长度范围修改值

  ```
  shoppingList[4...6] = ["Bananas", "Apples"]
  // shoppingList now contains 6 items
  ```

  指定索引插入值

  ```
  shoppingList.insert("Maple Syrup", at: 0)
  // shoppingList now contains 7 items
  // "Maple Syrup" is now the first item in the list
  ```

  使用 remove(at:) 删除值

  ```
  let mapleSyrup = shoppingList.remove(at: 0)
  // the item that was at index 0 has just been removed
  // shoppingList now contains 6 items, and no Maple Syrup
  // the mapleSyrup constant is now equal to the removed "Maple Syrup" string
  ```

  当一个参数被移除时，数组中的接口都会被关闭，因此索引为 0 的值又等于 "Six eggs"。

  ``` 
  firstItem = shoppingList[0]
  // firstItem is now equal to "Six eggs
  ```

  如果想删除数组的最后一项，要使用 removeLast() 方法，而不是 remove(at:)。避免查询数组的 count 属性。

  ```
  let apples = shoppingList.removeLast()
  // the last item in the array has just been removed
  // shoppingList now contains 5 items, and no apples
  // the apples constant is now equal to the removed "Apples" string
  ```

- 遍历数组

  for in 循环遍历数组中的值

  ```
  for item in shoppingList {
      print(item)
  }
  // Six eggs
  // Milk
  // Flour
  // Baking Powder
  // Bananas
  ```

  如果想知道每个参数的索引以及值，就使用 enumerated()  来遍历数组：

  ```
  for (index, value) in shoppingList.enumerated() {
      print("Item \(index + 1): \(value)")
  }
  // Item 1: Six eggs
  // Item 2: Milk
  // Item 3: Flour
  // Item 4: Baking Powder
  // Item 5: Bananas
  ```

- 集（Sets）

  没有定义排序的集合中，集合存储相同类型的不同值。如果参数的顺序不重要，或者需要确保只出现一次时，可以使用 set 而不是数组。

  #### 注意：Swift 的set 类型 桥接到 Foundation的 NSSet 类。

- 集合类型的 Hash 值

  类型提供了一种方法来计算自己的哈希值。哈希值是一个Int值，它对所有比较相同的对象都是相同的，例如，如果A == b，则该值为A。hashValue = = b.hashValue。

  Swift 的基本类型（例如字符串、Int、Double和Bool）默认状态是使用的，并且可以作为 set 类型或 dictionary 键类型使用。默认状态下，没有关联值的枚举实例值也是可以 hashable。

  如果要自己自定义类型来设置值类型或字典密钥类型。符合 Hashable 协议， 那么必须符合以下三个条件

  - a == a (Reflexivity)
  - a == b implies b == a (Symmetry)
  - a == b && b == c implies a == c (Transitivity)

- Set 类型的语法

  Swift 的类型是 set <Element>，元素是允许存储的类型。跟数组不一样，集合没有简写形式。

- 创建和初始化空集

  使用初始化语法创建一个特定类型的空集:

  ```
  var letters = Set<Character>()
  print("letters is of type Set<Character> with \(letters.count) items.")
  // Prints "letters is of type Set<Character> with 0 items.
  ```

  比如函数参数或输入的常量或变量已经提供了类型信息，那么可以使用空数组文本创建空集。

  ```
  letters.insert("a")
  // letters now contains 1 value of type Character
  letters = []
  // letters is now an empty set, but is still of type Set<Character>
  ```

- 用数组文字创建一个集合 

  用数组文本初始化一个集合，作为一个或多个值写入集合的简写方式。

  ```
  var favoriteGenres: Set<String> = ["Rock", "Classical", "Hip hop"]
  // favoriteGenres has been initialized with three initial items
  ```

  favoritetypes变量”被声明为“一组字符串值”，以set <String>的形式写入。这个集合的值类型就是 String，所以只允许存储字符串。

  集合类型不能从数组文字中推断出来类型，所以要显示声明值类型。但是，由于Swift的类型推断，如果您要用一个数组文字来初始化它，则不必编写set的类型。相同类型的值。最喜欢的类型的初始化可以用更短的形式写成:

  ```
  var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]
  ```

  因为数组中的值都是一样类型的，Swift 可以推断出 String 是正确的值类型。

- 访问和修改集合

  查找集合的项数：

  ```
  print("I have \(favoriteGenres.count) favorite music genres.")
  // Prints "I have 3 favorite music genres.
  ```

  使用 isEmpty 检查 count 属性是否为0 ：

  ```
  if favoriteGenres.isEmpty {
      print("As far as music goes, I'm not picky.")
  } else {
      print("I have particular music preferences.")
  }
  // Prints "I have particular music preferences.
  ```

  调用 Set 的 insert(_:) 方法添加新参数:

  ```
  favoriteGenres.insert("Jazz")
  // favoriteGenres now contains 4 items
  ```

  调用 Set 的 remove(_:) 删除一个值，如果值存在就被删除，不在就会返回 nil，使用 removeAll() 删除所有值。

  ```
  if let removedGenre = favoriteGenres.remove("Rock") {
      print("\(removedGenre)? I'm over it.")
  } else {
      print("I never much cared for that.")
  }
  // Prints "Rock? I'm over it.
  ```

  使用 contains(_:) 方法检查集合是否包含某个参数：

  ```
  if favoriteGenres.contains("Funk") {
      print("I get up on the good foot.")
  } else {
      print("It's too funky in here.")
  }
  // Prints "It's too funky in here.
  ```

- 遍历一个集合（Set）

  使用 for in 循环遍历集合中的值。

  ```
  for genre in favoriteGenres {
      print("\(genre)")
  }
  // Jazz
  // Hip hop
  // Classical
  ```

  使用 sorted() 可以对 Set 集合进行排序（Set 类型没有定义的排序）

  ```
  for genre in favoriteGenres.sorted() {
      print("\(genre)")
  }
  // Classical
  // Hip hop
  // Jazz
  ```

- 对 Set 集合一些操作

  可以用 Set 进行一些操作，比如将两个集合组合一起，确定两个集合是否具有相同的值，或是否有包含一些有的值，或没有的值。

  下图秒速了 两个 Set a 和 b，由阴影区域表示各种操作 Set 的结果：

  ![](http://ww1.sinaimg.cn/large/006hs9KEgy1frs8f4zt3nj30ky0gi3z6.jpg)

  - 使用 intersection(_:)  创建一个新的 Set 集合，只包含了两个集合中共有的值。
  - 使用 symmetricDifference(_:) 创建一个新的 Set 集合，去掉了两个集合共有的值。
  - 使用 union(_:) 创建一个新的 Set 集合，具有所有的值。
  - 使用 subtracting(_:) 创建一个新的 Set 集合，在原来集合里面去掉共有的值。

  ```
  let oddDigits: Set = [1, 3, 5, 7, 9]
  let evenDigits: Set = [0, 2, 4, 6, 8]
  let singleDigitPrimeNumbers: Set = [2, 3, 5, 7]
   
  oddDigits.union(evenDigits).sorted()
  // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
  oddDigits.intersection(evenDigits).sorted()
  // []
  oddDigits.subtracting(singleDigitPrimeNumbers).sorted()
  // [1, 9]
  oddDigits.symmetricDifference(singleDigitPrimeNumbers).sorted()
  // [1, 2, 9]
  ```

  ![](http://ww1.sinaimg.cn/large/006hs9KEgy1frs8pdgikfj30ke0g0t90.jpg)

  上图描述了 3个 集合 a 包含了 b，a 和 c 有部分共同的值，b 和 c 无关。

  - 使用 is equal 确定两个集合是否包含所有相同的值。
  - 使用 isSubset(of:) 来确定集合中的所有值是否包含在指定集合中。
  - 使用 isSuperset(of:) 来确定一个集合是否包含指定集合中的所有值。
  - 使用 isStrictSubset(of:) 或 isStrictSuperset(of:)  来确定集合是子集还是超级，但不等于指定的集合。
  - 使用 isDisjoint(with:) 来确定两个集合是否具有相同的值。

  ```
  let houseAnimals: Set = ["🐶", "🐱"]
  let farmAnimals: Set = ["🐮", "🐔", "🐑", "🐶", "🐱"]
  let cityAnimals: Set = ["🐦", "🐭"]
   
  houseAnimals.isSubset(of: farmAnimals)
  // true
  farmAnimals.isSuperset(of: houseAnimals)
  // true
  farmAnimals.isDisjoint(with: cityAnimals)
  // true
  ```

- 字典（Dictionaries）

  字典存储相同类型的键和相同类型的值之间的关联。与数组不同，字典中的值没有指定的顺序，需要根据键来找值。

  #### 注意：Swift 的 Dictionary 类型被桥接到 Foundation 的 NSDictionary 类中。

- 字典类型缩写语法

  Swift 字典（Dictionary）是完整的 Dictionary<Key, Value>，其中 Key 是可以用作字典键的值的类型，而 Value 是字典为这些键存储的值的类型。

  #### 注意: 字典的键类型必须符合 Hashable 的协议，就像 set 的值类型一样。

  也可以用简写的形式 [Key: Value]。

- 创建一个空的字典

  ```
  var namesOfIntegers = [Int: String]()
  // namesOfIntegers is an empty [Int: String] dictionary
  ```

  它的键是 Int 类型，值是 String 类型的。如果已经给了类型信息，可以再一个空字典字面量这样写:

  ```
  namesOfIntegers[16] = "sixteen"
  // namesOfIntegers now contains 1 key-value pair
  namesOfIntegers = [:]
  // namesOfIntegers is once again an empty dictionary of type [Int: String]
  ```

  还可以通过这样形式来创建字典 [key 1: value 1, key 2: value 2, key 3: value 3]

  ```
  var airports: [String: String] = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
  ```

  如果用字典文本初始化，就不必编写字典类型，而字典中的键和值具有一致的类型。就可以这样写：

  ```
  var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
  ```

- 访问和修改字典

  使用 count 属性检查字典的数量

  ```
  print("The airports dictionary contains \(airports.count) items.")
  // Prints "The airports dictionary contains 2 items.
  ```

  使用 isEmpty 属性检查 count 是否为0

  ```
  if airports.isEmpty {
      print("The airports dictionary is empty.")
  } else {
      print("The airports dictionary is not empty.")
  }
  // Prints "The airports dictionary is not empty.
  ```

  字典中添加新的值：

  ```
  airports["LHR"] = "London"
  // the airports dictionary now contains 3 items
  ```

  还可以修改值：

  ```
  airports["LHR"] = "London Heathrow"
  // the value for "LHR" has been changed to "London Heathrow
  ```

  可以使用 updateValue(_:forKey:) 来更新 Key 的值。这个可以检查是否发了更新，如果更新的值不存在会返回 nil。

  ```
  if let oldValue = airports.updateValue("Dublin Airport", forKey: "DUB") {
      print("The old value for DUB was \(oldValue).")
  }
  // Prints "The old value for DUB was Dublin.
  ```

  检索字典中是否包含某个值：

  ```
  if let airportName = airports["DUB"] {
      print("The name of the airport is \(airportName).")
  } else {
      print("That airport is not in the airports dictionary.")
  }
  // Prints "The name of the airport is Dublin Airport.
  ```

  删除某个值（在已知的情况下）

  ```
  airports["APL"] = "Apple International"
  // "Apple International" is not the real airport for APL, so delete it
  airports["APL"] = nil
  // APL has now been removed from the dictionary
  ```

  使用 removeValue(forKey:) 方法删除某个值，如果值存在就删除不存在就返回 nil。

  ```
  if let removedValue = airports.removeValue(forKey: "DUB") {
      print("The removed airport's name is \(removedValue).")
  } else {
      print("The airports dictionary does not contain a value for DUB.")
  }
  // Prints "The removed airport's name is Dublin Airport.
  ```

  使用 for in 循环遍历字典

  ```
  for (airportCode, airportName) in airports {
      print("\(airportCode): \(airportName)")
  }
  // YYZ: Toronto Pearson
  // LHR: London Heathrow
  ```

  通过访问 键/值 属性来检索 键/值 的集合

  ```
  for airportCode in airports.keys {
      print("Airport code: \(airportCode)")
  }
  // Airport code: YYZ
  // Airport code: LHR
   
  for airportName in airports.values {
      print("Airport name: \(airportName)")
  }
  // Airport name: Toronto Pearson
  // Airport name: London Heathrow
  ```

  可以创建个新数据来接收字典的 键/值 属性

  ```
  let airportCodes = [String](airports.keys)
  // airportCodes is ["YYZ", "LHR"]
   
  let airportNames = [String](airports.values)
  // airportNames is ["Toronto Pearson", "London Heathrow"]
  ```

  Swift 的字典类型也没有排序，所以在 键/值 属性上使用 sorted() 方法进行排序。

- 控制流（Control Flow）

  Swift 提供各种控制流语句。

  For in循环、break 之类的条件语句、switch 语句可以匹配不同的模式，包括区间匹配、元组和类型转换。switch case 中的匹配值可以绑定到临时常量或在 case 的主体中使用的变量，复杂匹配条件可以用 where 子句表示。

  ```
  let airportCodes = [String](airports.keys)
  // airportCodes is ["YYZ", "LHR"]
   
  let airportNames = [String](airports.values)
  // airportNames is ["Toronto Pearson", "London Heathrow"]
  ```

- For in 循环

  For in 循环一个数组

  ```
  let names = ["Anna", "Alex", "Brian", "Jack"]
  for name in names {
      print("Hello, \(name)!")
  }
  // Hello, Anna!
  // Hello, Alex!
  // Hello, Brian!
  // Hello, Jack!
  ```

  遍历字典来访问它的键值对，还可以把字典的键和值分解为常量：

  ```
  let numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
  for (animalName, legCount) in numberOfLegs {
      print("\(animalName)s have \(legCount) legs")
  }
  // ants have 6 legs
  // spiders have 8 legs
  // cats have 4 legs
  ```

  字典本质上是无序的，遍历它们并不能保证检索它们的顺序。

  使用 For in 循环与数值范围：

  ```
  for index in 1...5 {
      print("\(index) times 5 is \(index * 5)")
  }
  // 1 times 5 is 5
  // 2 times 5 is 10
  // 3 times 5 is 15
  // 4 times 5 is 20
  // 5 times 5 is 25
  ```

  上面例子中，index 是一个常量，它的值再每次迭代的开始自动设置，因此它被隐式地声明为包含在循环声明中，而不需要一个let声明关键字。

  如果您不需要从序列中获得每个值，则可以使用一个下划线代替变量名来忽略这些值。

  for 循环的次数用到了闭域操作符(…)。只包含了一句语句。

  ```
  let base = 3
  let power = 10
  var answer = 1
  for _ in 1...power {
      answer *= base
  }
  print("\(base) to the power of \(power) is \(answer)")
  // Prints "3 to the power of 10 is 59049
  ```

  这个例子计算的 3 的 10 次方。它的起始值是1(也就是3的0次方)乘以3,10倍，使用一个从1开始，以10结束的闭区间。对于这种计算，每次通过循环的单个计数器值都是不必要的——代码只是执行循环的正确次数。在循环变量中使用的下划线字符(_)会导致单个值被忽略，并且在循环的每次迭代中不提供对当前值的访问。

  有些情况，可能不希望用到闭范围，包括两个端点。可以使用半开放的范围操作符(..<)来包含下界，但不包括上界。

  ```
  let minutes = 60
  for tickMark in 0..<minutes {
      // render the tick mark each minute (60 times)
  }
  ```

  有些希望用更少的标记，可以使用 stride(from:to:by:) 函数来跳过不需要的标记（5次一出现）。

  ```
  let minuteInterval = 5
  for tickMark in stride(from: 0, to: minutes, by: minuteInterval) {
      // render the tick mark every 5 minutes (0, 5, 10, 15 ... 45, 50, 55)
  }
  ```

  通过 stride(from:through:by:)  关闭范围。

  ```
  let hours = 12
  let hourInterval = 3
  for tickMark in stride(from: 3, through: hours, by: hourInterval) {
      // render the tick mark every 3 hours (3, 6, 9, 12)
  }
  ```

  上面的例子使用一个非常简单的方法来掷骰子。它不是生成一个随机数，而是从一个0的diceRoll值开始。每次通过while循环时，diceRoll都会增加一个，然后检查它是否变得太大。当这个返回值等于7时，骰子滚动变得太大，重置为1的值。结果是一系列的diceRoll值，它们总是1、2、3、4、5、6、1、2等等。

  为了防止掷的骰子大于移动的范围，代码检查正方形是否小于板数组的count属性。如果square是有效的，则将存储在[square]中的值添加到当前的square值中，以将玩家向上或向下移动任何梯子或蛇。

  当前while循环执行结束，并且检查循环的条件，看看是否应该再次执行循环。如果玩家已经移动了或者超过了25的平方，循环的条件就会被计算为false，游戏结束。

  在这种情况下，while循环是合适的，因为在while循环开始时，游戏的长度不清楚。相反，循环会执行，直到满足特定条件为止。

- Repeat-While

  while循环的另一个变体，称为重复while循环，在考虑循环的条件之前，先通过循环块执行一个遍历。然后继续重复循环，直到条件为假为止。

  #### 注意：Swift 的 Repeat-While 与其他语言的 do-while 循环类似。

  ```
  repeat {
      statements
  } while condition
  ```

  还是蛇与梯子的例子，用 Repeat-While 写，finalSquare、board、square和diceRoll的值以与while循环完全相同的方式初始化。

  ```
  let finalSquare = 25
  var board = [Int](repeating: 0, count: finalSquare + 1)
  board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
  board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
  var square = 0
  var diceRoll = 0
  ```

  循环中的第一个动作是检查梯子或蛇。棋盘上没有梯子可以直接把玩家带到25号广场，所以不可能通过爬梯子来赢得比赛。因此，检查蛇或梯子作为回路中的第一个动作是安全的。

  在游戏开始时，玩家处于“零平方”状态。board[0]总是等于0，没有影响。

  ```
  repeat {
      // move up or down for a snake or ladder
      square += board[square]
      // roll the dice
      diceRoll += 1
      if diceRoll == 7 { diceRoll = 1 }
      // move by the rolled amount
      square += diceRoll
  } while square < finalSquare
  print("Game over!")
  ```

  在对蛇和梯子进行代码检查之后，骰子就会滚动，玩家就会被diceRoll方块向前移动。当前循环执行结束。

  循环的条件(while square < finalSquare)与以前相同，但这一次它不会被计算，直到第一次循环结束时为止。重复while循环的结构比前一个示例中的while循环更适合于此游戏。在重复while循环中，square += board[square]总是在循环结束后立即执行，而条件确认了square仍然在执行板上。这是为了防止数组越界。

- 条件语句（Conditional Statements）

  平常我们都要通过特定的条件来执行不同的代码。

  Swift 提供了两个代码中添加条件的方法 if 和switch 语句。通常，简单的条件就用 if 语句。复杂的就需要使用 switch 语句。

- If

  简单：在条件为真的时候执行一组语句。

  ```
  var temperatureInFahrenheit = 30
  if temperatureInFahrenheit <= 32 {
      print("It's very cold. Consider wearing a scarf.")
  }
  // Prints "It's very cold. Consider wearing a scarf.
  ```

  if 语句可以提供另一组语句，称为 else 子句，用于在 if 条件为 false 的情况下。这些语句由 else 关键字表示。

  ```
  temperatureInFahrenheit = 40
  if temperatureInFahrenheit <= 32 {
      print("It's very cold. Consider wearing a scarf.")
  } else {
      print("It's not that cold. Wear a t-shirt.")
  }
  // Prints "It's not that cold. Wear a t-shirt.
  ```

  也可以多个 if 语句组合在一起

  ```
  temperatureInFahrenheit = 90
  if temperatureInFahrenheit <= 32 {
      print("It's very cold. Consider wearing a scarf.")
  } else if temperatureInFahrenheit >= 86 {
      print("It's really warm. Don't forget to wear sunscreen.")
  } else {
      print("It's not that cold. Wear a t-shirt.")
  }
  // Prints "It's really warm. Don't forget to wear sunscreen.
  ```

  最后的else子句是可选的。

  ```
  temperatureInFahrenheit = 72
  if temperatureInFahrenheit <= 32 {
      print("It's very cold. Consider wearing a scarf.")
  } else if temperatureInFahrenheit >= 86 {
      print("It's really warm. Don't forget to wear sunscreen.")
  }
  ```

- Switch

  switch 语句是根据一个值，然后与几个可能出现的值匹配比较。然后，根据匹配成功的第一个模式，执行适当的代码块。switch 语句为响应多个可能状态的 if 语句提供了一种替代方法。

  ```
  switch some value to consider {
  case value 1:
      respond to value 1
  case value 2,
       value 3:
      respond to value 2 or 3
  default:
      otherwise, do something else
  }
  ```

  switch 里面 每个 case 都是代码执行的一个分支，每个 switch 语句必须是详细的。要考虑到可能会匹配的值。

  ```
  let someCharacter: Character = "z"
  switch someCharacter {
  case "a":
      print("The first letter of the alphabet")
  case "z":
      print("The last letter of the alphabet")
  default:
      print("Some other character")
  }
  // Prints "The last letter of the alphabet
  ```

- No Implicit Fallthrough

  与 C 和 Objective-C 中的switch语句相比，Swift的switch语句不会在每个case的底部出现，在默认情况下会进入下一个case。相反，当第一个匹配的switch case完成时，整个switch语句将完成它的执行，而不需要显式的break语句。这使得switch语句比在C语言中使用更安全，更容易使用，避免错误地执行多个switch case。

  #### 注意：虽然在Swift中不需要break，但是您可以使用break语句来匹配和忽略某个特定的情况，或者跳出当前条件语句。

  switch 必须包含一个可执行语句。因为第一个 case 是空的，所以下面的代码都是无效的。

  ```
  let anotherCharacter: Character = "a"
  switch anotherCharacter {
  case "a": // Invalid, the case has an empty body
  case "A":
      print("The letter A")
  default:
      print("Not the letter A")
  }
  // This will report a compile-time error.
  ```

  与 C 的 switch 不同，switch语句不匹配“a”和“A”，避免从一种情况到另一种情况的偶然故障，使代码更加安全和清晰。

  ```
  let anotherCharacter: Character = "a"
  switch anotherCharacter {
  case "a", "A":
      print("The letter A")
  default:
      print("Not the letter A")
  }
  // Prints "The letter A
  ```

- 间隔匹配（Interval Matching）

  可以对值检查是否在哪个区间存在：

  ```
  let approximateCount = 62
  let countedThings = "moons orbiting Saturn"
  let naturalCount: String
  switch approximateCount {
  case 0:
      naturalCount = "no"
  case 1..<5:
      naturalCount = "a few"
  case 5..<12:
      naturalCount = "several"
  case 12..<100:
      naturalCount = "dozens of"
  case 100..<1000:
      naturalCount = "hundreds of
  default:
      naturalCount = "many"
  }
  print("There are \(naturalCount) \(countedThings).")
  // Prints "There are dozens of moons orbiting Saturn.
  ```

- 元组（Tuples）

  使用元组在同一个switch语句中测试多个值。元组的每个元素都可以根据不同的值或值间隔进行测试。或者，使用下划线字符(_)，也称为通配符模式，以匹配任何可能的值。

  例子：使用一个(x, y)点，表示为一个简单的类型元组(Int, Int)，并将其分类在以示例为例的图上。

  ```
  let somePoint = (1, 1)
  switch somePoint {
  case (0, 0):
      print("\(somePoint) is at the origin")
  case (_, 0):
      print("\(somePoint) is on the x-axis")
  case (0, _):
      print("\(somePoint) is on the y-axis")
  case (-2...2, -2...2):
      print("\(somePoint) is inside the box")
  default:
      print("\(somePoint) is outside of the box")
  }
  // Prints "(1, 1) is inside the box
  ```

  ![](http://ww1.sinaimg.cn/large/006hs9KEgy1frth7xc4qpj30qi0jaq42.jpg)

  switch语句确定了在红色x轴上的原点(0,0)，在橙色y轴上，在以原点为中心的蓝色4乘4框内，或者在方框外。与C不同，Swift允许多个切换实例考虑相同的值或值。实际上，在这个例子中，点(0,0)可以匹配所有四个案例。但是，如果可能有多个匹配，则总是使用第一个匹配的实例。点(0,0)首先会匹配(0,0)，因此所有其他匹配的情况都将被忽略。

- 值绑定（Value Bindings）

  switch case可以将其匹配的值或值命名为临时常量或变量，方便使用。

  ```
  let anotherPoint = (2, 0)
  switch anotherPoint {
  case (let x, 0):
      print("on the x-axis with an x value of \(x)")
  case (0, let y):
      print("on the y-axis with a y value of \(y)")
  case let (x, y):
      print("somewhere else at (\(x), \(y))")
  }
  // Prints "on the x-axis with an x value of 2
  ```

  ![](http://ww1.sinaimg.cn/large/006hs9KEgy1frthfbwjxfj30o00jumy5.jpg)

  switch语句确定了这个点在红色x轴上，在橙色y轴上，或者在其他地方(在两个轴上)。

  第一种情况,(x,0),匹配任何点的y值0和分配点的x值暂时不变。

  第二种情况下,例(0,y)匹配任何点的x值0和分配点的y y值暂时不变。

  最后一种情况，case let (x, y)，声明了一个两个占位符常量的元组，它可以匹配任何值。因为另一个点总是两个值的元组，这个例子匹配所有可能的剩余值，所以不需要一个默认情况来使switch语句变得详细。

- Compound CasesWhere

  switch case可以使用where子句来检查附加条件。

  ```
  let yetAnotherPoint = (1, -1)
  switch yetAnotherPoint {
  case let (x, y) where x == y:
      print("(\(x), \(y)) is on the line x == y")
  case let (x, y) where x == -y:
      print("(\(x), \(y)) is on the line x == -y")
  case let (x, y):
      print("(\(x), \(y)) is just some arbitrary point")
  }
  // Prints "(1, -1) is on the line x == -y
  ```

  ![](http://ww1.sinaimg.cn/large/006hs9KEgy1frthn0erpwj30pg0j6dh3.jpg)

  只有当where子句的条件计算为true时，switch case才匹配当前值。与前面的例子一样，最终的案例匹配所有可能的剩余值，因此不需要使用默认的情况来彻底改变switch语句。

- Compound Cases

  匹配的值之间加逗号，可以多模式编写。

  ```
  let someCharacter: Character = "e"
  switch someCharacter {
  case "a", "e", "i", "o", "u":
      print("\(someCharacter) is a vowel")
  case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
       "n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
      print("\(someCharacter) is a consonant")
  default:
      print("\(someCharacter) is not a vowel or a consonant")
  }
  // Prints "e is a vowel
  ```

  还可以值绑定，确保无论多值匹配，总是能访问到被绑定的值：

  ```
  let stillAnotherPoint = (9, 0)
  switch stillAnotherPoint {
  case (let distance, 0), (0, let distance):
      print("On an axis, \(distance) from the origin")
  default:
      print("Not on an axis")
  }
  // Prints "On an axis, 9 from the origin
  ```

- 控制转移语句（Control Transfer Statements）

  将一段代码转移到另一段代码，改变执行代码的顺序。

  - continue
  - break
  - fallthrough
  - return
  - throw

- Continue

  Continue 语句就是告诉循环停止做的事情，并且在下一次迭代开始从头开始。没有完全退出循环。

  ```
  let puzzleInput = "great minds think alike"
  var puzzleOutput = ""
  let charactersToRemove: [Character] = ["a", "e", "i", "o", "u", " "]
  for character in puzzleInput {
      if charactersToRemove.contains(character) {
          continue
      } else {
          puzzleOutput.append(character)
      }
  }
  print(puzzleOutput)
  // Prints "grtmndsthnklk
  ```

- Break

  Break 语句会立马停止当前的循环语句。

  ``` 
  let numberSymbol: Character = "三"  // Chinese symbol for the number 3
  var possibleIntegerValue: Int?
  switch numberSymbol {
  case "1", "١", "一", "๑":
      possibleIntegerValue = 1
  case "2", "٢", "二", "๒":
      possibleIntegerValue = 2
  case "3", "٣", "三", "๓":
      possibleIntegerValue = 3
  case "4", "٤", "四", "๔":
      possibleIntegerValue = 4
  default:
      break
  }
  if let integerValue = possibleIntegerValue {
      print("The integer value of \(numberSymbol) is \(integerValue).")
  } else {
      print("An integer value could not be found for \(numberSymbol).")
  }
  // Prints "The integer value of 三 is 3.
  ```

- Fallthrough

  在 switch 中加入 Fallthrough 就像 C 中加入 break 一样，防止出现以外的错误。如果加了 fallthrough 那么不论是否进入了 case ，default 后的语句都会执行。

  ```
  let integerToDescribe = 5
  var description = "The number \(integerToDescribe) is"
  switch integerToDescribe {
  case 2, 3, 5, 7, 11, 13, 17, 19:
      description += " a prime number, and also"
      fallthrough
  default:
      description += " an integer."
  }
  print(description)
  // Prints "The number 5 is a prime number, and also an integer.
  ```

- 标记（Labeled Statements）

  可以使用语句标签标记一个循环语句或条件语句。使用条件语句，您可以使用语句标签和break语句来结束标记语句的执行。使用循环语句，您可以使用带有break或continue语句的语句标签来结束或继续执行标记语句。

  ```
  label name: while condition {
      statements
  }
  ```

- 提前退出（Early Exit）

  保护语句，根据表达式的布尔值执行语句。用一个保护语句来要求在执行保护语句之后的代码是正确的。如果条件不正确，else 语句就会执行。

  ```
  func greet(person: [String: String]) {
      guard let name = person["name"] else {
          return
      }
      
      print("Hello \(name)!")
      
      guard let location = person["location"] else {
          print("I hope the weather is nice near you.")
          return
      }
      
      print("I hope the weather is nice in \(location).")
  }
   
  greet(person: ["name": "John"])
  // Prints "Hello John!"
  // Prints "I hope the weather is nice near you."
  greet(person: ["name": "Jane", "location": "Cupertino"])
  // Prints "Hello Jane!"
  // Prints "I hope the weather is nice in Cupertino.
  ```

  使用保护语句提高您的代码的可读性。

- 检查API可用性（Checking API Availability）

  Swift内置了检查API可用性的方法，确保不会使用不存在的API。

  ```
  if #available(iOS 10, macOS 10.12, *) {
      // Use iOS 10 APIs on iOS, and use macOS 10.12 APIs on macOS
  } else {
      // Fall back to earlier iOS and macOS APIs
  }
  ```

  ```
  if #available(platform name version, ..., *) {
      statements to execute if the APIs are available
  } else {
      fallback statements to execute if the APIs are unavailable
  }
  ```

  ​

