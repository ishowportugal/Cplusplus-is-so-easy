# Really constexpr - answer

## C++11

No, (at least) constexpr implies const on methods.

## C++14

As you probably already know, since C++14, constexpr method is not necessarily const.

The funny thing is that `operator[]` is still not marked as constexpr. (Funny thing: `int a[5];` works perfectly).

## C++17

Alright, from `C++17` `std::array` is constexpr, right?

I'm so sorry to disappoint you, but that's wrong.
You can't compare two `std::array`s in constexpr. [cppref](https://en.cppreference.com/w/cpp/container/array/operator_cmp).

## C++20

Did C++ get it right this time?
No, `fill` is still not constexpr. [cppref](https://en.cppreference.com/w/cpp/container/array/fill).

This doesn't compile with GCC 8.1 (using `-std=2a`)

```c++
#include <array>

constexpr void f() {
    std::array<int, 5> a{};
    a.fill(3);
}

int main() {
  return 0;
}
```

If you think, that it's awkward to ask `fill` to be constexpr, [`std::fill`](https://en.cppreference.com/w/cpp/algorithm/fill) is constexpr since C++20.

Btw, [`std::array::swap`](https://en.cppreference.com/w/cpp/container/array/swap) and [`std::swap(std::array)`](https://en.cppreference.com/w/cpp/container/array/swap2) are also not constexpr.
