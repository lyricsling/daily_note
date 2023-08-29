---
tags: [Notebooks/Cpp]
title: 内存对齐
created: '2023-08-18T05:54:08.088Z'
modified: '2023-08-18T06:22:24.306Z'
---

# 内存对齐
cpu 一次不是从内存中访问一个byte的数据，而是一次访问一块数据（2，4，8，16，32），所以合理的数据大小，能够节省cpu 访问内存的时间。

当 misaligned 时，编译器需要做格外的操作去访问数据：需要访问多块数据，左移或右移，丢弃掉不需要的数据，整合数据

```cpp
struct foo1 // size 8, alignment = 4
{
  char a;   // 1 byte
  int b;    // 4 byte
};

struct foo1_
{
  char a;         // 1 byte
  char _pad0[3];  // 3 byte padding to put on 4-byte boundary
  int b;          // 4 byte
};
```
另一个例子
```cpp
struct foo2       // size 32, alignment = 8
{
  int a;
  char b;
  float c;
  double d;
  bool e;
};

struct foo2_
{
  int a;          // 4 byte
  char b;         // 1 byte
  char _pad0[3];  // 3 byte padding to put on 8-byte boundary
  float c;        // 4 byte
  char _pad1[4];  // 4 byte padding to put on 8-byte doundary
  double d;       // 8 byte
  bool e;         // 1 byte
  char _pad2[7];  // 7 byte padding to put on 8-byte doundary
};
```

## c++11 提供的对齐
```cpp
struct alignas(4) foo
{
  char a;
  char b;
};

struct alignas(4) foo_
{
  char a;         // byte 1
  char b;         // byte 1
  char _pad0[2];  // byte 2
};
```

## 取最大
```cpp
struct alignas(4) foo
{
  alignas(2)  char a;
  alignas(8)  int b;
};

struct alignas(4) foo_
{
  char a;         // byte 1
  char _pad0[7];  // byte 7
  int b;          // byte 4
  char _pad1[4];  // byte 4
};
```
