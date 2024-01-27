---
tip: translate by baidu@2024-01-27 20:47:56
author:
  - Douglas Gregor
  - Nicolai M. Josuttis
  - David Vandevoorde
coverage:
  - Indiana
  - Indianapolis
date: 2018
format: 822 Pages
identifier: 9780134778747
language: en
publisher: Pearson Education
rights: Copyright © 2018 Pearson Education, Inc.
source: "urn:isbn:9780134778747"
title: C++ Templates
type: Text
---

# **C++ Templates**

Many of the designations used by manufacturers and sellers to distinguish their products are claimed as trademarks. Where those designations appear in this book, and the publisher was aware of a trademark claim, the designations have been printed with initial capital letters or in all capitals.

> 制造商和销售商用来区分其产品的许多名称都被称为商标。如果这些名称出现在本书中，并且出版商知道商标声明，则这些名称已用首字母大写或全大写印刷。

The authors and publisher have taken care in the preparation of this book, but make no expressed or implied warranty of any kind and assume no responsibility for errors or omissions. No liability is assumed for incidental or consequential damages in connection with or arising out of the use of the information or programs contained herein.

> 作者和出版商在编写本书时非常谨慎，但不作任何明示或暗示的保证，也不对错误或遗漏承担任何责任。对于与使用此处包含的信息或程序有关或因使用这些信息或程序而产生的附带或间接损害，我们不承担任何责任。

For information about buying this title in bulk quantities, or for special sales opportunities (which may include electronic versions; custom cover designs; and content particular to your business, training goals, marketing focus, or branding interests), please contact our corporate sales department at `corpsales@pearsoned.com` or (800) 382-3419.

> 有关批量购买本标题的信息，或特殊销售机会(可能包括电子版本；定制封面设计；以及特定于您的业务、培训目标、营销重点或品牌兴趣的内容)，请联系我们的公司销售部门，网址为 `corpsales@pearsoned.com` 或(800)382-3419。

For government sales inquiries, please contact `governmentsales@pearsoned.com`.

> 政府销售咨询，请联系 `governmentsales@pearsoned.com`.

For questions about sales outside the U.S., please contact `intlcs@pearson.com`.

> 有关美国境外销售的问题，请联系 `intlcs@pearson.com`.

Visit us on the Web: `informit.com/aw`

Library of Congress Catalog Number: 2017946531

Copyright © 2018 Pearson Education, Inc.

This book was typeset by Nicolai M. Josuttis using the LATEX document processing system. All rights reserved. Printed in the United States of America. This publication is protected by copyright, and permission must be obtained from the publisher prior to any prohibited reproduction, storage in a retrieval system, or transmission in any form or by any means, electronic, mechanical, photocopying, recording, or likewise. For information regarding permissions, request forms and the appropriate contacts within the Pearson Education Global Rights & Permissions Department, please visit `www.pearsoned.com/permissions/`.

