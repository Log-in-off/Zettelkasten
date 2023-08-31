ключевое слов auto выводит тип ровно по таким же правилам, по которым его выводят шаблоны [[Вывод типов]]
поэтому неуточненное auto так же режет ссылки [[Неуточненные типы]]
```cpp
template <typename T> void foo(T x);

const int &t = 4;
foo(t); //->foo<int>(int x);
auto s = t; // -> int s;

для точного вывода существует decltype

decltype(t) u = 1;// const int& u
```
[[Decltype]]
[[Use before deduction]]

нюанс в использования auto [[CTAD]]

```cpp
auto foo(int x); // non-fixed ABI(form c++14)
int foo(auto x); // non-fixed ABI(from c++20) //по факту это шаблоная функция
```
