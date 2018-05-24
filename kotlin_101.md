# kotlin introduce
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
* kotlin 是`静态强类型语言`