или универсальная ссылка - universal reference 
[[Reference Collapsing]]

```cpp
int x;
auto &&y = x; // int &y = x;

declytype (x) &&z = x; // int &z = x;

template <typename T> void foo(T&& t);
```
иниверсальную ссылку очень легко сломать
[[Not universal references]]