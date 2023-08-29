---
tags: [Notebooks/Cpp]
title: auto & delctype
created: '2023-08-14T03:01:34.690Z'
modified: '2023-08-14T07:29:16.973Z'
---

# auto & delctype

## auto
在 c++11 之前，auto 关键字与 static 关键字是相对的。默认为 auto，所以这个关键字几乎用不到。

c++11 赋予了这个关键字新的含义。

```cpp
int a = 10;
auto au_a = a;
cout << typeid(au_a).name() << endl;  //运行时，获取
```
### auto 的使用场景
- 变量声明冗长
  ```cpp
  for(std::vector<std::string>::iterator i = vs.begin(); i != vs.end(); ++i)
  {
    //...
  }
  ```
- 模板函数中，声明模板参数
  ```cpp
  template <typename _Tx, typename _Ty>
  void Multiply(_Tx x, _Ty y)
  {
    auto v = x*y;
  }
  ```
- 模板参数的返回值
  ```cpp
  template<typename _Tx, typename _Ty>
  auto multiply(_Tx x, _Ty y)->decaltype(_Tx * _Ty)
  {
    return _Tx * _Ty;
  }
  ```

### 注意事项

- auto 变量必须在定义时初始化
- auto 变量变量必须始终推导成同一种类型
  ```cpp
  auto a4 = 10, a5 = 20, a6 = 30;// 正确
  auto b4 = 10, b5 = 20.0, b6 = 'a';// 错误
  ```
- 如果表达式是引用，就去除引用语义
  ```cpp
  int a = 10;
  int &b = a;

  auto c = b;   // c的类型为 int, 而非 int&
  auto &d = b;  // 
  ```
- 如果表达式为 const 或 volatile,则去除 const/volatile 语义
  ```cpp
  const int al = 10;
  auto b1 = a1;       // b1 的类型为 int, 而非 const int
  const auto c1 = a1;
  ```
- 如果 auto 关键字带上 & 号，则不去除 const 语义
  ```cpp
  const int a2 = 10;
  auto &b2 = a2;      // b2 推导为 const int
  ```
- 数组推导
  ```cpp
  int a3[3] = {1, 2, 3};
  auto b3 = a3;// a3 = int *
  auto & c3 = a3;// c3 = int[3]
  ```

  ## decltype
  ### 使用场景
  - 重用匿名类型
  ```cpp
  struct
  {
    int s_i;
    double s_d;
  }ty_s;

  ty_s as;// 非法代码
  delctype(ty_s) as;
    
  ```
  - 模板参数的返回值
  ```cpp
  template<typename _Tx, typename _Ty>
  auto multiply(_Tx x, _Ty y)->decaltype(_Tx * _Ty)
  {
    return _Tx * _Ty;
  }
  ```
  ### decltype
  - 如果 e 是一个没有带括号的标记符表达式或者类成员访问表达式,decltype（e）就是e所命名的实体的类型
  - e 的类型是T,如果 e 是一个将亡值，那么 decltype(e) 为 T&&
  - e 的类型是T,如果 e 是一个左值，那么 decltype(e) 为 T&
  - 

  

