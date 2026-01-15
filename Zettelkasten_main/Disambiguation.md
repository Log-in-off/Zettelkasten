зависимые имена типов могут порождать проблемы
```cpp
struct S {
	struct subtype {};
};

template <typename T> int foo(const T& x) {
	T::subtype* y; //ошибка. в данном случае `*` не указатель, а умножение
	//и т.д.

	//решение
	typename T::subtype* y;
}

foo<S>(S{});
```
# В разрешении имен есть правило, при выборе типа имени между другим типом и полем, выбирается поле!
для явного указания, что имя является типом используется ключевое слово `typename`

эта техника называется устранением неоднозначности(disambiguation)

еще пример
```cpp
template <typename T> struct {
	void foo(){}
};

template <typename T> void bar() {
	S<T> s;
	s.foo<T>(); //ошибка. на первом этапе будет принято, что foo - это поле, и `<` - это знак меньше
	//решение
	s.template foo<T>();
}
```
вместе это может выглядеть 
```cpp
typename T::template iterator<int>::value_type v;
```