> 本书由 Nicolai M.Josuttis 使用 LATEX 文档处理系统进行排版。保留所有权利。在美利坚合众国印制。本出版物受版权保护，在进行任何禁止复制、存储在检索系统中或以任何形式或通过任何方式(电子、机械、复印、录音或类似方式)传输之前，必须获得出版商的许可。有关培生教育全球权利与权限部门的权限、申请表和适当联系人的信息，请访问“[www.pearsoned.com/permissions/](http://www.pearsoned.com/permissions/)”。

## Contents

```md
- *C++ Templates*(#c-templates)
  - [Contents](#contents)
  - [Preface](#preface)
  - [Acknowledgments for the Second Edition](#acknowledgments-for-the-second-edition)
    - [David's Acknowledgments for the Second Edition](#davids-acknowledgments-for-the-second-edition)
    - [Nico's Acknowledgments for the Second Edition](#nicos-acknowledgments-for-the-second-edition)
    - [Doug's Acknowledgments for the Second Edition](#dougs-acknowledgments-for-the-second-edition)
  - [Acknowledgments for the First Edition](#acknowledgments-for-the-first-edition)
    - [Nico's Acknowledgments for the First Edition](#nicos-acknowledgments-for-the-first-edition)
    - [David's Acknowledgments for the First Edition](#davids-acknowledgments-for-the-first-edition)
  - [About This Book](#about-this-book)
    - [What You Should Know Before Reading This Book](#what-you-should-know-before-reading-this-book)
    - [Overall Structure of the Book](#overall-structure-of-the-book)
    - [How to Read This Book](#how-to-read-this-book)
    - [Some Remarks About Programming Style](#some-remarks-about-programming-style)
    - [The C++11, C++14, and C++17 Standards](#the-c11-c14-and-c17-standards)
    - [Example Code and Additional Information](#example-code-and-additional-information)
    - [Feedback](#feedback)
  - [Part I  The Basics](#part-i--the-basics)
    - [Why Templates?](#why-templates)
  - [Chapter 1](#chapter-1)
  - [Function Templates](#function-templates)
    - [1.1 A First Look at Function Templates](#11-a-first-look-at-function-templates)
      - [1.1.1 Defining the Template](#111-defining-the-template)
      - [1.1.2 Using the Template](#112-using-the-template)
      - [1.1.3 Two-Phase Translation](#113-two-phase-translation)
      - [Compiling and Linking](#compiling-and-linking)
    - [1.2 Template Argument Deduction](#12-template-argument-deduction)
        - [Type Conversions During Type Deduction](#type-conversions-during-type-deduction)
        - [Type Deduction for Default Arguments](#type-deduction-for-default-arguments)
    - [1.3 Multiple Template Parameters](#13-multiple-template-parameters)
      - [1.3.1 Template Parameters for Return Types](#131-template-parameters-for-return-types)
      - [1.3.2 Deducing the Return Type](#132-deducing-the-return-type)
      - [1.3.3 Return Type as Common Type](#133-return-type-as-common-type)
    - [1.4 Default Template Arguments](#14-default-template-arguments)
    - [1.5 Overloading Function Templates](#15-overloading-function-templates)
    - [1.6 But, Shouldn't We ...?](#16-but-shouldnt-we-)
      - [1.6.1 Pass by Value or by Reference?](#161-pass-by-value-or-by-reference)
      - [1.6.2 Why Not **inline**?](#162-why-not-inline)
      - [1.6.3 Why Not **constexpr**?](#163-why-not-constexpr)
    - [1.7 Summary](#17-summary)
  - [Chapter 2](#chapter-2)
  - [Class Templates](#class-templates)
    - [2.1 Implementation of Class Template **Stack*(#21-implementation-of-class-template-stack)
      - [2.1.1 Declaration of Class Templates](#211-declaration-of-class-templates)
      - [2.1.2 Implementation of Member Functions](#212-implementation-of-member-functions)
    - [2.2 Use of Class Template **Stack*(#22-use-of-class-template-stack)
    - [2.3 Partial Usage of Class Templates](#23-partial-usage-of-class-templates)
      - [2.3.1 Concepts](#231-concepts)
    - [2.4 Friends](#24-friends)
    - [2.5 Specializations of Class Templates](#25-specializations-of-class-templates)
    - [2.6 Partial Specialization](#26-partial-specialization)
        - [Partial Specialization with Multiple Parameters](#partial-specialization-with-multiple-parameters)
    - [2.7 Default Class Template Arguments](#27-default-class-template-arguments)
    - [2.8 Type Aliases](#28-type-aliases)
        - [Typedefs and Alias Declarations](#typedefs-and-alias-declarations)
        - [Alias Templates](#alias-templates)
        - [Alias Templates for Member Types](#alias-templates-for-member-types)
        - [Type Traits Suffix\_t](#type-traits-suffix_t)
    - [2.9 Class Template Argument Deduction](#29-class-template-argument-deduction)
        - [Class Template Arguments Deduction with String Literals](#class-template-arguments-deduction-with-string-literals)
        - [Deduction Guides](#deduction-guides)
    - [2.10 Templatized Aggregates](#210-templatized-aggregates)
    - [2.11 Summary](#211-summary)
  - [Chapter 3](#chapter-3)
  - [Nontype Template Parameters](#nontype-template-parameters)
    - [3.1 Nontype Class Template Parameters](#31-nontype-class-template-parameters)
    - [3.2 Nontype Function Template Parameters](#32-nontype-function-template-parameters)
    - [3.3 Restrictions for Nontype Template Parameters](#33-restrictions-for-nontype-template-parameters)
      - [Avoiding Invalid Expressions](#avoiding-invalid-expressions)
    - [3.4 Template Parameter Type **auto*(#34-template-parameter-type-auto)
    - [3.5 Summary](#35-summary)
  - [Chapter 4](#chapter-4)
  - [Variadic Templates](#variadic-templates)
    - [4.1 Variadic Templates](#41-variadic-templates)
      - [4.1.1 Variadic Templates by Example](#411-variadic-templates-by-example)
      - [4.1.2 Overloading Variadic and Nonvariadic Templates](#412-overloading-variadic-and-nonvariadic-templates)
      - [4.1.3 Operator **sizeof...*(#413-operator-sizeof)
    - [4.2 Fold Expressions](#42-fold-expressions)
    - [4.3 Application of Variadic Templates](#43-application-of-variadic-templates)
    - [4.4 Variadic Class Templates and Variadic Expressions](#44-variadic-class-templates-and-variadic-expressions)
      - [4.4.1 Variadic Expressions](#441-variadic-expressions)
      - [4.4.2 Variadic Indices](#442-variadic-indices)
      - [4.4.3 Variadic Class Templates](#443-variadic-class-templates)
      - [4.4.4 Variadic Deduction Guides](#444-variadic-deduction-guides)
      - [4.4.5 Variadic Base Classes and **using*(#445-variadic-base-classes-and-using)
    - [4.5 Summary](#45-summary)
  - [Chapter 5](#chapter-5)
  - [Tricky Basics](#tricky-basics)
    - [5.1 Keyword **typename*(#51-keyword-typename)
    - [5.2 Zero Initialization](#52-zero-initialization)
    - [5.3 Using **this->*(#53-using-this-)
    - [5.4 Templates for Raw Arrays and String Literals](#54-templates-for-raw-arrays-and-string-literals)
    - [5.5 Member Templates](#55-member-templates)
        - [Specialization of Member Function Templates](#specialization-of-member-function-templates)
        - [Special Member Function Templates](#special-member-function-templates)
      - [5.5.1 The **.template** Construct](#551-the-template-construct)
      - [5.5.2 Generic Lambdas and Member Templates](#552-generic-lambdas-and-member-templates)
    - [5.6 Variable Templates](#56-variable-templates)
        - [Variable Templates for Data Members](#variable-templates-for-data-members)
        - [Type Traits Suffix **\_v*(#type-traits-suffix-_v)
    - [5.7 Template Template Parameters](#57-template-template-parameters)
        - [Template Template Argument Matching](#template-template-argument-matching)
    - [5.8 Summary](#58-summary)
  - [Chapter 6](#chapter-6)
  - [Move Semantics and **enable\_if<>*(#move-semantics-and-enable_if)
    - [6.1 Perfect Forwarding](#61-perfect-forwarding)
    - [6.2 Special Member Function Templates](#62-special-member-function-templates)
    - [6.3 Disable Templates with **enable\_if<>*(#63-disable-templates-with-enable_if)
    - [6.4 Using **enable\_if<>*(#64-using-enable_if)
        - [Disabling Special Member Functions](#disabling-special-member-functions)
    - [6.5 Using Concepts to Simplify **enable\_if<>** Expressions](#65-using-concepts-to-simplify-enable_if-expressions)
    - [6.6 Summary](#66-summary)
  - [Chapter 7](#chapter-7)
  - [By Value or by Reference?](#by-value-or-by-reference)
    - [7.1 Passing by Value](#71-passing-by-value)
        - [Passing by Value Decays](#passing-by-value-decays)
    - [7.2 Passing by Reference](#72-passing-by-reference)
      - [7.2.1 Passing by Constant Reference](#721-passing-by-constant-reference)
        - [Passing by Reference Does Not Decay](#passing-by-reference-does-not-decay)
    - [7.2.2 Passing by Nonconstant Reference](#722-passing-by-nonconstant-reference)
    - [7.2.3 Passing by Forwarding Reference](#723-passing-by-forwarding-reference)
    - [7.3 Using **std::ref()** and **std::cref()*(#73-using-stdref-and-stdcref)
    - [7.4 Dealing with String Literals and Raw Arrays](#74-dealing-with-string-literals-and-raw-arrays)
    - [7.4.1 Special Implementations for String Literals and Raw Arrays](#741-special-implementations-for-string-literals-and-raw-arrays)
    - [7.5 Dealing with Return Values](#75-dealing-with-return-values)
    - [7.6 Recommended Template Parameter Declarations](#76-recommended-template-parameter-declarations)
        - [General Recommendations](#general-recommendations)
        - [Don't Be Over-Generic](#dont-be-over-generic)
    - [The **`std::make_pair()`** Example](#the-stdmake_pair-example)
    - [7.7 Summary](#77-summary)
  - [Chapter 8](#chapter-8)
  - [Compile-Time Programming](#compile-time-programming)
    - [8.1 Template Metaprogramming](#81-template-metaprogramming)
    - [8.2 Computing with **constexpr*(#82-computing-with-constexpr)
    - [8.3 Execution Path Selection with Partial Specialization](#83-execution-path-selection-with-partial-specialization)
    - [8.4 SFINAE (Substitution Failure Is Not An Error)](#84-sfinae-substitution-failure-is-not-an-error)
        - [SFINAE and Overload Resolution](#sfinae-and-overload-resolution)
      - [8.4.1 Expression SFINAE with **decltype*(#841-expression-sfinae-with-decltype)
    - [8.5 Compile-Time **if*(#85-compile-time-if)
    - [8.6 Summary](#86-summary)
  - [Chapter 9](#chapter-9)
  - [Using Templates in Practice](#using-templates-in-practice)
    - [9.1 The Inclusion Model](#91-the-inclusion-model)
      - [9.1.1 Linker Errors](#911-linker-errors)
      - [9.1.2 Templates in Header Files](#912-templates-in-header-files)
    - [9.2 Templates and **inline*(#92-templates-and-inline)
    - [9.3 Precompiled Headers](#93-precompiled-headers)
    - [9.4 Decoding the Error Novel](#94-decoding-the-error-novel)
        - [Simple Type Mismatch](#simple-type-mismatch)
    - [9.5 Afternotes](#95-afternotes)
    - [9.6 Summary](#96-summary)
  - [Chapter 10](#chapter-10)
  - [Basic Template Terminology](#basic-template-terminology)
    - [10.1 "Class Template" or "Template Class"?](#101-class-template-or-template-class)
    - [10.2 Substitution, Instantiation, and Specialization](#102-substitution-instantiation-and-specialization)
    - [10.3 Declarations versus Definitions](#103-declarations-versus-definitions)
      - [10.3.1 Complete versus Incomplete Types](#1031-complete-versus-incomplete-types)
    - [10.4 The One-Definition Rule](#104-the-one-definition-rule)
    - [10.5 Template Arguments versus Template Parameters](#105-template-arguments-versus-template-parameters)
    - [10.6 Summary](#106-summary)
  - [Chapter 11](#chapter-11)
  - [Generic Libraries](#generic-libraries)
    - [11.1 Callables](#111-callables)
      - [11.1.1 Supporting Function Objects](#1111-supporting-function-objects)
      - [11.1.2 Dealing with Member Functions and Additional Arguments](#1112-dealing-with-member-functions-and-additional-arguments)
      - [11.1.3 Wrapping Function Calls](#1113-wrapping-function-calls)
    - [11.2 Other Utilities to Implement Generic Libraries](#112-other-utilities-to-implement-generic-libraries)
      - [11.2.1 Type Traits](#1121-type-traits)
    - [11.2.2 **std::addressof()*(#1122-stdaddressof)
    - [11.2.3 **std::declval()*(#1123-stddeclval)
    - [11.3 Perfect Forwarding Temporaries](#113-perfect-forwarding-temporaries)
    - [11.4 References as Template Parameters](#114-references-as-template-parameters)
    - [11.5 Defer Evaluations](#115-defer-evaluations)
    - [11.6 Things to Consider When Writing Generic Libraries](#116-things-to-consider-when-writing-generic-libraries)
    - [11.7 Summary](#117-summary)
  - [Part II  Templates in Depth](#part-ii--templates-in-depth)
  - [Chapter 12](#chapter-12)
  - [Fundamentals in Depth](#fundamentals-in-depth)
    - [12.1 Parameterized Declarations](#121-parameterized-declarations)
        - [Union Templates](#union-templates)
        - [Default Call Arguments](#default-call-arguments)
        - [Nontemplate Members of Class Templates](#nontemplate-members-of-class-templates)
      - [12.1.1 Virtual Member Functions](#1211-virtual-member-functions)
      - [12.1.2 Linkage of Templates](#1212-linkage-of-templates)
      - [12.1.3 Primary Templates](#1213-primary-templates)
    - [12.2 Template Parameters](#122-template-parameters)
      - [12.2.1 Type Parameters](#1221-type-parameters)
      - [12.2.2 Nontype Parameters](#1222-nontype-parameters)
      - [12.2.3 Template Template Parameters](#1223-template-template-parameters)
      - [12.2.4 Template Parameter Packs](#1224-template-parameter-packs)
      - [12.2.5 Default Template Arguments](#1225-default-template-arguments)
    - [12.3 Template Arguments](#123-template-arguments)
      - [12.3.1 Function Template Arguments](#1231-function-template-arguments)
      - [12.3.2 Type Arguments](#1232-type-arguments)
      - [12.3.3 Nontype Arguments](#1233-nontype-arguments)
      - [12.3.4 Template Template Arguments](#1234-template-template-arguments)
      - [12.3.5 Equivalence](#1235-equivalence)
    - [12.4 Variadic Templates](#124-variadic-templates)
      - [12.4.1 Pack Expansions](#1241-pack-expansions)
      - [12.4.2 Where Can Pack Expansions Occur?](#1242-where-can-pack-expansions-occur)
      - [12.4.3 Function Parameter Packs](#1243-function-parameter-packs)
      - [12.4.4 Multiple and Nested Pack Expansions](#1244-multiple-and-nested-pack-expansions)
      - [12.4.5 Zero-Length Pack Expansions](#1245-zero-length-pack-expansions)
      - [12.4.6 Fold Expressions](#1246-fold-expressions)
    - [12.5 Friends](#125-friends)
      - [12.5.1 Friend Classes of Class Templates](#1251-friend-classes-of-class-templates)
      - [12.5.2 Friend Functions of Class Templates](#1252-friend-functions-of-class-templates)
      - [12.5.3 Friend Templates](#1253-friend-templates)
    - [12.6 Afternotes](#126-afternotes)
  - [Chapter 13](#chapter-13)
  - [Names in Templates](#names-in-templates)
    - [13.1 Name Taxonomy](#131-name-taxonomy)
    - [13.2 Looking Up Names](#132-looking-up-names)
      - [13.2.1 Argument-Dependent Lookup](#1321-argument-dependent-lookup)
      - [13.2.2 Argument-Dependent Lookup of Friend Declarations](#1322-argument-dependent-lookup-of-friend-declarations)
      - [13.2.3 Injected Class Names](#1323-injected-class-names)
      - [13.2.4 Current Instantiations](#1324-current-instantiations)
    - [13.3 Parsing Templates](#133-parsing-templates)
      - [13.3.1 Context Sensitivity in Nontemplates](#1331-context-sensitivity-in-nontemplates)
      - [13.3.2 Dependent Names of Types](#1332-dependent-names-of-types)
      - [13.3.3 Dependent Names of Templates](#1333-dependent-names-of-templates)
      - [13.3.4 Dependent Names in Using Declarations](#1334-dependent-names-in-using-declarations)
      - [13.3.5 ADL and Explicit Template Arguments](#1335-adl-and-explicit-template-arguments)
      - [13.3.6 Dependent Expressions](#1336-dependent-expressions)
      - [13.3.7 Compiler Errors](#1337-compiler-errors)
    - [13.4 Inheritance and Class Templates](#134-inheritance-and-class-templates)
      - [13.4.1 Nondependent Base Classes](#1341-nondependent-base-classes)
      - [13.4.2 Dependent Base Classes](#1342-dependent-base-classes)
    - [13.5 Afternotes](#135-afternotes)
  - [Chapter 14](#chapter-14)
  - [Instantiation](#instantiation)
    - [14.1 On-Demand Instantiation](#141-on-demand-instantiation)
    - [14.2 Lazy Instantiation](#142-lazy-instantiation)
      - [14.2.1 Partial and Full Instantiation](#1421-partial-and-full-instantiation)
      - [14.2.2 Instantiated Components](#1422-instantiated-components)
    - [14.3 The C++ Instantiation Model](#143-the-c-instantiation-model)
      - [14.3.1 Two-Phase Lookup](#1431-two-phase-lookup)
      - [14.3.2 Points of Instantiation](#1432-points-of-instantiation)
      - [14.3.3 The Inclusion Model](#1433-the-inclusion-model)
    - [14.4 Implementation Schemes](#144-implementation-schemes)
      - [14.4.1 Greedy Instantiation](#1441-greedy-instantiation)
      - [14.4.2 Queried Instantiation](#1442-queried-instantiation)
      - [14.4.3 Iterated Instantiation](#1443-iterated-instantiation)
    - [14.5 Explicit Instantiation](#145-explicit-instantiation)
      - [14.5.1 Manual Instantiation](#1451-manual-instantiation)
      - [14.5.2 Explicit Instantiation Declarations](#1452-explicit-instantiation-declarations)
    - [14.6 Compile-Time **if** Statements](#146-compile-time-if-statements)
    - [14.7 In the Standard Library](#147-in-the-standard-library)
    - [14.8 Afternotes](#148-afternotes)
  - [Chapter 15](#chapter-15)
  - [Template Argument Deduction](#template-argument-deduction)
    - [15.1 The Deduction Process](#151-the-deduction-process)
    - [15.2 Deduced Contexts](#152-deduced-contexts)
    - [15.3 Special Deduction Situations](#153-special-deduction-situations)
    - [15.4 Initializer Lists](#154-initializer-lists)
    - [15.5 Parameter Packs](#155-parameter-packs)
    - [15.5.1 Literal Operator Templates](#1551-literal-operator-templates)
    - [15.6 Rvalue References](#156-rvalue-references)
    - [15.6.1 Reference Collapsing Rules](#1561-reference-collapsing-rules)
    - [15.6.2 Forwarding References](#1562-forwarding-references)
    - [15.6.3 Perfect Forwarding](#1563-perfect-forwarding)
    - [Perfect Forwarding for Variadic Templates](#perfect-forwarding-for-variadic-templates)
    - [15.6.4 Deduction Surprises](#1564-deduction-surprises)
    - [15.7 SFINAE (Substitution Failure Is Not An Error)](#157-sfinae-substitution-failure-is-not-an-error)
    - [15.7.1 Immediate Context](#1571-immediate-context)
    - [15.8 Limitations of Deduction](#158-limitations-of-deduction)
    - [15.8.1 Allowable Argument Conversions](#1581-allowable-argument-conversions)
    - [15.8.2 Class Template Arguments](#1582-class-template-arguments)
    - [15.8.3 Default Call Arguments](#1583-default-call-arguments)
    - [15.8.4 Exception Specifications](#1584-exception-specifications)
    - [15.9 Explicit Function Template Arguments](#159-explicit-function-template-arguments)
    - [15.10 Deduction from Initializers and Expressions](#1510-deduction-from-initializers-and-expressions)
    - [15.10.1 The **auto** Type Specifier](#15101-the-auto-type-specifier)
    - [Deduced Return Types](#deduced-return-types)
    - [Deducible Nontype Parameters](#deducible-nontype-parameters)
      - [15.10.2 Expressing the Type of an Expression with **decltype*(#15102-expressing-the-type-of-an-expression-with-decltype)
      - [15.10.3 **decltype(auto)*(#15103-decltypeauto)
      - [15.10.4 Special Situations for **auto** Deduction](#15104-special-situations-for-auto-deduction)
      - [15.10.5 Structured Bindings](#15105-structured-bindings)
    - [15.10.6 Generic Lambdas](#15106-generic-lambdas)
    - [15.11 Alias Templates](#1511-alias-templates)
    - [15.12 Class Template Argument Deduction](#1512-class-template-argument-deduction)
      - [15.12.1 Deduction Guides](#15121-deduction-guides)
      - [15.12.2 Implicit Deduction Guides](#15122-implicit-deduction-guides)
      - [15.12.3 Other Subtleties](#15123-other-subtleties)
        - [Injected Class Names](#injected-class-names)
    - [Forwarding References](#forwarding-references)
        - [The **explicit** Keyword](#the-explicit-keyword)
        - [Copy Construction and Initializer Lists](#copy-construction-and-initializer-lists)
        - [Guides Are for Deduction Only](#guides-are-for-deduction-only)
    - [15.13 Afternotes](#1513-afternotes)
  - [Chapter 16](#chapter-16)
  - [Specialization and Overloading](#specialization-and-overloading)
    - [16.1 When "Generic Code" Doesn't Quite Cut It](#161-when-generic-code-doesnt-quite-cut-it)
      - [16.1.1 Transparent Customization](#1611-transparent-customization)
      - [16.1.2 Semantic Transparency](#1612-semantic-transparency)
    - [16.2 Overloading Function Templates](#162-overloading-function-templates)
      - [16.2.1 Signatures](#1621-signatures)
      - [16.2.2 Partial Ordering of Overloaded Function Templates](#1622-partial-ordering-of-overloaded-function-templates)
      - [16.2.3 Formal Ordering Rules](#1623-formal-ordering-rules)
      - [16.2.4 Templates and Nontemplates](#1624-templates-and-nontemplates)
      - [16.2.5 Variadic Function Templates](#1625-variadic-function-templates)
    - [16.3 Explicit Specialization](#163-explicit-specialization)
      - [16.3.1 Full Class Template Specialization](#1631-full-class-template-specialization)
      - [16.3.2 Full Function Template Specialization](#1632-full-function-template-specialization)
      - [16.3.3 Full Variable Template Specialization](#1633-full-variable-template-specialization)
      - [16.3.4 Full Member Specialization](#1634-full-member-specialization)
    - [16.4 Partial Class Template Specialization](#164-partial-class-template-specialization)
    - [16.5 Partial Variable Template Specialization](#165-partial-variable-template-specialization)
    - [16.6 Afternotes](#166-afternotes)
  - [Chapter 17](#chapter-17)
  - [Future Directions](#future-directions)
    - [17.1 Relaxed **typename** Rules](#171-relaxed-typename-rules)
    - [17.2 Generalized Nontype Template Parameters](#172-generalized-nontype-template-parameters)
    - [17.3 Partial Specialization of Function Templates](#173-partial-specialization-of-function-templates)
    - [17.4 Named Template Arguments](#174-named-template-arguments)
    - [17.5 Overloaded Class Templates](#175-overloaded-class-templates)
    - [17.6 Deduction for Nonfinal Pack Expansions](#176-deduction-for-nonfinal-pack-expansions)
    - [17.7 Regularization of **void*(#177-regularization-of-void)
    - [17.8 Type Checking for Templates](#178-type-checking-for-templates)
    - [17.9 Reflective Metaprogramming](#179-reflective-metaprogramming)
    - [17.10 Pack Facilities](#1710-pack-facilities)
    - [17.11 Modules](#1711-modules)
  - [Part III  Templates and Design](#part-iii--templates-and-design)
  - [Chapter 18](#chapter-18)
  - [The Polymorphic Power of Templates](#the-polymorphic-power-of-templates)
    - [18.1 Dynamic Polymorphism](#181-dynamic-polymorphism)
    - [18.2 Static Polymorphism](#182-static-polymorphism)
    - [18.3 Dynamic versus Static Polymorphism](#183-dynamic-versus-static-polymorphism)
        - [Terminology](#terminology)
        - [Strengths and Weaknesses](#strengths-and-weaknesses)
        - [Combining Both Forms](#combining-both-forms)
    - [18.4 Using Concepts](#184-using-concepts)
    - [18.5 New Forms of Design Patterns](#185-new-forms-of-design-patterns)
    - [18.6 Generic Programming](#186-generic-programming)
    - [18.7 Afternotes](#187-afternotes)
  - [Chapter 19](#chapter-19)
  - [Implementing Traits](#implementing-traits)
    - [19.1 An Example: Accumulating a Sequence](#191-an-example-accumulating-a-sequence)
      - [19.1.1 Fixed Traits](#1911-fixed-traits)
      - [19.1.2 Value Traits](#1912-value-traits)
      - [19.1.3 Parameterized Traits](#1913-parameterized-traits)
    - [19.2 Traits versus Policies and Policy Classes](#192-traits-versus-policies-and-policy-classes)
      - [19.2.1 Traits and Policies: What's the Difference?](#1921-traits-and-policies-whats-the-difference)
      - [19.2.2 Member Templates versus Template Template Parameters](#1922-member-templates-versus-template-template-parameters)
      - [19.2.3 Combining Multiple Policies and/or Traits](#1923-combining-multiple-policies-andor-traits)
      - [19.2.4 Accumulation with General Iterators](#1924-accumulation-with-general-iterators)
    - [19.3 Type Functions](#193-type-functions)
      - [19.3.1 Element Types](#1931-element-types)
      - [19.3.2 Transformation Traits](#1932-transformation-traits)
        - [Removing References](#removing-references)
        - [Adding References](#adding-references)
        - [Removing Qualifiers](#removing-qualifiers)
        - [Decay](#decay)
      - [19.3.3 Predicate Traits](#1933-predicate-traits)
        - [IsSameT](#issamet)
        - *true\_type** and **false\_type*(#true_type-and-false_type)
      - [19.3.4 Result Type Traits](#1934-result-type-traits)
        - *declval*(#declval)
    - [19.4 SFINAE-Based Traits](#194-sfinae-based-traits)
      - [19.4.1 SFINAE Out Function Overloads](#1941-sfinae-out-function-overloads)
        - [Alternative Implementation Strategies for SFINAE-based Traits](#alternative-implementation-strategies-for-sfinae-based-traits)
        - [Making SFINAE-based Traits Predicate Traits](#making-sfinae-based-traits-predicate-traits)
      - [19.4.2 SFINAE Out Partial Specializations](#1942-sfinae-out-partial-specializations)
      - [19.4.3 Using Generic Lambdas for SFINAE](#1943-using-generic-lambdas-for-sfinae)
      - [19.4.4 SFINAE-Friendly Traits](#1944-sfinae-friendly-traits)
    - [19.5 IsConvertibleT](#195-isconvertiblet)
        - [Handling Special Cases](#handling-special-cases)
    - [19.6 Detecting Members](#196-detecting-members)
      - [19.6.1 Detecting Member Types](#1961-detecting-member-types)
        - [Dealing with Reference Types](#dealing-with-reference-types)
        - [Injected Class Names](#injected-class-names-1)
      - [19.6.2 Detecting Arbitrary Member Types](#1962-detecting-arbitrary-member-types)
      - [19.6.3 Detecting Nontype Members](#1963-detecting-nontype-members)
        - [Detecting Member Functions](#detecting-member-functions)
        - [Detecting Other Expressions](#detecting-other-expressions)
      - [19.6.4 Using Generic Lambdas to Detect Members](#1964-using-generic-lambdas-to-detect-members)
    - [19.7 Other Traits Techniques](#197-other-traits-techniques)
      - [19.7.1 If-Then-Else](#1971-if-then-else)
      - [19.7.2 Detecting Nonthrowing Operations](#1972-detecting-nonthrowing-operations)
      - [19.7.3 Traits Convenience](#1973-traits-convenience)
        - [Alias Templates and Traits](#alias-templates-and-traits)
        - [Variable Templates and Traits](#variable-templates-and-traits)
    - [19.8 Type Classification](#198-type-classification)
      - [19.8.1 Determining Fundamental Types](#1981-determining-fundamental-types)
      - [19.8.2 Determining Compound Types](#1982-determining-compound-types)
        - [Pointers](#pointers)
        - [References](#references)
        - [Arrays](#arrays)
        - [Pointers to Members](#pointers-to-members)
      - [19.8.3 Identifying Function Types](#1983-identifying-function-types)
      - [19.8.4 Determining Class Types](#1984-determining-class-types)
      - [19.8.5 Determining Enumeration Types](#1985-determining-enumeration-types)
    - [19.9 Policy Traits](#199-policy-traits)
      - [19.9.1 Read-Only Parameter Types](#1991-read-only-parameter-types)
    - [19.10 In the Standard Library](#1910-in-the-standard-library)
    - [19.11 Afternotes](#1911-afternotes)
  - [Chapter 20](#chapter-20)
  - [Overloading on Type Properties](#overloading-on-type-properties)
    - [20.1 Algorithm Specialization](#201-algorithm-specialization)
    - [20.2 Tag Dispatching](#202-tag-dispatching)
    - [20.3 Enabling/Disabling Function Templates](#203-enablingdisabling-function-templates)
      - [20.3.1 Providing Multiple Specializations](#2031-providing-multiple-specializations)
      - [20.3.2 Where Does the **EnableIf** Go?](#2032-where-does-the-enableif-go)
      - [20.3.3 Compile-Time **if*(#2033-compile-time-if)
      - [20.3.4 Concepts](#2034-concepts)
    - [20.4 Class Specialization](#204-class-specialization)
      - [20.4.1 Enabling/Disabling Class Templates](#2041-enablingdisabling-class-templates)
      - [20.4.2 Tag Dispatching for Class Templates](#2042-tag-dispatching-for-class-templates)
    - [20.5 Instantiation-Safe Templates](#205-instantiation-safe-templates)
    - [20.6 In the Standard Library](#206-in-the-standard-library)
    - [20.7 Afternotes](#207-afternotes)
  - [Chapter 21](#chapter-21)
  - [Templates and Inheritance](#templates-and-inheritance)
    - [21.1 The Empty Base Class Optimization (EBCO)](#211-the-empty-base-class-optimization-ebco)
      - [21.1.1 Layout Principles](#2111-layout-principles)
      - [21.1.2 Members as Base Classes](#2112-members-as-base-classes)
    - [21.2 The Curiously Recurring Template Pattern (CRTP)](#212-the-curiously-recurring-template-pattern-crtp)
      - [21.2.1 The Barton-Nackman Trick](#2121-the-barton-nackman-trick)
      - [21.2.2 Operator Implementations](#2122-operator-implementations)
      - [21.2.3 Facades](#2123-facades)
        - [Defining a Linked-List Iterator](#defining-a-linked-list-iterator)
        - [Hiding the interface](#hiding-the-interface)
        - [Iterator Adapters](#iterator-adapters)
    - [21.3 Mixins](#213-mixins)
      - [21.3.1 Curious Mixins](#2131-curious-mixins)
      - [21.3.2 Parameterized Virtuality](#2132-parameterized-virtuality)
    - [21.4 Named Template Arguments](#214-named-template-arguments)
    - [21.5 Afternotes](#215-afternotes)
  - [Chapter 22](#chapter-22)
  - [Bridging Static and Dynamic Polymorphism](#bridging-static-and-dynamic-polymorphism)
    - [22.1 Function Objects, Pointers, and **std::function<>*(#221-function-objects-pointers-and-stdfunction)
    - [22.2 Generalized Function Pointers](#222-generalized-function-pointers)
    - [22.3 Bridge Interface](#223-bridge-interface)
    - [22.4 Type Erasure](#224-type-erasure)
    - [22.5 Optional Bridging](#225-optional-bridging)
    - [22.6 Performance Considerations](#226-performance-considerations)
    - [22.7 Afternotes](#227-afternotes)
  - [Chapter 23](#chapter-23)
  - [Metaprogramming](#metaprogramming)
    - [23.1 The State of Modern C++ Metaprogramming](#231-the-state-of-modern-c-metaprogramming)
      - [23.1.1 Value Metaprogramming](#2311-value-metaprogramming)
      - [23.1.2 Type Metaprogramming](#2312-type-metaprogramming)
      - [23.1.3 Hybrid Metaprogramming](#2313-hybrid-metaprogramming)
      - [23.1.4 Hybrid Metaprogramming for Unit Types](#2314-hybrid-metaprogramming-for-unit-types)
    - [23.2 The Dimensions of Reflective Metaprogramming](#232-the-dimensions-of-reflective-metaprogramming)
    - [23.3 The Cost of Recursive Instantiation](#233-the-cost-of-recursive-instantiation)
      - [23.3.1 Tracking All Instantiations](#2331-tracking-all-instantiations)
    - [23.4 Computational Completeness](#234-computational-completeness)
    - [23.5 Recursive Instantiation versus Recursive Template Arguments](#235-recursive-instantiation-versus-recursive-template-arguments)
    - [23.6 Enumeration Values versus Static Constants](#236-enumeration-values-versus-static-constants)
    - [23.7 Afternotes](#237-afternotes)
  - [Chapter 24](#chapter-24)
  - [Typelists](#typelists)
    - [24.1 Anatomy of a Typelist](#241-anatomy-of-a-typelist)
    - [24.2 Typelist Algorithms](#242-typelist-algorithms)
      - [24.2.1 Indexing](#2421-indexing)
      - [24.2.2 Finding the Best Match](#2422-finding-the-best-match)
      - [24.2.3 Appending to a Typelist](#2423-appending-to-a-typelist)
      - [24.2.4 Reversing a Typelist](#2424-reversing-a-typelist)
      - [24.2.5 Transforming a Typelist](#2425-transforming-a-typelist)
      - [24.2.6 Accumulating Typelists](#2426-accumulating-typelists)
      - [24.2.7 Insertion Sort](#2427-insertion-sort)
    - [24.3 Nontype Typelists](#243-nontype-typelists)
      - [24.3.1 Deducible Nontype Parameters](#2431-deducible-nontype-parameters)
    - [24.4 Optimizing Algorithms with Pack Expansions](#244-optimizing-algorithms-with-pack-expansions)
    - [24.5 Cons-style Typelists](#245-cons-style-typelists)
    - [24.6 Afternotes](#246-afternotes)
  - [Chapter 25](#chapter-25)
  - [Tuples](#tuples)
    - [25.1 Basic Tuple Design](#251-basic-tuple-design)
      - [25.1.1 Storage](#2511-storage)
      - [25.1.2 Construction](#2512-construction)
    - [25.2 Basic Tuple Operations](#252-basic-tuple-operations)
      - [25.2.1 Comparison](#2521-comparison)
      - [25.2.2 Output](#2522-output)
    - [25.3 Tuple Algorithms](#253-tuple-algorithms)
      - [25.3.1 Tuples as Typelists](#2531-tuples-as-typelists)
      - [25.3.2 Adding to and Removing from a Tuple](#2532-adding-to-and-removing-from-a-tuple)
      - [25.3.3 Reversing a Tuple](#2533-reversing-a-tuple)
      - [25.3.4 Index Lists](#2534-index-lists)
      - [25.3.5 Reversal with Index Lists](#2535-reversal-with-index-lists)
      - [25.3.6 Shuffle and Select](#2536-shuffle-and-select)
    - [25.4 Expanding Tuples](#254-expanding-tuples)
    - [25.5 Optimizing Tuple](#255-optimizing-tuple)
      - [25.5.1 Tuples and the EBCO](#2551-tuples-and-the-ebco)
      - [25.5.2 Constant-time **get()*(#2552-constant-time-get)
    - [25.6 Tuple Subscript](#256-tuple-subscript)
    - [25.7 Afternotes](#257-afternotes)
  - [Chapter 26](#chapter-26)
  - [Discriminated Unions](#discriminated-unions)
    - [26.1 Storage](#261-storage)
    - [26.2 Design](#262-design)
    - [26.3 Value Query and Extraction](#263-value-query-and-extraction)
    - [26.4 Element Initialization, Assignment and Destruction](#264-element-initialization-assignment-and-destruction)
      - [26.4.1 Initialization](#2641-initialization)
      - [26.4.2 Destruction](#2642-destruction)
      - [26.4.3 Assignment](#2643-assignment)
        - [Self-Assignment](#self-assignment)
        - [Exceptions](#exceptions)
    - [26.5 Visitors](#265-visitors)
      - [26.5.1 Visit Result Type](#2651-visit-result-type)
      - [26.5.2 Common Result Type](#2652-common-result-type)
    - [26.6 Variant Initialization and Assignment](#266-variant-initialization-and-assignment)
        - [Default Initialization](#default-initialization)
        - [Copy/Move Initialization](#copymove-initialization)
        - [Assignment](#assignment)
    - [26.7 Afternotes](#267-afternotes)
  - [Chapter 27](#chapter-27)
  - [Expression Templates](#expression-templates)
    - [27.1 Temporaries and Split Loops](#271-temporaries-and-split-loops)
    - [27.2 Encoding Expressions in Template Arguments](#272-encoding-expressions-in-template-arguments)
    - [27.2.1 Operands of the Expression Templates](#2721-operands-of-the-expression-templates)
      - [27.2.2 The **Array** Type](#2722-the-array-type)
      - [27.2.3 The Operators](#2723-the-operators)
      - [27.2.4 Review](#2724-review)
      - [27.2.5 Expression Templates Assignments](#2725-expression-templates-assignments)
    - [27.3 Performance and Limitations of Expression Templates](#273-performance-and-limitations-of-expression-templates)
    - [27.4 Afternotes](#274-afternotes)
  - [Chapter 28](#chapter-28)
  - [Debugging Templates](#debugging-templates)
    - [28.1 Shallow Instantiation](#281-shallow-instantiation)
        - [Concept Checking](#concept-checking)
    - [28.2 Static Assertions](#282-static-assertions)
    - [28.3 Archetypes](#283-archetypes)
    - [28.4 Tracers](#284-tracers)
    - [28.5 Oracles](#285-oracles)
    - [28.6 Afternotes](#286-afternotes)
  - [Appendix A](#appendix-a)
  - [The One-Definition Rule](#the-one-definition-rule)
    - [A.1 Translation Units](#a1-translation-units)
    - [A.2 Declarations and Definitions](#a2-declarations-and-definitions)
    - [A.3 The One-Definition Rule in Detail](#a3-the-one-definition-rule-in-detail)
      - [A.3.1 One-per-Program Constraints](#a31-one-per-program-constraints)
      - [A.3.2 One-per-Translation Unit Constraints](#a32-one-per-translation-unit-constraints)
      - [A.3.3 Cross-Translation Unit Equivalence Constraints](#a33-cross-translation-unit-equivalence-constraints)
  - [Appendix B](#appendix-b)
  - [Value Categories](#value-categories)
    - [B.1 Traditional Lvalues and Rvalues](#b1-traditional-lvalues-and-rvalues)
      - [B.1.1 Lvalue-to-Rvalue Conversions](#b11-lvalue-to-rvalue-conversions)
    - [B.2 Value Categories Since C++11](#b2-value-categories-since-c11)
      - [B.2.1 Temporary Materialization](#b21-temporary-materialization)
    - [B.3 Checking Value Categories with **decltype*(#b3-checking-value-categories-with-decltype)
    - [B.4 Reference Types](#b4-reference-types)
  - [Appendix C](#appendix-c)
  - [Overload Resolution](#overload-resolution)
    - [C.1 When Does Overload Resolution Kick In?](#c1-when-does-overload-resolution-kick-in)
    - [C.2 Simplified Overload Resolution](#c2-simplified-overload-resolution)
      - [C.2.1 The Implied Argument for Member Functions](#c21-the-implied-argument-for-member-functions)
    - [C.2.2 Refining the Perfect Match](#c22-refining-the-perfect-match)
    - [C.3 Overloading Details](#c3-overloading-details)
      - [C.3.1 Prefer Nontemplates or More Specialized Templates](#c31-prefer-nontemplates-or-more-specialized-templates)
      - [C.3.2 Conversion Sequences](#c32-conversion-sequences)
      - [C.3.3 Pointer Conversions](#c33-pointer-conversions)
      - [C.3.4 Initializer Lists](#c34-initializer-lists)
      - [C.3.5 Functors and Surrogate Functions](#c35-functors-and-surrogate-functions)
      - [C.3.6 Other Overloading Contexts](#c36-other-overloading-contexts)
  - [Appendix D](#appendix-d)
  - [Standard Type Utilities](#standard-type-utilities)
    - [D.1 Using Type Traits](#d1-using-type-traits)
      - [D.1.1 **std::integral\_constant** and **std::bool\_constant*(#d11-stdintegral_constant-and-stdbool_constant)
      - [D.1.2 Things You Should Know When Using Traits](#d12-things-you-should-know-when-using-traits)
    - [D.2 Primary and Composite Type Categories](#d2-primary-and-composite-type-categories)
      - [D.2.1 Testing for the Primary Type Category](#d21-testing-for-the-primary-type-category)
      - [D.2.2 Test for Composite Type Categories](#d22-test-for-composite-type-categories)
    - [D.3 Type Properties and Operations](#d3-type-properties-and-operations)
      - [D.3.1 Other Type Properties](#d31-other-type-properties)
      - [D.3.2 Test for Specific Operations](#d32-test-for-specific-operations)
      - [D.3.3 Relationships Between Types](#d33-relationships-between-types)
    - [D.4 Type Construction](#d4-type-construction)
    - [D.5 Other Traits](#d5-other-traits)
    - [D.6 Combining Type Traits](#d6-combining-type-traits)
    - [D.7 Other Utilities](#d7-other-utilities)
  - [Appendix E](#appendix-e)
  - [Concepts](#concepts)
    - [E.1 Using Concepts](#e1-using-concepts)
        - [Dealing with Requirements](#dealing-with-requirements)
        - [Dealing with Multiple Requirements](#dealing-with-multiple-requirements)
        - [Shorthand Notation for Single Requirements](#shorthand-notation-for-single-requirements)
    - [E.2 Defining Concepts](#e2-defining-concepts)
    - [E.3 Overloading on Constraints](#e3-overloading-on-constraints)
      - [E.3.1 Constraint Subsumption](#e31-constraint-subsumption)
      - [E.3.2 Constraints and Tag Dispatching](#e32-constraints-and-tag-dispatching)
    - [E.4 Concept Tips](#e4-concept-tips)
      - [E.4.1 Testing Concepts](#e41-testing-concepts)
      - [E.4.2 Concept Granularity](#e42-concept-granularity)
      - [E.4.3 Binary Compatibility](#e43-binary-compatibility)
  - [Code Snippets](#code-snippets)
  - [Bibliography](#bibliography)
    - [Forums](#forums)
    - [Books and Web Sites](#books-and-web-sites)
  - [Glossary](#glossary)
```

## Preface

The notion of templates in C++ is over 30 years old. C++ templates were already documented in 1990 in "The Annotated C++ Reference Manual" (ARM; see [EllisStroustrupARM]), and they had been described before then in more specialized publications. However, well over a decade later, we found a dearth of literature that concentrates on the fundamental concepts and advanced techniques of this fascinating, complex, and powerful C++ feature. With the first edition of this book, we wanted to address this issue and decided to write _the_ book about templates (with perhaps a slight lack of humility).

> C++ 中模板的概念已经有 30 多年的历史了。C++ 模板已经在 1990 年的“注释 C++ 参考手册”(ARM；参见[EllisStrouttrupARM])中进行了记录，在此之前，它们已经在更专业的出版物中进行了描述。然而，十多年后，我们发现缺乏专注于这一迷人、复杂和强大的 C++ 功能的基本概念和先进技术的文献。在这本书的第一版中，我们想解决这个问题，并决定写一本关于模板的书(也许有点不谦虚)。

Much has changed in C++ since that first edition was published in late 2002. New iterations of the C++ standard have added new features, and continued innovation in the C++ community has uncovered new template-based programming techniques. The second edition of this book therefore retains the same goals as the first edition, but for "Modern C++."

> 自 2002 年末第一版发布以来，C++ 已经发生了很大变化。C++ 标准的新迭代增加了新的功能，C++ 社区的持续创新揭示了新的基于模板的编程技术。因此，本书的第二版保留了与第一版相同的目标，但针对“现代 C++”

We approached the task of writing this book with different backgrounds and with different intentions. David (aka "Daveed"), an experienced compiler implementer and active participant of the C++ Standard Committee working groups that evolve the core language, was interested in a precise and detailed description of all the power (and problems) of templates. Nico, an "ordinary" application programmer and member of the C++ Standard Committee Library Working Group, was interested in understanding all the techniques of templates in a way that he could use and benefit from them. Doug, a template library developer turned compiler implementer and language designer, was interested in collecting, categorizing, and evaluating the myriad techniques used to build template libraries. In addition, we all wanted to share this knowledge with you, the reader, and the whole community to help to avoid further misunderstanding, confusion, or apprehension.

> 我们怀着不同的背景和不同的意图来完成写这本书的任务。David(又名“Davied”)是一位经验丰富的编译器实现者，也是开发核心语言的 C++ 标准委员会工作组的积极参与者，他对模板的所有功能(和问题)的精确而详细的描述很感兴趣。Nico 是一名“普通”应用程序程序员，也是 C++ 标准委员会图书馆工作组的成员，他有兴趣以一种可以使用并从中受益的方式来理解模板的所有技术。Doug 是一名模板库开发人员，后来成为编译器实现者和语言设计师，他对收集、分类和评估用于构建模板库的无数技术很感兴趣。此外，我们都想与您、读者和整个社区分享这些知识，以帮助避免进一步的误解、困惑或担忧。

As a consequence, you will see both conceptual introductions with day-to-day examples and detailed descriptions of the exact behavior of templates. Starting from the basic principles of templates and working up to the "art of template programming," you will discover (or rediscover) techniques such as static polymorphism, type traits, metaprogramming, and expression templates. You will also gain a deeper understanding of the C++ standard library, in which almost all code involves templates.

> 因此，您将看到带有日常示例的概念介绍和对模板确切行为的详细描述。从模板的基本原理开始，一直到“模板编程艺术”，您将发现(或重新发现)静态多态性、类型特征、元编程和表达式模板等技术。您还将对 C++ 标准库有更深入的了解，其中几乎所有代码都涉及模板。

We learned a lot and we had much fun while writing this book. We hope you will have the same experience while reading it. Enjoy!

> 在写这本书的时候，我们学到了很多，也玩得很开心。我们希望你在阅读时也能有同样的体验。享受吧！

## Acknowledgments for the Second Edition

Writing a book is hard. Maintaining a book is even harder. It took us more than five years---spread over the past decade---to come up with this second edition, and it couldn't have been done without the support and patience of a lot of people.

> 写书很难。维护一本书更难。在过去的十年里，我们花了五年多的时间才完成了第二版，如果没有很多人的支持和耐心，这是不可能完成的。

First, we'd like to thank everyone in the C++ community and on the C++ standardization committee. In addition to all the work to add new language and library features, they spent many, many hours explaining and discussing their work with us, and they did so with patience and enthusiasm.

> 首先，我们要感谢 C++ 社区和 C++ 标准化委员会的每一个人。除了增加新的语言和图书馆功能的所有工作外，他们还花了很多很多小时与我们解释和讨论他们的工作，他们这样做是有耐心和热情的。

Part of this community also includes the programmers who gave feedback for errors and possible improvement for the first edition over the past 15 years. There are simply too many to list them all, but you know who you are and we're truly grateful to you for taking the time to write up your thoughts and observations. Please accept our apologies if our answers were sometimes less than prompt.

> 这个社区的一部分还包括程序员，他们在过去 15 年中为第一版的错误和可能的改进提供了反馈。太多了，无法一一列出，但你知道自己是谁，我们非常感谢你花时间写下你的想法和观察。如果我们的回答有时不够及时，请接受我们的歉意。

We'd also like to thank everyone who reviewed drafts of this book and provided us with valuable feedback and clarifications. These reviews brought the book to a significantly higher level of quality, and it again proved that good things need the input of many "wise guys." For this reason, huge thanks to Steve Dewhurst, Howard Hinnant, Mikael Kilpel¨ainen, Dietmar Kühl, Daniel Krügler, Nevin Lieber, Andreas Neiser, Eric Niebler, Richard Smith, Andrew Sutton, Hubert Tong, and Ville Voutilainen.

> 我们还要感谢每一位审阅本书草稿并为我们提供宝贵反馈和澄清的人。这些评论将这本书的质量提升到了一个显著的水平，它再次证明了好的东西需要许多“智者”的投入。因此，非常感谢 Steve Dewhurst、Howard Hinnant、Mikael Kilpel¨ainen、Dietmar Kühl、Daniel Krügler、Nevin Lieber、Andreas Neiser、Eric Niebler、Richard Smith、Andrew Sutton、Hubert Tong 和 Ville Voutilainen。

Of course, thanks to all the people who supported us from Addison-Wesley/Pearson. These days, you can no longer take professional support for book authors for granted. But they were patient, nagged us when appropriate, and were of great help when knowledge and professionalism were necessary. So, many thanks to Peter Gordon, Kim Boedigheimer, Greg Doench, Julie Nahil, Dana Wilson, and Carol Lallier.

> 当然，感谢艾迪生-卫斯理/培生所有支持我们的人。如今，你不能再把对图书作者的专业支持视为理所当然。但他们很有耐心，在适当的时候对我们唠叨不休，在需要知识和专业精神的时候，他们会给我们很大的帮助。非常感谢 Peter Gordon、Kim Boedigheimer、Greg Doench、Julie Nahil、Dana Wilson 和 Carol Lallier。

A special thanks goes to the LaTeX community for a great text system and to Frank Mittelbach for solving our LATEX issues (it was almost always our fault).

> 特别感谢 LaTeX 社区提供了一个出色的文本系统，并感谢 Frank Mittelbach 解决了我们的 LaTeX 问题(这几乎总是我们的错)。

### David's Acknowledgments for the Second Edition

This second edition was a long time in the waiting, and as we put the finishing touches to it, I am grateful for the people in my life who made it possible despite many obligations vying for attention. First, I'm indebted to my wife (Karina) and daughters (Alessandra and Cassandra), for agreeing to let me take significant time out of the "family schedule" to complete this edition, particularly in the last year of work. My parents have always shown interest in my goals, and whenever I visit them, they do not forget this particular project.

> 这第二版等待了很长时间，当我们为它做最后的润色时，我感谢我生命中的人们，尽管有很多义务在争夺关注，但他们还是让它成为了可能。首先，我感谢我的妻子(Karina)和女儿(Alessandra 和 Cassandra)，他们同意让我从“家庭日程”中抽出大量时间来完成这一版本，尤其是在工作的最后一年。我的父母一直对我的目标感兴趣，每当我去看望他们时，他们都不会忘记这个特殊的项目。

Clearly, this is a technical book, and its contents reflect knowledge and experience about a programming topic. However, that is not enough to pull off completing this kind of work. I'm therefore extremely grateful to Nico for having taken upon himself the "management" and "production" aspects of this edition (in addition to all of his technical contributions). If this book is useful to you and you run into Nico some day, be sure to tell him thanks for keeping us all going. I'm also thankful to Doug for having agreed to come on board several years ago and to keep going even as demands on his own schedule made for tough going.

> 显然，这是一本技术性的书，其内容反映了编程主题的知识和经验。然而，这还不足以完成这类工作。因此，我非常感谢 Nico 承担了本版本的“管理”和“生产”方面的工作(以及他的所有技术贡献)。如果这本书对你有用，并且有一天你遇到了尼科，一定要告诉他谢谢你让我们继续前行。我也很感谢 Doug 几年前就同意加入，并继续前进，尽管他自己的日程安排要求很高。

Many programmers in our C++ community have shared nuggets of insight over the years, and I am grateful to all of them. However, I owe special thanks to Richard Smith, who has been efficiently answering my e-mails with arcane technical issues for years now. In the same vein, thanks to my colleagues John Spicer, Mike Miller, and Mike Herrick, for sharing their knowledge and creating an encouraging work environment that allows us to learn ever more.

> 多年来，我们 C++ 社区中的许多程序员都分享了一些真知灼见，我非常感谢他们。然而，我要特别感谢 Richard Smith，多年来他一直在用晦涩的技术问题高效地回复我的电子邮件。同样，感谢我的同事 John Spicer、Mike Miller 和 Mike Herrick 分享他们的知识，并创造了一个令人鼓舞的工作环境，让我们能够学到更多。

### Nico's Acknowledgments for the Second Edition

First, I want to thank the two hard-core experts, David and Doug, because, as an application programmer and library expert, I asked so many silly questions and learned so much. I now feel like becoming a core expert (only until the next issue, of course). It was fun, guys.

> 首先，我要感谢两位核心专家，David 和 Doug，因为作为一名应用程序程序员和库专家，我问了很多愚蠢的问题，学到了很多。我现在想成为一名核心专家(当然，只到下一期为止)。很有趣，伙计们。

All my other thanks go to Jutta Eckstein. Jutta has the wonderful ability to force and support people in their ideals, ideas, and goals. While most people experience this only occasionally when meeting her or working with her in our IT industry, I have the honor to benefit from her in my day-to-day life. After all these years, I still hope this will last forever.

> 我还要感谢尤塔·埃克斯坦。尤塔拥有强大的能力，能够在人们的理想、想法和目标方面给予他们力量和支持。虽然大多数人在 IT 行业遇到她或与她共事时偶尔会遇到这种情况，但我有幸在日常生活中从她身上受益。这么多年过去了，我仍然希望这将永远持续下去。

### Doug's Acknowledgments for the Second Edition

My heartfelt thanks go to my wonderful and supportive wife, Amy, and our two little girls, Molly and Tessa. Their love and companionship bring me daily joy and the confidence to tackle the greatest challenges in life and work. I'd also like to thank my parents, who instilled in me a great love of learning and encouraged me throughout these years.

> 我衷心感谢我出色且支持我的妻子 Amy，以及我们的两个小女儿 Molly 和 Tessa。他们的爱和陪伴给我带来了每天的快乐和应对生活和工作中最大挑战的信心。我还要感谢我的父母，这些年来，他们给我灌输了对学习的热爱，并鼓励我。

It was a pleasure to work with both David and Nico, who are so different in personality yet complement each other so well. David brings a great clarity to technical writing, honing in on descriptions that are precise and illuminating. Nico, beyond his exceptional organizational skills that kept two coauthors from wandering off into the weeds, brings a unique ability to take apart a complex technical discussion and make it simpler, more accessible, and far, far clearer.

> 很高兴能和大卫和尼科一起工作，他们性格迥异，但互补性很好。David 为技术写作带来了极大的清晰度，在精确而富有启发性的描述中不断磨练。Nico 除了出色的组织技能使两位合著者免于陷入困境之外，他还拥有一种独特的能力，可以分解复杂的技术讨论，使其更简单、更容易理解，也更清晰。

## Acknowledgments for the First Edition

This book presents ideas, concepts, solutions, and examples from many sources. We'd like to thank all the people and companies who helped and supported us during the past few years.

> 本书介绍了许多来源的想法、概念、解决方案和示例。我们要感谢在过去几年里帮助和支持我们的所有人和公司。

First, we'd like to thank all the reviewers and everyone else who gave us their opinion on early manuscripts. These people endow the book with a quality it would never have had without their input. The reviewers for this book were Kyle Blaney, Thomas Gschwind, Dennis Mancl, Patrick Mc Killen, and Jan Christiaan van Winkel. Special thanks to Dietmar Kühl, who meticulously reviewed and edited the whole book. His feedback was an incredible contribution to the quality of this book.

> 首先，我们要感谢所有的审稿人和其他所有对早期手稿发表意见的人。这些人赋予了这本书一种没有他们的投入就永远不会有的品质。这本书的评论家是凯尔·布莱尼、托马斯·格施温、丹尼斯·曼克尔、帕特里克·麦克基伦和扬·克里斯蒂安·范·温克尔。特别感谢 Dietmar Kühl，他对整本书进行了细致的审阅和编辑。他的反馈对这本书的质量做出了令人难以置信的贡献。

We'd also like to thank all the people and companies who gave us the opportunity to test our examples on different platforms with different compilers. Many thanks to the Edison Design Group for their great compiler and their support. It was a big help during the standardization process and the writing of this book. Many thanks also go to all the developers of the free GNU and egcs compilers (Jason Merrill was especially responsive) and to Microsoft for an evaluation version of Visual C++ (Jonathan Caves, Herb Sutter, and Jason Shirk were our contacts there).

> 我们还要感谢所有给我们机会在不同平台上使用不同编译器测试示例的人和公司。非常感谢爱迪生设计集团的优秀编译器和他们的支持。这对本书的标准化过程和写作都有很大帮助。还要感谢所有免费 GNU 和 egcs 编译器的开发人员(Jason Merrill 的反应特别快)，以及微软提供的 Visual C++ 评估版本(Jonathan Caves、Herb Sutter 和 Jason Shirk 是我们的联系人)。

Much of the existing "C++ wisdom" was collectively created by the online C++ community. Most of it comes from the moderated Usenet groups `comp.lang.c++.moderated` and `comp.std.c++`. We are therefore especially indebted to the active moderators of those groups, who keep the discussions useful and constructive. We also much appreciate all those who over the years have taken the time to describe and explain their ideas for us all to share.

> 大部分现有的“C++ 智慧”都是由在线 C++ 社区共同创建的。其中大部分来自有节制的 Usenet 小组“comp.lang.c++.mediated”和“comp.std.c++”。因此，我们特别感谢这些小组的积极主持人，他们保持了有益和建设性的讨论。我们也非常感谢那些多年来花时间描述和解释他们的想法供我们大家分享的人。

The Addison-Wesley team did another great job. We are most indebted to Debbie Lafferty (our editor) for her gentle prodding, good advice, and relentless hard work in support of this book. Thanks also go to Tyrrell Albaugh, Bunny Ames, Melanie Buck, Jacquelyn Doucette, Chanda Leary-Coutu, Catherine Ohala, and Marty Rabinowitz. We're grateful as well to Marina Lang, who first sponsored this book within Addison-Wesley. Susan Winer contributed an early round of editing that helped shape our later work.

> Addison-Wesley 团队又做了一件很棒的工作。我们非常感谢 Debbie Lafferty(我们的编辑)为支持这本书所做的温和的鞭策、良好的建议和不懈的努力。还要感谢 Tyrrell Albaugh、Bunny Ames、Melanie Buck、Jacquelyn Doucette、Chanda Leary Coutu、Catherine Ohala 和 Marty Rabinowitz。我们也非常感谢 Marina Lang，她在 Addison Wesley 内部首次赞助了这本书。苏珊·怀纳(Susan Winer)参与了早期的编辑工作，帮助塑造了我们后来的作品。

### Nico's Acknowledgments for the First Edition

My first personal thanks go with a lot of kisses to my family: Ulli, Lucas, Anica, and Frederic supported this book with a lot of patience, consideration, and encouragement.

> 我首先要感谢我的家人：Ulli、Lucas、Anica 和 Frederic 以极大的耐心、体贴和鼓励支持了这本书。

In addition, I want to thank David. His expertise turned out to be incredible, but his patience was even better (sometimes I ask really silly questions). It is a lot of fun to work with him.

> 此外，我还要感谢大卫。他的专业知识令人难以置信，但他的耐心甚至更好(有时我会问一些非常愚蠢的问题)。和他一起工作很有趣。

### David's Acknowledgments for the First Edition

My wife, Karina, has been instrumental in this book coming to a conclusion, and I am immensely grateful for the role that she plays in my life. Writing "in your spare time" quickly becomes erratic when many other activities vie for your schedule. Karina helped me to manage that schedule, taught me to say "no" in order to make the time needed to make regular progress in the writing process, and above all was amazingly supportive of this project. I thank God every day for her friendship and love.

> 我的妻子卡琳娜在这本书的结局中发挥了重要作用，我非常感谢她在我的生活中所扮演的角色。当许多其他活动争夺你的日程安排时，“在业余时间”写作很快就会变得不稳定。Karina 帮助我管理这个时间表，教我说“不”，以便在写作过程中有规律地取得进展，最重要的是，她非常支持这个项目。我每天都感谢上帝给予我的友谊和爱。

I'm also tremendously grateful to have been able to work with Nico. Besides his directly visible contributions to the text, his experience and discipline moved us from my pitiful doodling to a well-organized production.

> 我也非常感激能够和尼科一起工作。除了他对文本的直接贡献外，他的经验和纪律让我们从我可怜的涂鸦变成了一部组织严密的作品。

John "Mr. Template" Spicer and Steve "Mr. Overload" Adamczyk are wonderful friends and colleagues, but in my opinion they are (together) also the ultimate authority regarding the core C++ language. They clarified many of the trickier issues described in this book, and should you find an error in the description of a C++ language element, it is almost certainly attributable to my failing to consult with them.

> John“Mr.Template”Spicer 和 Steve“Mr.Overload”Adamczyk 是很好的朋友和同事，但在我看来，他们(一起)也是核心 C++ 语言的最终权威。他们澄清了本书中描述的许多棘手问题，如果你在描述 C++ 语言元素时发现错误，几乎可以肯定的是，这是由于我没有与他们协商。

Finally, I want to express my appreciation to those who were supportive of this project without necessarily contributing to it directly (the power of cheer cannot be understated). First, my parents: Their love for me and their encouragement made all the difference. And then there are the numerous friends inquiring: "How is the book going?" They, too, were a source of encouragement: Michael Beckmann, Brett and Julie Beene, Jarran Carr, Simon Chang, Ho and Sarah Cho, Christophe De Dinechin, Ewa Deelman, Neil Eberle, Sassan Hazeghi, Vikram Kumar, Jim and Lindsay Long, R.J. Morgan, Mike Puritano, Ragu Raghavendra, Jim and Phuong Sharp, Gregg Vaughn, and John Wiegley.

> 最后，我想向那些支持这个项目但不一定直接为其做出贡献的人表示感谢(欢呼的力量不容低估)。首先，我的父母：他们对我的爱和鼓励让一切变得不同。还有许多朋友在问：“这本书进展如何？”他们也是鼓励的源泉：迈克尔·贝克曼、布雷特和朱莉·比恩、贾兰·卡尔、张西蒙、何和莎拉·赵、克里斯托弗·德·迪内钦、埃娃·迪尔曼、尼尔·埃伯利、萨桑·哈泽吉、维克拉姆·库马尔、吉姆和林赛·朗、R.J.摩根、迈克·清教徒、拉古·拉加文德拉、吉姆和彭·夏普、格雷格·沃恩、，和约翰·维格利。

## About This Book

The first edition of this book was published almost 15 years ago. We had set out to write the definitive guide to C++ templates, with the expectation that it would be useful to practicing C++ programmers. That project was successful: It's been tremendously gratifying to hear from readers who found our material helpful, to see our book time and again being recommended as a work of reference, and to be universally well reviewed.

> 这本书的第一版出版于大约 15 年前。我们已经着手编写 C++ 模板的权威指南，希望它对实践 C++ 程序员有用。该项目取得了成功：很高兴听到读者们认为我们的材料很有帮助，看到我们的书一次又一次地被推荐为参考作品，并得到普遍好评。

That first edition has aged well, with most material remaining entirely relevant to the modern C++ programmer, but there is no denying that the evolution of the language---culminating in the "Modern C++" standards, C++11, C++14, and C++17---has raised the need for a revision of the material in the first edition.

> 第一版已经过时了，大多数材料仍然与现代 C++ 程序员完全相关，但不可否认，该语言的演变——最终形成了“现代 C++”标准 C++11、C++14 和 C++17——提出了对第一版材料进行修订的必要性。

So with this second edition, our high-level goal has remained unchanged: to provide the definitive guide to C++ templates, including both a solid reference and an accessible tutorial. This time, however, we work with the "Modern C++" language, which is a significantly bigger beast (still!) than the language available at the time of the prior edition.

> 因此，在第二版中，我们的高级目标保持不变：提供 C++ 模板的最终指南，包括可靠的参考和可访问的教程。然而，这一次，我们使用的是“现代 C++”语言，它比上一版本时的语言要大得多。

We're also acutely aware that C++ programming resources have changed (for the better) since the first edition was published. For example, several books have appeared that develop specific template-based applications in great depth. More important, far more information about C++ templates and template-based techniques is easily available online, as are examples of advanced uses of these techniques. So in this edition, we have decided to emphasize a breadth of techniques that can be used in a variety of applications.

> 我们还敏锐地意识到，自第一版发布以来，C++ 编程资源已经发生了变化(变得更好)。例如，已经出版了几本书，深入开发了特定的基于模板的应用程序。更重要的是，关于 C++ 模板和基于模板的技术的更多信息可以很容易地在网上获得，这些技术的高级使用示例也是如此。因此，在本期中，我们决定强调可用于各种应用程序的广泛技术。

Some of the techniques we presented in the first edition have become obsolete because the C++ language now offers more direct ways of achieving the same effects. Those techniques have been dropped (or relegated to minor notes), and instead you'll find new techniques that show the state-ofthe-art uses of the new language.

> 我们在第一版中介绍的一些技术已经过时，因为 C++ 语言现在提供了更直接的方法来实现同样的效果。这些技巧已经被删除(或被放在次要注释中)，取而代之的是，你会发现新的技巧，展示了新语言的最新使用状态。

We've now lived over 20 years with C++ templates, but the C++ programmers' community still regularly finds new fundamental insights into the way they can fit in our software development needs. Our goal with this book is to share that knowledge but also to fully equip the reader to develop new understanding and, perhaps, discover the next major C++ technique.

> 我们现在已经使用 C++ 模板生活了 20 多年，但 C++ 程序员社区仍然定期发现新的基本见解，了解它们如何适应我们的软件开发需求。我们这本书的目标是分享这些知识，同时也让读者充分掌握新的理解，也许还能发现下一个主要的 C++ 技术。

### What You Should Know Before Reading This Book

To get the most from this book, you should already know C++. We describe the details of a particular language feature, not the fundamentals of the language itself. You should be familiar with the concepts of classes and inheritance, and you should be able to write C++ programs using components such as IOstreams and containers from the C++ standard library. You should also be familiar with the basic features of "Modern C++", such as `auto`, `decltype`, move semantics, and lambdas. Nevertheless, we review more subtle issues as the need arises, even when such issues aren't directly related to templates. This ensures that the text is accessible to experts and intermediate programmers alike.

> 要想从这本书中获得最大的收获，你应该已经知道 C++ 了。我们描述的是特定语言特征的细节，而不是语言本身的基本原理。您应该熟悉类和继承的概念，并且应该能够使用 C++ 标准库中的 IOstreams 和容器等组件编写 C++ 程序。您还应该熟悉“现代 C++”的基本功能，如“auto”、“decltype”、移动语义和 lambdas。尽管如此，我们还是会根据需要审查更微妙的问题，即使这些问题与模板没有直接关系。这确保了专家和中级程序员都可以访问文本。

We deal primarily with the C++ language revisions standardized in 2011, 2014, and 2017. However, at the time of this writing, the ink is barely dry on the C++17 revision, and we expect that most of our readers will not be intimately familiar with its details. All revisions had a significant impact on the behavior and usage of templates. We therefore provide short introductions to those new features that have the greatest bearing on our subject matter. However, our goal is neither to introduce the modern C++ standards nor to provide an exhaustive description of the changes from the prior versions of this standard ([C++98] and [C++03]). Instead, we focus on templates as designed and used in C++, using the modern C++ standards ([C++11], [C++14], and [C++17]) as our basis, and we occasionally call out cases where the modern C++ standards enable or encourage different techniques than the prior standards.

> 我们主要处理 2011 年、2014 年和 2017 年标准化的 C++ 语言修订。然而，在撰写本文时，C++17 修订版的墨水还没有干，我们预计大多数读者不会非常熟悉它的细节。所有修订都对模板的行为和使用产生了重大影响。因此，我们将简要介绍那些对我们的主题影响最大的新功能。然而，我们的目标既不是引入现代 C++ 标准，也不是对本标准先前版本([C++98]和[C++03])的变化进行详尽描述。相反，我们关注 C++ 中设计和使用的模板，使用现代 C++ 标准([C++11]、[C++14]和[C++17])作为我们的基础，我们偶尔会指出现代 C++ 标准支持或鼓励使用与先前标准不同的技术的情况。

### Overall Structure of the Book

Our goal is to provide the information necessary to start using templates and benefit from their power, as well as to provide information that will enable experienced programmers to push the limits of the state-of-the-art. To achieve this, we decided to organize our text in _parts_:

> 我们的目标是提供开始使用模板所需的信息，并从模板的力量中受益，同时提供信息，使经验丰富的程序员能够突破最先进的极限。为了实现这一点，我们决定将文本组织在_parts_中：

• [Part I] introduces the basic concepts underlying templates. It is written in a tutorial style.
• [Part II] presents the language details and is a handy reference to template-related constructs.
• [Part III] explains fundamental design and coding techniques supported by C++ templates. They range from near-trivial ideas to sophisticated idioms.

> •[第一部分]介绍了模板的基本概念。它是以教程风格编写的。
> •[第二部分]介绍了语言细节，是对模板相关结构的方便参考。
> •[第三部分]解释了 C++ 模板支持的基本设计和编码技术。它们的范围从近乎琐碎的想法到复杂的习语。

Each of these parts consists of several chapters. In addition, we provide a few appendixes that cover material not exclusively related to templates (e.g., an overview of overload resolution in C++). An additional appendix covers _concepts_, which is a fundamental extension to templates that has been included in the draft for a future standard (C++20, presumably).

> 每一部分都由几个章节组成。此外，我们还提供了一些附录，涵盖了与模板无关的材料(例如，C++ 中过载解决方案的概述)。另一个附录涵盖了_concepts_，这是对模板的基本扩展，该模板已包含在未来标准(可能是 C++20)的草案中。

The chapters of [Part I] are meant to be read in sequence. For example, [Chapter 3] builds on the material covered in [Chapter 2]. In the other parts, however, the connection between chapters is considerably looser. Cross references will help readers jump through the different topics.

> [第一部分]的章节应按顺序阅读。例如，[第 3 章]建立在[第 2 章]所涵盖的材料之上。然而，在其他部分，章节之间的联系要松散得多。交叉引用将帮助读者跳过不同的主题。

Last, we provide a rather complete index that encourages additional ways to read this book out of sequence.

> 最后，我们提供了一个相当完整的索引，鼓励以其他方式无序阅读这本书。

### How to Read This Book

If you are a C++ programmer who wants to learn or review the concepts of templates, carefully read [Part I], The Basics. Even if you're quite familiar with templates already, it may help to skim through this part quickly to familiarize yourself with the style and terminology that we use. This part also covers some of the logistical aspects of organizing your source code when it contains templates.

> 如果你是一个想学习或复习模板概念的 C++ 程序员，请仔细阅读[第一部分]，基础知识。即使您已经非常熟悉模板，快速浏览这一部分也可能有助于您熟悉我们使用的风格和术语。本部分还介绍了当源代码包含模板时组织源代码的一些后勤方面。

Depending on your preferred learning method, you may decide to absorb the many details of templates in [Part II], or instead you could read about practical coding techniques in [Part III] (and refer back to [Part II] for the more subtle language issues). The latter approach is probably particularly useful if you bought this book with concrete day-to-day challenges in mind.

> 根据您喜欢的学习方法，您可能会决定吸收[第二部分]中模板的许多细节，或者您可以在[第三部分]中阅读有关实用编码技术的内容(有关更微妙的语言问题，请参阅[第二章])。如果你买这本书时考虑到了具体的日常挑战，后一种方法可能特别有用。

The appendixes contain much useful information that is often referred to in the main text. We have also tried to make them interesting in their own right.

> 附录中包含了许多在正文中经常提及的有用信息。我们也试图让它们本身变得有趣。

In our experience, the best way to learn something new is to look at examples. Therefore, you'll find a lot of examples throughout the book. Some are just a few lines of code illustrating an abstract concept, whereas others are complete programs that provide a concrete application of the material. The latter kind of examples will be introduced by a C++ comment describing the file containing the program code. You can find these files at the Web site of this book at `http://www.tmplbook.com`.

> 根据我们的经验，学习新东西的最好方法是看例子。因此，你会在整本书中找到很多例子。有些只是说明抽象概念的几行代码，而另一些则是提供材料具体应用的完整程序。后一类示例将通过描述包含程序代码的文件的 C++ 注释来介绍。你可以在这本书的网站上找到这些文件，网址是 `http://www.tmplbook.com`.

### Some Remarks About Programming Style

C++ programmers use different programming styles, and so do we: The usual questions about where to put whitespace, delimiters (braces, parentheses), and so forth came up. We tried to be consistent in general, although we occasionally make concessions to the topic at hand. For example, in tutorial sections, we may prefer generous use of whitespace and concrete names to help visualize code, whereas in more advanced discussions, a more compact style could be more appropriate.

> C++ 程序员使用不同的编程风格，我们也是：出现了关于将空格、分隔符(大括号、圆括号)等放在哪里的常见问题。我们试图在总体上保持一致，尽管我们偶尔会对手头的话题做出让步。例如，在教程部分，我们可能更喜欢大量使用空格和具体名称来帮助可视化代码，而在更高级的讨论中，更紧凑的样式可能更合适。

We do want to draw your attention to one slightly uncommon decision regarding the declaration of types, parameters, and variables. Clearly, several styles are possible:

> 我们确实想提请您注意一个关于类型、参数和变量声明的稍微不常见的决定。显然，有几种样式是可能的：

```cpp
void foo [(const int] &x);
void foo [(const int]& x);
void foo [(int const] &x);
void foo [(int const]& x);
```

Although it is a bit less common, we decided to use the order `int const` rather than `const int` for "constant integer." We have two reasons for using this order. First, it provides for an easier answer to the question, "_What_ is constant?" It's always what is in front of the `const` qualifier. Indeed, although

> 虽然它不太常见，但我们决定使用顺序“int const”而不是“const int”来表示“常量整数”。使用此顺序有两个原因。首先，它为“_What_是常量？”这个问题提供了一个更简单的答案，它总是在“const”限定符前面。的确，尽管

```cpp
[const int] N = 100;
```

is equivalent to

```cpp
[int const] N = 100;
```

there is no equivalent form for

```cpp
int\* const bookmark;      // the pointer cannot change, but the value pointed to can
```

that would place the `const` qualifier before the pointer operator `*`. In this example, it is the pointer itself that is constant, not the `int` to which it points.

> 这将把“const”限定符放在指针运算符“*”之前。在本例中，指针本身是常量，而不是它所指向的“int”。

Our second reason has to do with a syntactical substitution principle that is very common when dealing with templates. Consider the following two type declarations using the `typedef` keyword:[1]

> 我们的第二个原因与语法替换原则有关，这在处理模板时非常常见。考虑使用“typedef”关键字的以下两个类型声明：[1]

```cpp
[typedef char]\* CHARS;\
typedef CHARS const CPTR;      // constant pointer to [char]s
```

or using the `using` keyword:

```cpp
using CHARS = [char]\*;\
using CPTR = CHARS const;      // constant pointer to [char]s
```

The meaning of the second declaration is preserved when we textually replace `CHARS` with what it stands for:

> 当我们将“CHARS”从文本上替换为它所代表的含义时，第二个声明的含义得以保留：

```cpp
[typedef char]\* const CPTR;      // constant pointer to [char]s
```

or:

```cpp
using CPTR = [char]\* const; // constant pointer to [char]s
```

However, if we write `const` _before_ the type it qualifies, this principle doesn't apply. Consider the alternative to our first two type definitions presented earlier:

> 然而，如果我们在它限定的类型之前写“const”_，则此原则不适用。考虑前面介绍的前两个类型定义的替代方案：

```cpp
[typedef char]\* CHARS;\
[typedef const] CHARS CPTR;      // constant pointer to [char]s
```

Textually replacing `CHARS` results in a type with a different meaning:

```cpp
[typedef const char]\* CPTR;      // pointer to constant [char*s
```

The same observation applies to the `volatile` specifier, of course.

Regarding whitespaces, we decided to put the space between the ampersand and the parameter name:

> 关于空白，我们决定在“与”和参数名称之间加一个空格：

```cpp
void foo [(int const]& x);
```

By doing this, we emphasize the separation between the parameter type and the parameter name. This is admittedly more confusing for declarations such as

> 通过这样做，我们强调了参数类型和参数名称之间的分离。诚然，这对于诸如

```cpp
[char]\* a, b;
```

where, according to the rules inherited from C, `a` is a pointer but `b` is an ordinary `char`. To avoid such confusion, we simply avoid declaring multiple entities in this way.

> 其中，根据从 C 继承的规则，“a”是指针，而“b”是普通的“char”。为了避免这种混淆，我们只是避免以这种方式声明多个实体。

This is primarily a book about language features. However, many techniques, features, and helper templates now appear in the C++ standard library. To connect these two, we therefore demonstrate template techniques by illustrating how they are used to implement certain library components, _and_ we use standard library utilities to build our own more complex examples. Hence, we use not only headers such as `<iostream>` and `<string>` (which contain templates but are not particularly relevant to define other templates) but also `<cstddef>`, `<utilities>`, `<functional>`, and `<type_traits>` (which do provide building blocks for more complex templates).

> 这主要是一本关于语言特征的书。但是，许多技术、特性和辅助模板现在出现在 C++ 标准库中。因此，为了将这两者联系起来，我们通过说明如何使用模板技术来实现某些库组件来演示模板技术，并使用标准库实用程序来构建我们自己的更复杂的示例。因此，我们不仅使用诸如“＜iostream＞”和“＜string＞”之类的头(它们包含模板，但与定义其他模板并不特别相关)，而且还使用“＜cstdef＞”、“＜utilities＞”、‘＜functional＞’和“＜type_traits＞”(它们确实为更复杂的模板提供了构建块)。

In addition, we provide a reference, [Appendix [D]], about the major template utilities provided by the C++ standard library, including a detailed description of all the standard type traits. These are commonly used at the core of sophisticated template programming

> 此外，我们还提供了一个关于 C++ 标准库提供的主要模板实用程序的参考文献[附录[D]]，包括所有标准类型特征的详细描述。这些通常用于复杂模板编程的核心

### The C++11, C++14, and C++17 Standards

The original C++ standard was published in 1998 and subsequently amended by a _technical corrigendum_ in 2003, which provided minor corrections and clarifications to the original standard. This "old C++ standard" is known as C++98 or C++03.

> 最初的 C++ 标准于 1998 年发布，随后于 2003 年通过技术勘误表进行了修订，对最初的标准进行了轻微的更正和澄清。这个“老 C++ 标准”被称为 C++98 或 C++03。

The C++11 standard was the first major revision of C++ driven by the ISO C++ standardization committee, bringing a wealth of new features to the language. A number of these new features interact with templates and are described in this book, including:

> C++11 标准是由 ISO C++ 标准化委员会推动的 C++ 的第一次重大修订，为该语言带来了丰富的新功能。本书中介绍了许多与模板交互的新功能，包括：

• Variadic templates
• Alias templates
• Move semantics, rvalue references, and perfect forwarding
• Standard type traits

C++14 and C++17 followed, both introducing some new language features, although the changes brought about by these standards were not quite as dramatic as those of C++11.[2] New features interacting with templates and described in this book include but are not limited to:

> 接下来是 C++14 和 C++17，它们都引入了一些新的语言功能，尽管这些标准带来的变化并不像 C++11 那样引人注目。[2]本书中描述的与模板交互的新功能包括但不限于：

• Variable templates (C++14)
• Generic Lambdas (C++14)
• Class template argument deduction (C++17)
• Compile-time `if` (C++17)
• Fold expressions (C++17)

We even describe _concepts_ (template interfaces), which are currently slated for inclusion in the forthcoming C++20 standard.

> 我们甚至描述了_concepts_(模板接口)，目前计划将其包含在即将发布的 C++20 标准中。

At the time of this writing, the C++11 and C++14 standards are broadly supported by the major compilers, and C++17 is largely supported also. Still, compilers differ greatly in their support of the different language features. Several will compile most of the code in this book, but a few compilers may not be able to handle some of our examples. However, we expect that this problem will soon be resolved as programmers everywhere demand standard support from their vendors.

> 在撰写本文时，C++11 和 C++14 标准得到了主要编译器的广泛支持，C++17 也得到了很大程度的支持。尽管如此，编译器在支持不同的语言特性方面还是有很大的不同。一些编译器将编译本书中的大部分代码，但少数编译器可能无法处理我们的一些示例。然而，我们预计这个问题很快就会得到解决，因为各地的程序员都要求他们的供应商提供标准支持。

Even so, the C++ programming language is likely to continue to evolve as time passes. The experts of the C++ community (regardless of whether they participate in the C++ Standardization Committee) are discussing various ways to improve the language, and already several candidate improvements affect templates. [Chapter [17]] presents some trends in this area.

> 即便如此，C++ 编程语言很可能会随着时间的推移而不断发展。C++ 社区的专家(无论他们是否参加 C++ 标准化委员会)正在讨论改进语言的各种方法，已经有几个候选改进影响了模板。[第[17]章]介绍了这一领域的一些趋势。

### Example Code and Additional Information

You can access all example programs and find more information about this book from its Web site, which has the following URL: [http://www.tmplbook.com](http://www.tmplbook.com)

> 您可以访问所有示例程序，并从其网站上找到有关这本书的更多信息，该网站的 URL 如下：[http://www.tmplbook.com](http://www.tmplbook.com)

### Feedback

We welcome your constructive input---both the negative and the positive. We worked very hard to bring you what we hope you'll find to be an excellent book. However, at some point we had to stop writing, reviewing, and tweaking so we could "release the product." You may therefore find errors, inconsistencies, and presentations that could be improved, or topics that are missing altogether. Your feedback gives us a chance to inform all readers through the book's Web site and to improve any subsequent editions.

> 我们欢迎你的建设性意见，无论是消极的还是积极的。我们非常努力地为您带来了我们希望您能发现的一本优秀的书。然而，在某个时候，我们不得不停止写作、审查和调整，以便“发布产品”。因此，你可能会发现错误、不一致和可以改进的演示，或者完全缺失的主题。您的反馈使我们有机会通过本书的网站通知所有读者，并改进后续版本。

The best way to reach us is by email. You will find the email address at the Web site of this book: [http://www.tmplbook.com](http://www.tmplbook.com)

> 联系我们的最佳方式是通过电子邮件。您可以在本书的网站上找到电子邮件地址：[http://www.tmplbook.com](http://www.tmplbook.com)

Please, be sure to check the book's Web site for the currently known errata before submitting reports. Many thanks.

> 在提交报告之前，请务必查看本书的网站，了解目前已知的勘误表。非常感谢。

^[1]^ Note that in C++, a type definition defines a "type alias" rather than a new type (see Section [[2.8]] on page [[38]]).

> ^[1]^ 请注意，在 C++ 中，类型定义定义的是“类型别名”，而不是新类型(请参见第[[38]]页第[[2.8]]节)。

For example:

```cpp
     >typedef int Length; *// define* Length *as an alias for* int\
    int i = 42;\
    Length l = 88;\
    i = l;        *// OK*\
    l = i;        *// OK*
```

^[2]^ The committee now aims at issuing a new standard roughly every 3 years. Clearly, that leaves less time for massive additions, but it brings the changes more quickly to the broader programming community. The development of larger features, then, spans time and might cover multiple standards.

> ^[2]^ 委员会现在的目标是大约每 3 年发布一次新标准。显然，这减少了大量添加的时间，但它更快地为更广泛的编程社区带来了变化。因此，更大功能的开发跨越时间，可能涵盖多个标准。

## Part I The Basics

This part introduces the general concepts and language features of C++ templates. It starts with a discussion of the general goals and concepts by showing examples of function templates and class templates. It continues with some additional fundamental template features such as nontype template parameters, variadic templates, the keyword `typename`, and member templates. Also it discusses how to deal with move semantics, how to declare parameters, and how to use generic code for compile-time programming. It ends with some general hints about terminology and regarding the use and application of templates in practice both as application programmer and author of generic libraries.

> 这部分介绍了 C++ 模板的一般概念和语言特点。它首先通过展示函数模板和类模板的示例来讨论一般目标和概念。它继续使用一些附加的基本模板功能，如非类型模板参数、可变模板、关键字“typename”和成员模板。此外，它还讨论了如何处理移动语义，如何声明参数，以及如何在编译时编程中使用泛型代码。最后，作为应用程序程序员和通用库的作者，它给出了一些关于术语以及模板在实践中的使用和应用的一般提示。

### Why Templates?

C++ requires us to declare variables, functions, and most other kinds of entities using specific types. However, a lot of code looks the same for different types. For example, the implementation of the algorithm _quicksort_ looks structurally the same for different data structures, such as arrays of `int` s or vectors of strings, as long as the contained types can be compared to each other.

> C++ 要求我们使用特定类型声明变量、函数和大多数其他类型的实体。然而，对于不同的类型，许多代码看起来是相同的。例如，对于不同的数据结构，例如“int”的数组或字符串的向量，只要所包含的类型可以相互比较，算法_quicksort_的实现在结构上看起来是相同的。

If your programming language doesn't support a special language feature for this kind of genericity, you only have bad alternatives:

> 如果你的编程语言不支持这种泛型的特殊语言功能，那么你只有糟糕的选择：

1. You can implement the same behavior again and again for each type that needs this behavior.
2. You can write general code for a common base type such as `Object` or `void*`.
3. You can use special preprocessors.

> 1. 对于每个需要此行为的类型，您可以一次又一次地实现相同的行为。
> 2. 您可以为通用基类型(如“Object”或“void*”)编写通用代码。

If you come from other languages, you probably have done some or all of this before. However, each of these approaches has its drawbacks:

> 如果你来自其他语言，你可能以前做过一些或所有这些。然而，每种方法都有其缺点：

1. If you implement a behavior again and again, you reinvent the wheel. You make the same mistakes, and you tend to avoid complicated but better algorithms because they lead to even more mistakes.

> 1.如果你一次又一次地实施一种行为，你就重新发明了轮子。你会犯同样的错误，你倾向于避免复杂但更好的算法，因为它们会导致更多的错误。

2. If you write general code for a common base class, you lose the benefit of type checking. In addition, classes may be required to be derived from special base classes, which makes it more difficult to maintain your code.

> 2.如果你为一个公共基类编写通用代码，你就失去了类型检查的好处。此外，类可能需要从特殊的基类派生，这使得维护代码变得更加困难。

3. If you use a special preprocessor, code is replaced by some "stupid text replacement mechanism" that has no idea of scope and types, which might result in strange semantic errors. Templates are a solution to this problem without these drawbacks. They are functions or classes that are written for one or more types not yet specified. When you use a template, you pass the types as arguments, explicitly or implicitly. Because templates are language features, you have full support of type checking and scope.

> 3.如果使用特殊的预处理器，代码会被一些不知道范围和类型的“愚蠢的文本替换机制”替换，这可能会导致奇怪的语义错误。模板是这个问题的解决方案，没有这些缺点。它们是为一个或多个尚未指定的类型编写的函数或类。使用模板时，可以显式或隐式地将类型作为参数传递。因为模板是语言特性，所以您完全支持类型检查和作用域。

In today's programs, templates are used a lot. For example, inside the C++ standard library almost all code is template code. The library provides sort algorithms to sort objects and values of a specified type, data structures (also called _container classes_) to manage elements of a specified type, strings for which the type of a character is parameterized, and so on. However, this is only the beginning. Templates also allow us to parameterize behavior, to optimize code, and to parameterize information. These applications are covered in later chapters. Let's first start with some simple templates.

> 在今天的程序中，模板被大量使用。例如，在 C++ 标准库中，几乎所有的代码都是模板代码。该库提供了排序算法来对指定类型的对象和值进行排序，提供了数据结构(也称为_container classes_)来管理指定类型的元素，提供了参数化字符类型的字符串等等。然而，这只是开始。模板还允许我们参数化行为、优化代码和参数化信息。这些应用程序将在后面的章节中介绍。让我们首先从一些简单的模板开始。

## Chapter 1

## Function Templates

This chapter introduces function templates. Function templates are functions that are parameterized so that they represent a family of functions.

> 本章介绍功能模板。函数模板是参数化的函数，以便它们表示一系列函数。

### 1.1 A First Look at Function Templates

Function templates provide a functional behavior that can be called for different types. In other words, a function template represents a family of functions. The representation looks a lot like an ordinary function, except that some elements of the function are left undetermined: These elements are parameterized. To illustrate, let's look at a simple example.

> 函数模板提供了可以为不同类型调用的函数行为。换句话说，函数模板表示一个函数族。这个表示看起来很像一个普通的函数，只是函数的一些元素是不确定的：这些元素是参数化的。为了进行说明，让我们看一个简单的例子。

#### 1.1.1 Defining the Template

The following is a function template that returns the maximum of two values:

> 以下是一个函数模板，它最多返回两个值：

```cpp
`basics/max1.hpp`

template<typename T>
T max (T a, T b)
{
    // if [b < a] then yield [a] else yield [b]
    return b < a ? a : b;
}
```

This template definition specifies a family of functions that return the maximum of two values, which are passed as function parameters `a` and `b`.[1] The type of these parameters is left open as _template parameter_ `T`. As seen in this example, template parameters must be announced with syntax of the following form:

> 此模板定义指定了一系列函数，这些函数最多返回两个值，这些值作为函数参数“a”和“b”传递。[1] 这些参数的类型保留为_模板参数_`T`。如本例所示，必须使用以下形式的语法来宣布模板参数：

```cpp
template< *comma-separated-list-of-parameters* >
```

In our example, the list of parameters is `typename T`. Note how the `<` and `>` tokens are used as brackets; we refer to these as _angle brackets_. The keyword `typename` introduces a _type parameter_. This is by far the most common kind of template parameter in C++ programs, but other parameters are possible, and we discuss them later (see [Chapter [3]]).

> 在我们的示例中，参数列表是“typename T”。请注意“＜”和“＞”标记是如何用作括号的；我们称之为括号。关键字“typename”引入了_type 参数_。这是迄今为止 C++ 程序中最常见的一种模板参数，但其他参数也是可能的，我们稍后会讨论(见[第[3]章])。

Here, the type parameter is `T`. You can use any identifier as a parameter name, but using `T` is the convention. The type parameter represents an arbitrary type that is determined by the caller when the caller calls the function. You can use any type (fundamental type, class, and so on) as long as it provides the operations that the template uses. In this case, type `T` has to support operator `<` because `a` and `b` are compared using this operator. Perhaps less obvious from the definition of `max()` is that values of type `T` must also be copyable in order to be returned.[2]

> 这里，类型参数是“T”。您可以使用任何标识符作为参数名称，但使用“T”是惯例。type 参数表示由调用方在调用函数时确定的任意类型。您可以使用任何类型(基本类型、类等)，只要它提供模板使用的操作即可。在这种情况下，类型“T”必须支持运算符“<”，因为“a”和“b”是使用此运算符进行比较的。从“max()”的定义中可能不太明显的是，类型为“T”的值也必须是可复制的才能返回。2.

For historical reasons, you can also use the keyword `class` instead of `typename` to define a type parameter. The keyword `typename` came relatively late in the evolution of the C++98 standard. Prior to that, the keyword `class` was the only way to introduce a type parameter, and this remains a valid way to do so. Hence, the template `max()` could be defined equivalently as follows:

> 由于历史原因，您也可以使用关键字“class”而不是“typename”来定义类型参数。关键字“typename”在 C++98 标准的发展过程中出现得相对较晚。在此之前，关键字“class”是引入类型参数的唯一方法，并且这仍然是一种有效的方法。因此，模板“max()”可以等效地定义如下：

```cpp
template<class T>
T max (T a, T b)
{
    return b < a ? a : b;\
}
```

Semantically there is no difference in this context. So, even if you use `class` here, _any_ type may be used for template arguments. However, because this use of `class` can be misleading (not only class types can be substituted for `T`), you should prefer the use of `typename` in this context. However, note that unlike class type declarations, the keyword `struct` cannot be used in place of `typename` when declaring type parameters.

> 从语义上讲，在这种情况下没有区别。因此，即使在这里使用“class”，_any_type 也可能用于模板参数。然而，由于“class”的使用可能会产生误导(不仅类类型可以代替“T”)，因此在这种情况下，您应该更喜欢使用“typename”。但是，请注意，与类类型声明不同，在声明类型参数时，不能使用关键字“struct”代替“typename”。

#### 1.1.2 Using the Template

The following program shows how to use the `max()` function template:

```cpp
`basics/max1.cpp`

#include "max1.hpp"\
#include <iostream>
#include <string>
int main()
{
    int i = 42;\
    std::cout << "max(7,i):      " << ::max(7,i) << '\n';\
\
    [double] f1 = 3.4; [double] f2 = -6.7;\
    std::cout << "max(f1,f2):    " << ::max(f1,f2) << '\n';\
\
    std::string s1 = "mathematics"; std::string s2 = "math";\
    std::cout << "max(s1,s2):    " << ::max(s1,s2) << '\n';\
}
```

Inside the program, `max()` is called three times: once for two `int` s, once for two `double` s, and once for two `std::string` s. Each time, the maximum is computed. As a result, the program has the following output:

> 在程序中，“max()”被调用三次：一次用于两个“int”，一次用于二个“double”，一次于二个“std:：string”。每次都计算最大值。因此，程序具有以下输出：

```cpp
max(7,i): 42\
max(f1,f2): 3.4\
max(s1,s2): mathematics
```

Note that each call of the `max()` template is qualified with `::`. This is to ensure that our `max()` template is found in the global namespace. There is also a `std::max()` template in the standard library, which under some circumstances may be called or may lead to ambiguity.[3]

> 请注意，对“max()”模板的每次调用都用“：：”限定。这是为了确保在全局命名空间中找到我们的“max()”模板。标准库中还有一个“std:：max()”模板，在某些情况下可能会被调用或导致歧义。3.

Templates aren't compiled into single entities that can handle any type. Instead, different entities are generated from the template for every type for which the template is used.[4] Thus, `max()` is compiled for each of these three types. For example, the first call of `max()`

> 模板不会编译成可以处理任何类型的单个实体。相反，对于使用模板的每种类型，都会从模板中生成不同的实体。[4] 因此，将为这三种类型中的每一种类型编译“max()”。例如，`max()的第一个调用`

```cpp
int i = 42;\
... max(7,i) ...
```

uses the function template with `int` as template parameter `T`. Thus, it has the semantics of calling the following code:

> 使用带有“int”的函数模板作为模板参数“T”。因此，它具有调用以下代码的语义：

```cpp
int max [(int] a, int b)
{
    return b < a ? a : b;\
}
```

The process of replacing template parameters by concrete types is called _instantiation_. It results in an _instance_ of a template.[5]

> 用具体类型替换模板参数的过程称为_instantiation_。它会产生一个模板的实例(_instance_)。5.

Note that the mere use of a function template can trigger such an instantiation process. There is no need for the programmer to request the instantiation separately.

> 请注意，仅仅使用函数模板就可以触发这样的实例化过程。程序员没有必要单独请求实例化。

Similarly, the other calls of `max()` instantiate the `max` template for `double` and `std::string` as if they were declared and implemented individually:

> 类似地，“max()”的其他调用实例化“double”和“std:：string”的“max”模板，就好像它们是单独声明和实现的一样：

```cpp
[double] max [(double], [double]);
std::string max (std::string, std::string);
```

Note also that `void` is a valid template argument provided the resulting code is valid. For example:

> 还要注意，“void”是一个有效的模板参数，前提是生成的代码是有效的。例如

```cpp
template<typename T>
T foo(T*)
{
}
\
[void]\* vp = [nullptr];\
foo(vp);                            // OK: deduces [void foo(void\*)]
```

#### 1.1.3 Two-Phase Translation

An attempt to instantiate a template for a type that doesn't support all the operations used within it will result in a compile-time error. For example:

> 试图为不支持其中使用的所有操作的类型实例化模板将导致编译时错误。例如

```cpp
std::complex<[float]> c1, c2;        // doesn't provide operator [<]\
...
::max(c1,c2);                     // ERROR at compile time
```

Thus, templates are "compiled" in two phases:

1. Without instantiation at _definition time_, the template code itself is checked for correctness ignoring the template parameters. This includes:

> 1.在_definition time_没有实例化的情况下，忽略模板参数来检查模板代码本身的正确性。这包括：

-- Syntax errors are discovered, such as missing semicolons.

-- Using unknown names (type names, function names, ...) that don't depend on template parameters are discovered.

> --发现使用不依赖于模板参数的未知名称(类型名称、函数名称…)。
> -- Static assertions that don't depend on template parameters are checked.

2. At _instantiation time_, the template code is checked (again) to ensure that all code is valid. That is, now especially, all parts that depend on template parameters are double-checked.

> 2.在实例化时间_，(再次)检查模板代码以确保所有代码都是有效的。也就是说，尤其是现在，所有依赖于模板参数的零件都要经过双重检查。

For example:

```cpp
template<typename T>
void foo(T t)
{
   undeclared();        // first-phase compile-time error if [undeclared()] unknown
   undeclared(t);        // second-phase compile-time error if [undeclared(T)] unknown
   [static_assert]([sizeof](int) > 10,          // always fails if [sizeof(int)<=10]\
                 "int too small");
   [static_assert]([sizeof](T) > 10,            //fails if instantiated for [T] with size [<=10]\
                 "T too small");
}
```

The fact that names are checked twice is called _two-phase lookup_ and discussed in detail in Section [[14.3.1]] on page [[249]].

> 名称被检查两次的事实被称为_twophase lookup_，并在第[[249]]页的第[[14.3.1]]节中进行了详细讨论。

Note that some compilers don't perform the full checks of the first phase.[6] So you might not see general problems until the template code is instantiated at least once.

> 请注意，有些编译器不会执行第一阶段的全部检查。[6] 因此，在模板代码至少实例化一次之前，您可能不会看到一般问题。

#### Compiling and Linking

Two-phase translation leads to an important problem in the handling of templates in practice: When a function template is used in a way that triggers its instantiation, a compiler will (at some point) need to see that template's definition. This breaks the usual compile and link distinction for ordinary functions, when the declaration of a function is sufficient to compile its use. Methods of handling this problem are discussed in [Chapter [9]]. For the moment, let's take the simplest approach: Implement each template inside a header file.

> 两阶段翻译在实践中导致了模板处理中的一个重要问题：当函数模板以触发其实例化的方式使用时，编译器将(在某个时候)需要查看该模板的定义。当函数的声明足以编译其使用时，这打破了普通函数通常的编译和链接区别。处理这个问题的方法在[第[9]章]中进行了讨论。目前，让我们采用最简单的方法：在头文件中实现每个模板。

### 1.2 Template Argument Deduction

When we call a function template such as `max()` for some arguments, the template parameters are determined by the arguments we pass. If we pass two `int` s to the parameter types `T`, the C++ compiler has to conclude that `T` must be `int`.

> 当我们为某些参数调用函数模板(如“max()”)时，模板参数由我们传递的参数决定。如果我们向参数类型“T”传递两个“int”，C++ 编译器必须得出结论，“T”必须是“int”。

However, `T` might only be "part" of the type. For example, if we declare `max()` to use constant references:

> 但是，“T”可能只是类型的“一部分”。例如，如果我们声明“max()”使用常量引用：

```cpp
template<typename T>
T max (T const& a, T const& b)
{
    return b < a ? a : b;\
}
```

and pass `int`, again `T` is deduced as `int`, because the function parameters match for `int const&`.

> 并传递“int”，再次将“T”推导为“int”。因为函数参数与“int const&”匹配。

##### Type Conversions During Type Deduction

Note that automatic type conversions are limited during type deduction:

• When declaring call parameters by reference, even trivial conversions do not apply to type deduction. Two arguments declared with the same template parameter `T` must match exactly.

> •通过引用声明调用参数时，即使是微不足道的转换也不适用于类型推导。用同一模板参数“T”声明的两个参数必须完全匹配。

• When declaring call parameters by value, only trivial conversions that _decay_ are supported: Qualifications with `const` or `volatile` are ignored, references convert to the referenced type, and raw arrays or functions convert to the corresponding pointer type. For two arguments declared with the same template parameter `T` the _decayed_ types must match.

> •当按值声明调用参数时，只支持_decay_的琐碎转换：忽略带有“const”或“volatile”的限定，引用转换为引用类型，原始数组或函数转换为相应的指针类型。对于用同一模板参数“T”声明的两个参数，_decayed_类型必须匹配。

For example:

```cpp
template<typename T>
T max (T a, T b);
...
[int const] c = 42;\
max(i, c);            // OK: [T] is deduced as int\
max(c, c);            // OK: [T] is deduced as int\
int& ir = i;\
max(i, ir);          // OK: [T] is deduced as int\
int arr[4];\
foo(&i, arr);        // OK: [T] is deduced as [inT
```

However, the following are errors:

```cpp
`max(4, 7.2);`        // ERROR: `T` can be deduced as `int` or [double]\
std::string s;\
foo("hello", s);    //ERROR: [T] can be deduced as [char const[6]] or [std::string]
```

There are three ways to handle such errors:

1. Cast the arguments so that they both match:

```cpp
`max(static_cast<double>(4), 7.2);`        // OK
```

2. Specify (or qualify) explicitly the type of `T` to prevent the compiler from attempting type deduction:

> 2.显式指定(或限定)“T”的类型，以防止编译器尝试进行类型推导：

```cpp
`max<double>(4, 7.2);`                   // OK
```

3. Specify that the parameters may have different types.

Section [[1.3]] on page [[9]] will elaborate on these options. Section [[7.2]] on page [[108]] and [Chapter [15]] will discuss the rules for type conversions during type deduction in detail.

> 第[[9]页第[[1.3]]节将详细阐述这些备选方案。第[[108]]页第[[7.2]]节和第[15]章将详细讨论类型推导过程中的类型转换规则。

##### Type Deduction for Default Arguments

Note also that type deduction does not work for default call arguments. For example:

> 还要注意，类型推导不适用于默认的调用参数。例如

```cpp
template<typename T>
void f(T = "");
...
```

```cpp
f(1);        // OK: deduced [T] to be int, so that it calls [f<int>(1)]\
f();         // ERROR: cannot deduce [T]
```

To support this case, you also have to declare a default argument for the template parameter, which will be discussed in Section [[1.4]] on page [[13]]:

> 为了支持这种情况，您还必须为模板参数声明一个默认参数，这将在第[[13]]页的第[[1.4]]节中进行讨论：

```cpp
template<typename T = std::string>
void f(T = "");
...
f();        // OK
```

### 1.3 Multiple Template Parameters

As we have seen so far, function templates have two distinct sets of parameters:

> 到目前为止，我们已经看到，函数模板有两组不同的参数：

1. _Template parameters_, which are declared in angle brackets before the function template name:

> 1._Template 参数，在函数模板名称前的尖括号中声明：

```cpp
template<typename T>        // [T] is template parameter
```

2. _Call parameters_, which are declared in parentheses after the function template name:

> 2._Call 参数_，在函数模板名称后面的括号中声明：

```cpp
T max (T a, T b)            // [a] and [b] are call parameters
```

You may have as many template parameters as you like. For example, you could define the `max()` template for call parameters of two potentially different types:

> 您可以拥有任意数量的模板参数。例如，您可以为两种可能不同类型的调用参数定义“max()”模板：

```cpp
template<typename T1, typename T2>
T1 max (T1 a, T2 b)
{
    return b < a ? a : b; }
...
auto m = ::max(4, 7.2);        // OK, but type of first argument defines return type
```

It may appear desirable to be able to pass parameters of different types to the `max()` template, but, as this example shows, it raises a problem. If you use one of the parameter types as return type, the argument for the other parameter might get converted to this type, regardless of the caller's intention. Thus, the return type depends on the call argument order. The maximum of 66.66 and 42 will be the `double` 66.66, while the maximum of 42 and 66.66 will be the `int` 66.

> 可能希望能够将不同类型的参数传递到“max()”模板，但正如本例所示，这会带来一个问题。如果使用其中一个参数类型作为返回类型，则无论调用方的意图如何，另一个参数的参数都可能转换为此类型。因此，返回类型取决于调用参数的顺序。最大值 66.66 和 42 将是“双”66.66，而最大值 42 和 66.66 将是“int”66。

C++ provides different ways to deal with this problem:

• Introduce a third template parameter for the return type.
• Let the compiler find out the return type.

• Declare the return type to be the "common type" of the two parameter types.

> •将返回类型声明为两种参数类型中的“公共类型”。

All these options are discussed next.

#### 1.3.1 Template Parameters for Return Types

Our earlier discussion showed that _template argument deduction_ allows us to call function templates with syntax identical to that of calling an ordinary function: We do not have to explicitly specify the types corresponding to the template parameters.

> 我们之前的讨论表明，_template 参数推导允许我们调用语法与调用普通函数相同的函数模板：我们不必显式指定与模板参数对应的类型。

We also mentioned, however, that we can specify the types to use for the template parameters explicitly:

> 但是，我们还提到，我们可以明确指定用于模板参数的类型：

```cpp
template<typename T>
T max (T a, T b);
...
::max<[double]>(4, 7.2);        // instantiate [T] as [double]
```

In cases when there is no connection between template and call parameters and when template parameters cannot be determined, you must specify the template argument explicitly with the call. For example, you can introduce a third template argument type to define the return type of a function template:

> 如果模板和调用参数之间没有连接，并且无法确定模板参数，则必须在调用中显式指定模板参数。例如，可以引入第三个模板参数类型来定义函数模板的返回类型：

```cpp
template<typename T1, typename T2, typename RT>
RT max (T1 a, T2 b);
```

However, template argument deduction does not take return types into account,[7] and `RT` does not appear in the types of the function call parameters. Therefore, `RT` cannot be deduced.[8]

> 然而，模板参数推导不考虑返回类型，[7]和“RT”不出现在函数调用参数的类型中。因此，不能推导出“RT”。8.

As a consequence, you have to specify the template argument list explicitly. For example:

> 因此，必须显式指定模板参数列表。例如

```cpp
template<typename T1, typename T2, typename RT>
RT max (T1 a, T2 b);
...
::max<int,[double],[double]>(4, 7.2);        // OK, but tedious
```

So far, we have looked at cases in which either all or none of the function template arguments were mentioned explicitly. Another approach is to specify only the first arguments explicitly and to allow the deduction process to derive the rest. In general, you must specify all the argument types up to the last argument type that cannot be determined implicitly. Thus, if you change the order of the template parameters in our example, the caller needs to specify only the return type:

> 到目前为止，我们已经研究了明确提及所有或不提及函数模板参数的情况。另一种方法是只显式指定第一个参数，并允许推导过程派生其余参数。通常，您必须指定所有参数类型，直到不能隐式确定的最后一个参数类型。因此，如果您在我们的示例中更改模板参数的顺序，那么调用者只需要指定返回类型：

```cpp
template<typename RT, typename T1, typename T2>
RT max (T1 a, T2 b);
...
::max<[double]>(4, 7.2)        //OK: return type is [double], [T1] and [T2] are deduced
```

In this example, the call to `max<double>` explicitly sets `RT` to `double`, but the parameters `T1` and `T2` are deduced to be `int` and `double` from the arguments.

> 在这个例子中，对“max＜double＞”的调用显式地将“RT”设置为“double”，但参数“T1”和“T2”从变元推导为“int”和“double’。

Note that these modified versions of `max()` don't lead to significant advantages. For the one-parameter version you can already specify the parameter (and return) type if two arguments of a different type are passed. Thus, it's a good idea to keep it simple and use the one-parameter version of `max()` (as we do in the following sections when discussing other template issues).

> 请注意，“max()”的这些修改版本并没有带来显著的优势。对于单参数版本，如果传递了两个不同类型的参数，则已经可以指定参数(和返回)类型。因此，保持简单并使用单参数版本的“max()”是一个好主意(正如我们在下面讨论其他模板问题时所做的那样)。

See [Chapter [15]] for details of the deduction process.

#### 1.3.2 Deducing the Return Type

If a return type depends on template parameters, the simplest and best approach to deduce the return type is to let the compiler find out. Since C++14, this is possible by simply not declaring any return type (you still have to declare the return type to be `auto`):

> 如果返回类型依赖于模板参数，那么推导返回类型的最简单、最好的方法是让编译器找出。由于 C++14，这可以通过简单地不声明任何返回类型来实现(您仍然需要将返回类型声明为“auto”)：

```cpp
`basics/maxauto.hpp`

template<typename T1, typename T2>
auto max (T1 a, T2 b)
{
  return b < a ? a : b;\
}
```

In fact, the use of `auto` for the return type without a corresponding _trailing return type_ (which would be introduced with a `->` at the end) indicates that the actual return type must be deduced from the return statements in the function body. Of course, deducing the return type from the function body has to be possible. Therefore, the code must be available and multiple return statements have to match.

> 事实上，对返回类型使用“auto”而没有相应的_trailing 返回类型_(将在末尾引入“->”)表明实际的返回类型必须从函数体中的返回语句中推导出来。当然，从函数体推导返回类型必须是可能的。因此，代码必须可用，并且多个返回语句必须匹配。

Before C++14, it is only possible to let the compiler determine the return type by more or less making the implementation of the function part of its declaration. In C++11 we can benefit from the fact that the _trailing return type_ syntax allows us to use the call parameters. That is, we can _declare_ that the return type is derived from what `operator?:` yields:

> 在 C++14 之前，只有通过或多或少地将函数的实现作为其声明的一部分，才能让编译器确定返回类型。在 C++11 中，_trailing 返回 type_语法允许我们使用调用参数，这一事实使我们受益匪浅。也就是说，我们可以声明返回类型是从什么 `operator？：` 派生的产量：

```cpp
`basics/maxdecltype.hpp`

template<typename T1, typename T2>
auto max (T1 a, T2 b) -> decltype(b<a?a:b)
{
  return b < a ? a : b;\
}
```

Here, the resulting type is determined by the rules for operator `?:`, which are fairly elaborate but generally produce an intuitively expected result (e.g., if `a` and `b` have different arithmetic types, a common arithmetic type is found for the result).

> 这里，结果类型由运算符“？：”的规则确定，它们相当复杂，但通常会产生直观的预期结果(例如，如果“a”和“b”具有不同的算术类型，则会为结果找到一种常见的算术类型)。

Note that

```cpp
template<typename T1, typename T2>
auto max (T1 a, T2 b) -> decltype(b<a?a:b);
```

is a _declaration_, so that the compiler uses the rules of `operator?:` called for parameters `a` and `b` to find out the return type of `max()` at compile time. The implementation does not necessarily have to match. In fact, using `true` as the condition for `operator?:` in the declaration is enough:

> 是_declaration_，因此编译器使用 `operator？：` 的规则调用了参数“a”和“b”，以在编译时找出“max()”的返回类型。实现不一定要匹配。事实上，使用“true”作为“operator？：”的条件在声明中就足够了：

```cpp
template<typename T1, typename T2>
auto max (T1 a, T2 b) -> decltype[(true]?a:b);
```

However, in any case this definition has a significant drawback: It might happen that the return type is a reference type, because under some conditions `T` might be a reference. For this reason you should return the type _decayed_ from `T`, which looks as follows:

> 然而，在任何情况下，这个定义都有一个显著的缺点：返回类型可能是引用类型，因为在某些条件下“T”可能是引用。因此，您应该从“T”返回类型_decayed_，如下所示：

```cpp
`basics/maxdecltypedecay.hpp`

#include <type_traits>
template<typename T1, typename T2>
auto max (T1 a, T2 b) -> typename std::decay[<decltype][(true]?a:b)>::type\
 b < a ? a : b;\
}
```

Here, the type trait `std::decay<>` is used, which returns the resulting type in a member `type`. It is defined by the standard library in `<type_trait>` (see Section [[D.5]] on page [[732]]). Because the member `type` is a type, you have to qualify the expression with `typename` to access it (see Section [[5.1]] on page [[67]]).

> 这里使用了类型特性“std:：decay＜＞”，它返回成员“type”中的结果类型。它由 `<type_trait>` 中的标准库定义(见第[[732]]页第[[D.5]节)。因为成员“type”是一个类型，所以必须用“typename”限定表达式才能访问它(请参见第[[67]]页的第[[5.1]]节)。

Note that an initialization of type `auto` always decays. This also applies to return values when the return type is just `auto`. `auto` as a return type behaves just as in the following code, where `a` is declared by the decayed type of `i`, `int`:

> 请注意，“auto”类型的初始化总是会衰减。当返回类型仅为“auto”时，这也适用于返回值 `auto 作为返回类型的行为与以下代码中的行为相同，其中“a”由衰退类型“i”、“int”声明：

```cpp
int i = 42;\
[int const]& ir = i;        // [ir] refers to
[i] auto a = ir;            // [a] is declared as new object of type int
```

#### 1.3.3 Return Type as Common Type

Since C++11, the C++ standard library provides a means to specify choosing "the more general type." `std::common_type<>::type` yields the "common type" of two (or more) different types passed as template arguments. For example:

> 自 C++11 以来，C++ 标准库提供了一种指定选择“更通用的类型”的方法。`std:：common_type<>：：type` 产生作为模板参数传递的两个(或多个)不同类型的“公共类型”。例如

```cpp
`basics/maxcommon.hpp`

#include <type_traits>
template<typename T1, typename T2>
std::common_type_t<T1,T2> max (T1 a, T2 b)
{
  return b < a ? a : b;\
}
```

Again, `std::common_type` is a _type trait_, defined in `<type_traits>`, which yields a structure having a `type` member for the resulting type. Thus, its core usage is as follows:

> 同样，“std:：common_type”是在“＜type_traits＞”中定义的_type-trait_，它为生成的类型生成具有“type”成员的结构。因此，其核心用途如下：

```cpp
typename std::common_type<T1,T2>::type        //since C++11
```

However, since C++14 you can simplify the usage of traits like this by appending `_t` to the trait name and skipping `typename` and `::type` (see Section [[2.8]] on page [[40]] for details), so that the return type definition simply becomes:

> 然而，由于 C++14，您可以通过在特性名称后附加“_t”并跳过“typename”和“：：type”来简化像这样的特性的使用(有关详细信息，请参阅第[[40]]页的第[[2.8]]节)，因此返回类型定义简单地变为：

```cpp
std::common_type_t<T1,T2>                    // equivalent since C++14
```

The way `std::common_type<>` is implemented uses some tricky template programming, which is discussed in Section [[26.5.2]] on page [[622]]. Internally, it chooses the resulting type according to the language rules of operator `?:` or specializations for specific types. Thus, both `::max(4, 7.2)` and `::max(7.2, 4)` yield the same value 7.2 of type `double`. Note that `std::common_type<>` also decays. See Section [[D.5]] on page [[732]] for details.

> “std:：common_type<>'的实现方式使用了一些棘手的模板编程，这在第[[622]]页的第[[26.5.2]]节中进行了讨论。在内部，它根据运算符“？：”的语言规则选择结果类型或特定类型的专业化。因此，“：：max(4，7.2)”和“：：最大(7.2，4)”都产生了类型为“double”的相同值 7.2。请注意，`std:：common_type<>` 也会衰减。详见第[[732]]页第[[D.5]节。

### 1.4 Default Template Arguments

You can also define default values for template parameters. These values are called _default template arguments_ and can be used with any kind of template.[9] They may even refer to previous template parameters.

> 还可以定义模板参数的默认值。这些值被称为_default 模板参数_，可以与任何类型的模板一起使用。[9] 它们甚至可以引用以前的模板参数。

For example, if you want to combine the approaches to define the return type with the ability to have multiple parameter types (as discussed in the section before), you can introduce a template parameter `RT` for the return type with the common type of the two arguments as default. Again, we have multiple options:

> 例如，如果您想将定义返回类型的方法与具有多个参数类型的能力相结合(如前一节所述)，则可以为返回类型引入模板参数“RT”，默认情况下使用两个参数的公共类型。同样，我们有多种选择：

1. We can use `operator?:` directly. However, because we have to apply `operator?:` before the call parameters `a` and `b` are declared, we can only use their types:

> 1.我们可以使用 `operator？：` 直接地但是，因为我们必须应用“运算符？：”在声明调用参数“a”和“b”之前，我们只能使用它们的类型：

```cpp
`basics/maxdefault1.hpp`

#include <type_traits>
template<typename T1, typename T2,\
         typename RT = std::decay_t[<decltype][(true] ? T1() : T2())>>
RT max (T1 a, T2 b)
{
  return b < a ? a : b;\
}
```

Note again the usage of `std::decay_t<>` to ensure that no reference can be returned.[10]

> 再次注意 `std:：decay_t<>` 的用法，以确保不能返回任何引用。[10]

Note also that this implementation requires that we are able to call default constructors for the passed types. There is another solution, using `std::declval`, which, however, makes the declaration even more complicated. See Section [[11.2.3]] on page [[166]] for an example.

> 还要注意，此实现要求我们能够为传递的类型调用默认构造函数。还有另一种解决方案，使用“std:：declval”，但这会使声明更加复杂。有关示例，请参见第[[166]]页第[[11.2.3]]节。

2. We can also use the `std::common_type<>` type trait to specify the default value for the return type:

> 2.我们还可以使用 `std:：common_type<>` 类型特征来指定返回类型的默认值：

```cpp
`basics/maxdefault3.hpp`

#include <type_traits>
\
template<typename T1, typename T2,\
         typename RT = std::common_type_t<T1,T2>>
RT max (T1 a, T2 b)
{
  return b < a ? a : b;\
}
```

Again, note that `std::common_type<>` decays so that the return value can't become a reference. In all cases, as a caller, you can now use the default value for the return type:

> 再次注意，`std:：common_type<>` 衰减，因此返回值不能成为引用。在所有情况下，作为调用者，您现在都可以使用返回类型的默认值：

```cpp
auto a = ::max(4, 7.2);
```

or specify the return type after all other argument types explicitly:

```cpp
auto b = ::max[<double][,int][,long double]>(7.2, 4);
```

However, again we have the problem that we have to specify three types to be able to specify the return type only. Instead, we would need the ability to have the return type as the first template parameter, while still being able to deduce it from the argument types. In principle, it is possible to have default arguments for leading function template parameters even if parameters without default arguments follow:

> 然而，我们再次遇到的问题是，我们必须指定三种类型才能仅指定返回类型。相反，我们需要能够将返回类型作为第一个模板参数，同时仍然能够从参数类型中推导出它。原则上，即使没有默认参数的参数如下所示，也可以为前导函数模板参数设置默认参数：

```cpp
template<typename RT = [long], typename T1, typename T2>
RT max (T1 a, T2 b)
{
  return b < a ? a : b;\
}
```

With this definition, for example, you can call:

```cpp
int i; [long] l;\
...
max(i, l);              // returns [long] (default argument of template parameter for return type)
max<int>(4, 42);        // returns int as explicitly requested
```

However, this approach only makes sense, if there is a "natural" default for a template parameter. Here, we need the default argument for the template parameter to depend from previous template parameters. In principle, this is possible as we discuss in Section [[26.5.1]] on page [[621]], but the technique depends on type traits and complicates the definition.

> 然而，只有当模板参数存在“自然”默认值时，这种方法才有意义。这里，我们需要模板参数的默认参数来依赖于以前的模板参数。原则上，正如我们在第[[621]]页第[[26.5.1]]节中所讨论的那样，这是可能的，但该技术取决于类型特征，并使定义复杂化。

For all these reasons, the best and easiest solution is to let the compiler deduce the return type as proposed in Section [[1.3.2]] on page [[11]].

> 出于所有这些原因，最好和最简单的解决方案是让编译器推导出第[[11]]页第[[1.3.2]]节中提出的返回类型。

### 1.5 Overloading Function Templates

Like ordinary functions, function templates can be overloaded. That is, you can have different function definitions with the same function name so that when that name is used in a function call, a C++ compiler must decide which one of the various candidates to call. The rules for this decision may become rather complicated, even without templates. In this section we discuss overloading when templates are involved. If you are not familiar with the basic rules of overloading without templates, please look at [Appendix [C]], where we provide a reasonably detailed survey of the overload resolution rules.

> 与普通函数一样，函数模板也可以重载。也就是说，可以使用相同的函数名来定义不同的函数，这样当在函数调用中使用该名称时，C++ 编译器必须决定调用各种候选函数中的哪一个。即使没有模板，这个决策的规则也可能变得相当复杂。在本节中，我们将讨论涉及模板时的重载。如果您不熟悉无模板重载的基本规则，请参阅[附录[C]，我们在其中提供了对重载解决规则的合理详细的调查。

The following short program illustrates overloading a function template:

```cpp
`basics/max2.cpp`

// maximum of two int values:
int max [(int] a,\
int b)
{
  return b < a ? a : b;\
}
// maximum of two values of any type:
template<typename T>
T max (T a, T b)
{
  return b < a ? a : b;\
}
\
int main()
{
  ::max(7, 42);                // calls the nontemplate for two ints
  ::max(7.0, 42.0);            // calls [max<double>] (by argument deduction)
  ::max(['a'], ['b']);              //calls [max<char>] (by argument deduction)
  ::max<>(7, 42);              // calls [max<int>] (by argument deduction)
  ::max<[double]>(7, 42);        // calls [max<double>] (no argument deduction)
  ::max(['a'], 42.7);             //calls the nontemplate for two ints
}
```

As this example shows, a nontemplate function can coexist with a function template that has the same name and can be instantiated with the same type. All other factors being equal, the overload resolution process prefers the nontemplate over one generated from the template. The first call falls under this rule:

> 如本例所示，非模板函数可以与具有相同名称且可以使用相同类型实例化的函数模板共存。在所有其他因素相同的情况下，重载解析过程更喜欢非模板，而不是从模板生成的模板。第一个调用属于此规则：

```cpp
::max(7, 42);        // both int values match the nontemplate function perfectly
```

If the template can generate a function with a better match, however, then the template is selected. This is demonstrated by the second and third calls of `max()`:

> 但是，如果模板可以生成匹配度更好的函数，则会选择该模板。这可以通过“max()”的第二次和第三次调用来证明：

```cpp
::max(7.0, 42.0);        // calls the [max<double>] (by argument deduction)
::max(['a'], ['b']);          //calls the [max<char>] (by argument deduction)
```

Here, the template is a better match because no conversion from `double` or `char` to `int` is required (see Section [[C.2]] on page [[682]] for the rules of overload resolution).

> 这里，模板是一个更好的匹配，因为不需要从“double”或“char”转换为“int”(过载解决规则见第[[682]]页第[[C.2]]节)。

It is also possible to specify explicitly an empty template argument list. This syntax indicates that only templates may resolve a call, but all the template parameters should be deduced from the call arguments:

> 也可以显式指定一个空的模板参数列表。此语法表示只有模板可以解析调用，但所有模板参数都应该从调用参数中推导出来：

```cpp
::max<>(7, 42);        // calls [max<int>] (by argument deduction)
```

Because automatic type conversion is not considered for deduced template parameters but is considered for ordinary function parameters, the last call uses the nontemplate function (while `’a’` and `42.7` both are converted to `int`):

> 由于推导的模板参数不考虑自动类型转换，而是考虑普通函数参数，因此最后一个调用使用非模板函数(而“'a”和“42.7'都转换为“int”)：

```cpp
::max(['a'], 42.7);        //only the nontemplate function allows nontrivial conversions
```

An interesting example would be to overload the maximum template to be able to explicitly specify the return type only:

> 一个有趣的例子是重载最大模板，使其只能显式指定返回类型：

```cpp
`basics/maxdefault4.hpp`

template<typename T1, typename T2>
auto max (T1 a, T2 b)
{
  return b < a ? a : b;\
}
template<typename RT, typename T1, typename T2>
RT max (T1 a, T2 b)
{
  return b < a ? a : b;\
}
```

Now, we can call `max()`, for example, as follows:

```cpp
auto a = ::max(4, 7.2);                     // uses first template
auto b = ::max[<long double]>(7.2, 4);        // uses second template

However, when calling:

auto c = ::max[<int]>(4, 7.2);                // ERROR: both function templates match
```

both templates match, which causes the overload resolution process normally to prefer none and result in an ambiguity error. Thus, when overloading function templates, you should ensure that only one of them matches for any call.

> 两个模板匹配，这导致过载解决过程通常不选择任何模板，并导致歧义错误。因此，当重载函数模板时，应该确保其中只有一个模板与任何调用匹配。

A useful example would be to overload the maximum template for pointers and ordinary C-strings:

> 一个有用的例子是重载指针和普通 C 字符串的最大模板：

```cpp
`basics/max3val.cpp`

\
#include   <cstring>
#include   <string>
\
[// maximum of two values of any type:]\
[template<typename]    T>
T max (T a, T b)
{
   [return]      b < a ? a : b;\
}
\
[// maximum of two pointers:]\
[template<typename]    T>
T* max (T* a, T* b)
{
   [return]       \*b < \*a   ? a : b;\
}
\
// maximum of two C-strings:\
[char const]\* max ([char   const]\* a,   [char const]\* b)
{
   [return]       std::strcmp(b,a) < 0   ? a : b;\
}
\
int   main ()
{
   int a = 7;\
   int b = 42;\
   auto m1 = ::max(a,b);         [// max() *for two values of type int
\
   std::string s1 =   "hey"; \"\
   std::string s2 =   "you"; \"\
   auto m2 = ::max(s1,s2);       [// max() *for two values of type std::string
\
  int* p1 = &b;\
  int* p2 = &a;\
   auto m3 = ::max(p1,p2);       [// max() *for two pointers
\
   [char const]\* x =  [hello"; \"\
   [char const]\* y =  "world"; \"\
   auto m4 = ::max(x,y);         [// max() *for two C-strings
}
```

Note that in all overloads of `max()` we pass the arguments by value. In general, it is a good idea not to change more than necessary when overloading function templates. You should limit your changes to the number of parameters or to specifying template parameters explicitly. Otherwise, unexpected effects may happen. For example, if you implement your `max()` template to pass the arguments by reference and overload it for two C-strings passed by value, you can't use the three-argument version to compute the maximum of three C-strings:

> 请注意，在“max()”的所有重载中，我们按值传递参数。一般来说，在重载函数模板时，最好不要进行过多的更改。您应该将更改限制在参数数量或显式指定模板参数。否则，可能会产生意想不到的影响。例如，如果您实现“max()”模板以通过引用传递参数，并为通过值传递的两个 C 字符串重载它，则不能使用三参数版本来计算最多三个 C 字符串：

```cpp
`basics/max3ref.cpp`

#include <cstring>
\
// maximum of two values of any type (call-by-reference)
template<typename\
T> T const& max (T const& a, T const& b)
{
  return b < a ? a : b;\
}
// maximum of two C-strings (call-by-value)
[char const]\* max [(char const]\* a, [char const]\* b)
{
  return std::strcmp(b,a) < 0 ? a : b;\
}
\
// maximum of three values of any type (call-by-reference)
template<typename T>
`T const& max (T const& a, T const& b, T const& c)  `max(a,b)` uses call-by-value
`}`\
int main ()
{
    auto m1 = ::max(7, 42, 68);        // OK
    [char const]\* s1 = "frederic";\
    [char const]\* s2 = "anica";\
    [char const]\* s3 = "lucas";\
    auto m2 = ::max(s1, s2, s3);       //run-time ERROR
}
```

The problem is that if you call `max()` for three C-strings, the statement

> 问题是，如果对三个 C 字符串调用“max()”，则语句

```cpp
return max (max(a,b), c);
```

becomes a run-time error because for C-strings, `max(a,b)` creates a new, temporary local value that is returned by reference, but that temporary value expires as soon as the return statement is complete, leaving `main()` with a dangling reference. Unfortunately, the error is quite subtle and may not manifest itself in all cases.[11]

> 成为运行时错误，因为对于 C 字符串，“max(a，b)”创建了一个新的临时本地值，该值通过引用返回，但该临时值在返回语句完成后立即过期，留下了一个悬空引用“main()”。不幸的是，这个错误非常微妙，可能不会在所有情况下都表现出来。[11]

Note, in contrast, that the first call to `max()` in `main()` doesn't suffer from the same issue. There temporaries are created for the arguments (7, 42, and 68), but those temporaries are created in `main()` where they persist until the statement is done.

> 相反，请注意，在“main()”中对“max()”的第一次调用不会遇到同样的问题。为参数(7、42 和 68)创建了临时变量，但这些临时变量是在“main()”中创建的，它们在语句完成之前一直存在。

This is only one example of code that might behave differently than expected as a result of detailed overload resolution rules. In addition, ensure that all overloaded versions of a function are declared before the function is called. This is because the fact that not all overloaded functions are visible when a corresponding function call is made may matter. For example, defining a three-argument version of `max()` without having seen the declaration of a special two-argument version of `max()` for `int` s causes the two-argument template to be used by the three-argument version:

> 这只是代码的一个例子，由于详细的重载解决规则，代码的行为可能与预期不同。此外，请确保在调用函数之前声明函数的所有重载版本。这是因为在进行相应的函数调用时，并非所有重载函数都可见这一事实可能很重要。例如，在没有看到“int”的“max()”的特殊双参数版本的声明的情况下定义“max(

```cpp

*basics/max4.cpp*

#include <iostream>
\
// maximum of two values of any type:
template<typename T>
T max (T a, T b)
{
  std::cout << "max<T>() \\n";\
  return b < a ? a : b;\
}
\
// maximum of three values of any type:
template<typename T>
T max (T a, T b, T c)
{
  return max (max(a,b), c);          // uses the template version even for ints
}                                    //because the following declaration comes
                                   // too late:
\
// maximum of two int values:
int max [(int] a,\
int b)
{
  std::cout << "max(int,int) \\n";\
  return b < a ? a : b;\
}
\
int main()
{
  ::max(47,11,33);        // OOPS: uses [max<T>()] instead of [max(int,int)]\
}
```

We discuss details in Section [[13.2]] on page [[217]].

### 1.6 But, Shouldn't We ...?

Probably, even these simple function template examples might raise further questions. Three questions are probably so common that we should discuss them here briefly.

> 也许，即使是这些简单的函数模板示例也可能引发进一步的问题。三个问题可能很常见，我们应该在这里简要讨论一下。

#### 1.6.1 Pass by Value or by Reference?

You might wonder, why we in general declare the functions to pass the arguments by value instead of using references. In general, passing by reference is recommended for types other than cheap simple types (such as fundamental types or `std::string_view`), because no unnecessary copies are created.

> 您可能会想，为什么我们通常声明函数以按值传递参数，而不是使用引用。通常，建议对廉价简单类型以外的类型(如基本类型或“std:：string_view”)进行引用传递，因为不会创建不必要的副本。

However, for a couple of reasons, passing by value in general is often better:

> 然而，出于以下几个原因，传递价值通常更好些：

• The syntax is simple.
• Compilers optimize better.
• Move semantics often makes copies cheap.
• And sometimes there is no copy or move at all.

In addition, for templates, specific aspects come into play:

• A template might be used for both simple and complex types, so choosing the approach for complex types might be counter-productive for simple types.

> •模板可能用于简单类型和复杂类型，因此选择复杂类型的方法可能会对简单类型产生反作用。

• As a caller you can often still decide to pass arguments by reference, using `std::ref()` and `std::cref()` (see Section [[7.3]] on page [[112]]).

> •作为调用者，您通常仍然可以决定通过引用传递参数，使用“std:：ref()”和“std：：cref()”(请参见第[[112]]页的第[[7.3]]节)。

• Although passing string literals or raw arrays always can become a problem, passing them by reference often is considered to become the bigger problem. All this will be discussed in detail in [Chapter [7]]. For the moment inside the book we will usually pass arguments by value unless some functionality is only possible when using references.

> •尽管传递字符串文字或原始数组总是会成为一个问题，但通过引用传递它们通常被认为是一个更大的问题。所有这些将在[第[7]章]中详细讨论。目前，在书中，我们通常会按值传递参数，除非某些功能只有在使用引用时才可能实现。

#### 1.6.2 Why Not **inline**?

In general, function templates don't have to be declared with `inline`. Unlike ordinary noninline functions, we can define noninline function templates in a header file and include this header file in multiple translation units.

> 通常，函数模板不必用“inline”来声明。与普通的非线性函数不同，我们可以在头文件中定义非线性函数模板，并将该头文件包含在多个翻译单元中。

The only exception to this rule are full specializations of templates for specific types, so that the resulting code is no longer generic (all template parameters are defined). See Section [[9.2]] on page [[140]] for more details.

> 该规则的唯一例外是特定类型的模板的完全专业化，因此生成的代码不再是通用的(所有模板参数都已定义)。详见第[[140]]页第[[9.2]]节。

From a strict language definition perspective, `inline` only means that a definition of a function can appear multiple times in a program. However, it is also meant as a hint to the compiler that calls to that function should be "expanded inline": Doing so can produce more efficient code for certain cases, but it can also make the code less efficient for many other cases. Nowadays, compilers usually are better at deciding this without the hint implied by the `inline` keyword. However, compilers still account for the presence of `inline` in that decision.

> 从严格的语言定义角度来看，“内联”仅意味着函数的定义可以在程序中多次出现。然而，这也意味着向编译器提示，对该函数的调用应该“内联扩展”：这样做可以在某些情况下产生更高效的代码，但在许多其他情况下也会降低代码的效率。如今，编译器通常更善于在没有“inline”关键字暗示的情况下决定这一点。然而，编译器仍然解释了“内联”在该决定中的存在。

#### 1.6.3 Why Not **constexpr**?

Since C++11, you can use `constexpr` to provide the ability to use code to compute some values at compile time. For a lot of templates this makes sense.

> 从 C++11 开始，您可以使用“constexpr”来提供在编译时使用代码计算某些值的能力。对于许多模板来说，这是有意义的。

For example, to be able to use the maximum function at compile time, you have to declare it as follows:

> 例如，为了能够在编译时使用 maximum 函数，您必须如下声明它：

```cpp
`basics/maxconstexpr.hpp`

template<typename T1, typename T2>
[constexpr auto] max (T1 a, T2 b)
{
  return b < a ? a : b;\
}
```

With this, you can use the maximum function template in places with compile-time context, such as when declaring the size of a raw array:

> 这样，您就可以在编译时上下文的地方使用最大函数模板，例如在声明原始数组的大小时：

```cpp
int a[::max[(sizeof][(char]),1000u)];
```

or the size of a `std::array<>`:

```cpp
std::array<std::string, ::max[(sizeof][(char]),1000u)> arr;
```

Note that we pass `1000` as `unsigned int` to avoid warnings about comparing a signed with an unsigned value inside the template.

> 请注意，我们将“1000”作为“unsigned int”传递，以避免在模板内比较有符号值和无符号值时出现警告。

Section [[8.2]] on page [[125]] will discuss other examples of using `constexpr`. However, to keep our focus on the fundamentals, we usually will skip `constexpr` when discussing other template features.

> 第[[125]]页第[[8.2]]节将讨论使用“constexpr”的其他示例。然而，为了保持我们对基本原理的关注，在讨论其他模板功能时，我们通常会跳过“constexpr”。

### 1.7 Summary

```cpp
- Function templates define a family of functions for different template arguments.
- When you pass arguments to function parameters depending on template parameters, function templates deduce the template parameters to be instantiated for the corresponding parameter types.
- You can explicitly qualify the leading template parameters.
- You can define default arguments for template parameters. These may refer to previous template parameters and be followed by parameters not having default arguments.
- You can overload function templates.
- When overloading function templates with other function templates, you should ensure that only one of them matches for any call.
- When you overload function templates, limit your changes to specifying template parameters explicitly.
- Ensure the compiler sees all overloaded versions of function templates before you call them.
```

```cpp
^[1]^ Note that the `max()` template according to [StepanovNotes] intentionally returns "`b < a ? a : b`" instead of "`a < b ? b : a`" to ensure that the function behaves correctly even if the two values are equivalent but not equal.
^[2]^ Before C++17, type `T` also had to be copyable to be able to pass in arguments, but since C++17 you can pass temporaries (rvalues, see [Appendix [B]]) even if neither a copy nor a move constructor is valid.
^[3]^ For example, if one argument type is defined in namespace `std` (such as `std::string`), according to the lookup rules of C++, both the global and the `max()` template in `std` are found (see [Appendix [C]]).
^[4]^ A "one-entity-fits-all" alternative is conceivable but not used in practice (it would be less efficient at run time). All language rules are based on the principle that different entities are generated for different template arguments.
^[5]^ The terms *instance* and *instantiate* are used in a different context in object-oriented programming---namely, for a concrete object of a class. However, because this book is about templates, we use this term for the "use" of templates unless otherwise specified.
^[6]^ For example, The Visual C++ compiler in some versions (such as Visual Studio 20133 and 2015) allow undeclared names that don't depend on template parameters and even some syntax flaws (such as a missing semicolon).
^[7]^ Deduction can be seen as part of overload resolution---a process that is not based on selection of return types either. The sole exception is the return type of conversion operator members.
^[8]^ In C++, the return type also cannot be deduced from the context in which the caller uses the call.
^[9]^ Prior to C++11, default template arguments were only permitted in class templates, due to a historical glitch in the development of function templates.
^[10]^ Again, in C++11 you had to use `typename std::decay<`...`>::type` instead of `std::decay_t<`...`>` (see Section [[2.8]] on page [[40]]).
^[11]^ In general, a conforming compiler isn't even permitted to reject this code.
```

## Chapter 2

## Class Templates

Similar to functions, classes can also be parameterized with one or more types. Container classes, which are used to manage elements of a certain type, are a typical example of this feature. By using class templates, you can implement such container classes while the element type is still open. In this chapter we use a stack as an example of a class template.

> 与函数类似，类也可以用一个或多个类型进行参数化。用于管理特定类型元素的容器类就是此功能的典型示例。通过使用类模板，您可以在元素类型仍然打开的情况下实现这样的容器类。在本章中，我们使用堆栈作为类模板的示例。

### 2.1 Implementation of Class Template **Stack**

As we did with function templates, we declare and define class `Stack<>` in a header file as follows:

> 正如我们对函数模板所做的那样，我们在头文件中声明和定义类“Stack＜＞”，如下所示：

```cpp
`basics/stack1.hpp`

#include <vector>
#include <cassert>
\
template<typename T>
class Stack {
     private:\
     std::vector<T> elems;      // elements
   public:
\
     void push(T const& elem);  // push element
     void pop();                // pop element
     T const& top() const;      // return top element
     [bool] empty() const \
        return elems.empty();
     }
};
template<typename T>
void Stack<T>::push (T const& elem)
{
   elems.push_back(elem);      // append copy of passed [elem]}
\
template<typename T>
void Stack<T>::pop ()
{
   assert(!elems.empty());
   elems.pop_back();           // remove last element
}
\
template<typename T>
T const& Stack<T>::top () const\
{
   assert(!elems.empty());
   return elems.back();        // return copy of last element
}
```

As you can see, the class template is implemented by using a class template of the C++ standard library: `vector<>`. As a result, we don't have to implement memory management, copy constructor, and assignment operator, so we can concentrate on the interface of this class template.

> 正如您所看到的，类模板是通过使用 C++ 标准库的类模板来实现的：`vector<>`。因此，我们不必实现内存管理、复制构造函数和赋值运算符，所以我们可以专注于这个类模板的接口。

#### 2.1.1 Declaration of Class Templates

Declaring class templates is similar to declaring function templates: Before the declaration, you have to declare one or multiple identifiers as a type parameter(s). Again, `T` is usually used as an identifier:

> 声明类模板类似于声明函数模板：在声明之前，必须将一个或多个标识符声明为类型参数。同样，“T”通常用作标识符：

```cpp
template<typename T>
class Stack {
   ...
};
```

Here again, the keyword `class` can be used instead of `typename`:

```cpp
template<class T>
class Stack {
   ...
};
```

Inside the class template, `T` can be used just like any other type to declare members and member functions. In this example, `T` is used to declare the type of the elements as vector of `T` s, to declare `push()` as a member function that uses a `T` as an argument, and to declare `top()` as a function that returns a `T`:

> 在类模板中，“T”可以像任何其他类型一样用于声明成员和成员函数。在本例中，“T”用于将元素的类型声明为“T”的向量，将“push()”声明为使用“T”作为参数的成员函数，并将“top()”宣布为返回“T”：

```cpp
template<\
typename T>
class Stack {
  private:\
    std::vector<T> elems;      // elements
\
  public:
    void push(T const& elem);  // push element
    void pop();                // pop element
    T const& top()
    const;                     // return top element
    [bool] empty() const \
        return elems.empty();
    }
};
```

The type of this class is `Stack<T>`, with `T` being a template parameter. Thus, you have to use `Stack<T>` whenever you use the type of this class in a declaration except in cases where the template arguments can be deduced. However, inside a class template using the class name not followed by template arguments represents the class with its template parameters as its arguments (see Section [[13.2.3]] on page [[221]] for details).

> 此类的类型为“Stack＜T＞”，其中“T”是一个模板参数。因此，无论何时在声明中使用此类的类型，都必须使用“Stack＜T＞”，除非可以推导出模板参数。但是，在类模板中，使用类名而不后跟模板参数表示以其模板参数作为参数的类(有关详细信息，请参见第[[221]]页的第[[13.2.3]]节)。

If, for example, you have to declare your own copy constructor and assignment operator, it typically looks like this:

> 例如，如果您必须声明自己的复制构造函数和赋值运算符，则通常如下所示：

```cpp
template<typename T>
class Stack {
   ...
   Stack (Stack const&);                    // copy constructor
   Stack& [operator]= (Stack const&);         // assignment operator
   ...
};
```

which is formally equivalent to:

```cpp
template<typename T>
class Stack {
   ...
   Stack (Stack<T> const&);                  // copy constructor
   Stack<T>& [operator]= (Stack<T> const&);    // assignment operator
   ...
};
```

but usually the `<T>` signals special handling of special template parameters, so it's usually better to use the first form.

> 但通常“＜T＞”表示对特殊模板参数的特殊处理，因此通常最好使用第一种形式。

However, outside the class structure you'd need:

```cpp
template<typename T>
[bool operator]== (Stack<T> const& lhs, Stack<T> const& rhs);
```

Note that in places where the name and not the type of the class is required, only `Stack` may be used. This is especially the case when you specify the _name_ of constructors (not their arguments) and the destructor.

> 请注意，在需要类的名称而不是类型的地方，只能使用“堆栈”。当您指定构造函数(而不是它们的参数)和析构函数的名称时，情况尤其如此。

Note also that, unlike nontemplate classes, you can't declare or define class templates inside functions or block scope. In general, templates can only be defined in global/namespace scope or inside class declarations (see Section [[12.1]] on page [[177]] for details).

> 还要注意，与非模板类不同，不能在函数或块范围内声明或定义类模板。通常，模板只能在全局/命名空间范围内或类声明内定义(有关详细信息，请参阅第[[177]]页的第[[12.1]]节)。

#### 2.1.2 Implementation of Member Functions

To define a member function of a class template, you have to specify that it is a template, and you have to use the full type qualification of the class template. Thus, the implementation of the member function `push()` for type `Stack<T>` looks like this:

> 要定义类模板的成员函数，必须指定它是一个模板，并且必须使用类模板的完整类型限定。因此，类型“Stack＜T＞”的成员函数“push()”的实现如下所示：

```cpp
template<typename T>
void Stack<T>::push (T const& elem)
{
   elems.push_back(elem);        // append copy of passed [elem]\
}
```

In this case, `push_back()` of the element vector is called, which appends the element at the end of the vector.

> 在这种情况下，调用元素向量的“push_back()”，它将元素附加在向量的末尾。

Note that `pop_back()` of a vector removes the last element but doesn't return it. The reason for this behavior is exception safety. It is impossible to implement a completely exception-safe version of `pop()` that returns the removed element (this topic was first discussed by Tom Cargill in [CargillExceptionSafety] and is discussed as Item 10 in [SutterExceptional]). However, ignoring this danger, we could implement a `pop()` that returns the element just removed. To do this, we simply use `T` to declare a local variable of the element type:

> 请注意，向量的“pop_back()”会删除最后一个元素，但不会返回它。这种行为的原因是异常安全。不可能实现返回已删除元素的完全异常安全的“pop()”版本(此主题由 Tom Cargill 在[CargillExceptionSafety]中首次讨论，并在[SutterException]中作为第 10 项讨论)。然而，忽略这个危险，我们可以实现一个返回刚刚删除的元素的“pop()”。为此，我们只需使用“T”来声明元素类型的局部变量：

```cpp
\
template<typename T>
T Stack<T>::pop ()
{
   assert(!elems.empty());
   T elem = elems.back();        // save copy of last element
   elems.pop_back();             // remove last element
   return elem;                  // return copy of saved element
}
```

Because `back()` (which returns the last element) and `pop_back()` (which removes the last element) have undefined behavior when there is no element in the vector, we decided to check whether the stack is empty. If it is empty, we assert, because it is a usage error to call `pop()` on an empty stack. This is also done in `top()`, which returns but does not remove the top element, on attempts to remove a nonexistent top element:

> 因为当向量中没有元素时，“back()”(返回最后一个元素)和“pop_back()””(删除最后一个元件)具有未定义的行为，所以我们决定检查堆栈是否为空。如果它是空的，我们断言，因为在空堆栈上调用“pop()”是一个用法错误。这也在“top()”中完成，当试图删除不存在的 top 元素时，返回但不删除 top 元素：

```cpp
template<typename T>
T const& Stack<T>::top () const\
{
    assert(!elems.empty());
   return elems.back();        // return copy of last element
}
```

Of course, as for any member function, you can also implement member functions of class templates as an inline function inside the class declaration. For example:

> 当然，对于任何成员函数，也可以将类模板的成员函数实现为类声明中的内联函数。例如

```cpp
template<typename T>
class Stack {
   ...
   void push (T const& elem) {
       elems.push_back(elem);        // append copy of passed [elem]\
   }
   ...
};
```

### 2.2 Use of Class Template **Stack**

To use an object of a class template, until C++17 you must always specify the template arguments explicitly.[1] The following example shows how to use the class template `Stack<>`:

> 要使用类模板的对象，在 C++17 之前，必须始终显式指定模板参数。[1] 以下示例显示了如何使用类模板“Stack＜＞”：

```cpp
`basics/stack1test.cpp`

#include "stack1.hpp"\
#include <iostream>
#include <string>
\
int main()
{
  Stack< int>       intStack;      // stack of ints
  Stack<std::string> stringStack;  // stack of strings
\
  // manipulate int stack
  intStack.push(7);
  std::cout << intStack.top() << '\n';\
\
  // manipulate string stack
  stringStack.push("hello");
  std::cout << stringStack.top() << '\n';\
  stringStack.pop();
}
```

By declaring type `Stack<int>`, `int` is used as type `T` inside the class template. Thus, `intStack` is created as an object that uses a vector of `int` s as elements and, for all member functions that are called, code for this type is instantiated. Similarly, by declaring and using `Stack<std::string>`, an object that uses a vector of strings as elements is created, and for all member functions that are called, code for this type is instantiated.

> 通过声明类型“Stack＜int＞”，“int”被用作类模板内的类型“T”。因此，“intStack”被创建为一个使用“int”的向量作为元素的对象，并且对于所有被调用的成员函数，该类型的代码都被实例化。类似地，通过声明和使用“Stack＜std:：string＞”，将创建一个使用字符串向量作为元素的对象，并为所有被调用的成员函数实例化此类型的代码。

Note that code is instantiated _only for template (member) functions that are called_. For class templates, member functions are instantiated only if they are used. This, of course, saves time and space and allows use of class templates only partially, which we will discuss in Section [[2.3]] on page [[29]].

> 请注意，代码仅被实例化为被调用的模板(成员)函数。对于类模板，成员函数只有在使用时才被实例化。当然，这节省了时间和空间，并且只允许部分使用类模板，我们将在第[29]页的第[2.3]]节中讨论这一点。

In this example, the default constructor, `push()`, and `top()` are instantiated for both `int` and strings. However, `pop()` is instantiated only for strings. If a class template has static members, these are also instantiated once for each type for which the class template is used.

> 在本例中，默认构造函数“push()”和“top()”都是为“int”和字符串实例化的。但是，“pop()”仅针对字符串进行实例化。如果类模板具有静态成员，则也会为使用该类模板的每个类型实例化一次。

An instantiated class template's type can be used just like any other type. You can qualify it with `const` or `volatile` or derive array and reference types from it. You can also use it as part of a type definition with `typedef` or `using` (see Section [[2.8]] on page [[38]] for details about type definitions) or use it as a type parameter when building another template type. For example:

> 实例化类模板的类型可以像任何其他类型一样使用。您可以用“const”或“volatile”限定它，也可以从中派生数组和引用类型。您也可以将它用作带有“typedef”和“using”的类型定义的一部分(有关类型定义的详细信息，请参阅第[[38]]页的第[[2.8]]节)，或者在构建另一个模板类型时将它用作类型参数。例如

```cpp
void foo(Stack [<int]> const& s)   // parameter [s] is int stack
{
  using IntStack = Stack [<int]>;  // [IntStack] is another name for [Stack<int>]\
  Stack< int> istack[10];        // [istack] is array of 10 int stacks
  IntStack istack2[10];          // [istack2] is also an array of 10 int stacks (same type)
  ...
}
```

Template arguments may be any type, such as pointers to `float` s or even stacks of `int` s:

> 模板参数可以是任何类型，例如指向“float”的指针，甚至是“int”的堆栈：

```cpp
Stack< [float]\*>     floatPtrStack;        // stack of [float] pointers
Stack<Stack< int>> intStackStack;        // stack of stack of ints
```

The only requirement is that any operation that is called is possible according to this type.

> 唯一的要求是，根据此类型，调用的任何操作都是可能的。

Note that before C++11 you had to put whitespace between the two closing template brackets:

> 请注意，在 C++11 之前，您必须在两个结束模板方括号之间放置空格：

```cpp
Stack<Stack< int> > intStackStack;        // OK with all C++ versions
```

If you didn't do this, you were using operator `>>`, which resulted in a syntax error:

> 如果不执行此操作，则说明您使用了运算符“>>”，从而导致语法错误：

```cpp
`Stack<Stack< int>> intStackStack;`        // ERROR before C++11
```

The reason for the old behavior was that it helped the first pass of a C++ compiler to tokenize the source code independent of the semantics of the code. However, because the missing space was a typical bug, which required corresponding error messages, the semantics of the code more and more had to get taken into account anyway. So, with C++11 the rule to put a space between two closing template brackets was removed with the "angle bracket hack" (see Section [[13.3.1]] on page [[226]] for details).

> 旧行为的原因是它有助于 C++ 编译器的第一次传递，使源代码独立于代码的语义进行标记化。然而，由于缺少的空间是一个典型的错误，需要相应的错误消息，因此无论如何都必须越来越多地考虑代码的语义。因此，在 C++11 中，在两个闭合模板括号之间放置空格的规则被“角括号破解”删除(详见第[[226]]页第[[13.3.1]]节)。

### 2.3 Partial Usage of Class Templates

A class template usually applies multiple operations on the template arguments it is instantiated for (including construction and destruction). This might lead to the impression that these template arguments have to provide all operations necessary for all member functions of a class template. But this is not the case: Template arguments only have to provide all necessary operations that _are_ needed (instead of that _could_ be needed).

> 类模板通常对实例化的模板参数应用多个操作(包括构造和销毁)。这可能会导致这样的印象，即这些模板参数必须提供类模板的所有成员函数所需的所有操作。但事实并非如此：Template 参数只需要提供_are_所需的所有必要操作(而不是_could_ be need)。

If, for example, class `Stack<>` would provide a member function `printOn()` to print the whole stack content, which calls `operator<<` for each element:

> 例如，如果类“Stack＜＞”将提供一个成员函数“printOn()”来打印整个堆栈内容，该函数为每个元素调用“operator＜＜”：

```cpp
template<typename T>
class Stack {
  ...
  void printOn() (std::ostream& strm) const {
     [for] (T const& elem : elems) {
       strm << elem << ['] ';        // call [<<] for each element
     }
   }
};
```

You can still use this class for elements that don't have operator<< defined:

> 您仍然可以将此类用于没有运算符 << 定义的元素：

```cpp
Stack<std::pair< int, int>> ps;        // note: [std::pair<>] has no [operator<<] defined
ps.push();                       // OK
ps.push();                       // OK
std::cout << ps.top().first << '\n';         // OK
std::cout << ps.top().second << '\n';        // OK
```

Only if you call `printOn()` for such a stack, the code will produce an error, because it can't instantiate the call of `operator<<` for this specific element type:

> 只有当您为这样的堆栈调用“printOn()”时，代码才会产生错误，因为它无法实例化此特定元素类型的“operator<<”调用：

```cpp
ps.printOn(std::cout);     // ERROR: [operator<<] not supported for element type
```

#### 2.3.1 Concepts

This raises the question: How do we know which operations are required for a template to be able to get instantiated? The term _concept_ is often used to denote a set of constraints that is repeatedly required in a template library. For example, the C++ standard library relies on such concepts as _random access iterator_ and _default constructible_.

> 这就提出了一个问题：我们如何知道模板需要哪些操作才能实例化？术语_concept_通常用于表示模板库中重复需要的一组约束。例如，C++ 标准库依赖于_random 访问迭代器_和_default 构造_等概念。

Currently (i.e., as of C++17), concepts can more or less only be expressed in the documentation (e.g., code comments). This can become a significant problem because failures to follow constraints can lead to terrible error messages (see Section [[9.4]] on page [[143]]).

> 目前(即，从 C++17 开始)，概念或多或少只能在文档中表达(例如，代码注释)。这可能成为一个重大问题，因为未能遵守约束可能会导致可怕的错误消息(见第[[143]]页第[[9.4]]节)。

For years, there have also been approaches and trials to support the definition and validation of concepts as a language feature. However, up to C++17 no such approach was standardized yet.

> 多年来，也有一些方法和试验来支持概念作为一种语言特征的定义和验证。然而，到 C++17 为止，还没有这样的方法被标准化。

Since C++11, you can at least check for some basic constraints by using the `static_assert` keyword and some predefined type traits. For example:

> 自从 C++11 以来，您至少可以通过使用“static_assert”关键字和一些预定义的类型特征来检查一些基本约束。例如

```cpp
template<typename T>
class C\
{
\
    [static_assert](std::is_default_constructible<T>::value,\
                  "Class C requires default-constructible elements");
    ...
};
```

Without this assertion the compilation will still fail, if the default constructor is required. However, the error message then might contain the entire template instantiation history from the initial cause of the instantiation down to the actual template definition in which the error was detected (see Section [[9.4]] on page [[143]]).

> 如果没有这个断言，如果需要默认的构造函数，编译仍然会失败。然而，错误消息可能包含从实例化的初始原因到检测到错误的实际模板定义的整个模板实例化历史(参见第[[143]]页第[[9.4]]节)。

However, more complicated code is necessary to check, for example, objects of type `T` provide a specific member function or that they can be compared using operator `<`. See Section [[19.6.3]] on page [[436]] for a detailed example of such code.

> 然而，需要更复杂的代码来检查，例如，类型为“T”的对象是否提供了特定的成员函数，或者它们是否可以使用运算符“<”进行比较。有关此类代码的详细示例，请参见第[[436]]页第[[19.6.3]]节。

See [Appendix [E]] for a detailed discussion of concepts for C++.

### 2.4 Friends

Instead of printing the stack contents with `printOn()` it is better to implement `operator<<` for the stack. However, as usual `operator<<` has to be implemented as nonmember function, which then could call `printOn()` inline:

> 与其用“printOn()”打印堆栈内容，不如为堆栈实现“operator<<”。然而，像往常一样，“operator<<”必须实现为非成员函数，然后可以内联调用“printOn()”：

```cpp
template<typename T>
class Stack {
   ...
   void printOn() (std::ostream& strm) const {
    ...
   }
   [friend] std::ostream& [operator]<< (std::ostream& strm,\
                                    Stack<T> const& s) {
     s.printOn(strm);
     return strm;\
   }
};
```

Note that this means that `operator<<` for class `Stack<>` is not a function template, but an "ordinary" function instantiated with the class template if needed.[2]

> 请注意，这意味着类“Stack＜＞”的“operator＜＜”不是函数模板，而是在需要时使用类模板实例化的“普通”函数。2.

However, when trying to _declare_ the friend function and _define_ it afterwards, things become more complicated. In fact, we have two options:

> 然而，当尝试_declare_friend 函数并在之后对其进行_define_时，事情会变得更加复杂。事实上，我们有两种选择：

1. We can implicitly declare a new function template, which must use a different template parameter, such as `U`:

> 1.我们可以隐式声明一个新的函数模板，它必须使用不同的模板参数，例如“U”：

```cpp
template<typename T>
class Stack {
   ...
   template<typename U>
   [friend] std::ostream& [operator]<< (std::ostream&, Stack<U> const&);
};
```

Neither using `T` again nor skipping the template parameter declaration would work (either the inner `T` hides the outer `T` or we declare a nontemplate function in namespace scope).

> 再次使用“T”或跳过模板参数声明都不起作用(内部“T”隐藏外部“T”，或者我们在命名空间范围中声明非模板函数)。

2. We can forward declare the output operator for a `Stack<T>` to be a template, which, however, means that we first have to forward declare `Stack<T>`:

> 2.我们可以将“Stack＜T＞”的输出运算符转发声明为模板，但这意味着我们首先必须转发声明“Stack＞T＞”：

```cpp
template<typename T>
class Stack;\
template<typename T>
std::ostream& [operator]<< (std::ostream&, Stack<T> const&);
```

Then, we can declare this function as friend:

```cpp
template<typename T>
class Stack {
   ...
   [friend] std::ostream& [operator]<< <T> (std::ostream&,\
                                        Stack<T> const&);
};
```

Note the <T> behind the "function name" operator<<. Thus, we declare a specialization of the nonmember function template as friend. Without <T> we would declare a new nontemplate function. See Section [[12.5.2]] on page [[211]] for details.

> 请注意“函数名”运算符 << 后面的<T>。因此，我们将非成员函数模板的专门化声明为友元。如果没有<T>，我们将声明一个新的非模板函数。详见第[[211]]页第[[12.5.2]]节。

In any case, you can still use this class for elements that don't have operator<< defined. Only calling operator<< for this stack results in an error:

> 在任何情况下，您仍然可以将此类用于未定义运算符 << 的元素。仅对此堆栈调用运算符 << 会导致错误：

```cpp
Stack<std::pair< int, int>> ps;      // [std::pair<>] has no [operator<<] defined
ps.push();                     // OK
ps.push();                     // OK
std::cout <<\
ps.top().first << '\n';               // OK
std::cout <<\
ps.top().second << '\n';              // OK
std::cout << ps << '\n';              // ERROR: [operator<<] not supported
                                     //       for element type
```

### 2.5 Specializations of Class Templates

You can specialize a class template for certain template arguments. Similar to the overloading of function templates (see Section [[1.5]] on page [[15]]), specializing class templates allows you to optimize implementations for certain types or to fix a misbehavior of certain types for an instantiation of the class template. However, if you specialize a class template, you must also specialize all member functions. Although it is possible to specialize a single member function of a class template, once you have done so, you can no longer specialize the whole class template instance that the specialized member belongs to.

> 您可以为某些模板参数专门化类模板。与函数模板的重载类似(请参见第[[15]]页的第[[1.5]]节)，专门化类模板允许您优化某些类型的实现，或修复某些类型的不当行为以实例化类模板。但是，如果专门化类模板，则还必须专门化所有成员函数。虽然可以专门化类模板的单个成员函数，但一旦这样做，就不能再专门化该专门化成员所属的整个类模板实例。

To specialize a class template, you have to declare the class with a leading `template<>` and a specification of the types for which the class template is specialized. The types are used as a template argument and must be specified directly following the name of the class:

> 要专门化类模板，必须用前导的“template＜＞”和类模板所专门化的类型的规范来声明类。类型用作模板参数，必须直接在类的名称后面指定：

```cpp
template<>
class Stack<std::string> {
   ...
};
```

For these specializations, any definition of a member function must be defined as an "ordinary" member function, with each occurrence of `T` being replaced by the specialized type:

> 对于这些专门化，成员函数的任何定义都必须定义为“普通”成员函数，每次出现的“T”都被专门化类型取代：

```cpp
void Stack<std::string>::push (std::string const& elem)
{
   elems.push_back(elem);        // append copy of passed [elem]\
}
```

Here is a complete example of a specialization of `Stack<>` for type `std::string`:

> 以下是“std:：string”类型的“Stack＜＞”专业化的完整示例：

```cpp
`basics/stack2.hpp`

#include "stack1.hpp"\
#include <deque>
#include <string>
#include <cassert>
\
template<>
class Stack<std::string> {
   private:\
      std::deque<std::string> elems;    // elements
\
   public:
      void push(std::string const&);    // push element
      void pop();                       // pop element
      std::string const& top() const;   // return top element
      [bool] empty() const \
          return elems.empty();
   }
};
\
void Stack<std::string>::push (std::string const& elem)
{
   elems.push_back(elem);     // append copy of passed [elem]\
}
\
void Stack<std::string>::pop ()
{
   assert(!elems.empty());
   elems.pop_back();          // remove last element
}
\
std::string const& Stack<std::string>::top () const\
{
   assert(!elems.empty());
   return elems.back();      // return copy of last element
}
```

In this example, the specialization uses reference semantics to pass the string argument to `push()`, which makes more sense for this specific type (we should even better pass a forwarding reference, though, which is discussed in Section [[6.1]] on page [[91]]).

> 在本例中，专业化使用引用语义将字符串参数传递给“push()”，这对这种特定类型更有意义(不过，我们应该更好地传递转发引用，这在第[[91]]页的第[[6.1]]节中进行了讨论)。

Another difference is to use a deque instead of a vector to manage the elements inside the stack. Although this has no particular benefit here, it does demonstrate that the implementation of a specialization might look very different from the implementation of the primary template.

> 另一个区别是使用 deque 而不是向量来管理堆栈中的元素。尽管这在这里没有特别的好处，但它确实表明了专业化的实现可能与主模板的实现非常不同。

### 2.6 Partial Specialization

Class templates can be partially specialized. You can provide special implementations for particular circumstances, but some template parameters must still be defined by the user. For example, we can define a special implementation of class `Stack<>` for pointers:

> 类模板可以是部分专用的。您可以为特定情况提供特殊的实现，但某些模板参数仍必须由用户定义。例如，我们可以为指针定义类“Stack＜＞”的特殊实现：

```cpp
`basics/stackpartspec.hpp`

#include "stack1.hpp"\
\
// partial specialization of class [Stack<>] for pointers:
template<typename T>
class Stack<T*> {
   private:\
      std::vector<T*> elems;     // elements
\
public:
   void push(T*);                // push element
   T* pop();                     // pop element
   T* top() const;               // return top element
   [bool] empty() const \
      return elems.empty();
   }
};
template<typename T>
void Stack<T*>::push (T* elem)
{
   elems.push_back(elem);        // append copy of passed [elem]\
}
\
template<typename T>
T* Stack<T*>::pop ()
{
    assert(!elems.empty());
    T* p = elems.back();
    elems.pop_back();           // remove last element
    return p;                   // and return it (unlike in the general case)
}
\
template<typename T>
T* Stack<T*>::top () const\
{
   assert(!elems.empty());
   return elems.back();        // return copy of last element
}
```

With

```cpp
template<typename T>
class Stack<T*> {
};
```

we define a class template, still parameterized for `T` but specialized for a pointer (`Stack<T*>`).

> 我们定义了一个类模板，仍然为“T”参数化，但专门用于指针(“Stack＜T*＞”)。

Note again that the specialization might provide a (slightly) different interface. Here, for example, `pop()` returns the stored pointer, so that a user of the class template can call `delete` for the removed value, when it was created with `new`:

> 再次注意，专业化可能会提供一个(稍微)不同的接口。例如，在这里，“pop()”返回存储的指针，这样类模板的用户就可以在使用“new”创建删除的值时调用“delete”：

```cpp
Stack<int*> ptrStack;        // stack of pointers (special implementation)
\
ptrStack.push([new int]);
std::cout << \*ptrStack.top() << '\n';\
delete ptrStack.pop();
```

##### Partial Specialization with Multiple Parameters

Class templates might also specialize the relationship between multiple template parameters. For example, for the following class template:

> 类模板还可以专门化多个模板参数之间的关系。例如，对于以下类模板：

```cpp
template<typename     T1, typename T2>
class MyClass {
   ...
};
```

the following partial specializations are possible:

```cpp
// partial specialization: both template parameters have same type
template<typename T>
class MyClass<T,T> {
   ...
};
\
// partial specialization: second type is int\
template<typename T>
class MyClass<T,int> {
   ...
};
\
// partial specialization: both template parameters are pointer types
template<typename T1, typename T2>
class MyClass<T1\*,T2\*> {
   ...
};
```

The following examples show which template is used by which declaration:

```cpp
MyClass< int, [float]> mif;      // uses [MyClass<T1,T2>]\
MyClass< [float], [float]> mff;    // uses [MyClass<T,T>]\
MyClass< [float], int> mfi;      // uses [MyClass<T,int>]\
MyClass<int*, [float]\*> mp;     // uses [MyClass<T1\*,T2\*>]
```

If more than one partial specialization matches equally well, the declaration is ambiguous:

> 如果多个分部专门化匹配得同样好，则声明不明确：

```cpp
MyClass< int, int> m;             // ERROR: matches [MyClass<T,T>]\
                                 //        and [MyClass<T,int>]\
MyClass<int*,int*> m;         // ERROR: matches [MyClass<T,T>]\
                              //         and [MyClass<T1\*,T2\*>]
```

To resolve the second ambiguity, you could provide an additional partial specialization for pointers of the same type:

> 为了解决第二个歧义，可以为相同类型的指针提供额外的部分专用化：

```cpp
template<typename T>
class MyClass<T*,T*> {
   ...
};
```

For details of partial specialization, see Section [[16.4]] on page [[347]].

> 有关部分专业化的详细信息，请参见第[[347]]页第[[16.4]]节。

### 2.7 Default Class Template Arguments

As for function templates, you can define default values for class template parameters. For example, in class `Stack<>` you can define the container that is used to manage the elements as a second template parameter, using `std::vector<>` as the default value:

> 对于函数模板，可以定义类模板参数的默认值。例如，在类“Stack＜＞”中，您可以将用于管理元素的容器定义为第二个模板参数，使用“std:：vector＜＞”作为默认值：

```cpp
`basics/stack3.hpp`

#include <vector>
#include <cassert>
\
template<typename T, typename Cont = std::vector<T>>
class Stack {
   private:\
      Cont elems;                // elements
\
   public:
      void push(T const& elem);  // push element
      void pop();                // pop element
      T const& top() const;      // return top element
      [bool] empty() const \
            return elems.empty();
   }
};
\
template<typename T, typename Cont>
void Stack<T,Cont>::push (T const& elem)
{
elems.push_back(elem);           // append copy of passed [elem]}
template<typename T,\
typename Cont>
\
void Stack<T,Cont>::pop ()
{
   assert(!elems.empty());
   elems.pop_back();             // remove last element
}
\
template<typename T, typename Cont>
T const& Stack<T,Cont>::top () const\
{
   assert(!elems.empty());
   return elems.back();        // return copy of last element
}
```

Note that we now have two template parameters, so each definition of a member function must be defined with these two parameters:

> 请注意，我们现在有两个模板参数，因此成员函数的每个定义都必须使用这两个参数进行定义：

```cpp
template<typename T, typename Cont>
void Stack<T,Cont>::push (T const& elem)
{
   elems.push_back(elem);        // append copy of passed [elem]\
}
```

You can use this stack the same way it was used before. Thus, if you pass a first and only argument as an element type, a vector is used to manage the elements of this type:

> 您可以使用与以前相同的方式使用此堆栈。因此，如果将第一个也是唯一一个参数作为元素类型传递，则会使用向量来管理此类型的元素：

```cpp
template<typename T, typename Cont = std::vector<T>>
class Stack {
   private:\
      Cont elems;        // elements
    ...
};
```

In addition, you could specify the container for the elements when you declare a Stack object in your program:

> 此外，当您在程序中声明 Stack 对象时，您可以指定元素的容器：

```cpp
`basics/stack3test.cpp`

#include "stack3.hpp"\
   
#include <iostream>
   
#include <deque>
int main()
{
\
  // stack of ints:
  Stack< int> intStack;\
\
  // stack of [double]s using a [std::deque<>] to manage the elements
  Stack< [double],std::deque< [double]>> dblStack;\
\
  // manipulate int stack
  intStack.push(7);
  std::cout << intStack.top() << '\n';\
  intStack.pop();
\
  // manipulate [double] stack
  dblStack.push(42.42);
  std::cout << dblStack.top() << '\n';\
  dblStack.pop();
}
```

With

```cpp
`Stack< double,std::deque< double>>`
```

you declare a stack for `double` s that uses a `std::deque<>` to manage the elements internally.

> 您为“double”声明了一个堆栈，该堆栈使用“std:：deque＜＞”在内部管理元素。

### 2.8 Type Aliases

You can make using a class template more convenient by defining a new name for the whole type.

> 通过为整个类型定义一个新名称，可以更方便地使用类模板。

##### Typedefs and Alias Declarations

To simply define a new name for a complete type, there are two ways to do it:

> 要简单地为一个完整的类型定义一个新名称，有两种方法：

1. By using the keyword `typedef`:

```cpp
typedef Stack\
typedef Stack[<int]> IntStack;     *[// typedef]*\
void foo (IntStack const& s);    *[//]* [s *is stack ofint*[s]*\
IntStack istack[10];             *[//]* [istack] *[is array of 10 stacks of]* [int*[s]
```

We call this declaration a _typedef_[3] and the resulting name is called a _typedef-name_.

> 我们将此声明称为_typedef_[3]，生成的名称称为_type 定义名称。

2. By using the keyword `using` (since C++11):

```cpp
using IntStack = Stack [<int]>;        // alias declaration
void foo (IntStack const& s);        // [s] is stack of ints
IntStack istack[10];                 // [istack] is array of 10 stacks of ints
```

Introduced by [DosReisMarcusAliasTemplates], this is called an _alias declaration_.

> 由[DosReisMacusAliasTemplates]引入，这被称为_alias 声明。

Note that in both cases we define a new name for an existing type rather than a new type. Thus, after the typedef

> 请注意，在这两种情况下，我们都为现有类型定义一个新名称，而不是新类型。因此，在 typedef 之后

```cpp
typedef Stack [<int]> IntStack;
```

or

```cpp
using IntStack = Stack [<int]>;
```

`IntStack` and `Stack<int>` are two interchangeable notations for the same type.

As a common term for both alternatives to define a new name for an existing type, we use the term _type alias declaration_. The new name is a _type alias_ then.

> 作为为现有类型定义新名称的两种备选方案的通用术语，我们使用术语_type alias declaration_。新名称为 a _type alias_then。

Because it is more readable (always having the defined type name on the left side of the `=`, for the remainder of this book, we prefer the alias declaration syntax when declaring an type alias.

> 因为它更可读(总是将定义的类型名称放在“=”的左侧，对于本书的其余部分，在声明类型别名时，我们更喜欢使用别名声明语法。

##### Alias Templates

Unlike a `typedef`, an alias declaration can be templated to provide a convenient name for a family of types. This is also available since C++11 and is called an _alias template_.[4]

> 与“typedef”不同，可以模板化别名声明，为类型族提供方便的名称。这也是从 C++11 开始提供的，称为_alias template_。4.

The following alias template `DequeStack`, parameterized over the element type `T`, expands to a `Stack` that stores its elements in a `std::deque`:

> 以下别名模板“DequeStack”在元素类型“T”上参数化，扩展为一个“Stack”，该“堆栈”将其元素存储在“std:：deque”中：

```cpp
template<typename T>
using DequeStack = Stack<T, std::deque<T>>;
```

Thus, both class templates and alias templates can be used as a parameterized type. But again, an alias template simply gives a new name to an existing type, which can still be used. Both `DequeStack<int>` and `Stack<int, std::deque<int>>` represent the same type.

> 因此，类模板和别名模板都可以用作参数化类型。但是，别名模板只是为现有类型提供一个新名称，该名称仍然可以使用。`DequeStack<int>` 和 `Stack<int，std:：deque<int>>` 表示相同的类型。

Note again that, in general, templates can only be declared and defined in global/namespace scope or inside class declarations.

> 再次注意，通常情况下，模板只能在全局/命名空间范围或类声明内部声明和定义。

##### Alias Templates for Member Types

Alias templates are especially helpful to define shortcuts for types that are members of class templates. After

> Alias 模板特别有助于为类模板的成员类型定义快捷方式。之后

```cpp
struct C {
   typedef ... iterator;\
   ...
};
```

or:

```cpp
struct MyType {
  using iterator = ...;\
  ...
};
```

a definition such as

```cpp
template<typename T>
using MyTypeIterator = typename MyType<T>::iterator;
```

allows the use of

```cpp
`MyTypeIterator< int> pos;`
```

instead of the following:[5]

```cpp
typename MyType<T>::iterator pos;
```

##### Type Traits Suffix_t

Since C++14, the standard library uses this technique to define shortcuts for all type traits in the standard library that yield a type. For example, to be able to write

> 自 C++14 以来，标准库使用此技术为标准库中生成类型的所有类型特征定义快捷方式。例如，为了能够写作

```cpp
std::add_const_t<T>                // since C++14
```

instead of

```cpp
typename std::add_const<T>::type   // since C++11
```

the standard library defines:

```cpp
namespace std {
  template<typename T> using add_const_t = typename add_const<T>::type;\
}
```

### 2.9 Class Template Argument Deduction

Until C++17, you always had to pass all template parameter types to class templates (unless they have default values). Since C++17, the constraint that you always have to specify the template arguments explicitly was relaxed. Instead, you can skip to define the templates arguments explicitly, if the constructor is able to _deduce_ all template parameters (that don't have a default value),

> 在 C++17 之前，您总是必须将所有模板参数类型传递给类模板(除非它们有默认值)。自从 C++17 以来，您总是必须显式指定模板参数的约束被放宽了。相反，如果构造函数能够减少所有模板参数(没有默认值)，则可以跳过显式定义模板参数，

For example, in all previous code examples, you can use a copy constructor without specifying the template arguments:

> 例如，在前面的所有代码示例中，您可以使用复制构造函数而不指定模板参数：

```cpp
Stack< int> intStack1;                 // stack of strings
Stack< int> intStack2 = intStack1;     // OK in all versions
Stack intStack3 = intStack1;           // OK since C++17
```

By providing constructors that pass some initial arguments, you can support deduction of the element type of a stack. For example, we could provide a stack that can be initialized by a single element:

> 通过提供传递一些初始参数的构造函数，您可以支持堆栈的元素类型的推导。例如，我们可以提供一个可以由单个元素初始化的堆栈：

```cpp
template<typename T>
class Stack {
   private:\
     std::vector<T> elems;        // elements
   public:
     Stack () = [default];\
     Stack (T const& elem)        // initialize stack with one element
       : elems() {
     }
     ...
};
```

This allows you to declare a stack as follows:

```cpp
`Stack intStack = 0;`              // `Stack<int>` deduced since C++17
```

By initializing the stack with the integer `0`, the template parameter `T` is deduced to be `int`, so that a `Stack<int>` is instantiated.

> 通过用整数“0”初始化堆栈，模板参数“T”被推导为“int”，从而实例化“stack＜int＞”。

Note the following:

• Due to the definition of the `int` constructor, you have to request the default constructors to be available with its default behavior, because the default constructor is available only if no other constructor is defined:

> •由于“int”构造函数的定义，您必须请求默认构造函数与其默认行为一起可用，因为只有在没有定义其他构造函数的情况下，默认构造函数才可用：

`Stack() = default;`

• The argument `elem` is passed to `elems` with braces around to initialize the vector `elems` with an initializer list with `elem` as the only argument:

> •参数“elem”通过大括号传递给“elems”，以初始化向量“elems’”，初始化器列表以“elem’”作为唯一参数：

`: elems()`

There is no constructor for a vector that is able to take a single parameter as initial element directly.[6]

> 没有一个向量的构造函数能够直接将单个参数作为初始元素。6.

Note that, unlike for function templates, class template arguments may not be deduced only partially (by explicitly specifying only _some_ of the template arguments). See Section [[15.12]] on page [[314]] for details.

> 注意，与函数模板不同，类模板参数可能不会仅部分推导(通过显式指定模板参数中的_some_)。详见第[[314]]页第[[15.12]]节。

##### Class Template Arguments Deduction with String Literals

In principle, you can even initialize the stack with a string literal:

```cpp
Stack stringStack = "bottom"; // `Stack<char const[7]>` deduced since C++17
```

**But** this causes a lot of trouble: In general, when passing arguments of a template type `T` by reference, the parameter doesn't _decay_, which is the term for the mechanism to convert a raw array type to the corresponding raw pointer type. This means that we really initialize a

> **但是**这会引起很多麻烦：通常，当通过引用传递模板类型“T”的参数时，参数不会_decay_，这是将原始数组类型转换为相应的原始指针类型的机制的术语。这意味着我们真正初始化

`Stack< char const[7]>`

and use type `char const[7]` wherever `T` is used. For example, we may not push a string of different size, because it has a different type. For a detailed discussion see Section [[7.4]] on page [[115]].

> 并在使用“T”的任何地方使用类型“char const[7]”。例如，我们可能不会推送不同大小的字符串，因为它有不同的类型。有关详细讨论，请参见第[[115]]页第[[7.4]]节。

However, when passing arguments of a template type `T` by value, the parameter _decays_, which is the term for the mechanism to convert a raw array type to the corresponding raw pointer type. That is, the call parameter `T` of the constructor is deduced to be `char const*` so that the whole class is deduced to be a `Stack<char const*>`.

> 然而，当按值传递模板类型“T”的参数时，参数_decays_是将原始数组类型转换为相应原始指针类型的机制的术语。也就是说，构造函数的调用参数“T”被推导为“char const*”，从而整个类被推导为一个“Stack＜char const*＞”。

For this reason, it might be worthwhile to declare the constructor so that the argument is passed by value:

> 出于这个原因，可能值得声明构造函数，以便按值传递参数：

```cpp
template<typename T>
class Stack {
   private:\
      std::vector<T> elems;    // elements
   public:
      `Stack (T elem)`           // initialize stack with one element by value
      `: elems() \
     }
    ...
};
```

With this, the following initialization works fine:

```cpp
Stack stringStack = "bottom"; // `Stack<char const*>` deduced since C++17
```

In this case, however, we should better move the temporary `elem` into the stack to avoid unnecessarily copying it:

> 然而，在这种情况下，我们应该更好地将临时“elem”移动到堆栈中，以避免不必要地复制它：

```cpp
template<typename T>
class Stack {
    private:\
       std::vector<T> elems;        // elements
    public:
       `Stack (T elem)`               // initialize stack with one element by value
        `: elems() `\
    ...
};
```

##### Deduction Guides

Instead of declaring the constructor to be called by value, there is a different solution: Because handling raw pointers in containers is a source of trouble, we should disable automatically deducing raw character pointers for container classes.

> 有一个不同的解决方案，而不是声明构造函数由值调用：因为处理容器中的原始指针是麻烦的根源，所以我们应该禁用自动推导容器类的原始字符指针。

You can define specific _deduction guides_ to provide additional or fix existing class template argument deductions. For example, you can define that whenever a string literal or C string is passed, the stack is instantiated for `std::string`:

> 您可以定义特定的推导指南_以提供额外的或修复现有的类模板参数推导。例如，您可以定义每当传递字符串文字或 C 字符串时，堆栈都会实例化为“std:：string”：

```cpp
`Stack( char const*) -> Stack<std::string>;`
```

This guide has to appear in the same scope (namespace) as the class definition. Usually, it follows the class definition. We call the type following the `->` the _guided type_ of the deduction guide.

> 本指南必须出现在与类定义相同的范围(命名空间)中。通常，它遵循类定义。我们将 `->` 后面的类型称为演绎指南的_guided type_。

Now, the declaration with

```cpp
Stack stringStack[};        // OK: `Stack<std::string>` deduced since C++17
```

deduces the stack to be a `Stack<std::string>`. However, the following still doesn't work:

> 将堆栈推导为 `stack<std:：string>`。但是，以下仍然不起作用：

```cpp
Stack stringStack = "bottom"; // `Stack<std::string>` deduced, but still not valid
```

We deduce `std::string` so that we instantiate a `Stack<std::string>`:

class Stack {
   private:
      std::vector[std::string](std::string) elems;        // elements
   public:

      Stack (std::string const& elem)        // initialize stack with one element

> 堆栈(std:：string const&elem)//用一个元素初始化堆栈
>       : elems() {
>     }
>     ...
> };

However, by language rules, you can't copy initialize (initialize using `=`) an object by passing a string literal to a constructor expecting a `std::string`. So you have to initialize the stack as follows:

> 但是，根据语言规则，不能通过将字符串文本传递给需要“std:：string”的构造函数来复制 initialize(使用“=”初始化)对象。因此，您必须按如下方式初始化堆栈：

```cpp
Stack stringStack[}; // `Stack<std::string>` deduced and valid
```

Note that, if in doubt, class template argument deduction copies. After declaring `stringStack` as `Stack<std::string>` the following initializations declare the same type (thus, calling the copy constructor) instead of initializing a stack by elements that are string stacks:

> 请注意，如果有疑问，类模板参数推导会复制。在将“stringStack”声明为“Stack＜std:：string＞”之后，以下初始化声明相同的类型(因此，调用复制构造函数)，而不是通过作为字符串堆栈的元素初始化堆栈：

```cpp
`Stack stack2;`        // `Stack<std::string>` deduced
`Stack stack3(stringStack);`        // `Stack<std::string>` deduced
`Stack stack4 = ;`     // `Stack<std::string>` deduced
```

See Section [[15.12]] on page [[313]] for more details about class template argument deduction.

> 有关类模板参数推导的更多详细信息，请参见第[[313]]页第[[15.12]]节。

### 2.10 Templatized Aggregates

Aggregate classes (classes/structs with no user-provided, explicit, or inherited constructors, no private or protected nonstatic data members, no virtual functions, and no virtual, private, or protected base classes) can also be templates. For example:

> 聚合类(没有用户提供的、显式的或继承的构造函数，没有私有或受保护的非静态数据成员，没有虚拟函数，也没有虚拟的、私有的或受保护基类的类/结构)也可以是模板。例如

```cpp
template<typename T>
struct ValueWithComment {
    T value;\
    std::string comment;\
};
```

defines an aggregate parameterized for the type of the value `val` it holds. You can declare objects as for any other class template and still use it as aggregate:

> 为它所持有的值“val”的类型定义了一个参数化的聚合。您可以将对象声明为任何其他类模板，但仍将其用作聚合：

```cpp
ValueWithComment< int> vc;\
vc.value = 42;\
vc.comment = "initial value";
```

Since C++17, you can even define deduction guides for aggregate class templates:

> 从 C++17 开始，您甚至可以为聚合类模板定义推导指南：

```cpp
`ValueWithComment( char const*, char const*)`\
  -> ValueWithComment<std::string>;\
ValueWithComment vc2 = [, "initial value"};
```

Without the deduction guide, the initialization would not be possible, because `ValueWithComment` has no constructor to perform the deduction against.

> 如果没有推导指南，初始化是不可能的，因为“ValueWithComment”没有可用于执行推导的构造函数。

The standard library class `std::array<>` is also an aggregate, parameterized for both the element type and the size. The C++17 standard library also defines a deduction guide for it, which we discuss in Section [[4.4.4]] on page [[64]].

> 标准库类“std:：array＜＞”也是一个聚合，对元素类型和大小都进行了参数化。C++17 标准库还为其定义了一个推导指南，我们将在第[[64]]页的第[[4.4.4]]节中对此进行讨论。

### 2.11 Summary

```cpp
  - A class template is a class that is implemented with one or more type parameters left open.
  - To use a class template, you pass the open types as template arguments. The class template is then instantiated (and compiled) for these types.
  - For class templates, only those member functions that are called are instantiated.
  - You can specialize class templates for certain types.
  - You can partially specialize class templates for certain types.
  - Since C++17, class template arguments can automatically be deduced from constructors.
  - You can define aggregate class templates.
  - Call parameters of a template type decay if declared to be called by value.
  - Templates can only be declared and defined in global/namespace scope or inside class declarations.

^[1]^ C++17 introduced class argument template deduction, which allows skipping template arguments if they can be derived from the constructor. This will be discussed in Section [[2.9]] on page [[40]].
^[2]^ It is a *templated entity*, see Section [[12.1]] on page [[181]].
^[3]^ Using the word *typedef* instead of "type definition" in intentional. The keyword `typedef` was originally meant to suggest "type definition." However, in C++, "type definition" really means something else (e.g., the definition of a class or enumeration type). Instead, a *typedef* should just be thought of as an alternative name (an "alias") for an existing type, which can be done by a `typedef`.
^[4]^ Alias templates are sometimes (incorrectly) referred to as *typedef templates* because they fulfill the same role that a `typedef` would if it could be made into a template.
^[5]^ The `typename` is necessary here because the member is a type. See Section [[5.1]] on page [[67]] for details.
^[6]^ Even worse, there is a vector constructor taking one integral argument as initial size, so that for a stack with the initial value `5`, the vector would get an initial size of five elements when `: elems(elem)` is used.
```

## Chapter 3

## Nontype Template Parameters

For function and class templates, template parameters don't have to be types. They can also be ordinary values. As with templates using type parameters, you define code for which a certain detail remains open until the code is used. However, the detail that is open is a value instead of a type. When using such a template, you have to specify this value explicitly. The resulting code then gets instantiated. This chapter illustrates this feature for a new version of the stack class template. In addition, we show an example of nontype function template parameters and discuss some restrictions to this technique.

> 对于函数和类模板，模板参数不必是类型。它们也可以是普通值。与使用类型参数的模板一样，您可以定义某些详细信息在使用代码之前保持打开状态的代码。但是，打开的详细信息是一个值，而不是类型。使用这样的模板时，必须显式指定此值。生成的代码随后被实例化。本章说明了新版本的堆栈类模板的这一功能。此外，我们还展示了一个非类型函数模板参数的示例，并讨论了对该技术的一些限制。

### 3.1 Nontype Class Template Parameters

In contrast to the sample implementations of a stack in previous chapters, you can also implement a stack by using a fixed-size array for the elements. An advantage of this method is that the memory management overhead, whether performed by you or by a standard container, is avoided. However, determining the best size for such a stack can be challenging. The smaller the size you specify, the more likely it is that the stack will get full. The larger the size you specify, the more likely it is that memory will be reserved unnecessarily. A good solution is to let the user of the stack specify the size of the array as the maximum size needed for stack elements.

> 与前几章中的堆栈示例实现不同，您还可以通过为元素使用固定大小的数组来实现堆栈。这种方法的一个优点是避免了内存管理开销，无论是由您还是由标准容器执行。然而，确定这种堆栈的最佳大小可能具有挑战性。指定的大小越小，堆栈越有可能被填满。指定的大小越大，内存被不必要地保留的可能性就越大。一个好的解决方案是让堆栈的用户将数组的大小指定为堆栈元素所需的最大大小。

To do this, define the size as a template parameter:

```cpp
`basics/stacknontype.hpp`

#include <array>
#include <cassert>

template<typename T, std::size_t Maxsize>
class Stack {
  private:\
    std::array<T,Maxsize> elems; // elements
    std::size_t numElems;        // current number of elements
   public:
    Stack();                     // constructor
    void push(T const& elem);    // push element
    void pop();                  // pop element
    T const& top() const;        // return top element
    [bool] empty() const \
        return numElems == 0;\
    }
    std::size_t size() const \
        return numElems;\
    }
};

template<typename T, std::size_t Maxsize>
Stack<T,Maxsize>::Stack ()
 : numElems(0)                 //start with no elements
{
   // nothing else to do
}

template<typename T, std::size_t Maxsize>
void Stack<T,Maxsize>::push (T const& elem)
{
    assert(numElems < Maxsize);
    elems[numElems] = elem;    // append element
    ++numElems;                // increment number of elements
}

template<typename T, std::size_t Maxsize>
void Stack<T,Maxsize>::pop ()
{
    assert(!elems.empty());
    \--numElems;                // decrement number of elements
}

template<typename T, std::size_t Maxsize>
T const& Stack<T,Maxsize>::top () const\
{
    assert(!elems.empty());
    return elems[numElems-1];  // return last element
}
```

The new second template parameter, `Maxsize`, is of type `int`. It specifies the size of the internal array of stack elements:

> 新的第二个模板参数“Maxsize”的类型为“int”。它指定堆栈元素的内部数组的大小：

```cpp
template<typename T, std::size_t Maxsize>
class Stack {
  private:\
    std::array<T,Maxsize> elems; // elements
    ...
};
```

In addition, it is used in `push()` to check whether the stack is full:

```cpp
template<typename T, std::size_t Maxsize>
void Stack<T,Maxsize>::push (T const& elem)
{
    assert(numElems < Maxsize);
    elems[numElems] = elem;   // append element     ++numElems;               // increment number of elements
}
```

To use this class template you have to specify both the element type and the maximum size:

> 若要使用此类模板，必须同时指定元素类型和最大大小：

```cpp
`basics/stacknontype.cpp`

#include "stacknontype.hpp"\
#include <iostream>
#include <string>

int main()
{
  Stack<int,20>         int20Stack;      // stack of up to 20 ints
  Stack<int,40>         int40Stack;      // stack of up to 40 ints
  Stack<std::string,40> stringStack;     // stack of up to 40 strings

  // manipulate stack of up to 20 ints
  int20Stack.push(7);
  std::cout << int20Stack.top() << '\n';\
  int20Stack.pop();

  // manipulate stack of up to 40 strings
  stringStack.push("hello");
  std::cout << stringStack.top() << '\n';\
  stringStack.pop();
}
```

Note that each template instantiation is its own type. Thus, `int20Stack` and `int40Stack` are two different types, and no implicit or explicit type conversion between them is defined. Thus, one cannot be used instead of the other, and you cannot assign one to the other.

> 请注意，每个模板实例化都是其自己的类型。因此，“int20Stack”和“int40Stack”是两种不同的类型，它们之间没有定义隐式或显式的类型转换。因此，不能使用一个来代替另一个，也不能将一个分配给另一个。

Again, default arguments for the template parameters can be specified:

```cpp
template<typename T = int, std::size_t Maxsize = 100>
class Stack {
  ...
};
```

However, from a perspective of good design, this may not be appropriate in this example. Default arguments should be intuitively correct. But neither type `int` nor a maximum size of 100 seems intuitive for a general stack type. Thus, it is better when the programmer has to specify both values explicitly so that these two attributes are always documented during a declaration.

> 然而，从良好设计的角度来看，这在本例中可能不合适。默认参数应该直观正确。但对于一般堆栈类型来说，类型“int”和最大大小 100 似乎都不直观。因此，最好是程序员必须显式指定这两个值，以便在声明过程中始终记录这两个属性。

### 3.2 Nontype Function Template Parameters

You can also define nontype parameters for function templates. For example, the following function template defines a group of functions for which a certain value can be added:

> 还可以为函数模板定义非类型参数。例如，以下函数模板定义了一组可以添加特定值的函数：

```cpp
`basics/addvalue.hpp`

template<int Val, typename T>
T addValue (T x)
{
  return x + Val;\
}
```

These kinds of functions can be useful if functions or operations are used as parameters. For example, if you use the C++ standard library you can pass an instantiation of this function template to add a value to each element of a collection:

> 如果函数或操作被用作参数，这些类型的函数可能是有用的。例如，如果您使用 C++ 标准库，您可以传递此函数模板的实例化，以向集合的每个元素添加一个值：

```cpp
std::transform (source.begin(), source.end(),  //start and end of source
                dest.begin(),                  //start of destination
                addValue<5,int>);              // operation
```

The last argument instantiates the function template `addValue<>()` to add 5 to a passed `int` value. The resulting function is called for each element in the source collection `source`, while it is translated into the destination collection `dest`.

> 最后一个参数实例化函数模板“addValue＜＞()”，以便将 5 添加到传递的“int”值中。为源集合“source”中的每个元素调用生成的函数，同时将其转换为目标集合“dest”。

Note that you have to specify the argument `int` for the template parameter `T` of `addValue<>()`. Deduction only works for immediate calls and `std::transform()` need a complete type to deduce the type of its fourth parameter. There is no support to substitute/deduce only some template parameters and the see, what could fit, and deduce the remaining parameters.

> 请注意，必须为“addValue＜＞()”的模板参数“T”指定参数“int”。推导只适用于立即调用，“std:：transform()”需要一个完整的类型来推导其第四个参数的类型。不支持仅替换/推导一些模板参数，并查看可以拟合的内容，然后推导其余参数。

Again, you can also specify that a template parameter is deduced from the previous parameter. For example, to derive the return type from the passed nontype:

> 同样，您也可以指定从上一个参数推导出模板参数。例如，要从传递的非类型派生返回类型：

```cpp
template<auto Val, typename T = decltype(Val)>
T foo();
```

or to ensure that the passed value has the same type as the passed type:

```cpp
template<typename T, T Val = T>
T bar();
```

### 3.3 Restrictions for Nontype Template Parameters

Note that nontype template parameters carry some restrictions. In general, they can be only constant integral values (including enumerations), pointers to objects/functions/members, lvalue references to objects or functions, or `std::nullptr_t` (the type of `nullptr`).

> 请注意，非类型模板参数有一些限制。通常，它们只能是常量整数值(包括枚举)、指向对象/函数/成员的指针、指向对象或函数的左值引用或“std:：nullptr_t”(“nullptr”的类型)。

Floating-point numbers and class-type objects are not allowed as nontype template parameters:

> 浮点数字和类类型对象不允许作为非类型模板参数：

```cpp
template<[double] VAT>         // ERROR: floating-point values are not
[double] process [(double] v)    //        allowed as template parameters
{
    return v \* VAT;\
}

template<std::string name>   // ERROR: class-type objects are not
class MyClass \
  ...
};
```

When passing template arguments to pointers or references, the objects must not be string literals, temporaries, or data members and other subobjects. Because these restrictions were relaxed with each and every C++ version before C++17, additional constraints apply:

> 将模板参数传递给指针或引用时，对象不能是字符串文字、临时对象或数据成员和其他子对象。因为在 C++17 之前的每个 C++ 版本都放宽了这些限制，所以还适用其他限制：

• In C++11, the objects also had to have external linkage.
• In C++14, the objects also had to have external or internal linkage.

Thus, the following is not possible:

```cpp
template<[char const]\* name>
class MyClass {
  ...
};

MyClass<"hello"> x;  //ERROR: string literal "hello" not allowed
```

However there are workarounds (again depending on the C++ version):

```cpp
[extern char const] s03[] = "hi";    // external linkage
[char const] s11[] = "hi";           // internal linkage

int main()
{
  Message<s03> m03;                // OK (all versions)
  Message<s11> m11;                // OK since C++11
   [static char const] s17[] = "hi";  // no linkage
  Message<s17> m17;                // OK since C++17
}
```

In all three cases a constant character array is initialized by `"hello"` and this object is used as a template parameter declared with `char const*`. This is valid in all C++ versions if the object has external linkage (`s03`), in C++11 and C++14 also if it has internal linkage (`s11`), and since C++17 if it has no linkage at all.

> 在这三种情况下，常量字符数组都由“hello”初始化，该对象用作用“char const*”声明的模板参数。如果对象具有外部链接(“s03”)，则这在所有 C++ 版本中都是有效的，在 C++11 和 C++14 中，如果它具有内部链接(“s11”)，并且由于 C++17，如果它根本没有链接。

See Section [[12.3.3]] on page [[194]] for a detailed discussion and Section [[17.2]] on page [[354]] for a discussion of possible future changes in this area.

> 有关详细讨论，请参见第[[194]]页第[[12.3.3]]节，有关该领域未来可能发生的变化的讨论，请参阅第[[354]]页第[17.2]]节。

#### Avoiding Invalid Expressions

Arguments for nontype template parameters might be any compile-time expressions. For example:

> 非类型模板参数的参数可以是任何编译时表达式。例如

```cpp
template<int I, [bool] B>
class C;\
...
C<[sizeof](int) + 4, [sizeof][(int])==4> c;
```

However, note that if `operator>` is used in the expression, you have to put the whole expression into parentheses so that the nested `>` ends the argument list:

> 但是，请注意，如果表达式中使用了“operator>”，则必须将整个表达式放在括号中，以便嵌套的“>”结束参数列表：

```cpp
C<42, [sizeof][(int]) > 4> c;    // ERROR: first [>] ends the template argument list
C<42, [(sizeof][(int]) > 4)> c;  // OK
```

### 3.4 Template Parameter Type **auto**

Since C++17, you can define a nontype template parameter to generically accept any type that is allowed for a nontype parameter. Using this feature, we can provide an even more generic stack class with fixed size:

> 从 C++17 开始，您可以定义一个非类型模板参数，以通用方式接受非类型参数所允许的任何类型。使用此功能，我们可以提供一个更通用的固定大小堆栈类：

```cpp
`basics/stackauto.hpp`

#include <array>
#include <cassert>

template<typename T, auto Maxsize>
class Stack {
  public:
    using size_type = decltype(Maxsize);
  private:\
    std::array<T,Maxsize> elems; // elements
    size_type numElems;          // current number of elements
   public:
    Stack();                     // constructor
    void push(T const& elem);    // push element
    void pop();                  // pop element
    T const& top() const;        // return top element
    [bool] empty() const \
        return numElems == 0;\
    }
    size_type size() const \
        return numElems;\
    }
};

// constructor
template<typename T, auto Maxsize>
Stack<T,Maxsize>::Stack ()
 : numElems(0)                 //start with no elements
{
    // nothing else to do
}

template<typename T, auto Maxsize>
void Stack<T,Maxsize>::push (T const& elem)
{
    assert(numElems < Maxsize);
    elems[numElems] = elem;   // append element
    ++numElems;               // increment number of elements
}

template<typename T, auto Maxsize>
void Stack<T,Maxsize>::pop ()
{
    assert(!elems.empty());
    \--numElems;                // decrement number of elements
}

template<typename T, auto Maxsize>
T const& Stack<T,Maxsize>::top () const\
{
    assert(!elems.empty());
    return elems[numElems-1];  // return last element
}
```

By defining

```cpp
template<typename T, auto Maxsize>
class Stack {
  ...
};
```

by using the _placeholder type_ `auto`, you define `Maxsize` to be a value of a type not specified yet. It might be any type that is allowed to be a nontype template parameter type.

> 通过使用_placeholder type_`auto`，可以将“Maxsize”定义为尚未指定的类型的值。它可以是允许作为非类型模板参数类型的任何类型。

Internally you can use both the value:

```cpp
std::array<T,Maxsize> elems;     // elements
```

and its type:

```cpp
    using size_type = decltype(Maxsize);
```

which is then, for example, used as return type of the `size()` member function:

> 例如，它被用作“size()”成员函数的返回类型：

```cpp
size_type size() const \
    return numElems;\
}
```

Since C++14, you could also just use `auto` here as return type to let the compiler find out the return type:

> 由于 C++14，您也可以在这里使用“auto”作为返回类型，让编译器找出返回类型：

```cpp
auto size() const \
    return numElems;\
}
```

With this class declaration the type of the number of elements is defined by the type used for the number of elements, when using a stack:

> 使用此类声明时，元素数量的类型由用于元素数量的类别定义，当使用堆栈时：

```cpp
`basics/stackauto.cpp`

#include <iostream>
#include <string>
#include "stackauto.hpp"\

int main()
{
  Stack<int,20u>        int20Stack;     // stack of up to 20 ints
  Stack<std::string,40> stringStack;    // stack of up to 40 strings

  // manipulate stack of up to 20 ints
  int20Stack.push(7);
  std::cout << int20Stack.top() << '\n';\
  auto size1 = int20Stack.size();

  // manipulate stack of up to 40 strings
   stringStack.push("hello");
  std::cout << stringStack.top() << '\n';\
  auto size2 = stringStack.size();

  if (!std::is_same_v[<decltype](size1), decltype(size2)>) {
    std::cout << "size types differ" << '\n';\
  }
}
```

With

```cpp
`Stack<int,20u> int20Stack;`        // stack of up to 20 `int`s
```

the internal size type is `unsigned int`, because `20u` is passed.

With

```cpp
`Stack<std::string,40> stringStack;`   // stack of up to 40 strings
```

the internal size type is `int`, because `40` is passed.

`size()` for the two stacks will have different return types, so that after

```cpp
    auto size1 = int20Stack.size();
    ...
    auto size2 = stringStack.size();
```

the types of `size1` and `size2` differ. By using the standard type trait `std::is_same` (see Section [[D.3.3]] on page [[726]]) and `decltype`, we can check that:

> “size1”和“size2”的类型不同。通过使用标准类型特征“std:：is_same”(请参见第[[726]]页的第[[D.3.3]]节)和“decltype”，我们可以检查：

```cpp
if (!std::is_same[<decltype](size1), decltype(size2)>::value) {
  std::cout << "size types differ" << '\n';\
}
```

Thus, the output will be:

size types differ

Since C++17, for traits returning values, you can also use the suffix `_v` and skip `::value` (see Section [[5.6]] on page [[83]] for details):

> 由于 C++17，对于返回值的特征，您也可以使用后缀“_v”和跳过“：：value”(有关详细信息，请参见第[[83]]页的第[[5.6]]节)：

```cpp
if (!std::is_same_v[<decltype](size1), decltype(size2)>) {
  std::cout << "size types differ" << '\n';\
}
```

Note that other constraints on the type of nontype template parameters remain in effect. Especially, the restrictions about possible types for nontype template arguments discussed in Section [[3.3]] on page [[49]] still apply. For example:

> 请注意，对非类型模板参数类型的其他约束仍然有效。特别是，第[[49]]页第[[3.3]]节中讨论的关于非类型模板参数的可能类型的限制仍然适用。例如

```cpp
`Stack<int,3.14> sd;`        // ERROR: Floating-point nontype argument
```

And, because you can also pass strings as constant arrays (since C++17 even static locally declared; see Section [[3.3]] on page [[49]]), the following is possible:

> 而且，因为您也可以将字符串作为常量数组传递(由于 C++17 甚至是静态的本地声明；请参阅第[[49]]页的第[[3.3]]节)，所以以下内容是可能的：

```cpp

`basics/message.cpp`

#include <iostream>

template<auto T>       // take value of any possible nontype parameter (since C++17)
class Message {
  public:
    void print() {
      std::cout << T << '\n';\
    }
};

int main()
{
  Message<42> msg1;\
  msg1.print();        // initialize with int 42 and print that value

  [static char const] s[] = "hello";\
  Message<s> msg2;     // initialize with [char const[6] \"hello"\
  msg2.print();        // and print that value
}
```

Note also that even `template<decltype(auto) N>` is possible, which allows instantiation of `N` as a reference:

> 还要注意，甚至“template＜decltype(auto)N＞”也是可能的，这允许实例化“N”作为引用：

```cpp
template<decltype(auto) N>
class C {
  ...
};

int i;\
C<(i)> x;  // [N] is [int&]
```

See Section [[15.10.1]] on page [[296]] for details.

### 3.5 Summary

```cpp
  - Templates can have template parameters that are values rather than types.
  - You cannot use floating-point numbers or class-type objects as arguments for nontype template parameters. For pointers/references to string literals, temporaries, and subobjects, restrictions apply.
  - Using `auto` enables templates to have nontype template parameters that are values of generic types.
```

## Chapter 4

## Variadic Templates

Since C++11, templates can have parameters that accept a variable number of template arguments. This feature allows the use of templates in places where you have to pass an arbitrary number of arguments of arbitrary types. A typical application is to pass an arbitrary number of parameters of arbitrary type through a class or framework. Another application is to provide generic code to process any number of parameters of any type.

> 从 C++11 开始，模板的参数可以接受数量可变的模板参数。此功能允许在必须传递任意数量的任意类型参数的地方使用模板。一个典型的应用程序是通过类或框架传递任意数量的任意类型的参数。另一个应用是提供通用代码来处理任意数量的任意类型的参数。

### 4.1 Variadic Templates

Template parameters can be defined to accept an unbounded number of template arguments. Templates with this ability are called _variadic templates_.

> 模板参数可以定义为接受无限数量的模板参数。具有此功能的模板称为_variadic Templates_。

#### 4.1.1 Variadic Templates by Example

For example, you can use the following code to call `print()` for a variable number of arguments of different types:

> 例如，您可以使用以下代码为不同类型的可变数量的参数调用“print()”：

```cpp
`basics/varprint1.hpp`

#include <iostream>

void print ()
{
}

template<typename T, typename... Types>
void print (T firstArg, Types... args)
{
  std::cout << firstArg << '\n';  //print first argument
  print(args...);                 // call print() for remaining arguments
}
```

If one or more arguments are passed, the function template is used, which by specifying the first argument separately allows printing of the first argument before recursively calling `print()` for the remaining arguments. These remaining arguments named `args` are a _function parameter pack_:

> 如果传递了一个或多个参数，则使用函数模板，通过单独指定第一个参数，可以在递归调用其余参数的“print()”之前打印第一个参数。剩下的这些名为“args”的参数是一个函数参数包_：

```cpp
void print (T firstArg, Types... args)
```

using different "`Types`" specified by a _template parameter pack_:

```cpp
template<typename T, typename... Types>
```

To end the recursion, the nontemplate overload of `print()` is provided, which is issued when the parameter pack is empty.

> 为了结束递归，提供了“print()”的非模板重载，该重载在参数包为空时发出。

For example, a call such as

```cpp
std::string s[(\"world");
print (7.5, "hello", s);
```

would output the following:

```cpp
7.5\
hello\
world
```

The reason is that the call first expands to

```cpp
print<[double], [char const]\*, std::string> (7.5, "hello", s);
```

with

- `firstArg` having the value `7.5` so that type `T` is a `double` and
- `args` being a variadic template argument having the values `"hello"` of type `char const*` and `"world"` of type `std::string`.

> -args 是一个可变模板参数，具有类型为 char const*的值“hello”和类型为 std:：string 的值“world”。

After printing `7.5` as `firstArg`, it calls `print()` again for the remaining arguments, which then expands to:

> 在将“7.5”打印为“firstArg”后，它将再次为其余参数调用“print()”，然后扩展为：

```cpp
print<[char const]\*, std::string> [(\"hello", s);
```

with

- `firstArg` having the value `"hello"` so that type `T` is a `char const*` here and
- `args` being a variadic template argument having the value of type `std::string`.

After printing `"hello"` as `firstArg`, it calls `print()` again for the remaining arguments, which then expands to:

> 在将“hello”打印为“firstArg”后，它将再次为其余参数调用“print()”，然后扩展为：

```cpp
print<std::string> (s);
```

with

- `firstArg` having the value `"world"` so that type `T` is a `std::string` now and
- `args` being an empty variadic template argument having no value.

Thus, after printing `"world"` as `firstArg`, we calls `print()` with no arguments, which results in calling the nontemplate overload of `print()` doing nothing.

> 因此，在将“world”打印为“firstArg”后，我们在没有参数的情况下调用“print()”，这导致调用“print”()的非模板重载时无所作为。

#### 4.1.2 Overloading Variadic and Nonvariadic Templates

Note that you can also implement the example above as follows:

```cpp
`basics/varprint2.hpp`

#include <iostream>

template<typename T>
void print (T arg)
{
  std::cout << arg << '\n';  //print passed argument
}

template<typename T, typename... Types>
void print (T firstArg, Types... args)
{
  print(firstArg);                // call* print()] for the first argument
  print(args...);                 // call print() for remaining arguments
}
```

That is, if two function templates only differ by a trailing parameter pack, the function template without the trailing parameter pack is preferred.[1] Section [[C.3.1]] on page [[688]] explains the more general overload resolution rule that applies here.

> 也就是说，如果两个函数模板仅相差一个尾随参数包，则优选不包含尾随参数包的函数模板。[1] 第[[688]]页第[[C.3.1]]节解释了此处适用的更通用的过载解决规则。

#### 4.1.3 Operator **sizeof...**

C++11 also introduced a new form of the `sizeof` operator for variadic templates: sizeof.... It expands to the number of elements a parameter pack contains. Thus,

> C++11 还为可变模板引入了一种新形式的“sizeof”运算符：sizeof。。。。它扩展到参数包包含的元素数。因此

```cpp
template<typename T, typename... Types>
void print (T firstArg, Types... args)
{
  std::cout << [sizeof]...(Types) << '\n';  //print number of remaining types
  std::cout << [sizeof]...(args) << '\n';   //print number of remaining args
  ...
}
```

twice prints the number of remaining arguments after the first argument passed to `print()`. As you can see, you can call `sizeof…` for both template parameter packs and function parameter packs.

> 两次打印传递给“print()”的第一个参数之后的剩余参数数。正如您所看到的，您可以为模板参数包和函数参数包调用“sizeof…”。

This might lead us to think we can skip the function for the end of the recursion by not calling it in case there are no more arguments:

> 这可能会导致我们认为，在没有更多参数的情况下，我们可以通过不调用该函数来跳过递归结束时的函数：

```cpp
template<typename T, typename... Types>
void print (T firstArg, Types... args)
{
  std::cout << firstArg << '\n';\
  if [(sizeof]...(args) > 0)  [sizeof...(args)==0]\
    print(args...);               // and no print() for no arguments declared
  }
}
```

However, this approach doesn't work because in general both branches of all _if_ statements in function templates are instantiated. Whether the instantiated code is useful is a _run-time_ decision, while the instantiation of the call is a _compile-time_ decision. For this reason, if you call the `print()` function template for one (last) argument, the statement with the call of `print(args…)` still is instantiated for no argument, and if there is no function `print()` for no arguments provided, this is an error.

> 然而，这种方法不起作用，因为通常情况下，函数模板中所有_if_语句的两个分支都是实例化的。实例化的代码是否有用是一个_run-time_决策，而调用的实例化是一个_compile-time_决定。因此，如果您为一个(最后一个)参数调用“print()”函数模板，则调用为“print(args…)”的语句仍会在没有参数的情况下实例化，如果没有为没有提供的参数提供函数“print(()”，则这是一个错误。

However, note that since C++17, a compile-time `if` is available, which achieves what was expected here with a slightly different syntax. This will be discussed in Section [[8.5]] on page [[134]].

> 然而，请注意，自 C++17 以来，编译时“if”是可用的，它以略微不同的语法实现了预期的效果。这将在第[[134]]页的第[[8.5]]节中进行讨论。

### 4.2 Fold Expressions

Since C++17, there is a feature to compute the result of using a binary operator over _all_ the arguments of a parameter pack (with an optional initial value).

> 自从 C++17 以来，有一个功能可以计算在参数包的_all_参数上使用二进制运算符的结果(具有可选的初始值)。

For example, the following function returns the sum of all passed arguments:

> 例如，以下函数返回所有传递参数的总和：

```cpp
template<typename... T>
auto foldSum (T... s) {
  return (... + s);   // [((s1 + s2) + s3)] [...]\
}
```

If the parameter pack is empty, the expression is usually ill-formed (with the exception that for operator `&&` the value is `true`, for operator `||` the value is `false`, and for the comma operator the value for an empty parameter pack is `void()`).

> 如果参数包为空，则表达式的格式通常不正确(除了运算符“&&”的值为“true”，运算符“||”的值是“false”，逗号运算符的空参数包的值为为“void()”)。

Table [[4.1]] lists the possible fold expressions.

**Fold Expression** **Evaluation**

---

`( …` _op pack_ `)` `(((` _pack1 op pack2_ `)` _op pack3_ `)` ... _op packN_ `)`
`(` _pack op_ `… )` `(` _pack1 op_ `(` ... `(` _packN-1 op packN_ `)))`
`(` _init op_ `…` _op pack_ `)` `(((` _init op pack1_ `)` _op pack2_ `)` ... _op packN_ `)`
`(` _pack op_ `…` _op init_ `)` `(` _pack1 op_ `(` ... `(` _packN op init_ `)))`

_Table 4.1. Fold Expressions (since C++17)_

You can use almost all binary operators for fold expressions (see Section [[12.4.6]] on page [[208]] for details). For example, you can use a fold expression to traverse a path in a binary tree using operator `->*`:

> 您可以将几乎所有的二进制运算符用于折叠表达式(有关详细信息，请参见第[[208]]页的第[[12.4.6]]节)。例如，您可以使用 fold 表达式使用运算符“->*”遍历二叉树中的路径：

```cpp
`basics/foldtraverse.cpp`

*[// define binary tree structure and traverse helpers:]*\
struct Node {
  int value;\
  Node\* left;\
  Node\* right;\
  Node(int i=0) : value(i), left[(nullptr]), right[(nullptr]) {
  }
  ...
};
auto left = &Node::left;\
auto right = &Node::right;\

*[// traverse tree, using fold expression:]*\
template<typename T, typename... TP>
Node\* traverse (T np, TP... paths) {
  return (np ->\* ... ->\* paths); *[//]* [np ->\* paths1 ->\* paths2 *...
}

int main()
{
  *[// init binary tree structure:]*\
  Node\* root = [new] Node;\
  root->left = [new] Node;\
  root->left->right = [new] Node;\
  ...
  // traverse binary tree:
  Node\* node = traverse(root, left, right);
  ...
}
```

Here,

`(np ->* … ->* paths)`

uses a fold expression to traverse the variadic elements of `paths` from `np`.

> 使用折叠表达式从“np”遍历“path”的变元。

With such a fold expression using an initializer, we might think about simplifying the variadic template to print all arguments, introduced above:

> 有了这样一个使用初始化器的 fold 表达式，我们可能会考虑简化 varadic 模板来打印上面介绍的所有参数：

```cpp
template<typename... Types>
void print (Types const&... args)
{
  (std::cout << ... << args) << '\n';\
}
```

However, note that in this case no whitespace separates all the elements from the parameter pack. To do that, you need an additional class template, which ensures that any output of any argument is extended by a space:

> 但是，请注意，在这种情况下，没有空格将参数包中的所有元素分隔开。要做到这一点，您需要一个额外的类模板，它可以确保任何参数的任何输出都扩展了一个空格：

```cpp
`basics/addspace.hpp`

template<typename T>
class AddSpace\
{
  private:\
    T const& ref;*                  [// refer to argument passed in constructor]*\
  public:
    AddSpace(T const& r): ref(r) {
    }
    [friend] std::ostream& [operator]<< (std::ostream& os, AddSpace<T> s) {
      return os << s.ref <<[''];*   [// output passed argument and a space]*\
    }
};

template<typename... Args>
void print (Args... args) {
  ( std::cout << ... << AddSpace(args) ) << '\n';\
}

\
```

Note that the expression `AddSpace(args)` uses class template argument deduction (see Section [[2.9]] on page [[40]]) to have the effect of `AddSpace<Args>(args)`, which for each argument creates an `AddSpace` object that refers to the passed argument and adds a space when it is used in output expressions.

> 请注意，表达式“AddSpace(args)”使用类模板参数推导(请参见第[[40]]页的第[[2.9]]节)来产生“AddSpace＜args＞(args’)”的效果，它为每个参数创建一个“AddSpace”对象，该对象引用传递的参数，并在输出表达式中使用时添加一个空格。

See Section [[12.4.6]] on page [[207]] for details about fold expressions.

> 有关折叠表达式的详细信息，请参见第[[207]]页第[[12.4.6]]节。

### 4.3 Application of Variadic Templates

Variadic templates play an important role when implementing generic libraries, such as the C++ standard library.

> 变分模板在实现泛型库(如 C++ 标准库)时发挥着重要作用。

One typical application is the forwarding of a variadic number of arguments of arbitrary type. For example, we use this feature when:

> 一个典型的应用是转发任意类型的可变数量的参数。例如，我们在以下情况下使用此功能：

• Passing arguments to the constructor of a new heap object owned by a shared pointer:

> •将参数传递给共享指针所拥有的新堆对象的构造函数：

```cpp
// create shared pointer to `complex<float>` initialized by `4.2` and `7.7: auto sp = std::make_shared<std::complex<float>>(4.2, 7.7);`
```

• Passing arguments to a thread, which is started by the library:

```cpp
std::thread t (foo, 42, "hello");        //call [foo(42,\"hello\")] in a separate thread
```

• Passing arguments to the constructor of a new element pushed into a vector:

> •将参数传递给推入向量的新元素的构造函数：

```cpp
std::vector<Customer> v;\
...
v.emplace("Tim", "Jovi", 1962);        //insert a [Customer] initialized by three arguments
```

Usually, the arguments are "_perfectly forwarded_" with move semantics (see Section [[6.1]] on page [[91]]), so that the corresponding declarations are, for example:

> 通常，参数是具有移动语义的“_perfectly forwarded_”(请参见第[[91]]页第[[6.1]]节)，因此相应的声明是，例如：

```cpp
namespace std {
  template<typename T, typename... Args> shared_ptr<T>
  make_shared(Args&&... args);

  class thread {
   public:
    template<typename F, typename... Args>
    [explicit] thread(F&& f, Args&&... args);   
    ...
  };

  template<typename T, typename Allocator = allocator<T>>
  class vector {
   public:
    template<typename... Args> reference emplace_back(Args&&... args);
    ...
  };
}
```

Note also that the same rules apply to variadic function template parameters as for ordinary parameters. For example, if passed by value, arguments are copied and decay (e.g., arrays become pointers), while if passed by reference, parameters refer to the original parameter and don't decay:

> 还应注意，与普通参数相同的规则适用于可变函数模板参数。例如，如果通过值传递，参数会被复制并衰减(例如，数组变成指针)，而如果通过引用传递，参数则引用原始参数，而不会衰减：

```cpp
// [args] are copies with decayed types:
template<typename... Args> void foo (Args... args);
// [args] are nondecayed references to passed objects:
template<typename... Args> void bar (Args const&... args);
```

### 4.4 Variadic Class Templates and Variadic Expressions

Besides the examples above, parameter packs can appear in additional places, including, for example, expressions, class templates, using declarations, and even deduction guides. Section [[12.4.2]] on page [[202]] has a complete list.

> 除了上面的例子，参数包还可以出现在其他地方，例如，包括表达式、类模板、使用声明，甚至推导指南。第[[202]]页第[[12.4.2]]节有一份完整的清单。

#### 4.4.1 Variadic Expressions

You can do more than just forward all the parameters. You can compute with them, which means to compute with all the parameters in a parameter pack.

> 您可以做的不仅仅是转发所有参数。您可以使用它们进行计算，这意味着使用参数包中的所有参数进行计算。

For example, the following function doubles each parameter of the parameter pack `args` and passes each doubled argument to `print()`:

> 例如，以下函数将参数包“args”的每个参数加倍，并将每个加倍的参数传递给“print()”：

```cpp
template<typename... T>
void printDoubled (T const&... args)
{
  print (args + args...);
}
```

If, for example, you call

```cpp
`printDoubled(7.5, std::string("hello"), std::complex<float>(4,2));`
```

the function has the following effect (except for any constructor side effects):

> 该函数具有以下效果(构造函数的任何副作用除外)：

```cpp
print(7.5 + 7.5,\
      std::string("hello") + std::string[(\"hello"),\
      std::complex<[float]>(4,2) + std::complex[<float]>(4,2);
```

If you just want to add 1 to each argument, note that the dots from the ellipsis may not directly follow a numeric literal:

> 如果您只想在每个参数上加 1，请注意省略号中的点可能不会直接跟在数字文字后面：

```cpp
template<typename... T>
void addOne (T const&... args)
{
  print (args + 1...);    // ERROR: [1...] is a literal with too many decimal points
  print (args + 1 ...);   // OK
  print ((args + 1)...);  // OK
}
```

Compile-time expressions can include template parameter packs in the same way. For example, the following function template returns whether the types of all the arguments are the same:

> 编译时表达式可以以相同的方式包含模板参数包。例如，以下函数模板返回所有参数的类型是否相同：

```cpp
template<typename T1, typename... TN>
[constexpr bool] isHomogeneous (T1, TN...)
{
  return (std::is_same<T1,TN>::value && ...);  // since C++17
}
```

This is an application of fold expressions (see Section [[4.2]] on page [[58]]): For

> 这是折叠表达式的应用(见第[[58]]页第[[4.2]]节)：对于

```cpp
`isHomogeneous(43, -1, "hello")`
```

the expression for the return value expands to

```cpp
`std::is_same<int,int>::value && std::is_same<int,char const*>::value`
```

and yields `false`, while

```cpp
isHomogeneous("hello", "", "world", "!")
```

yields `true` because all passed arguments are deduced to be `char const*` (note that the argument types decay because the call arguments are passed by value).

> 产生“true”，因为所有传递的参数都被推导为“char const*”(请注意，参数类型会衰减，因为调用参数是按值传递的)。

#### 4.4.2 Variadic Indices

As another example, the following function uses a variadic list of indices to access the corresponding element of the passed first argument:

> 作为另一个示例，以下函数使用索引的可变列表来访问传递的第一个参数的相应元素：

```cpp
template<typename C, typename... Idx>
void printElems (C const& coll, Idx... idx)
{
  print (coll[idx]...);
}
```

That is, when calling

```cpp
std::vector<std::string> coll = [, "times", "say", "bye"}; printElems(coll,2,0,3);
```

the effect is to call

```cpp
`print (coll[2], coll[0], coll[3]);`
```

You can also declare nontype template parameters to be parameter packs. For example:

> 您还可以将非类型模板参数声明为参数包。例如

```cpp
template<std::size_t... Idx, typename C>
void printIdx (C const& coll)
{
  print(coll[Idx]...);
}
```

allows you to call

```cpp
`std::vector<std::string> coll = ; printIdx<2,0,3>(coll);`
```

which has the same effect as the previous example.

#### 4.4.3 Variadic Class Templates

Variadic templates can also be class templates. An important example is a class where an arbitrary number of template parameters specify the types of corresponding members:

> 变分模板也可以是类模板。一个重要的例子是一个类，其中任意数量的模板参数指定相应成员的类型：

```cpp
template<typename... Elements>
class Tuple;\

Tuple<int, std::string, [char]> t;    // [t] can hold integer, string, *and* character
```

This will be discussed in [Chapter [25]].

Another example is to be able to specify the possible types objects can have:

> 另一个例子是能够指定对象可能具有的类型：

```cpp
template<typename... Types>
class Variant;

`Variant<int, std::string, char> v;`        // `v` can hold integer, string, [or] character
```

This will be discussed in [Chapter [26]].

You can also define a class that _as a type_ represents a list of indices:

> 您还可以定义一个类，该类作为类型_表示索引列表：

```cpp
// type for arbitrary number of indices:
template<std::size_t...>
struct Indices {
};
```

This can be used to define a function that calls `print()` for the elements of a `std::array` or `std::tuple` using the compile-time access with `get<>()` for the given indices:

> 这可用于定义一个函数，该函数对给定索引使用带有“get＜＞()”的编译时访问为“std:：array”或“std：：tuple”的元素调用“print()”：

```cpp
template<typename T, std::size_t... Idx>
void printByIdx(T t, Indices<Idx...>)
{
  print(std::get<Idx>(t)...);
}
```

This template can be used as follows:

```cpp
std::array<std::string, 5> arr = [, "my", "new", "!", "World"}; printByIdx(arr, Indices<0, 4, 3>());
```

or as follows:

```cpp
    auto t = std::make_tuple(12, "monkeys", 2.0);
printByIdx(t, Indices<0, 1, 2>());
```

This is a first step towards meta-programming, which will be discussed in Section [[8.1]] on page [[123]] and [Chapter [23]].

> 这是迈向元编程的第一步，将在第[[123]]页的第[[8.1]]节和第[23]]章中进行讨论。

#### 4.4.4 Variadic Deduction Guides

Even deduction guides (see Section [[2.9]] on page [[42]]) can be variadic. For example, the C++ standard library defines the following deduction guide for `std::array` s:

> 即使是推导指南(见第[[42]]页第[[2.9]]节)也可能是可变的。例如，C++ 标准库为“std:：array”定义了以下推导指南：

```cpp
namespace std {
  template<typename T, typename... U> array(T, U...)
    -> array<enable_if_t<(is_same_v<T, U> && ...), T>,\
             (1 + [sizeof]...(U))>;\
}
```

An initialization such as

```cpp
`std::array a;`
```

deduces `T` in the guide to the type of the element, and the various `U…` types to the types of the subsequent elements. The total number of elements is therefore `1 + sizeof…(U)`:

> 将指南中的“T”推导出元素的类型，并将各种“U…”类型推导出后续元素的类型。因此，元素的总数是“1+sizeof…(U)”：

```cpp
std::array<int, 3> a;
```

The `std::enable_if<>` expression for the first `array` parameter is a fold expression that (as introduced as `isHomogeneous()` in Section [[4.4.1]] on page [[62]]) expands to:

> 第一个“array”参数的“std:：enable_if＜＞”表达式是一个折叠表达式，(如第[[62]]页第[[4.4.4]]节中的“ishomogenous()”所述)扩展为：

```cpp
is_same_v<T, U1> && is_same_v<T, U2> && is_same_v<T, U3> ...
```

If the result is not `true` (i.e., not all the element types are the same), the deduction guide is discarded and the overall deduction fails. This way, the standard library ensures that all elements must have the same type for the deduction guide to succeed.

> 如果结果不是“真的”(即，并非所有元素类型都相同)，则放弃推导指南，并且整体推导失败。通过这种方式，标准库确保所有元素必须具有相同的类型，才能使推导指南成功。

#### 4.4.5 Variadic Base Classes and **using**

Finally, consider the following example:

```cpp
`basics/varusing.cpp`

#include <string>
#include <unordered_set>

class Customer\
{
  private:\
    std::string name;\
  public:
    Customer(std::string const& n) : name(n) \
    std::string getName() const  name; }
};

struct CustomerEq {
    [bool operator]() (Customer const& c1, Customer const& c2) const {
      return c1.getName() == c2.getName();
    }
};

struct CustomerHash {
    std::size_t [operator]() (Customer const& c) const {
      return std::hash<std::string>()(c.getName());
    }
};

*[// define class that combines]* [operator() *for variadic base classes:
template<typename... Bases>
struct Overloader : Bases...
{
      using Bases:[:operator]()...;  *[// OK since C++17]*\
};

int main()
{
  *[// combine hasher and equality for customers in one type:]*\
  using CustomerOP = Overloader<CustomerHash,CustomerEq>;\

  std::unordered_set<Customer,CustomerHash,CustomerEq> coll1;\
  std::unordered_set<Customer,CustomerOP,CustomerOP> coll2;\
  ...
}
```

Here, we first define a class `Customer` and independent function objects to hash and compare `Customer` objects. With

> 在这里，我们首先定义一个类“Customer”和独立的函数对象来散列和比较“Customer”对象。具有

```cpp
template<typename... Bases>
struct Overloader : Bases...
{
    using Bases:[:operator]()...;  // OK since C++17
};
```

we can define a class derived from a variadic number of base classes that brings in the `operator()` declarations from each of those base classes. With

> 我们可以定义一个从各种基类派生的类，这些基类会从每个基类中引入“operator()”声明。具有

```cpp
using CustomerOP = Overloader<CustomerHash,CustomerEq>;
```

we use this feature to derive `CustomerOP` from `CustomerHash` and `CustomerEq` and enable both implementations of `operator()` in the derived class.

> 我们使用此功能从“CustomerHash”和“CustomerEq”派生“CustomerOP”，并在派生类中启用“operator()”的两个实现。

See Section [[26.4]] on page [[611]] for another application of this technique.

> 有关该技术的另一应用，请参见第[[611]]页的第[[26.4]]节。

### 4.5 Summary

```cpp
- By using parameter packs, templates can be defined for an arbitrary number of template parameters of arbitrary type.
- To process the parameters, you need recursion and/or a matching nonvariadic function.
- Operator `sizeof…` yields the number of arguments provided for a parameter pack.
- A typical application of variadic templates is forwarding an arbitrary number of arguments of arbitrary type.
- By using fold expressions, you can apply operators to all arguments of a parameter pack.

^[1]^ Initially, in C++11 and C++14 this was an ambiguity, which was fixed later (see [CoreIssue1395]), but all compilers handle it this way in all versions.
```

## Chapter 5

## Tricky Basics

This chapter covers some further basic aspects of templates that are relevant to the practical use of templates: an additional use of the `typename` keyword, defining member functions and nested classes as templates, template template parameters, zero initialization, and some details about using string literals as arguments for function templates. These aspects can be tricky at times, but every day-to-day programmer should have heard of them.

> 本章涵盖了与模板实际使用相关的模板的一些进一步的基本方面：“typename”关键字的额外使用，将成员函数和嵌套类定义为模板，模板模板参数，零初始化，以及有关使用字符串文字作为函数模板参数的一些细节。这些方面有时可能很棘手，但每个日常程序员都应该听说过。

### 5.1 Keyword **typename**

The keyword `typename` was introduced during the standardization of C++ to clarify that an identifier inside a template is a type. Consider the following example:

> 关键字“typename”是在 C++ 标准化过程中引入的，目的是澄清模板中的标识符是类型。考虑以下示例：

```cpp
template<typename T>
class MyClass {
  public:
    *...*\
    void foo() {
      typename T::SubType\* ptr;\
    }
};
```

Here, the second `typename` is used to clarify that `SubType` is a type defined within class `T`. Thus, `ptr` is a pointer to the type `T::SubType`.

> 这里，第二个“typename”用于说明“SubType”是在类“T”中定义的类型。因此，“ptr”是指向类型“T:：SubType”的指针。

Without `typename`, `SubType` would be assumed to be a nontype member (e.g., a static data member or an enumerator constant). As a result, the expression

> 如果没有“typename”，“SubType”将被假定为非类型成员(例如，静态数据成员或枚举器常量)。因此，表达式

```cpp
`T::SubType* ptr`
```

would be a multiplication of the static `SubType` member of class `T` with `ptr`, which is not an error, because for some instantiations of `MyClass<>` this could be valid code.

> 将是类“T”的静态“SubType”成员与“ptr”的乘积，这不是错误，因为对于“MyClass＜＞”的某些实例化来说，这可能是有效的代码。

In general, `typename` has to be used whenever a name that depends on a template parameter is a type. This is discussed in detail in Section [[13.3.2]] on page [[228]].

> 通常，只要依赖于模板参数的名称是类型，就必须使用“typename”。第[[228]]页第[[13.3.2]]节对此进行了详细讨论。

One application of `typename` is the declaration to iterators of standard containers in generic code:

> “typename”的一个应用程序是对泛型代码中标准容器的迭代器的声明：

```cpp
`basics/printcoll.hpp`

#include <iostream>
\
*[// print elements of an STL container]*\
template<typename T>
void printcoll (T const& coll)
{
    typename T::const_iterator pos;  *[// iterator to iterate over]* [coll]\
    typename T::const_iterator end(coll.end());*  [// end position]*\
    [for] (pos=coll.begin(); pos!=end; ++pos) {
        std::cout << \*pos << [' '];\
    }
    std::cout << '\n';\
}
```

In this function template, the call parameter is an standard container of type `T`. To iterate over all elements of the container, the iterator type of the container is used, which is declared as type `const_iterator` inside each standard container class:

> 在这个函数模板中，调用参数是“T”类型的标准容器。为了迭代容器的所有元素，使用容器的迭代器类型，在每个标准容器类中声明为类型“const_iterator”：

```cpp
class *stlcontainer* {
 public:
  using iterator = ...;        // iterator for read/write access
  using const_iterator = ...;  // iterator for read access
 ...
};
```

Thus, to access type `const_iterator` of template type `T`, you have to qualify it with a leading `typename`:

> 因此，要访问模板类型“T”的类型“const_iterator”，必须使用前导的“typename”对其进行限定：

```cpp
typename T::const_iterator pos;
```

See Section [[13.3.2]] on page [[228]] for more details about the need for `typename` until C++17. Note that C++20 will probably remove the need for `typename` in many common cases (see Section [[17.1]] on page [[354]] for details).

> 有关在 C++17 之前需要“typename”的更多详细信息，请参见第[[228]]页上的第[[13.3.2]]节。请注意，在许多常见情况下，C++20 可能会取消对“typename”的需要(有关详细信息，请参见第[[354]]页的第[[17.1]]节)。

### 5.2 Zero Initialization

For fundamental types such as `int`, `double`, or pointer types, there is no default constructor that initializes them with a useful default value. Instead, any noninitialized local variable has an undefined value:

> 对于基本类型，如“int”、“double”或指针类型，没有默认构造函数可以使用有用的默认值初始化它们。相反，任何未初始化的局部变量都有一个未定义的值：

```cpp
void foo()
{
  int x;       // [x] has undefined value
  int\* ptr;    // [ptr] points to anywhere (instead of nowhere)
}
```

Now if you write templates and want to have variables of a template type initialized by a default value, you have the problem that a simple definition doesn't do this for built-in types:

> 现在，如果您编写模板并希望使用默认值初始化模板类型的变量，则会遇到一个问题，即对于内置类型，简单的定义无法做到这一点：

```cpp
template<typename T>
void foo()
{
  T x;*        [//]* [x *has undefined value if [T *is built-in type
}
```

For this reason, it is possible to call explicitly a default constructor for built-in types that initializes them with zero (or `false` for `bool` or `nullptr` for pointers). As a consequence, you can ensure proper initialization even for built-in types by writing the following:

> 出于这个原因，可以显式调用内置类型的默认构造函数，该构造函数用零初始化它们(或“false”表示“bool”或“nullptr”表示指针)。因此，即使对于内置类型，也可以通过编写以下内容来确保正确的初始化：

```cpp
template<typename T>
void foo()
{
  T x;      *[//]* [x *is zero (or [false*) if* T *is a built-in type
}
```

This way of initialization is called _value initialization_, which means to either call a provided constructor or _zero initialize_ an object. This even works if the constructor is `explicit`.

> 这种初始化方式称为_value initialization_，意思是调用提供的构造函数或_zero initialize_对象。即使构造函数是“显式”的，这也能起作用。

Before C++11, the syntax to ensure proper initialization was

```cpp
`T x = T();`      // `x` is zero (or `false`) if `T` is a built-in type
```

Prior to C++17, this mechanism (which is still supported) only worked if the constructor selected for the copy-initialization is not `explicit`. In C++17, mandatory copy elision avoids that limitation and either syntax can work, but the braced initialized notation can use an initializer-list constructor[1] if no default constructor is available.

> 在 C++17 之前，只有当为副本初始化选择的构造函数不是“显式”时，这种机制(仍然受支持)才有效。在 C++17 中，强制的副本省略避免了这一限制，并且任何一种语法都可以工作，但如果没有默认构造函数可用，则支持的初始化表示法可以使用初始化器列表构造函数[1]。

To ensure that a member of a class template, for which the type is parameterized, gets initialized, you can define a default constructor that uses a braced initializer to initialize the member:

> 要确保初始化类型为其参数化的类模板的成员，可以定义一个默认构造函数，该构造函数使用支持的初始值设定项来初始化该成员：

```cpp
template<typename T>
class MyClass {
  private:\
    T x;\
  public:
    MyClass() : x * [x *is initialized even for built-in types
    }
    *...*\
};
```

The pre-C++11 syntax

```cpp
MyClass() : x()  [x] is initialized even for built-in types
}
```

also still works.

Since C++11, you can also provide a default initialization for a nonstatic member, so that the following is also possible:

> 由于 C++11，您还可以为非静态成员提供默认初始化，因此也可以执行以下操作：

```cpp
template<typename T>
class MyClass {
  private:\
    T x;            *[// zero-initialize]* [x *unless otherwise specified
    *...*\
};
```

However, note that default arguments cannot use that syntax. For example,

```cpp
template<typename T>
void foo(T p) \
    ...
}
```

Instead, we have to write:

```cpp
template<typename T>
void foo(T p = T)  [T()] before C++11)
    ...
}
```

### 5.3 Using **this->**

For class templates with base classes that depend on template parameters, using a name `x` by itself is not always equivalent to `this->x`, even though a member `x` is inherited. For example:

> 对于具有依赖于模板参数的基类的类模板，单独使用名称“x”并不总是等同于“this->x”，即使成员“x”是继承的。例如

```cpp
template<typename T>
class Base {
  public:
    void bar();
};
\
template<typename T>
class Derived : Base<T> {
  public:
    void foo() {
        bar(); *[// calls external]* [bar() *or error
    }
};
```

In this example, for resolving the symbol `bar` inside `foo()`, `bar()` defined in `Base` is _never_ considered. Therefore, either you have an error, or another `bar()` (such as a global `bar()`) is called.

> 在本例中，为了解析“foo()”中的符号“bar”，在“Base”中定义的“bar()”是_never_考虑的。因此，要么出现错误，要么调用另一个“bar()”(如全局“bar(()”)。

We discuss this issue in Section [[13.4.2]] on page [[237]] in detail. For the moment, as a rule of thumb, we recommend that you always qualify any symbol that is declared in a base that is somehow dependent on a template parameter with `this->` or `Base<T>::`.

> 我们在第[[237]]页的第[[13.4.2]]节中详细讨论了这个问题。目前，根据经验，我们建议您始终使用 `this->` 或 `base<T>：：` 限定在以某种方式依赖于模板参数的基中声明的任何符号。

### 5.4 Templates for Raw Arrays and String Literals

When passing raw arrays or string literals to templates, some care has to be taken. First, if the template parameters are declared as references, the arguments don't decay. That is, a passed argument of `"hello"` has type `char const[6]`. This can become a problem if raw arrays or string arguments of different length are passed because the types differ. Only when passing the argument by value, the types decay, so that string literals are converted to type `char const*`. This is discussed in detail in [Chapter [7]].

> 将原始数组或字符串文字传递给模板时，必须格外小心。首先，如果模板参数被声明为引用，则参数不会衰减。也就是说，“hello”的传递参数的类型为“char const[6]”。如果由于类型不同而传递不同长度的原始数组或字符串参数，这可能会成为一个问题。只有在按值传递参数时，类型才会衰减，因此字符串文字会转换为类型“char const*”。这将在[第[7]章]中进行详细讨论。

Note that you can also provide templates that specifically deal with raw arrays or string literals. For example:

> 请注意，您还可以提供专门处理原始数组或字符串文字的模板。例如

```cpp
`basics/lessarray.hpp`

    template<typename T,\
    int N,\
    int M> [bool] less (T(&a)[N], T(&b)[M])
    {
        [for] [(int] i = 0; i<N && i<M; ++i)
    {
        if (a[i]<b[i]) [return true]; if (b[i]<a[i]) [return false]; } return N < M;\
    }
```

Here, when calling

```cpp
int x[] = ;\
int y[] = ;\
std::cout << less(x,y) << '\n';
```

`less<>()` is instantiated with `T` being `int`, `N` being `3`, and `M` being `5`.

You can also use this template for string literals:

```cpp
std::cout << less[(\"ab"[,\"abc") << '\n';
```

In this case, `less<>()` is instantiated with `T` being `char const`, `N` being `3` and `M` being `4`.

> 在这种情况下，“less＜＞()”被实例化，其中“T”是“char const”，“N”是“3”，“M”是“4”。

If you only want to provide a function template for string literals (and other `char` arrays), you can do this as follows:

> 如果您只想为字符串文字(和其他“char”数组)提供一个函数模板，可以按如下方式执行：

```cpp
`basics/lessstring.hpp`

template<int N, int M>
[bool] less [(char const](&a)[N], [char const](&b)[M])
{
    [for] [(int] i = 0; i<N && i<M; ++i) {
        if (a[i]<b[i]) [return true];\
        if (b[i]<a[i]) [return false];\
    }
    return N < M;\
}
```

Note that you can and sometimes have to overload or partially specialize for arrays of unknown bounds. The following program illustrates all possible overloads for arrays:

> 请注意，您可以而且有时必须重载或部分专用于未知边界的数组。以下程序说明了阵列的所有可能过载：

```cpp
`basics/arrays.hpp`

#include <iostream>
\
template<typename T>
struct MyClass;             // primary template
\
template<typename T, std::size_t SZ>
struct MyClass<T[SZ]>       *[// partial specialization for arrays of known bounds]*\
{
  [static void] print()  << SZ << "]\\n"; }
};
\
template<typename T, std::size_t SZ>
struct MyClass<T(&)[SZ]>    *[// partial spec. for references to arrays of known bounds]*\
{
  [static void] print()  << SZ << "]\\n"; }
};
\
template<typename T>
struct MyClass<T[]>         *[// partial specialization for arrays of unknown bounds]*\
{
  [static void] print() ; }
};
\
template<typename T>
struct MyClass<T(&)[]>      *[// partial spec. for references to arrays of unknown bounds]*\
{
  [static void] print() ; }
};
\
template<typename T>
struct MyClass<T*>         *[// partial specialization for pointers]*\
{
  [static void] print() ; }
};
```

Here, the class template `MyClass<>` is specialized for various types: arrays of known and unknown bound, references to arrays of known and unknown bounds, and pointers. Each case is different and can occur when using arrays:

> 这里，类模板“MyClass＜＞”专门用于各种类型：已知和未知边界的数组、对已知和未知界限的数组的引用以及指针。每种情况都不同，在使用阵列时都可能发生：

```cpp
`basics/arrays.cpp`

#include "arrays.hpp"\
\
template<typename T1, typename T2, typename T3>
void foo[(int] a1[7], int a2[],    *[// pointers by language rules]*\
         int (&a3)[42],          *[// reference to array of known bound]*\
         int (&x0)[],            *[// reference to array of unknown bound]*\
         T1 x1,                  *[// passing by value decays]*\
         T2& x2, T3&& x3)        *[// passing by reference]*\
{
  MyClass<decltype(a1)>::print();      *[// uses]* [MyClass<T*>]\
  MyClass<decltype(a2)>::print();      *[// uses]* [MyClass<T*>]\
  MyClass<decltype(a3)>::print();      *[// uses]* [MyClass<T(&)[SZ]>]\
  MyClass<decltype(x0)>::print();      *[// uses]* [MyClass<T(&)[]>]\
  MyClass<decltype(x1)>::print();      *[// uses]* [MyClass<T*>]\
  MyClass<decltype(x2)>::print();      *[// uses]* [MyClass<T(&)[]>]\
  MyClass<decltype(x3)>::print();      *[// uses]* [MyClass<T(&)[]>]\
}
\
int main()
{
  int a[42];\
  MyClass<decltype(a)>::print();       *[// uses]* [MyClass<T[SZ]>]\
\
  [extern int] x[];                      *[// forward declare array]*\
  MyClass<decltype(x)>::print();       *[// uses]* [MyClass<T[]>]\
\
  foo(a, a, a, x, x, x, x);
}
\
int x[] = ;                *[// define forward-declared array]*
```

Note that a _call parameter_ declared as an array (with or without length) by language rules really has a pointer type. Note also that templates for arrays of unknown bounds can be used for an incomplete type such as

> 请注意，由语言规则声明为数组(有或没有长度)的_call 参数_实际上具有指针类型。还要注意，未知边界数组的模板可以用于不完整的类型，例如

```cpp
[extern int] i[];
```

And when this is passed by reference, it becomes a `int(&)[]`, which can also be used as a template parameter.[2]

> 当它通过引用传递时，它将变为“int(&)[]”，也可以用作模板参数。2.

See Section [[19.3.1]] on page [[401]] for another example using the different array types in generic code.

> 有关在泛型代码中使用不同数组类型的另一个示例，请参见第[[401]]页的第[[19.3.1]]节。

### 5.5 Member Templates

Class members can also be templates. This is possible for both nested classes and member functions. The application and advantage of this ability can again be demonstrated with the `Stack<>` class template. Normally you can assign stacks to each other only when they have the same type, which implies that the elements have the same type. However, you can't assign a stack with elements of any other type, even if there is an implicit type conversion for the element types defined:

> 类成员也可以是模板。这对于嵌套类和成员函数都是可能的。这种能力的应用和优势可以用“Stack＜＞”类模板再次展示。通常情况下，只有当堆栈具有相同的类型时，才可以将它们相互分配，这意味着元素具有相同类型。但是，即使对定义的元素类型进行了隐式类型转换，也不能为堆栈分配任何其他类型的元素：

```cpp
Stack<int> intStack1, intStack2;  // stacks for ints
Stack<[float]> floatStack;          // stack for [float]s
...
intStack1 = intStack2;            // OK: stacks have same type
floatStack = intStack1;           // ERROR: stacks have different types
```

The default assignment operator requires that both sides of the assignment operator have the same type, which is not the case if stacks have different element types.

> 默认赋值运算符要求赋值运算符的两侧都具有相同的类型，但如果堆栈具有不同的元素类型，则情况并非如此。

By defining an assignment operator as a template, however, you can enable the assignment of stacks with elements for which an appropriate type conversion is defined. To do this you have to declare `Stack<>` as follows:

> 但是，通过将赋值运算符定义为模板，可以启用具有定义了适当类型转换的元素的堆栈的赋值。要执行此操作，您必须声明“Stack＜＞”，如下所示：

```cpp
`basics/stack5decl.hpp`

template<typename T>
class Stack {
  private:\
    std::deque<T> elems;        *[// elements]*\
\
  public:
    void push(T const&);        *[// push element]*\
    void pop();                 *[// pop element]*\
    T const& top() const;       *[// return top element]*\
    [bool] empty() const *\
        return elems.empty();
    }
\
    *[// assign stack of elements of type]* [T2]\
    template<typename T2>
    Stack& [operator]= (Stack<T2> const&);
};
```

The following two changes have been made:

1. We added a declaration of an assignment operator for stacks of elements of another type `T2`.

> 1.我们为另一种类型“T2”的元素堆栈添加了赋值运算符的声明。

2. The stack now uses a `std::deque<>` as an internal container for the elements. Again, this is a consequence of the implementation of the new assignment operator.

> 2.堆栈现在使用“std:：deque＜＞”作为元素的内部容器。同样，这是实现新赋值运算符的结果。

The implementation of the new assignment operator looks like this:[3]

```cpp
`basics/stack5assign.hpp`

template<typename T>
template<typename T2>
Stack<T>& Stack<T>:[:operator]= (Stack<T2> const& op2)
{
    Stack<T2> tmp(op2);              // create a copy of the assigned stack
\
    elems.clear();                   *[// remove existing elements]*\
    [while] (!tmp.empty()) *\
        elems.push_front(tmp.top());
        tmp.pop();
    }
    return [\*this];\
}
```

First let's look at the syntax to define a member template. Inside the template with template parameter `T`, an inner template with template parameter `T2` is defined:

> 首先，我们来看一下定义成员模板的语法。在具有模板参数“T”的模板内部，定义了具有模板参数‘T2’的内部模板：

```cpp
template<typename T>
 template<typename T2>
...
```

Inside the member function, you may expect simply to access all necessary data for the assigned stack `op2`. However, this stack has a different type (if you instantiate a class template for two different argument types, you get two different class types), so you are restricted to using the public interface. It follows that the only way to access the elements is by calling `top()`. However, each element has to become a top element, then. Thus, a copy of `op2` must first be made, so that the elements are taken from that copy by calling `pop()`. Because `top()` returns the last element pushed onto the stack, we might prefer to use a container that supports the insertion of elements at the other end of the collection. For this reason, we use a `std::deque<>`, which provides `push_front()` to put an element on the other side of the collection.

> 在成员函数中，您可能只需要访问指定堆栈“op2”的所有必要数据。但是，这个堆栈有一个不同的类型(如果您为两种不同的参数类型实例化一个类模板，则会得到两种不同类型的类)，因此您只能使用公共接口。因此，访问元素的唯一方法是调用“top()”。然而，每个元素都必须成为顶级元素。因此，必须首先制作“op2”的副本，以便通过调用“pop()”从该副本中获取元素。因为“top()”返回推送到堆栈上的最后一个元素，所以我们可能更喜欢使用支持在集合的另一端插入元素的容器。出于这个原因，我们使用了一个“std:：deque＜＞”，它提供了“push_front()”将元素放在集合的另一侧。

To get access to all the members of `op2` you can declare that all other stack instances are friends:

> 要访问“op2”的所有成员，您可以声明所有其他堆栈实例都是朋友：

```cpp
`basics/stack6decl.hpp`

template<typename T>
class Stack {
  private:\
    std::deque<T> elems;       // elements
   public:
    void push(T const&);       *[// push element]*\
    void pop();                *[// pop element]*\
    T const& top() const;      *[// return top element]*\
    [bool] empty() const *\
        return elems.empty();
    }

\
    *[// assign stack of elements of type]* [T2]\
    template<typename T2>
    Stack& [operator]= (Stack<T2> const&);
    *[// to get access to private members of]* [Stack<T2> for any type T2*:
    template<typename> [friend class] Stack;\
};
```

As you can see, because the name of the template parameter is not used, you can omit it:

> 正如您所看到的，由于没有使用模板参数的名称，您可以省略它：

```cpp
template<typename> [friend class] Stack;
```

Now, the following implementation of the template assignment operator is possible:

> 现在，可以实现以下模板分配运算符：

```cpp
`basics/stack6assign.hpp`

template<typename T>
 template<typename T2>
Stack<T>& Stack<T>:[:operator]= (Stack<T2> const& op2)
{
    elems.clear();                        *[// remove existing elements]*\
    elems.insert(elems.begin(),           *[// insert at the beginning]*\
                 op2.elems.begin(),       *[// all elements from]* [op2]\
                 op2.elems.end());
    return \*[this];\
}
```

Whatever your implementation is, having this member template, you can now assign a stack of `int` s to a stack of `float` s:

> 无论您的实现是什么，有了这个成员模板，现在都可以将“int”的堆栈分配给“float”的堆栈：

```cpp
Stack<int> intStack;      // stack for ints
Stack<[float]> floatStack;  // stack for [float]s
...
floatStack = intStack;    // OK: stacks have different types,
                          //     but int converts to [float]
```

Of course, this assignment does not change the type of the stack and its elements. After the assignment, the elements of the `floatStack` are still `floats` and therefore `top()` still returns a `float`.

> 当然，此赋值不会更改堆栈及其元素的类型。赋值之后，“floatStack”的元素仍然是“float”，因此“top()”仍然返回“float(浮点)”。

It may appear that this function would disable type checking such that you could assign a stack with elements of any type, but this is not the case. The necessary type checking occurs when the element of the (copy of the) source stack is moved to the destination stack:

> 这个函数可能会禁用类型检查，这样您就可以为堆栈分配任何类型的元素，但事实并非如此。将源堆栈(的副本)的元素移动到目标堆栈时，将进行必要的类型检查：

```cpp
elems.push_front(tmp.top());
```

If, for example, a stack of strings gets assigned to a stack of `float` s, the compilation of this line results in an error message stating that the string returned by `tmp.top()` cannot be passed as an argument to `elems.push_front()` (the message varies depending on the compiler, but this is the gist of what is meant):

> 例如，如果一个字符串堆栈被分配给一个“float”堆栈，则这一行的编译会导致一条错误消息，说明“tmp.top()”返回的字符串不能作为参数传递给“elems.push_front()”(该消息因编译器而异，但这是含义的要点)：

```cpp
Stack<std::string> stringStack;  // stack of [string]s
Stack<[float]> floatStack;         // stack of [float]s
...
floatStack = stringStack;        // ERROR: [std::string] doesn't convert to [float]
```

Again, you could change the implementation to parameterize the internal container type:

> 同样，您可以更改实现以参数化内部容器类型：

```cpp
`basics/stack7decl.hpp`

template<typename T, typename Cont = std::deque<T>>
class Stack {
  private:\
    Cont elems;                // elements
\
  public:
    void push(T const&);       *[// push element]*\
    void pop();                *[// pop element]*\
    T const& top() const;      *[// return top element]*\
    [bool] empty() const *\
        return elems.empty();
    }
\
    *[// assign stack of elements of type]* [T2]\
    template<typename T2, typename Cont2>
    Stack& [operator]= (Stack<T2,Cont2> const&);
    *[// to get access to private members of]* [Stack<T2> *for any type* T2*:
    template<typename, typename> [friend class] Stack;\
};

\
```

Then the template assignment operator is implemented like this:

```cpp
`basics/stack7assign.hpp`

template<typename T, typename Cont>
 template<typename T2, typename Cont2>
Stack<T,Cont>&\
Stack<T,Cont>::[operator]= (Stack<T2,Cont2> const& op2)
 {
    elems.clear();                        *[// remove existing elements]*\
    elems.insert(elems.begin(),           *[// insert at the beginning]*\
                 op2.elems.begin(),       *[// all elements from]* [op2]\
                 op2.elems.end());
    return [\*this];\
}
```

Remember, for class templates, only those member functions that are called are instantiated. Thus, if you avoid assigning a stack with elements of a different type, you could even use a vector as an internal container:

> 请记住，对于类模板，只有那些被调用的成员函数才会被实例化。因此，如果避免为堆栈分配不同类型的元素，甚至可以使用向量作为内部容器：

```cpp
// stack for ints using a vector as an internal container
Stack<int,std::vector<int>> vStack;\
...
vStack.push(42); vStack.push(7);
std::cout << vStack.top() << '\n';
```

Because the assignment operator template isn't necessary, no error message of a missing member function `push_front()` occurs and the program is fine.

> 由于不需要赋值运算符模板，因此不会出现缺少成员函数“push_front()”的错误消息，并且程序正常。

For the complete implementation of the last example, see all the files with a name that starts with _stack7_ in the subdirectory _basics_.

> 有关最后一个示例的完整实现，请参阅子目录_basics_中名称以_stack7_开头的所有文件。

##### Specialization of Member Function Templates

Member function templates can also be partially or fully specialized. For example, for the following class:

> 成员函数模板也可以部分或完全专门化。例如，对于以下类：

```cpp
`basics/boolstring.hpp`

class BoolString {
  private:\
    std::string value;\
  public:
    BoolString (std::string const& s)
     : value(s) {
    }
\
    template<typename T = std::string>
    T get() const \
      return value;\
    }
};
```

you can provide a full specialization for the member function template as follows:

> 您可以为成员函数模板提供完整的专业化，如下所示：

```cpp
`basics/boolstringgetbool.hpp`

// full specialization for [BoolString::getValue<>()] for [bool]\
template<>
[inline bool] BoolString::get[<bool]>() const {
  return value == "true" \|\| value == "1" \|\| value == "on";\
}
```

Note that you don't need and also can't declare the specializations; you only define them. Because it is a full specialization and it is in a header file you have to declare it with `inline` to avoid errors if the definition is included by different translation units.

> 请注意，您不需要也不能声明专业化；你只能定义它们。因为它是完全专业化的，并且在头文件中，所以如果定义由不同的翻译单元包含，则必须用“inline”声明它，以避免出现错误。

You can use class and the full specialization as follows:

```cpp
std::cout << std::boolalpha;\
BoolString s1[(\"hello");
std::cout << s1.get() << '\n';        //prints [hello]\
std::cout << s1.get[<bool]>() << '\n';  //prints [false]\
BoolString s2[(\"on");
std::cout << s2.get[<bool]>() << '\n';  //prints [true]
```

##### Special Member Function Templates

Template member functions can be used wherever special member functions allow copying or moving objects. Similar to assignment operators as defined above, they can also be constructors. However, note that template constructors or template assignment operators don't replace predefined constructors or assignment operators. Member templates don't count as _the_ special member functions that copy or move objects. In this example, for assignments of stacks of the same type, the default assignment operator is still called.

> 在特殊成员函数允许复制或移动对象的情况下，可以使用模板成员函数。与上面定义的赋值运算符类似，它们也可以是构造函数。但是，请注意，模板构造函数或模板赋值运算符不会替换预定义的构造函数或赋值运算符。成员模板不算作复制或移动对象的特殊成员函数。在本例中，对于相同类型堆栈的赋值，仍调用默认赋值运算符。

This effect can be good and bad:

• It can happen that a template constructor or assignment operator is a better match than the predefined copy/move constructor or assignment operator, although a template version is provided for initialization of other types only. See Section [[6.2]] on page [[95]] for details.

> •模板构造函数或赋值运算符可能比预定义的复制/移动构造函数或赋值操作符更匹配，尽管模板版本仅用于初始化其他类型。详见第[[95]]页第[[6.2]]节。

• It is not easy to "templify" a copy/move constructor, for example, to be able to constrain its existence. See Section [[6.4]] on page [[102]] for details.

> •“临时”复制/移动构造函数并不容易，例如，要约束其存在。详见第[[102]]页第[[6.4]]节。

#### 5.5.1 The **.template** Construct

Sometimes, it is necessary to explicitly qualify template arguments when calling a member template. In that case, you have to use the `template` keyword to ensure that a `<` is the beginning of the template argument list. Consider the following example using the standard `bitset` type:

> 有时，在调用成员模板时需要显式限定模板参数。在这种情况下，您必须使用“template”关键字来确保“<”是模板参数列表的开头。考虑以下使用标准“位集”类型的示例：

```cpp
template<[unsigned long] N>
void printBitset (std::bitset<N> const& bs) {
  std::cout << bs[.template] to_string[<char], std::char_traits[<char]>,\
                                     std::allocator<[char]>>();
}
```

For the bitset `bs` we call the member function template `to_string()`, while explicitly specifying the string type details. Without that extra use of `.template`, the compiler does not know that the less-than token (`<`) that follows is not really less-than but the beginning of a template argument list. Note that this is a problem only if the construct before the period depends on a template parameter. In our example, the parameter `bs` depends on the template parameter `N`.

> 对于位集“bs”，我们调用成员函数模板“to_string()”，同时显式指定字符串类型的详细信息。如果没有“.template”的额外使用，编译器就不知道后面的小于标记(“<”)实际上并不小于模板参数列表的开头。请注意，只有当句点之前的构造依赖于模板参数时，这才是一个问题。在我们的示例中，参数“bs”取决于模板参数“N”。

The `.template` notation (and similar notations such as `->template` and `::template`) should be used only inside templates and only if they follow something that depends on a template parameter. See Section [[13.3.3]] on page [[230]] for details.

> “.template”表示法(以及类似的表示法，如“->template”和“：：template”)应仅在模板内部使用，并且仅当它们遵循依赖于模板参数的内容时使用。详见第[[230]]页第[[13.3.3]]节。

#### 5.5.2 Generic Lambdas and Member Templates

Note that generic lambdas, introduced with C++14, are shortcuts for member templates. A simple lambda computing the "sum" of two arguments of arbitrary types:

> 请注意，C++14 中引入的通用 lambda 是成员模板的快捷方式。一个简单的 lambda 计算任意类型的两个参数的“和”：

```cpp
[] [(auto] x, auto y) {
  return x + y;\
}
```

is a shortcut for a default-constructed object of the following class:

```cpp
class *SomeCompilerSpecificName* {
  public:
    *SomeCompilerSpecificName*`();`  // constructor only callable by compiler
    template<typename T1, typename T2>
    [auto operator]() (T1 x, T2 y) const {
      return x + y;\
    }
};
```

See Section [[15.10.6]] on page [[309]] for details.

### 5.6 Variable Templates

Since C++14, variables also can be parameterized by a specific type. Such a thing is called a _variable template_.[4]

> 由于 C++14，变量也可以通过特定类型进行参数化。这样的东西被称为可变模板。4.

For example, you can use the following code to define the value of _ˇ_ while still not defining the type of the value:

> 例如，您可以使用以下代码定义_的值，但仍然不定义值的类型：

```cpp
template<typename T>
[constexpr] T pi;
```

Note that, as for all templates, this declaration may not occur inside functions or block scope.

> 请注意，对于所有模板，此声明可能不会出现在函数或块范围内。

To use a variable template, you have to specify its type. For example, the following code uses two different variables of the scope where `pi<>` is declared:

> 若要使用变量模板，必须指定其类型。例如，以下代码使用声明“pi＜＞”的作用域的两个不同变量：

```cpp
std::cout << pi[<double]> << '\n';\
std::cout << pi[<float]> << '\n';
```

You can also declare variable templates that are used in different translation units:

> 您还可以声明在不同翻译单位中使用的变量模板：

```cpp
// == ***header.hpp:***\
template<typename T> T val;     // zero initialized value
\
// == ***translation unit 1:***\
#include "header.hpp"\
\
int main()
{
  val<[long]> = 42;\
  print();
}
\
// == ***translation unit 2:***\
#include "header.hpp"\
\
void print()
{
  std::cout << val[<long]> << '\n'; *[// OK: prints]* [42]\
}
```

Variable templates can also have default template arguments:

```cpp
template<typename T = [long double]>
[constexpr] T pi = T;
```

You can use the default or any other type:

```cpp
std::cout << pi<> << '\n';       //outputs a long double
std::cout << pi[<float]> << '\n';  //outputs a float
```

However, note that you always have to specify the angle brackets. Just using `pi` is an error:

> 但是，请注意，必须始终指定尖括号。仅使用“pi”是一个错误：

```cpp
std::cout << pi << '\n';        //ERROR
```

Variable templates can also be parameterized by nontype parameters, which also may be used to parameterize the initializer. For example:

> 变量模板也可以通过非类型参数进行参数化，这些参数也可以用于参数化初始值设定项。例如

```cpp
#include <iostream>
#include <array>
\
template<int N>
  std::array<int,N> arr;         *[// array with]* [N] *[elements, zero-initialized]*\
 template<auto N>
  [constexpr decltype](N) dval = N;  *[// type of]* [dval] depends on passed value
\
int main()
{
  std::cout << dval[<'c]'> << '\n';             *[//]* [N] *[has value]* ['c'] *[of type]* [char]\
  arr<10>[0] = 42;                            *[// sets first element of global]* [arr]\
  [for] (std::size_t i=0; i<arr<10>.size(); ++i) * [arr]\
   std::cout << arr<10>[i] << '\n';\
  }
}
```

Again, note that even when the initialization of and iteration over `arr` happens in different translation units the same variable `std::array<int,10> arr` of global scope is still used.

> 再次注意，即使“arr”的初始化和迭代发生在不同的转换单元中，仍然使用全局范围的相同变量“std:：array＜int，10＞arr”。

##### Variable Templates for Data Members

A useful application of variable templates is to define variables that represent members of class templates. For example, if a class template is defined as follows:

> 变量模板的一个有用应用是定义表示类模板成员的变量。例如，如果类模板定义如下：

```cpp
template<typename T>
class MyClass {
  public:
    [static constexpr int] max = 1000;\
};
```

which allows you to define different values for different specializations of `MyClass<>`, then you can define

> 它允许您为“MyClass＜＞”的不同专业化定义不同的值，然后您可以定义

```cpp
template<typename T>
int myMax = MyClass<T>::max;
```

so that application programmers can just write

```cpp
auto i = myMax<std::string>;
```

instead of

```cpp
auto i = MyClass<std::string>::max;
```

This means, for a standard class such as

```cpp
namespace std {
  template<typename T> class numeric_limits {
    public:
      ...
      [static constexpr bool] is_signed = [false];\
      ...
  };
}
```

you can define

```cpp
template<typename T>
[constexpr bool] isSigned = std::numeric_limits<T>::is_signed;
```

to be able to write

```cpp
isSigned<[char]>
```

instead of

```cpp
std::numeric_limits<[char]>::is_signed
```

##### Type Traits Suffix **\_v**

Since C++17, the standard library uses the technique of variable templates to define shortcuts for all type traits in the standard library that yield a (Boolean) value. For example, to be able to write

> 自 C++17 以来，标准库使用变量模板技术为标准库中产生(布尔)值的所有类型特征定义快捷方式。例如，为了能够写作

```cpp
std::is_const_v<T>        // since C++17
```

instead of

```cpp
std::is_const<T>::value        //since C++11
```

the standard library defines

```cpp
namespace std {
  template<typename T> [constexpr bool] is_const_v = is_const<T>::value;\
}
```

### 5.7 Template Template Parameters

It can be useful to allow a template parameter itself to be a class template. Again, our stack class template can be used as an example.

> 允许模板参数本身作为类模板是非常有用的。同样，我们的堆栈类模板可以作为一个例子。

To use a different internal container for stacks, the application programmer has to specify the element type twice. Thus, to specify the type of the internal container, you have to pass the type of the container _and_ the type of its elements again:

> 要对堆栈使用不同的内部容器，应用程序程序员必须指定两次元素类型。因此，要指定内部容器的类型，必须再次传递容器的类型_and_其元素的类型：

```cpp
`Stack<int, std::vector<int>> vStack;`  // integer stack that uses a vector
```

Using template template parameters allows you to declare the `Stack` class template by specifying the type of the container without respecifying the type of its elements:

> 使用模板模板参数可以通过指定容器的类型来声明“堆栈”类模板，而无需重新指定其元素的类型：

```cpp
`Stack<int, std::vector> vStack;`        // integer stack that uses a vector
```

To do this, you must specify the second template parameter as a template template parameter. In principle, this looks as follows:[5]

> 要执行此操作，必须将第二个模板参数指定为模板模板参数。原则上，这看起来如下：[5]

```cpp
`basics/stack8decl.hpp`

template<typename T,\
         template<typename Elem> class Cont = std::deque>
class Stack {
  private:\
    Cont<T> elems;             // elements
\
  public:
    void push(T const&);       *[// push element]*\
    void pop();                *[// pop element]*\
    T const& top() const;      *[// return top element]*\
    [bool] empty() const *\
        return elems.empty();
    }
    *...*\
};
```

The difference is that the second template parameter is declared as being a class template:

> 不同之处在于，第二个模板参数被声明为类模板：

```cpp
template<typename Elem> class Cont
```

The default value has changed from `std::deque<T>` to `std::deque`. This parameter has to be a class template, which is instantiated for the type that is passed as the first template parameter:

> 默认值已从“std:：deque＜T＞”更改为“std::deque”。此参数必须是类模板，它是为作为第一个模板参数传递的类型实例化的：

```cpp
`Cont<T> elems;`
```

This use of the first template parameter for the instantiation of the second template parameter is particular to this example. In general, you can instantiate a template template parameter with any type inside a class template.

> 第一模板参数用于第二模板参数的实例化的这种使用对于该示例是特定的。通常，您可以实例化类模板中任何类型的模板模板参数。

As usual, instead of `typename` you could use the keyword `class` for template parameters. Before C++11, `Cont` could only be substituted by the name of a class template.

> 和往常一样，您可以使用关键字“class”代替“typename”作为模板参数。在 C++11 之前，“Cont”只能用类模板的名称代替。

```cpp
template<typename T,\
         template<class Elem> class Cont = std::deque>
class Stack \
  ...
};
```

Since C++11, we can also substitute `Cont` with the name of an alias template, but it wasn't until C++17 that a corresponding change was made to permit the use of the keyword `typename` instead of `class` to declare a template template parameter:

> 由于 C++11，我们也可以用别名模板的名称替换“Cont”，但直到 C++17 才进行了相应的更改，允许使用关键字“typename”而不是“class”来声明模板模板参数：

```cpp
template<typename T,\
         template<typename Elem> typename Cont = std::deque>
class Stack \
  ...
};
```

Those two variants mean exactly the same thing: Using `class` instead of `typename` does not prevent us from specifying an alias template as the argument corresponding to the `Cont` parameter.

> 这两种变体的意思完全相同：使用“class”而不是“typename”并不能阻止我们将别名模板指定为与“Cont”参数对应的参数。

Because the template parameter of the template template parameter is not used, it is customary to omit its name (unless it provides useful documentation):

> 由于没有使用模板模板参数的模板参数，因此通常会省略其名称(除非它提供有用的文档)：

```cpp
template<typename T,\
         template<typename> class Cont = std::deque>
class Stack {
  ...
};
```

Member functions must be modified accordingly. Thus, you have to specify the second template parameter as the template template parameter. The same applies to the implementation of the member function. The `push()` member function, for example, is implemented as follows:

> 成员职能必须相应修改。因此，您必须指定第二个模板参数作为模板模板参数。这同样适用于成员职能的实施。例如，“push()”成员函数的实现方式如下：

```cpp
template<typename T, template[<typename]> class Cont>
void Stack<T,Cont>::push (T const& elem)
{
    elems.push_back(elem);    // append copy of passed [elem]\
}
```

Note that while template template parameters are placeholders for class or alias templates, there is no corresponding placeholder for function or variable templates.

> 请注意，虽然模板模板参数是类或别名模板的占位符，但函数或变量模板没有相应的占位符。

##### Template Template Argument Matching

If you try to use the new version of `Stack`, you may get an error message saying that the default value `std::deque` is not compatible with the template template parameter `Cont`. The problem is that prior to C++17 a template template argument had to be a template with parameters that _exactly_ match the parameters of the template template parameter it substitutes, with some exceptions related to variadic template parameters (see Section [[12.3.4]] on page [[197]]). Default template arguments of template template arguments were not considered, so that a match couldn't be achieved by leaving out arguments that have default values (in C++17, default arguments _are_ considered).

> 如果尝试使用新版本的“Stack”，可能会收到一条错误消息，指出默认值“std:：deque”与模板模板参数“Cont”不兼容。问题是，在 C++17 之前，模板模板参数必须是一个模板，其参数_exactly_与它所替代的模板模板参数的参数匹配，但与可变模板参数有关的一些例外情况除外(见第[[197]]页第[[12.3.4]]节)。没有考虑模板模板参数的默认模板参数，因此无法通过省略具有默认值的参数(在 C++17 中，默认参数_are_ consided)来实现匹配。

The pre-C++17 problem in this example is that the `std::deque` template of the standard library has more than one parameter: The second parameter (which describes an _allocator_) has a default value, but prior to C++17 this was not considered when matching `std::deque` to the `Cont` parameter.

> 本例中 C++17 之前的问题是标准库的“std:：deque”模板有多个参数：第二个参数(描述_allocator_)有一个默认值，但在 C++17 之前，将“std:”deque“与“Cont”参数匹配时没有考虑这一点。

There is a workaround, however. We can rewrite the class declaration so that the `Cont` parameter expects containers with two template parameters:

> 然而，有一个变通办法。我们可以重写类声明，使“Cont”参数期望容器具有两个模板参数：

```cpp
template<typename T,\
         template<typename Elem,\
                  typename Alloc = std::allocator<Elem>>
          class Cont = std::deque>
class Stack {
  private:\
    Cont<T> elems;         // elements
    ...
};
```

Again, we could omit `Alloc` because it is not used.

The final version of our `Stack` template (including member templates for assignments of stacks of different element types) now looks as follows:

> “堆栈”模板的最终版本(包括用于分配不同元素类型堆栈的成员模板)现在如下所示：

```cpp
`basics/stack9.hpp`

#include <deque>
#include <cassert>
#include <memory>
\
template<typename T,\
         template<typename Elem,\
                  typename = std::allocator<Elem>>
         class Cont = std::deque>
class Stack {
  private:\
    Cont<T> elems;            // elements
\
  public:
    void push(T const&);      *[// push element]*\
    void pop();               *[// pop element]*\
    T const& top() const;     *[// return top element]*\
    [bool] empty() const *\
        return elems.empty();
    }
\
    *[// assign stack of elements of type]* [T2]\
    template<typename T2,\
             template<typename Elem2,\
                      typename = std::allocator<Elem2>
                     >class Cont2>
    Stack<T,Cont>& [operator]= (Stack<T2,Cont2> const&);
    *[// to get access to private members of any Stack with elements of type]* [T2]*[:]*\
    template<typename, template[<typename], typename[>class]>
    [friend class] Stack;\
};
\
template<typename T, template[<typename][,typename]> class Cont>
void Stack<T,Cont>::push (T const& elem)
{
    elems.push_back(elem);    *[// append copy of passed]* [elem]\
}
\
template<typename T, template[<typename][,typename]> class Cont>
 void Stack<T,Cont>::pop ()
{
    assert(!elems.empty());
    elems.pop_back();          *[// remove last element]*\
}
\
template<typename T, template[<typename][,typename]> class Cont>
T const& Stack<T,Cont>::top () const\
{
    assert(!elems.empty());
    return elems.back();       *[// return copy of last element]*\
}
\
template<typename T, template[<typename][,typename]> class Cont>
 template<typename T2, template[<typename][,typename]> class Cont2>
Stack<T,Cont>&\
Stack<T,Cont>::[operator]= (Stack<T2,Cont2> const& op2)
{
    elems.clear();                        *[// remove existing elements]*\
    elems.insert(elems.begin(),           *[// insert at the beginning]*\
                 op2.elems.begin(),       *[// all elements from]* [op2]\
                 op2.elems.end());
    return [\*this];\
}
```

Note again that to get access to all the members of `op2` we declare that all other stack instances are friends (omitting the names of the template parameters):

> 再次注意，为了访问“op2”的所有成员，我们声明所有其他堆栈实例都是朋友(省略模板参数的名称)：

```cpp
template<typename, template[<typename], typename[>class]>
[friend class] Stack;
```

Still, not _all_ standard container templates can be used for `Cont` parameter. For example, `std::array` will not work because it includes a nontype template parameter for the array length that has no match in our template template parameter declaration.

> 不过，并非所有标准容器模板都可以用于“Cont”参数。例如，“std:：array”将不起作用，因为它包含的数组长度的非类型模板参数在我们的模板模板参数声明中不匹配。

The following program uses all features of this final version:

```cpp
`basics/stack9test.cpp`

#include "stack9.hpp"\
#include <iostream>
#include <vector>
\
int main()
{
  Stack<int>   iStack;    *[// stack of]* [int*s
  Stack<[float]> fStack;    *[// stack of]* [float*s
\
*[// manipulate]* [int *stack
iStack.push(1);
iStack.push(2);
std::cout << "iStack.top(): " << iStack.top() << '\n';\
\
*[// manipulate]* [float *stack:
fStack.push(3.3);
std::cout << "fStack.top(): " << fStack.top() << '\n';\
\
*[// assign stack of different type and manipulate again]*\
fStack = iStack;\
fStack.push(4.4);
std::cout << "fStack.top(): " << fStack.top() << '\n';\
\
*[// stack for]* [doubles*s using a vector as an internal container
Stack<[double], std::vector> vStack;\
vStack.push(5.5);
vStack.push(6.6);
std::cout << "vStack.top(): " << vStack.top() << '\n';\
\
vStack = fStack;\
std::cout << "vStack: ";\
[while] (! vStack.empty()) {
  std::cout << vStack.top() << [' '];\
  vStack.pop();
}
std::cout << '\n';\
}
```

The program has the following output:

```cpp
iStack.top(): 2\
fStack.top(): 3.3\
fStack.top(): 4.4\
vStack.top(): 6.6\
vStack: 4.4 2 1
```

For further discussion and examples of template template parameters, see Section [[12.2.3]] on page [[187]], Section [[12.3.4]] on page [[197]], and Section [[19.2.2]] on page [[398]].

> 有关模板模板参数的进一步讨论和示例，请参见第[[187]]页第[[12.2.3]]节、第[[197]]页第[12.3.4]]节和第[[398]]页第][19.2.2]]节。

### 5.8 Summary

```cpp
  - To access a type name that depends on a template parameter, you have to qualify the name with a leading `typename`.
  - To access members of bases classes that depend on template parameters, you have to qualify the access by `this->` or their class name.
  - Nested classes and member functions can also be templates. One application is the ability to implement generic operations with internal type conversions.
  - Template versions of constructors or assignment operators don't replace predefined constructors or assignment operators.
  - By using braced initialization or explicitly calling a default constructor, you can ensure that variables and members of templates are initialized with a default value even if they are instantiated with a built-in type.
  - You can provide specific templates for raw arrays, which can also be applicable to string literals.
  - When passing raw arrays or string literals, arguments decay (perform an array-to-pointer conversion) during argument deduction if and only if the parameter is not a reference.
  - You can define *variable templates* (since C++14).
  - You can also use class templates as template parameters, as *template template parameters*.
  - Template template arguments must usually match their parameters exactly.

  ^[1]^ That is, a constructor with a parameter of type `std::initializer_list<X>`, for some type `X`.

  ^[2]^ Parameters of type `X (&)[]`---for some arbitrary type `X`---have become valid only in C++17, through the resolution of Core issue 393. However, many compilers accepted such parameters in earlier versions of the language.

  ^[3]^ This is a basic implementation to demonstrate the template features. Issues like proper exception handling are certainly missing.

  ^[4]^ Yes, we have very similar terms for very different things: A *variable template* is a variable that is a template (*variable* is a noun here). A *variadic template* is a template for a variadic number of template parameters (*variadic* is an adjective here).

  ^[5]^ Before C++17, there is an issue with this version that we explain in a minute. However, this affects only the default value `std::deque`. Thus, we can illustrate the general features of template template parameters with this default value before we discuss how to deal with it before C++17.
```

## Chapter 6

## Move Semantics and **enable_if<>**

One of the most prominent features C++11 introduced was _move semantics_. You can use it to optimize copying and assignments by moving ("stealing") internal resources from a source object to a destination object instead of copying those contents. This can be done provided the source no longer needs its internal value or state (because it is about to be discarded).

> C++11 引入的最突出的特性之一是动语义。您可以使用它来优化复制和分配，方法是将内部资源从源对象移动(“窃取”)到目标对象，而不是复制这些内容。只要源不再需要其内部值或状态(因为它即将被丢弃)，就可以做到这一点。

Move semantics has a significant influence on the design of templates, and special rules were introduced to support move semantics in generic code. This chapter introduces these features.

> 移动语义对模板的设计有着重要的影响，在泛型代码中引入了特殊的规则来支持移动语义。本章介绍这些功能。

### 6.1 Perfect Forwarding

Suppose you want to write generic code that forwards the basic property of passed arguments:

> 假设您想编写通用代码来转发传递参数的基本属性：

- Modifyable objects should be forwarded so that they still can be modified.
- Constant objects should be forwarded as read-only objects.
- Movable objects (objects we can "steal" from because they are about to expire) should be forwarded as movable objects.

> -可移动对象(我们可以“偷”的对象，因为它们即将过期)应该作为可移动对象转发。

To achieve this functionality without templates, we have to program all three cases. For example, to forward a call of `f()` to a corresponding function `g()`:

> 为了在没有模板的情况下实现这一功能，我们必须对所有三种情况进行编程。例如，要将“f()”的调用转发到相应的函数“g()”：

```cpp
`basics/move1.cpp`

#include <utility>
#include <iostream>
\
class X {
  *...*\
};
\
void g (X&) {
  std::cout << "g() for variable\\n";\
}
 void g (X const&) {
  std::cout << "g() for constant\\n";\
}
void g (X&&) {
  std::cout << "g() for movable object\\n";\
}
\
*[// let]* [f()] *[forward argument val to]* [g()]*[:]*\
void f (X& val) {
  g(val);             *[//]* [val] *[is non-]*const *[lvalue]* [=>] *[calls]* [g(X&)]\
}
void f (X const& val) {
  g(val);             *[//]* [val] *[is]* const *[lvalue]* [=>] *[calls]* [g(X const&)]\
}
void f (X&& val) {
  g(std::move(val));  *[//]* [val] *[is non-]*const *[lvalue]* [=>] *[needs]* [std::move()] *[to call]* [g(X&&)]\
}
\
int main()
{
  X v;              *[// create variable]*\
  X const c;        // create constant
\
  f(v);             *[//]* [f()] *[for nonconstant object calls]* [f(X&) =>] *[calls]* [g(X&)]\
  f(c);             *[//]* [f()] *[for constant object calls]* [f(X const&) =>] *[calls]* [g(X const&)]\
  f(X());           *[//]* [f()] *[for temporary calls]* [f(X&&) =>] *[calls]* [g(X&&)]\
  f(std::move(v));  *[//]* [f()] *[for movable variable calls]* [f(X&&) =>] *[calls]* [g(X&&)]\
}
```

Here, we see three different implementations of `f()` forwarding its argument to `g()`:

> 在这里，我们看到“f()”的三种不同实现将其参数转发到“g()”：

```cpp
void f (X& val) {
  g(val);             *[//]* [val] *[is non-]*const *[lvalue]* [=>] *[calls]* [g(X&)]\
}
void f (X const& val) {
  g(val);             *[//]* [val] *[is]* const *[lvalue]* [=>] *[calls]* [g(X const&)]\
}
void f (X&& val) {
  g(std::move(val));  *[//]* [val] *[is non-]*const *[lvalue]* [=>] *[needs]* [std::move()] *[to call]* [g(X&&)]\
}
```

Note that the code for movable objects (via an _rvalue reference_) differs from the other code: It needs a `std::move()` because according to language rules, move semantics is not passed through.[1] Although `val` in the third `f()` is declared as rvalue reference its value category when used as expression is a nonconstant lvalue (see [Appendix [B]]) and behaves as `val` in the first `f()`. Without the `move()`, `g(X&)` for nonconstant lvalues instead of `g(&&)` would be called.

> 请注意，可移动对象的代码(通过_rvalue reference_)与其他代码不同：它需要一个“std:：move()”，因为根据语言规则，移动语义是不传递的。[1] 尽管第三个“f()”中的“val”被声明为右值引用，但当用作表达式时，其值类别是一个非恒定的左值(请参见[附录[B]])，并且在第一个“f”中表现为“val”。如果没有“move()”，将调用非常值的“g(X&)”而不是“g(&&)”。

If we want to combine all three cases in generic code, we have a problem:

```cpp
template<typename T>
void f (T val) {
  g(T);
}
```

works for the first two cases, but not for the (third) case where movable objects are passed.

> 适用于前两种情况，但不适用于通过可移动对象的(第三种)情况。

C++11 for this reason introduces special rules for _perfect forwarding_ parameters. The idiomatic code pattern to achieve this is as follows:

> 由于这个原因，C++11 为_ perfect forwarding_参数引入了特殊规则。实现这一点的惯用代码模式如下：

```cpp
template<typename T>
void f (T&& val) {
  g(std::forward<T>(val));  // perfect forward [val] to [g()]\
}
```

Note that `std::move()` has no template parameter and "triggers" move semantics for the passed argument, while `std::forward<>()` "forwards" potential move semantic depending on a passed template argument.

> 请注意，“std:：move()”没有模板参数，并且“触发”了传递参数的移动语义，而“std：：forward＜＞()”则根据传递的模板参数“转发”了潜在的移动语义。

Don't assume that `T&&` for a template parameter `T` behaves as `X&&` for a specific type `X`. Different rules apply! However, syntactically they look identical:

> 不要假设模板参数“t”的“t&&”行为与特定类型“X”的“X&&&”相同。适用不同的规则！然而，在语法上它们看起来完全相同：

• `X&&` for a specific type `X` declares a parameter to be an rvalue reference. It can only be bound to a movable object (a prvalue, such as a temporary object, and an xvalue, such as an object passed with `std::move()`; see [Appendix [B]] for details). It is always mutable and you can always "steal" its value.[2]

> •特定类型“X”的“X&&”将参数声明为右值引用。它只能绑定到一个可移动对象(一个 prvalue，如临时对象，和一个 xvalue，如用“std:：move()”传递的对象；详见【附录【B】】)。它总是可变的，你总是可以“窃取”它的价值。2.

• `T&&` for a template parameter `T` declares a _forwarding reference_ (also called _universal reference_).[3] It can be bound to a mutable, immutable (i.e., `const`), or movable object. Inside the function definition, the parameter may be mutable, immutable, or refer to a value you can "steal" the internals from.

> •模板参数“T”的“T&&”声明了_forwarding reference_(也称为_universal reference_)。[3] 它可以绑定到可变、不可变(即“const”)或可移动对象。在函数定义中，参数可能是可变的、不可变的，或者引用一个可以“窃取”内部信息的值。

Note that `T` must really be the name of a template parameter. Depending on a template parameter is not sufficient. For a template parameter `T`, a declaration such as `typename T::iterator&&` is just an rvalue reference, not a forwarding reference.

> 请注意，“T”实际上必须是模板参数的名称。仅仅依靠模板参数是不够的。对于模板参数“T”，诸如“typename T：：迭代器&&”之类的声明只是右值引用，而不是转发引用。

So, the whole program to perfect forward arguments will look as follows:

```cpp
`basics/move2.cpp`

#include <utility>
#include <iostream>
\
class X {
  *...*\
};
\
void g (X&) {
  std::cout << "g() for variable\\n";\
}
void g (X const&) {
  std::cout << "g() for constant\\n";\
}
void g (X&&) {
  std::cout << "g() for movable object\\n";\
}
\
*[// let f() perfect forward argument val to g():]*\
template<typename T>
void f (T&& val) {
  g(std::forward<T>(val));   *[// call the right]* [g()] *[for any passed argument]* [val]\
}
\
int main()
{
  X v;              *[// create variable]*\
  X const c;        // create constant
\
  f(v);             *[//]* [f()] *[for variable calls]* [f(X&) =>] *[calls]* [g(X&)]\
  f(c);             *[//]* [f()] *[for constant calls]* [f(X const&)] => *[calls]* [g(X const&)]\
  f(X());           *[//]* [f()] *[for temporary calls]* [f(X&&) =>] *[calls]* [g(X&&)]\
  f(std::move(v));  *[//]* [f()] *[for move-enabled variable calls]* [f(X&&) =>] *[calls]* [g(X&&)]\
}
```

Of course, perfect forwarding can also be used with variadic templates (see Section [[4.3]] on page [[60]] for some examples). See Section [[15.6.3]] on page [[280]] for details of perfect forwarding.

> 当然，完美转发也可以与可变模板一起使用(有关一些示例，请参见第[[60]]页的第[[4.3]]节)。有关完美转发的详细信息，请参见第[[280]]页第[[15.6.3]]节。

### 6.2 Special Member Function Templates

Member function templates can also be used as special member functions, including as a constructor, which, however, might lead to surprising behavior.

> 成员函数模板也可以用作特殊的成员函数，包括构造函数，但这可能会导致令人惊讶的行为。

Consider the following example:

```cpp
`basics/specialmemtmpl1.cpp`

#include <utility>
#include <string>
#include <iostream>
\
class Person\
{
  private:\
    std::string name;\
  public:
    *[// constructor for passed initial name:]*\
    [explicit] Person(std::string const& n) : name(n) {
        std::cout << "copying string-CONSTR for '" << name << "'\\n";\
    }
    [explicit] Person(std::string&& n) : name(std::move(n)) {
        std::cout << "moving string-CONSTR for '" << name << "'\\n";\
    }
    *[// copy and move constructor:]*\
    Person (Person const& p) : name(p.name) {
        std::cout << "COPY-CONSTR Person '" << name << "'\\n";\
    }
    Person (Person&& p) : name(std::move(p.name)) {
        std::cout << "MOVE-CONSTR Person '" << name << "'\\n";\
    }
};
\
int main()
{
  std::string s = "sname";\
  Person p1(s);              *[// init with string object]* [=>] *[calls copying string-CONSTR]*\
  Person p2[(\"tmp");          *[// init with string literal]* [=>] *[calls moving string-CONSTR]*\
  Person p3(p1);             *[// copy Person]* [=>] *[calls COPY-CONSTR]*\
  Person p4(std::move(p1));  *[// move Person]* [=>] *[calls MOVE-CONST]*\
}
```

Here, we have a class `Person` with a string member `name` for which we provide initializing constructors. To support move semantics, we overload the constructor taking a `std::string`:

> 这里，我们有一个类“Person”，它有一个字符串成员“name”，我们为它提供初始化构造函数。为了支持移动语义，我们重载了采用“std:：string”的构造函数：

• We provide a version for string object the caller still needs, for which `name` is initialized by a copy of the passed argument:

> •我们为调用方仍然需要的字符串对象提供了一个版本，其中“name”由传递参数的副本初始化：

```cpp
Person(std::string const& n) : name(n) {
    std::cout << "copying string-CONSTR for '" << name << "'\\n";\
}
```

• We provide a version for movable string object, for which we call `std::move()` to "steal" the value from:

> •我们为可移动字符串对象提供了一个版本，为此我们调用“std:：move()”来“窃取”值：

```cpp
Person(std::string&& n) : name(std::move(n)) {
   std::cout << "moving string-CONSTR for '" << name << "'\\n";\
}
```

As expected, the first is called for passed string objects that are in use (lvalues), while the latter is called for movable objects (rvalues):

> 正如预期的那样，第一个用于正在使用的传递字符串对象(lvalues)，而后者用于可移动对象(rvalues)：

```cpp
std::string s = "sname";\
Person p1(s);              // init with string object `=>` calls copying string-CONSTR
Person p2[(\"tmp");          // init with string literal `=>` calls moving string-CONSTR
```

Besides these constructors, the example has specific implementations for the copy and move constructor to see when a `Person` as a whole is copied/moved:

> 除了这些构造函数之外，该示例还为复制和移动构造函数提供了特定的实现，以查看“Person”作为一个整体何时被复制/移动：

```cpp
Person p3(p1);             // copy Person [=>] calls COPY-CONSTR
Person p4(std::move(p1));  // move Person [=>] calls MOVE-CONSTR
```

Now let's replace the two string constructors with one generic constructor perfect forwarding the passed argument to the member `name`:

> 现在，让我们用一个泛型构造函数替换这两个字符串构造函数，完美地将传递的参数转发到成员“name”：

```cpp
`basics/specialmemtmpl2.hpp`

#include <utility>
#include <string>
#include <iostream>
\
class Person\
{
  private:\
    std::string name;\
  public:
    *[// generic constructor for passed initial name:]*\
    template<typename STR>
    [explicit] Person(STR&& n) : name(std::forward<STR>(n)) {
        std::cout << "TMPL-CONSTR for '" << name << "'\\n";\
    }
\
    *[// copy and move constructor:]*\
    Person (Person const& p) : name(p.name) {
        std::cout << "COPY-CONSTR Person '" << name << "'\\n";\
    }
     Person (Person&& p) : name(std::move(p.name)) {
        std::cout << "MOVE-CONSTR Person '" << name << "'\\n";\
    }
};
```

Construction with passed string works fine, as expected:

```cpp
std::string s = "sname";\
Person p1(s);              // init with string object [=>] calls TMPL-CONSTR
Person p2[(\"tmp");          //init with string literal [=>] calls TMPL-CONSTR
```

Note how the construction of `p2` does not create a temporary string in this case: The parameter `STR` is deduced to be of type `char const[4]`. Applying `std::forward<STR>` to the pointer parameter of the constructor has not much of an effect, and the `name` member is thus constructed from a null-terminated string.

> 请注意，在这种情况下，“p2”的构造不会创建临时字符串：参数“STR”被推断为“char const[4]”类型。将“std:：forward＜STR＞”应用于构造函数的指针参数并没有太大效果，因此“name”成员是由以 null 结尾的字符串构造的。

But when we attempt to call the copy constructor, we get an error:

```cpp
Person p3(p1);               // ERROR
```

while initializing a new `Person` by a movable object still works fine:

```cpp
Person p4(std::move(p1));  // OK: move Person [=>] calls MOVE-CONST
```

Note that also copying a constant `Person` works fine:

```cpp
Person const p2c[(\"ctmp");  //init constant object with string literal
Person p3c(p2c);           // OK: copy constant Person [=>] calls COPY-CONSTR
```

The problem is that, according to the overload resolution rules of C++ (see Section [[16.2.4]] on page [[333]]), for a nonconstant lvalue `Person p` the member template

> 问题是，根据 C++ 的过载解决规则(见第[[333]]页第[[16.2.4]]节)，对于非恒定左值“Person p”，成员模板

```cpp
template<typename STR>
Person(STR&& n)
```

is a better match than the (usually predefined) copy constructor:

```cpp
Person (Person const& p)
```

`STR` is just substituted with `Person&`, while for the copy constructor a conversion to `const` is necessary.

You might think about solving this by also providing a nonconstant copy constructor:

> 您可能会考虑通过提供一个非恒定副本构造函数来解决此问题：

```cpp
Person (Person& p)
```

However, that is only a partial solution because for objects of a derived class, the member template is still a better match. What you really want is to disable the member template for the case that the passed argument is a `Person` or an expression that can be converted to a `Person`. This can be done by using `std::enable_if<>`, which is introduced in the next section.

> 但是，这只是部分解决方案，因为对于派生类的对象，成员模板仍然是更好的匹配。您真正想要的是禁用成员模板，以防传递的参数是“Person”或可以转换为“Person’的表达式。这可以通过使用“std:：enable_if＜＞”来完成，这将在下一节中介绍。

### 6.3 Disable Templates with **enable_if<>**

Since C++11, the C++ standard library provides a helper template `std::enable_if<>` to ignore function templates under certain compile-time conditions.

> 自 C++11 以来，C++ 标准库提供了一个帮助模板“std:：enable_if＜＞”，用于在某些编译时条件下忽略函数模板。

For example, if a function template `foo<>()` is defined as follows:

```cpp
template<typename T>
typename std::enable_if<[(sizeof](T) > 4)>::type\
foo() {
}
```

this definition of `foo<>()` is ignored if `sizeof(T) > 4` yields `false`.[4] If `sizeof(T) > 4` yields `true`, the function template instance expands to

> 如果“sizeof(T)>4”产生“false”，则忽略“foo＜＞()”的定义。[4] 如果“sizeof(T)>4”产生“true”，则函数模板实例扩展为

```cpp
void foo() {
}
```

That is, `std::enable_if<>` is a type trait that evaluates a given compile-time expression passed as its (first) template argument and behaves as follows:

> 也就是说，“std:：enable_if＜＞”是一个类型特征，用于计算作为其(第一个)模板参数传递的给定编译时表达式，其行为如下：

• If the expression yields `true`, its type member `type` yields a type:

-- The type is `void` if no second template argument is passed.
-- Otherwise, the type is the second template argument type.

• If the expression yields `false`, the member `type` is not defined. Due to a template feature called SFINAE (substitution failure is not an error), which is introduced later (see Section [[8.4]] on page [[129]]), this has the effect that the function template with the `enable_if` expression is ignored.

> •如果表达式产生“false”，则不定义成员“type”。由于稍后介绍了一个名为 SFINAE 的模板功能(替换失败不是错误)(请参见第[[129]]页第[[8.4]]节)，这会导致忽略具有“enable_if”表达式的函数模板。

As for all type traits yielding a type since C++14, there is a corresponding alias template `std::enable_if_t<>`, which allows you to skip `typename` and `::type` (see Section [[2.8]] on page [[40]] for details). Thus, since C++14 you can write

> 对于 C++14 以来产生类型的所有类型特征，都有一个相应的别名模板“std:：enable_if_t<>'”，它允许您跳过“typename”和“：：type”(有关详细信息，请参阅第[[40]]页的第[[2.8]]节)。因此，由于 C++14，您可以编写

```cpp
template<typename T>
std::enable_if_t<([sizeof](T) > 4)>
foo() {
}
```

If a second argument is passed to `enable_if<>` or `enable_if_t<>`:

```cpp
template<typename T>
std::enable_if_t<([sizeof](T) > 4), T>
foo() {
  return T();
}
```

the `enable_if` construct expands to this second argument if the expression yields `true`. So, if `MyType` is the concrete type passed or deduced as `T`, whose size is larger than 4, the effect is

> 如果表达式产生“true”，那么“enable_if”构造将扩展到第二个参数。因此，如果“MyType”是传递或推导为“T”的具体类型，其大小大于 4，则效果为

```cpp
MyType foo();
```

Note that having the `enable_if` expression in the middle of a declaration is pretty clumsy. For this reason, the common way to use `std::enable_if<>` is to use an additional function template argument with a default value:

> 请注意，在声明中间使用“enable_if”表达式是相当笨拙的。因此，使用“std:：enable_if＜＞”的常见方法是使用具有默认值的附加函数模板参数：

```cpp
template<typename T,\
         typename = std::enable_if_t<[(sizeof](T) > 4)>>
void foo() {
}
```

which expands to

```cpp
template<typename T,\
         typename = [void]>
void foo() {
}
```

if `sizeof(T) > 4`.

If that is still too clumsy, and you want to make the requirement/constraint more explicit, you can define your own name for it using an alias template:[5]

> 如果这仍然过于笨拙，并且您希望使需求/约束更加明确，则可以使用别名模板为其定义自己的名称：[5]

```cpp
template<typename T>
using EnableIfSizeGreater4 = std::enable_if_t<[(sizeof](T) > 4)>;\
\
template<typename T,\
         typename = EnableIfSizeGreater4<T>>
void foo() {
}
```

See Section [[20.3]] on page [[469]] for a discussion of how `std::enable_if` is implemented.

> 关于如何实现“std:：enable_if”的讨论，请参见第[[469]]页第[[20.3]]节。

### 6.4 Using **enable_if<>**

We can use `enable_if<>` to solve our problem with the constructor template introduced in Section [[6.2]] on page [[95]].

> 我们可以使用 `enable_if<>` 来解决第[[95]]页第[[6.2]]节中介绍的构造函数模板的问题。

The problem we have to solve is to disable the declaration of the template constructor

> 我们必须解决的问题是禁用模板构造函数的声明

```cpp
template<typename STR>
Person(STR&& n);
```

if the passed argument `STR` has the right type (i.e., is a `std::string` or a type convertible to `std::string`).

> 如果传递的参数“STR”具有正确的类型(即为“std:：string”或可转换为“std：：string”的类型)。

For this, we use another standard type trait, `std::is_convertible<` _FROM_ `,` _TO_ `>`. With C++17, the corresponding declaration looks as follows:

> 为此，我们使用另一个标准类型特征，`std:：is_convertable<` _FROM_ `，` _TO_ `>`。对于 C++17，相应的声明如下所示：

```cpp
template<typename STR,\
         typename = std::enable_if_t<\
                      std::is_convertible_v<STR, std::string>>>
Person(STR&& n);
```

If type `STR` is convertible to type `std::string`, the whole declaration expands to

> 如果类型“STR”可转换为类型“std:：string”，则整个声明扩展为

```cpp
template<typename STR,\
         typename = [void]>
Person(STR&& n);
```

If type `STR` is not convertible to type `std::string`, the whole function template is ignored.[6]

> 如果类型“STR”不能转换为类型“std:：string”，则忽略整个函数模板。6.

Again, we can define our own name for the constraint by using an alias template:

> 同样，我们可以使用别名模板为约束定义自己的名称：

```cpp
template<typename T>
using EnableIfString = std::enable_if_t<\
                         std::is_convertible_v<T, std::string>>;\
...
template<typename STR, typename = EnableIfString<STR>>
Person(STR&& n);
```

Thus, the whole class `Person` should look as follows:

```cpp
`basics/specialmemtmpl3.hpp`

#include <utility>
#include <string>
#include <iostream>
#include <type_traits>
\
template<typename T>
using EnableIfString = std::enable_if_t<\
                         std::is_convertible_v<T,std::string>>;\
\
class Person\
{
  private:\
    std::string name;\
  public:
    *[// generic constructor for passed initial name:]*\
    template<typename STR, typename = EnableIfString<STR>>
    [explicit] Person(STR&& n)
     : name(std::forward<STR>(n)) {
        std::cout << "TMPL-CONSTR for '" << name << "'\\n";\
    }
     *[// copy and move constructor:]*\
    Person (Person const& p) : name(p.name) {
        std::cout << "COPY-CONSTR Person '" << name << "'\\n";\
    }
    Person (Person&& p) : name(std::move(p.name)) {
        std::cout << "MOVE-CONSTR Person '" << name << "'\\n";\
    }
};
```

Now, all calls behave as expected:

```cpp
`basics/specialmemtmpl3.cpp`

#include "specialmemtmpl3.hpp"\
\
int main()
{
  std::string s = "sname";\
  Person p1(s);              *[// init with string object]* [=>] *[calls TMPL-CONSTR]*\
  Person p2[(\"tmp");          *[// init with string literal]* [=>] *[calls TMPL-CONSTR]*\
  Person p3(p1);             *[// OK]* [=>] *[calls COPY-CONSTR]*\
  Person p4(std::move(p1));  *[// OK]* [=>] *[calls MOVE-CONST]*\
}
```

Note again that in C++14, we have to declare the alias template as follows, because the `_v` version is not defined for type traits that yield a value:

> 再次注意，在 C++14 中，我们必须如下声明别名模板，因为“_v”版本不是为产生值的类型特征定义的：

```cpp
template<typename T>
using EnableIfString = std::enable_if_t<\
                         std::is_convertible<T, std::string>::value>;
```

And in C++11, we have to declare the special member template as follows, because as written the `_t` version is not defined for type traits that yield a type:

> 在 C++11 中，我们必须如下声明特殊的成员模板，因为正如所写的那样，“_t”版本不是为产生类型的类型特征定义的：

```cpp
template<typename T>
using EnableIfString\
  = typename std::enable_if<std::is_convertible<T, std::string>::value\
                           >::type;
```

But that's all hidden now in the definition of `EnableIfString<>`.

Note also that there is an alternative to using `std::is_convertible<>` because it requires that the types are implicitly convertible. By using `std::is_constructible<>`, we also allow explicit conversions to be used for the initialization. However, the order of the arguments is the opposite is this case:

> 还要注意，还有一种替代方法可以使用“std:：is_convertable＜＞”，因为它要求类型是隐式可转换的。通过使用“std:：is_constructible＜＞”，我们还允许显式转换用于初始化。然而，在这种情况下，论点的顺序相反：

```cpp
template<typename T>
using EnableIfString = std::enable_if_t<\
                         std::is_constructible_v<std::string, T>>;
```

See Section [[D.3.2]] on page [[719]] for details about `std::is_constructible<>` and Section [[D.3.3]] on page [[727]] for details about `std::is_convertible<>`. See Section [[D.6]] on page [[734]] for details and examples to apply `enable_if<>` on variadic templates.

> 有关“std:：is_constructible<>'”的详细信息，请参见第[[719]]页的第[[D.3.2]]节；有关“std：：is_convertible<>`”的详细内容，请参阅第[[727]]页的[[D.3.3]]节。有关在可变模板上应用` enable_if<>` 的详细信息和示例，请参见第[[734]]页的第[[D.6]]节。

##### Disabling Special Member Functions

Note that normally we can't use `enable_if<>` to disable the predefined copy/move constructors and/or assignment operators. The reason is that member function templates never count as special member functions and are ignored when, for example, a copy constructor is needed. Thus, with this declaration:

> 请注意，通常我们不能使用 `enable_if<>` 来禁用预定义的复制/移动构造函数和/或赋值运算符。原因是成员函数模板从不算作特殊的成员函数，并且在需要复制构造函数时会被忽略。因此，在此声明中：

```cpp
class C {
  public:
    template<typename T>
    C (T const&) {
        std::cout << "tmpl copy constructor\\n";\
    }
    ...
};
```

the predefined copy constructor is still used, when a copy of a `C` is requested:

> 当请求“C”的副本时，仍然使用预定义的副本构造函数：

```cpp
C x;\
C y;  // still uses the predefined copy constructor (not the member template)
```

(There is really no way to use the member template because there is no way to specify or deduce its template parameter T.)

> (实际上没有办法使用成员模板，因为没有办法指定或推导其模板参数 T。)

Deleting the predefined copy constructor is no solution, because then the trial to copy a `C` results in an error.

> 删除预定义的复制构造函数不是解决方案，因为尝试复制“C”会导致错误。

There is a tricky solution, though:[7] We can declare a copy constructor for `const volatile` arguments and mark it "deleted" (i.e., define it with `= delete`). Doing so prevents another copy constructor from being implicitly declared. With that in place, we can define a constructor template that will be preferred over the (deleted) copy constructor for nonvolatile types:

> 不过，有一个棘手的解决方案：[7]我们可以为 `const-variable` 参数声明一个复制构造函数，并将其标记为“已删除”(即，用 `=delete` 定义它)。这样做可以防止隐式声明另一个复制构造函数。有了它，我们可以定义一个构造函数模板，该模板将优先于非易失性类型的(已删除的)复制构造函数：

```cpp
class C\
{
  public:
    *...*\
    // user-define the predefined copy constructor as deleted
    // (with conversion to* volatile] *[to enable better matches)]*\
    C(C [const volatile]&) = [delete];\
\
    *[// implement copy constructor template with better match:]*\
    template<typename T>
    C (T const&) {
        std::cout << "tmpl copy constructor\\n";\
     }
    *...*\
};
```

Now the template constructors are used even for "normal" copying:

```cpp
C x;\
C y;  // uses the member template
```

In such a template constructor we can then apply additional constraints with `enable_if<>`. For example, to prevent being able to copy objects of a class template `C<>` if the template parameter is an integral type, we can implement the following:

> 在这样的模板构造函数中，我们可以使用 `enable_if<>` 应用额外的约束。例如，如果模板参数是整型，为了防止复制类模板“C<>'”的对象，我们可以实现以下内容：

```cpp
template<typename T>
class C\
{
  public:
    *...*\
    // user-define the predefined copy constructor as deleted
    *// (with conversion to* [volatile] *[to enable better matches)]*\
    C(C [const volatile]&) = [delete];\
\
    *[// if]* [T] *[is no integral type, provide copy constructor template with better match:]*\
    template<typename U,\
             typename = std::enable_if_t<!std::is_integral<U>::value>>
    C (C<U> const&) {
        *...*\
    }
    *...*\
};
```

### 6.5 Using Concepts to Simplify **enable_if<>** Expressions

Even when using alias templates, the `enable_if` syntax is pretty clumsy, because it uses a work-around: To get the desired effect, we add an additional template parameter and "abuse" that parameter to provide a specific requirement for the function template to be available at all. Code like this is hard to read and makes the rest of the function template hard to understand.

> 即使在使用别名模板时，“enable_if”语法也相当笨拙，因为它使用了一种变通方法：为了获得所需的效果，我们添加了一个额外的模板参数并“滥用”该参数，以提供对函数模板可用的特定要求。像这样的代码很难阅读，并且使得函数模板的其余部分很难理解。

In principle, we just need a language feature that allows us to formulate requirements or constraints for a function in a way that causes the function to be ignored if the requirements/constraints are not met.

> 原则上，我们只需要一个语言功能，它允许我们为一个函数制定要求或约束，如果不满足要求/约束，就会忽略该函数。

This is an application of the long-awaited language feature _concepts_, which allows us to formulate requirements/conditions for templates with its own simple syntax. Unfortunately, although long discussed, concepts still did not become part of the C++17 standard. Some compilers provide experimental support for such a feature, however, and concepts will likely become part of the next standard after C++17.

> 这是期待已久的语言特性_concepts_的应用程序，它允许我们用自己的简单语法来制定模板的需求/条件。不幸的是，尽管讨论了很长时间，但概念仍然没有成为 C++17 标准的一部分。然而，一些编译器为这一特性提供了实验性支持，概念可能会成为继 C++17 之后的下一个标准的一部分。

With concepts, as their use is proposed, we simply have to write the following:

> 对于概念，在提出使用它们时，我们只需编写以下内容：

```cpp
template<typename STR>
[requires] std::is_convertible_v<STR,std::string>
Person(STR&& n) : name(std::forward<STR>(n)) {
    ...
}
```

We can even specify the requirement as a general concept

```cpp
template<typename T>
[concept] ConvertibleToString = std::is_convertible_v<T,std::string>;
```

and formulate this concept as a requirement:

```cpp
template<typename STR>
[requires] ConvertibleToString<STR>
Person(STR&& n) : name(std::forward<STR>(n)) {
    ...
}
```

This also can be formulated as follows:

```cpp
template<ConvertibleToString STR>
Person(STR&& n) : name(std::forward<STR>(n)) {
    ...
}
```

See [Appendix [E]] for a detailed discussion of concepts for C++.

### 6.6 Summary

- In templates, you can "perfectly" forward parameters by declaring them as *forwarding references* (declared with a type formed with the name of a template parameter followed by `&&`) and using `std::forward<>()` in the forwarded call.
- When using perfect forwarding member function templates, they might match better than the predefined special member function to copy or move objects.
- With `std::enable_if<>`, you can disable a function template when a compile-time condition is false (the template is then ignored once that condition has been determined).
- By using `std::enable_if<>` you can avoid problems when constructor templates or assignment operator templates that can be called for single arguments are a better match than implicitly generated special member functions.
- You can templify (and apply `enable_if<>`) to special member functions by deleting the predefined special member functions for `const volatile`.
- Concepts will allow us to use a more intuitive syntax for requirements on function templates.

^[1]^ The fact that move semantics is not automatically passed through is intentional and important. If it weren't, we would lose the value of a movable object the first time we use it in a function.
^[2]^ A type like `X const&&` is valid but provides no common semantics in practice because "stealing" the internal representation of a movable object requires modifying that object. It might be used, though, to force passing only temporaries or objects marked with `std::move()` without being able to modify them.
^[3]^ The term *universal reference* was coined by Scott Meyers as a common term that could result in either an "lvalue reference" or an "rvalue reference." Because "universal" was, well, too universal, the C++17 standard introduced the term *forwarding reference*, because the major reason to use such a reference is to forward objects. However, note that it does not automatically forward. The term does not describe what it is but what it is typically used for.
^[4]^ Don't forget to place the condition into parentheses, because otherwise the `>` in the condition would end the template argument list.
^[5]^ Thanks to Stephen C. Dewhurst for pointing that out.
^[6]^ If you wonder why we don't instead check whether `STR` is "not convertible to `Person`," beware: We are defining a function that might allow us to convert a string to a `Person`. So the constructor has to know whether it is enabled, which depends on whether it is convertible, which depends on whether it is enabled, and so on. Never use `enable_if` in places that impact the condition used by `enable_if`. This is a logical error that compilers do not necessarily detect.
^[7]^ Thanks to Peter Dimov for pointing out this technique.
