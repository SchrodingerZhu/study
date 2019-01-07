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



## 删除函数

在`C++98`环境下，移除不想使用的构造函数的方法往往是把它引入到`private`块中。问题在于这种方式还是会定义那些函数，成员函数的友元访问直到链接阶段才会报错失败。

在`C++11`中，引入了`delete`关键字的新用法。可以一定程度上地解决这个问题。但是注意，把删除函数保留在`public`块里会更好的处理报错。

一个特性，因为`float`在面临转向`int`还是`double`时会优先选择`double`，以下这种写法会同时禁用掉所有的浮点数类型：

```c++
bool f(int);
bool f(double) = delete;	
```

另外，`delete`h还可以用来删除模板的特例化，而`private`是做不到的。

## override 声明

首先来看看虚函数改写的层层要求：

- 基类中的函数必须是虚函数

- 基类和派生类中的函数名称必须完全相同（析构函数除外）

- 基类和派生类中函数形参的类别必须完全相同

- 基类和派生类中函数的常量性必须完全相同

- 类和派生类中函数的返回值和异常规格必须兼容

- **`C++11`：**基类和派生类函数引用修饰词必须完全相同。

  引用修饰词是`C++11`引入的比较鲜为人知的语言特性，用来区分该函数被左值。一个常用的场景是获取右值对象的内部字段时，直接移动往往是最好的选择，为了达到这一点，对右值调用进行区别处理，返回移动后的右值。

  实例还是右值实例调用。示例如下：

  ```c++
  class Widget {
      public: 
      void doWork() &; // function_1, for left value
      void doWork() &&; // function_2, for right value
  };
  
  Widget makeWidget(); //Class Factory
  Weight w;
  
  w.doWork(); // call function_1
  makeWidget().doWork(); //call function_2
  ```

  重写条件多而复杂，极易出错。因此建议在重写虚函数的时候加上`override`关键字，迫使编译器检查是否真正进行了重写。

  ```c++
  class Foo: public Bar {
      public: 
      virtual void func() override;
  };
  ```

  `C++11`实际上引入了两个**语境关键词**——`override`和`final`。语境关键词的意思是只在函数签名、类签名末尾等地方才会被识别为关键词。因此仍可以使用`override`为函数名。（`final`用于禁止虚函数被改写或者类被派生）。

## 更多的const_iterator支持

`C++98`下的`const_iterator`支持很不到位（而且要知道很多时候`const_iterator`到`iterator`连`reinterpret_cast`都做不到）。但是到了`C++11`，`const_iterator`的获得和使用都变得简单了。

甚至连非常量容器的`cend(),cbegin()`等返回的指示位置的迭代器（用于插入删除）也是`const_iterator`了。某些最为泛化的情况（内建数组的支持）会要求使用非成员函数`begin()、end()`等在`C++11`中只支持这两个函数，所以`const_iterator`在这种情况下不适用。但是`C++14`就增添了其它函数的支持。一个很`striky`的`C++11`兼容写法是：

```c++
template <class C>
auto cbegin(const C& container)->decltype(std::begin(container)) {
    return std::begin(container);
}
```

这个写法很不容易看出最后返回的是`const_iterator`（确实是，因为`std::begin()`作用于容器`const`引用返回的是`const`迭代器），但是可以用于仅支持`begin()`的容器。

## noexcept

`noexcept`用于标注不发射异常的函数。可以让编译器更好的生成目标代码。来看看不抛出异常的两种语法：

```c++
int f(int x) throw(); //C++98
int f(int x) noexcept; //C++11
```
前者的优化就可能比后者差。这里引用原文解释：

> 如果,在运行期,一个异常逸出`f`的作用域,则`f`的异常规格被违反。在`C++98`异常规格下,调用栈会开解至`f`的调用方,然后执行了一些与本条款无关的动作以后,程执行中止。而在`C++11`异常规格下,运行期行为会稍有不同:程序执行中止之前栈只是可能会开解。
>开解调用栈和**可能**开解调用栈,这一点点区别对于代码生成造成的影响之大可能出乎人们的意料。在带有`noexcept`声明的函数中,优化器不需要在异常传出函数的前提下将执行期栈保持在可开解状态；也不需要在异常一处函数的前提下，保证其中的对象以其被构造顺序的逆序完成析构。

很多函数（某些`push_back`）具有**能移动则移动，必须复制才复制**的优化，为了保证移动安全，很多时候就是采用了对`noexcept`进行检验的方式。

>此校验动作相当迂回。像`std::vector::push_back`这样的函数会调用`std::move_if_noexcept`后者是`std::move`的一个变体,它会在一定条件下强制转换至右值型别, 取决于型别的移动构造函数是否带有`noexcept`声明。接下来,`std::move_if_noexcept`则会向`std::is_nothrow_move_constructible`求助,该模板特征的值由编译器根据移动构造函数是否指定了`noexcept`(或 `throw()`)来设置。

**条件式`noexcept`**

