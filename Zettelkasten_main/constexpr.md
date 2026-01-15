указывает что объект имеет значение известное на этапе компиляции.

Все объекты [[constexpr]] являются [[const]], но не все объекты [[const]] являются [[constexpr]]
```cpp
int sz;
...
const auto arraySzie = sz; //ok
std::array<int, arraySzie> data; //ошибка. значение не известно при компиляции

constexpr auto arraySize2 = 10; //ok
std::array<int, arraySzie2> data; // тоже ок
```

[[constexpr]] функции работают в 2х режимах:
1. если все аргументы известны при компиляции, её результат тоже будет подсчитан при ней
2. если хоть один из аргументов не известен, работает как обычная функция
аргменты должны быть только литеральными типами(могут иметь значение на этапе компиляции). Пользовательские типы тоже могу быть литеральными

Конструктор тоже может быть объявлен как [[constexpr]]
```cpp
class Point {
public:
	constexpr Point(double xVal = 0, yVal = 0) noexcept : x(xVal), y(yVal) {}
	
	constexpr double xValue() const noexcept {return x;}
	constexpr double yValue() const noexcept {return y;}
private:
	double x, y;
};

#теперь мы можем написать
constexpr Point p1(9.4, 27.7);
constexpr Point p2(28.8, 5.3);

#и даже сделать другие вычисления
constexpr Point midpoint(const Point& p1, const Point& p2) noexcept {
	return {(p1.xValue() + p2.xValue())/2, 
	        (p1.yValue() + p2.yValue())/2};
}

constexpr auto mid = midpoint(p1, p2);
```