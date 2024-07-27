> ## [返回索引](../index.md)

static\_assert一共有2种:
1. `static_assert(bool类型常量表达式,报错信息(字符串字面量))`
2. `static_assert(bool类型常量表达式)`  
作用是在bool类型常量表达式为false时报错，其中第二种是C++17引入的

- 补充:
	1. 编译器可能不会显示你给的错误信息但通常来说编译器会尽可能的显示
	2. static\_assert用在不同地方没有不一样的效果
	3. 当static\_assert出现在只进行语法检查不进行编译的模板中且此时已经知道bool类型常量表达式条件为false(即此bool值未依靠模板实参)那么程序非良构，示例:
	```
	template <>
	struct S {
		static_assert(false);
	};
	```
- 功能测试宏:
	1. \_\_cpp\_static\_assert 所有static\_assert语法，在C++11的值为200410L在C++17为201411L