# kotlin introduce 101
## source
* http://toughcoder.net/blog/2018/05/17/introduction-to-kotlin-programming-language

## Hello kotlin, 你的第一行 kotlin code
* 文件扩展名字 `*.kt`, hello.kt

```
package hello

fun main(args: Array<String>) {
    println("Hello kotlin")
}
```

* 编译源码，得到 hello.jar 文件

```
kotlinc hello.kt -include-runtime -d hello.jar

## -h 查看 kotlinc 帮助
kotlinc -h 
```

* 运行 hello.jar, 编译得到了标准的 java jar 文件。

```
java -jar hello.jar
```

## The baisc

### 语句结构
* 一行语句，结尾不用分号
* 缩进不强制，一般与 java 相同，4个空格缩进
* 语句使用大括号 {}

### 变量
* `var` 声明变量， `val` 声明常量
* kotlin 是`静态强类型语言` （每个变量在编译时需要知道类型), 变量声明需要带上类型。格式 `var str: String`, 如果声明时直接赋值, 编译器会根据 context 推到出类型, 可以不加类型。

例子：
```
var str: String
val i: Int
// str 类型由编译器推导, 可以不加类型
var str = "Hello kotlin"
```

### 语句和表达式
* 表达式有值，可以放在变量赋值的右边。 语句没有值，不能放在赋值右边。

### 注释

* 与 java 相同， 单行注释 `//` ， 多行注释 `/*   */`

### 函数
* 用 `fun` 定义函数, 格式 `fun 函数名(参数): 返回值 {函数体}`

例子：
```
fun foo(name: String): Int {
    return name.length()
}
```

* 参数可以有默认值，调用函数值可以加上参数名字, 增加可读性。

例子:

```
fun foo(name: String, num: Int = 42, flag: Boolean = false) {
    //
}
```
函数调用可以指定参数名字增加可读性

```
foo("a")
foo(name = "b", number = 1)
```

* 如果函数只有一个表达式, 且有返回值, 可以不用 {}, 直接把他放在函数后面，例子:

```
fun foo(name: String): String = name.toUpperCase()

// 可以去掉返回类型，类型可以推导得到
fun foo(name: String) = name.toUpperCase()
```

* 与 java 不同， kotlin 中函数是和 class 一个级别的，`fun` 可以不在任何类中。函数可以赋给变量。 在 kotlin 中函数式一等公民。

### 类和对象

* 用 `class` 声明类型， 用分号 `:` 来继承父类或实现接口， `不用 new` 来创建对象. 例子:

```
class Person {
    var name: String
    var age: Int
}
```
 
* 空类可以省略 `{}` ， 例子:

```
class Person
```

* 创建对象, 例子:

```
var someone = Person()
```

### Primary constructor

* 构造方法，有所谓的 primary constructor, 可以直接写在类名后面, 例子:

```
class Person constructor(name: String)

// constructor 可以省略
class Person(name: String)
```

* primary constructor 的初始化工作在 initializer block, 例子:

```
class Person(name: String) {
    var firstName = name
    init {
        println("fist init block print ${name}")
    }
}
```

* 如果声明的属性在 primary constructor 中有赋值, 可以写为:

```
class Person(var name: String, var age: Int)

// 等价于

class Person(name: String, age: Int) {
    var name = name
    var age = age
}
```

* 如果 primary constructor 前面有属性声明，或 annotation 的话， `constructor` 关键字不能省略.

```
class Person public @Inect constructor(var name: String)
```

### Secondary constructor
* 除了 primary constructor 外, 还可以声明其他 constructor, 即 secondary constructor

```
class Person(var name: String) {
    constructor(name: String, parent: Person): this(name) {
        parent.addChild(this)
    }
}
```

* secondary constructor 需要 delegate 到 primary constructor 上, 就是 primary 会在 secondary 之前执行。 init block 是在 primary constructor 中执行的。 如果没有显示的 primary constructor 声明，编译器会生成默认的 primary constructor, 并默认 delegate 到 secondary constructor 上面。例子:

```
class Person {
    init {
        println("init block")
    }
    
    constructor(i: Int) {
        println("second constructor")
    }
}

fun main(args: Array<String>) {
    val c = Person(1)
}
```

### 属性和方法
* kotlin 为属性生成默认的 getter 和 setter
```
class Person(var name: String, var age: Int)

val p = Person("tom", 3)

p.getName()
p.setAge(5)
```

### 定义类方法
* 和普通 `fun` 声明一样, 只是放在类里面

```
class Person(var name: String, var age: Int) {
    fun report() = "My name is $name, age $age"
}
```

* 覆写父类的方法，加上 `override` 

```
class Dog(var name: String): Animal {
    override fun yell() = "Yell from $name"
}
```

### 访问权限
* 与 java 类似，分为 `public`, `protected`, `private`, `internal`, 前 3 个与 java 相同, 只是默认值不同, java 默认  package scope, kotlin 默认 public scope.  `internal` 是 `module` 内部可见, module 定义和 package 不同， module 是一组编译在一起的 kotlin 文件， 简单理解 module 比 package 范围大。

* kotlin 中类默认不可继承, 即 final class, 如果需要继承需要声明是加上 `open` 

### String
* 与 java 中类似， kotlin 中可以用 `$` 将变量嵌入字符串中

```
var msg = "hello"
println("we got message $msg")
```

### lambda 表达式
* 高阶函数的概念, 高阶函数即将别的函数作为参数或返回值的函数. lambda 表达式就是为高阶函数方便使用而生

* 简单的讲, lambda 表达式即没有名字的函数。例如 `{a,b -> c}`

```
var sum = {x: Int, y: Int -> x + y}
```

* 当 lambda 是最后一个参数，传给函数时，可以把 lambda 表达式写在参数外面

```
var product = item.fold(1) {acc, e -> acc * e}
```

* 当 lambda 是唯一参数，参数括号可以省略

```
run { println("hello, kotlin") }
```

* 当 lambda 只有一个参数，参数可以省略

```
eval {x * x}
```

### 函数类型
* kotlin 中函数也是变量， 它也有类型。 形式 `(a, b) -> c` 括号内是参数类型, c 是返回类型

```
var sum: (Int, Int) -> Int = {x, y -> x + y}
var square: (Int) -> Int = {x -> x * x}
```

* 声明高阶函数时有时需要函数类型

```
fun walk(f: (Int) -> Int)

// Unit 相当于 void, 即无返回值
fun run(f: () -> Unit)
```

### 集合
* 大部分和 java 相同，添加了一些函数式操作，代码更简洁
* 遍历, 过滤, 映射, 排序, 折叠, 分组, 归类

```
fun collectionCase() {
    val list = listOf("Apple", "Amazon", "Ali", "Facebook")
    
    //遍历
    list.forEach {println(it)}
    
    //过滤 返回条件为 true 的
    var short = list.filter { it.length < 6 }
    
    //把列表元素映射为另一种元素, [5, 6, 3, 8]
    var lenList = list.map {it.length}
    
    // 按某条件进行排序
    var orderList = list.sortBy {it.length}
    // 折叠
    var joint = list.fold("", {partial, item -> if })
    // 分组
    var (first, second) = list.partition {it.length < 6}
    // 归类，返回一个 map, {5=[apple], 6=[Amazon]}
    var bucket = list.groupBy {it.length}
}
```