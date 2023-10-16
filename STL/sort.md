> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [zhuanlan.zhihu.com](https://zhuanlan.zhihu.com/p/615321693)

`std::sort()`函数的常用参数：

1. 小于比较
`sort(begin1, end1,less<T>)`

2. 大于比较
`sort(begin1, end1,greater<T>)`

3. 小于等于比较
`sort(begin1, end1,less_equal<T>)`

4. 大于等于比较
`sort(begin1, end1,greater_equal<T>)`

---

`sort(container.begin(), container.end(), cmp);`

可以自定义比较规范。

以下是一个使用 sort() 函数按照字符串长度升序排序的示例：

```C++
#include <iostream> 
#include <algorithm> 
#include <string> 
#include <vector> 
using namespace std;

bool cmp(const string& s1, const string& s2) { 
    return s1.size() < s2.size(); 
}

int main() { 
    vector<string> v = {"hello", "world", "this", "is", "a", "test"}; 
    sort(v.begin(), v.end(), cmp); 
    for (auto s : v) cout << s << " "; 
    return 0; 
}


```

输出结果为：`a is test this world hello`
