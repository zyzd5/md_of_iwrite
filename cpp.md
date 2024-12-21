* `翻译单元`: 是指编译之前, 编译器处理好的即将要编译的代码文件
* R字符串: R"(原始字符串)";
## constexpr
## round() ceil() floor()
* round(double num)
    * 四舍五入到最接近的整数
* ceil(double num)
    * 向上取整
* floor(double num)                                                        
    * 向下取整
## random number
```cc
std::random_device rnd;
std::uniform_int_distribution<int> dist(1, 6);

std::cout << dist(rnd) << std::endl;
```
## regex
## enum class
* 传统 `enum` 会将所有枚举值暴露在外部作用域, `enum class` 将枚举值限定在自身的作用域中, 从而避免冲突
```cc
enum class ErrorCode { NotFound, PermissionDenied, Unknown};
enum class Status { Success, NotFound, Running};
```
## vector 
* `vector` 有 `大小` 和 `容量` 两个概念, 当大小超过容量后, vector 会通过重新 `allocate` 来改变其容量, 这有可能会造成性能影响
### reserve()
* `$vector.reserve()`: 用于预先分配动态数组的内存空间，以提高容器在插入元素时的效率

* reserve 只改变 capacity，不会影响当前的元素个数（size）。调用 reserve 后，vector 的 size() 仍然保持不变，只有 capacity() 会变大

* `reserve` 主要用于需要大量添加元素的场景, 当你知道插入元素的数量时, 可以使用 `reserve` 来避免内存重新分配和元素拷贝
    
## void*
* 通用指针

* 不可解引用, 由于 void* 不知道指向对象的类型, 所以不能访问其指向的内容

* 使用前必须要强制转换
## 三路比较运算符 (C++20)(懒得看, 以后再看)
## lambda
* lambda 的本质上是, 编译器创建了一个匿名类, 在类中实现了operator()的重载

* operator() 函数默认使用 const 修饰, 在说明符中添加 `mutable` 可以使成员可被修改
### 闭包对象
* 是指由 lambda 表达式生成的对象, 包括被捕获的变量的引用(或副本), lambda 的函数体

* 每个 lambda 表达式在编译时都会生成一个独一无二的匿名类, 闭包对象就是这个类的一个实例

* 无状态的闭包对象是指 这个 lambda 表达式没有捕获任何变量, 只是一个简单的函数对象

* 只有`不带有捕获变量的 lambda 表示式`, 可以当作函数对象被传入函数, `带有捕获变量的 lambda 表达式`可以使用 `\<functional>` 或者 `模版` 的方式来使用
### +运算符
* 当对 lambda 表达式使用 `+` 运算符时, 它将会将 lambda 对象隐式转换为一个指向函数的指针

* 这仅适用于没有捕获外部变量(也叫无状态)的 lambda 表达式, 这样的 lambda被视为纯函数, 可以直接被转换为函数指针
### 捕获
* `[&]`: 按引用捕获被使用的自动变量
* `[=]`: 按复制捕获被使用的自动变量
```cc
int i = 9;
auto func = [=, &i] {}
// 按值捕获, 但是 i 按引用捕获

int x = 8;
auto func = [&, x] {}
// 按引用捕获, 但是 x 按值捕获
```

## std::boolalpha
* 在标准流输出时, 不设置 boolalpha 时, 输出 `true` 和 `false` 默认输出 `0`/`1` 
* 在`std::cout << std::boolalpha << ` 后, 就能输出 `true` 和 `false` 为 `true`/`false` 
## fstream
```cpp
#include<fstream>

std::fstream file(file_name, option)       //option: ios::in, ios::out, ios::app，
//ios::in   :拥有读权限
//ios::out   :拥有写权限
//ios::in   :拥有写权限，写入时为在文件末尾写入

//没有验证过, 在option的部分可以使用(ios::in, ios::out), 也就是使用括号括起来, 或者使用ios::in | ios::out 来选择选项

//还有其他的随用随查

//在ios::前都要加std::
std::fstream file(file_name)     
//不写选项时默认为ios::in, ios::out

std::ifstream file(file_name)
//不写选项时默认为只有读权限

std::ofstream file(file_name)
//不写选项时默认为只有写权限

if (!file.is_open())            
    std::cout << "error opening" << std::endl;
//判断是否正常打开

file.read(file_text, string_size)  
//读入的值传入file_text，大小为string_size
//string_size可以写为sizeof(file_text)

file >> file_text;      //读入的值传入file_text

while (file.get(character))      
//使用get函数读入到character,character为char类型

while (file.getline(char store_char[size], size))
    std::cout << store_char;     
//使用fstream下成员函数getline读入到store_char,store_char为char[]类型，而不是char*类型,size为一个int类型的数字

while(std::getline(file, file_text))
    std::cout << string;     
//使用标准库中getline函数读入,file为fstream对象，file_text为string类型

flie.write(file_text, string_size)
//写入的值传入file_text，大小为string_size
//string_size可以写为sizeof(file_text)

file << "helloworld";   //文本写入file
```
## key word
## explicit
```cpp
explicit                
//意为明确的，只能在构造函数中使用，禁用创建实例时的隐式转换
```
### variant
```cpp
#include<variant>

std::variant<std::string, int> data;
data = "zyzds";
data = 5;
std::get<int>(data);     //返回int类型的data值

data = "helloworld";
data.index()            //返回当前data的index值，与类型相关，第二次赋值string型数据仍返回0

get_if<std::string>(&data)      //返回一个指向data的指针，如果错误则返回空指针

if (auto pointer = std::get_if<std::string>(&data))
    std::cout << "variant value: " << *data << std::endl;
else                                                //判断类型是否正确
    std::cout << "invaild value" << std::endl;


    //实现方式
    std::variant<int, std::string, int> data;

    std::cout << sizeof(int) << std::endl;          //输出4
    std::cout << sizeof(std::string) << std::endl;  //输出32
    std::cout << sizeof(data) << std::endl;         //输出40
    //所以实现方式是储存了每一个可能出现的类型大小，所以性能不如union，但是仍然好用

```
### inline        
* 内联函数`或内联变量(C++17)`
    * 内联函数中, 所有函数定义的局部静态对象在所有翻译单元中共享 
    * 当在不同文件中定义的值不同时, 编译器会随机使用一个值

