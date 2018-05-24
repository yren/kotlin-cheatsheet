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