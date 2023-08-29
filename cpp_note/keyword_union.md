---
tags: [Notebooks/Cpp]
title: union 结构 和 struct 结构
created: '2023-05-30T06:48:33.034Z'
modified: '2023-05-30T08:06:45.658Z'
---

# union 结构 和 struct 结构
以下程序可以解析 Union 在内存中的结构

```cpp
union myun {
    struct { int x, int y, int z; } u;
    int k;
}a;

int main()
{
    a.u.x = 4;
    a.u.y = 5;
    a.u.z = 6;
    a.k = 0;
    printf("%d, %d, %d\n", a.u.x, a.u.y, a.u.z);// 0, 5, 6
    return 0;
}
```
