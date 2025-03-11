* 高精度加法
```cc
void solve(std::string& a, std::string& b) {
    std::reverse(a.begin(), a.end());
    std::reverse(b.begin(), b.end());
    int max_len = std::max(a.size(), b.size());
    std::string result;
    int carry = 0;

    for (int i = 0; i < max_len; i++) {
        int num_a = i < a.size() ? int(a[i] - '0') : 0;
        int num_b = i < b.size() ? int(b[i] - '0') : 0;

        int sum = num_a + num_b + carry;
        carry = sum / 10;
        result.push_back(char(sum % 10) + '0');
    }
    if (carry)
        result.push_back(carry + '0');

    std::reverse(result.begin(), result.end());
    std::cout << result << std::endl;
}
'3' - '0' = 3;
char(3 + '0') = '3'
```
* 素数: > 1 是素数的范围 
```cc
bool is_prime(int num) {
    if (num <= 1) return false;
    if (num == 2) return true;  // only even num but prime
    if (num % 2 == 0) return false;              
    // even num already be dealed
    for (int i = 3; i < std::sqrt(num); i += 2) 
        if (num % i == 0) return false;
    return true;
}
```
* 二分
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
