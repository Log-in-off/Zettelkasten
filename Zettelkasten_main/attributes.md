атрибуты - это конструкции в С++ служащие для накладывания и снимания ограничений с методов

`[[nodiscard]]` - нельзя игнорировать возращаемое значение. 
```cpp
class SensorLogger : public px4::ScheduledWorkItem {
public:
	//static singleton
	[[nodiscard]] static SensorLogger& get_instance() {
		static SensorLogger instance;
		return instance;
	}
```

`[[maybe_unused]]` - переменная, параметр, функция или [[enum_class]] может быть не использованны
```cpp
void fun1(int a, int b, [[maybe_unused]] int c) {
	[[maybe_unused]] auto self = this;
    return 0;
}
[[maybe_unused]] void helper();
class enum [[maybe_unused]] E { A, B };
```