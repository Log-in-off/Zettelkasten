 [Документация](https://cmake.org/cmake/help/latest/command/list.html)
 [[debug]] Что бы вывести список элементов `OBJECT`
 ```cmake
foreach(arg IN LISTS OBJECT)
	 message("item: ${arg}")
endforeach()
```