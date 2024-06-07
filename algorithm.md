## 回溯
```cpp
void backtracking(...)
{
    if (终止条件)
    {
        收集结果;
        return;
    }
    for()
    {
        处理节点;
        递归函数;
        回溯操作;
    }
}
```
```cpp
#include <iostream>
#include <vector>

using vec_int = std::vector<int>;

auto backtracking(const vec_int &data,
                  const int index, 
                  vec_int &temp, 
                  std::vector<vec_int> &result) -> void
{
    result.push_back(temp);

    for (int i = index; i < data.size(); i++)
    {
        temp.push_back(data[i]);
        backtracking(data, i+1, temp, result);
        temp.pop_back();
    }
}

int main()
{
    vec_int data = {1, 2, 3};
    vec_int temp;
    std::vector<vec_int> result;

    backtracking(data, 0, temp, result);

    for (auto &&vec : result)
    {
        for (auto &&num : vec)
            std::cout << num << " ";
        std::cout << std::endl;
    }
}
```
