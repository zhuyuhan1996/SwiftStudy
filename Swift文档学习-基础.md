## 简介

Swift 包含了 C 和 Objective-C 上所有基础数据类型，`Int`表示整型值； `Double` 和 `Float` 表示浮点型值； `Bool`是布尔型值；`String` 是文本型数据。 Swift 还提供了三个基本的集合类型，`Array` ，`Set` 和 `Dictionary` 

除了我们熟悉的类型，Swift 还增加了 Objective-C 中没有的高阶数据类型比如元组（Tuple）。元组可以让你创建或者传递一组数据，比如作为函数的返回值时，你可以用一个元组可以返回多个值。

Swift 还增加了可选（Optional）类型，用于处理值缺失的情况。可选表示 “那儿有一个值，并且它等于 *x* ” 或者 “那儿没有值” 。可选有点像在 Objective-C 中使用 `nil` ，但是它可以用在任何类型上，不仅仅是类。可选类型比 Objective-C 中的 `nil` 指针更加安全也更具表现力，它是 Swift 许多强大特性的重要组成部分。

Swift 是一门*类型安全*的语言，这意味着 Swift 可以让你清楚地知道值的类型。如果你的代码需要一个 `String` ，类型安全会阻止你不小心传入一个 `Int` 。同样的，如果你的代码需要一个 `String`，类型安全会阻止你意外传入一个可选的 `String` 。类型安全可以帮助你在开发阶段尽早发现并修正错误。

## 基础部分

### 常量和变量

*常量*的值一旦设定就不能改变，而*变量*的值可以随意更改。

#### 声明

常量和变量必须在使用前声明，用 `let` 来声明常量，用 `var` 来声明变量。下面的例子展示了如何用常量和变量来记录用户尝试登录的次数：

```swift
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0
var x = 0.0, y = 0.0, z = 0.0
```

#### 类型标注

如果要添加类型标注，需要在常量或者变量名后面加上一个冒号和空格，然后加上类型名称

```swift
var welcomeMessage: String
var red, green, blue: Double
```

