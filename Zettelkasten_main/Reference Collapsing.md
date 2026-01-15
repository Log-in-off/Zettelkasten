Свертка ссылок
[Лекция](https://youtu.be/MsuddUd7E2A?list=PL3BR09unfgciJ1_K_E914nohpiOiHnpsK&t=2642)

| Inner | Outer | Result |
| ----- | ----- | ------ |
| T&    | T&    | T&     |
| T&    | T&&   | T&     |
| T&&   | T&    | T&     |
| T&&   | T&&   | T&&    |

Левая ссылка выигрывает, если она есть
```cpp
auto &&c = y;       //->  int & && c = y;
		            //-> int &c = y;
auto &&d = move(y); //-> int && && d = move(y);
					//-> int &&d = move(y);
```

auto & -  это всегда lvalue ref
auto && -это или lvalue ref или rvalue ref(зависит от контекста)

Условия:
1. не уточненный ничем кроме ссылки тип
2. контекст вывода типов
## Уточнение
При сворачивании типов шаблонами мы должны также вывести тип шаблонного параметра. и если уточнено rvalue, и есть контекст сворачивания, но при этом мы сворачиваем из lvalue, то для косистентности тип шаблонного параметра выводится по правилам [[Decltype]]. т.е. туда добавляется одна лишняя lvalue ссылка. 
```cpp
template <typename T> int foo(T&&);

int x;
const int y = 5;

foo(x); //-> int foo<int&> foo(int&);
foo(y); //-> int foo<const int&> foo(const int&);
foo(5); //-> int foo<int &&> foo(int&&);
```
Для консистентности он выводит в ссылку для lvalue, но не для rvalue. 
если есть возможный референс калапсинг, то его устраивают, добавля сюда лишний `int&`
[лекция Владимирова](https://youtu.be/MsuddUd7E2A?list=PL3BR09unfgciJ1_K_E914nohpiOiHnpsK&t=2966)
