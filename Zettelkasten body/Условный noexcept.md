Условная аннотация в зависимости от типа `T`
```
template <class T>
T copy(T const& orig) noexcept(is_fundamental<T>::value) {
	return orig
}
```
можно сделать проверку на то, бросают ли у объектов конструкторы копирования
```
template <class T>
T copy(const T& orig) noexcept(
						std::is_nothrow_copy_constructible<T>::value) {
	return orig;
}
```