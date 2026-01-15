`void* operator new(std::size_t, void* ptr) noexcept;`
`void* operatro new[](std::size_t, void*ptr) noexcept;`
размещающий new нельзя переопределить, потому что мы не может вручную вызвать конструктор размещаемого объекта.
если вызывали там образом конструктор, нужно руками вызвать дестуктор
```
void* raw = ::operator new (sizeof(Widget), std::nothrow);
if (!raw) {обработка}

Widget* w = new(raw) Widget;
//использование
w->~Widget();
::operator delete (raw);
```