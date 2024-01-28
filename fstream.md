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