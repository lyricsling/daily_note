---
tags: [Notebooks/Cpp]
title: nodiscard
created: '2023-08-10T07:03:02.251Z'
modified: '2023-08-10T07:04:46.535Z'
---

# nodiscard
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
