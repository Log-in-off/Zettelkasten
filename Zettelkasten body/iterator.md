стараться использовать const_iterator
```cpp
std::vector<int> values;

#найти и заменить 1983 на 1998 или добавить в конец
auto it = std::find(value.cbegin(), value.cend(), 1983);
value.insert(it, 1998)

//обобщенный шаблонный код
template <typename C, typename V>
void findAndInsert(C& container, const V& targetVal, const V& insertValue) {
	//используем не методы контейнеров, а функции потому что некоторые контейнеры могут не иметь таких методов
	using std::cbegin;
	using std::cend;
	
	auto it = find(cbegin(container), cend(container), targetValue);
	container.insert(it, insertValue);
}
```

своя реализация `cbegin`
```cpp
template <typename C>
auto cbegin(const C& container) -> decltype(std::begin(container)) {
	return std::begin(conatainer); // поскольку container у нас const, то и итератор будет на константынй объект
}
```