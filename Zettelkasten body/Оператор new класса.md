```cpp
struct Widget {
void* operator new(size_t n);
void operator delete(void* mem) noexcept;
}

Widget* w = new Widget; //вызовется кастомный new
```
его можно перегружать сколько угодно раз.