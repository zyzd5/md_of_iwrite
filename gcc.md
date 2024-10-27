```sh
g++ -o $output_file source.cc

g++ -o $output_file file1.cc file2.cc

g++ -c source.cc
# create source.o

g++ -g source.cc -o $output_file
# 包含调试信息，便于使用调试工具（如 gdb）进行调试

g++ -O0 file.cc -o $output_file
# -O0: 无优化（默认）
# -O1: 基本优化
# -O2: 更高级的优化
# -O3: 更高级的优化，可能会增加编译时间和可执行文件大小

g++ -Wall source.cc -o $output_file
# -Wall: 启用所有常见的警告 
# -Wextra: 启用额外的警告

g++ -std=c++17 source.cc -o $output_file




```

