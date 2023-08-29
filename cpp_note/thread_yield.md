---
tags: [Notebooks/Cpp]
title: yield
created: '2023-08-10T06:54:04.532Z'
modified: '2023-08-10T06:59:26.309Z'
---

# yield

```cpp
while(true) {
  if (pool.try_get_work()) {
    //do work
  }
  else {
    std::this_thread::yield();// other threads can push work to the queue now
  }
}
```

(1) std::this_thread::yield(); 是将当前线程所抢到的CPU”时间片A”让渡给其他线程(其他线程会争抢”时间片A”,

注意: 此时”当前线程”不参与争抢). 等到其他线程使用完”时间片A”后, 再由操作系统调度, 当前线程再和其他线程一起开始抢CPU时间片.

(2) 如果将 std::this_thread::yield();上述语句修改为: return; ,则将未使用完的CPU”时间片A”还给操作系统, 再由操作系统调度, 当前线程和其他线程一起开始抢CPU时间片.

因为条件不满足, 所以此线程很快就返回(然后立即与其他线程竞争CPU时间片), 结果就是此线程频繁的与其他线程争抢CPU时间片, 从而影响程序性能,使用 std::this_thread::yield() 后, 就相当于”当前线程”检查条件不成功后, 将其未使用完的”CPU时间片”分享给其他线程使用, 等到其他线程用完后, 再和其他线程一起竞争.

sleep_for()也可以起到 std::this_thread::yield()相似的作用, (即:当前线程在休眠期间, 自然不会与其他线程争抢CPU时间片)但两者的使用目的是大不相同的: std::this_thread::yield() 是让线程让渡出自己的CPU时间片(给其他线程使用) sleep_for() 是线程根据某种需要, 需要等待若干时间.


