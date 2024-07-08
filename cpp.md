# fstream
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
## inline        
* 多重定义
    * 在C++17之前，inline关键字也用于解决链接问题。当一个函数或变量在多个编译单元中定义时，如果它被声明为inline，那么只要每个定义都相同，就不会出现多重定义错误。
    
    * 当在不同文件中定义的值不同时, 编译器会随机使用一个值

* 命名空间
    * 将使用 inline 关键字声明的命名空间中的成员可以被上次元素访问
```cpp
namespace Parent{
    namespace Child1{
        void func() {std::cout << "Child1::foo()" << std::endl;}
    }

    inline namespace Child2{
        void func() {std::cout << "Child2::foo()" << std::endl;}
    }
}
int main()
{
    Parent::Child1::func();
    Parent::func();
}
/*
output:
Child1::foo()
Child2::foo()
说明 Child2 作用域中的 func() 可以被 Parent 访问
*/
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
# tuple
```cpp
#include<tuple>
    std::tuple<std::string, int, int> person1 = {"zbxds", 19, 12345678};    //带等号的初始化方式

    std::get<1>(person)     //返回1号位元素，即19 

```
# vector
```cpp
std::vector<int> array(size, value);
// 创建一个大小为 size, 内容为 value 的矩阵 

std::vector<std::vector<int>> array(row, std::vector<int>(col, value))
// 创建一个大小为 row*col, 内容全为 value 的矩阵

std::vector<std::vector<int>> array(5, std::vector<int>(3, 2));
// 创建一个大小为 5*3, 内容全为2的矩阵
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
    // g++编译结果为1+0=1, 在clang或者msvc中可能会不一样
    // 写这种代码就是语义不清晰
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
# cout 
```cpp
std::cout.width(2);
std::cout << "1" << "2";         
// 控制下一项的缩进, 1 会缩进, 2 不会

#include<iomanip>

std::cout << year << "-";
std::cout << std::setw(2) << std::setfill('0') << month << "-";
// 设置填充和宽度

std::cout << std::fixed << std::setprecision(3) << sum << std::endl;
// 保留小数点后n位
```
# thread
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