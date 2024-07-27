> ## [返回索引](../index.md)

decltype关键字是C++11引入的，用于获取一个表达式返回的类型，例如`decltype(1)`返回int类型，当然可以直接decltype对象

- 补充:
	1. decltype不会真正的执行表达式(例如函数调用，不会调用函数)
        2. 虽然decltype不会真正的执行表达式但是如果表达式是函数且此函数仅仅只是个声明那么程序非良构
        3. decltype({花括号初始化})非良构
        4. decltype Lambda是不合法的 (Until: C++20)
        5. 对于直接decltype对象那么返回的结果类型是此decltype的对象定义时声明的类型，若此decltype的对象是一个对象里面的成员且这个对象具有CV那么得到的结果也是具有CV的
        6. decltype可以使用类名访问非静态数据成员，但这并非C++标准内的写法
        7. decltype的对象(例如alignas(8) int a = 0)如果设置了alignas那么decltype会忽略此alignas，除非此类型已经设定了alignas(例如struct A alignas(8))

- 功能测试宏:
	1. \_\_cpp\_decltype(200707L) decltype关键字