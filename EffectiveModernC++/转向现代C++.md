# 转向现代C++

## 关于大括号初始化

大括号初始化可用于指定`stl`容器的初始状态或非静态成员变量的初始值。特别地，不可复制对象（如`std::atomic`）只能通过大小括号进行初始化，而不能用等号。

大括号的新特性是禁止内建类型的隐式窄化类型转换。一下代码将会报错：

```c++
double x, y, z;
//code
int sum{x + y + x};	
```

`C++`的解析语法会导致本来想调用无参构造函数却声明了一个新的函数的情况，如：

```c++
Widget w1(10); //normal
Widget w2(); //declare a new function
```

但是使用大括号初始化却可以避免这种问题。

如果一个类的构造函数的形参没有`std::initializer_list`型别的时候，大括号和小括号选择构造函数的方式是一致的。但是如果存在`std::initializer_list`编译器会尽可能地调用它。如：

```c++
class Widget {
public:
	Widget(int, bool b);
    Widget(std::initializer_list<long double> il);
    //code
};
Widget w1(10, true); //the first one
Widget w2{10, true}; //the second one with type cast
```

即使是复制或移动构造函数，也会被`std::initializer_list`劫持。在发生窄化类型转换时，编译器会选择报错而不是选用其他的构造函数。但型别无法转换时，则会尝试匹配其它的构造函数。

然而，空的大括号会被理解成没有实参而不是空的初始化列表。如果硬要传入一个空的初始化列表，方法是：

```c++
Widget empty1({});
Widget empty2{{}};	
```

特别地，`std::vector`就有着一个型别为`std::initializer_list`的构造函数，这回造成如下区别：

```c++
std::vector<int> vec1(2, 20); // two elements with value 20
std::vector<int> vec2{2, 20}; // two elements which are 2 and 20
```

## nullptr

```c++
#include <iostream>

void f(int){
  std::cout << "int" << std::endl;
}
void f(void*){
  std::cout << "void*" << std::endl;
}
int main(){
  f(NULL);
}
```

以上代码会无法通过编译或最动调用`f(int)`，这是因为`NULL`和`0`他们都不是指针类型的。换用`nullptr`可以解决问题。`nullptr`的类型是`std::nullptr_t`，可以隐式转换到所有裸指针型别。在使用模板的情况下，`nullptr`可能会扮演更重要的效果：

```c++
int f1(std::shared_ptr<Widget> spw);
double f2(std::unique_ptr<Widget> upw);
bool f3(Widget* pw);

template <typename Func, typename Mux, typename Ptr>
decltype(auto) lockAndCall(Func func, Mux& mux, Ptr ptr) {
	std::lock_guard<Mux> g(mux);
	return func(ptr);
}
std::mutex f1m, f2m, f3m;

auto res1 = lockAndCall(f1, f1m, 0); //error
auto res2 = lockAndCall(f2, f2m, NULL); //error
auto res3 = lockAndCall(f3, f3m, nullptr); //okay!
```

## 别名声明

在声明函数指针的时候别名声明比`typedef`更易读一些：

```c++
typedef void (*FP)(int, const std::string&);

using FP = void (*)(int, const std::string&);
```

更重要的事，`using`可以模板化：

```c++
//using
template <typename T>
using MyAllocList = std::list<T, MyAlloc<T>>;

//typedef
template <typename T>
struct MyAllocList {
    typedef std::list<T, MyAlloc<T>> type;
};
```

特别地，`using`在处理依赖型别时特别优雅：

```c++
//typedef
template <typename T>
class Widget {
private:
	typename MyAllocList<T>::type list;
}
```

因为`MyAllocList<T>::type`的类型依赖于模板参数`T`，因而被称依赖型别，声明时需要加一个`typename`

但是`using`的写法本身是模板类别，那么就可以直接这样写：

```c++
//using
template <typename T>
class Widget {
private:
	MyAllocList<T> list;
}
```

事实上，在`C++14`中标准委员会专门为一些`TMP`的模板库加上了别名：

```c++
template <class T>
using remove_const_t = typename remove_const<T>::type;

template <class T>
using remove_reference_t = typename remove_reference<T>::type;

template <class T>
using add_lvalue_reference_t = typename add_lvalue_reference<T>::type;
```

## 限定作用域的enum

`C++98`模式的`enum`枚举量是超出作用域的。

```c++
enum Color {black, white, red};
auto white = false; // error!
```

为此，`C++11`引入了限定作用域的`enum`:

```c++
enum class Color {black, white, red};

auto while = false;
Color c = Color::white;
```

要将枚举量转换成其他数值类型，需要强制类型转换（如使用`static_cast`）.

还有一个特性，那就是枚举类可以在枚举变量前声明。实际上原来的也可以，但是会存在后期改变枚举量底层型别的问题，导致编译上的复杂度上升。但是限定范围的枚举的底层型别是已知的（默认为`int`），而且可以指定：

```c++
enum class Status: std::uint32_t;
```

在使用`std::tuple`时，建议仍使用普通的`enum`来更方便的作为`get`等函数的模板参数。像稍微方便一些使用限定范围的枚举，可以这样写一个泛型函数：
```c++
//c++14
template <typename E>
constexpr auto toUType(E enumerator) noexcept {
    return static_cast<std::underlying_type_t<E>>(enumerator);
}
```



**My OS wanna update itself, back later :)**


