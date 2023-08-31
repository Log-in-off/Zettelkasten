происходит когда возвращаемый тип `auto` и компилятор не справился
```cpp
auto bad_sum_to(int i) {
	// use befor duduction
	return (i > 2) ? bad_sum_to(i-1) + i : i;
}
```
ошибка будет и без рекурсии
```cpp
auto func();
int main () {func();} //use before deduction

auto func() {return 0;}
```

