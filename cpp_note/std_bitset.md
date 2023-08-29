---
tags: [Notebooks/Cpp]
title: bitset
created: '2023-05-26T08:09:15.949Z'
modified: '2023-05-30T06:44:41.686Z'
---

# bitset
```cpp
#include <bitset>
using std::bitset;

bitset<32> bitvec;  // 32 位，全为 0


bitvec.any();     // b 中是否存在值为 1 的二进制位
bitvec.none();    // b 中是否全为 0
bitvec.count();   // b 中值为 1 的个数
bitvec.flip(pos)  // b 在 pos 处的二进制位取反
```
