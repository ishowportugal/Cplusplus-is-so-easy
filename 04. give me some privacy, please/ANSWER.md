# Give me some privacy, please - answer

There are at least 2 solutions:

1. When one virtual method overrides another one, they shouldn't be both public/private/protected.

```c++
#include <iostream>

class A {
public:
  virtual ~A() = default;

  virtual void f() const {
    std::cout << "A\n";
  }
};

class B : public A {
private:
  void f() const override {
    std::cout << "B\n";
  }
};

int main() {
  B* b = new B();
  static_cast<A*>(b)->f();
  delete b;
}
```

Note: destructor of A is virtual, otherwise it's UB.

2. Nested class. Methods of nested class can call private methods of subclass.

```c++
#include <iostream>

class A {
public:

  class B {
  public:
    void g() {
      A a;
      a.f();
    }
  };

private:
  void f() const {
    std::cout << "A\n";
  }
};

int main() {
  A::B b;
  b.g();
}
```