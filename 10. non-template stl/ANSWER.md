# Non-template STL - answer

There is at least one interesting answer to this question:
```c++
class any;
```

Funny thing is that this class is not templated, but the nature is all about various types it can store.

There are two non-STL containers in the standard library: `bitset` and `valarray`.

Another interesting example: `class mutex;`. Other mutexes are not templates as well.
And there is more about threading: `std::thread` is not a template.

There are many enums in the standard library, like `std::memory_order`.

`filesystem` is (almost) without templates.

`class error_code;` is a simple class (`error_category` too).

There is some stuff in `pmr`, like `std::pmr::memory_resource`.

These were just an examples, you can see, there is a lot of stuff in the standard **template** library, and does not seem to be a template.
