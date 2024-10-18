## 二分查找
* left 为 -1, right 为 arr.size()
```cc
int left = -1, right = arr.size();

while (left + 1 != right)
{
    int mid = (left + right) / 2;
    if (nums[mid] > target)
        right = mid;
    else if (nums[mid] < target)
        left = mid;
    else return mid;
}
return -1
```
## 二叉树
```cc
struct TreeNode
{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode() : val(0), left(nullptr), right(nullptr) {}
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    TreeNode(int x, TreeNode* left, TreeNode* right) : val(x), left(left), right(right) {}
};
```
### 前序后序中序遍历二叉树
1. 前往需要先记录的节点
2. 无法继续前进(当前val为 nullptr, return)
3. 开始记录数据

```cc
void recursion(std::vector<int> &result, TreeNode* root) noexcept
{
    if (root == nullptr)
        return;

    recursion(result, root->left);
    result.push_back(root->val);
    recursion(result, root->right);
    // 先遍历到左树的根, 不存在下一级时, 存储当前的 val, 再遍历右树
    // 中序需要先遍历到左根, 以保证均为 左中右的储值顺序
    // 前序则为先储值, 再遍历左树, 再遍历右树
    // 后序再为先遍历左, 再遍历右树, 再储值
}
```
### 求深度
```cc
int maxDepth(TreeNode* root) 
{
    if (root == nullptr) return 0;
    return std::max(maxDepth(root->left), maxDepth(root->right))+1;
}
```
## 回溯(i will rewrite it)
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
