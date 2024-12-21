```cmake
cmake_minimum_required(VERSION $cur_version)

project($project_name)

add_executable($target dependencies1.cc dependencies2.cc)

set(CMAKE_CXX_STANDARD 11)
``` 
