---
tip: translate by baidu@2024-01-28 14:59:23
---
## Chapter 7

## By Value or by Reference?

Since the beginning, C++ has provided call-by-value and call-by-reference, and it is not always easy to decide which one to choose: Usually calling by reference is cheaper for nontrivial objects but more complicated. C++11 added move semantics to the mix, which means that we now have different ways to pass by reference:[1]

> 从一开始，C++ 就提供了按值调用和按引用调用，而且选择哪一种并不总是容易的：通常，对非平凡的对象来说，按引用调用更便宜，但更复杂。C++11 为混合添加了移动语义，这意味着我们现在有不同的方法来通过引用传递：[1]

1. **X const&** (constant lvalue reference):

The parameter refers to the passed object, without the ability to modify it.

> 参数是指传递的对象，但不能对其进行修改。

2. **X&** (nonconstant lvalue reference):

The parameter refers to the passed object, with the ability to modify it.

3. **X&&** (rvalue reference):

The parameter refers to the passed object, with move semantics, meaning that you can modify or "steal" the value.

> 该参数引用传递的对象，具有 move 语义，这意味着您可以修改或“窃取”该值。

Deciding how to declare parameters with known concrete types is complicated enough. In templates, types are not known, and therefore it becomes even harder to decide which passing mechanism is appropriate.

> 决定如何声明具有已知具体类型的参数已经足够复杂了。在模板中，类型是未知的，因此更难决定哪种传递机制是合适的。

Nevertheless, in Section [[1.6.1]] on page [[20]] we did recommend passing parameters in function templates by value unless there are good reasons, such as the following:

> 尽管如此，在第[[20]]页的第[[1.6.1]]节中，我们确实建议按值传递函数模板中的参数，除非有充分的理由，例如：

- Copying is not possible.[2]
- Parameters are used to return data.
- Templates just forward the parameters to somewhere else by keeping all the properties of the original arguments.

> -模板只是通过保留原始参数的所有属性，将参数转发到其他地方。

- There are significant performance improvements.

This chapter discusses the different approaches to declare parameters in templates, motivating the general recommendation to pass by value, and providing arguments for the reasons not to do so. It also discusses the tricky problems you run into when dealing with string literals and other raw arrays.

> 本章讨论了在模板中声明参数的不同方法，激发了传递值的一般建议，并为不这样做的原因提供了参数。它还讨论了在处理字符串文字和其他原始数组时遇到的棘手问题。

When reading this chapter, it is helpful to be familiar with the terminology of value categories (_lvalue_, _rvalue_, _prvalue_, _xvalue_, etc.), which is explained in [Appendix [B]].

> 在阅读本章时，熟悉价值类别的术语（_lvalue_、_rvalue_、_prervale_、_xvalue_等）会有所帮助，如[附录[B]]所述。

### 7.1 Passing by Value

When passing arguments by value, each argument must in principle be copied. Thus, each parameter becomes a copy of the passed argument. For classes, the object created as a copy generally is initialized by the copy constructor.

> 按值传递参数时，原则上必须复制每个参数。因此，每个参数都成为传递参数的副本。对于类，创建为副本的对象通常由副本构造函数初始化。

Calling a copy constructor can become expensive. However, there are various way to avoid expensive copying even when passing parameters by value: In fact, compilers might optimize away copy operations copying objects and can become cheap even for complex objects by using move semantics.

> 调用复制构造函数可能会变得昂贵。然而，即使按值传递参数，也有多种方法可以避免昂贵的复制：事实上，编译器可能会优化复制对象的复制操作，并且通过使用移动语义，即使对于复杂的对象，也会变得便宜。

For example, let's look at a simple function template implemented so that the argument is passed by value:

> 例如，让我们看看一个简单的函数模板，它是通过值传递参数实现的：

```cpp
template<typename T>
void printV (T arg) {
  ...
}
```

When calling this function template for an integer, the resulting code is

```cpp
void printV (int] arg) {
  ...
}
```

Parameter `arg` becomes a copy of any passed argument, whether it is an object or a literal or a value returned by a function.

> 参数“arg”将成为任何传递参数的副本，无论它是对象、文字还是函数返回的值。

If we define a `std::string` and call our function template for it:

```cpp
std::string s = "hi";
printV(s);
```

the template parameter `T` is instantiated as `std::string` so that we get

> 模板参数“T”被实例化为“std:：string”，因此我们得到

```cpp
void printV (std::string arg)
{
  ...
}
```

Again, when passing the string, `arg` becomes a copy of `s`. This time the copy is created by the copy constructor of the string class, which is a potentially expensive operation, because in principle this copy operation creates a full or "deep" copy so that the copy internally allocates its own memory to hold the value.[3]

> 同样，在传递字符串时，“arg”将成为“s”的副本。这一次，副本是由字符串类的副本构造函数创建的，这是一个潜在的昂贵操作，因为原则上，此副本操作会创建一个完整或“深度”副本，以便副本在内部分配自己的内存来保存值。3.

However, the potential copy constructor is not always called. Consider the following:

> 但是，并不总是调用潜在的复制构造函数。考虑以下内容：

```cpp
std::string returnString();
std::string s = "hi";
printV(s);                  //copy constructor
printV(std::string("hi"));  //copying usually optimized away (if not, move constructor)
printV(returnString());     // copying usually optimized away (if not, move constructor)
printV(std::move(s));       // move constructor
```

In the first call we pass an _lvalue_, which means that the copy constructor is used. However, in the second and third calls, when directly calling the function template for _prvalues_ (temporary objects created on the fly or returned by another function; see [Appendix [B]]), compilers usually optimize passing the argument so that no copying constructor is called at all. Note that since C++17, this optimization is required. Before C++17, a compiler that doesn't optimize the copying away, must at least have to try to use move semantics, which usually makes copying cheap. In the last call, when passing an _xvalue_ (an existing nonconstant object with `std::move()`), we force to call the move constructor by signaling that we no longer need the value of `s`.

> 在第一个调用中，我们传递一个_lvalue_，这意味着使用了复制构造函数。然而，在第二次和第三次调用中，当直接调用_prvlues_（动态创建或由另一个函数返回的临时对象；请参见[附录[B]]）的函数模板时，编译器通常会优化传递参数，从而根本不调用复制构造函数。请注意，由于 C++17，因此需要进行此优化。在 C++17 之前，一个不优化复制的编译器至少必须尝试使用移动语义，这通常会使复制变得便宜。在上一次调用中，当传递_xvalue_（具有“std:：move（）”的现有非常量对象）时，我们通过发出不再需要“s”值的信号来强制调用 move 构造函数。

