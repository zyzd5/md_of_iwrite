* `rdi`, `rsi`, `rdx` 是用于函数调用的标准寄存器
    * `rdi`: Register Destination Index
    * `rsi`: Register Source Index
    * `rdx`: Register Destination Index

* 在 `x86-64` 的调用约定中, 前六个整数类型的参数通过`寄存器`传递, 之后的参数通过 `栈` 传递
    * `rdi`: `first` parameter
    * `rsi`: `second` parameter
    * `rdx`: `third` parameter
    * `rcx`: `fourth` parameter
    * `r8 `: `fifth` parameter
    * `r9 `: `sixth` parameter

* 示例
```cc
int add(int a, int b, int c) {}
/* 
    在参数传递时, 
    a 存放到 rdi,
    b 存放到 rsi,
    c 存放到 rdx,
*/
```
