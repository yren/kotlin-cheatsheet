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