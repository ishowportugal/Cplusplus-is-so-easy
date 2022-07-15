# Prime - answer

Do you know what, [`std::unordered_set`](https://en.cppreference.com/w/cpp/container/unordered_set) is?

`Internally, the elements are not sorted in any particular order, but organized into buckets.` - that's what cppreference tells us.

How to choose the number of buckets?
GCC implementation of C++ standard library (aka libstdc++) always chooses a prime number which is at least the number of elements in the set.

So, here comes the answer:

```c++
#include <iostream>
#include <unordered_set>

size_t find_prime(size_t n) {
  return std::unordered_set<int>(n).bucket_count();
}

bool is_prime(size_t n) {
  if (n < 2) {
    return false;
  }
  for (size_t i = 2; i * i <= n; ++i) {
    if (n % i == 0) {
      return false;
    }
  }

  return true;
}

int main() {
  for (int n : {1, 2, 3, 4, 5, 8, 9, 10, 1'000'000'006}) {
    std::cout << "n: " << n << " p: " << find_prime(n) << '\n';
  }

  for (size_t n = 0; n < 10'000; ++n) {
    auto p = find_prime(n);
    if (!is_prime(p)) {
      std::cout << "n: " << n << " p: " << find_prime(n) << '\n';
    }
  }
}
```

Some notes:

1. GCC (libstdc++) doesn't give exactly next prime.

2. Clang (libc++) almost always does.
  But for powers of `2`, the result is exactly that power of `2`.
  And for `0`, the result is `0`.

3. Microsoft's STL always gives a power of `2`.

4. I (almost) didn't look at the sources of STLs, please, feel free to make some PRs if I'm wrong.