> 注意：
> 一般来说你很少需要写类型标注。如果你在声明常量或者变量的时候赋了一个初始值，Swift可以推断出这个常量或者变量的类型，请参考[类型安全和类型推断](http://www.swift51.com/swift4.0/chapter2/01_The_Basics.html#type_safety_and_type_inference)。在上面的例子中，没有给 `welcomeMessage` 赋初始值，所以变量 `welcomeMessage` 的类型是通过一个类型标注指定的，而不是通过初始值推断的

#### 命名

常量与变量名不能包含数学符号，箭头，保留的（或者非法的）Unicode 码位，连线与制表符。也不能以数字开头，但是可以在常量与变量名的其他地方包含数字。

#### 打印

```swift
var friendlyWelcome = "Bonjour!"
print("The current value of friendlyWelcome is \(friendlyWelcome)")
// 输出 "The current value of friendlyWelcome is Bonjour!
```

#### 注释

```swift
// 这是一个注释
/* 这是一个, 多行注释 */
/* 这是第一个多行注释的开头 /* 这是第二个被嵌套的多行注释 */ 这是第一个多行注释的结尾 */
```

#### 分号

与其他大部分编程语言不同，Swift 并不强制要求你在每条语句的结尾处使用分号（`;`），当然，你也可以按照你自己的习惯添加分号。有一种情况下必须要用分号，即你打算在同一行内写多条独立的语句：

```swift
let cat = "🐱"; print(cat)
// 输出 "🐱"
```

### 整数

- swift提供了8，16，32，64位有符号和无符号整数类型，

  ```swift
  let i: UInt8 = 8
  let j: Int32 = 32	
  ```

- 整数范围

  ```swift
  let minValue = UInt8.min  // minValue 为 0，是 UInt8 类型
  let maxValue = UInt8.max  // maxValue 为 255，是 UInt8 类型
  ```

- Int

  一般来说不需要指定整数的长度，Int长度跟当前平台原生字长相同，32位平台上，Int和Int32长度相同，64位平台上，Int与Int64长度相同

- UInt 跟Int一样，相对应的数据为UInt32，UInt64

### 浮点数

Double表示64位浮点数，需要存储很大或者很高精度的浮点数时使用此类型

Float表示32位浮点数，精度要求不高可以使用此类型

	`			Double`精确度很高，至少有15位数字，而`Float`只有6位数字。

### 类型安全和类型推断

Swift 是一个*类型安全（type safe）*的语言。类型安全的语言可以让你清楚地知道代码要处理的值的类型。如	果你的代码需要一个`String`，你绝对不可能不小心传进去一个`Int`。它会在编译你的代码时进行*类型检查	（type checks）*，并把不匹配的类型标记为错误

类型推断就是根据赋值字面量的类型推断常量或变量的类型	

```swift
let meaningOfLife = 42
// meaningOfLife 会被推测为 Int 类型
```

同理，如果你没有给浮点字面量标明类型，Swift 会推断你想要的是 `Double`：

```swift
let pi = 3.14159
// pi 会被推测为 Double 类型
```

当推断浮点数的类型时，Swift 总是会选择 `Double` 而不是`Float`。

### 数值类型转换

如果数字超出了常量或者变量可存储的范围，编译的时候会报错：

```swift
let cannotBeNegative: UInt8 = -1
// UInt8 类型不能存储负数，所以会报错
let tooBig: Int8 = Int8.max + 1
// Int8 类型不能存储超过最大值的数，所以会报错
```

在下面的例子中，常量`twoThousand`是`UInt16`类型，然而常量`one`是`UInt8`类型。它们不能直接相加，因为它们类型不同。所以要调用`UInt16(one)`来创建一个新的`UInt16`数字并用`one`的值来初始化，然后使用这个新数字来计算：

```swift
let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
```

### 整数和浮点数转换

整数和浮点数的转换必须显式指定类型：

```swift
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
// pi 等于 3.14159，所以被推测为 Double 类型
```

这个例子中，常量 `three` 的值被用来创建一个 `Double` 类型的值，所以加号两边的数类型须相同。如果不进行转换，两者无法相加。

浮点数到整数的反向转换同样行，整数类型可以用 `Double` 或者 `Float` 类型来初始化：

```swift
let integerPi = Int(pi)
// integerPi 等于 3，所以被推测为 Int 类型
```

当用这种方式来初始化一个新的整数值时，浮点值会被截断。也就是说 `4.75` 会变成 `4`，`-3.9` 会变成 `-3`。

### 布尔值

Swift 有一个基本的*布尔（Boolean）类型*，叫做`Bool`。布尔值指*逻辑*上的值，因为它们只能是真或者假。Swift 有两个布尔常量，`true` 和 `false`：

### 元组

*元组（tuples）*把多个值组合成一个复合值。元组内的值可以是任意类型，并不要求是相同类型。

```swift
let http404Error = (404, "Not Found")
// http404Error 的类型是 (Int, String)，值是 (404, "Not Found")

let (statusCode, statusMessage) = http404Error

let (justTheStatusCode, _) = http404Error

print("The status code is \(http404Error.0)")
// 输出 "The status code is 404"
print("The status message is \(http404Error.1)")
// 输出 "The status message is Not Found"
```

你可以在定义元组的时候给单个元素命名：

```swift
let http200Status = (statusCode: 200, description: "OK")
print("The status code is \(http200Status.statusCode)")
// 输出 "The status code is 200"
print("The status message is \(http200Status.description)")
// 输出 "The status message is OK"
```

### 可选类型

使用*可选类型（optionals）*来处理值可能缺失的情况。可选类型表示：

- 有值，等于 x

或者

- 没有值

```swift
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)
// convertedNumber 被推测为类型 "Int?"， 或者类型 "optional Int"
```

> Swift 的 `nil` 和 Objective-C 中的 `nil` 并不一样。在 Objective-C 中，`nil` 是一个指向不存在对象的指针。在 Swift 中，`nil` 不是指针——它是一个确定的值，用来表示值缺失。任何类型的可选状态都可以被设置为 `nil`，不只是对象类型。

### if 语句以及强制解析

你可以使用 `if` 语句和 `nil` 比较来判断一个可选值是否包含值。你可以使用“相等”(`==`)或“不等”(`!=`)来执行比较。

当你确定可选类型确实包含值之后，你可以在可选的名字后面加一个感叹号（`!`）来获取值。

```swift
if convertedNumber != nil {
    print("convertedNumber has an integer value of \(convertedNumber!).")
}
// 输出 "convertedNumber has an integer value of 123."
```

### 可选绑定

```swift
if let actualNumber = Int(possibleNumber) {
    print("\'\(possibleNumber)\' has an integer value of \(actualNumber)")
} else {
    print("\'\(possibleNumber)\' could not be converted to an integer")
}
// 输出 "'123' has an integer value of 123"
```

这段代码可以被理解为：

“如果 `Int(possibleNumber)` 返回的可选 `Int` 包含一个值，创建一个叫做 `actualNumber` 的新常量并将可选包含的值赋给它。”

如果转换成功，`actualNumber` 常量可以在 `if` 语句的第一个分支中使用。它已经被可选类型 *包含的* 值初始化过，所以不需要再使用 `!` 后缀来获取它的值。在这个例子中，`actualNumber` 只被用来输出转换结果。

### 隐式解析可选类型（隐式解包）

把想要用作可选的类型的后面的问号（`String?`）改成感叹号（`String!`）来声明一个隐式解析可选类型。

首先需要明确的是，隐式解包的 Optional 本质上与普通的 Optional 值并没有任何不同，只是我们在对这类变量的成员或方法进行访问的时候，编译器会自动为我们在后面插入解包符号 `!`，也就是说，对于一个隐式解包的下面的两种写法是等效的：

```swift
var maybeObject: MyClass! = MyClass()
maybeObject!.foo()
maybeObject.foo()
```

### 错误处理

当一个函数遇到错误条件，它能报错。调用函数的地方能抛出错误消息并合理处理。

```swift
func canThrowAnError() throws {
    // 这个函数有可能抛出错误
}
```

一个函数可以通过在声明中添加`throws`关键词来抛出错误消息。当你的函数能抛出错误消息时, 你应该在表达式中前置`try`关键词。

```swift
do {
    try canThrowAnError()
    // 没有错误消息抛出
} catch {
    // 有一个错误消息抛出
}
```

### 断言和先决条件

断言和先决条件是在运行时所做的检查，如果断言或者先决条件中的布尔条件评估的结果为 true（真），则代码像往常一样继续执行。如果布尔条件评估结果为false（假），程序的当前状态是无效的，则代码执行结束，应用程序中止。

断言仅在调试环境运行，而先决条件则在调试环境和生产环境中运行

### 使用断言进行调试

你可以调用 Swift 标准库的 `assert(_:_:file:line:)` 函数来写一个断言。向这个函数传入一个结果为 `true`或者 `false` 的表达式以及一条信息，当表达式的结果为 `false` 的时候这条信息会被显示：

```swift
let age = -3
assert(age >= 0, "A person's age cannot be less than zero")
// 因为 age < 0，所以断言会触发
```

如果不需要断言信息，可以就像这样忽略掉：

```swift
assert(age >= 0)
```

如果代码已经检查了条件，你可以使用 `assertionFailure(_:file:line:)`函数来表明断言失败了，例如：

```swift
if age > 10 {
    print("You can ride the roller-coaster or the ferris wheel.")
} else if age > 0 {
    print("You can ride the ferris wheel.")
} else {
    assertionFailure("A person's age can't be less than zero.")
}
```

### 强制执行先决条件

你可以使用全局 `precondition(_:_:file:line:)` 函数来写一个先决条件。向这个函数传入一个结果为 `true` 或者 `false` 的表达式以及一条信息，当表达式的结果为 `false` 的时候这条信息会被显示：

```swift
// 在一个下标的实现里...
precondition(index > 0, "Index must be greater than zero.")
```

> 你能使用 `fatalError(_:file:line:)`函数在设计原型和早期开发阶段，这个阶段只有方法的声明，但是没有具体实现，你可以在方法体中写上fatalError("Unimplemented")作为具体实现。因为fatalError不会像断言和先决条件那样被优化掉，所以你可以确保当代码执行到一个没有被实现的方法时，程序会被中断。

## 基本运算符

Swift 支持大部分标准 C 语言的运算符，且改进许多特性来减少常规编码错误。如：赋值符（`=`）不返回值，以防止把想要判断相等运算符（`==`）的地方写成赋值符导致的错误。算术运算符（`+`，`-`，`*`，`/`，`%`等）会检测并不允许值溢出，以此来避免保存变量时由于变量大于或小于其类型所能承载的范围时导致的异常结果。当然允许你使用 Swift 的溢出运算符来实现溢出。

Swift 还提供了 C 语言没有的区间运算符，例如 `a..<b` 或 `a...b`，这方便我们表达一个区间内的数值。

### 赋值运算符

如果赋值的右边是一个多元组，它的元素可以马上被分解成多个常量或变量：

```swift
let (x, y) = (1, 2)
// 现在 x 等于 1，y 等于 2
```

与 C 语言和 Objective-C 不同，Swift 的赋值操作并不返回任何值。所以以下代码是错误的：

```swift
if x = y {
    // 此句错误, 因为 x = y 并不返回任何值
}
```

### 算术运算符

四则运算符，加法运算符也可用于 `String` 的拼接：

```swift
"hello, " + "world"  // 等于 "hello, world"
```

### 求余运算符

*求余运算符*（`a % b`）是计算 `b` 的多少倍刚刚好可以容入`a`，返回多出来的那部分（余数），并且当`倍数`取最大值的时候，就会刚好可以容入 `a` 中。

```swift
-9 = (4 × -2) + -1 // -2是最大倍数
```

### 组合赋值运算符

例如：+=

> 注意：
> 复合赋值运算没有返回值，`let b = a += 2`这类代码是错误

### 比较运算符

所有标准 C 语言中的*比较运算符*都可以在 Swift 中使用：

 如：等于，不等于，大于，小于，大于等于，小于等于

> 注意： Swift 也提供恒等（`===`）和不恒等（`!==`）这两个比较符来判断两个对象是否引用同一个对象实例。

等于运算符可以用于比较字符串、元组

如果两个元组的元素相同，且长度相同的话，元组就可以被比较。比较元组大小会按照从左到右、逐值比较的方式，直到发现有两个值不等时停止，并且元组中的元素都是可比较的，如Int、String，Bool不能被比较

```swift
(1, "zebra") < (2, "apple")   // true，因为 1 小于 2
(3, "apple") < (3, "bird")    // true，因为 3 等于 3，但是 apple 小于 bird
(4, "dog") == (4, "dog")      // true，因为 4 等于 4，dog 等于 dog
```

```swift
("blue", -1) < ("purple", 1)       // 正常，比较的结果为 true
("blue", false) < ("purple", true) // 错误，因为 < 不能比较布尔类型
```

> 注意：
> Swift 标准库只能比较七个以内元素的元组比较函数。如果你的元组元素超过七个时，你需要自己实现比较运算符。

### 空合运算符（Nil Coalescing Operator）

*空合运算符*（`a ?? b`）将对可选类型 `a` 进行空判断，如果 `a` 包含一个值就进行解封，否则就返回一个默认值 `b`。

空合运算符是对以下代码的简短表达方法：

```swift
a != nil ? a! : b
```

### 区间运算符

- 闭区间运算符

  *闭区间运算符*（`a...b`）定义一个包含从 `a` 到 `b`（包括 `a` 和 `b`）的所有值的区间。`a` 的值不能超过 `b`。 ‌ 闭区间运算符在迭代一个区间的所有值时是非常有用的，如在 `for-in` 循环中：

  ```swift
  for index in 1...5 {
      print("\(index) * 5 = \(index * 5)")
  }
  ```

- 半开区间运算符

  *半开区间运算符*（`a..<b`）定义一个从 `a` 到 `b` 但不包括 `b` 的区间。 之所以称为*半开区间*，是因为该区间包含第一个值而不包括最后的值，适用于数组遍历。

  ```swift
  let names = ["Anna", "Alex", "Brian", "Jack"]
  let count = names.count
  for i in 0..<count {
      print("第 \(i + 1) 个人叫 \(names[i])")
  }
  ```

- 单侧区间

  闭区间操作符有另一个表达形式，可以表达往一侧无限延伸的区间 —— 例如，一个包含了数组从索引 2 到结尾的所有值的区间。在这些情况下，你可以省略掉区间操作符一侧的值。这种区间叫做单侧区间，因为操作符只有一侧有值。例如：

  ```swift
  for name in names[2...] {
      print(name)
  }
  // Brian
  // Jack
  
  for name in names[...2] {
      print(name)
  }
  // Anna
  // Alex
  // Brian
  ```

  半开区间操作符也有单侧表达形式，附带上它的最终值。就像你使用区间去包含一个值，最终值并不会落在区间内。例如：

  ```swift
  for name in names[..<2] {
      print(name)
  }
  // Anna
  // Alex
  ```

### 逻辑运算符

逻辑与或非，跟C一样，略过

## 字符串和字符

字符串字面量可以用于为常量和变量提供初始值：

```swift
let someString = "Some string literal value"
```

### 多行字符串字面量

```swift
let quotation = """
The White Rabbit put on his spectacles.  "Where shall I begin,
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on
till you come to the end; then stop."
"""
```

如果你的代码中，多行字符串字面量包含换行符的话，则多行字符串字面量中也会包含换行符。如果你想换行，以便加强代码的可读性，但是你又不想在你的多行字符串字面量中出现换行符的话，你可以用在行尾写一个反斜杠(`\`)作为续行符。

```swift
let softWrappedQuotation = """
The White Rabbit put on his spectacles.  "Where shall I begin, \
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on \
till you come to the end; then stop."
"""
```

### 字符串字面量的特殊字符

字符串字面量可以包含以下特殊字符：

- 转义字符`\0`(空字符)、`\\`(反斜线)、`\t`(水平制表符)、`\n`(换行符)、`\r`(回车符)、`\"`(双引号)、`\'`(单引号)。

### 初始化空字符串

要创建一个空字符串作为初始值，可以将空的字符串字面量赋值给变量，也可以初始化一个新的`String`实例：

```swift
var emptyString = ""               // 空字符串字面量
var anotherEmptyString = String()  // 初始化方法
// 两个字符串均为空并等价。
if emptyString.isEmpty {
    print("Nothing to see here")
}
// 打印输出："Nothing to see here"
```

### 字符串是值类型

Swift 的`String`类型是*值类型*。 如果您创建了一个新的字符串，那么当其进行常量、变量赋值操作，或在函数/方法中传递时，会进行值拷贝。 任何情况下，都会对已有字符串值创建新副本，并对该新副本进行传递或赋值操作。

### 使用字符

您可通过`for-in`循环来遍历字符串，获取字符串中每一个字符的值：

```swift
// Swift 中以下赋值会报错
let char: Character = "AB"

// Swift 中以下赋值会报错
let char1: Character = ""
var char2: Character = ""

for character in "Dog!🐶" {
    print(character)
}
// D
// o
// g
// !
// 🐶
```

字符串可以通过传递一个值类型为`Character`的数组作为自变量来初始化：

```swift
let catCharacters: [Character] = ["C", "a", "t", "!", "🐱"]
let catString = String(catCharacters)
print(catString)
// 打印输出："Cat!🐱"
```

### 链接字符串和字符

您可以用`append()`方法将一个字符附加到一个字符串变量的尾部：

```swift
let exclamationMark: Character = "!"
welcome.append(exclamationMark)
// welcome 现在等于 "hello there!"
```

### 字符串插值

*字符串插值*是一种构建新字符串的方式，可以在其中包含常量、变量、字面量和表达式。**字符串字面量**和**多行字符串字面量**都可以使用字符串插值。 您插入的字符串字面量的每一项都在以反斜线为前缀的圆括号中：

```swift
let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
```

### 字符串函数及运算符

Swift 支持以下几种字符串函数及运算符：

| 序号 | 函数/运算符 & 描述                                           |
| ---- | ------------------------------------------------------------ |
| 1    | **isEmpty**判断字符串是否为空，返回布尔值                    |
| 2    | **hasPrefix(prefix: String)**检查字符串是否拥有特定前缀      |
| 3    | **hasSuffix(suffix: String)**检查字符串是否拥有特定后缀。    |
| 4    | **Int(String)**转换字符串数字为整型。 实例: `let myString: String = "256" let myInt: Int? = Int(myString) ` |
| 5    | **String.count**计算字符串的长度                             |
| 6    | **+**连接两个字符串，并返回一个新的字符串                    |
| 7    | **+=**连接操作符两边的字符串并将新字符串赋值给左边的操作符变量 |
| 8    | **==**判断两个字符串是否相等                                 |
| 9    | **<**比较两个字符串，对两个字符串的字母逐一比较。            |
| 10   | **!=**比较两个字符串是否不相等。                             |

## 控制流

### 循环语句

| 循环类型                                                     | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [for-in](https://www.w3cschool.cn/swift/swift-for-in.html)   | 遍历一个集合里面的所有元素，例如由数字表示的区间、数组中的元素、字符串中的字符。 |
| [repeat...while 循环](https://www.w3cschool.cn/swift/swift-repeat-while-loop.html) | 类似 while 语句区别在于判断循环条件之前，先执行一次循环的代码块。 |
| [while 循环](https://www.w3cschool.cn/swift/swift-while-loop.html) | 运行一系列语句，如果条件为true，会重复运行，直到条件变为false。 |

### 循环控制语句

循环控制语句改变你代码的执行顺序，通过它你可以实现代码的跳转。Swift 以下几种循环控制语句：

| 控制语句                                                     | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [continue 语句](https://www.w3cschool.cn/swift/swift-continue-statement.html) | 告诉一个循环体立刻停止本次循环迭代，重新开始下次循环迭代。   |
| [break 语句](https://www.w3cschool.cn/swift/swift-break-statement.html) | 中断当前循环。                                               |
| [fallthrough 语句](https://www.w3cschool.cn/swift/swift-fallthrough-statement.html) | 如果在一个case执行完后，继续执行下面的case，需要使用fallthrough(贯穿) |

```swift
repeat {
    print( "index 的值为 \(index)")
    index = index + 1
} while index < 20
```

```swift
var index = 10

switch index {
   case 100  :
      print( "index 的值为 100")
   case 10,15  :
      print( "index 的值为 10 或 15")
      fallthrough
   case 5  :
      print( "index 的值为 5")
   default :
      print( "默认 case")
}
```

### guard

保证判断条件为true，继续向后执行

```swift
let name: String? = "老王"
let age: Int? = 10

func testGuard () {
    guard let nameNew = name,
        let ageNew = age else {
            print("姓名 或 年龄 为nil")
            return
    }
    // 代码执行至此, nameNew 和 ageNew 一定有值
    print(nameNew + String(ageNew))     // 输出:老王10
}

testGuard()
```

## 字典

Swift 字典用来存储无序的相同类型数据的集合，Swift 数组会强制检测元素的类型，如果类型不同则会报错。

如果创建一个字典，并赋值给一个变量，则创建的字典就是可以修改的。这意味着在创建字典后，可以通过添加、删除、修改的方式改变字典里的项目。如果将一个字典赋值给常量，字典就不可修改，并且字典的大小和内容都不可以修改。

```swift
// 创建字典
var someDict =  [KeyType: ValueType]()
// 创建空字典
var someDict = [Int: String]()
// 创建非空字典
var someDict:[Int:String] = [1:"One", 2:"Two", 3:"Three"]
// 基于序列的字典初始化
var cities = ["Haikou", "Beijing", "Nanjing"]
var Distance = [2000,10, 620]
let cityDistanceDict = Dictionary(uniqueKeysWithValues: zip(cities, Distance))

// 过滤
var closeCities = cityDistanceDict.filter { $0.value < 1000 }

// 分组
var cities = ["Delhi","Bangalore","Hyderabad","Dehradun","Bihar"]
var GroupedCities = Dictionary(grouping: cities ) { $0.first! }
// ["D" :["Delhi","Dehradun"], "B" : ["Bengaluru","Bihar"], "H" : ["Hyderabad"]]

// 访问字典
var someVar = someDict[key]
var someVar = someDict[1] // return optional value

// 通过updateValue方法修改字典，返回可选值，返回旧的value
var oldVal = someDict.updateValue("One 新的值", forKey: 1)
// 通过指定key修改字典
someDict[1] = "One 新的值"

// 通过removeValueForKey方法删除k-v，方法返回可选值，如果key存在则返回对应value
var removedValue = someDict.removeValue(forKey: 2)
// 通过指定key的值为 nil 来移除
someDict[2] = nil

// 通过for-in遍历
for (key, value) in someDict {
   print("字典 key \(key) -  字典 value \(value)")
}
// 使用enumerated()方法来进行字典遍历，返回的是字典的索引及 (key, value) 对
for (key, value) in someDict.enumerated() {
    print("字典 key \(key) -  字典 (key, value) 对 \(value)")
}
/* 输出结果
字典 key 0 -  字典 (key, value) 对 (2, "Two")
字典 key 1 -  字典 (key, value) 对 (3, "Three")
字典 key 2 -  字典 (key, value) 对 (1, "One")
*/ 

// k-v分别转换成数组
let dictKeys = [Int](someDict.keys)
let dictValues = [String](someDict.values)

// count、isEmpty属性
```

## 数组

数据跟字典一样，检查数据类型，只能保存同一类型数据，变量可修改，常量不可修改

```swift
// 创建空数组
var someInts = [Int]()
// 创建一个初始化大小数组
var threeDoubles = Array(repeating: 0.0, count: 3)

var someInts:[Int] = [10, 20, 30]

// 通过下标访问数组
var someVar = someInts[0]

// 使用 append() 方法或者赋值运算符 += 在数组末尾添加元素
var someInts = [Int]()
someInts.append(20)
someInts.append(30)
someInts += [40]

// 通过下标修改最后一个元素
someInts[2] = 50

// 调用数组的insert(_:at:)方法来在某个具体索引值之前添加数据项：
someInts.insert(60, at: 0)
// 删除
let a = someInts.remove(at: 0)

// 通过for-in遍历数组
for item in someInts {
   print(item)
}
// 通过enumerate方法遍历数组
for (index, item) in someInts.enumerated() {
   print("在 index = \(index) 位置上的值为 \(item)")
}

// 使用加法操作符（+）来合并两种已存在的相同类型数组
var intsA = Array(repeating: 2, count: 2)
var intsB = Array(repeating: 1, count: 3)

var intsC = intsA + intsB

for item in intsC {
   print(item)
}

// count、isEmpty属性
```

## Set

不包含重复值，同类型，无序，值可比较

```swift
// 语法格式
var someSet = Set<Character>() // 字符可以由集合的数据类型替换。

// 获取元素数量
someSet.count 

// 插入值
someSet.insert("c")

// 判断set是否为空
someSet.isEmpty 

// 删除set中的值
someSet.remove("c")

// 检查set是否包含值
someSet.contains("c")
```

### 迭代

```swift
for items in someSet {
   print(items)
}

// 排序之后遍历
for items in someSet.sorted() {
   print(items)
}
```

### set操作

```swift
let evens: Set = [10, 12, 14, 16, 18]
let odds: Set = [5, 7, 9, 11, 13]
let primes = [2, 3, 5, 7]
// 联合
odds.union(evens).sorted()
// [5,7,9,10,11,12,13,14,16,18]

// 相交
odds.intersection(evens).sorted()
//[]

// 相差
odds.subtracting(primes).sorted()
//[9, 11, 13]	

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

## 函数

```swift
// 语法
func funcname(形参) -> returntype
{
   Statement1
   ……
   Statement N
   return parameters
}

// 元组作为参数
func mult(no1: Int, no2: Int) -> Int {
    return no1 * no2;
}
print(mult(no1: 2, no2: 10))
print(mult(no1: 3, no2: 10))

// 元组作为返回值
func minMax(array: [Int]) -> (min: Int, max: Int)? {
    if array.isEmpty { return nil; }
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
}

if let bounds = minMax(array: [-6, 8, 2, 109, 3, 71]) {
    print("最小值为 \(bounds.min) ，最大值为 \(bounds.max)")
}

// 可以在局部参数名前指定外部参数名，中间以空格分隔，外部参数名用于在函数调用时传递给函数的参数
func pow(firstArg a: Int, secondArg b: Int) -> Int {
    if b <= 0 { return 1; }
    var res = a
    for _ in 1..<b {
        res = res * a
    }
    print(res)
    return res
}
pow(firstArg: 5, secondArg: 0)

// 可变参数
// 可变参数可以接受零个或多个值，通过在变量类型名后面加入（...）的方式来定义
func vari<N>(members: N...){
    for i in members {
        print(i)
    }
}
vari(members: 4,3,5)
vari(members: 4.5, 3.1, 5.6)
vari(members: "yuanfudao", "zebra", "swift")
```

一般默认在函数中定义的参数都是常量参数，如果想要声明一个变量参数，可以在前面加上var，这样就可以改变这个参数的值了。

例如：

```swift
func getName(var id: String).........
```

定义一个输入输出参数时，在参数定义前加 inout 关键字。一个输入输出参数有传入函数的值，这个值被函数修改，然后被传出函数，替换原来的值。

## 闭包

Swift中的闭包有很多优化的地方: 

1. 根据上下文推断参数和返回值类型
2. 从单行表达式闭包中隐式返回（也就是闭包体只有一行代码，可以省略return）
3. 可以使用简化参数名，如$0, $1(从0开始，表示第i个参数...)
4. 提供了尾随闭包语法(Trailing closure syntax)

```swift
// 语法格式
{(parameters) -> return type in
   statements
}

// demo 
let divide = {(val1: Int, val2: Int) -> Int in
    return val1 / val2
}
let result = divide(200, 20)
print (result)

var names = ["AT", "AE", "D", "S", "BE"]
var reversed = names.sorted { (s1, s2) -> Bool in
    return s1 > s2
}
// 参数名称缩写
var reversed = names.sorted(by: { $0 > $1})
// 运算符函数，String定义了大于的实现，需要两个字符串参数，自动推断为$0 > $1
var reversed = names.sorted(by: >)

print(reversed)

// 尾随闭包，最后一个参数是闭包
var reversed = names.sorted() { $0 < $1}
var reversed = names.sorted { $0 < $1}

// 捕获值
func makeIncrementor(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementor() -> Int {
        // 闭包保存了runningTotal的值得副本，因此多次调用会一直累加
        runningTotal += amount
        return runningTotal
    }
    return incrementor
}

let incrementByTen = makeIncrementor(forIncrement: 10)

// 返回的值为10
print(incrementByTen())
// 返回的值为20
print(incrementByTen())
// 返回的值为30
print(incrementByTen())

```

注意：上面的例子中，incrementByTen是常量，但是这些常量指向的闭包仍然可以增加其捕获的变量值。

这是因为函数和闭包都是引用类型。

## 枚举

- 它声明在类中，可以通过实例化类来访问它的值。
- 枚举也可以定义构造函数（initializers）来提供一个初始成员值；可以在原始的实现基础上扩展它们的功能。
- 可以遵守协议（protocols）来提供标准的功能。

```swift
// 语法格式
enum enumname {
   // 枚举定义放在这里
}

// 定义枚举
enum DaysofaWeek {
    case Sunday
    case Monday
    case TUESDAY
    case WEDNESDAY
    case THURSDAY
    case FRIDAY
    case Saturday
}

var weekDay = DaysofaWeek.THURSDAY
// 当weekDay的类型已知时，再次为其赋值可以省略枚举名
weekDay = .THURSDAY
switch weekDay
{
case .Sunday:
    print("星期天")
case .Monday:
    print("星期一")
case .TUESDAY:
    print("星期二")
case .WEDNESDAY:
    print("星期三")
case .THURSDAY:
    print("星期四")
case .FRIDAY:
    print("星期五")
case .Saturday:
    print("星期六")
}
```

- 相关值

- ```swift
  enum Student {
      case Name(String)
      case Mark(Int, Int, Int)
  }
  var studDetails = Student.Name("Swift")
  var studMarks = Student.Mark(98, 97, 95)
  switch studMarks {
  case .Name(let studName):
      print("学生的名字是: \(studName)。")
  case .Mark(let Mark1, let Mark2, let Mark3):
      print("学生的成绩是: \(Mark1), \(Mark2), \(Mark3)。")
  }
  ```

- 原始值

  原始值可以是字符串，字符，或者任何整型值或浮点型值。每个原始值在它的枚举声明中必须是唯一的

  在原始值为整数的枚举时，不需要显式的为每一个成员赋值，Swift会自动为你赋值。

  例如，当使用整数作为原始值时，隐式赋值的值依次递增1。如果第一个值没有被赋初值，将会被自动置为0

  ```swift
  enum Month: Int {
      case January = 1, February, March, April, May, June, July, August, September, October, November, December
  }
  
  let yearMonth = Month.May.rawValue
  print("数字月份为: \(yearMonth)。") 
  // 输出结果为5
  ```

- 区别

| 相关值                                                       | 原始值                |
| ------------------------------------------------------------ | --------------------- |
| 不同数据类型                                                 | 相同数据类型          |
| 实例: enum {10,0.8,"Hello"}                                  | 实例: enum {10,35,50} |
| 值的创建基于常量或变量                                       | 预先填充的值          |
| 相关值是当你在创建一个基于枚举成员的新常量或变量时才会被设置，并且每次当你这么做得时候，它的值可以是不同的。 | 原始值始终是相同的    |

## 结构体

与 C 和 Objective C 不同的是：

- 结构体不需要包含实现文件和接口。 
- 结构体允许我们创建一个单一文件，且系统会自动生成面向其它代码的外部接口。 

结构体总是通过被复制的方式在代码中传递，因此它的值是不可修改的。

```swift
// 语法
struct nameStruct { 
   Definition 1
   Definition 2
   ……
   Definition N
}

struct MarksStruct {
   var mark: Int

   init(mark: Int) {
      self.mark = mark
   }
}
var aStruct = MarksStruct(mark: 98)
var bStruct = aStruct // aStruct 和 bStruct 是使用相同值的结构体！
bStruct.mark = 97
print(aStruct.mark) // 98
print(bStruct.mark) // 97
```

## 类

Swift 并不要求你为自定义类去创建独立的接口和实现文件。你所要做的是在一个单一文件中定义一个类，系统会自动生成面向其它代码的外部接口。

```swift
// 语法
Class classname {
   Definition 1
   Definition 2
   ……
   Definition N
}

class studentMarks {
   var mark1 = 300
   var mark2 = 400
   var mark3 = 900
}
// 实例化
let marks = studentMarks()
// 访问属性
print("Mark1 is \(marks.mark1)")
print("Mark2 is \(marks.mark2)")
print("Mark3 is \(marks.mark3)")
```

#### 恒等运算符

因为类是引用类型，有可能有多个常量和变量在后台同时引用某一个类实例。

为了能够判定两个常量或者变量是否引用同一个类实例，Swift 内建了两个恒等运算符：

| **恒等运算符**                                  | **不恒等运算符**                                  |
| ----------------------------------------------- | ------------------------------------------------- |
| 运算符为：===                                   | 运算符为：!==                                     |
| 如果两个常量或者变量引用同一个类实例则返回 true | 如果两个常量或者变量引用不同一个类实例则返回 true |

```swift
class SampleClass: Equatable {
    let myProperty: String
    init(s: String) {
        myProperty = s
    }
}
func ==(lhs: SampleClass, rhs: SampleClass) -> Bool {
    return lhs.myProperty == rhs.myProperty
}

let spClass1 = SampleClass(s: "Hello")
let spClass2 = SampleClass(s: "Hello")

if spClass1 === spClass2 {// false
    print("引用相同的类实例 \(spClass1)")
}

if spClass1 !== spClass2 {// true
    print("引用不相同的类实例 \(spClass2)")
}
```

## 属性

### 存储属性

常见的常量、变量都是存储属性

```swift
struct Number {
   var digits: Int
   let pi = 3.1415
}

var n = Number(digits: 12345)
n.digits = 67

print("\(n.digits)")
print("\(n.pi)")
```

### 延迟存储属性

延迟存储属性是指当第一次被调用的时候才会计算其初始值的属性。

在属性声明前使用 **lazy** 来标示一个延迟存储属性。

> 必须将延迟存储属性声明成变量（使用`var`关键字），因为属性的值在实例构造完成之前可能无法得到。而常量属性在构造过程完成之前必须要有初始值，因此无法声明成延迟属性。 

```swift
class sample {
    lazy var no = number() // `var` 关键字是必须的
}

class number {
    var name = "swift"
}

var firstsample = sample()
print(firstsample.no.name)
```

### 计算属性

除存储属性外，类、结构体和枚举可以定义*计算属性*，计算属性不直接存储值，而是提供一个 getter 来获取值，一个可选的 setter 来间接设置其他属性或变量的值。

```swift
class sample {
    var no1 = 0.0, no2 = 0.0
    var length = 300.0, breadth = 150.0
    
    var middle: (Double, Double) {
        get {
            return (lngth / 2, breadth / 2)
        }
        // 如果计算属性的 setter 没有定义表示新值的参数名，则可以使用默认名称 newValue。
        set(axis) {
            no1 = axis.0 - (length / 2)
            no2 = axis.1 - (breadth / 2)
        }
    }
}

var result = sample()
print(result.middle)
result.middle = (0.0, 10.0)

print(result.no1)
print(result.no2)
```

### 只读计算属性

只有 getter 没有 setter 的计算属性就是只读计算属性。

只读计算属性总是返回一个值，可以通过点(.)运算符访问，但不能设置新的值。

```swift
class film {
    var head = ""
    var duration = 0.0
    var metaInfo: [String:String] {
        return [
            "head": self.head,
            "duration":"\(self.duration)"
        ]
    }
}

var movie = film()
movie.head = "Swift 属性"
movie.duration = 3.09

print(movie.metaInfo["head"]!)
print(movie.metaInfo["duration"]!)
```

> 注意：
>
> 必须使用`var`关键字定义计算属性，包括只读计算属性，因为它们的值不是固定的。`let`关键字只用来声明常量属性，表示初始化后再也无法修改的值。

### 属性观察器

可以为属性添加如下的一个或全部观察器：

- `willSet`在设置新的值之前调用
- `didSet`在新的值被设置之后立即调用
- willSet和didSet观察器在属性初始化过程中不会被调用

```swift
class Samplepgm {
    var counter: Int = 0 {
        willSet(newTotal) {
            print("计数器: \(newTotal)")
        }
        didSet {
            if counter > oldValue {
                print("新增数 \(counter - oldValue)")
            }
        }
    }
}
let NewCounter = Samplepgm()
NewCounter.counter = 100
NewCounter.counter = 800
```

### 类型属性

类型属性是作为类型定义的一部分写在类型最外层的花括号（{}）内。

使用关键字 static 来定义值类型的类型属性，关键字 class 来为类定义类型属性。

```
struct Structname {
   static var storedTypeProperty = " "
   static var computedTypeProperty: Int {
      // 这里返回一个 Int 值
   }
}

enum Enumname {
   static var storedTypeProperty = " "
   static var computedTypeProperty: Int {
      // 这里返回一个 Int 值
   }
}

class Classname {
   class var computedTypeProperty: Int {
      // 这里返回一个 Int 值
   }
}
```

> 注意：
> 例子中的计算型类型属性是只读的，但也可以定义可读可写的计算型类型属性，跟实例计算属性的语法类似。 

### 获取和设置类型属性的值

类似于实例的属性，类型属性的访问也是通过点运算符(.)来进行。但是，类型属性是通过类型本身来获取和设置，而不是通过实例。实例如下：

```
struct StudMarks {
   static let markCount = 97
   static var totalCount = 0
   var InternalMarks: Int = 0 {
      didSet {
         if InternalMarks > StudMarks.markCount {
            InternalMarks = StudMarks.markCount
         }
         if InternalMarks > StudMarks.totalCount {
            StudMarks.totalCount = InternalMarks
         }
      }
   }
}

var stud1Mark1 = StudMarks()
var stud1Mark2 = StudMarks()

stud1Mark1.InternalMarks = 98
print(stud1Mark1.InternalMarks) 

stud1Mark2.InternalMarks = 87
print(stud1Mark2.InternalMarks)
```

## 方法

### 语法

```swift
func funcname(Parameters) -> returntype {
   Statement1
   Statement2
   ---
   Statement N
   return parameters
}
```

### 局部和外部参数名称

Swift 4通过将第一个参数名称声明为局部参数名称，而其余参数名称为全局参数名称，提供了方法的灵活性。 这里`no1`由Swift 4方法声明为局部参数名称。 `no2`用于全局声明并通过程序访问。

```swift
class division {
   var count: Int = 0
   func incrementBy(no1: Int, and no2: Int) {
      count = no1 / no2
      print(count)
   }
}

let counter = division()
counter.incrementBy(no1: 1800, no2: 3)
counter.incrementBy(no1: 1600, no2: 5)
counter.incrementBy(no1: 11000, no2: 3)
```

### 实例方法修改值类型

结构体和枚举都是值类型，不能通过实例方法修改属性，可以通过mutating实现实例方法修改属性

```swift
struct area {
   var length = 1
   var breadth = 1

   func area() -> Int {
      return length * breadth
   }
   mutating func scaleBy(res: Int) {
      length *= res
      breadth *= res
      print(length)
      print(breadth)
   }
}

var val = area(length: 3, breadth: 5)
val.scaleBy(res: 3)
val.scaleBy(res: 30)
val.scaleBy(res: 300)
/* 输出结果
9
15
270
450
81000
135000
*/
```

### 类型方法

```swift
class Math {
   class func abs(number: Int) -> Int {
      if number < 0 {
         return (-number)
      } else {
         return number
      }
   }
}

struct absno {
   static func abs(number: Int) -> Int {
      if number < 0 {
         return (-number)
      } else {
         return number
      }
   }
}

let no = Math.abs(number: -35)
let num = absno.abs(number: -5)

print(no)
print(num)
```

## 下标

```swift
struct subexample {
   let decrementer: Int
   subscript(index: Int) -> Int {
      return decrementer / index
   }
}
let division = subexample(decrementer: 100)

print("The number is divisible by \(division[9]) times")

class daysofaweek {
   private var days = ["Sunday", "Monday", "Tuesday", "Wednesday",
      "Thursday", "Friday", "saturday"]
   subscript(index: Int) -> String {
      get {
         return days[index]
      }
      set(newValue) {
         self.days[index] = newValue
      }
   }
}
var p = daysofaweek()

print(p[0])
```

### 下标中的选项

定义多个下标称为“下标重载”，类或结构可根据需要提供多个下标定义。 这些多个下标是根据下标括号中声明的值的类型推断的。参考以下示例代码

```swift
struct Matrix {
   let rows: Int, columns: Int
   var print: [Double]
   init(rows: Int, columns: Int) {
      self.rows = rows
      self.columns = columns
      print = Array(count: rows * columns, repeatedValue: 0.0)
   }
   subscript(row: Int, column: Int) -> Double {
      get {
         return print[(row * columns) + column]
      }
      set {
         print[(row * columns) + column] = newValue
      }
   }
}
var mat = Matrix(rows: 3, columns: 3)

mat[0,0] = 1.0
mat[0,1] = 2.0
mat[1,0] = 3.0
mat[1,1] = 5.0

print("\(mat[0,0])")
```

## 继承

### 方法覆盖

override关键字用于覆盖超类中声明的方法，super关键字用作访问超类中的方法，属性和下标的前缀

```swift
class cricket {
   func print() {
      print("Welcome to Swift 4 Super Class")
   }
}

class tennis: cricket {
   override func print() {
      print("Welcome to Swift 4 Sub Class")
   }
}

let cricinstance = cricket()
cricinstance.print()

let tennisinstance = tennis()
tennisinstance.print()
```

### 属性覆盖

- 当为覆盖属性定义`setter`时，也必须定义`getter`。
- 当不想修改继承的属性`getter`时，可以简单地将继承的值通过语法`super.someProperty`传递给超类。

```swift
class Circle {
   var radius = 12.5
   var area: String {
      return "of rectangle for \(radius) "
   }
}

class Rectangle: Circle {
   var print = 7
   override var area: String {
      return super.area + " is now overridden as \(print)"
   }
}

let rect = Rectangle()
rect.radius = 25.0
rect.print = 3
print("Radius \(rect.area)")
```

### 覆盖属性观察员

```swift
class Square: Rectangle {
   override var radius: Double {
      didSet {
         print = Int(radius/5.0)+1
      }
   }
}

let sq = Square()
sq.radius = 100.0
print("Radius \(sq.area)")
```

### 防止覆盖的final属性

final关键字可用于类、属性、方法、下标，声明之后不允许覆盖

```swift
final class Circle {
   final var radius = 12.5
   var area: String {
      return "of rectangle for \(radius) "
   }
}

class Rectangle: Circle { // error, 不允许继承
   var print = 7
   override var area: String { // error, 不允许继承
      return super.area + " is now overridden as \(print)"
   }
}

let rect = Rectangle()
rect.radius = 25.0
rect.print = 3
print("Radius \(rect.area)")

class Square: Rectangle {
   override var radius: Double { // error, 不允许继承
      didSet {
         print = Int(radius/5.0)+1
      }
   }
}

let sq = Square()
sq.radius = 100.0
print("Radius \(sq.area)")
```

## 构造函数

### 语法

```swift
init() {
   //New Instance initialization goes here
}

struct rectangle {
   var length: Double
   var breadth: Double
   // 通过init初始化
   init() { 
      length = 6
      breadth = 12
   }
}

struct rectangle {
   // 通过设置默认值初始化
   var length = 6
   var breadth = 12
}

var area = rectangle()
print("area of rectangle is \(area.length*area.breadth)")
```

### 参数初始化

```swift
struct Rectangle {
   var length: Double
   var breadth: Double
   var area: Double

   init(fromLength length: Double, fromBreadth breadth: Double) {
      self.length = length
      self.breadth = breadth
      area = length * breadth
   }
}
```

### 局部和外部参数

同函数局部外部参数

下滑线表示不需要外部名称

```swift
struct Rectangle {
   var length: Double

   init(frombreadth breadth: Double) {
      length = breadth * 10
   }
   init(_ area: Double) {
      length = area
   }
}
```

### optional属性类型

自动初始化为nil

```swift
struct Rectangle {
   var length: Double?
   init(_ area: Double) {
      length = area
   }
}

let rectarea = Rectangle(180.0)
print("area is: \(rectarea.length)")
// area is: Optional(180.0)
```

### 初始化期间修改常量属性

```swift
struct Rectangle {
   let length: Double?
   init(_ area: Double) {
      length = area
   }
}

let rectarea = Rectangle(180.0)
print("area is: \(rectarea.length)")
```

### 默认初始化方法

默认初始值设定项为其所有声明的基类或结构属性提供一个新实例，并使用默认值。

### 指定、便捷初始化方法

```swift
class mainClass {
   var no1 : Int // local storage
   init(no1 : Int) {
      self.no1 = no1 // initialization
   }
}

class subClass : mainClass {
   var no2 : Int
   // 指定初始化
   init(no1 : Int, no2 : Int) {
      self.no2 = no2
      super.init(no1:no1)
   }
   // 便捷初始化方法
   override convenience init(no1: Int) {
      self.init(no1:no1, no2:0)
   }
}

let res = mainClass(no1: 20)
let print = subClass(no1: 30, no2: 50)

print("res is: \(res.no1)")
print("res is: \(print.no1)")
print("res is: \(print.no2)")
```

### 可失败的初始化方法

```swift
struct studrecord {
   let stname: String
   init?(stname: String) {
      if stname.isEmpty {return nil }
      self.stname = stname
   }
}

enum functions {
   case a, b, c, d
   init?(funct: String) {
      switch funct {
      case "one":
         self = .a
      case "two":
         self = .b
      case "three":
         self = .c
      case "four":
         self = .d
      default:
         return nil
      }
   }
}
```

### 必须的初始化方法

```swift
class classA {
   required init() {
      var a = 10
      print(a)
   }
}

class classB: classA {
   required init() {
      var b = 30
      print(b)
   }
}

let res = classA()
let print = classB()
```

## 析构函数

```swift
var counter = 0; // for reference counting
class baseclass {
   init() {
      counter++;
   }
   deinit {
      counter--;
   }
}
var print: baseclass? = baseclass()

print(counter)
print = nil
print(counter)
```

## 协议

### 语法

```swift
protocol SomeProtocol {
	// protocol definition
}

// 枚举、struct、类都可以实现多个协议
struct SomeStructure: Protocol1, Protocol2 {
   // structure definition 
}
class SomeClass: SomeSuperclass, Protocol1, Protocol2 {
   // class definition 
}

// demo
protocol classa {
   var marks: Int { get set }
   var result: Bool { get }

   func attendance() -> String
   func markssecured() -> String
}

protocol classb: classa {
   var present: Bool { get set }
   var subject: String { get set }
   var stname: String { get set }
}

class classc: classb {
   var marks = 96
   let result = true
   var present = false
   var subject = "Swift 4 Protocols"
   var stname = "Protocols"

   func attendance() -> String {
      return "The \(stname) has secured 99% attendance"
   }
   func markssecured() -> String {
      return "\(stname) has scored \(marks)"
   }
}

let studdet = classc()
studdet.stname = "Swift 4"
studdet.marks = 98
studdet.markssecured()

print(studdet.marks)
print(studdet.result)
print(studdet.present)
print(studdet.subject)
print(studdet.stname)
```

### mutating方法

有时需要在方法中改变方法所属的实例。例如，在值类型（即结构体和枚举）的实例方法中，将 `mutating` 关键字作为方法的前缀，写在 `func` 关键字之前，表示可以在该方法中修改它所属的实例以及实例的任意属性的值

> 注意
> 实现协议中的 `mutating` 方法时，若是类类型，则不用写 `mutating` 关键字。而对于结构体和枚举，则必须写 `mutating` 关键字。

```swift
protocol Togglable {
    mutating func toggle()
}
enum OnOffSwitch: Togglable {
    case off, on
    mutating func toggle() {
        switch self {
        case .off:
            self = .on
        case .on:
            self = .off
        }
    }
}
var lightSwitch = OnOffSwitch.off
lightSwitch.toggle()
// lightSwitch 现在的值为 .on
```

### 构造方法

```swift
protocol SomeProtocol {
    init(someParameter: Int)
}
```

你可以在遵循协议的类中实现构造器，无论是作为指定构造器，还是作为便利构造器。无论哪种情况，你都必须为构造器实现标上 `required` 修饰符：

```swift
class SomeClass: SomeProtocol {
    required init(someParameter: Int) {
        // 这里是构造器的实现部分
    }
}
```

如果一个子类重写了父类的指定构造器，并且该构造器满足了某个协议的要求，那么该构造器的实现需要同时标注 `required` 和 `override` 修饰符：

```swift
protocol SomeProtocol {
    init()
}

class SomeSuperClass {
    init() {
        // 这里是构造器的实现部分
    }
}

class SomeSubClass: SomeSuperClass, SomeProtocol {
    // 因为遵循协议，需要加上 required
    // 因为继承自父类，需要加上 override
    required override init() {
        // 这里是构造器的实现部分
    }
}
```

## 通知

```swift
class ViewController: UIViewController {

    let observers = [MyObserver(name: "观察者1"), MyObserver(name: "观察者2")]

    override func viewDidLoad() {
        super.viewDidLoad()

        let notificationCenter = NotificationCenter.default
        let operationQueue = OperationQueue.main

        let _ = notificationCenter.addObserver(forName: UIApplication.didEnterBackgroundNotification, object: nil, queue: operationQueue) { (notification) in
            print("did enter background")
        }

        print("发送通知")
      	// 发送通知 DownloadImageNotification
        let notificationName = Notification.Name(rawValue: "DownloadImageNotification")
        notificationCenter.post(name: notificationName, object: self, userInfo: ["value1": "hangge.com", "value2": 12345])
        print("通知完毕")
    }
}

class MyObserver: NSObject {
    var name: String = "";

    init(name: String) {
        super.init()

        self.name = name
        let notificationName = Notification.Name(rawValue: "DownloadImageNotification")
      	// 监听通知 DownloadImageNotification
        NotificationCenter.default.addObserver(self, selector: #selector(downloadImage(notification:)), name: notificationName, object: nil)
    }

    @objc func downloadImage(notification: NSNotification) {
        let userInfo = notification.userInfo as! [String: AnyObject]
        let value1 = userInfo["value1"] as! String;
        let value2 = userInfo["value2"] as! Int

        print("\(name) get notification, user info is [\(value1), \(value2)]")

        sleep(3)

        print("\(name) done")
    }

    deinit {
      	// 移除通知
        NotificationCenter.default.removeObserver(self)
    }
}
```

### KVO

仅限于NSObject的子类可以使用KVO，需要监听的属性需要加上dynamic关键字

这是因为 KVO 是基于 KVC (Key-Value Coding) 以及动态派发技术实现的，而这些东西都是 Objective-C 运行时的概念。另外由于 Swift 为了效率，默认禁用了动态派发

```swift
class Person: NSObject {
	// 想用 Swift 来实现 KVO，我们还需要做额外的工作，那就是将想要观测的对象标记为dynamic。。
	var name = "青"
	dynamic var age = 18
	var sex = "女"
	var height = 170

	override init() {
		super.init()
	}
}

// 监听
var person = Person()
	
override func viewDidLoad() {
	super.viewDidLoad()
	// 为 person添加观察者，观察 age 属性的值是否有了新的赋值。
	person.addObserver(self, forKeyPath: "age", options: .new, context: nil)
}

override func observeValue(forKeyPath keyPath: String?, of object: Any?, change: [NSKeyValueChangeKey : Any]?, context: UnsafeMutableRawPointer?) {
		// 输出改变后的新值
	print(change![NSKeyValueChangeKey.newKey]!)
}

// 移除观察者
override func viewWillDisappear(_ animated: Bool) {
	person.removeObserver(self, forKeyPath: "age")
}
```