[[Decltype]]
# Прозрачная функция
```cpp
template <typename Fun, typename Arg> decltype(auto)
transparent (Fun fun, Arg arg) {
return fun(arg);
}

extern Buffer foo(Buffer x);

Buffer b;
Buffer t = transparet(&foo, b); //ок
Buffer u = transparet(&foo, foo(b)); //лишнее копирование
```

можно использовать для `arg` &&, но его недостаточно. для решения необходимо сделать внутри `transparent` условие
```cpp 
template <typename Fun, typename Arg> decltype(auto)
transparent (Fun fun, Arg&& arg) {
	if(arg это rvalue)
		return fun(std::move(arg));
	else
		return fun(arg); // если это ссылка
}
```
Решение:

```cpp
template <typename Fun, typename Arg> decltype(auto)
transparet (Fun fun, Arg&& arg) {
	return fun(std::forward<Arg>(arg));
}

Buffer b;
Buffer t = transparet(&foo, b); //ок
Buffer u = transparet(&foo, foo(b)); //тоже ок
```

это называется [[Perfect forwarding]]
3 условия:
1. контекст вывода:  template <typename Fun,  **typename Arg** > decltype(auto)
2. уточнение только правой ссылкой: transparet (Fun fun, **Arg&&** arg) {
3. использование std::forward: return fun( **std::forward\<Arg>(arg)**);