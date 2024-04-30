## 概念
inline namespace 并没有引进一个 scope
```cpp
namespace foo
{
  void foo_func();
}

inline namespace bar
{
  void bar_func();
}

// call the function
foo::foo_func();  //ok
bar::bar_func();  //ok

foo_func();  //not ok
bar_func();  /ok
```
但是他的用途是什么呢？

## 库的版本控制
```cpp
namespace mylibrary
{
  class foo
  {
    ...
  };
}
```
假如 mylibrary 中显示了 foo 功能，但是你对功能并不满意，想重新实现，但想保留原本的接口,可以使用以下方法
```cpp
namespace mylibrary
{
  inline namepsace v1
  {
    class foo
    {
      ...
    };
  }

  inline namespace v2
  {
    class foo
    {
      ...
    };
  }
}

// 调用
mylibrary::foo;  //调用的 v2 版本
mylibrary::v1::foo;  //仍然可以调用 v1 版本
```

另一种办法也可以解决版本区分的办法，但有缺陷。
```
namespace mylibrary
{
  inline namepsace v1
  {
    class foo
    {
      ...
    };
  }

  inline namespace v2
  {
    class foo
    {
      ...
    };
  }

  using namespace v2;
}
```
mylibrary 命名空间中并不包含 v2::foo,只包含 v2。会影响到诸如模板查找的功能。

## 解决 ABI 问题
对于动态库来说，只要 API 接口没有发送变化，动态库编译后，应用程序不需要重新链接，就可以正常运行。
对于c++来说，情况就变复杂了。比如在类中新增加了 private 的成员变量，API 虽然没变，ABI却变了。
这个时候，应用程序就需要重新编译新生成的动态库，否则就会出现问题。

增加 inline namespace 后，应用程序会调用掉v2::foo，此时会发现找不到链接，提醒应用程序开发者重新链接。

