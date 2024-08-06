* `翻译单元`: 是指编译之前, 编译器处理好的即将要编译的代码文件

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
# optional
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
# ::std::
* 基本上, 这种符号的意义为: 优先从全局作用域中搜索
```cpp
int x = 10; 

void func() {
    int x = 20; 
    std::cout << x << std::endl; // 20
    std::cout << ::x << std::endl; // 10
}
```
