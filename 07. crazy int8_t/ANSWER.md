# Crazy int8_t - answer

Run this code:

```c++
#include <cstddef>
#include <iostream>

int main() {
  std::cout << static_cast<int8_t>(0) << static_cast<uint8_t>(1);
  return 0;
}
```

You won't see `01`.
That's because int8_t is actually char, so when you output it, you see a char with code `0` (and char with code `1`).

If you think that it doesn't happen in the real code, let's suppose you have enum class like this

```c++
#include <cstddef>
#include <iostream>

enum class Printable : uint8_t {
  NO,
  YES
};

int main() {
  auto printable = Printable::NO;
  std::cout << static_cast<uint8_t>(printable) << '\n';
}
```

Having `static_cast<uint8_t>` seems reasonable in this code (since we have Printable enum class with underlying type `uint8_t`, but it's not and it doesn't do what you see.
