специализации можно удалять сомостоятельно и запрещять компилятору создавать их самостоятельно

```cpp
//для всех указателей
template <typename T> void foo(T*){...}

//но не для char* и void*/ оба варианта записи рабочие
template<> void foo<char>(char*) = delete;
template<> void foo(void*) = delete;
```

Так же можно удалить и перегрузки функции
```cpp

void foo(int*) = delete;
```