Thus, calling an implementation of `printV()` that declares the parameter to be passed by value usually is only expensive if we pass an _lvalue_ (an object we created before and typically still use afterwards, as we didn't use `std::move()` to pass it). Unfortunately, this is a pretty common case. One reason is that it is pretty common to create objects early to pass them later (after some modifications) to other functions.

> 因此，如果我们传递_lvalue_（一个我们之前创建的对象，通常在之后仍然使用，因为我们没有使用“std:：move（）”来传递它），那么调用“printV（）”的实现来声明要按值传递的参数通常是昂贵的。不幸的是，这种情况很常见。其中一个原因是，很常见的情况是提前创建对象，然后（经过一些修改后）将其传递给其他函数。

##### Passing by Value Decays

There is another property of passing by value we have to mention: When passing arguments to a parameter by value, the type _decays_. This means that raw arrays get converted to pointers and that qualifiers such as `const` and `volatile` are removed (just like using the value as initializer for an object declared with `auto`):[4]

> 我们必须提到按值传递的另一个属性：当按值向参数传递参数时，类型_decays_。这意味着原始数组被转换为指针，并且诸如“const”和“volatile”之类的限定符被移除（就像使用值作为用“auto”声明的对象的初始值设定项一样）：[4]

```cpp
template<typename T>
void printV (T arg) {
  ...
}
```

```cpp
std::string const c = "hi";
printV(c);                  // [c] decays so that [arg] has type [std::string]
printV("hi");               //decays to pointer so that [arg] has type [char consT
int arr[4];
printV(arr);                // decays to pointer so that [arg] has type [char consT
```

Thus, when passing the string literal "hi"`, its type ` char const[3]`decays to` char const\*`so that this is the deduced type of` T`. Thus, the template is instantiated as follows:

> 因此，当传递字符串文字“hi”` 时，其类型“char const[3]”衰减为“char const\*”，因此这是“T”的推导类型。因此，模板被实例化如下：

```cpp
void printV (char const* arg)
{
  ...
}
```

This behavior is derived from C and has its benefits and drawbacks. Often it simplifies the handling of passed string literals, but the drawback is that inside `printV()` we can't distinguish between passing a pointer to a single element and passing a raw array. For this reason, we will discuss how to deal with string literals and other raw arrays in Section [[7.4]] on page [[115]].

> 这种行为源于 C，有其优点和缺点。它通常简化了对传递的字符串文字的处理，但缺点是在“printV（）”中，我们无法区分向单个元素传递指针和传递原始数组。因此，我们将在第[[115]]页的第[[7.4]]节中讨论如何处理字符串文字和其他原始数组。

### 7.2 Passing by Reference

Now let's discuss the different flavors of passing by reference. In all cases, no copy gets created (because the parameter just refers to the passed argument). Also, passing the argument never decays. However, sometimes passing is not possible, and if passing is possible, there are cases in which the resulting type of the parameter may cause problems.

> 现在让我们讨论一下通过引用传递的不同风格。在所有情况下，都不会创建任何副本（因为参数仅引用传递的参数）。此外，传递论点永远不会失败。然而，有时传递是不可能的，如果传递是可能的，则在某些情况下，生成的参数类型可能会导致问题。

#### 7.2.1 Passing by Constant Reference

To avoid any (unnecessary) copying, when passing nontemporary objects, we can use constant references. For example:

> 为了避免任何（不必要的）复制，在传递非临时对象时，我们可以使用常量引用。例如

```cpp
template<typename T>
void printR (T const& arg) {
  ...
}
```

With this declaration, passing an object never creates a copy (whether it's cheap or not):

> 使用此声明，传递对象永远不会创建副本（无论是否便宜）：

```cpp
std::string returnString();
std::string s = "hi";
printR(s);                  // no copy
printR(std::string("hi"));  // no copy
printR(returnString());     // no copy
printR(std::move(s));       // no copy
```

Even an `int` is passed by reference, which is a bit counterproductive but shouldn't matter that much. Thus:

> 即使是“int”也是通过引用传递的，这有点适得其反，但应该没那么重要。因此

```cpp
int i = 42;
printR(i);                  // passes reference instead of just copying [i]
```

results in `printR()` being instantiated as:

```cpp
void printR(int const& arg) {
  ...
}
```

Under the hood, passing an argument by reference is implemented by passing the address of the argument. Addresses are encoded compactly, and therefore transferring an address from the caller to the callee is efficient in itself. However, passing an address can create uncertainties for the compiler when it compiles the caller's code: What is the callee doing with that address? In theory, the callee can change all the values that are "reachable" through that address. That means, that the compiler has to assume that all the values it may have cached (usually, in machine registers) are invalid after the call. Reloading all those values can be quite expensive. You may be thinking that we are passing by _constant_ reference: Cannot the compiler deduce from that that no change can happen? Unfortunately, that is not the case because the caller may modify the referenced object through its own, non-`const` reference.[5]

> 在后台，通过引用传递参数是通过传递参数的地址来实现的。地址编码紧凑，因此将地址从调用者传输到被调用者本身就很有效。然而，当编译器编译调用者的代码时，传递地址可能会给编译器带来不确定性：被调用者对该地址做了什么？理论上，被调用者可以更改通过该地址“可达”的所有值。这意味着，编译器必须假设它可能缓存的所有值（通常在机器寄存器中）在调用后都是无效的。重新加载所有这些值可能相当昂贵。您可能认为我们传递的是_constant_reference：编译器不能从中推断出不会发生任何更改吗？不幸的是，事实并非如此，因为调用者可以通过其自己的非常量引用来修改被引用的对象。5.

This bad news is moderated by inlining: If the compiler can expand the call _inline_, it can reason about the caller and the callee _together_ and in many cases "see" that the address is not used for anything but passing the underlying value. Function templates are often very short and therefore likely candidates for inline expansion. However, if a template encapsulates a more complex algorithm, inlining is less likely to happen.

> 这个坏消息是通过内联来控制的：如果编译器可以扩展 call_inline_，它可以推断调用者和被调用者_together_，并且在许多情况下“看到”该地址除了传递底层值之外没有用于任何事情。函数模板通常很短，因此很可能是内联扩展的候选者。然而，如果模板封装了更复杂的算法，那么内联就不太可能发生。

##### Passing by Reference Does Not Decay

When passing arguments to parameters by reference, they do not _decay_. This means that raw arrays are not converted to pointers and that qualifiers such as `const` and `volatile` are not removed. However, because the _call_ parameter is declared as `T` **const** `&`, the _template_ parameter `T` itself is not deduced as `const`. For example:

> 通过引用将参数传递给参数时，它们不会_decay_。这意味着原始数组不会转换为指针，并且不会删除诸如“const”和“volatile”之类的限定符。但是，因为_call_参数被声明为 `T` **const** `&`，所以_template_参数 `T` 本身不被推导为 `const`。例如

```cpp
template<typename T>
void printR (T const& arg) {
  ...
}

std::string const c = "hi";
printR(c);              // [T] deduced as [std::string], [arg] is [std::string const&]

printR("hi");           // [T] deduced as [char[3]], [arg] is [char const(&)[3]]
int arr[4];
printR(arr);            // [T] deduced as [int[4]], [arg] is [int const(&)[4]]
```

Thus, local objects declared with type `T` in `printR()` are not constant.

> 因此，在“printR（）”中用类型“T”声明的局部对象不是常量。

### 7.2.2 Passing by Nonconstant Reference

When you want to return values through passed arguments (i.e., when you want to use _out_ or _inout_ parameters), you have to use nonconstant references (unless you prefer to pass them via pointers). Again, this means that when passing the arguments, no copy gets created. The parameters of the called function template just get direct access to the passed argument.

> 当您想通过传递的参数返回值时（即，当您想使用_out_或_inout_参数时），您必须使用非恒定引用（除非您更喜欢通过指针传递它们）。同样，这意味着在传递参数时，不会创建任何副本。被调用的函数模板的参数只能直接访问传递的参数。

Consider the following:

```cpp
template<typename T>
void outR (T& arg) {
  ...
}
```

Note that calling `outR()` for a temporary (prvalue) or an existing object passed with `std::move()` (xvalue) usually is not allowed:

> 请注意，对于用“std:：move（）”（xvalue）传递的临时（prvalue）或现有对象，通常不允许调用“outR（）”：

```cpp
std::string returnString();
std::string s = "hi";
outR(s);                  //OK: [T] deduced as [std::string], [arg] is [std::string&]
outR(std::string("hi"));  //ERROR: not allowed to pass a temporary (prvalue)
outR(returnString());     // ERROR: not allowed to pass a temporary (prvalue)
outR(std::move(s));       // ERROR: not allowed to pass an xvalue
```

You can pass raw arrays of nonconstant types, which again don't decay:

```cpp
int arr[4];
outR(arr);              // OK: [T] deduced as [int[4]], [arg] is [int(&)[4]]
```

Thus, you can modify elements and, for example, deal with the size of the array. For example:

> 因此，您可以修改元素，例如，处理数组的大小。例如

```cpp
template<typename T>
void outR (T& arg) {
  if (std::is_array<T>::value) {
    std::cout << "got array of " << std::extent<T>::value << " elems\n";
  }
  ...
}
```

However, templates are a bit tricky here. If you pass a `const` argument, the deduction might result in `arg` becoming a declaration of a constant reference, which means that passing an rvalue is suddenly allowed, where an lvalue is expected:

> 然而，模板在这里有点棘手。如果传递“const”参数，则推导可能导致“arg”成为常量引用的声明，这意味着突然允许传递右值，其中应为左值：

```cpp
std::string const c = "hi";
outR(c);                   // OK: [T] deduced as [std::string const
outR(returnConstString()); // OK: same if [returnConstString()] returns const string
outR(std::move(c));        // OK: [T] deduced as [std::string const[6]
outR("hi");                // OK: [T] deduced as [char const[3]]
```

Of course, any attempt to modify the passed argument inside the function template is an error in such cases. Passing a `const` object is possible in the call expression itself, but when the function is fully instantiated (which may happen later in the compilation process) any attempt to modify the value will trigger an error (which, however, might happen deep inside the called template; see Section [[9.4]] on page [[143]]).

> 当然，在这种情况下，试图修改函数模板内传递的参数都是错误的。在调用表达式本身中传递“const”对象是可能的，但当函数被完全实例化时（这可能在编译过程的稍后发生），任何修改值的尝试都会触发错误（然而，这可能发生在被调用的模板内部；请参阅第[[143]]页第[[9.4]]节）。

If you want to disable passing constant objects to nonconstant references, you can do the following:

> 如果要禁用将常量对象传递给非常量引用，可以执行以下操作：

• Use a static assertion to trigger a compile-time error:

```cpp
template<typename T>
void outR (T& arg) {
  [static_assert](!std::is_const<T>::value,\
                "out parameter of foo<T>(T&) is const");
  ...
}
```

• Disable the template for this case either by using `std::enable_if<>` (see Section [[6.3]] on page [[98]]):

> •使用“std:：enable_if＜＞”禁用此情况下的模板（请参见第[[98]]页的第[[6.3]]节）：

```cpp
template<typename T,\
         typename = std::enable_if_t<!std::is_const<T>::value>
void outR (T& arg) {
  ...
}
```

or concepts once they are supported (see Section [[6.5]] on page [[103]] and [Appendix [E]]):

```cpp
template<typename T>
[requires] !std::is_const_v<T>
void outR (T& arg) {
  ...
}
```

### 7.2.3 Passing by Forwarding Reference

One reason to use call-by-reference is to be able to perfect forward a parameter (see Section [[6.1]] on page [[91]]). But remember that when a forwarding reference is used, which is defined as an rvalue reference of a template parameter, special rules apply. Consider the following:

> 使用引用调用的一个原因是能够完美地转发参数（请参阅第[[91]]页第[[6.1]]节）。但请记住，当使用转发引用（定义为模板参数的右值引用）时，会应用特殊规则。考虑以下内容：

```cpp
template<typename T>
void passR (T&& arg)  [arg] declared as forwarding reference
  ...
}
```

You can pass everything to a forwarding reference and, as usual when passing by reference, no copy gets created:

> 您可以将所有内容传递给转发引用，并且在传递引用时，通常不会创建任何副本：

```cpp
std::string s = "hi";
passR(s);                 // OK: [T] deduced as [std::string&] (also the type of [arg)
passR(std::string("hi")); // OK: [T] deduced as [std::string], [arg] is [std::string&&]\
passR(returnString());    // OK: [T] deduced as [std::string], [arg] is [std::string&&]\
passR(std::move(s));      // OK: [T] deduced as [std::string], [arg] is [std::string&&]\
passR(arr);               // OK: [T] deduced as [int(&)[4]] (also the type of [arg)
```

However, the special rules for type deduction may result in some surprises:

> 然而，类型推导的特殊规则可能会导致一些意外：

```cpp
std::string const c = "hi";
passR(c);                 //OK: [T] deduced as [std::string const&]\
passR("hi");              //OK: [T] deduced as [char const(&)[3]] (also the type of [arg)
int arr[4];
passR("hi");              //OK: [T] deduced as [int (&)[4]] (also the type of [arg)
```

In each of these cases, inside `passR()` the parameter `arg` has a type that "knows" whether we passed an rvalue (to use move semantics) or a constant/nonconstant lvalue. This is the only way to pass an argument, such that it can be used to distinguish behavior for all of these three cases.

> 在每种情况下，在“passR（）”中，参数“arg”都有一个类型，它“知道”我们传递的是右值（使用移动语义）还是常量/非常量左值。这是传递论点的唯一方法，因此它可以用于区分这三种情况下的行为。

This gives the impression that declaring a parameter as a forwarding reference is almost perfect. But beware, there is no free lunch.

> 这给人的印象是，将参数声明为转发引用几乎是完美的。但是要小心，这里没有免费的午餐。

For example, this is the only case where the template parameter `T` implicitly can become a reference type. As a consequence, it might become an error to use `T` to declare a local object without initialization:

> 例如，这是模板参数“T”可以隐式成为引用类型的唯一情况。因此，在未初始化的情况下使用“T”声明本地对象可能会出错：

```cpp
template<typename T>
void passR(T&& arg)  [arg] is a forwarding reference
  T x;    // for passed lvalues, [x] is a reference, which requires an initializer
  ...
\
}
\
foo(42);  // OK: [T] deduced as int\
int i;
foo(i);   // ERROR: [T] deduced as [int&], which makes the declaration of [x] in [passR()] invalid
```

See Section [[15.6.2]] on page [[279]] for further details about how you can deal with this situation.

> 有关如何处理这种情况的更多详细信息，请参见第[[279]]页的第[[15.6.2]]节。

### 7.3 Using **std::ref()** and **std::cref()**

Since C++11, you can let the caller decide, for a function template argument, whether to pass it by value or by reference. When a template is declared to take arguments by value, the caller can use `std::cref()` and `std::ref()`, declared in header file `<functional>`, to pass the argument by reference. For example:

> 从 C++11 开始，对于函数模板参数，可以让调用方决定是通过值传递还是通过引用传递。当一个模板被声明为按值接受参数时，调用方可以使用头文件“＜functional＞”中声明的“std:：cref（）”和“std：：ref（）”通过引用传递参数。例如

```cpp
template<typename T>
void printT (T arg) {
  ...
}
\
std::string s = "hello";
printT(s);                //pass [s] by reference
printT(std::cref(s));     // pass [s] "as if by reference"
```

However, note that `std::cref()` does not change the handling of parameters in templates. Instead, it uses a trick: It wraps the passed argument `s` by an object that acts like a reference. In fact, it creates an object of type `std::reference_wrapper<>` referring to the original argument and passes this object by value. The wrapper more or less supports only one operation: an implicit type conversion back to the original type, yielding the original object.[7] So, whenever you have a valid operator for the passed object, you can use the reference wrapper instead. For example:

> 但是，请注意“std:：cref（）”不会更改模板中参数的处理方式。相反，它使用了一个技巧：它用一个像引用一样的对象包装传递的参数“s”。事实上，它创建了一个引用原始参数的“std:：reference_wrapper＜＞”类型的对象，并按值传递该对象。包装器或多或少只支持一个操作：隐式类型转换回原始类型，生成原始对象。[7] 因此，只要您对传递的对象有一个有效的运算符，就可以使用引用包装器。例如

```cpp
`basics/cref.cpp`

#include <functional>  // for]* [std::cref()]\
#include <string>
#include <iostream>
\
void printString(std::string const& s)
{
  std::cout << s << '\n';
}
\
template<typename T>
void printT (T arg)
{
  printString(arg);         // might convert]* [arg] *[back to]* [std::string]\
}
\
int main()
{
  std::string s = "hello";
  printT(s);               // print]* [s] *[passed by value]*\
  printT(std::cref(s));    // print]* [s] *[passed "as if by reference"]*\
}
```

The last call passes by value an object of type `std::reference_wrapper<string const>` to the parameter `arg`, which then passes and therefore converts it back to its underlying type `std::string`.

> 最后一个调用将类型为“std:：reference_wrapper＜string const＞”的对象按值传递给参数“arg”，然后参数“arg”传递并因此将其转换回其基础类型“std：：string”。

Note that the compiler has to know that an implicit conversion back to the original type is necessary. For this reason, `std::ref()` and `std::cref()` usually work fine only if you pass objects through generic code. For example, directly trying to output the passed object of the generic type `T` will fail because there is no output operator defined for `std::reference_wrapper<>`:

> 请注意，编译器必须知道隐式转换回原始类型是必要的。出于这个原因，“std:：ref（）”和“std：：cref（）”通常只有在通过泛型代码传递对象时才能正常工作。例如，直接尝试输出泛型类型“T”的传递对象将失败，因为没有为“std:：reference_wrapper＜＞”定义输出运算符：

```cpp
template<typename T>
void printV (T arg) {
  std::cout << arg << '\n';
}
...
std::string s = "hello";
printV(s);                //OK
printV(std::cref(s));     // ERROR: no operator [<<] for reference wrapper defined
```

Also, the following fails because you can't compare a reference wrapper with a `char const*` or `std::string`:

> 此外，以下操作也会失败，因为您无法将引用包装与“char const*”或“std:：string”进行比较：

```cpp
template<typename T1, typename T2>
[bool] isless(T1 arg1, T2 arg2)
{
   return arg1 < arg2;
}
...
std::string s = "hello";
if (isless(std::cref(s) < "world")) ...               //ERROR
if (isless(std::cref(s) < std::string(\"world"))) ...  //ERROR
```

It also doesn't help to give `arg1` and `arg2` a common type `T`:

```cpp
template<typename T>
[bool] isless(T arg1, T arg2)
{
   return arg1 < arg2;
}
```

because then the compiler gets conflicting types when trying to deduce `T` for `arg1` and `arg2`.

> 因为编译器在试图推导“arg1”和“arg2”的“T”时会得到冲突的类型。

Thus, the effect of class `std::reference_wrapper<>` is to be able to use a reference as a "first class object," which you can copy and therefore pass by value to function templates. You can also use it in classes, for example, to hold references to objects in containers. But you always finally need a conversion back to the underlying type.

> 因此，类“std:：reference_wrapper＜＞”的效果是能够将引用用作“第一类对象”，您可以复制该引用，并因此将值传递给函数模板。您也可以在类中使用它，例如，在容器中保存对对象的引用。但您最终总是需要转换回底层类型。

### 7.4 Dealing with String Literals and Raw Arrays

So far, we have seen the different effects for templates parameters when using string literals and raw arrays:

> 到目前为止，我们已经看到了使用字符串文字和原始数组时模板参数的不同效果：

• Call-by-value decays so that they become pointers to the element type.

• Any form of call-by-reference does not decay so that the arguments become references that still refer to arrays.

> •任何形式的引用调用都不会衰减，因此参数会成为仍然引用数组的引用。

Both can be good and bad. When decaying arrays to pointers, you lose the ability to distinguish between handling pointers to elements from handling passed arrays. On the other hand, when dealing with parameters where string literals may be passed, not decaying can become a problem, because string literals of different size have different types. For example:

> 两者都有好的也有坏的。将数组衰减为指针时，将无法区分处理指向元素的指针和处理传递的数组。另一方面，当处理可能传递字符串文字的参数时，不衰减可能会成为一个问题，因为不同大小的字符串文字有不同的类型。例如

```cpp
template<typename T>
void foo (T const& arg1, T const& arg2)
{
  ...
}
\
foo("hi", "guy");  //ERROR
```

Here, `foo("hi","guy")` fails to compile, because "hi"`has type` char const[3]`, while "guy"` has type `char const[4]`, but the template requires them to have the same type `T`. Only if the string literals were to have the same length would such code compile. For this reason, it is strongly recommended to use string literals of different lengths in test cases.

> 这里，`foo（“hi”，“guy”）` 无法编译，因为“hi”`的类型为` char const[3]`，而“guy“` 的类型是 `char const[4]`，但模板要求它们具有相同的类型 `T`。只有当字符串文字具有相同的长度时，才会编译这样的代码。因此，强烈建议在测试用例中使用不同长度的字符串文字。

By declaring the function template `foo()` to pass the argument by value the call is possible:

> 通过声明函数模板“foo（）”以按值传递参数，可以进行调用：

```cpp
template<typename T>
void foo (T arg1, T arg2)
{
  ...
}
\
foo("hi", "guy");      //compiles, but ...
```

But, that doesn't mean that all problems are gone. Even worse, compile-time problems may have become run-time problems. Consider the following code, where we compare the passed argument using `operator==`:

> 但是，这并不意味着所有的问题都消失了。更糟糕的是，编译时问题可能已经变成了运行时问题。考虑以下代码，其中我们使用“operator==”比较传递的参数：

```cpp
template<typename T>
void foo (T arg1, T arg2)
{
  if (arg1 == arg2) \
    ...
  }
}
\
foo("hi", "guy");    //compiles, but ...
```

As written, you have to know that you should interpret the passed character pointers as strings. But that's probably the case anyway, because the template also has to deal with arguments coming from string literals that have been decayed already (e.g., by coming from another function called by value or being assigned to an object declared with `auto`).

> 在编写时，您必须知道应该将传递的字符指针解释为字符串。但无论如何，情况可能是这样的，因为模板还必须处理来自已经衰减的字符串文字的参数（例如，来自由值调用的另一个函数或分配给用“auto”声明的对象）。

Nevertheless, in many cases decaying is helpful, especially for checking whether two objects (both passed as arguments or one passed as argument and the other expecting the argument) have or convert to the same type. One typical usage is perfect forwarding. But if you want to use perfect forwarding, you have to declare the parameters as forwarding references. In those cases, you might explicitly decay the arguments using the type trait `std::decay<>()`. See the story of `std::make_pair()` in Section [[7.6]] on page [[120]] for a concrete example.

> 然而，在许多情况下，衰减是有帮助的，尤其是对于检查两个对象（都作为参数传递，或者一个作为参数传递而另一个期望参数）是否具有或转换为相同的类型。一个典型的用法是完美转发。但是，如果要使用完美转发，则必须将参数声明为转发引用。在这些情况下，可以使用类型 trait“std:：decay<>（）”显式衰减参数。具体示例请参见第[[120]]页第[[7.6]]节中的“std:：make_pair（）”。

Note that other type traits sometimes also implicitly decay, such as `std::common_type<>`, which yields the common type of two passed argument types (see Section [[1.3.3]] on page [[12]] and Section [[D.5]] on page [[732]]).

> 请注意，其他类型特征有时也会隐式衰减，如“std:：common_type<>`，这会产生两个传递参数类型的公共类型（请参见第[[12]]页第[[1.3.3]]节和第[[732]]页第[D.5]]节）。

### 7.4.1 Special Implementations for String Literals and Raw Arrays

You might have to distinguish your implementation according to whether a pointer or an array was passed. This, of course, requires that a passed array wasn't decayed yet.

> 您可能必须根据传递的是指针还是数组来区分您的实现。当然，这需要传递的数组还没有衰减。

To distinguish these cases, you have to detect whether arrays are passed. Basically, there are two options:

> 为了区分这些情况，您必须检测是否传递了数组。基本上有两种选择：

• You can declare template parameters so that they are only valid for arrays:

> •您可以声明模板参数，使其仅对数组有效：

```cpp
template<typename T, std::size_t L1, std::size_t L2>
void foo(T (&arg1)[L1], T (&arg2)[L2)
{
  T* pa = arg1;  // decay [arg1]\
  T* pb = arg2;  // decay [arg2]\
  if (compareArrays(pa, L1, pb, L2)) {
    ...
  }
}
```

Here, `arg1` and `arg2` have to be raw arrays of the same element type `T` but with different sizes `L1` and `L2`. However, note that you might need multiple implementations to support the various forms of raw arrays (see Section [[5.4]] on page [[71]]).

> 这里，“arg1”和“arg2”必须是相同元素类型“T”但具有不同大小“L1”和“L2”的原始阵列。但是，请注意，您可能需要多个实现来支持各种形式的原始数组（请参见第[[71]]页的第[[5.4]]节）。

• You can use type traits to detect whether an array (or a pointer) was passed:

> •您可以使用类型特征来检测是否传递了数组（或指针）：

```cpp
template<typename T,\
         typename = std::enable_if_t<std::is_array_v<T>>>
void foo (T&& arg1, T&& arg2)
{
  ...
}
```

Due to these special handling, often the best way to deal with arrays in different ways is simply to use different function names. Even better, of course, is to ensure that the caller of a template uses `std::vector` or `std::array`. But as long as string literals are raw arrays, we always have to take them into account.

> 由于这些特殊的处理方式，通常以不同的方式处理数组的最佳方法就是简单地使用不同的函数名。当然，更好的方法是确保模板的调用方使用“std:：vector”或“std：：array”。但是，只要字符串文字是原始数组，我们就必须将它们考虑在内。

### 7.5 Dealing with Return Values

For return values, you can also decide between returning by value or by reference. However, returning references is potentially a source of trouble, because you refer to something that is out of your control. There are a few cases where returning references is common programming practice:

> 对于返回值，您还可以决定是按值返回还是按引用返回。然而，返回引用可能会带来麻烦，因为您引用的内容超出了您的控制范围。在一些情况下，返回引用是常见的编程实践：

• Returning elements of containers or strings (e.g., by `operator[]` or `front()`)

> •返回容器或字符串的元素（例如，通过“operator[]”或“front（）”）
> • Granting write access to class members

• Returning objects for chained calls (`operator<<` and `operator>>` for streams and `operator=` for class objects in general)

> •返回链接调用的对象（流的“operator<<”和“operator>>”以及类对象的“operator=”）

In addition, it is common to grant read access to members by returning const references.

> 此外，通常通过返回 const 引用来授予成员读取访问权限。

Note that all these cases may cause trouble if used improperly. For example:

> 请注意，如果使用不当，所有这些情况都可能导致故障。例如

```cpp
std::string* s = [new] std::string(\"whatever");
auto& c = (*s)[0];
delete s;
std::cout << c;   //run-time ERROR
```

Here, we obtained a reference to an element of a string, but by the time we use that reference, the underlying string no longer exists (i.e., we created a _dangling reference_), and we have undefined behavior. This example is somewhat contrived (the experienced programmer is likely to notice the problem right away), but things easily become less obvious. For example:

> 在这里，我们获得了对字符串中某个元素的引用，但当我们使用该引用时，基础字符串已不存在（即，我们创建了一个_dangling reference_），并且我们有未定义的行为。这个例子有些做作（有经验的程序员可能会立即注意到问题），但事情很容易变得不那么明显。例如

```cpp
auto s = std::make_shared<std::string>(\"whatever");
auto& c = (*s)[0];
s.reset();
std::cout << c;   //run-time ERROR
```

We should therefore ensure that function templates return their result by value. However, as discussed in this chapter, using a template parameter `T` is no guarantee that it is not a reference, because `T` might sometimes implicitly be deduced as a reference:

> 因此，我们应该确保函数模板按值返回结果。然而，如本章所述，使用模板参数“T”并不能保证它不是引用，因为“T”有时可能隐含地被推导为引用：

```cpp
template<typename T>
T retR(T&& p)    // [p] is a forwarding reference
{
  return T;   // OOPS: returns by reference when called for lvalues
}
```

Even when `T` is a template parameter deduced from a call-by-value call, it might become a reference type when explicitly specifying the template parameter to be a reference:

> 即使“T”是从按值调用推导的模板参数，当显式指定模板参数为引用时，它也可能成为引用类型：

```cpp
template<typename T>
T retV(T p)     //Note: [T] might become a reference
{
  return T;  // OOPS: returns a reference if [T] is a reference
}
\
int x;
retV<int&>(x);  // [retT()] instantiated for [T] as [int&]
```

To be safe, you have two options:

• Use the type trait `std::remove_reference<>` (see Section [[D.4]] on page [[729]]) to convert type `T` to a nonreference:

> •使用类型特征“std:：remove_reference<>`（请参见第[[729]]页的第[[D.4]]节）将类型“T”转换为非引用：

```cpp
template<typename T>
typename std::remove_reference<T>::type retV(T p)
{
  return T;  // always returns by value
}
```

Other traits, such as `std::decay<>` (see Section [[D.4]] on page [[731]]), may also be useful here because they also implicitly remove references.

> 其他特征，如“std:：decay<>`（请参见第[[731]]页的第[[D.4]]节），在这里也可能很有用，因为它们也隐式地删除了引用。

• Let the compiler deduce the return type by just declaring the return type to be `auto` (since C++14; see Section [[1.3.2]] on page [[11]]), because `auto` always decays:

> •让编译器通过将返回类型声明为“auto”来推导返回类型（因为 C++14；请参见第[[11]]页的第[[1.3.2]]节），因为“auto’总是衰减：

```cpp
template<typename T>
auto retV(T p)  // by-value return type deduced by compiler
{
  return T;  // always returns by value
}
```

### 7.6 Recommended Template Parameter Declarations

As we learned in the previous sections, we have very different ways to declare parameters that depend on template parameters:

> 正如我们在前几节中所了解到的，我们有非常不同的方法来声明依赖于模板参数的参数：

• Declare to pass the arguments by value:

This approach is simple, it decays string literals and raw arrays, but it doesn't provide the best performance for large objects. Still the caller can decide to pass by reference using `std::cref()` and `std::ref()`, but the caller must be careful that doing so is valid.

> 这种方法很简单，它会衰减字符串文字和原始数组，但它不能为大型对象提供最佳性能。尽管如此，调用方可以决定使用“std:：cref（）”和“std：：ref（）”通过引用传递，但调用方必须小心这样做是有效的。

• Declare to pass the arguments by-reference:

This approach often provides better performance for somewhat large objects, especially when passing

> 这种方法通常为稍大的对象提供更好的性能，尤其是在传递

-- existing objects (lvalues) to lvalue references,
-- temporary objects (prvalues) or objects marked as movable (xvalue) to rvalue references,
-- or both to forwarding references.

Because in all these cases the arguments don't decay, you may need special care when passing string literals and other raw arrays. For forwarding references, you also have to beware that with this approach template parameters implicitly can deduce to reference types.

> 因为在所有这些情况下，参数都不会衰减，所以在传递字符串文字和其他原始数组时可能需要特别小心。对于转发引用，您还必须注意，使用这种方法，模板参数可以隐式推导为引用类型。

##### General Recommendations

With these options in mind, for function templates we recommend the following:

> 考虑到这些选项，对于函数模板，我们建议如下：

1. By default, declare parameters to be passed by value. This is simple and usually works even with string literals. The performance is fine for small arguments and for temporary or movable objects. The caller can sometimes use `std::ref()` and `std::cref()` when passing existing large objects (lvalues) to avoid expensive copying.

> 1.默认情况下，声明要按值传递的参数。这很简单，通常甚至适用于字符串文字。对于小参数以及临时或可移动对象，性能都很好。调用方在传递现有的大对象（lvalues）时，有时可以使用“std:：ref（）”和“std：：cref（）”来避免昂贵的复制。

2. If there are good reasons, do otherwise:

-- If you need an _out_ or _inout_ parameter, which returns a new object or allows to modify an argument to/for the caller, pass the argument as a nonconstant reference (unless you prefer to pass it via a pointer). However, you might consider disabling accidentally accepting `const` objects as discussed in Section [[7.2.2]] on page [[110]].

> --如果需要返回新对象或允许修改调用者的参数的_out_或_inout_参数，请将该参数作为非恒定引用传递（除非您更喜欢通过指针传递）。但是，您可能会考虑禁用意外接受“const”对象，如第[[110]]页第[[7.2.2]]节所述。

-- If a template is provided to _forward_ an argument, use perfect forwarding. That is, declare parameters to be forwarding references and use `std::forward<>()` where appropriate. Consider using `std::decay<>` or `std::common_type<>` to "harmonize" the different types of string literals and raw arrays.

> --如果为_forward_an 参数提供了模板，请使用完全转发。也就是说，将参数声明为转发引用，并在适当的情况下使用“std:：forward<>（）”。考虑使用“std:：decay＜＞”或“std::：common_type＜＞”来“协调”不同类型的字符串文字和原始数组。

-- If _performance_ is key and it is expected that copying arguments is expensive, use constant references. This, of course, does not apply if you need a local copy anyway.

> --如果_performance_是关键，并且复制参数的成本很高，请使用常量引用。当然，如果您无论如何都需要本地副本，则这不适用。

3. If you know better, don't follow these recommendations. However, do not make intuitive assumptions about performance. Even experts fail if they try. Instead: Measure!

> 3.如果你更清楚，不要遵循这些建议。但是，不要对性能做出直观的假设。即使是专家也会失败。相反：测量！

##### Don't Be Over-Generic

Note that, in practice, function templates often are not for arbitrary types of arguments. Instead, some constraints apply. For example, you may know that only vectors of some type are passed. In this case, it is better not to declare such a function too generically, because, as discussed, surprising side effects may occur. Instead, use the following declaration:

> 请注意，在实践中，函数模板通常不适用于任意类型的参数。取而代之的是一些约束条件。例如，您可能知道只传递某种类型的向量。在这种情况下，最好不要过于笼统地声明这样的函数，因为正如所讨论的，可能会出现令人惊讶的副作用。相反，请使用以下声明：

```cpp
template<typename T>
void printVector (std::vector<T> const& v)
{
  ...
}
```

With this declaration of parameter `v` in `printVector()`, we can be sure that the passed `T` can't become a reference because vectors can't use references as element types. Also, it is pretty clear that passing a vector by value almost always can become expensive because the copy constructor of `std::vector<>` creates a copy of the elements. For this reason, it is probably never useful to declare such a vector parameter to be passed by value. If we declare parameter `v` just as having type `T` deciding, between call-by-value and call-by-reference becomes less obvious.

> 通过在“printVector（）”中声明参数“v”，我们可以确保传递的“T”不能成为引用，因为向量不能将引用用作元素类型。此外，很明显，按值传递向量几乎总是会变得昂贵，因为“std:：vector＜＞”的复制构造函数会创建元素的副本。出于这个原因，声明这样一个按值传递的向量参数可能永远都不会有用。如果我们将参数“v”声明为具有类型“T”决策，则按值调用和按引用调用之间的区别就不那么明显了。

### The **`std::make_pair()`** Example

`std::make_pair<>()` is a good example to demonstrate the pitfalls of deciding a parameter passing mechanism. It is a convenience function template in the C++ standard library to create `std::pair<>` objects using type deduction. Its declaration changed through different versions of the C++ standard:

• In the first C++ standard, C++98, `make_pair<>()` was declared inside namespace `std` to use call-by-reference to avoid unnecessary copying:

> •在第一个 C++ 标准 C++98 中，在命名空间“std”内声明了“make_pair＜＞（）”，以使用引用调用来避免不必要的复制：

```cpp
template<typename T1, typename T2>
pair<T1,T2> make_pair (T1 const& a, T2 const& b)
{
  return pair<T1,T2>(a,b);
}
```

This, however, almost immediately caused significant problems when using pairs of string literals or raw arrays of different size.[8]

> 然而，当使用不同大小的字符串文字对或原始数组时，这几乎立即导致了重大问题。8.

• As a consequence, with C++03 the function definition was changed to use call-by-value:

> •因此，在 C++03 中，函数定义被更改为使用按值调用：

```cpp
template<typename T1, typename T2>
pair<T1,T2> make_pair (T1 a, T2 b)
{
  return pair<T1,T2>(a,b);
}
```

As you can read in the rationale for the issue resolution, "_it appeared that this was a much smaller change to the standard than the other two suggestions, and any efficiency concerns were more than offset by the advantages of the solution_."

> 正如您在问题解决方案的基本原理中所读到的，“这似乎是对标准的一个比其他两个建议小得多的更改，任何效率问题都被解决方案的优势所抵消。”

• However, with C++11, `make_pair()` had to support move semantics, so that the arguments had to become forwarding references. For this reason, the definition changed roughly again as follows:

> •然而，在 C++11 中，“make_pair（）”必须支持移动语义，因此参数必须成为转发引用。出于这个原因，定义再次大致更改如下：

```cpp
template<typename T1, typename T2>
[constexpr] pair[<typename] decay<T1>::type, typename decay<T2>::type>
make_pair (T1&& a, T2&& b)
{
   return pair[<typename] decay<T1>::type,\
               typename decay<T2>::type>(forward<T1>(a), forward<T2>(b));
}
```

The complete implementation is even more complex: To support `std::ref()` and `std::cref()`, the function also unwraps instances of `std::reference_wrapper` into real references.

> 完整的实现甚至更为复杂：为了支持“std:：ref（）”和“std：：cref（）”，该函数还将“std::reference_wrapper”的实例展开为实际引用。

The C++ standard library now perfectly forwards passed arguments in many places in similar way, often combined with using `std::decay<>`.

> C++ 标准库现在以类似的方式在许多地方完美地转发传递的参数，通常与使用“std:：decay＜＞”相结合。

### 7.7 Summary

```cpp
- When testing templates, use string literals of different length.
- Template parameters passed by value decay, while passing them by reference does not decay.
- The type trait `std::decay<>` allows you to decay parameters in templates passed by reference.
- In some cases `std::cref()` and `std::ref()` allow you to pass arguments by reference when function templates declare them to be passed by value.
- Passing template parameters by value is simple but may not result in the best performance.
- Pass parameters to function templates by value unless there are good reasons to do otherwise.
- Ensure that return values are usually passed by value (which might mean that a template parameter can't be specified directly as a return type).
- Always measure performance when it is important. Do not rely on intuition; it's probably wrong.

^[1]^ A constant rvalue reference `X const&&` is also possible but there is no established semantic meaning for it.
^[2]^ Note that since C++17 you can pass temporary entities (rvalues) by value even if no copy or move constructor is available (see Section [[B.2.1]] on page [[676]]). So, since C++17 the additional constraint is that copying *for lvalues* is not possible.
^[3]^ The implementation of the string class might itself have some optimizations to make copying cheaper. One is the *small string optimization* (*SSO*), using some memory directly inside the object to hold the value without allocating memory as long as the value is not too long. Another is the *copy-on-write* optimization, which creates a copy using the same memory as the source as long as neither source nor the copy is modified. However, the copy-on-write optimization has significant drawbacks in multithreaded code. For this reason, it is forbidden for standard strings since C++11.
^[4]^ The term *decay* comes from C, and also applies to the type conversion from a function to a function pointer (see Section [[11.1.1]] on page [[159]]).
^[5]^ The use of `const_cast` is another, more explicit, way to modify the referenced object.
^[6]^ When passing `std::move(c)`, `std::move()` first converts `c` to `std::string const&&`, which then has the effect that `T` is deduced as `std::string const`.
^[7]^ You can also call `get()` on a reference wrapper and use it as function object.
^[8]^ See C++ library issue 181 [LibIssue181] for details.
```

## Chapter 8

## Compile-Time Programming

C++ has always included some simple ways to compute values at compile time. Templates considerably increased the possibilities in this area, and further evolution of the language has only added to this toolbox.

> C++ 总是包含一些在编译时计算值的简单方法。模板大大增加了这一领域的可能性，而语言的进一步发展只会增加这个工具箱。

In the simple case, you can decide whether or not to use certain or to choose between different template code. But the compiler even can compute the outcome of control flow at compile time, provided all necessary input is available.

> 在简单的情况下，您可以决定是否使用某些模板代码或在不同的模板代码之间进行选择。但是，只要所有必要的输入都可用，编译器甚至可以在编译时计算控制流的结果。

In fact, C++ has multiple features to support compile-time programming:

• Since before C++98, templates have provided the ability to compute at compile time, including using loops and execution path selection. (However, some consider this an "abuse" of template features, e.g., because it requires nonintuitive syntax.)

> •在 C++98 之前，模板就提供了在编译时进行计算的能力，包括使用循环和执行路径选择。（然而，有些人认为这是对模板功能的“滥用”，例如，因为它需要非直觉语法。）

• With partial specialization we can choose at compile time between different class template implementations depending on specific constraints or requirements.

> •通过部分专业化，我们可以在编译时根据特定的约束或要求在不同的类模板实现之间进行选择。

• With the SFINAE principle, we can allow selection between different function template implementations for different types or different constraints.

> •利用 SFINAE 原理，我们可以在不同类型或不同约束的不同功能模板实现之间进行选择。

• In C++11 and C++14, compile-time computing became increasingly better supported with the `constexpr` feature using "intuitive" execution path selection and, since C++14, most statement kinds (including `for` loops, `switch` statements, etc.).

> •在 C++11 和 C++14 中，使用“直观”执行路径选择的“constexpr”功能，以及自 C++14 以来的大多数语句类型（包括“for”循环、“switch”语句等），越来越能更好地支持编译时计算。

• C++17 introduced a "compile-time `if" to discard statements depending on compile-time conditions or constraints. It works even outside of templates.

> •C++17 引入了“编译时 `if”，根据编译时条件或约束来丢弃语句。它甚至可以在模板之外工作。

This chapter introduces these features with a special focus on the role and context of templates.

> 本章介绍了这些功能，并特别关注模板的作用和上下文。

### 8.1 Template Metaprogramming

Templates are instantiated at compile time (in contrast to dynamic languages, where genericity is handled at run time). It turns out that some of the features of C++ templates can be combined with the instantiation process to produce a sort of primitive recursive "programming language" within the C++ language itself.[1] For this reason, templates can be used to "compute a program." [Chapter [23]] will cover the whole story and all features, but here is a short example of what is possible.

> 模板在编译时实例化（与在运行时处理泛型的动态语言不同）。事实证明，C++ 模板的一些特性可以与实例化过程相结合，在 C++ 语言本身中产生一种原始的递归“编程语言”。[1] 因此，模板可以用于“计算程序”。[第[23]章]将涵盖整个故事和所有功能，但这里有一个可能的简短例子。

The following code finds out at compile time whether a given number is a prime number:

> 以下代码在编译时找出给定的数字是否是素数：

```cpp
`basics/isprime.hpp`

template<[unsigned] p, [unsigned] d>  // p: number to check, d: current divisor]*\
struct DoIsPrime {
  [static constexpr bool] value = (p%d != 0) && DoIsPrime<p,d-1>::value;
};
\
template<[unsigned] p>              // end recursion if divisor is 2]*\
struct DoIsPrime<p,2> {
  [static constexpr bool] value = (p%2 != 0);
};
\
template<[unsigned] p>              // primary template]*\
struct IsPrime {
  // start recursion with divisor from p/2:]*\
  [static constexpr bool] value = DoIsPrime<p,p/2>::value;
};
\
// special cases (to avoid endless recursion with template instantiation):]*\
template<>
struct IsPrime<0>  value = [false]; };
template<>
struct IsPrime<1>  value = [false]; };
template<>
struct IsPrime<2>  value = [true]; };
template<>
struct IsPrime<3>  value = [true]; };
```

The `IsPrime<>` template returns in member `value` whether the passed template parameter `p` is a prime number. To achieve this, it instantiates `DoIsPrime<>`, which recursively expands to an expression checking for each divisor `d` between `p/2` and `2` whether the divisor divides `p` without remainder.

> “IsPrime＜＞”模板在成员“value”中返回传递的模板参数“p”是否为素数。为了实现这一点，它实例化了“DoIsPrime＜＞”，它递归地扩展到一个表达式，检查“p/2”和“2”之间的每个除数“d”，该除数是否在没有余数的情况下除“p”。

For example, the expression

```cpp
IsPrime<9>::value
```

expands to

```cpp
DoIsPrime<9,4>::value
```

which expands to

```cpp
9%4!=0 && DoIsPrime<9,3>::value
```

which expands to

```cpp
9%4!=0 && 9%3!=0 && DoIsPrime<9,2>::value
```

which expands to

```cpp
9%4!=0 && 9%3!=0 && 9%2!=0
```

which evaluates to `false`, because `9%3` is `0`.

As this chain of instantiations demonstrates:

• We use recursive expansions of `DoIsPrime<>` to iterate over all divisors from `p/2` down to `2` to find out whether any of these divisors divide the given integer exactly (i.e., without remainder).

> •我们使用“DoIsPrime＜＞”的递归展开来迭代从“p/2”到“2”的所有除数，以找出这些除数中是否有任何除数能精确地除给定整数（即无余数）。

• The partial specialization of `DoIsPrime<>` for `d` equal to `2` serves as the criterion to end the recursion.

> •对于等于“2”的“d”，“DoIsPrime＜＞”的部分专门化用作结束递归的标准。

Note that all this is done at compile time. That is,

```cpp
IsPrime<9>::value
```

expands to `false` at compile time.

The template syntax is arguably clumsy, but code similar to this has been valid since C++98 (and earlier) and has proven useful for quite a few libraries.[2]

> 模板语法可以说是笨拙的，但类似的代码自 C++98（及更早版本）以来一直有效，并且已被证明对相当多的库有用。2.

See [Chapter [23]] for details.

### 8.2 Computing with **constexpr**

C++11 introduced a new feature, `constexpr`, that greatly simplifies various forms of compile-time computation. In particular, given proper input, a `constexpr` function can be evaluated at compile time. While in C++11 `constexpr` functions were introduced with stringent limitations (e.g., each `constexpr` function definition was essentially limited to consist of a `return` statement), most of these restrictions were removed with C++14. Of course, successfully evaluating a `constexpr` function still requires that all computational steps be possible and valid at compile time: Currently, that excludes things like heap allocation or throwing exceptions.

> C++11 引入了一个新特性“constexpr”，它大大简化了各种形式的编译时计算。特别是，如果输入正确，“constexpr”函数可以在编译时求值。虽然在 C++11 中，引入“constexpr”函数时有严格的限制（例如，每个“constexpr”函数定义基本上都被限制为由一个“return”语句组成），但大多数这些限制在 C++14 中都被删除了。当然，成功地评估“constexpr”函数仍然需要所有计算步骤在编译时都是可能的和有效的：目前，这不包括堆分配或抛出异常等情况。

Our example to test whether a number is a prime number could be implemented as follows in C++11:

> 我们测试一个数字是否是素数的例子可以在 C++11 中实现如下：

```cpp
`basics/isprime11.hpp`

