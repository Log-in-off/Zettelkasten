Избегания копирования - формалиация ситуаций, когда компилятор может и должен избегать копирования

начиная с с++17
```cpp
auto a = std::atomic<int>{9}; //ок. только в с++17. до этого вызвало бы конструктор копирования
auto arr = std::array<int, 100>{}; // быстро только с с++17
```