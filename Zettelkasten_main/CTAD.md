# Class Template Argument Deduction
в с++17  механизм определения типов аргументов шаблона
deduction hint-ы(намеки компилятору) для вывода типа

```cpp
#include <iterator>

template <typename T> struct container {
	template <typename Iter> container (Iter beg, Iter end);
	// и т.дю
};

//пользовательский хинт для вывода(типа)
template <typename Iter> container (Iter b, Iter e) -> container <typename std::iterator_traits<Iter>::value_type>;

std::vector<double> v;
auto d = container(v.begin(), v.end());
```

deduction hint - это hint из срезанного типа, поэтому можно и так
```cpp
template <typename T> struct NameValue {
	T value;
	std::string name;
};

//помощь компилятору
NameValue(const char*, const char*) -> NameValue<std::string>;

//теперь конструируем агрегат из двух строк
NameValue n{"hello", "world"};// -> NameValue<std::sting>
//по умолнчания был бы тип const char [6], но он срезается до const char*
```

основной принцип
слева стоит синтаксис вызова конструктора, а справа тип, которые нужно вывести для класса, который создает это конструктор

```cpp
int foo(); // обычный синтаксис
auto foo() -> int; // расширенный синтаксис
```

решение для в с++11

```cpp
template <typename T> auto // c++11 eroor
makeAndProcessObject(const T& builder) {
	auto var = builder.makeObject();
	//что-то
	return var;
}

//варианты
template <typename T> decltype (builder.makeObject()) //Fail. не в области видимости
makeAndProcessObject(const T& builder) {}

//рабочее решение
template <typename> auto makeAndProcessObject(const T& builder) ->
decltype (builder.makeObject()) {
	auto var = builder.makeObject();
	//что-то
	return var;
}
```

в с++14 можно `auto foo();` но у нее не фиксированная сигнатура в отличии от прошлого примера, поэтому где можно, лучше писать `decltype` [[Decltype]]

и вообще избегать писать `auto fun();` везде кроме `cpp` файлов