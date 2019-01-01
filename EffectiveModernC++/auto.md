# auto

`auto`常用的三个情景举例：

- 复杂类型（如某些迭代器）取代
- 避免忘记初始化
- 捕捉闭包型别

## 关于lambda表达式

首先关注一下`std::function`.使用这个抽象出来的模板类可以让我们持有闭包，如：

```c++
std::function<bool(const std::unique_ptr<Widget>&
			  	   const std::unique_ptr<Widget>&)>
func = [](const std::unique_ptr<Widget>& p1,
		  const std::unique_ptr<Widget>& p2)
		  {return *p1 < *p2; };
```

`auto`储存的闭包大小和原来是一致的，而这个方式储存的实例尺寸是固定的，如果原有空间不够，其构造函数会在堆上分配内存，结果上会造成更多空间占用。同时这用方式会限制编译器内联，使调用效率下降。

## 各种妙用

- 标准中规定，`std::size_type`只须是一个无符号整形，在不同平台上可以使用`auto`来化解问题

- 某些迭代过程中可以提高效率

  ```c++
  std::unordered_map<std::string, int> m;
  //codes
  for (const std::pair<std::string, int>& p : m) {
  //codes
  }
  ```

  以上看似合情合理的代码实际上蕴含着大危机，哈系表里的哈希键值对首项类型是`const`的，因此会导致编译器寻找转换方式，而他采用的方式则是每一次循环进行复制构造然后再析构，`auto`则可以解决这种问题。

## 某些需显示标出类型的情形

### 恶心的`std::vector<bool>`

用`auto`推断`std::vector<bool>`中的类型，会产生各种未定义行为。原文表述（有部分删改）：

> 尽管从概念上说,`std::vector<bool>`应该持有的是`bool`型别的元素, 但`std: vector<bool>`的 `operator[]`的返回值并不是容器中的一个元素的引用。它返回的是个`std::vector<bool>::reference`型别的对象(这是个嵌套在`std::vector<bool>`里面的类)。
> 之所以要弄出个`std::vector<bool>::reference`,是因为`std::vector<bool>`做
 过特化,用了一种压缩形式表示其持有的元素,每个元素用一个比特来
 表示。这种做法给`std::vector<bool>`的`operator[]`带来了一个问题,因为按理
 说`std::vector<>`的 `operator[]`应该返回一个`T&`,然而`C++`中却禁止比特的引
 用。既然不能返回一个`bool&`,`std: vector<bool>`的 `operator[]`转而返回了一个
 表现得像`bool&`对象。而这个把戏若要成功, `std::vector<bool>::reference`型
 的对象就要在所有能用`boo1&`的地方保证它们也能用。实现这个效果的原理是,
 `std: vector<bool>::reference`做了一个向`bool`的隐式型别转换(目标型别不是
 `bool&`,而是`bool`。

而`auto`这里会把类型推导成`std::vector<bool>::reference`根据不同实现而产生未定义行为。

**拓展**:

`std::vector<bool>::reference`这种封装模式被称为代理类，是最为常用的设计模式之一。`C++`中`std::shared_ptr`,`std::unique_ptr`也是对裸指针的再封装而生成的代理类。

另为一种代理类的用法称为表达式模板，如：

```c++
Matrix sum = m1 + m2 + m3 + m4;
```

为了效率，这些库的`operator+`这通常会生成类似`Sum<Matrix, Matrix>`这样的代理类，这对用户是不可见的，但是`auto`推导却会产生麻烦。因此要注意不应将`auto`	与隐式代理类同用。

另一种共存的方案是使用类似以下的代码：

```c++
auto sum = static_cast<Matrix>(m1 + m2 + m3 + m4);
```

这种手法可以用在类型很模糊的场合。

