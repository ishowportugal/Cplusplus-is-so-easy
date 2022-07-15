# Ordered tuple - answer

This is what I came up with:

```c++
// Confidential Information. "AIM High Tech" LLC
#pragma once
#include <cstddef>
#include <tuple>

template <typename... Elements>
struct OrderedTuple;

namespace impl {

template<typename Element, std::size_t /* RestArgumentsCounter */>
struct OneElementContainer {
  Element element;
};

template<size_t Index>
struct Getter {
  template <typename T>
  static constexpr const T& get_reference(const OneElementContainer<T, Index>& e) { return e.element; }

  template <typename T>
  static constexpr T& get_reference(OneElementContainer<T, Index>& e) { return e.element; }
};

}  // namespace impl

template<>
struct OrderedTuple<> {
};

template<typename Head, typename... Tail>
struct OrderedTuple<Head, Tail...>: public impl::OneElementContainer<Head, sizeof...(Tail)>, OrderedTuple<Tail...> {
  OrderedTuple(Head head, Tail... tail) :
      impl::OneElementContainer<Head, sizeof...(Tail)>(head),
      OrderedTuple<Tail...>(tail...) {}

  OrderedTuple() :
      impl::OneElementContainer<Head, sizeof...(Tail)>(),
      OrderedTuple<Tail...>() {}
};

namespace std {

template<class... Elements>
struct tuple_size<OrderedTuple<Elements...>> {
static constexpr auto value = sizeof...(Elements);
};

template<size_t index, typename... Elements>
constexpr const auto& get(const OrderedTuple<Elements...>& t) {
  return impl::Getter<sizeof...(Elements) - 1 - index>::get_reference(t);
}

template<size_t index, typename... Elements>
constexpr auto& get(OrderedTuple<Elements...>& t) {
  return impl::Getter<sizeof...(Elements) - 1 - index>::get_reference(t);
}

}  // namespace std
```

In this code it's obvious, that x equals to 4 (and therefore it can be optimized away).
Now, try it in clang or GCC [here](https://gcc.godbolt.org).

And after that change `f` to be constexpr.
You would be surprised, but your code got faster.
