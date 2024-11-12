## 排序
### 快速排序
## 回溯
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