* 内联命名空间
    * 将使用 inline 关键字声明的命名空间中的成员可以在上层被访问
> inline 关键词的本意是作为给优化器的指示器，以指示优先采用函数的内联替换而非进行函数调用，即并不执行将控制转移到函数体内的函数调用 CPU 指令，而是代之以执行函数体的一份副本而无需生成调用。这会避免函数调用的开销（传递实参及返回结果），但它可能导致更大的可执行文件，因为函数体必须被复制多次
>
>因为关键词 inline 的含义是非强制的，编译器拥有对任何未标记为 inline 的函数使用内联替换的自由，和对任何标记为 inline 的函数生成函数调用的自由。这些优化选择不改变上述关于多个定义和共享静态变量的规则
>
>由于关键词 inline 对于函数的含义已经变为“容许多次定义”而不是“优先内联”，因此这个含义也扩展到了变量
>(cppreference.com)

(C++17 起)
### noexcept
* 使用 noexcept 的好处
    * 编译器不会为该函数建立异常处理相关的代码, 这有助于提高性能
    * 当编译器认定函数有可能会抛出异常后, 编译器会建立异常处理机制, 包括建立和拆卸栈帧, 异常传播
    * 当真的抛出异常时, 编译器会确保正确地进行栈展开, 这意味着在 func 退出时, 所有局部变量的析构函数都会被调用, 以免资源泄漏
#### noexcept 运算符
```cpp
noexcept($expression)
```
* noexcept 运算符进行编译时检查，如果表达式被标记为 `noexcept`, 则返回 `true`, 否则返回 `false`
* 在运算符中的表达式并不会真的被执行, 仅仅只进行检查是否有标记
#### noexcept 说明符
* C++17前不是函数类型的一部分
* C++17后是函数类型的一部分

* noexcept 在 C++17 后是函数类型的一部分, 但是不能作为函数重载的依据(不能将函数重载为有noexcept说明符和没有的版本)

* 当在函数后添加说明符时, 基本上是给编译器做了一个保证, 保证这个函数不会出错, 当函数出错时, 就会调用标准库中的 terminate 函数来终止程序

* 当函数声明为 `void func() noexcept` 和 `void func() noexcept(true)` 时, 它们等价
* 当函数声明为 `void func()` 和 `void func()` 时, 它们等价

#### noexcept 和 throw
* C++11: 相同的结果, 不同的机制
* C++17: 相同的结果和机制(noexcept 成为了 throw 的别名)
* C++20: 移除 throw
## cout 
## 四舍五入
 
## iomanip
### 控制精度
* std::fixed << std::setprecision(`num`)
    * 在直接使用 `std::setprecision()` 时, 会将所有数字算在精度中
    * 使用 `std::fixed << std::setprecision()` 时, 只会限制小数点后的精度

```cc
std::cout << std::fixed << std::setprecision(`num`) << `value` << std::endl;
```
#### 十进制, 八进制, 十六禁进制
* std::dec -> 8 进制 
* std::oct -> 10 进制
* std::hex -> 16 进制

```cc
std::cout << `std::dec` << `num` << std::endl;  
std::cout << `std::oct` << `num` << std::endl; 
std::cout << `std::hex` << `num` << std::endl; 
```
#### 填充和宽度
* std::setw(10)
* std::setfill('*')

```cc
std::cout << std::setw(10) << std::setfill('*') << 42 << std::endl; 
// 输出: ********42
```
#### 对齐
* std::left
* std::internal
* std::right
```cc
* std::cout << std::left << std::setw(10) << "left" 
    << std::right << std::setw(10) << "right" << std::endl;
```
## thread
```cpp
#include<iostream>
#include<chrono>
#include<thread>
int main()
{
    using namespace std::literals::chrono_literals;	// 引入线程头文件中的休眠部分

    auto start_time = std::chrono::high_resolution_clock::now();	// 得到开始时间
    auto end_time = std::chrono::high_resolution_clock::now();	// 得到结束时间
    
    std::this_thread::sleep_for(1s);	// 休眠1s
    
    std::chrono::duration<float> duration = end_time - start_time;	// 使用特殊类型得到经过时间
    
    std::cout << duration.count() << std::endl;		// 使用count方法打印出来
}
```
## optional
```cpp
#include<optional>          // C++ 17

std::optional<std::string> data = "helloworld";

data.value()                // 返回data的值
data.has_value()            // 返回bool值

if (data)
    cout << data.value() << endl;
else                    // 优雅的判断是否有值的方法
    cout << "empty" << endl;
```
