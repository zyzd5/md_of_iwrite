* 变量使用必须要使用 {} 包括
## 内置变量
* 使用 set() 来修改变量
* EXECUTABLE_OUTPUT_PATH
* PROJECT_SOURCE_DIR

```cmake
set($variable_name $value)

cmake_minimum_required(VERSION $cur_version)

project($project_name)

add_executable($target dependencies1.cc dependencies2.cc)
# 指定和目标和依赖

target_include_directories($target [INTERFACE | PUBLIC | PRIVATE] $dirs...)
# 较传统 include 更推荐使用, 可以避免污染到其他 target 的头文件搜索路径

# $target: 通过 `add_executable` 或 `add_library` 创建的目标

# [INTERFACE | PUBLIC | PRIVATE]: 当前头文件的可见范围
    # INTERFACE: 仅对依赖目标有效，目标本身不会用到这些头文件目录
    # PUBLIC: 对目标及其依赖目标有效。适用于库头文件需要暴露给使用该库的其他目标时使用
    # PRIVATE: 仅对目标本身有效，适用于头文件只用于构建该目标，不对其他目标暴露

# SYSTEM: 标记目录, 将目录添加到系统目录, 可以让编译器忽略这些文件中的警告
    # 这种方式常用于第三方库的头文件, 以避免项目中出现不必要的警告信息

include_directories([AFTER | BEFORE] [SYSTEM] $dirs...)
# 告诉编译器在编译源文件时, 去哪些目录寻找头文件. 通常在项目中使用自定义库或外部库时，需要指定这些库的头文件路径

# AFTER: 将目录添加到包含目录列表的末尾，表示优先级较低。
# BEFORE: 将目录添加到包含目录列表的开头，表示优先级较高。

# SYSTEM: 标记目录, 将目录添加到系统目录, 可以让编译器忽略这些文件中的警告
    # 这种方式常用于第三方库的头文件, 以避免项目中出现不必要的警告信息


aux_source_directory($dir $variable_name)
# auxiliary
# 某个目录下的所有源文件添加到一个变量中
# 不推荐使用, 会使可维护性变差
# 不灵活, 无法递归到子目录下

``` 
