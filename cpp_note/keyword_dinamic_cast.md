# 动态强制转化
dynamic_cast 和 static_cast 相对应。
static_cast 是在编译期间进行转化，dynamic_cast 是在运算期间使用RTTI机制进行动态转化。

有如下代码继承关系
```cpp
class Artist {
  public:
    virtual void draw() { std::cout << "Artist draw" << std::endl; }
};

class Musician {
  public:
};

class Teatch {
  public:
    virtual void teach() { std::cout << "teach student" << std::end; }
};

class People : public Artist, pubilc Musician, public Teacher {
  public:
};
```
## 子类转化为父类（向上转化）
```cpp
  People *p = new People;
  // 以下两种方式均可
  Artist *a = dynamic_cast<Artist *>(p);
  // Artist *a = p; 此种方式也合法
```

## 父类转化为子类（向下转化）
```cpp
  People *p = new People;
  Artist *a = p;

  People *other_p = dynamic_cast<People *>(a);
  // People *other_p = a; 此种写法不合法
```
两条比较重要的规则：
1. 使用 dynamic_cast 进行转化时，会先找到指针指向的对象的信息类型，并沿此节点向上遍历（查找其子类），如果找到了需要转化的类型，就说明转化是安全的，
  如果没有找到需要转化的类型，就不能转化。
2. dynamic_cast 转化符只能用于含有序函数的类。 
