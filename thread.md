# 示例
```cpp
#include<iostream>
#include<chrono>
#include<thread>
int main()
{
    using namespace std::literals::chrono_literals;	//引入线程头文件中的休眠部分

    auto start_time = std::chrono::high_resolution_clock::now();	//得到开始时间
    auto end_time = std::chrono::high_resolution_clock::now();	//得到结束时间
    
    std::this_thread::sleep_for(1s);	//休眠1s
    
    std::chrono::duration<float> duration = end_time - start_time;	//使用特殊类型得到经过时间
    
    std::cout << duration.count() << std::endl;		//使用count方法打印出来
}
```