[constexpr bool]\
doIsPrime (unsigned] p, [unsigned] d)  // p: number to check, d: current divisor]*\
{
  return d!=2 ? (p%d!=0) && doIsPrime(p,d-1) // check this and smaller divisors]*\
              : (p%2!=0);                    // end recursion if divisor is 2]*\
\
}
\
[constexpr bool] isPrime (unsigned] p)
{
  return p < 4 ? !(p<2)               // handle special cases]*\
               : doIsPrime(p,p/2);    // start recursion with divisor from p/2]*\
}
```

Due to the limitation of having only one statement, we can only use the conditional operator as a selection mechanism, and we still need recursion to iterate over the elements. But the syntax is ordinary C++ function code, making it more accessible than our first version relying on template instantiation.

> 由于只有一个语句的限制，我们只能使用条件运算符作为选择机制，并且我们仍然需要递归来迭代元素。但是语法是普通的 C++ 函数代码，这使得它比我们依赖模板实例化的第一个版本更容易访问。

With C++14, `constexpr` functions can make use of most control structures available in general C++ code. So, instead of writing unwieldy template code or somewhat arcane one-liners, we can now just use a plain `for` loop:

> 在 C++14 中，“constexpr”函数可以使用通用 C++ 代码中可用的大多数控制结构。因此，我们现在可以使用一个简单的“for”循环，而不是编写笨拙的模板代码或有点晦涩的一行代码：

```cpp
`basics/isprime14.hpp`

