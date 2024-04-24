```bash
# 配置项目
cmake -S . -B build

# 构建项目
cmake --build build
```

```cmake
# 设置最低版本
cmake_minimum_required(VERSION 3.22.1)

# 设置项目名称 
PROJECT(Project_name)
PROJECT(name CXX) # 指定工程名称, 支持语言为c++
PROJECT(name CXX C) # 指定工程名称, 支持语言为c++, c


# 指定c++标准
set(CMAKE_CXX_STANDARD 20)

# 使C++标准成为必需的，如果编译器不支持，则会报错
set(CMAKE_CXX_STANDARD_REQUIRED True)

# 添加第三方库
find_package(imgui REQUIRED)

# 添加可执行文件
add_executable(main main.cpp ./Hello/hello.cpp ./World/world.cpp)
# 第一个参数为主要可执行程序, 后面的为可执行程序的依赖项

# 链接库
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE imgui::imgui)

target_include_directories(main PUBLIC world)
# 第一个参数是可执行文件, 第二个参数为选项, 第三个参数为搜索目录
```
