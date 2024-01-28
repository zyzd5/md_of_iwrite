## bits/stdc++.h
```cpp
#include<bits/stdc++.h>
int main()
{
    clock_t start_time = clock();
    clock_t end_time = clock();
    
    std::cout << time: << end_time - start_time;
    //输出时间    
}
```
## chrono库的计时方式
*这是一个基于构造和析构函数和chrono库的计时程序*

```cpp
#include<iostream>
#include<chrono>

struct Timer
{
    std::chrono::time_point<std::chrono::steady_clock> start, end;  //使用g++编译时把类型改为high_resolution_clock
    std::chrono::duration<float> duration;

    Timer()
    {
        start = std::chrono::high_resolution_clock::now();
    }
                                                            //can run in visual studio
                                                            //but cant in VScode
    ~Timer()
    {
        end = std::chrono::high_resolution_clock::now();
        duration = end - start;
        
        std::cout << duration.count() << "s" << std::endl;
    }
};
```
