观察者模式（Observer Pattern）
是一种设计模式，用来描述一对多关系：一个对象发生改变时将自动通知其他对象，其他对象将相应做出反应。这两类对象分别被称为被观察目标（Observable）和 观察者（Observer），也就是说一个观察目标可以对应多个观察者，观察者可以订阅它们感兴趣的内容，当观察目标内容改变时，它会向这些观察者广播通知（调用 Observer 的更新方法）。有一点需要说明的是，观察者之间彼此时互相独立的，也并不知道对方的存在。

响应式编程（Reactive Programming）
是一种编程思想，相对应的也有面向过程编程、面向对象编程、函数式编程等等。不同的是，响应式编程的核心是面向异步数据流和变化的。

Combine
官方文档：

The Combine framework provides a declarative Swift API for processing values over time. These values can represent user interface events, network responses, scheduled events, and many other kinds of asynchronous data.

By adopting Combine, you’ll make your code easier to read and maintain, by centralizing your event-processing code and eliminating troublesome techniques like nested closures and convention-based callbacks.

是基于泛型实现的，是类型安全的。



combine提供三个Subscriber: Sink, Assign, Subject.

Sink 是非常通用的 Subscriber，我们可以自由的处理数据流的状态。

在初始化的时候，需要定义类型，因为是协议式编程，不然会报错。

Assign 可以很方便地将接收到的值通过 KeyPath 设置到指定的 Class 上（不支持 Struct），很适合将已有的程序改造成 Reactive。

Subject 有些时候我们想随时在 Publisher 插入值来通知订阅者，在 Rx 中也提供了一个 Subject 类型来实现。Subject 通常是一个中间代理，即可以作为 Publisher，也可以作为 Observer.

有三个已经实现的 Subject: AnySubject，CurrentValueSubject 和 PassthroughSubject 

CurrentValueSubject 的功能很简单，就是包含一个初始值，并且会在每次值变化的时候发送一个消息，这个值会被保存，可以很方便的用来替代 Property Observer。在上例中，以前需要实现 delegate 来获取变化，现在只需要订阅 content 的变化即可，并且它作为一个 Publisher，可以很方便的利用操作符进行组合变换。类似于BehaviorRelay。

PassthroughSubject 和 CurrentValueSubject 几乎一样，只是没有初始值，也不会保存任何值。

CurrentValueSubject 相对于 PassthroughSubject, 是沒有.send(), 取而代之的是一个 value, 就像是 didSet 的方式。

操作符

map 将收到的值按照给定的 closure 转换为其他值，mapError 则将错误转换为另外一种错误类型。

replaceNil 将收到的 nil 转换为给定的值。

scan 将收到的值与当前的值（第一次使用 initialResult ）按照给定的 closure 进行转换。