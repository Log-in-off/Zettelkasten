предназначен для указания компилятору, что мы намерены переопределить метод родительского класса. В этом случае не случится ошибки, если не совпадут типы и [[annotation]] базового и проиводного класса
```cpp
class Base {
public:
	virtual void mf1() const;
	virtual void mf2(int x);
	virtual void mf3 () &;
};

class Derived: public Base {
public:
	virtual void mf1(); // это будет новая функция без ошибкок
	virtual void mf1() override; // ОШИБКА КОМПИЛЯЦИИ, т.е. нет const
	
	virtual void mf2(unsigned int x); //компилятор тоже промолчит
	virtual void mf2(unsigned int x) override; // ОШИБКА КОМПИЛЯЦИИ
	
	virtual void mf3() &&; //тоже будет молчать
	virtual void mf3() && override; // ОШИБКА КОМПИЛЯЦИИ
	
};
```