[constexpr bool] isPrime (unsigned int] p)
{
  [for] (unsigned int] d=2; d<=p/2; ++d) {
    if (p % d == 0) {
      [return false];  // found divisor without remainder]*\
    }
  }
  return p > 1;     // no divisor without remainder found]*\
}
```

With both the C++11 and C++14 versions of our `constexpr isPrime()` implementations, we can simply call

> 对于“constexpr isPrime（）”实现的 C++11 和 C++14 版本，我们可以简单地调用

```cpp
isPrime(9)
```

to find out whether `9` is a prime number. Note that it can do so at compile time, but it need not necessarily do so. In a context that requires a compile-time value (e.g., an array length or a nontype template argument), the compiler will attempt to evaluate a call to a `constexpr` function at compile time and issue an error if that is not possible (since a constant must be produced in the end). In other contexts, the compiler may or may not attempt the evaluation at compile time[3] but if such an evaluation fails, no error is issued and the call is left as a run-time call instead.

> 以找出“9”是否是素数。请注意，它可以在编译时这样做，但不一定要这样做。在需要编译时值（例如，数组长度或非类型模板参数）的上下文中，编译器将尝试在编译时评估对“constexpr”函数的调用，如果不可能，则会发出错误（因为最终必须生成常量）。在其他情况下，编译器可能会也可能不会在编译时尝试评估[3]，但如果这种评估失败，则不会发出错误，而是将调用作为运行时调用。

For example:

```cpp
[constexpr bool] b1 = isPrime(9);   // evaluated at compile time
```

will compute the value at compile time. The same is true with

```cpp
[const bool] b2 = isPrime(9);       // evaluated at compile time if in namespace scope
```

provided `b2` is defined globally or in a namespace. At block scope, the compiler can decide whether to compute it at compile or run time.[4] This, for example, is also the case here:

> 如果“b2”是全局定义的或在名称空间中定义的。在块范围内，编译器可以决定是在编译时还是在运行时计算它。[4] 例如，这里的情况也是如此：

```cpp
[bool] fiftySevenIsPrime() {
  return isPrime(57);             // evaluated at compile or running time
}
```

the compiler may or may not evaluate the call to `isPrime` at compile time.

> 编译器可以在编译时评估对“isPrime”的调用，也可以不评估。

On the other hand:

```cpp
int x;
...
std::cout << isPrime(x);           // evaluated at run time
```

will generate code that computes at run time whether `x` is a prime number.

> 将生成在运行时计算“x”是否为素数的代码。

### 8.3 Execution Path Selection with Partial Specialization

An interesting application of a compile-time test such as `isPrime()` is to use partial specialization to select at compile time between different implementations.

> 编译时测试（如“isPrime（）”）的一个有趣应用是使用部分专门化在编译时在不同的实现之间进行选择。

For example, we can choose between different implementations depending on whether a template argument is a prime number:

> 例如，我们可以根据模板参数是否为素数在不同的实现之间进行选择：

```cpp
// primary helper template:]*\
template<int SZ, [bool] = isPrime(SZ)>
struct Helper;
\
// implementation if]* SZ *[is not a prime number:]*\
template<int SZ>
struct Helper<SZ, [false]>
{
\
  ...
};
\
// implementation if]* SZ *[is a prime number:]*\
template<int SZ>
struct Helper<SZ, [true]>
{
\
  ...
};
\
template<typename T, std::size_t SZ>
[long] foo (std::array<T,SZ> const& coll)
{
  Helper<SZ> h;   // implementation depends on whether array has prime number as size]*\
  ...
\
}
```

Here, depending on whether the size of the `std::array<>` argument is a prime number, we use two different implementations of class `Helper<>`. This kind of application of partial specialization is broadly applicable to select among different implementations of a function template depending on properties of the arguments it's being invoked for.

> 这里，根据“std:：array＜＞”参数的大小是否为素数，我们使用类“Helper＜＞”的两种不同实现。这种部分专门化的应用程序广泛适用于根据调用函数模板的参数的属性在函数模板的不同实现中进行选择。

Above, we used two partial specializations to implement the two possible alternatives. Instead, we can also use the primary template for one of the alternatives (the default) case and partial specializations for any other special case:

> 上面，我们使用了两个部分专业化来实现两个可能的替代方案。相反，我们也可以将主模板用于其中一个备选（默认）情况，并将部分专业化用于任何其他特殊情况：

```cpp
// primary helper template (used if no specialization fits):]*\
template<int SZ, [bool] = isPrime(SZ)>
struct Helper\
{
\
  ...
};
\
// special implementation if]* SZ *[is a prime number:]*\
template<int SZ>
struct Helper<SZ, [true]>
{
\
  ...
};
```

Because function templates do not support partial specialization, you have to use other mechanisms to change function implementation based on certain constraints. Our options include the following:

> 因为函数模板不支持部分专业化，所以必须使用其他机制根据某些约束来更改函数实现。我们的选择包括以下内容：

- Use classes with static functions,
- Use `std::enable_if`, introduced in Section [[6.3]] on page [[98]],
- Use the _SFINAE_ feature, which is introduced next, or
- Use the compile-time `if` feature, available since C++17, which is introduced below in Section [[8.5]] on page [[135]].

> -使用编译时“if”功能，该功能自 C++17 以来就可用，下面在第[[135]]页的第[[8.5]]节中介绍。

[Chapter [20]] discusses techniques for selecting a function implementation based on constraints.

> [第[20]章]讨论了基于约束选择功能实现的技术。

### 8.4 SFINAE (Substitution Failure Is Not An Error)

In C++ it is pretty common to overload functions to account for various argument types. When a compiler sees a call to an overloaded function, it must therefore consider each candidate separately, evaluating the arguments of the call and picking the candidate that matches best (see also [Appendix [C]] for some details about this process).

> 在 C++ 中，重载函数以考虑各种参数类型是很常见的。因此，当编译器看到对重载函数的调用时，它必须分别考虑每个候选函数，评估调用的参数并选择最匹配的候选函数（有关此过程的一些详细信息，请参见[附录[C]]）。

In cases where the set of candidates for a call includes function templates, the compiler first has to determine what template arguments should be used for that candidate, then substitute those arguments in the function parameter list and in its return type, and then evaluate how well it matches (just like an ordinary function). However, the substitution process could run into problems: It could produce constructs that make no sense. Rather than deciding that such meaningless substitutions lead to errors, the language rules instead say that candidates with such substitution problems are simply ignored.

> 如果调用的候选集包括函数模板，编译器首先必须确定该候选应使用哪些模板参数，然后在函数参数列表及其返回类型中替换这些参数，然后评估其匹配程度（就像普通函数一样）。然而，替换过程可能会遇到问题：它可能会产生毫无意义的构造。语言规则并没有决定这种毫无意义的替换会导致错误，而是说，有这种替换问题的考生会被忽略。

We call this principle _SFINAE_ (pronounced like _sfee-nay_), which stands for "substitution failure is not an error."

> 我们将这一原理称为_SFINAE_（发音类似_sfee-namey_），它代表“替换失败不是错误”

Note that the substitution process described here is distinct from the on-demand instantiation process (see Section [[2.2]] on page [[27]]): The substitution may be done even for potential instantiations that are not needed (so the compiler can evaluate whether indeed they are unneeded). It is a substitution of the constructs appearing directly in the declaration of the function (but not its body).

> 请注意，此处描述的替换过程不同于按需实例化过程（请参见第[27]]页第[[2.2]]节）：即使是不需要的潜在实例化，也可以进行替换（因此编译器可以评估它们是否确实不需要）。它是对直接出现在函数声明中的构造（而不是其主体）的替换。

Consider the following example:

```cpp
`basics/len1.hpp`

