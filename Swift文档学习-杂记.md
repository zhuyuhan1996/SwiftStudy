--------------------------------------------
使界面进行旋转的方式
- 通过stack可以讲UI界面组合到一起，在分开，这是对界面进行旋转很重要的一步。
- embed in stack可以进行stack操作，并设置为标准间距，设置上左右间距。
- 设置合适的大小，使用最右下角三角符号。最后再对两个UI进行合适的间距设置。
--------------------------------------------
- 怎么进行小数的计数，整数为..<，小数是：stride，例子：

```
for i in stride （from 0.5,through: 15.25,by: 0.3）{
}
```
- 是一个闭环的计数范围。to：为开环。
--------------------------------------------
tuples 元组变量 
- 类似与一个变量组合，可以同时传递多个变量值,可以在定义的时候定义别名

```
let x: (w:String, i:Int, v:Double) = ("hello",5,0.85)
```
- 利用tuples可以返回多个值，这将非常方便，Swift中函数只能返回一个值，，一般不会在tuples中使用数组下标这一方式访问数值。
- 当我们需要执行小的功能时，可以使用get和set，当需要设计很大的功能时，最好编写函数功能。
---------------------------------------------
访问控制
- internal 缺省类型，可以被任何对象访问。
- private 只有当前的对象可以访问。
- private(set) 可以被其他对象读但是不能写。
- fileprivate 可以被当前源文件内的所有代码访问。
- public 只针对框架，可以被外部对象使用
- open 只针对框架，外部对象可以继承。
----------------------------------------------
assert
- 断言，一个断言的判定条件必须是true，如果满足，则程序继续执行，如果不满足则代码停止。

