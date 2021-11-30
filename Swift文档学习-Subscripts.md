# Subscripts

下标脚本可以定义在class、structure、enumeration中，可以认为是访问对象、集合、序列的快捷方式，不需要再调用实例的特定的赋值和访问方法。

同一个目标可以定义多个下标脚本，通过索引值的不同来进行重载。

可以传入一个或者多个索引值来进行实例的访问和赋值，语法类似于实例方法和计算属性的混合。

```swift
subscript(index: Int) -> Int {
  get {
  // 返回与入参匹配的Int类型的值
  }
  set(newValue) {
  // 执行赋值操作
  }
}
```

