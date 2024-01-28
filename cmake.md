```cmake
cmake_minimum_required(VERSION 3.22.1)
# version

project(Project_name)

add_executable(main main.cpp ./Hello/hello.cpp ./World/world.cpp)
# 第一个参数为主要可执行程序, 后面的为可执行程序的依赖项

target_include_directories(main PUBLIC world)
# 第一个参数是可执行文件, 第二个参数为选项, 第三个参数为搜索目录
```