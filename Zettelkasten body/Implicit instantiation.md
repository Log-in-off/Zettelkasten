
```cpp
template<typename T>
T max(T x, T y) { return x>y?x:y;}

max<int>(2, 4); //порождает template<> int max(int, int)
```
Этот процесс называется неявным (implicit) инстанцированием. по вашему требованию создает специализию вашего класса с телом, которое было задано. и создает его через подстановку (substitution) - замен T на тип.
копилятор проводит его где захочет.
[Лекция](https://youtu.be/UrL5gdW2JOM?list=PL3BR09unfgciJ1_K_E914nohpiOiHnpsK&t=1878)

у функции `max<int>(2, 4)`  есть имя и это ее [[template id]]

неявное инстанцирование шаблона ведет себя лениво. аналог [[Short-circuit evaluation]]
```cpp
template <int N> struct Danger {
	using block = char[N];
};

template <typename T, int N> struct Tricky {
	void test_lazyness() {Danger<N> no_boom_yet; }
};

int main() {
	Tricky <int, -2> ok;// ошибка будет только при ok.test_lazyness();
}
```
При инстанцировании шаблонного класса, он инстанцируется не весь. Те методы, котоые не используются, инстанцированны не будут.