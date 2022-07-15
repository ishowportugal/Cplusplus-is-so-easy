# Give me some privacy, please

You have some object of class `A`.
And `f()` is a private method of this class.

Is there any context, from which `f()` can be called?

Some restrictions apply:

1. Context is not some method of `A`.

2. Do not use `#define private public`, or `reinterpret_cast`, it should be uncluttered `C++` solution.

3. There are no restrictions on class `A` - so you can assume anything you want, it shouldn't be arbitrary class.
