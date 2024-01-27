## Contents

[**Preface**](#preface.xhtml#preface)

[**Acknowledgments for the Second Edition**](#ack.xhtml#ack)

[**Acknowledgments for the First Edition**](#ack1.xhtml#ack1)

[**About This Book**](#about.xhtml#about)

[What You Should Know Before Reading This Book](#about.xhtml#alev1)

[Overall Structure of the Book](#about.xhtml#alev2)

[How to Read This Book](#about.xhtml#alev3)

[Some Remarks About Programming Style](#about.xhtml#alev4)

[The C++11, C++14, and C++17 Standards](#about.xhtml#alev5)

[Example Code and Additional Information](#about.xhtml#alev6)

[Feedback](#about.xhtml#alev7)

[**Part I: The Basics**](#part1.xhtml#part1)

[**1 Function Templates**](#ch1.xhtml#ch1)

[1.1    A First Look at Function Templates](#ch1.xhtml#ch1_lev1)

[1.1.1 Defining the Template](#ch1.xhtml#ch1lev1sec1)

[1.1.2 Using the Template](#ch1.xhtml#ch1lev1sec2)

[1.1.3 Two-Phase Translation](#ch1.xhtml#ch1lev1sec3)

[1.2    Template Argument Deduction](#ch1.xhtml#ch1_lev2)

[1.3    Multiple Template Parameters](#ch1.xhtml#ch1_lev3)

[1.3.1 Template Parameters for Return Types](#ch1.xhtml#ch1lev3sec1)

[1.3.2 Deducing the Return Type](#ch1.xhtml#ch1lev3sec2)

[1.3.3 Return Type as Common Type](#ch1.xhtml#ch1lev3sec3)

[1.4    Default Template Arguments](#ch1.xhtml#ch1_lev4)

[1.5    Overloading Function Templates](#ch1.xhtml#ch1_lev5)

[1.6    But, Shouldn't We ...?](#ch1.xhtml#ch1_lev6)

[1.6.1 Pass by Value or by Reference?](#ch1.xhtml#ch1lev6sec1)

[1.6.2 Why Not `inline`?](#ch1.xhtml#ch1lev6sec2)

[1.6.3 Why Not `constexpr`?](#ch1.xhtml#ch1lev6sec3)

[1.7    Summary](#ch1.xhtml#ch1_lev7)

[**2 Class Templates**](#ch2.xhtml#ch2)

[2.1    Implementation of Class Template `Stack`](#ch2.xhtml#ch2_lev1)

[2.1.1 Declaration of Class Templates](#ch2.xhtml#ch2lev1sec1)

[2.1.2 Implementation of Member Functions](#ch2.xhtml#ch2lev1sec2)

[2.2    Use of Class Template `Stack`](#ch2.xhtml#ch2_lev2)

[2.3    Partial Usage of Class Templates](#ch2.xhtml#ch2_lev3)

[2.3.1 Concepts](#ch2.xhtml#ch2lev3sec1)

[2.4    Friends](#ch2.xhtml#ch2_lev4)

[2.5    Specializations of Class Templates](#ch2.xhtml#ch2_lev5)

[2.6    Partial Specialization](#ch2.xhtml#ch2_lev6)

[2.7    Default Class Template Arguments](#ch2.xhtml#ch2_lev7)

[2.8    Type Aliases](#ch2.xhtml#ch2_lev8)

[2.9    Class Template Argument Deduction](#ch2.xhtml#ch2_lev9)

[2.10   Templatized Aggregates](#ch2.xhtml#ch2_lev10)

[2.11   Summary](#ch2.xhtml#ch2_lev11)

[**3 Nontype Template Parameters**](#ch3.xhtml#ch3)

[3.1    Nontype Class Template Parameters](#ch3.xhtml#ch3_lev1)

[3.2    Nontype Function Template Parameters](#ch3.xhtml#ch3_lev2)

[3.3    Restrictions for Nontype Template Parameters](#ch3.xhtml#ch3_lev3)

[3.4    Template Parameter Type `auto`](#ch3.xhtml#ch3_lev4)

[3.5    Summary](#ch3.xhtml#ch3_lev5)

[**4 Variadic Templates**](#ch4.xhtml#ch4)

[4.1    Variadic Templates](#ch4.xhtml#ch4_lev1)

[4.1.1 Variadic Templates by Example](#ch4.xhtml#ch4lev1sec1)

[4.1.2 Overloading Variadic and Nonvariadic Templates](#ch4.xhtml#ch4lev1sec2)

[4.1.3 Operator `sizeof…`](#ch4.xhtml#ch4lev1sec3)

[4.2    Fold Expressions](#ch4.xhtml#ch4_lev2)

[4.3    Application of Variadic Templates](#ch4.xhtml#ch4_lev3)

[4.4    Variadic Class Templates and Variadic Expressions](#ch4.xhtml#ch4_lev4)

[4.4.1 Variadic Expressions](#ch4.xhtml#ch4lev4sec1)

[4.4.2 Variadic Indices](#ch4.xhtml#ch4lev4sec2)

[4.4.3 Variadic Class Templates](#ch4.xhtml#ch4lev4sec3)

[4.4.4 Variadic Deduction Guides](#ch4.xhtml#ch4lev4sec4)

[4.4.5 Variadic Base Classes and `using`](#ch4.xhtml#ch4lev4sec5)

[4.5    Summary](#ch4.xhtml#ch4_lev5)

[**5 Tricky Basics**](#ch5.xhtml#ch5)

[5.1    Keyword `typename`](#ch5.xhtml#ch5_lev1)

[5.2    Zero Initialization](#ch5.xhtml#ch5_lev2)

[5.3    Using `this->`](#ch5.xhtml#ch5_lev3)

[5.4    Templates for Raw Arrays and String Literals](#ch5.xhtml#ch5_lev4)

[5.5    Member Templates](#ch5.xhtml#ch5_lev5)

[5.5.1 The `.template` Construct](#ch5.xhtml#ch5lev5sec1)

[5.5.2 Generic Lambdas and Member Templates](#ch5.xhtml#ch5lev5sec2)

[5.6    Variable Templates](#ch5.xhtml#ch5_lev6)

[5.7    Template Template Parameters](#ch5.xhtml#ch5_lev7)

[5.8    Summary](#ch5.xhtml#ch5_lev8)

[**6 Move Semantics and **enable_if\<\>\*\*\*\*](#ch6.xhtml#ch6)

[6.1    Perfect Forwarding](#ch6.xhtml#ch6_lev1)

[6.2    Special Member Function Templates](#ch6.xhtml#ch6_lev2)

[6.3    Disable Templates with `enable_if<>`](#ch6.xhtml#ch6_lev3)

[6.4    Using `enable_if<>`](#ch6.xhtml#ch6_lev4)

[6.5    Using Concepts to Simplify `enable_if<>` Expressions](#ch6.xhtml#ch6_lev5)

[6.6    Summary](#ch6.xhtml#ch6_lev6)

[**7 By Value or by Reference?**](#ch7.xhtml#ch7)

[7.1    Passing by Value](#ch7.xhtml#ch7_lev1)

[7.2    Passing by Reference](#ch7.xhtml#ch7_lev2)

[7.2.1 Passing by Constant Reference](#ch7.xhtml#ch7lev2sec1)

[7.2.2 Passing by Nonconstant Reference](#ch7.xhtml#ch7lev2sec2)

[7.2.3 Passing by Forwarding Reference](#ch7.xhtml#ch7lev2sec3)

[7.3    Using `std::ref()` and `std::cref()`](#ch7.xhtml#ch7_lev3)

[7.4    Dealing with String Literals and Raw Arrays](#ch7.xhtml#ch7_lev4)

[7.4.1 Special Implementations for String Literals and Raw Arrays](#ch7.xhtml#ch7lev4sec1)

[7.5    Dealing with Return Values](#ch7.xhtml#ch7_lev5)

[7.6    Recommended Template Parameter Declarations](#ch7.xhtml#ch7_lev6)

[7.7    Summary](#ch7.xhtml#ch7_lev7)

[**8 Compile-Time Programming**](#ch8.xhtml#ch8)

[8.1    Template Metaprogramming](#ch8.xhtml#ch8_lev1)

[8.2    Computing with `constexpr`](#ch8.xhtml#ch8_lev2)

[8.3    Execution Path Selection with Partial Specialization](#ch8.xhtml#ch8_lev3)

[8.4    SFINAE (Substitution Failure Is Not An Error)](#ch8.xhtml#ch8_lev4)

[8.4.1 Expression SFINAE with `decltype`](#ch8.xhtml#ch8lev4sec1)

[8.5    Compile-Time `if`](#ch8.xhtml#ch8_lev5)

[8.6    Summary](#ch8.xhtml#ch8_lev6)

[**9 Using Templates in Practice**](#ch9.xhtml#ch9)

[9.1    The Inclusion Model](#ch9.xhtml#ch9_lev1)

[9.1.1 Linker Errors](#ch9.xhtml#ch9lev1sec1)

[9.1.2 Templates in Header Files](#ch9.xhtml#ch9lev1sec2)

[9.2    Templates and `inline`](#ch9.xhtml#ch9_lev2)

[9.3    Precompiled Headers](#ch9.xhtml#ch9_lev3)

[9.4    Decoding the Error Novel](#ch9.xhtml#ch9_lev4)

[9.5    Afternotes](#ch9.xhtml#ch9_lev5)

[9.6    Summary](#ch9.xhtml#ch9_lev6)

[**10 Basic Template Terminology**](#ch10.xhtml#ch10)

[10.1  "Class Template" or "Template Class"?](#ch10.xhtml#ch10_lev1)

[10.2  Substitution, Instantiation, and Specialization](#ch10.xhtml#ch10_lev2)

[10.3  Declarations versus Definitions](#ch10.xhtml#ch10_lev3)

[10.3.1 Complete versus Incomplete Types](#ch10.xhtml#ch10lev3sec1)

[10.4  The One-Definition Rule](#ch10.xhtml#ch10_lev4)

[10.5  Template Arguments versus Template Parameters](#ch10.xhtml#ch10_lev5)

[10.6  Summary](#ch10.xhtml#ch10_lev6)

[**11 Generic Libraries**](#ch11.xhtml#ch11)

[11.1  Callables](#ch11.xhtml#ch11_lev1)

[11.1.1 Supporting Function Objects](#ch11.xhtml#ch11lev1sec1)

[11.1.2 Dealing with Member Functions and Additional Arguments](#ch11.xhtml#ch11lev1sec2)

[11.1.3 Wrapping Function Calls](#ch11.xhtml#ch11lev1sec3)

[11.2  Other Utilities to Implement Generic Libraries](#ch11.xhtml#ch11_lev2)

[11.2.1 Type Traits](#ch11.xhtml#ch11lev2sec1)

[11.2.2 `std::addressof()`](#ch11.xhtml#ch11lev2sec2)

[11.2.3 `std::declval()`](#ch11.xhtml#ch11lev2sec3)

[11.3  Perfect Forwarding Temporaries](#ch11.xhtml#ch11_lev3)

[11.4  References as Template Parameters](#ch11.xhtml#ch11_lev4)

[11.5  Defer Evaluations](#ch11.xhtml#ch11_lev5)

[11.6  Things to Consider When Writing Generic Libraries](#ch11.xhtml#ch11_lev6)

[11.7  Summary](#ch11.xhtml#ch11_lev7)

[**Part II: Templates in Depth**](#part2.xhtml#part2)

[**12 Fundamentals in Depth**](#ch12.xhtml#ch12)

[12.1  Parameterized Declarations](#ch12.xhtml#ch12_lev1)

[12.1.1 Virtual Member Functions](#ch12.xhtml#ch12lev1sec1)

[12.1.2 Linkage of Templates](#ch12.xhtml#ch12lev1sec2)

[12.1.3 Primary Templates](#ch12.xhtml#ch12lev1sec3)

[12.2  Template Parameters](#ch12.xhtml#ch12_lev2)

[12.2.1 Type Parameters](#ch12.xhtml#ch12lev2sec1)

[12.2.2 Nontype Parameters](#ch12.xhtml#ch12lev2sec2)

[12.2.3 Template Template Parameters](#ch12.xhtml#ch12lev2sec3)

[12.2.4 Template Parameter Packs](#ch12.xhtml#ch12lev2sec4)

[12.2.5 Default Template Arguments](#ch12.xhtml#ch12lev2sec5)

[12.3  Template Arguments](#ch12.xhtml#ch12_lev3)

[12.3.1 Function Template Arguments](#ch12.xhtml#ch12lev3sec1)

[12.3.2 Type Arguments](#ch12.xhtml#ch12lev3sec2)

[12.3.3 Nontype Arguments](#ch12.xhtml#ch12lev3sec3)

[12.3.4 Template Template Arguments](#ch12.xhtml#ch12lev3sec4)

[12.3.5 Equivalence](#ch12.xhtml#ch12lev3sec5)

[12.4  Variadic Templates](#ch12.xhtml#ch12_lev4)

[12.4.1 Pack Expansions](#ch12.xhtml#ch12lev4sec1)

[12.4.2 Where Can Pack Expansions Occur?](#ch12.xhtml#ch12lev4sec2)

[12.4.3 Function Parameter Packs](#ch12.xhtml#ch12lev4sec3)

[12.4.4 Multiple and Nested Pack Expansions](#ch12.xhtml#ch12lev4sec4)

[12.4.5 Zero-Length Pack Expansions](#ch12.xhtml#ch12lev4sec5)

[12.4.6 Fold Expressions](#ch12.xhtml#ch12lev4sec6)

[12.5  Friends](#ch12.xhtml#ch12_lev5)

[12.5.1 Friend Classes of Class Templates](#ch12.xhtml#ch12lev5sec1)

[12.5.2 Friend Functions of Class Templates](#ch12.xhtml#ch12lev5sec2)

[12.5.3 Friend Templates](#ch12.xhtml#ch12lev5sec3)

[12.6  Afternotes](#ch12.xhtml#ch12_lev6)

[**13 Names in Templates**](#ch13.xhtml#ch13)

[13.1  Name Taxonomy](#ch13.xhtml#ch13_lev1)

[13.2  Looking Up Names](#ch13.xhtml#ch13_lev2)

[13.2.1 Argument-Dependent Lookup](#ch13.xhtml#ch13lev2sec1)

[13.2.2 Argument-Dependent Lookup of Friend Declarations](#ch13.xhtml#ch13lev2sec2)

[13.2.3 Injected Class Names](#ch13.xhtml#ch13lev2sec3)

[13.2.4 Current Instantiations](#ch13.xhtml#ch13lev2sec4)

[13.3  Parsing Templates](#ch13.xhtml#ch13_lev3)

[13.3.1 Context Sensitivity in Nontemplates](#ch13.xhtml#ch13lev3sec1)

[13.3.2 Dependent Names of Types](#ch13.xhtml#ch13lev3sec2)

[13.3.3 Dependent Names of Templates](#ch13.xhtml#ch13lev3sec3)

[13.3.4 Dependent Names in Using Declarations](#ch13.xhtml#ch13lev3sec4)

[13.3.5 ADL and Explicit Template Arguments](#ch13.xhtml#ch13lev3sec5)

[13.3.6 Dependent Expressions](#ch13.xhtml#ch13lev3sec6)

[13.3.7 Compiler Errors](#ch13.xhtml#ch13lev3sec7)

[13.4  Inheritance and Class Templates](#ch13.xhtml#ch13_lev4)

[13.4.1 Nondependent Base Classes](#ch13.xhtml#ch13lev4sec1)

[13.4.2 Dependent Base Classes](#ch13.xhtml#ch13lev4sec2)

[13.5  Afternotes](#ch13.xhtml#ch13_lev5)

[**14 Instantiation**](#ch14.xhtml#ch14)

[14.1  On-Demand Instantiation](#ch14.xhtml#ch14_lev1)

[14.2  Lazy Instantiation](#ch14.xhtml#ch14_lev2)

[14.2.1 Partial and Full Instantiation](#ch14.xhtml#ch14lev2sec1)

[14.2.2 Instantiated Components](#ch14.xhtml#ch14lev2sec2)

[14.3  The C++ Instantiation Model](#ch14.xhtml#ch14_lev3)

[14.3.1 Two-Phase Lookup](#ch14.xhtml#ch14lev3sec1)

[14.3.2 Points of Instantiation](#ch14.xhtml#ch14lev3sec2)

[14.3.3 The Inclusion Model](#ch14.xhtml#ch14lev3sec3)

[14.4  Implementation Schemes](#ch14.xhtml#ch14_lev4)

[14.4.1 Greedy Instantiation](#ch14.xhtml#ch14lev4sec1)

[14.4.2 Queried Instantiation](#ch14.xhtml#ch14lev4sec2)

[14.4.3 Iterated Instantiation](#ch14.xhtml#ch14lev4sec3)

[14.5  Explicit Instantiation](#ch14.xhtml#ch14_lev5)

[14.5.1 Manual Instantiation](#ch14.xhtml#ch14lev5sec1)

[14.5.2 Explicit Instantiation Declarations](#ch14.xhtml#ch14lev5sec2)

[14.6  Compile-Time `if` Statements](#ch14.xhtml#ch14_lev6)

[14.7  In the Standard Library](#ch14.xhtml#ch14_lev7)

[14.8  Afternotes](#ch14.xhtml#ch14_lev8)

[**15 Template Argument Deduction**](#ch15.xhtml#ch15)

[15.1  The Deduction Process](#ch15.xhtml#ch15_lev1)

[15.2  Deduced Contexts](#ch15.xhtml#ch15_lev2)

[15.3  Special Deduction Situations](#ch15.xhtml#ch15_lev3)

[15.4  Initializer Lists](#ch15.xhtml#ch15_lev4)

[15.5  Parameter Packs](#ch15.xhtml#ch15_lev5)

[15.5.1 Literal Operator Templates](#ch15.xhtml#ch15lev5sec1)

[15.6  Rvalue References](#ch15.xhtml#ch15_lev6)

[15.6.1 Reference Collapsing Rules](#ch15.xhtml#ch15lev6sec1)

[15.6.2 Forwarding References](#ch15.xhtml#ch15lev6sec2)

[15.6.3 Perfect Forwarding](#ch15.xhtml#ch15lev6sec3)

[15.6.4 Deduction Surprises](#ch15.xhtml#ch15lev6sec4)

[15.7  SFINAE (Substitution Failure Is Not An Error)](#ch15.xhtml#ch15_lev7)

[15.7.1 Immediate Context](#ch15.xhtml#ch15lev7sec1)

[15.8  Limitations of Deduction](#ch15.xhtml#ch15_lev8)

[15.8.1 Allowable Argument Conversions](#ch15.xhtml#ch15lev8sec1)

[15.8.2 Class Template Arguments](#ch15.xhtml#ch15lev8sec2)

[15.8.3 Default Call Arguments](#ch15.xhtml#ch15lev8sec3)

[15.8.4 Exception Specifications](#ch15.xhtml#ch15lev8sec4)

[15.9  Explicit Function Template Arguments](#ch15.xhtml#ch15_lev9)

[15.10  Deduction from Initializers and Expressions](#ch15.xhtml#ch15_lev10)

[15.10.1 The `auto` Type Specifier](#ch15.xhtml#ch15lev10sec1)

[15.10.2 Expressing the Type of an Expression with `decltype`](#ch15.xhtml#ch15lev10sec2)

[15.10.3 `decltype(auto)`](#ch15.xhtml#ch15lev10sec3)

[15.10.4 Special Situations for `auto` Deduction](#ch15.xhtml#ch15lev10sec4)

[15.10.5 Structured Bindings](#ch15.xhtml#ch15lev10sec5)

[15.10.6 Generic Lambdas](#ch15.xhtml#ch15lev10sec6)

[15.11  Alias Templates](#ch15.xhtml#ch15_lev11)

[15.12  Class Template Argument Deduction](#ch15.xhtml#ch15_lev12)

[15.12.1 Deduction Guides](#ch15.xhtml#ch15lev12sec1)

[15.12.2 Implicit Deduction Guides](#ch15.xhtml#ch15lev12sec2)

[15.12.3 Other Subtleties](#ch15.xhtml#ch15lev12sec3)

[15.13  Afternotes](#ch15.xhtml#ch15_lev13)

[**16 Specialization and Overloading**](#ch16.xhtml#ch16)

[16.1  When "Generic Code" Doesn't Quite Cut It](#ch16.xhtml#ch16_lev1)

[16.1.1 Transparent Customization](#ch16.xhtml#ch16lev1sec1)

[16.1.2 Semantic Transparency](#ch16.xhtml#ch16lev1sec2)

[16.2  Overloading Function Templates](#ch16.xhtml#ch16_lev2)

[16.2.1 Signatures](#ch16.xhtml#ch16lev2sec1)

[16.2.2 Partial Ordering of Overloaded Function Templates](#ch16.xhtml#ch16lev2sec2)

[16.2.3 Formal Ordering Rules](#ch16.xhtml#ch16lev2sec3)

[16.2.4 Templates and Nontemplates](#ch16.xhtml#ch16lev2sec4)

[16.2.5 Variadic Function Templates](#ch16.xhtml#ch16lev2sec5)

[16.3  Explicit Specialization](#ch16.xhtml#ch16_lev3)

[16.3.1 Full Class Template Specialization](#ch16.xhtml#ch16lev3sec1)

[16.3.2 Full Function Template Specialization](#ch16.xhtml#ch16lev3sec2)

[16.3.3 Full Variable Template Specialization](#ch16.xhtml#ch16lev3sec3)

[16.3.4 Full Member Specialization](#ch16.xhtml#ch16lev3sec4)

[16.4  Partial Class Template Specialization](#ch16.xhtml#ch16_lev4)

[16.5  Partial Variable Template Specialization](#ch16.xhtml#ch16_lev5)

[16.6  Afternotes](#ch16.xhtml#ch16_lev6)

[**17 Future Directions**](#ch17.xhtml#ch17)

[17.1  Relaxed `typename` Rules](#ch17.xhtml#ch17_lev1)

[17.2  Generalized Nontype Template Parameters](#ch17.xhtml#ch17_lev2)

[17.3  Partial Specialization of Function Templates](#ch17.xhtml#ch17_lev3)

[17.4  Named Template Arguments](#ch17.xhtml#ch17_lev4)

[17.5  Overloaded Class Templates](#ch17.xhtml#ch17_lev5)

[17.6  Deduction for Nonfinal Pack Expansions](#ch17.xhtml#ch17_lev6)

[17.7  Regularization of `void`](#ch17.xhtml#ch17_lev7)

[17.8  Type Checking for Templates](#ch17.xhtml#ch17_lev8)

[17.9  Reflective Metaprogramming](#ch17.xhtml#ch17_lev9)

[17.10  Pack Facilities](#ch17.xhtml#ch17_lev10)

[17.11  Modules](#ch17.xhtml#ch17_lev11)

[**Part III: Templates and Design**](#part3.xhtml#part3)

[**18 The Polymorphic Power of Templates**](#ch18.xhtml#ch18)

[18.1  Dynamic Polymorphism](#ch18.xhtml#ch18_lev1)

[18.2  Static Polymorphism](#ch18.xhtml#ch18_lev2)

[18.3  Dynamic versus Static Polymorphism](#ch18.xhtml#ch18_lev3)

[18.4  Using Concepts](#ch18.xhtml#ch18_lev4)

[18.5  New Forms of Design Patterns](#ch18.xhtml#ch18_lev5)

[18.6  Generic Programming](#ch18.xhtml#ch18_lev6)

[18.7  Afternotes](#ch18.xhtml#ch18_lev7)

[**19 Implementing Traits**](#ch19.xhtml#ch19)

[19.1  An Example: Accumulating a Sequence](#ch19.xhtml#ch19_lev1)

[19.1.1 Fixed Traits](#ch19.xhtml#ch19lev1sec1)

[19.1.2 Value Traits](#ch19.xhtml#ch19lev1sec2)

[19.1.3 Parameterized Traits](#ch19.xhtml#ch19lev1sec3)

[19.2  Traits versus Policies and Policy Classes](#ch19.xhtml#ch19_lev2)

[19.2.1 Traits and Policies: What's the Difference?](#ch19.xhtml#ch19lev2sec1)

[19.2.2 Member Templates versus Template Template Parameters](#ch19.xhtml#ch19lev2sec2)

[19.2.3 Combining Multiple Policies and/or Traits](#ch19.xhtml#ch19lev2sec3)

[19.2.4 Accumulation with General Iterators](#ch19.xhtml#ch19lev2sec4)

[19.3  Type Functions](#ch19.xhtml#ch19_lev3)

[19.3.1 Element Types](#ch19.xhtml#ch19lev3sec1)

[19.3.2 Transformation Traits](#ch19.xhtml#ch19lev3sec2)

[19.3.3 Predicate Traits](#ch19.xhtml#ch19lev3sec3)

[19.3.4 Result Type Traits](#ch19.xhtml#ch19lev3sec4)

[19.4  SFINAE-Based Traits](#ch19.xhtml#ch19_lev4)

[19.4.1 SFINAE Out Function Overloads](#ch19.xhtml#ch19lev4sec1)

[19.4.2 SFINAE Out Partial Specializations](#ch19.xhtml#ch19lev4sec2)

[19.4.3 Using Generic Lambdas for SFINAE](#ch19.xhtml#ch19lev4sec3)

[19.4.4 SFINAE-Friendly Traits](#ch19.xhtml#ch19lev4sec4)

[19.5  IsConvertibleT](#ch19.xhtml#ch19_lev5)

[19.6  Detecting Members](#ch19.xhtml#ch19_lev6)

[19.6.1 Detecting Member Types](#ch19.xhtml#ch19lev6sec1)

[19.6.2 Detecting Arbitrary Member Types](#ch19.xhtml#ch19lev6sec2)

[19.6.3 Detecting Nontype Members](#ch19.xhtml#ch19lev6sec3)

[19.6.4 Using Generic Lambdas to Detect Members](#ch19.xhtml#ch19lev6sec4)

[19.7  Other Traits Techniques](#ch19.xhtml#ch19_lev7)

[19.7.1 If-Then-Else](#ch19.xhtml#ch19lev7sec1)

[19.7.2 Detecting Nonthrowing Operations](#ch19.xhtml#ch19lev7sec2)

[19.7.3 Traits Convenience](#ch19.xhtml#ch19lev7sec3)

[19.8  Type Classification](#ch19.xhtml#ch19_lev8)

[19.8.1 Determining Fundamental Types](#ch19.xhtml#ch19lev8sec1)

[19.8.2 Determining Compound Types](#ch19.xhtml#ch19lev8sec2)

[19.8.3 Identifying Function Types](#ch19.xhtml#ch19lev8sec3)

[19.8.4 Determining Class Types](#ch19.xhtml#ch19lev8sec4)

[19.8.5 Determining Enumeration Types](#ch19.xhtml#ch19lev8sec5)

[19.9  Policy Traits](#ch19.xhtml#ch19_lev9)

[19.9.1 Read-Only Parameter Types](#ch19.xhtml#ch19lev9sec1)

[19.10  In the Standard Library](#ch19.xhtml#ch19_lev10)

[19.11  Afternotes](#ch19.xhtml#ch19_lev11)

[**20 Overloading on Type Properties**](#ch20.xhtml#ch20)

[20.1  Algorithm Specialization](#ch20.xhtml#ch20_lev1)

[20.2  Tag Dispatching](#ch20.xhtml#ch20_lev2)

[20.3  Enabling/Disabling Function Templates](#ch20.xhtml#ch20_lev3)

[20.3.1 Providing Multiple Specializations](#ch20.xhtml#ch20lev3sec1)

[20.3.2 Where Does the `EnableIf` Go?](#ch20.xhtml#ch20lev3sec2)

[20.3.3 Compile-Time `if`](#ch20.xhtml#ch20lev3sec3)

[20.3.4 Concepts](#ch20.xhtml#ch20lev3sec4)

[20.4  Class Specialization](#ch20.xhtml#ch20_lev4)

[20.4.1 Enabling/Disabling Class Templates](#ch20.xhtml#ch20lev4sec1)

[20.4.2 Tag Dispatching for Class Templates](#ch20.xhtml#ch20lev4sec2)

[20.5  Instantiation-Safe Templates](#ch20.xhtml#ch20_lev5)

[20.6  In the Standard Library](#ch20.xhtml#ch20_lev6)

[20.7  Afternotes](#ch20.xhtml#ch20_lev7)

[**21 Templates and Inheritance**](#ch21.xhtml#ch21)

[21.1  The Empty Base Class Optimization (EBCO)](#ch21.xhtml#ch21_lev1)

[21.1.1 Layout Principles](#ch21.xhtml#ch21lev1sec1)

[21.1.2 Members as Base Classes](#ch21.xhtml#ch21lev1sec2)

[21.2  The Curiously Recurring Template Pattern (CRTP)](#ch21.xhtml#ch21_lev2)

[21.2.1 The Barton-Nackman Trick](#ch21.xhtml#ch21lev2sec1)

[21.2.2 Operator Implementations](#ch21.xhtml#ch21lev2sec2)

[21.2.3 Facades](#ch21.xhtml#ch21lev2sec3)

[21.3  Mixins](#ch21.xhtml#ch21_lev3)

[21.3.1 Curious Mixins](#ch21.xhtml#ch21lev3sec1)

[21.3.2 Parameterized Virtuality](#ch21.xhtml#ch21lev3sec2)

[21.4  Named Template Arguments](#ch21.xhtml#ch21_lev4)

[21.5  Afternotes](#ch21.xhtml#ch21_lev5)

[**22 Bridging Static and Dynamic Polymorphism**](#ch22.xhtml#ch22)

[22.1  Function Objects, Pointers, and `std::function<>`](#ch22.xhtml#ch22_lev1)

[22.2  Generalized Function Pointers](#ch22.xhtml#ch22_lev2)

[22.3  Bridge Interface](#ch22.xhtml#ch22_lev3)

[22.4  Type Erasure](#ch22.xhtml#ch22_lev4)

[22.5  Optional Bridging](#ch22.xhtml#ch22_lev5)

[22.6  Performance Considerations](#ch22.xhtml#ch22_lev6)

[22.7  Afternotes](#ch22.xhtml#ch22_lev7)

[**23 Metaprogramming**](#ch23.xhtml#ch23)

[23.1  The State of Modern C++ Metaprogramming](#ch23.xhtml#ch23_lev1)

[23.1.1 Value Metaprogramming](#ch23.xhtml#ch23lev1sec1)

[23.1.2 Type Metaprogramming](#ch23.xhtml#ch23lev1sec2)

[23.1.3 Hybrid Metaprogramming](#ch23.xhtml#ch23lev1sec3)

[23.1.4 Hybrid Metaprogramming for Unit Types](#ch23.xhtml#ch23lev1sec4)

[23.2  The Dimensions of Reflective Metaprogramming](#ch23.xhtml#ch23_lev2)

[23.3  The Cost of Recursive Instantiation](#ch23.xhtml#ch23_lev3)

[23.3.1 Tracking All Instantiations](#ch23.xhtml#ch23lev3sec1)

[23.4  Computational Completeness](#ch23.xhtml#ch23_lev4)

[23.5  Recursive Instantiation versus Recursive Template Arguments](#ch23.xhtml#ch23_lev5)

[23.6  Enumeration Values versus Static Constants](#ch23.xhtml#ch23_lev6)

[23.7  Afternotes](#ch23.xhtml#ch23_lev7)

[**24 Typelists**](#ch24.xhtml#ch24)

[24.1  Anatomy of a Typelist](#ch24.xhtml#ch24_lev1)

[24.2  Typelist Algorithms](#ch24.xhtml#ch24_lev2)

[24.2.1 Indexing](#ch24.xhtml#ch24lev2sec1)

[24.2.2 Finding the Best Match](#ch24.xhtml#ch24lev2sec2)

[24.2.3 Appending to a Typelist](#ch24.xhtml#ch24lev2sec3)

[24.2.4 Reversing a Typelist](#ch24.xhtml#ch24lev2sec4)

[24.2.5 Transforming a Typelist](#ch24.xhtml#ch24lev2sec5)

[24.2.6 Accumulating Typelists](#ch24.xhtml#ch24lev2sec6)

[24.2.7 Insertion Sort](#ch24.xhtml#ch24lev2sec7)

[24.3  Nontype Typelists](#ch24.xhtml#ch24_lev3)

[24.3.1 Deducible Nontype Parameters](#ch24.xhtml#ch24lev3sec1)

[24.4  Optimizing Algorithms with Pack Expansions](#ch24.xhtml#ch24_lev4)

[24.5  Cons-style Typelists](#ch24.xhtml#ch24_lev5)

[24.6  Afternotes](#ch24.xhtml#ch24_lev6)

[**25 Tuples**](#ch25.xhtml#ch25)

[25.1  Basic Tuple Design](#ch25.xhtml#ch25_lev1)

[25.1.1 Storage](#ch25.xhtml#ch25lev1sec1)

[25.1.2 Construction](#ch25.xhtml#ch25lev1sec2)

[25.2  Basic Tuple Operations](#ch25.xhtml#ch25_lev2)

[25.2.1 Comparison](#ch25.xhtml#ch25lev2sec1)

[25.2.2 Output](#ch25.xhtml#ch25lev2sec2)

[25.3  Tuple Algorithms](#ch25.xhtml#ch25_lev3)

[25.3.1 Tuples as Typelists](#ch25.xhtml#ch25lev3sec1)

[25.3.2 Adding to and Removing from a Tuple](#ch25.xhtml#ch25lev3sec2)

[25.3.3 Reversing a Tuple](#ch25.xhtml#ch25lev3sec3)

[25.3.4 Index Lists](#ch25.xhtml#ch25lev3sec4)

[25.3.5 Reversal with Index Lists](#ch25.xhtml#ch25lev3sec5)

[25.3.6 Shuffle and Select](#ch25.xhtml#ch25lev3sec6)

[25.4  Expanding Tuples](#ch25.xhtml#ch25_lev4)

[25.5  Optimizing Tuple](#ch25.xhtml#ch25_lev5)

[25.5.1 Tuples and the EBCO](#ch25.xhtml#ch25lev5sec1)

[25.5.2 Constant-time `get()`](#ch25.xhtml#ch25lev5sec2)

[25.6  Tuple Subscript](#ch25.xhtml#ch25_lev6)

[25.7  Afternotes](#ch25.xhtml#ch25_lev7)

[**26 Discriminated Unions**](#ch26.xhtml#ch26)

[26.1  Storage](#ch26.xhtml#ch26_lev1)

[26.2  Design](#ch26.xhtml#ch26_lev2)

[26.3  Value Query and Extraction](#ch26.xhtml#ch26_lev3)

[26.4  Element Initialization, Assignment and Destruction](#ch26.xhtml#ch26_lev4)

[26.4.1 Initialization](#ch26.xhtml#ch26lev4sec1)

[26.4.2 Destruction](#ch26.xhtml#ch26lev4sec2)

[26.4.3 Assignment](#ch26.xhtml#ch26lev4sec3)

[26.5  Visitors](#ch26.xhtml#ch26_lev5)

[26.5.1 Visit Result Type](#ch26.xhtml#ch26lev5sec1)

[26.5.2 Common Result Type](#ch26.xhtml#ch26lev5sec2)

[26.6  Variant Initialization and Assignment](#ch26.xhtml#ch26_lev6)

[26.7  Afternotes](#ch26.xhtml#ch26_lev7)

[**27 Expression Templates**](#ch27.xhtml#ch27)

[27.1  Temporaries and Split Loops](#ch27.xhtml#ch27_lev1)

[27.2  Encoding Expressions in Template Arguments](#ch27.xhtml#ch27_lev2)

[27.2.1 Operands of the Expression Templates](#ch27.xhtml#ch27lev2sec1)

[27.2.2 The `Array` Type](#ch27.xhtml#ch27lev2sec2)

[27.2.3 The Operators](#ch27.xhtml#ch27lev2sec3)

[27.2.4 Review](#ch27.xhtml#ch27lev2sec4)

[27.2.5 Expression Templates Assignments](#ch27.xhtml#ch27lev2sec5)

[27.3  Performance and Limitations of Expression Templates](#ch27.xhtml#ch27_lev3)

[27.4  Afternotes](#ch27.xhtml#ch27_lev4)

[**28 Debugging Templates**](#ch28.xhtml#ch28)

[28.1  Shallow Instantiation](#ch28.xhtml#ch28_lev1)

[28.2  Static Assertions](#ch28.xhtml#ch28_lev2)

[28.3  Archetypes](#ch28.xhtml#ch28_lev3)

[28.4  Tracers](#ch28.xhtml#ch28_lev4)

[28.5  Oracles](#ch28.xhtml#ch28_lev5)

[28.6  Afternotes](#ch28.xhtml#ch28_lev6)

[**Appendixes**](#appa.xhtml#appa)

[**A The One-Definition Rule**](#appa.xhtml#appa)

[A.1 Translation Units](#appa.xhtml#chAapp1)

[A.2 Declarations and Definitions](#appa.xhtml#chAapp2)

[A.3 The One-Definition Rule in Detail](#appa.xhtml#chAapp3)

[A.3.1 One-per-Program Constraints](#appa.xhtml#chAapp3s1)

[A.3.2 One-per-Translation Unit Constraints](#appa.xhtml#chAapp3s2)

[A.3.3 Cross-Translation Unit Equivalence Constraints](#appa.xhtml#chAapp3s3)

[**B Value Categories**](#appb.xhtml#appb)

[B.1 Traditional Lvalues and Rvalues](#appb.xhtml#chBapp1)

[B.1.1 Lvalue-to-Rvalue Conversions](#appb.xhtml#chBapp1s1)

[B.2 Value Categories Since C++11](#appb.xhtml#chBapp2)

[B.2.1 Temporary Materialization](#appb.xhtml#chBapp2s1)

[B.3 Checking Value Categories with `decltype`](#appb.xhtml#chBapp3)

[B.4 Reference Types](#appb.xhtml#chBapp4)

[**C Overload Resolution**](#appc.xhtml#appc)

[C.1 When Does Overload Resolution Kick In?](#appc.xhtml#chCapp1)

[C.2 Simplified Overload Resolution](#appc.xhtml#chCapp2)

[C.2.1 The Implied Argument for Member Functions](#appc.xhtml#chCapp2s1)

[C.2.2 Refining the Perfect Match](#appc.xhtml#chCapp2s2)

[C.3 Overloading Details](#appc.xhtml#chCapp3)

[C.3.1 Prefer Nontemplates or More Specialized Templates](#appc.xhtml#chCapp3s1)

[C.3.2 Conversion Sequences](#appc.xhtml#chCapp3s2)

[C.3.3 Pointer Conversions](#appc.xhtml#chCapp3s3)

[C.3.4 Initializer Lists](#appc.xhtml#chCapp3s4)

[C.3.5 Functors and Surrogate Functions](#appc.xhtml#chCapp3s5)

[C.3.6 Other Overloading Contexts](#appc.xhtml#chCapp3s6)

[**D Standard Type Utilities**](#appd.xhtml#appd)

[D.1 Using Type Traits](#appd.xhtml#chDapp1)

[D.1.1 `std::integral_constant` and `std::bool_constant`](#appd.xhtml#chDapp1s1)

[D.1.2 Things You Should Know When Using Traits](#appd.xhtml#chDapp1s2)

[D.2 Primary and Composite Type Categories](#appd.xhtml#chDapp2)

[D.2.1 Testing for the Primary Type Category](#appd.xhtml#chDapp2s1)

[D.2.2 Test for Composite Type Categories](#appd.xhtml#chDapp2s2)

[D.3 Type Properties and Operations](#appd.xhtml#chDapp3)

[D.3.1 Other Type Properties](#appd.xhtml#chDapp3s1)

[D.3.2 Test for Specific Operations](#appd.xhtml#chDapp3s2)

[D.3.3 Relationships Between Types](#appd.xhtml#chDapp3s3)

[D.4 Type Construction](#appd.xhtml#chDapp4)

[D.5 Other Traits](#appd.xhtml#chDapp5)

[D.6 Combining Type Traits](#appd.xhtml#chDapp6)

[D.7 Other Utilities](#appd.xhtml#chDapp7)

[**E Concepts**](#appe.xhtml#appe)

[E.1 Using Concepts](#appe.xhtml#chEapp1)

[E.2 Defining Concepts](#appe.xhtml#chEapp2)

[E.3 Overloading on Constraints](#appe.xhtml#chEapp3)

[E.3.1 Constraint Subsumption](#appe.xhtml#chEapp3s1)

[E.3.2 Constraints and Tag Dispatching](#appe.xhtml#chEapp3s2)

[E.4 Concept Tips](#appe.xhtml#chEapp4)

[E.4.1 Testing Concepts](#appe.xhtml#chEapp4s1)

[E.4.2 Concept Granularity](#appe.xhtml#chEapp4s2)

[E.4.3 Binary Compatibility](#appe.xhtml#chEapp4s3)

[**Bibliography**](#bib.xhtml#bib)

[Forums](#bib.xhtml#bib1)

[Books and Web Sites](#bib.xhtml#bib2)

[**Glossary**](#glossary.xhtml#glossary)

[**Index**](#index.xhtml#index)
