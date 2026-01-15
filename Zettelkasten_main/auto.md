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

## Нюанс использования auto

`operator[]` у  `std::vector<bool>` не возвращает ссылку на `bool` элемент. На самом деле возвращает  `std::vector<bool>::referance` или `std::_Bit_reference`

```cpp
std::vector<bool> function_a(const Widget& w) { /*code*/}

//correct
bool isHightBit = function_a(w)[5]; // обращаемся к пятому элементу вектора битов
if (isHightBit)
{
	//do this
}

//UB
auto isHightBit = function_a(w)[5];
if (isHightBit) // это не bool. по факту это висячий указатель
{
}
```

`std::vector<bool>::referance` это по факту "невидимые прокси класс" и нужно избегать конструкции
```cpp
auto someVar = выражения с типом "невидимого" прокси-класса
```

решение [Явно_типизированный_иницализатор]
```cpp
auto value = static_ast<bool>function_a(w)[5];
```