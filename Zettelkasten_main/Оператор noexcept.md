```cpp
template <class T>
T copy(T const& orig) noexcept(noexcept(T(orig))) {
	return orig;
}
```
оператор noexcept служит для более тонкой настройки с помощью [[annotation]]. Он проверят, может ли объект бросить исключение(точнее копи-конструктор и деструктор)

В идеале он должен быть глубоко в библиотечном коде. И лучше пользовать им(пример `std::is_nothrow_copy_constructible<T>::value`) если это возможно. 

Он оценивает выражение стоящее под ним, но не вычисляет его.(смотрит на анотацию)
```cpp
struct ThrowingCtor {ThrowingCtor(){}};
void foo(ThrowingCtor) noexcept;
void foo(int) noexcept;

assert(noexcept(foo(1))) == true);
assert(noexcept(foo(ThrowingCtor{})) == false);
```
потому что конструктор `ThrowingCtor` не анотирован `ThrowingCtor`
[URL](https://youtu.be/d0iqsUx_Aow?t=831)

