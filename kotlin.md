## by
* `by` 可以将一个对象的属性操作委托给另一个对象来处理, 当你使用 `by` 关键字时, Kotlin 自动为你处理一些重复的代码逻辑, 将属性的访问和修改操作交给委托对象
```kotlin
class Example {
    var value: String by AnotherClass()
}
```
* value 属性的 `get` 和 `set` 操作会被委托给 `AnotherClass` 的对象来处理
## lambda
```kotlin
val sum = { x: Int, y: Int -> x + y }
```
### it 关键字
* 当 lambda 表达式只有一个参数时，Kotlin 提供了简写形式，默认参数名为 it，不需要显式声明参数
```kotlin
val printMessage = { message: String -> println(message) }
// 等价于:
val printMessageSimplified = { println(it) }

fun main() {
    printMessage("Hello, Kotlin!")
    printMessageSimplified("Hello again!")
}
```
### 和 it 关键字结合使用
```kotlin
val numbers = listOf(1, 2, 3, 4, 5)

// 使用高阶函数 `map` 和 lambda 转换集合
val doubled = numbers.map { it * 2 }
println(doubled)  // 输出: [2, 4, 6, 8, 10]

// 使用高阶函数 `filter` 和 lambda 过滤集合
val evenNumbers = numbers.filter { it % 2 == 0 }
println(evenNumbers)  // 输出: [2, 4]
```
## 简洁的 for
```kotlin
for (i in 1..5) 
{
    println(i + " ");
}
```
## when 
* 类似 `switch-case`, 但是更加灵活
* 可以代替 `if-else` 

* 按值匹配
* 匹配类型
```kotlin
fun describe(obj: Any): String =
    when (obj) {
        1          -> "One"
        "Hello"    -> "Greeting"
        is Long    -> "Long number"
        !is String -> "Not a string"
        else       -> "Unknown"
    }
```
* 作为`表达式`
```kotlin
val result = when (x) {
    1 -> "x is 1"
    2 -> "x is 2"
    else -> "x is neither 1 nor 2"
}
println(result)  
```
* 作为`语句`
```kotlin
when (x) {
    1 -> println("x is 1")
    2 -> println("x is 2")
    else -> println("x is neither 1 nor 2")
}
```
* bool 表达式分支
```kotlin
when {
    x % 2 == 0 -> println("x is even")
    x % 2 != 0 -> println("x is odd")
}
```
* 多条件匹配
```kotlin
val result = when (x) {
    0, 1 -> "x is 0 or 1"
    else -> "x is something else"
}
```
* 范围操作
```kotlin
val result = when (x) {
    in 1..10 -> "x is in the range"
    !in 10..20 -> "x is outside the range"
    else -> "x is something else"
}
```
