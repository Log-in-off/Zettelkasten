основное отличие между `enum Data1 { d1, d2};` и `enum class Data2 {b1, b2};`
в том, что для первого случая переменные `d1` и `d2` будут видны в общем пространстве имен, поэтому второй лучше. 1

Единственная причина, когда первый лучше использование [[tuple]] для доступа к полям
```cpp
using UserInfo = std::tuple<std::string, std::string, std::string>;

UserInfo uInfo{"a", "b", "c"};
#варианты получени
auto a = std::get<0>(uInfo)

enum UserFields {uiName, uiEmail, uiReputation};
auto b = std::get<uiEmail>(uInfo);
```
можно сделать подобное и для [[enum_class]] , но нужно использовать вспомогательную шаблонну функцию выполняемую в момент компиляции ([[constexpr]]) без исключений ([[noexcept]])
```cpp
template <typename E>
constexpr std::underlying_type_t<E> toUType (E enumerator) noexcept {
	return static_cast<std::underlying_type_t<E>>(enumerator);
}

//третий варинат получения
auto c = std::get<toUType(UserInfoFields::uiReputation)>(uInfo);
```
enum можно анатировать типом

```cpp
enum class Var:uint32 { var1, var2};
```
