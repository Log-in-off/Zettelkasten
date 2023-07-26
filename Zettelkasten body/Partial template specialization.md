Частичная специализация доступна только для классов. Позволяет сделать частично специализированный шаблон класса.
Частичная специализаця метода невозможна! 

```cpp
template <typename T, typename U>
class Foo{}; // primary template

template <typename T>
class Foo<T,T>{}; // case T == U

template <typename T>
class Foo<T,int>{}; // case U == int

template <typename T, typename U>
class Foo<T*, U*>{}; // case pointers
```

Частичная специализация возможна по семейству похожих типов
Можно "выворачивать" специализацию наоборот.
```cpp
template <typename T> struct X { T a;};
template <typename T> struct X<std::vector<T>> {T b;};
X<int> a; // primary template X<T>
X<std::vector<int>> b; // X<std::vector<T>>
a.a = 5; // но в обоих случаях переменная типа T это int
b.b = 5;
```
Можно специлизировать для всех функций
```cpp
template <typename T> struct Foot{
void dump() { std::cout << "Primary\n"; }
};

template <typename R, typename T> struct Foot<R(T)>{
T obj;
void dump() { std::cout << "Specialization\n"; }
};

template <typename R> struct Foot<R(int)>{
void dump() { std::cout << "Specialization int\n"; }
};

int foot(float x) {}
int footI(int x) {}

Foot<int> tmp0;
tmp0.dump(); 

Foot<decltype(foot)> tmp1;
tmp1.dump();
tmp1.obj = 2;  

Foot<decltype(footI)> tmpI;
tmpI.dump();
```
