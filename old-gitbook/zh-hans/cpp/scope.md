#### 作用域

##### 命名空间

+ 推荐使用匿名命名空间来避免命名冲突，虽然违背了唯一定义原则
+ 不要声明命名空间 `std` 下的任何内容
+ 避免使用 `using`，确保命名空间下所有名称都可用
+ 适当使用命名空间别名简化定义 `namespace fbz = ::foo::bar::baz;`

留有适当的注释

```cpp
namespace foo {
enum {UNUSED, EOF, ERROR };
bool AtEof() { return pos_ == EOF; }
} // namespace foo
```

> 笔者的注释略有不同

```cpp
namespace bar {
class MyClass {
};
} /* namespace: bar */
```

##### 嵌套类

+ 推荐使用命名空间代替嵌套类
+ 尽量不要定义成 `public`，除非接口需要

##### 函数

+ 有时不把函数限定在类实体中是有益的
+ 单纯封装若干不共享任何静态数据的静态成员函数而创建的类，不如使用命名空间
+ 全局函数不如使命命名空间的非成员函数或静态成员函数
+ 独立的命名空间或新类可以解决跨编译单元调用的函数所引入的耦合和依赖

##### 局部变量

+ 尽可能的使用最小作用域，距离使用越近越好，最好初始化跟赋值在一起
+ 如果变量是在循环体中的对象，频繁的构造和析构是低效的，应放到循环外面声明

##### 全局变量

+ 禁止类(含 STL)、多线程、函数返回初始化全局变量
+ 内建类型和只有内建类型构成的结构体可以使用
+ 单例类可考虑使用类的全局变量
+ 字符串常量只能使用 `const char []`

##### 小结

规范作用域除了考虑名称污染、可读性之外，主要是为降低耦合，提高编译/执行效率。

