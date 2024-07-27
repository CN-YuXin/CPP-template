> ## [返回索引](../index.md)

template嵌套是C++17新增的语法，语法是:
`template <template <typename> typename T>`
这个里面的template可以说是把这个模板类型参数T变为了模板，tip: 此时只有这一个T参数，里面的template的那个typename可以加上参数名字虽然完全没有必要，因为它的作用只是说明传入的自定义类型的模板应该是什么样的，这个typename也可以改为class，这是在前几章就说过的

如果给这个T模板类型传入参数那么就必须传入一个自定义类型，且这个自定义类型必须是模板(换句话说就是类模板)，模板参数只有一个类型参数(因为template嵌套的template的参数就有一个类型参数)，这个自定义类型的模板就如同刚才的template里面的template声明一样的模板:  
`template <typename>`

使用这个T类型也是跟模板一样需要传入参数这个就没什么好说的了

- 补充:
	1. template嵌套只能作用于类型参数，错误示范:
        ```
        template <template <typename> int T>
        void FN() {}
        ```
	2. template内部嵌套的template的模板参数如果有默认值那么意思不是传入的类型的模板的模板参数有这个默认实参，示例:
        ```
        template <typename>
        class L {};
        template <template <typename = int> typename T>
        class G {};
        ```
        这个G类的嵌套template的默认实参为int，不过这并没有任何用处甚至可以之间忽略掉，且在G类使用这个类型时也不会被这个int的默认实参影响到
	3. 嵌套template可以有默认实参:
        ```
        template <typemame>
        struct A {};
        template <template <typemame> typemame T = A>
        struct B {};
        ```
	4. 嵌套template可以是占位参数(即没有形参标识符)
	5. 嵌套template与实际传入的类模板可以有一点出入，首先是值参数还是类型参数必须一样，若不是类型参数那么它的类型必须完全一样，若是类型参数那么可以形参包混用例如:
	```
	template <class T1, class T2>
	struct A {
	};

	template <template <class...> class T>
	using Ty = T<int,long>;
	```
	这种情况下是可以编译通过的，不过在Ty中传入的参数个数还是得符合实参的类模板，假如实参是A类模板那么Ty就只能传入两个类型参数不能多不能少，如果不是2个的话就会报错

	换句话说就是template嵌套的模板形参包可以指代实参的模板的多个类型参数(若这形参包里面不是类型而是值也可以这样)，但是在template嵌套里面还是只能有一个形参包(即使是一个类型的一个值的也不行)，例如:
	```
	template <class T1, class T2, int, class TT1, class TT2>
	struct A {
	};

	template <template <class..., int, class...> class T>
	using Ty = T<int,long,123,char,bool>;
	```
	在这里它会报错，因为编译器认为这个Ty里的123会传入到那个类型形参包里(即template嵌套中第一个class...)