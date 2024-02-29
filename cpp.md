# key word
## explicit
```cpp
explicit                
//意为明确的，只能在构造函数中使用，禁用创建实例时的隐式转换
```
## variant
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
# 代码优化
## 编译器选项
* 在编译器选项前加上 -O1 or -O2 or -O3

* 优化性能 -O0 -O1 -O2 -O3 从低到高
## 循环步长
```cpp
for (int i = 0; i < 50; i++)
    sum += i;
```
优化为
```cpp
for (int i = 0; i < 50; i++)
    sum += i + (i + 1) + (i + 2) + (i + 3);
```
# 左值和右值
粗略来说，  
左值是`可以通过地址`找到的变量  
右值是`不能通过地址`找到的常量
## 概念
```cpp
string first_name = "z"
string last_name = "yz"

string full_name = (first_name + last_name)
```

在这种条件下，等号左边的值全部是左值，等号右边的值都是右值  
>因为你不能通过地址寻找到"z"，"yz"，(first_name + last_name)这三个表达式的地址
#### 左值引用和右值引用
```cpp
//左值引用
int& i          

//右值引用
void print_value(int&& i)
{
    std::cout << i << std::endl; 
}
//只接受右值参数，如果放入左值会报错
```
# 结构化绑定
```cpp
#include<tuple>
    //绑定到元组
int main()
{
    std::tuple<std::string, int, int> Person = {"zyzds", 19, 123123123};
    
    auto[name, age, id] = Person;   //or auto[name, age, id](Person);

    std::cout << name << std::endl;
    //提供了一种便利的方法来访问成员变量
}
```
```cpp
    //绑定到结构体，类也同理
struct Human
{
    std::string name = "zyzds";
    int age = 19;
    int id = 123123;
};

int main()
{
    Human human;
    auto[name, age, id] = human;
    std::cout << name << std::endl;         
                                            //确实用来访问结构体好蠢
}                                   
```
# tuple
```cpp
#include<tuple>
    std::tuple<std::string, int, int> person{"zyzds", 19, 22219131139}; //不带等号的初始化方式
    std::tuple<std::string, int, int> person1 = {"zbxds", 19, 12345678};    //带等号的初始化方式

    std::get<1>(person)     //返回1号位元素，即19 

```
# unordered_map
```cpp
std::unordered_map<type, type> map;

map.find(key)   //返回key对应的键值对的迭代器
        //没有找到则返回map.end()对应的迭代器

map.at(key)     //返回key所在的value值，不存在则报错

map.emplace(key, value) //往map中插入值，性能比insert更优

std::unordered_map<int, int>::iterator //迭代器的类型
iterator->first //访问键值对的key
iterator->second //访问键值对的value
```
# 参数计算顺序
```cpp
#include<iostream>

int getSum(int a, int b)
{
    std::cout << a << "+" << b << "=" <<(a+b) << std::endl;
}   
int main()
{
    int value = 0;
    getSum(value++, value++);
    //g++编译结果为1+0=1, 在clang或者msvc中可能会不一样
    //写这种代码就是语义不清晰
}
```
# enum
* `enum` 是一种用于定义一组命名`整数常量`的方式
```cpp
enum Example
{
    A, B = 5, C
//A, B, C 不需要提前定义
};
Example num
switch (num)
{
    case A:
    //something
    break;
    default:
}
//or 
if (num = A)
{
    //something
}
```
# cout 和 cerr
* std::cerr 和 std::cout 都是输出流对象，用于向控制台输出信息。它们之间的主要区别在于输出的流：
    
    * std::cerr 是标准错误流，用于输出错误消息。与 std::cout 不同，std::cerr 的输出不会被缓冲，这意味着它们会立即被发送到终端，即使在程序崩溃时也是如此。这使得 std::cerr 适用于输出严重的错误消息，即使程序发生崩溃，也能及时获得相关信息。

    * std::cout 是标准输出流，用于一般输出。它的输出会被缓冲，因此输出不会立即显示在终端上。相比之下，std::cout 的缓冲可以提高程序的性能，但在某些情况下，如需要立即查看输出结果时，可能会造成延迟。
# cout 
```cpp
std::cout.width(2);
std::cout << "1" << "2";         
// 控制下一项的缩进, 1 会缩进, 2 不会

#include<iomanip>

std::cout << year << "-";
std::cout << std::setw(2) << std::setfill('0') << month << "-";
// 设置填充和宽度

// cout.width() 和 std::setw() 类似, setw 来自 <iomanip>, 可以在流中插入
```
# thread
```cpp
#include<iostream>
#include<chrono>
#include<thread>
int main()
{
    using namespace std::literals::chrono_literals;	//引入线程头文件中的休眠部分

    auto start_time = std::chrono::high_resolution_clock::now();	//得到开始时间
    auto end_time = std::chrono::high_resolution_clock::now();	//得到结束时间
    
    std::this_thread::sleep_for(1s);	//休眠1s
    
    std::chrono::duration<float> duration = end_time - start_time;	//使用特殊类型得到经过时间
    
    std::cout << duration.count() << std::endl;		//使用count方法打印出来
}
```
# optional
```cpp
#include<optional>          //C++ 17

std::optional<std::string> data = "helloworld";

data.value()                //返回data的值
data.has_value()            //返回bool值

if (data)
    cout << data.value() << endl;
else                    //优雅的判断是否有值的方法
    cout << "empty" << endl;
```