* val: read-only
* var: read and write
```kotlin
val num = 8;                
// cant modify

var str = "helloworld";      
str = "i am the storm that is approaching";
// it worked
```

* 字符串中使用 $ 提示变量
```kotlin
var str = "helloworld";
println("here is a str: $str");
```

* for
```kotlin
for (i in 1..5) 
{
    println(i + " ");
}
```