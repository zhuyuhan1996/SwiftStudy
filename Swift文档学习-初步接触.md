- argument -实参；raw value -原始值；optional -可选；convention -约定；subscript -下标；
- 1、变量始终在使用前初始化。
2、检查数组索引超出范围的错误。
3、检查整数是否溢出。
4、可选值确保明确处理 nil 值。
5、内存被自动管理。
6、错误处理允许从意外故障控制恢复
----
### 简单值
- 值永远不会被隐式转换为其他类型。如果你需要把一个值转换成其他类型，请显式转换
- 使用一对三个单引号（"""）来包含多行字符串内容，字符串中的内容（包括引号、空格、换行符等）都会保留下来
```Swift
let quotation = """
I said "I have \(apples) apples."
And then I said "I have \(apples + oranges) pieces of fruit."
"""
```
- 使用方括号 [] 来创建数组和字典，并使用下标或者键（key）来访问元素。最后一个元素后面允许有个逗号.
- 如果类型信息可以被推断出来，你可以用 [] 和 [:] 来创建空数组和空字典——就像你声明变量或者给函数传参数的时候一样。
```Swift
shoppingList = []
occupations = [:]
```
----
### 控制流
- 使用 if 和 switch 来进行条件操作，使用 for-in、while 和 repeat-while 来进行循环。包裹条件和循环变量的括号可以省略，但是语句体的大括号是必须的
- 你可以一起使用 if 和 let 一起来处理值缺失的情况。这些值可由可选值来代表。一个可选的值是一个具体的值或者是 nil 以表示值缺失。在类型后面加一个问号（?）来标记这个变量的值是可选的
- 如果变量的可选值是 nil，条件会判断为 false，大括号中的代码会被跳过。如果不是 nil，会将值解包并赋给 let 后面的常量，这样代码块中就可以使用这个值了。 另一种处理可选值的方法是通过使用 ?? 操作符来提供一个默认值。如果可选值缺失的话，可以使用默认值来代替。
- hasSuffix 是否有后缀并返回后缀。
- 运行 switch 中匹配到的 case 语句之后，程序会退出 switch 语句，并不会继续向下运行，所以不需要在每个子句结尾写 break
- 使用 ..< 创建的范围不包含上界，如果想包含的话需要使用 ...
--------
### 函数
- 默认情况下，函数使用它们的参数名称作为它们参数的标签，在参数名称前可以自定义参数标签，或者使用 _ 表示不使用参数标签
```Swift
func greet(_ person: String, on day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet("John", on: "Wednesday")
```
- 函数可以嵌套。被嵌套的函数可以访问外侧函数的变量，你可以使用嵌套函数来重构一个太长或者太复杂的函数。
- 函数也可以当做参数传入另一个函数
```Swift
func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
    for item in list {
        if condition(item) {
            return true
        }
    }
    return false
}
func lessThanTen(number: Int) -> Bool {
    return number < 10
}
var numbers = [20, 19, 11, 12,]
print(hasAnyMatches(list: numbers, condition: lessThanTen))
```
----
### 闭包
- 有很多种创建更简洁的闭包的方法。如果一个闭包的类型已知，比如作为一个代理的回调，你可以忽略参数，返回值，甚至两个都忽略。单个语句闭包会把它语句的值当做结果返回
- 你可以通过参数位置而不是参数名字来引用参数——这个方法在非常短的闭包中非常有用。当一个闭包作为最后一个参数传给一个函数的时候，它可以直接跟在括号后面。当一个闭包是传给函数的唯一参数，你可以完全忽略括号
----
### 对象和类
- self 被用来区别实例变量 name 和构造器的参数 name。当你创建实例的时候，像传入函数参数一样给类传入构造器的参数。每个属性都需要赋值——无论是通过声明（就像 numberOfSides）还是通过构造器（就像 name）。
- 如果你需要在对象释放之前进行一些清理工作，使用 deinit 创建一个析构函数
- 子类如果要重写父类的方法的话，需要用 override 标记——如果没有添加 override 就重写父类方法的话编译器会报错。编译器同样会检测 override 标记的方法是否确实在父类中
- 在Swift中使用pi，需要带前缀，Double.pi、float.pi、CGFloat.pi。
- 在 perimeter 的 setter 中，新值的名字是 newValue。你可以在 set 之后显式的设置一个名字。
注意 EquilateralTriangle 类的构造器执行了三步：
1、设置子类声明的属性值
2、调用父类的构造器
3、改变父类定义的属性值。其他的工作比如调用方法、getters 和 setters 也可以在这个阶段完成
```swift
class EquilateralTriangle: NamedShape {
    var sideLength: Double = 0.0

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }

    var perimeter: Double {
        get {
             return 3.0 * sideLength
        }
        set {
            sideLength = newValue / 3.0
        }
    }

    override func simpleDescription() -> String {
        return "An equilateral triangle with sides of length \(sideLength)."
    }
}
var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
print(triangle.perimeter)
triangle.perimeter = 9.9
print(triangle.sideLength)

```
----
### 结构体
- Swift 按照从0开始每次加1的方式为原始值进行赋值，不过你可以通过显式赋值进行改变。在上面的例子中，Ace被显式赋值为1，并且剩下的原始值会按照顺序赋值。你也可以使用字符串或者浮点数作为枚举的原始值。使用 rawValue 属性来访问一个枚举成员的原始值
- 用 init?(rawValue:)初始化构造器来创建一个带有原始值的枚举成员。如果存在与原始值相应的枚举成员就返回该枚举成员，否则就返回 nil。
```Swift
if let convertedRank = Rank(rawValue: 3) {
    let threeDescription = convertedRank.simpleDescription()
}
```
- 给 hearts 常量赋值时，枚举成员 Suit.hearts 需要用全名来引用，因为常量没有显式指定类型。在 switch 里，枚举成员使用缩写 .hearts 来引用，因为 self 的值已经是一个 suit 类型，在已知变量类型的情况下可以使用缩写
----
### 协议和扩展
- 使用protocol声明一个协议。用enum完成一个协议时，可以按照case的方式，根据不同的输入值选择不同的返回值。增加方法时需要注意使用mutating。
- 注意声明SimpleStructure时候mutating关键字用来标记一个会修改结构体的方法。SimpleClass的声明不需要标记任何方法，因为类中的方法通常可以修改类属性（类的性质）
- 创建一个有不同类型但是都实现一个协议的对象集合。当你处理类型是协议的值时，协议外定义的方法不可用.即使 protocolValue 变量运行时的类型是 simpleClass ，编译器还是会把它的类型当做 ExampleProtocol。这表示你不能调用在协议之外的方法或者属性.
```Swift
let protocolValue: ExampleProtocol = a
print(protocolValue.simpleDescription)
//print(protocolValue.anotherProperty) 这里是因为虽然a是class对象但是protocolValue还是协议对象，不能调用协议之外的值
```
----
### 错误处理
- 使用Error协议的类型来表示错误：
```Swift
enum PrinterError: Error {
    case outOfPaper
    case noToner
    case onFire
}
```
- 使用 throw 来抛出一个错误和使用 throws 来表示一个可以抛出错误的函数。如果在函数中抛出一个错误，这个函数会立刻返回并且调用该函数的代码会进行错误处理
- 一种方式是使用do-catch。在do代码块中，使用try来标记可以抛出错误的代码。在 catch代码块中，除非你另外命名，否则错误会自动命名为error
- 另一种处理错误的方式使用try?将结果转换为可选的。如果函数抛出错误，该错误会被抛弃并且结果为nil。否则，结果会是一个包含函数返回值的可选值
----
### 泛型
- 在尖括号里写一个名字来创建一个泛型函数或者类型。
- <T: Equatable> 和 <T> ... where T: Equatable> 的写法是等价的