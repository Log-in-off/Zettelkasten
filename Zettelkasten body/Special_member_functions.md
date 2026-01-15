специальны функции члены это те функции члены, которые могут быть автоматичекси сгенерированы комплилятом для класса:
1. [[default_constructor]]
2. [[destructor]]        [microsoft_doc](https://learn.microsoft.com/en-us/cpp/cpp/destructors-cpp?view=msvc-170)
3. [[copy_constructor]]  [[copy_assignment_operation]]
4. [[move_constructor]] и [[move_assignment operator]]

есть важные нюансы: 
1. перемещающие операции герерируются только если нет явно объявленных копирующих операция и наоборот 
2. операции перемещения по умолчанию могут быть отменены, даже если появляется декструктор
```cpp
class StringTable {
public:
	StringTable() {dosomething();}
	~StringTable() {dosomething();}
private:
	std::map<int, std::string> value;
};

//без дестукртора класс раньше был перемещаемым
```
