 [example](https://devtut.github.io/cpp/templates.html#template-specialization)
cпециализация шаблонов
Шаблон класса может быть специализирован, т.е. его частный случай для конкретного типа будет указан непосредственно
```cpp
template <typename T> struct S {
	void dump() {std::cout << "for all\n";}
}

template <> struct S<int> {
	void dump() {std::cout << "int\n";}
}
```

частный случай специлизации - является запрет специализации [[Delete specialization]]

Пример ReferenceHandler-a
[Лекция Владимирова](https://youtu.be/UrL5gdW2JOM?list=PL3BR09unfgciJ1_K_E914nohpiOiHnpsK&t=485)
```cpp
//Общий случай
template<typename T> struct ReferenceHandler {} //пустая структура здесь специально, что бы любая попытка подставить то, чего нет, давало ошибку компиляции

//Конкретный случай
template<> struct ReferenceHandler<cl_mem> {
	static cl_int retain(cl_mem memory) {
		return ::clRetainMemoryObject(memory);}
	static cl_int release(cl_mem memory) {
		return ::clReleaseMemoryObject(memory);}	
};

//теперь
ReferenceHandler<X>::relese(obj); это либо releseX, либо ошибка
```
Специализация руками не отличается от неявного инстанцирования([[Instantiation]])

Специализая должня быть ниже основного шаблона (primary template)
но выше первого использования, иначе компилятор сам инстанцирует экземляр и будет конфликт (двойное определение) [[double definition]]

```cpp
template<typename T>
T max(T x, T y) { return x>y?x:y;}
//ok указваем явную специализацию
template <> double max(double x, y) {return 42.0;}
// никакой implicit instantiation не нужен
int foo() {return max<double>(2.0, 3.0);}
// процесс impicit instantiation нужен и он произошел
int bar() {return max<int>(2, 3);}
// Ошибка: ODR violation. explicit specialization after instantiation
template<> int max(int x, int y) {return 43;}
```

### Специализация метода шаблонного класса

```cpp
template <typename T>
class Observer:public IObserver<T> {
public:
	Observer(ISubject<T>& obj): subject_(obj) {
		subject_.Attach(this);
	} 

	virtual ~Observer() override = default;	  
	
	void Update(T data) override {	
		data_ = data;		
		std::cout << "data was updated\n";	
		PrintData();
	}

	void PrintData() {}
	
	void Unsubscribe(void) {	
		subject_.Detach(this);	
	}

private:
	ISubject<T>& subject_;	
	T data_;
};

template<>
void Observer<std::string>::PrintData() {
	std::cout << "print string: " << data_ << std::endl;
}

template<>
void Observer<int>::PrintData() {
	std::cout << "print int:" << data_ << std::endl;
}
```