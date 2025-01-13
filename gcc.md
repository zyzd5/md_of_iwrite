```sh
g++ -o $output_file source.cc

g++ -o $output_file file1.cc file2.cc

g++ -c source.cc
# create source.o

g++ -g source.cc -o $output_file
# 包含调试信息，便于使用调试工具（如 gdb）进行调试

g++ -O0 file.cc -o $output_file
# -O0 for non-optimize, higher num, higher optimize

g++ -Wall source.cc -o $output_file
# -Wall: enable wall
# -Wextra: enable extra-wall

g++ -S test.cc
# generate `test.s`

```