// number of elements in a raw array:]*\
template<typename T, [unsigned] N>
std::size_t len (T(&)[N)
{
  return N;
}
\
// number of elements for a type having]* size_type*[:]*\
template<typename T>
typename T::size_type len (T const& t)
{
  return t.size();
}
```

Here, we define two function templates `len()` taking one generic argument:[5]

> 在这里，我们定义了两个函数模板“len（）”，采用一个通用参数：[5]

1. The first function template declares the parameter as `T(&)[N]`, which means that the parameter has to be an array of `N` elements of type `T`.

> 1.第一个函数模板将参数声明为“T（&）[N]'，这意味着该参数必须是类型为“T”的“N”个元素的数组。

2. The second function template declares the parameter simply as `T`, which places no constraints on the parameter but returns type `T::size_type`, which requires that the passed argument type has a corresponding member `size_type`.

> 2.第二个函数模板将参数简单地声明为“T”，这不对参数施加约束，但返回类型“T：：size_type”，这要求传递的参数类型具有相应的成员“size_type“。

When passing a raw array or string literals, only the function template for raw arrays matches:

> 传递原始数组或字符串文字时，只有原始数组的函数模板匹配：

```cpp
int a[10];
std::cout << len(a);       // OK: only [len()] for array matches
std::cout << len(\"tmp");   //OK: only [len()] for array matches
```

According to its signature, the second function template also matches when substituting (respectively) `int[10]` and `char const[4]` for `T`, but those substitutions lead to potential errors in the return type `T::size_type`. The second template is therefore ignored for these calls.

> 根据其签名，当（分别）用“int[10]”和“char const[4]”代替“T”时，第二个函数模板也匹配，但这些替换会导致返回类型“T：：size_type”中的潜在错误。因此，对于这些调用，将忽略第二个模板。

When passing a `std::vector<>`, only the second function template matches:

> 当传递“std:：vector＜＞”时，只有第二个函数模板匹配：

```cpp
std::vector<int> v;
std::cout << len(v);   // OK: only [len()] for a type with [size_type] matches
```

When passing a raw pointer, neither of the templates match (without a failure). As a result, the compiler will complain that no matching `len()` function is found:

> 当传递原始指针时，两个模板都不匹配（没有失败）。因此，编译器将抱怨找不到匹配的“len（）”函数：

```cpp
int* p;
std::cout << len(p);   // ERROR: no matching [len()] function found
```

Note that this differs from passing an object of a type having a `size_type` member, but no `size()` member function, as is, for example, the case for `std::allocator<>`:

> 请注意，这与传递具有“size_type”成员但没有“size（）”成员函数的类型的对象不同，例如，“std:：allocater<>'的情况就是这样：

```cpp
std::allocator<int> x;
std::cout << len(x);   // ERROR: [len()] function found, but can't [size()]
```

When passing an object of such a type, the compiler finds the second function template as matching function template. So instead of an error that no matching `len()` function is found, this will result in a compile-time error that calling `size()` for a `std::allocator<int>` is invalid. This time, the second function template is not ignored.

> 当传递这种类型的对象时，编译器会找到第二个函数模板作为匹配的函数模板。因此，这将导致编译时错误，即为“std:：allocater＜int＞”调用“size（）”是无效的，而不是没有找到匹配的“len（）”函数。这一次，第二个函数模板没有被忽略。

Ignoring a candidate when substituting its return type is meaningless can cause the compiler to select another candidate whose parameters are a worse match. For example:

> 当替换一个候选者的返回类型时忽略它是没有意义的，这可能会导致编译器选择另一个参数匹配更差的候选者。例如

```cpp
`basics/len2.hpp`

// number of elements in a raw array:]*\
template<typename T, [unsigned] N>
std::size_t len (T(&)[N)
{
  return N;
}
\
// number of elements for a type having]* size_type*[:]*\
template<typename T>
typename T::size_type len (T const& t)
{
  return t.size();
}
\
// fallback for all other types:]*\
std::size_t len (...)
{
  return 0;
}
```

Here, we also provide a general `len()` function that always matches but has the worst match (match with _ellipsis_ (`…`) in overload resolution (see Section [[C.2]] on page [[682]]).

> 在这里，我们还提供了一个通用的“len（）”函数，它总是匹配，但在过载解析中具有最差的匹配（与_ellipsis_（`…` 匹配）（见第[[682]]页的第[[C.2]]节）。

So, for raw arrays and vectors, we have two matches where the specific match is the better match. For pointers, only the fallback matches so that the compiler no longer complains about a missing `len()` for this call.[6] But for the allocator, the second and third function templates match, with the second function template as the better match. So, still, this results in an error that no `size()` member function can be called:

> 因此，对于原始数组和向量，我们有两个匹配，其中特定的匹配是更好的匹配。对于指针，只有回退匹配，这样编译器就不会再抱怨此调用缺少“len（）”。[6] 但对于分配器，第二个和第三个函数模板匹配，第二种函数模板匹配得更好。因此，这仍然会导致无法调用“size（）”成员函数的错误：

```cpp
int a[10];
std::cout << len(a);        // OK: [len()] for array is best match
std::cout << len(\"tmp");    //OK: [len()] for array is best match
\
`std::vector<int> v; std::cout << len(v);`        // OK: `len()` for a type with `size_type` is best match
\
int* p;
std::cout << len(p);        // OK: only fallback [len()] matches
\
`std::allocator<int> x; std::cout << len(x);`        // ERROR: 2nd `len()` function matches best,
                            //        but can't call `size()` for `x`
```

See Section [[15.7]] on page [[284]] for more details about SFINAE and Section [[19.4]] on page [[416]] about some applications of SFINAE.

> 有关 SFINAE 的更多详细信息，请参见第[[284]]页第[[15.7]]节，以及关于 SFINAE 某些应用的第[[416]]页第[19.4]]节。

##### SFINAE and Overload Resolution

Over time, the SFINAE principle has become so important and so prevalent among template designers that the abbreviation has become a verb. We say "we _SFINAE out_ a function" if we mean to apply the SFINAE mechanism to ensure that function templates are ignored for certain constraints by instrumenting the template code to result in invalid code for these constraints. And whenever you read in the C++ standard that a function template "_shall not participate in overload resolution unless..._" it means that SFINAE is used to "SFINAE out" that function template for certain cases.

> 随着时间的推移，SFINAE 原则在模板设计者中变得如此重要和普遍，以至于缩写已经成为一个动词。如果我们打算应用 SFINAE 机制，通过检测模板代码来确保某些约束的函数模板被忽略，从而导致这些约束的代码无效，那么我们称之为“We _SFINAE out_ a function”。每当你在 C++ 标准中读到函数模板“_除非…_，否则不应参与重载解析”时，这意味着 SFINAE 在某些情况下被用来“SFINAE out”该函数模板。

For example, class `std::thread` declares a constructor:

```cpp
namespace std {
  class thread {
    public:
      ...
      template<typename F, typename... Args>
        [explicit] thread(F&& f, Args&&... args);
    ...
  };
}
```

with the following remark:

_Remarks:_ This constructor shall not participate in overload resolution if `decay_t<F>` is the same type as `std::thread`.

> _备注：_如果 `decay_t<F>` 与 `std:：thread` 类型相同，则此构造函数不应参与重载解析。

This means that the template constructor is ignored if it is called with a `std::thread` as first and only argument. The reason is that otherwise a member template like this sometimes might better match than any predefined copy or move constructor (see Section [[6.2]] on page [[95]] and Section [[16.2.4]] on page [[333]] for details). By _SFINAE'ing out_ the constructor template when called for a thread, we ensure that the predefined copy or move constructor is always used when a thread gets constructed from another thread.[7]

> 这意味着，如果以“std:：thread”作为第一个也是唯一的参数调用模板构造函数，则会忽略它。原因是，在其他情况下，像这样的成员模板有时可能比任何预定义的复制或移动构造函数更好地匹配（详见第[[95]]页第[[6.2]]节和第[[333]]页第[16.2.4]]节）。通过在为线程调用构造函数模板时_SFINAE，我们确保在从另一个线程构造线程时始终使用预定义的复制或移动构造函数。7.

Applying this technique on a case-by-case basis can be unwieldy. Fortunately, the standard library provides tools to disable templates more easily. The best-known such feature is `std::enable_if<>`, which was introduced in Section [[6.3]] on page [[98]]. It allows us to disable a template just by replacing a type with a construct containing the condition to disable it.

> 在个案的基础上应用这种技术可能会很困难。幸运的是，标准库提供了更容易禁用模板的工具。最著名的此类功能是“std:：enable_if<>'，它在第[[98]]页的第[[6.3]]节中介绍。它允许我们禁用模板，只需将类型替换为包含禁用条件的构造即可。

As a consequence, the real declaration of `std::thread` typically is as follows:

> 因此，“std:：thread”的实际声明通常如下所示：

````cpp
namespace std {
  class thread {
    public:
      ...
      template<typename F, typename... Args, typename = std::enable_if_t<!std::is_same_v<std::decay_t<F>, thread>>>
        [explicit] thread(F&& f, Args&&... args);
      ...
  }; }```

See Section [[20.3]] on page [[469]] for details about how `std::enable_if<>` is implemented, using partial specialization and SFINAE.

#### 8.4.1 Expression SFINAE with **decltype**

It's not always easy to find out and formulate the right expression to _SFINAE out_ function templates for certain conditions.

Suppose, for example, that we want to ensure that the function template `len()` is ignored for arguments of a type that has a `size_type` member but not a `size()` member function. Without any form of requirements for a `size()` member function in the function declaration, the function template is selected and its ultimate instantiation then results in an error:

```cpp
template<typename T>
typename T::size_type len (T const& t)
{
  return t.size();
}
\
`std::allocator<int> x; std::cout << len(x) << ’\n`';        //ERROR: `len()` selected, but `x` has no `size()`
````

There is a common pattern or idiom to deal with such a situation:

- Specify the return type with the _trailing return type syntax_ (use `auto` at the front and `->` before the return type at the end).
- Define the return type using `decltype` and the comma operator.
- Formulate all expressions that must be valid at the beginning of the comma operator (converted to `void` in case the comma operator is overloaded).
- Define an object of the real return type at the end of the comma operator.

For example:

```cpp
template<typename T>
auto len (T const& t) -> decltype( (void)(t.size()), T::size_type() )
{
    return t.size();
}
```

Here the return type is given by

```cpp
decltype( (void)(t.size)(), T::size_type() )
```

The operand of the `decltype` construct is a comma-separated list of expressions, so that the last expression `T::size_type()` yields a value of the desired return type (which `decltype` uses to convert into the return type). Before the (last) comma, we have the expressions that must be valid, which in this case is just `t.size()`. The cast of the expression to `void` is to avoid the possibility of a user-defined comma operator overloaded for the type of the expressions.

Note that the argument of `decltype` is an _unevaluated operand_, which means that you, for example, can create "dummy objects" without calling constructors, which is discussed in Section [[11.2.3]] on page [[166]].

### 8.5 Compile-Time **if**

Partial specialization, SFINAE, and `std::enable_if` allow us to enable or disable templates as a whole. C++17 additionally introduces a compile-time `if` statement that allows is to enable or disable specific statements based on compile-time conditions. With the syntax `if constexpr(`... `)`, the compiler uses a compile-time expression to decide whether to apply the _then_ part or the _else_ part (if any).

As a first example, consider the variadic function template `print()` introduced in Section [[4.1.1]] on page [[55]]. It prints its arguments (of arbitrary types) using recursion. Instead of providing a separate function to end the recursion, the _constexpr if_ feature allows us to decide locally whether to continue the recursion:[8]

```cpp
template<typename T, typename... Types>
void print (T const& firstArg, Types const&... args)
{
  std::cout << firstArg << '\n';
  [if constexpr](sizeof]...(args) > 0) {

    print(args...);   //code only available if `sizeof…(args)>0` (since C++17) `   } }

> print（args…）；//只有当`sizeof…（args）>0`（自C++17以来）`}｝时，代码才可用
```

Here, if `print()` is called for one argument only, `args` becomes an empty parameter pack so that `sizeof…(args)` becomes 0. As a result, the recursive call of `print()` becomes a _discarded statement_, for which the code is not instantiated. Thus, a corresponding function is not required to exist and the recursion ends.

The fact that the code is not instantiated means that only the first translation phase (the _definition time_) is performed, which checks for correct syntax and names that don't depend on template parameters (see Section [[1.1.3]] on page [[6]]). For example:

```cpp
template<typename T>
void foo(T t)
{
  [if constexpr](std::is_integral_v<T>) {
    if (t > 0) {
      foo(t-1);   // OK
    }
  }
  [else] {

    undeclared(t);       // error if not declared and not discarded (i.e. [T] is not integral)

> 未申报（t）；//如果未声明且未丢弃，则出错（即[T]不是整数）
    undeclared();        // error if not declared (even if discarded)

    [static_assert]([false], "no integral"]);    // always asserts (even if discarded)

> [static_assert]（[false]，“无积分”]）；//总是断言（即使被丢弃）
    [static_assert](!std::is_integral_v<T>, "no integral");        //OK
  }
}
```

Note that `if constexpr` can be used in any function, not only in templates. We only need a compile-time expression that yields a Boolean value. For example:

```cpp
int main()
{
    [if constexpr](std::numeric_limits[<char]>::is_signed {
      foo(42);        // OK
  }
  [else] {
    undeclared(42);        // error if
    [undeclared()] not declared

    [static_assert]([false], "unsigned"]);          // always asserts (even if discarded)

> [static_assert]（[false]，“unsigned”]）；//总是断言（即使被丢弃）
    [static_assert](!std::numeric_limits<[char]>::is_signed,\
                  "char is unsigned");        //OK
} }
```

With this feature, we can, for example, use our `isPrime()` compile-time function, introduced in Section [[8.2]] on page [[125]], to perform additional code if a given size is not a prime number:

```cpp
template<typename T, std::size_t SZ>
void foo (std::array<T,SZ> const& coll)
{
  [if constexpr](!isPrime(SZ)) {

    ...    //special additional handling if the passed array has no prime number as size

>     ...//如果传递的数组没有素数作为大小，则进行特殊的附加处理
  }`\
  ...
}
```

See Section [[14.6]] on page [[263]] for further details.

### 8.6 Summary

```

- Templates provide the ability to compute at compile time (using recursion to iterate and partial specialization or operator `?:` for selections).

> -模板提供了在编译时进行计算的能力（使用递归进行迭代，并使用部分专用化或运算符“？：”进行选择）。

- With `constexpr` functions, we can replace most compile-time computations with "ordinary functions" that are callable in compile-time contexts.

> -使用“constexpr”函数，我们可以用在编译时上下文中可调用的“普通函数”来替换大多数编译时计算。

- With partial specialization, we can choose between different implementations of class templates based on certain compile-time constraints.

> -通过部分专业化，我们可以根据某些编译时间限制在类模板的不同实现之间进行选择。

- Templates are used only if needed *and* substitutions in function template declarations do not result in invalid code. This principle is called SFINAE (substitution failure is not an error).

> -只有在需要时才使用模板。函数模板声明中的*和*替换不会导致无效代码。这个原理被称为SFINAE（替换失败不是错误）。
- SFINAE can be used to provide function templates only for certain types and/or constraints.

- Since C++17, a compile-time `if` allows us to enable or discard statements according to compile-time conditions (even outside templates).

> -自C++17以来，编译时“if”允许我们根据编译时条件启用或丢弃语句（甚至在模板之外）。


^[1]^ In fact, it was Erwin Unruh who first found it out by presenting a program computing prime numbers at compile time. See Section [[23.7]] on page [[545]] for details.

> ^[1] ^事实上，是Erwin Unruh通过在编译时提供一个计算素数的程序首次发现了这一点。详见第[[545]]页第[[23.7]节。

^[2]^ Before C++11, it was common to declare the `value` members as enumerator constants instead of static data members to avoid the need to have an out-of-class definition of the static data member (see Section [[23.6]] on page [[543]] for details). For example:

> ^[2] ^在C++11之前，通常将“value”成员声明为枚举器常量，而不是静态数据成员，以避免需要对静态数据成员进行类外定义（有关详细信息，请参见第[[543]]页的第[[23.6]]节）。例如

```

enum ;

```

^[3]^ At the time of writing this book in 2012\"fn\">^[4]^ Theoretically, even with `constexpr`, the compiler can decide to compute the initial value of `b` at run time.

> ^[3] ^在2012年撰写本书时\“fn \”>^[4]理论上，即使使用“constexpr”，编译器也可以决定在运行时计算“b”的初始值。


^[5]^ We don't name this function `size()` because we want to avoid a naming conflict with the C++ standard library, which defines a standard function template `std::size()` since C++17.

> ^[5] ^我们不将此函数命名为“size（）”，因为我们希望避免与C++标准库的命名冲突，C++标准库自C++17以来定义了一个标准函数模板“std:：size（））”。


^[6]^ In practice, such a fallback function would usually provide a more useful default, throw an exception, or contain a static assertion to result in a useful error message.

> ^[6] ^在实践中，这样的回退函数通常会提供更有用的默认值、引发异常或包含静态断言以产生有用的错误消息。


^[7]^ Since the copy constructor for class `thread` is deleted, this also ensures that copying is forbidden.

> ^[7] ^由于类“thread”的复制构造函数被删除，这也确保了复制被禁止。


^[8]^ Although the code reads `if constexpr`, the feature is called *constexpr if*, because it is the "constexpr" form of `if` (and for historical reasons).

> ^[8] ^虽然代码读作“if constexpr”，但该功能被称为*constexpr if*，因为它是“if”的“constexpr“形式（出于历史原因）。
```

## Chapter 9

## Using Templates in Practice

Template code is a little different from ordinary code. In some ways templates lie somewhere between macros and ordinary (nontemplate) declarations. Although this may be an oversimplification, it has consequences not only for the way we write algorithms and data structures using templates but also for the day-to-day logistics of expressing and analyzing programs involving templates.

In this chapter we address some of these practicalities without necessarily delving into the technical details that underlie them. Many of these details are explored in [Chapter [14]]. To keep the discussion simple, we assume that our C++ compilation systems consist of fairly traditional compilers and linkers (C++ systems that don't fall in this category are rare).

### 9.1 The Inclusion Model

There are several ways to organize template source code. This section presents the most popular approach: the inclusion model.

#### 9.1.1 Linker Errors

Most C and C++ programmers organize their nontemplate code largely as follows:

• Classes and other types are entirely placed in _header files_. Typically, this is a file with a `.hpp` (or `.H`, `.h`, `.hh`, `.hxx`) filename extension.

• For global (noninline) variables and (noninline) functions, only a declaration is put in a header file, and the definition goes into a file compiled as its own translation unit. Such a _CPP file_ typically is a file with a `.cpp` (or `.C`, `.c`, `.cc`, or `.cxx`) filename extension.

This works well: It makes the needed type definition easily available throughout the program and avoids duplicate definition errors on variables and functions from the linker.

With these conventions in mind, a common error about which beginning template programmers complain is illustrated by the following (erroneous) little program. As usual for "ordinary code," we declare the template in a header file:

```cpp
*basics/myfirst.hpp*

#ifndef MYFIRST_HPP\
#define MYFIRST_HPP\
\
// declaration of template]*\
template<typename T>
void printTypeof (T const&);
\
#endif   //MYFIRST_HPP]*
```

`printTypeof()` is the declaration of a simple auxiliary function that prints some type information. The implementation of the function is placed in a CPP file:

```cpp
*basics/myfirst.cpp*

#include <iostream>
#include <typeinfo>
#include "myfirst.hpp"\
\
// implementation/definition of template]*\
template<typename T>
void printTypeof (T const& x)
{
    std::cout << [typeid](x).name() << '\n';
}
```

The example uses the `typeid` operator to print a string that describes the type of the expression passed to it. It returns an lvalue of the static type `std::type_info`, which provides a member function `name()` that shows the types of some expressions. The C++ standard doesn't actually say that `name()` must return something meaningful, but on good C++ implementations, you should get a string that gives a good description of the type of the expression passed to `typeid`.[1]

Finally, we use the template in another CPP file, into which our template declaration is `#include` d:

```cpp
*basics/myfirstmain.cpp*

#include "myfirst.hpp"\
\
// use of the template]*\
int main()
{
    [double] ice = 3.0;
    printTypeof(ice);    // call function template for type]* [double]\
}
```

A C++ compiler will most likely accept this program without any problems, but the linker will probably report an error, implying that there is no definition of the function `printTypeof()`.

The reason for this error is that the definition of the function template `printTypeof()` has not been instantiated. In order for a template to be instantiated, the compiler must know which definition should be instantiated and for what template arguments it should be instantiated. Unfortunately, in the previous example, these two pieces of information are in files that are compiled separately. Therefore, when our compiler sees the call to `printTypeof()` but has no definition in sight to instantiate this function for `double`, it just assumes that such a definition is provided elsewhere and creates a reference (for the linker to resolve) to that definition. On the other hand, when the compiler processes the file `myfirst.cpp`, it has no indication at that point that it must instantiate the template definition it contains for specific arguments.

#### 9.1.2 Templates in Header Files

The common solution to the previous problem is to use the same approach that we would take with macros or with inline functions: We include the definitions of a template in the header file that declares that template.

That is, instead of providing a file `myfirst.cpp`, we rewrite `myfirst.hpp` so that it contains all template declarations _and_ template definitions:

```cpp
*basics/myfirst2.hpp*

#ifndef MYFIRST_HPP\
#define MYFIRST_HPP\
\
#include <iostream>
#include <typeinfo>
\
// declaration of template]*\
template<typename T>
void printTypeof (T const&);
\
// implementation/definition of template]*\
template<typename T>
void printTypeof (T const& x)
{
    std::cout << [typeid](x).name() << '\n'; }
\
#endif   //MYFIRST_HPP]*
```

This way of organizing templates is called the _inclusion model_. With this in place, you should find that our program now correctly compiles, links, and executes.

There are a few observations we can make at this point. The most notable is that this approach has considerably increased the cost of including the header file `myfirst.hpp`. In this example, the cost is not the result of the size of the template definition itself but the result of the fact that we must also include the headers used by the definition of our template---in this case `<iostream>` and `<typeinfo>`. You may find that this amounts to tens of thousands of lines of code because headers like `<iostream>` contain many template definitions of their own.

This is a real problem in practice because it considerably increases the time needed by the compiler to compile significant programs. We will therefore examine some possible ways to approach this problem, including precompiled headers (see Section [[9.3]] on page [[141]]) and the use of explicit template instantiation (see Section [[14.5]] on page [[260]]).

Despite this build-time issue, we do recommend following this inclusion model to organize your templates when possible until a better mechanism becomes available. At the time of writing this book in 2017, such a mechanism is in the works: _modules_, which is introduced in Section [[17.11]] on page [[366]]. They are a language mechanism that allows the programmer to more logically organize code in such a way that a compiler can separately compile all declarations and then efficiently and selectively import the processed declarations whenever needed.

Another (more subtle) observation about the inclusion approach is that noninline function templates are distinct from inline functions and macros in an important way: They are not expanded at the call site. Instead, when they are instantiated, they create a new copy of a function. Because this is an automatic process, a compiler could end up creating two copies in two different files, and some linkers could issue errors when they find two distinct definitions for the same function. In theory, this should not be a concern of ours: It is a problem for the C++ compilation system to accommodate. In practice, things work well most of the time, and we don't need to deal with this issue at all. For large projects that create their own library of code, however, problems occasionally show up. A discussion of instantiation schemes in [Chapter [14]] and a close study of the documentation that came with the C++ translation system (compiler) should help address these problems.

Finally, we need to point out that what applies to the ordinary function template in our example also applies to member functions and static data members of class templates, as well as to member function templates.

### 9.2 Templates and **inline**

Declaring functions to be inline is a common tool to improve the running time of programs. The `inline` specifier was meant to be a hint for the implementation that inline substitution of the function body at the point of call is preferred over the usual function call mechanism.

However, an implementation may ignore the hint. Hence, the only guaranteed effect of `inline` is to allow a function definition to appear multiple times in a program (usually because it appears in a header file that is included in multiple places).

Like inline functions, function templates can be defined in multiple translation units. This is usually achieved by placing the definition in a header file that is included by multiple CPP files.

This doesn't mean, however, that function templates use inline substitutions by default. It is entirely up to the compiler whether and when inline substitution of a function template body at the point of call is preferred over the usual function call mechanism. Perhaps surprisingly, compilers are often better than programmers at estimating whether inlining a call would lead to a net performance improvement. As a result, the precise policy of a compiler with respect to `inline` varies from compiler to compiler, and even depends on the options selected for a specific compilation.

Nevertheless, with appropriate performance monitoring tools, a programmer may have better information than a compiler and may therefore wish to override compiler decisions (e.g., when tuning software for particular platforms, such as mobiles phones, or particular inputs). Sometimes this is only possible with compiler-specific attributes such as `noinline` or `always_inline`.

It's worth pointing out at this point that full specializations of function templates act like ordinary functions in this regard: Their definition can appear only once unless they're defined `inline` (see Section [[16.3]] on page [[338]]). See also [Appendix [A]] for a broader, detailed overview of this topic.

### 9.3 Precompiled Headers

Even without templates, C++ header files can become very large and therefore take a long time to compile. Templates add to this tendency, and the outcry of waiting programmers has in many cases driven vendors to implement a scheme usually known as _precompiled headers_ (_PCH_). This scheme operates outside the scope of the standard and relies on vendor-specific options. Although we leave the details on how to create and use precompiled header files to the documentation of the various C++ compilation systems that have this feature, it is useful to gain some understanding of how it works.

When a compiler translates a file, it does so starting from the beginning of the file and working through to the end. As it processes each token from the file (which may come from `#include` d files), it adapts its internal state, including such things as adding entries to a table of symbols so they may be looked up later. While doing so, the compiler may also generate code in object files.

The precompiled header scheme relies on the fact that code can be organized in such a manner that many files start with the same lines of code. Let's assume for the sake of argument that every file to be compiled starts with the same _N_ lines of code. We could compile these _N_ lines and save the complete state of the compiler at that point in a _precompiled header_. Then, for every file in our program, we could reload the saved state and start compilation at line _N+1_. At this point it is worthwhile to note that reloading the saved state is an operation that can be orders of magnitude faster than actually compiling the first _N_ lines. However, saving the state in the first place is typically more expensive than just compiling the _N_ lines. The increase in cost varies roughly from 20 to 200 percent.

#include <iostream>

The key to making effective use of precompiled headers is to ensure that---as much as possible--- files start with a maximum number of common lines of code. In practice this means the files must start with the same `#include` directives, which (as mentioned earlier) consume a substantial portion of our build time. Hence, it can be very advantageous to pay attention to the order in which headers are included. For example, the following two files:

#include <vector>
    #include <list>
    ...

and

#include <list>
    #include <vector>
    ...

inhibit the use of precompiled headers because there is no common initial state in the sources.

Some programmers decide that it is better to `#include` some extra unnecessary headers than to pass on an opportunity to accelerate the translation of a file using a precompiled header. This decision can considerably ease the management of the inclusion policy. For example, it is usually relatively straightforward to create a header file named `std.hpp` that includes all the standard headers:[2]

#include <iostream>
    #include <string>
    #include <vector>
    #include <deque>
    #include <list>
    ...

This file can then be precompiled, and every program file that makes use of the standard library can then simply be started as follows:

#include "std.hpp"
    ...

Normally this would take a while to compile, but given a system with sufficient memory, the pre-compiled header scheme allows it to be processed significantly faster than almost any single standard header would require without precompilation. The standard headers are particularly convenient in this way because they rarely change, and hence the precompiled header for our `std.hpp` file can be built once. Otherwise, precompiled headers are typically part of the dependency configuration of a project (e.g., they are updated as needed by the popular `make` tool or an integrated development environment's (IDE) project build tool).

One attractive approach to manage precompiled headers is to create _layers_ of precompiled headers that go from the most widely used and stable headers (e.g., our `std.hpp` header) to headers that aren't expected to change all the time and therefore are still worth precompiling. However, if headers are under heavy development, creating precompiled headers for them can take more time than what is saved by reusing them. A key concept to this approach is that a precompiled header for a more stable layer can be reused to improve the precompilation time of a less stable header. For example, suppose that in addition to our `std.hpp` header (which we have precompiled), we also define a `core.hpp` header that includes additional facilities that are specific to our project but nonetheless achieve a certain level of stability:

#include "std.hpp"
    #include "core_data.hpp]
    #include "core_algos.hpp"
    ...

Because this file starts with `#include "std.hpp"`, the compiler can load the associated precom-piled header and continue with the next line without recompiling all the standard headers. When the file is completely processed, a new precompiled header can be produced. Applications can then use `#include "core.hpp"` to provide access quickly to large amounts of functionality because the compiler can load the latter precompiled header.

### 9.4 Decoding the Error Novel

Ordinary compilation errors are normally quite succinct and to the point. For example, when a compiler says "`class X has no member ’fun’`," it usually isn't too hard to figure out what is wrong in our code (e.g., we might have mistyped `run` as `fun`). Not so with templates. Let's look at some examples.

##### Simple Type Mismatch

Consider the following relatively simple example using the C++ standard library:

_basics/errornovel1.cpp_

#include <string>
#include <map>
#include <algorithm>
int main()
{
    std::map[std::string,[double]](std::string,%5Bdouble%5D) coll;
    ...
    // find the first nonempty string in]_ [coll]_[:]\*
    auto pos = std::find_if (coll.begin(), coll.end(),
                    `[] (std::string const& s));`
}

It contains a fairly small mistake: In the lambda used to find the first matching string in the collection, we check against a given string. However, the elements in a map are key/value pairs, so that we should expect a `std::pair<std::string const, double>`.

A version of the popular GNU C++ compiler reports the following error:

1   In file included from /cygdrive/p/gcc/gcc61-include/bits/stl*algobase.h:71:0,
2  from /cygdrive/p/gcc/gcc61-include/bits/char_traits.h:39,
3  from /cygdrive/p/gcc/gcc61-include/string:40,
4  from errornovel1.cpp:1:
5   /cygdrive/p/gcc/gcc61-include/bits/predefined_ops.h: In instantiation of \'bool \_\_gnu_cxx
      ::\_\_ops::\_Iter_pred<\_Predicate>::operator()(\_Iterator) [with _Iterator = std::\_Rb_tree_i
      terator[std::pair[const std::\_\_cxx11::basic_string<char](std::pair%3Cconst%C2%A0std::%5C*%5C*cxx11::basic_string%3Cchar), double](const%C2%A0std::%5C_%5C_cxx11::basic_string%3Cchar%5D(std::pair%3Cconst%C2%A0std::%5C*%5C*cxx11::basic_string%3Cchar),%C2%A0double) >; _Predicate = main()
       ::<lambda(const string&)>]\':
6  /cygdrive/p/gcc/gcc61-include/bits/stl_algo.h:104:42:  required from \'\_InputIterator
      std::\_\_find_if(\_InputIterator, _InputIterator, _Predicate, std::input_iterator_tag)
      [with _InputIterator = std::\_Rb_tree_iterator[std::pair[const std::\_\_cxx11::basic_string\
        <char](std::pair%3Cconst%C2%A0std::%5C*%5C*cxx11::basic_string%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%3Cchar), double](const%C2%A0std::%5C_%5C_cxx11::basic_string%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%3Cchar%5D(std::pair%3Cconst%C2%A0std::%5C*%5C*cxx11::basic_string%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%3Cchar),%C2%A0double) >; _Predicate = \_\_gnu_cxx::\_\_ops::\_Iter_pred[main()::[lambda(const\
        string&)](<main()::%3Clambda(const%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0string&)](lambda(const%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0string&)%5D(%3Cmain()::%3Clambda(const%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0string&))) >]\'
7  /cygdrive/p/gcc/gcc61-include/bits/stl_algo.h:161:23:  required from \'\_Iterator std::\_\_
      find_if(\_Iterator, _Iterator, _Predicate) [with _Iterator = std::\_Rb_tree_iterator[std::
      pair[const std::\_\_cxx11::basic_string<char](std::%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0pair%3Cconst%C2%A0std::%5C*%5C*cxx11::basic_string%3Cchar), double](const%C2%A0std::%5C_%5C_cxx11::basic_string%3Cchar%5D(std::%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0pair%3Cconst%C2%A0std::%5C*%5C*cxx11::basic_string%3Cchar),%C2%A0double) >; _Predicate = \_\_gnu_cxx::\_\_ops::\_
      Iter_pred[main()::[lambda(const string&)](<main()::%3Clambda(const%C2%A0string&)](lambda(const%C2%A0string&)%5D(%3Cmain()::%3Clambda(const%C2%A0string&))) >]\'
8  /cygdrive/p/gcc/gcc61-include/bits/stl_algo.h:3824:28:  required from \'\_IIter std::find
      _if(\_IIter, _IIter, _Predicate) [with _IIter = std::\_Rb_tree_iterator[std::pair[const\
      std::\_\_cxx11::basic_string<char](std::pair%3Cconst%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0std::%5C*%5C*cxx11::basic_string%3Cchar), double](const%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0std::%5C_%5C_cxx11::basic_string%3Cchar%5D(std::pair%3Cconst%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0std::%5C*%5C*cxx11::basic_string%3Cchar),%C2%A0double) >; _Predicate = main()::<lambda(const string&)
      >]\'
9   errornovel1.cpp:13:29:     required from here
10 /cygdrive/p/gcc/gcc61-include/bits/predefined_ops.h:234:11: error: no match for call to
      \'(main()::<lambda(const string&)>) (std::pair[const std::\_\_cxx11::basic_string[char](const%C2%A0std::%5C*%5C*cxx11::basic_string%3Cchar),
      double](char%5D(const%C2%A0std::%5C*%5C*cxx11::basic_string%3Cchar),%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0double)&)'
11    
12  \^\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~
13 /cygdrive/p/gcc/gcc61-include/bits/predefined_ops.h:234:11: note: candidate: bool (\*)(
      const string&)  <conversion>
14 /cygdrive/p/gcc/gcc61-include/bits/predefined_ops.h:234:11: note:     candidate expects 2
      arguments, 2 provided
15 errornovel1.cpp:11:52: note: candidate: main()::<lambda(const string&)>
16  [] (std::string const& s) {
17  \^
18 errornovel1.cpp:11:52: note:     no known conversion for argument 1 from \'std::pair[const
      std::\_\_cxx11::basic_string[char](const%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0std::%5C*%5C_cxx11::basic_string%3Cchar), double](char%5D(const%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0std::%5C*%5C_cxx11::basic_string%3Cchar),%C2%A0double)\' to \'const string& {aka const std::\_\_cxx11::
      basic_string<char>&}'\

A message like this starts looking more like a novel than a diagnostic. It can also be overwhelming to the point of discouraging novice template users. However, with some practice, messages like this become manageable, and the errors are at least relatively easily located.

The first part of this error message says that an error occurred in a function template instance deep inside an internal `predefined_ops.h` header, included from `errornovel1.cpp` via various other headers. Here and in the following lines, the compiler reports what was instantiated with which arguments. In this case, it all started with the statement ending on line 13 of `errornovel1.cpp`, which is:

auto pos = std::find_if (coll.begin(), coll.end(),                     `[] (std::string const& s) );`

This caused the instantiation of a `find_if` template on line 115 of the `stl_algo.h` header, where the code

`_IIter std::find_if(_IIter, _IIter, _Predicate)`

is instantiated with

\_IIter = std::\_Rb_tree_iterator<std::pair<const std::\_\_cxx11::basic_string<char>,
                        double> >
\_Predicate = main()::<lambda(const string&)>

The compiler reports all this in case we simply were not expecting all these templates to be instantiated. It allows us to determine the chain of events that caused the instantiations.

However, in our example, we're willing to believe that all kinds of templates needed to be instantiated, and we just wonder why it didn't work. This information comes in the last part of the message: The part that says "`no match for call" implies that a function call could not be resolved because the types of the arguments and the parameter types didn't match. It lists what is called

(main()::<lambda(const string&)>) (std::pair<const std::\_\_cxx11::basic_string<char>,
                            double>&)

and code that caused this call:

Furthermore, just after this, the line containing "`note: candidate:" explains that there was a single candidate type expecting a ` const string&`and that this candidate is defined in line 11 of` errornovel1.cpp `as lambda`[] (std::string const& s)` combined with a reason why a possible candidate didn't fit:

`no known conversion for argument 1 from ’std::pair<const std::__cxx11::basic_string<char>, double>’ to ’const string& ’`

which describes the problem we have.

There is no doubt that the error message could be better. The actual problem could be emitted before the history of the instantiation, and instead of using fully expanded template instantiation names like `std::__cxx11::basic_string<char>`, using just `std::string` might be enough. However, it is also true that all the information in this diagnostic could be useful in some situations. It is therefore not surprising that other compilers provide similar information (although some use the structuring techniques mentioned).

For example, the Visual C++ compiler outputs something like:

1   c:\\tools_root\\cl\\inc\\algorithm(166): error C2664: \'bool main::<lambda_b863c1c7cd07048816
      f454330789acb4>::operator ()(const std::string &) const\': cannot convert argument 1 from
      \'std::pair<const _Kty,\_Ty>\' to \'const std::string &\'
2        with
3        [
4              \_Kty=std::string,
5              \_Ty=double
6        ]
7   c:\\tools_root\\cl\\inc\\algorithm(166): note: Reason: cannot convert from \'std::pair<const
      _Kty,\_Ty>\' to \'const std::string\'
8        with
9        [
10              \_Kty=std::string,
11              \_Ty=double
12        ]
13 c:\\tools_root\\cl\\inc\\algorithm(166): note: No user-defined-conversion operator available
   that can perform this conversion, or the operator cannot be called
14 c:\\tools_root\\cl\\inc\\algorithm(177): note: see reference to function template instantiat
   ion \'\_InIt std::\_Find_if_unchecked[std::\_Tree_unchecked_iterator[\_Mytree](std::%5C_Tree_unchecked_iterator%3C%5C_Mytree),\_Pr](%5C_Mytree%5D(std::%5C_Tree_unchecked_iterator%3C%5C_Mytree),%5C_Pr)(\_InIt,\_In
   It,\_Pr &)' being compiled
15        with
16        [
17            _InIt=std::\_Tree_unchecked_iterator[std::\_Tree_val[std::\_Tree_simple_types\
              <std::pair<const std::string,double](std::%5C_Tree_val%3Cstd::%5C_Tree_simple_types%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%3Cstd::pair%3Cconst%C2%A0std::string,double)](std::%5C_Tree_simple_types%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%3Cstd::pair%3Cconst%C2%A0std::string,double%5D(std::%5C_Tree_val%3Cstd::%5C_Tree_simple_types%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%3Cstd::pair%3Cconst%C2%A0std::string,double))>>,
18            _Mytree=std::\_Tree_val[std::\_Tree_simple_types[std::pair<const std::string,\
              double](std::%5C_Tree_simple_types%3Cstd::pair%3Cconst%C2%A0std::string,%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0double)](std::pair%3Cconst%C2%A0std::string,%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0double%5D(std::%5C_Tree_simple_types%3Cstd::pair%3Cconst%C2%A0std::string,%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0double))>,
19            _Pr=main::<lambda_b863c1c7cd07048816f454330789acb4>
20        ]
21 main.cpp(13): note: see reference to function template instantiation \'\_InIt std::find_if
   [std::\_Tree_iterator[std::\_Tree_val<std::\_Tree_simple_types<std::pair<const _Kty,\_Ty](std::%5C_Tree_iterator%3Cstd::%5C_Tree_val%3Cstd::%5C_Tree_simple_types%3Cstd::pair%3Cconst%C2%A0_Kty,%5C_Ty)](std::%5C_Tree_val%3Cstd::%5C_Tree_simple_types%3Cstd::pair%3Cconst%C2%A0_Kty,%5C_Ty%5D(std::%5C_Tree_iterator%3Cstd::%5C_Tree_val%3Cstd::%5C_Tree_simple_types%3Cstd::pair%3Cconst%C2%A0_Kty,%5C_Ty))>>
   ,main::<lambda_b863c1c7cd07048816f454330789acb4>>(\_InIt,\_InIt,\_Pr)' being compiled
22        with
23        [
24            _InIt=std::\_Tree_iterator[std::\_Tree_val[std::\_Tree_simple_types<std::pair<\
              const std::string,double](std::%5C_Tree_val%3Cstd::%5C_Tree_simple_types%3Cstd::pair%3C%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0const%C2%A0std::string,double)](std::%5C_Tree_simple_types%3Cstd::pair%3C%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0const%C2%A0std::string,double%5D(std::%5C_Tree_val%3Cstd::%5C_Tree_simple_types%3Cstd::pair%3C%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0const%C2%A0std::string,double))>>,
25            _Kty=std::string,
26            _Ty=double,
27            _Pr=main::<lambda_b863c1c7cd07048816f454330789acb4>
28        ]\

Here, again, we provide the chain of instantiations with the information telling us what was instantiated by which arguments and where in the code, and we see twice that we

`cannot convert from ’std::pair<const _Kty,_Ty>’ to ’const std::string’ with [     _Kty=std::string,     _Ty=double ]`

**Missing `const` on Some Compilers**

Unfortunately, it sometimes happens that generic code is a problem only with some compilers. Consider the following example:

_basics/errornovel2.cpp_

#include <string>
#include <unordered_set>

class Customer
{
  private:
    std::string name;
  public:

Customer (std::string const& n)
     : name(n) {
    }
    std::string getName() const {
     return name;
  }
};
int main()
{

// provide our own hash function:]_
   struct MyCustomerHash {
     // NOTE: missing]_ const _[is only an error with g++ and clang:]_
     std::size_t [operator]() (Customer const& c) {
      return std::hash[std::string](std::string)()(c.getName());
   }
};

// and use it for a hash table of]_ Customer_[s:]_
   std::unordered_set<Customer,MyCustomerHash> coll; _...
\*}

With Visual Studio 2013 or 2015, this code compiles as expected. However, with g++ or clang, the code causes significant error messages. On g++ 6.1, for example, the first error message is as follows:

1   In file included from /cygdrive/p/gcc/gcc61-include/bits/hashtable.h:35:0,
2     from /cygdrive/p/gcc/gcc61-include/unordered*set:47,
3     from errornovel2.cpp:2:
4   /cygdrive/p/gcc/gcc61-include/bits/hashtable_policy.h: In instantiation of \'struct std::
      \_\_detail::\_\_is_noexcept_hash<Customer, main()::MyCustomerHash>\':
5   /cygdrive/p/gcc/gcc61-include/type_traits:143:12:     required from \'struct std::\_\_and\_[
      std::\_\_is_fast_hash<main()::MyCustomerHash](%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0std::%5C*%5C*is_fast_hash%3Cmain()::MyCustomerHash), std::\_\_detail::\_\_is_noexcept_hash[Customer,
      main()::MyCustomerHash](Customer,%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0main()::MyCustomerHash) >\'
6   /cygdrive/p/gcc/gcc61-include/type_traits:154:38:     required from \'struct std::\_\_not\_[
      std::\_\_and\_<std::\_\_is_fast_hash<main()::MyCustomerHash](%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0std::%5C*%5C*and%5C*%3Cstd::%5C_%5C_is_fast_hash%3Cmain()::MyCustomerHash), std::\_\_detail::\_\_is_noexcept\_
      hash<Customer, main()::MyCustomerHash> > >\'
7  /cygdrive/p/gcc/gcc61-include/bits/unordered_set.h:95:63:  required from \'class std::
      unordered_set<Customer, main()::MyCustomerHash>\'
8   errornovel2.cpp:28:47:     required from here
9   /cygdrive/p/gcc/gcc61-include/bits/hashtable_policy.h:85:34: error: no match for call to
      \'(const main()::MyCustomerHash) (const Customer&)'
10     noexcept(declval<const \_Hash&>()(declval<const \_Key&>()))>
11  \~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\^\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~
12 errornovel2.cpp:22:17: note: candidate: std::size_t main()::MyCustomerHash::operator()(
      const Customer&) <near match>
13     std::size_t operator() (const Customer& c) {
14  \^\~\~\~\~\~\~\~
15 errornovel2.cpp:22:17: note:     passing \'const main()::MyCustomerHash\*\' as \'this\' argument
      discards qualifiers

immediately followed by more than 20 other error messages:

16 In file included from /cygdrive/p/gcc/gcc61-include/bits/move.h:57:0,
18      from /cygdrive/p/gcc/gcc61-include/bits/stl*pair.h:59,
19      from /cygdrive/p/gcc/gcc61-include/bits/stl_algobase.h:64,
20      from /cygdrive/p/gcc/gcc61-include/bits/char_traits.h:39,
21      from /cygdrive/p/gcc/gcc61-include/string:40,
22      from errornovel2.cpp:1:
23 /cygdrive/p/gcc/gcc61-include/type_traits: In instantiation of \'struct std::\_\_not\_[std::
      \_\_and\_<std::\_\_is_fast_hash<main()::MyCustomerHash](std::%5C%0A%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%C2%A0%5C*%5C*and%5C*%3Cstd::%5C_%5C_is_fast_hash%3Cmain()::MyCustomerHash), std::\_\_detail::\_\_is_noexcept_hash<
      Customer, main()::MyCustomerHash> > >\':

24 /cygdrive/p/gcc/gcc61-include/bits/unordered*set.h:95:63:     required from \'class std::
      unordered_set<Customer, main()::MyCustomerHash>\'
25 errornovel2.cpp:28:47:     required from here
26 /cygdrive/p/gcc/gcc61-include/type_traits:154:38: error: \'value\' is not a member of \'std
      ::\_\_and\_[std::\_\_is_fast_hash<main()::MyCustomerHash](std::%5C*%5C*is_fast_hash%3Cmain()::MyCustomerHash), std::\_\_detail::\_\_is_noexcept_hash<
      Customer, main()::MyCustomerHash> >\'
27      : public integral_constant<bool, !\_Pp::value>
28  \^\~\~\~
29 In file included from /cygdrive/p/gcc/gcc61-include/unordered_set:48:0,
30  from errornovel2.cpp:2:
31 /cygdrive/p/gcc/gcc61-include/bits/unordered_set.h: In instantiation of \'class std::
      unordered_set<Customer, main()::MyCustomerHash>\':
32 errornovel2.cpp:28:47:     required from here
33 /cygdrive/p/gcc/gcc61-include/bits/unordered_set.h:95:63: error: \'value\' is not a member
      of \'std::\_\_not\_[std::\_\_and\_<std::\_\_is_fast_hash<main()::MyCustomerHash](std::%5C*%5C*and%5C*%3Cstd::%5C*%5C_is_fast_hash%3Cmain()::MyCustomerHash), std::\_\_detail::
      \_\_is_noexcept_hash<Customer, main()::MyCustomerHash> > >\'
34  typedef \_\_uset_hashtable<\_Value, \_Hash, \_Pred, \_Alloc>   \_Hashtable;
35 \^\~\~\~\~\~\~\~\~\~
36 /cygdrive/p/gcc/gcc61-include/bits/unordered_set.h:102:45: error: \'value\' is not a member
      of \'std::\_\_not\_[std::\_\_and\_<std::\_\_is_fast_hash<main()::MyCustomerHash](std::%5C*%5C*and%5C*%3Cstd::%5C_%5C_is_fast_hash%3Cmain()::MyCustomerHash), std::\_\_detail::
      \_\_is_noexcept_hash<Customer, main()::MyCustomerHash> > >\'
37  typedef typename \_Hashtable::key_type key_type;
38  \^\~\~\~\~\~\~\~
...

Again, it's hard to read the error message (even finding the beginning and end of each message is a chore). The essence is that deep in header file `hashtable_policy.h` in the instantiation of `std::unordered_set<>` required by

std::unordered_set<Customer,MyCustomerHash> coll;

there is no match for the call to

const main()::MyCustomerHash (const Customer&)

in the instantiation of

[noexcept](declval<const \_Hash&>()(declval[<const \_Key&>()))>
        \~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\^\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~

(`declval<const _Hash&>()` is an expression of type `main()::MyCustomerHash`). A possible "near match" candidate is

`std::size_t main()::MyCustomerHash::operator()(const Customer&)`

which is declared as

`std::size_t operator() (const Customer& c) {`
        `^~~~~~~~`

and the last note says something about the problem:

`passing ’const main()::MyCustomerHash*’ as ’this’ argument discards qualifiers`

Can you see what the problem is? This implementation of the `std::unordered_set` class template requires that the function call operator for the hash object be a `const` member function (see also Section [[11.1.1]] on page [[159]]). When that's not the case, an error arises deep in the guts of the algorithm.

All other error messages cascade from the first and go away when a `const` qualifier is simply added to the hash function operator:

````cpp
std::size_t [operator]() (const Customer& c) const {
...
}```


Clang 3.9 gives the slightly better hint at the end of the first error message that `operator()` of the hash functor is not marked `const`:

> Clang 3.9在第一条错误消息的末尾给出了一个稍微好一点的提示，即哈希函数的“operator（）”没有标记为“const”：

```cpp
...
errornovel2.cpp:28:47: note: in instantiation of template class 'std::unordered_set<Customer\
, MyCustomerHash, std::equal_to<Customer>, std::allocator<Customer> >' requested here\
  std::unordered_set<Customer,MyCustomerHash> coll;
                                              \^\
\
errornovel2.cpp:22:17: note: candidate function not viable: 'this' argument has type 'const\
MyCustomerHash', but method is not marked const\
    std::size_t operator() (const Customer& c) {
                \^
````

Note that clang here mentions default template parameters such as `std::allocator<Customer>`, while gcc skips them.

> 请注意，clang 在这里提到了默认的模板参数，如“std:：allocater＜Customer＞”，而 gcc 则跳过了这些参数。

As you can see, it is often helpful to have more than one compiler available to test your code. Not only does it help you write more portable code, but where one compiler produces a particularly inscrutable error message, another might provide more insight.

> 正如您所看到的，拥有多个编译器来测试代码通常是很有帮助的。它不仅可以帮助您编写更可移植的代码，而且当一个编译器产生特别难以理解的错误消息时，另一个编译器可能会提供更多的见解。

### 9.5 Afternotes

The organization of source code in header files and CPP files is a practical consequence of various incarnations of the _one-definition rule_ or _ODR_. An extensive discussion of this rule is presented in [Appendix [A]].

> 头文件和 CPP 文件中源代码的组织是定义规则_或_ODR_的各种体现的实际结果。对该规则的广泛讨论见[附录[A]]。

The inclusion model is a pragmatic answer dictated largely by existing practice in C++ compiler implementations. However, the first C++ implementation was different: The inclusion of template definitions was implicit, which created a certain illusion of _separation_ (see [Chapter [14]] for details on this original model).

> 包含模型是一个实用的答案，主要由 C++ 编译器实现中的现有实践决定。然而，第一个 C++ 实现是不同的：模板定义的包含是隐含的，这造成了_separation_的某种错觉（有关此原始模型的详细信息，请参见[第[14]]章）。

The first C++ standard ([C++98]) provided explicit support for the _separation model_ of template compilation via _exported templates_. The separation model allowed template declarations marked as `export` to be declared in headers, while their corresponding definitions were placed in CPP files, much like declarations and definitions for nontemplate code. Unlike the inclusion model, this model was a theoretical model not based on any existing implementation, and the implementation itself proved far more complicated than the C++ standardization committee had anticipated. It took more than five years to see its first implementation published (May 2002), and no other implementations appeared in the years since. To better align the C++ standard with existing practice, the C++ standardization committee removed exported templates from C++11. Readers interested in learning more about the details (and pitfalls) of the separation model are encouraged to read Sections 6.3 and 10.3 of the first edition of this book ([VandevoordeJosuttisTemplates1st]).

> 第一个 C++ 标准（[C++98]）通过导出模板为模板编译的分离模型提供了明确的支持。分离模型允许在标头中声明标记为“export”的模板声明，而其相应的定义则放置在 CPP 文件中，非常类似于非模板代码的声明和定义。与包含模型不同，该模型是一个不基于任何现有实现的理论模型，事实证明，实现本身比 C++ 标准化委员会预期的要复杂得多。它花了五年多的时间才发布了第一个实现（2002 年 5 月），此后几年没有出现其他实现。为了更好地使 C++ 标准与现有实践保持一致，C++ 标准化委员会从 C++11 中删除了导出的模板。鼓励有兴趣了解更多分离模型细节（和陷阱）的读者阅读本书第一版的第 6.3 节和第 10.3 节（[VandevooordeJosuttisTemplates1st]）。

It is sometimes tempting to imagine ways of extending the concept of precompiled headers so that more than one header could be loaded for a single compilation. This would in principle allow for a finer grained approach to precompilation. The obstacle here is mainly the preprocessor: Macros in one header file can entirely change the meaning of subsequent header files. However, once a file has been precompiled, macro processing is completed, and it is hardly practical to attempt to patch a precompiled header for the preprocessor effects induced by other headers. A new language feature known as _modules_ (see Section [[17.11]] on page [[366]]) is expected to be added to C++ in the not too distant future to address this issue (macro definitions cannot leak into module interfaces).

> 有时很容易想象如何扩展预编译头的概念，以便在一次编译中可以加载多个头。原则上，这将允许使用更细粒度的预编译方法。这里的障碍主要是预处理器：一个头文件中的宏可以完全改变后续头文件的含义。然而，一旦文件被预编译，宏处理就完成了，并且尝试修补预编译的头以获得其他头引起的预处理器效果是很难实现的。一个新的语言功能_modules_（参见第[[366]]页的第[[17.11]]节）预计将在不久的将来添加到 C++ 中，以解决这个问题（宏定义不能泄漏到模块接口中）。

### 9.6 Summary

```
- The inclusion model of templates is the most widely used model for organizing template code. Alternatives are discussed in [Chapter [14]].
- Only full specializations of function templates need `inline` when defined in header files outside classes or structures.
- To take advantage of precompiled headers, be sure to keep the same order for `#include` directives.
- Debugging code with templates can be challenging.

^[1]^ With some implementations this string is *mangled* (encoded with types of arguments and names of surrounding scopes to distinguish it from other names), but a *demangler* is available to turn it into human-readable text.
^[2]^ In theory, the standard headers do not actually need to correspond to physical files. In practice, however, they do, and the files are very large.
```
