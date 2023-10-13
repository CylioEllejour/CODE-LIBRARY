> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [zhuanlan.zhihu.com](https://zhuanlan.zhihu.com/p/127860466)

一、map 简介
--------

map 是 STL（中文标准模板库）的一个关联容器。

1.  可以将任何基本类型映射到任何基本类型。如 int array[100] 事实上就是定义了一个 int 型到 int 型的映射。
2.  map 提供一对一的数据处理，key-value 键值对，其类型可以自己定义，第一个称为关键字，第二个为关键字的值
3.  map 内部是自动排序的

二、map 的用法
---------

1.  必须引入包

```C++
#include<map>
```

2.map 的定义

map<type1name,type2name> maps;// 第一个是键的类型，第二个是值的类型

```C++
map<string,int> maps;
```

**3.map 容器内元素的访问**

*   **通过下标进行访问**

如：maps['c']=5;

*   **访问方式**

```C++
// member此处是引用类型，如果要限定语句块中不允许修改，可以使用类型修饰符const指定: const auto &
    for (auto &member : mapStudent)
    {
        member.second = "x";
    }
```

```C++
// member此处是临时变量类型，语句块内赋值并不影响mapStudent原始成员值
    for (auto member : mapStudent)
    {
        member.second = "x";
    }
```

```C++
 // 演示迭代器用法
for (std::map<int, string>::iterator iter = mapStudent.begin(); iter != mapStudent.end(); iter++)
    {
        cout << iter->second << endl;
    }
```

```C++
// 演示for_each遍历map
    std::for_each(mapStudent.begin(), mapStudent.end(), funcStudent);
```

4.**map 的常用用法**

*   maps.insert() 插入

```C++
// 定义一个map对象
map<int, string> m;
 
//用insert函数插入pair
m.insert(pair<int, string>(111, "kk"));
 
// 用insert函数插入value_type数据
m.insert(map<int, string>::value_type(222, "pp"));
 
// 用数组方式插入
m[123] = "dd";
m[456] = "ff";
```

*   maps.find() 查找一个元素

find(key): 返回键是 key 的映射的迭代器

```C++
map<string,int>::iterator it;
it=maps.find("123");
```

*   maps.clear() 清空

*   maps.erase() 删除一个元素

```C++
//迭代器刪除
it = maps.find("123");
maps.erase(it);

//关键字删除
int n = maps.erase("123"); //如果刪除了返回1，否则返回0

//用迭代器范围刪除 : 把整个map清空
maps.erase(maps.begin(), maps.end());
//等同于mapStudent.clear()
```

*   maps.szie() 长度

```C++
int len=maps.size();获取到map中映射的次数
```

*   maps.begin() 返回指向 map 头部的迭代器
*   maps.end() 返回指向 map 末尾的迭代器

```C++
//迭代
map< string,int>::iterator it;
for(it = maps.begin(); it != maps.end(); it++)
    cout<<it->first<<" "<<itr->second<<endl;//输出key 和value值
```

*   maps.rbegin() 返回指向 map 尾部的逆向迭代器
*   maps.rend() 返回指向 map 头部的逆向迭代器

```C++
//反向迭代
map<string,int>::reverse_iterator it;
for(it = maps.rbegin(); it != maps.rend(); it++)
    cout<<it->first<<' '<<it->second<<endl;
```

*   maps.empty() 判断其是否为空
*   maps.swap() 交换两个 map