一下是某标准库`pair`写的`swap`函数的签名的简化版：

```c++
void swap(pair& p) noexcept(noexcept(swap(first, p.first)) &&
							noexcept(swap(second, p.second)));
```

这种用法就是条件式`noexcept`，具体是不是`noexcept`取决于各分句是不是`noexcept`.

`C++11`的`operator delete`和`operator delete[]`默认`noexcept`。显式取消默认值的方法是`noexcept(false)`.

**契约**

- 宽松契约函数：无前置调用条件，更适合标记`noexcept`。
- 狭隘契约函数：有前置调用条件，调用条件被违反则导致为定义行为。

**大多数函数是异常中立的**

## constexpr

### constexpr对象

`constexpr`对象意味着`const`且编译期已知。声明为`constexpr`可以用来让编译器检查一些需有编译期值的对象。

### constexpr函数

行为比较复杂，传参编译期已知，则函数值在编译期产生；否则运行时产生输出。但单纯这样理解是不到位的。

书上解释：
> -  `constexpr`函数可以用在要求编译期常量的语境中。在这样的语境中,若你传给
个 `constexpr`函数的实参值是在编译期已知的,则结果也会在编译期间计算出
来。如果任何一个实参值在编译期未知,则你的代码将无法通过编译。
>- 在调用 `constexpr`函数时,若传入的值有一个或多个在编译期未知,则它的运作
方式和普通函数无异,亦即它也是在运行期执行结果的计算。这意味着,如果函
数执行的是同样的操作,仅仅应用的语境一个是要求编译期常量的,一个是用于
所有其他值的话,那就不必写两个函数。 `constexpr`函数就可以同时满足所有需求。

### 编译期求幂的一个示例

#### C++11

`C++11`要求`constexpr`函数不能有超过一个的可执行语句，写法为：

```c++
constexpr int pow(int base, int exp) noexcept {
    return (exp == 0 ? 1 : base * pow(basem exp - 1));
}
```

#### C++14

`C++14`极大地放宽了限制，所以可以这样实现：

```c++
constexpr int pow(int base, int exp) noexcept {
    auto result = 1;
    while(exp){
        if(exp & 1){
            result *= base;
        }
        base *= base;
        exp >>= 1;
    }
    return result;
}
```

### 其他注意事项

- `constexpr`函数仅限于传入和返回支持字面量的类型，因为这种类型可以持有编译期决议的值。在`C++11`中，内建类型除了`void`都符合这个要求。
- 用户定义字面量类型，可以在构造函数和其他成员函数前面标注`constexpr`.这些函数也可以互相调用。
- `C++11`的`constexpr`成员函数被隐式声明为`const`，返回默认`void`，但`C++14`取消了限制。

## const成员函数的线程安全

考虑在一个类里面实现缓存机制，如果之前没有缓存则进行计算并储存；否则直接返回缓存信息。这个计算如果不需要修改类本身的内容，很有可能会被声明称`const`函数，但是由于需要进行有无缓存的判断和计算缓存等操作，这个常函数却不是线程安全的。

一个方案是使用互斥锁,在函数添加

```c++
std::lock_guard<std::mutex> g(m);
```

在类的域里面声明：

```c++
mutable std::mutex m;
```

缺点在于`std::mutex`是一个**只移类型**，这样会导致这个类不能被复制但可以移动。。

有些时候引入互斥量是过度使用的，只用`std::atomic`的成本相对更低（还要看硬件和具体实现），但是它也是只移类型。

一般的，如果一个过程涉及到的变量只有一个，`std::atomic`通常是足够的；而需要连续操作多个相互关联的变量时，则需要互斥锁机制。

## 特种成员函数

常识补充：

> 这些函数仅在需要时才会生成,亦即,在某些代码使用了它们,而在类中并未显式声明的场合。仅当一个类没有声明任何构造函数时,才会生成默认构造函数(只要指定了一个要求传参的构造函数,就会阻止编译器生成默认构造函数)。生成的特种成员函数都具有`public`访问层级且是`inline`的,而且它们都是非虚的,除非讨论的是一个析构函数,位于一个派生类中,并且基类的析构函数是个虚函数。在那种情况下,编译器为派生类生成的析构函数也是个虚函数。（`C++11`还会默认添加`noexcept`）

`C++11`以后新引入的特种函数：移动构造函数和移动赋值运算符。默认生成时采用按成员移动（包括基类）的方式。

```c++
Foo(Foo&& bar);
Foo& operator=(Foo&& bar);
```

复制操作的构造函数和赋值是互相独立的，即声明了构造函数但调用了赋值运算符，编译器仍会自动生成。**但是移动却不是独立的，且声明了复制的类不会生成移动操作，声明了移动操作的类的复制操作会被以`delete`的方式废除**。

`C++11`的另一个规定：**只要用户声明了析构函数，就不会生成移动操作。**

仍想使用默认方式的方法是使用`= default`标注函数。