```
assert(number > 3, "number 不大于3")
```
----------------------------------------------
extensions 扩展
[link](https://www.jianshu.com/p/0c963bc2194c)
- 添加计算实例属性和计算类型属性；定义实例方法和类型方法；提供新构造器；定义下标；定义和使用新的嵌套类型；使现有类型符合协议；

```
extension SomeType {
    // new functionality to add to SomeType goes here
}
```
- 如果定义扩展向现有类型添加新功能，那么该新功能将在该类型的所有现有实例上可用，即使它们是在定义扩展之前创建的。
- 扩展可以添加新的计算属性，但它们不能添加存储属性，或向现有属性添加属性观察者.
---------------------------------------------
Optional [link](https://www.jianshu.com/p/8b622333d6db?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation)
- enum [link](https://www.jianshu.com/p/6b180ef4c23e)枚举类型。可以不使用全部的名称，常与switch一起使用，如果不想做任何事，则使用break进行跳出，如果想要剩下的所有都执行相同操作，可以使用default
- 可以调用enum属性后的值

```
case .fries(let size): print("a \(size) order of fries!")
```
- 使用mutating可以修改enum中self的值，因为enum没有存储属性，所以只有在写的时候才可以进行修改。

```
enum Optional<T> {
    case some(T)   //对于所有成功的情况，我们用case some，并且把成功的结果保存在associated value里；
    case none        对于所有错误的情况，我们用case none来表示；
}
```
-------------------------------------------------
数据结构
- class：支持面向对象的设计，采用引用计数的方式存储在堆上
- struct
- enum
- protocol

--------------------------------------------------
引用 [link](https://www.jianshu.com/p/42c09c4bf6de)
- strong:当你声明一个属性时,它默认就是强引用
- weak:弱引用对象的引用计数不会+1, 必须为可选类型变量
- 在声明弱引用对象是必须用var关键字,不能用let.因为弱引用变量在没有被强引用的条件下会变为nil,而let常量在运行的时候不能被改变
- unowned:相当于__unsafe_unretained, 不安全. 必须为非可选类型.
- unowned引用是non-zeroing(非零的),在ARC销毁内存后，不会被赋为nil, 这表示着当一个对象被销毁时,它指引的对象不会清零.也就是说使用unowned引用在某些情况下可能导致dangling pointers(野指针).所以在访问无主引用的时候，要确保其引用正确，不然会引起内存崩溃.

--------------------------------------------------
mutating [可变的](https://www.jianshu.com/p/14cc9d30770a)
- Swift中protocol的功能比OC中强大很多，不仅能再class中实现，同时也适用于struct、enum。使用mutating关键字修饰方法是为了能在该方法中修改struct或是enum的变量，在设计接口的时候，也要考虑到使用者程序的扩展性。所以要多考虑使用mutating来修饰方法。
- 对于一般情况的var，Swift知道它是一个变量，因此不需要设置为mutating
- 为什么要用struct而不是class，是因为struct是值类型，class是引用类型，这样不会造成野指针的情况。

--------------------------------------------------
protocols [协议](https://www.jianshu.com/p/e386737754d1)
- 作为Swift中的一种自定义类型，和struct，class、enum不同，我们使用protocol来定义某种约定，而不是某一个具体的类型，这种约定通常用于表示某些类型的共性
- 在Swift中，定义一个协议需要实现所有的对象和方法，在OC中不是必须的，需要标记为@objc
- 支持多继承，在一个class创建一个protocol，init需要被标记为[required](https://www.jianshu.com/p/09c6c88ed61e)。
- protocol可以被class，struct，enum同时继承，会有不同的实现方式。
- countableRange，序列和聚集。字典就是一个聚集。
- 可以用extension扩展一个protocol，同时，利用协议可以的这种方式可以称之为功能性编程。

--------------------------------------------------
string
- 在string中，string。startIndex返回一个字符串位置类型，offsetBy是向后移动几位。采用index(of: "")可以找到相关字符所在的位置。同时..<是一个字符串位置的范围。

```
for c in s { }
```
- 注意使用offset和remove(at: )

--------------------------------------------------
[NSAttributedString](https://blog.csdn.net/qq_14920635/article/details/76318309)
- 每一个字符都有一个小的属性与之联系。1.多样式的显示富文本信息2.可用于图文混排，借助NSTextAttachment。3.一条语句代码（属性字典）可以设置多个属性。
- 相当于设置一个字符串中的属性，大小，颜色等等。
- 创建一个可变的，需要使用NSMutableAttributedString
- 可以定义一个变量为一个功能。

```
var operation: (Double) -> Double
operation = sqrt
let result = operation(4.0)
```
- 这里用一个double返回一个double

--------------------------------------------------
Closures [闭包](https://www.cnblogs.com/FBiOSBlog/p/7593921.html)
- 当我们创建功能，但是功能不存在时，就需要自己进行定义。类似于一个内联功能。就是将方法的实现直接传递给function名
- Swift自动为内联闭包提供简写参数名称，可用于通过名称$ 0，$ 1，$ 2等引用闭包参数的值。
- 如果在闭包表达式中使用这些简写参数名称，则可以从其定义中省略闭包的参数列表，并根据预期的函数类型推断速记参数名称的数量和类型。 in关键字也可以省略，因为闭包表达式完全由其主体组成。

```
reversedNames = names.sorted(by: { s1, s2 in s1 > s2 } )
reversedNames = names.sorted(by: { $0 > $1 } )
```
- 是引用类型。会不断的改变引用值得大小

异常处理
- throws and catch

```
func save() throws
do {
    try context.save()
} catch let error {
    throw error
}
```
----
Any & AnyObject
- 一半是与传统的OC接口一起使用，你不知道它的具体类型，他可以是任何类型。可以承载任何类型的变量，AnyObject只能承载类。因此不能承载方法，需要先把他转化为一个具体类型。
- segue 链接另一个MVC
- 不能直接使用，因为不知道他的具体类型，因此需要先转化为一个已知类型。可以通过as？来转换格式
- 可以用as？将任何类型的值cast to 其他任何类型的值。当用父类的指针指向子类的对象，指针不能访问子类特有的方法，用as？可以进行转换。
----
NSObject
- 是所有OC类的基类。但是在Swift里不是必须要的。

NSNumber
- 可以包含所有的数据类型。并可以返回所需要的数据类型。

Date
- 不同的date有不同的表示方法，因此还有Calender、DateFormatter、DateComponent。
----
Views
- 是UIVIew的子类，代表了一个方形的区域
- 分层的：一个View只有一个父View var superview： UIView？，但是可以有多个子View var subview: [UIView]
- 只有一个UIWindow。
- 可以通过code来进行删除和增加view：

```
func addSubview (_ view: UIView)
func removeFromSuperview()
```
- 一般避免使用初始化。如果需要初始化，那么他们都要进行实现。

```
init(frame: CGRect)//如果是在代码创建
init(coder: NSCoder)//从面板得到。
```
- awakeFromNib()只能用于从面板得到的view
- CGFloat，对于view就需要用这个方法，而不是常规的double和float。
- CGPoint，点的坐标，为一个struct
- CGSize，长宽的值。
- CGRect包含了这两个值的struct。
- 原点在左上角，计量单位是点，而不是像素，一般一个点有两个像素，也可以有一个或者三个。
- frame包含在父view中。bounds就是原点和长宽，frame就是实际原点和点在现在坐标系中坐标，center为中心点坐标。
- 创建UIView可以使用draw和handle touch events，对于draw：override func draw(_ rect: CGRect),一定不要draw(CGRect)!!!如果想要redrawn，可以采用setNeedsDisplay()或者setNeedsDisplay(_ rect: CGRect)
- 可以利用UIBezierPath类来创建一系列的draw。UIGraphicsGetCurrentContext()给了draw的环境。

```
//define a path
let path = UIBezierPath()
path.move(to: CGPoint(80, 50))
path.addLine(to: CGPoint(140, 150))
path.addLine(to: CGPoint(10, 150))
path.close()
//画完后是不会有显示的，需要对线条进行设置
UIColor.green.setFill()
UIColor.red.setStroke()
path.linewidth = 3.0
path.fill()//得到绿色的填充
pth.stroke()//得到红色的线条。
```
- addClip() 截断。
----
UIColor
- 设置背景颜色：var backgroundColor: UIColor。颜色可以有透明度：let semitransparentYellow = UIColor.yellow.withAlphaComponent(0.5)。如果需要设置透明度，需要先设置：var opaque = false
- var layer: CALayer 代表了动画。
- 如果重叠了，那么底层的那个（数组中靠前的那个）就会有透明度的存在
- 写文字
```
let text = NSAttributedString(string: "hello")
text.draw(at: aCGPoint)
let textSize: CGSize = text.size
```
- 能够调整字体大小，就需要自动布局。按比例调整字体大小：scaledFont。

UIImageView
- 可以创建一个UIImage对象。
```
let image: UIImage = ...
image.draw(at point: aCGPoint)
image.draw(in rect: aCGRect)
image.drawAsPattern(in rect: aCGRect)
```
----
bounds change
- var contentMode: UIViewContentMode 

description 描述
- 在我们打印对象的时候，会直接输出对象的地址，可以采用description方法，输出对象的属性。
- 在旋转时需要将界面也进行旋转，因此需要设置content Mode为redraw
- [UIBezierPath](https://www.jianshu.com/p/5abd2da87e94)：使用UIBezierPath可以创建基于矢量的路径。使用此类可以定义简单的形状，如椭圆、矩形或者有多个直线和曲线段组成的形状等。主要用到的该类的属性包括
- 一般0代表了你想要多少的数据自己设置。numberOfLines
- 通过isHidden，可以把View放在合适的位置，但是隐藏起来。
- 可以通过transform进行旋转，只有rotate、tranform、scale三种方法。



------------
现在的Swift视频对我来说难度有点大了，我有点云里雾里的了，听不太懂他在讲什么了，决定先看看中文文档，再进一步学习视频所讲述的东西。