`int* n = ::operator new (sizeof(int));` - только выделение памяти(как malloc).
Отличие только в том, что `new` может бросить исключение в отличии от malloc.

```
void* operator new(size_t n) {
	void* p = malloc(n);
	if (!p) throw std::bad_alloc{};
	return p;
}
void operator delete(void* mem) noexcept {
	free(mem);
}
std::list<int> l;
l.push_back(42);
```
