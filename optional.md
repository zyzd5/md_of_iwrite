```cpp
#include<optional>          //C++ 17

std::optional<std::string> data = "helloworld";

data.value()                //返回data的值
data.has_value()            //返回bool值

if (data)
    cout << data.value() << endl;
else                    //优雅的判断是否有值的方法
    cout << "empty" << endl;
```