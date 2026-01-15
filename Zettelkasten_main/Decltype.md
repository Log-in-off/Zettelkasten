Четыре формы decltype:
существует в двух формах: для имени и для выражения

`decltype(name)` выводит тип, с которым было объявлено имя
`decltype(expression)` работает сложнее
	`decltype(lvalue)` - это тип выражения + левая ссылка
	`decltype(xvalue)` - это тип выражения + правая ссылка
	`decltype(prvalue)` - это тип выражения

В итоге левые и правые ссылки встречаются в неожиданных местах
```cpp
int a[10]; decltype(a[0]) b = a[0]; // -> int& b;

int x;
decletype((x)) t = x; // ->int& t/ из-за лишних скобочек вокруг x
```

# decletype(auto)

вовмещает лучшие стороны двух механизмов вывода
он выводит по правилам decltype, но при этом пользуется правой частью(как auto)

Вывод типов является точным, но при этом выводится из всей правой части
```cpp

double x = 1.0;
decltype(x) tmp = x; //два раза х не нужне
decltype(auto) tmp = x; //это именно то, что нужно

//что стоит справа exp или id-exp зависит от выражения
decltype(auto) tmp = x;   // -> double
decltype(auto) tmp = (x); // -> double&
```
decltype(auto) - опасная штука и лучше не пользоваться если не знаешь, что хочешь сделать

## Трюк как узнать тип во время компиляции
```cpp
//пустой шаблон
template <typename T>
class TD;

//передаем тип
int x = 0;
TD<decltype(x)> xType;
//получаем ошибку
check.cpp:18:21: error: conflicting declaration ‘TD<int> xType’
   18 |     TD<decltype(x)> xType;
      |                     ^~~~~
```
более сложный пример
```cpp
#include <vector>
#include <iostream>  

template <typename T>
class TD;  

template <typename T>
void f(const T& param) {
	std::cout << "T = " <<typeid(T).name() << '\n';
	std::cout << "param = " << typeid(param).name() << '\n'; // выведет неверный тип
	
	TD<T> dType;
	TD<decltype(param)> xType;
}

class Widget {
	public:
	Widget(int var): var_(var) {}
	int var_;
};
  

std::vector<Widget> createVec() {
	return std::vector<Widget>{Widget(1), Widget(2)};
}  

int main() {
	const auto vw = createVec();
	
	if (!vw.empty()) {
		f(&vw[0]);
	}

}
```