---
tags: [Notebooks/Cpp]
title: Decay
created: '2023-08-15T02:13:12.712Z'
modified: '2023-08-15T02:42:19.432Z'
---

# Decay

## 数组会被转化成指针
```cpp
void print_size(char arr[128]) {
  // warning: 'sizeof' on array function paramter 'arr;
  //  will return size of 'char *' [-Wsizeof-array-argument]
  std::cout << sizeof(arr) << '\n';
}
```

## 函数会被转化成指针
```cpp
void call(void callback(int), int x) {
  // 第一个参数变成了-> void (*callback)(int)
  callback(x);
}
```

## 去掉 const/volatile 修饰符
```cpp
void use_int(int my_int) {
  /* ... */
}

int main()
{
  // 3 --> int
  use_int(3);

  // x --> int
  const volatile int x = 7;
  use_int(x);
}
```
## std::decay
```cpp
// no decay
std::decay_t<int>           -> int  
// discarding references
std::decay_t<int&>          -> int  
// discarding references and const qualifier
std::decay_t<const int&>    -> int
// discarding volatile
std::decay_t<volatile int>  -> int
// array-to-pointer
std::decay_t<int[8]>        -> int*
// array-to-pointer, and also discarding the reference
std::decay_t<int(&)[8]>     -> int*
// function-to-pointer
std::decay_t<int(int)>      -> int(*)(int)

```

## decay 的使用场景
```cpp
// 不使用 decay, "foo" 会被推断为 char[4], 所以以下语句会编译不通过
std::pair<std::string, int> p = make_pair("foo", 0);


// make_pair 的实现
template <class T1, class T2> 
inline pair< typename decay<T1>::type, typename decay<T2>::type > 
make_pair(T1&& x, T2&& y)
{ 
    return pair< typename decay<T1>::type, 
                 typename decay<T2>::type >(std::forward<T1>(x), 
                                            std::forward<T2>(y)); 
}
```

