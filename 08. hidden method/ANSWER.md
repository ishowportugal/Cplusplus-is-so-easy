# Hidden method - answer

```c++
#include <string>
#include <iostream>

class Base {
public:
  void f(int) { std::cout << "int" << std::endl; }
  virtual void f(std::string) { std::cout << "string" << std::endl; }

  virtual ~Base() = default;
};

class Derived : public Base {
public:
  void f(std::string) override { std::cout << "derived string" << std::endl; }
};

int main() {
  Derived* obj = new Derived();
  obj->f(13);
  delete obj;
  return 0;
}
```

To fix this, add `using Base::f;` to the public part of `Derived` class.

Some links on the same topic:

1. [C++ standard](http://www.open-std.org/jtc1/sc22/open/n2356/derived.html#class.member.lookup)

2. [Overriding Virtual Functions GotW](http://www.gotw.ca/gotw/005.htm)
