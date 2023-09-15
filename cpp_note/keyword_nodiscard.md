---
tags: [Notebooks/Cpp]
title: nodiscard
created: '2023-08-10T07:03:02.251Z'
modified: '2023-08-10T07:04:46.535Z'
---

# nodiscard
问题：nodiscard 是什么作用

解决：通常加在函数的返回值之前,当调用函数者没有使用函数返回值时，编译器会发出警告
```cpp
int func1(int num)
{ return num; }

[[nodiscard]] int func2(int num)
{ return num; }

int main()
{
  int num = 1;
  func1(num); // 编译器不会产生警告
  func2(num); // 编译器会产生警告
}
```
