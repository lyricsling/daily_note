.template 明确指定调用的是模板，而不是成员函数

print_element() 中的 .template 是不可缺少的。
```cpp
c.GetValue<I>();
```
会被错误解释为，((c.GetValue) < I) > ()

具体例程如下
```cpp
#include <iostream>

template <int N>
struct Collection {
  int data[N];

  Collection() {
    for(int i = 0; i < N; ++i) {
      data[i] = 0;
    }
  };

  void SetValue(int v) {
    for(int i = 0; i < N; ++i) {
      data[i] = v;
    }
  };

  template <int I>
  int GetValue(void) const {
    return data[I];
  };
};

template <int N, int I>
void printElement(Collection<N> const & c) {
  std::cout << c.template GetValue<I>() << std::endl; /// doesn't compile without ".template"
}

int main() {
  Collection<10> myc;
  myc.SetValue(5);
  printElement<10, 2>(myc);
  return 0;
}

```
