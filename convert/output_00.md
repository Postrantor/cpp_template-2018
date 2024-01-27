---
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

The authors and publisher have taken care in the preparation of this book, but make no expressed or implied warranty of any kind and assume no responsibility for errors or omissions. No liability is assumed for incidental or consequential damages in connection with or arising out of the use of the information or programs contained herein.

For information about buying this title in bulk quantities, or for special sales opportunities (which may include electronic versions; custom cover designs; and content particular to your business, training goals, marketing focus, or branding interests), please contact our corporate sales department at `corpsales@pearsoned.com` or (800) 382-3419.

For government sales inquiries, please contact `governmentsales@pearsoned.com`.

For questions about sales outside the U.S., please contact `intlcs@pearson.com`.

Visit us on the Web: `informit.com/aw`

Library of Congress Catalog Number: 2017946531

Copyright © 2018 Pearson Education, Inc.

This book was typeset by Nicolai M. Josuttis using the LATEX document processing system. All rights reserved. Printed in the United States of America. This publication is protected by copyright, and permission must be obtained from the publisher prior to any prohibited reproduction, storage in a retrieval system, or transmission in any form or by any means, electronic, mechanical, photocopying, recording, or likewise. For information regarding permissions, request forms and the appropriate contacts within the Pearson Education Global Rights & Permissions Department, please visit `www.pearsoned.com/permissions/`.

## Contents

```cpp
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

Much has changed in C++ since that first edition was published in late 2002. New iterations of the C++ standard have added new features, and continued innovation in the C++ community has uncovered new template-based programming techniques. The second edition of this book therefore retains the same goals as the first edition, but for "Modern C++."

We approached the task of writing this book with different backgrounds and with different intentions. David (aka "Daveed"), an experienced compiler implementer and active participant of the C++ Standard Committee working groups that evolve the core language, was interested in a precise and detailed description of all the power (and problems) of templates. Nico, an "ordinary" application programmer and member of the C++ Standard Committee Library Working Group, was interested in understanding all the techniques of templates in a way that he could use and benefit from them. Doug, a template library developer turned compiler implementer and language designer, was interested in collecting, categorizing, and evaluating the myriad techniques used to build template libraries. In addition, we all wanted to share this knowledge with you, the reader, and the whole community to help to avoid further misunderstanding, confusion, or apprehension.

As a consequence, you will see both conceptual introductions with day-to-day examples and detailed descriptions of the exact behavior of templates. Starting from the basic principles of templates and working up to the "art of template programming," you will discover (or rediscover) techniques such as static polymorphism, type traits, metaprogramming, and expression templates. You will also gain a deeper understanding of the C++ standard library, in which almost all code involves templates.

We learned a lot and we had much fun while writing this book. We hope you will have the same experience while reading it. Enjoy!

## Acknowledgments for the Second Edition

Writing a book is hard. Maintaining a book is even harder. It took us more than five years---spread over the past decade---to come up with this second edition, and it couldn't have been done without the support and patience of a lot of people.

First, we'd like to thank everyone in the C++ community and on the C++ standardization committee. In addition to all the work to add new language and library features, they spent many, many hours explaining and discussing their work with us, and they did so with patience and enthusiasm.

Part of this community also includes the programmers who gave feedback for errors and possible improvement for the first edition over the past 15 years. There are simply too many to list them all, but you know who you are and we're truly grateful to you for taking the time to write up your thoughts and observations. Please accept our apologies if our answers were sometimes less than prompt.

We'd also like to thank everyone who reviewed drafts of this book and provided us with valuable feedback and clarifications. These reviews brought the book to a significantly higher level of quality, and it again proved that good things need the input of many "wise guys." For this reason, huge thanks to Steve Dewhurst, Howard Hinnant, Mikael Kilpel¨ainen, Dietmar Kühl, Daniel Krügler, Nevin Lieber, Andreas Neiser, Eric Niebler, Richard Smith, Andrew Sutton, Hubert Tong, and Ville Voutilainen.

Of course, thanks to all the people who supported us from Addison-Wesley/Pearson. These days, you can no longer take professional support for book authors for granted. But they were patient, nagged us when appropriate, and were of great help when knowledge and professionalism were necessary. So, many thanks to Peter Gordon, Kim Boedigheimer, Greg Doench, Julie Nahil, Dana Wilson, and Carol Lallier.

A special thanks goes to the LaTeX community for a great text system and to Frank Mittelbach for solving our LATEX issues (it was almost always our fault).

### David's Acknowledgments for the Second Edition

This second edition was a long time in the waiting, and as we put the finishing touches to it, I am grateful for the people in my life who made it possible despite many obligations vying for attention. First, I'm indebted to my wife (Karina) and daughters (Alessandra and Cassandra), for agreeing to let me take significant time out of the "family schedule" to complete this edition, particularly in the last year of work. My parents have always shown interest in my goals, and whenever I visit them, they do not forget this particular project.

Clearly, this is a technical book, and its contents reflect knowledge and experience about a programming topic. However, that is not enough to pull off completing this kind of work. I'm therefore extremely grateful to Nico for having taken upon himself the "management" and "production" aspects of this edition (in addition to all of his technical contributions). If this book is useful to you and you run into Nico some day, be sure to tell him thanks for keeping us all going. I'm also thankful to Doug for having agreed to come on board several years ago and to keep going even as demands on his own schedule made for tough going.

Many programmers in our C++ community have shared nuggets of insight over the years, and I am grateful to all of them. However, I owe special thanks to Richard Smith, who has been efficiently answering my e-mails with arcane technical issues for years now. In the same vein, thanks to my colleagues John Spicer, Mike Miller, and Mike Herrick, for sharing their knowledge and creating an encouraging work environment that allows us to learn ever more.

### Nico's Acknowledgments for the Second Edition

First, I want to thank the two hard-core experts, David and Doug, because, as an application programmer and library expert, I asked so many silly questions and learned so much. I now feel like becoming a core expert (only until the next issue, of course). It was fun, guys.

All my other thanks go to Jutta Eckstein. Jutta has the wonderful ability to force and support people in their ideals, ideas, and goals. While most people experience this only occasionally when meeting her or working with her in our IT industry, I have the honor to benefit from her in my day-to-day life. After all these years, I still hope this will last forever.

### Doug's Acknowledgments for the Second Edition

My heartfelt thanks go to my wonderful and supportive wife, Amy, and our two little girls, Molly and Tessa. Their love and companionship bring me daily joy and the confidence to tackle the greatest challenges in life and work. I'd also like to thank my parents, who instilled in me a great love of learning and encouraged me throughout these years.

It was a pleasure to work with both David and Nico, who are so different in personality yet complement each other so well. David brings a great clarity to technical writing, honing in on descriptions that are precise and illuminating. Nico, beyond his exceptional organizational skills that kept two coauthors from wandering off into the weeds, brings a unique ability to take apart a complex technical discussion and make it simpler, more accessible, and far, far clearer.

## Acknowledgments for the First Edition

This book presents ideas, concepts, solutions, and examples from many sources. We'd like to thank all the people and companies who helped and supported us during the past few years.

First, we'd like to thank all the reviewers and everyone else who gave us their opinion on early manuscripts. These people endow the book with a quality it would never have had without their input. The reviewers for this book were Kyle Blaney, Thomas Gschwind, Dennis Mancl, Patrick Mc Killen, and Jan Christiaan van Winkel. Special thanks to Dietmar Kühl, who meticulously reviewed and edited the whole book. His feedback was an incredible contribution to the quality of this book.

We'd also like to thank all the people and companies who gave us the opportunity to test our examples on different platforms with different compilers. Many thanks to the Edison Design Group for their great compiler and their support. It was a big help during the standardization process and the writing of this book. Many thanks also go to all the developers of the free GNU and egcs compilers (Jason Merrill was especially responsive) and to Microsoft for an evaluation version of Visual C++ (Jonathan Caves, Herb Sutter, and Jason Shirk were our contacts there).

Much of the existing "C++ wisdom" was collectively created by the online C++ community. Most of it comes from the moderated Usenet groups `comp.lang.c++.moderated` and `comp.std.c++`. We are therefore especially indebted to the active moderators of those groups, who keep the discussions useful and constructive. We also much appreciate all those who over the years have taken the time to describe and explain their ideas for us all to share.

The Addison-Wesley team did another great job. We are most indebted to Debbie Lafferty (our editor) for her gentle prodding, good advice, and relentless hard work in support of this book. Thanks also go to Tyrrell Albaugh, Bunny Ames, Melanie Buck, Jacquelyn Doucette, Chanda Leary-Coutu, Catherine Ohala, and Marty Rabinowitz. We're grateful as well to Marina Lang, who first sponsored this book within Addison-Wesley. Susan Winer contributed an early round of editing that helped shape our later work.

### Nico's Acknowledgments for the First Edition

My first personal thanks go with a lot of kisses to my family: Ulli, Lucas, Anica, and Frederic supported this book with a lot of patience, consideration, and encouragement.

In addition, I want to thank David. His expertise turned out to be incredible, but his patience was even better (sometimes I ask really silly questions). It is a lot of fun to work with him.

### David's Acknowledgments for the First Edition

My wife, Karina, has been instrumental in this book coming to a conclusion, and I am immensely grateful for the role that she plays in my life. Writing "in your spare time" quickly becomes erratic when many other activities vie for your schedule. Karina helped me to manage that schedule, taught me to say "no" in order to make the time needed to make regular progress in the writing process, and above all was amazingly supportive of this project. I thank God every day for her friendship and love.

I'm also tremendously grateful to have been able to work with Nico. Besides his directly visible contributions to the text, his experience and discipline moved us from my pitiful doodling to a well-organized production.

John "Mr. Template" Spicer and Steve "Mr. Overload" Adamczyk are wonderful friends and colleagues, but in my opinion they are (together) also the ultimate authority regarding the core C++ language. They clarified many of the trickier issues described in this book, and should you find an error in the description of a C++ language element, it is almost certainly attributable to my failing to consult with them.

Finally, I want to express my appreciation to those who were supportive of this project without necessarily contributing to it directly (the power of cheer cannot be understated). First, my parents: Their love for me and their encouragement made all the difference. And then there are the numerous friends inquiring: "How is the book going?" They, too, were a source of encouragement: Michael Beckmann, Brett and Julie Beene, Jarran Carr, Simon Chang, Ho and Sarah Cho, Christophe De Dinechin, Ewa Deelman, Neil Eberle, Sassan Hazeghi, Vikram Kumar, Jim and Lindsay Long, R.J. Morgan, Mike Puritano, Ragu Raghavendra, Jim and Phuong Sharp, Gregg Vaughn, and John Wiegley.

## About This Book

The first edition of this book was published almost 15 years ago. We had set out to write the definitive guide to C++ templates, with the expectation that it would be useful to practicing C++ programmers. That project was successful: It's been tremendously gratifying to hear from readers who found our material helpful, to see our book time and again being recommended as a work of reference, and to be universally well reviewed.

That first edition has aged well, with most material remaining entirely relevant to the modern C++ programmer, but there is no denying that the evolution of the language---culminating in the "Modern C++" standards, C++11, C++14, and C++17---has raised the need for a revision of the material in the first edition.

So with this second edition, our high-level goal has remained unchanged: to provide the definitive guide to C++ templates, including both a solid reference and an accessible tutorial. This time, however, we work with the "Modern C++" language, which is a significantly bigger beast (still!) than the language available at the time of the prior edition.

We're also acutely aware that C++ programming resources have changed (for the better) since the first edition was published. For example, several books have appeared that develop specific template-based applications in great depth. More important, far more information about C++ templates and template-based techniques is easily available online, as are examples of advanced uses of these techniques. So in this edition, we have decided to emphasize a breadth of techniques that can be used in a variety of applications.

Some of the techniques we presented in the first edition have become obsolete because the C++ language now offers more direct ways of achieving the same effects. Those techniques have been dropped (or relegated to minor notes), and instead you'll find new techniques that show the state-ofthe-art uses of the new language.

We've now lived over 20 years with C++ templates, but the C++ programmers' community still regularly finds new fundamental insights into the way they can fit in our software development needs. Our goal with this book is to share that knowledge but also to fully equip the reader to develop new understanding and, perhaps, discover the next major C++ technique.

### What You Should Know Before Reading This Book

To get the most from this book, you should already know C++. We describe the details of a particular language feature, not the fundamentals of the language itself. You should be familiar with the concepts of classes and inheritance, and you should be able to write C++ programs using components such as IOstreams and containers from the C++ standard library. You should also be familiar with the basic features of "Modern C++", such as `auto`, `decltype`, move semantics, and lambdas. Nevertheless, we review more subtle issues as the need arises, even when such issues aren't directly related to templates. This ensures that the text is accessible to experts and intermediate programmers alike.

We deal primarily with the C++ language revisions standardized in 2011, 2014, and 2017. However, at the time of this writing, the ink is barely dry on the C++17 revision, and we expect that most of our readers will not be intimately familiar with its details. All revisions had a significant impact on the behavior and usage of templates. We therefore provide short introductions to those new features that have the greatest bearing on our subject matter. However, our goal is neither to introduce the modern C++ standards nor to provide an exhaustive description of the changes from the prior versions of this standard ([C++98] and [C++03]). Instead, we focus on templates as designed and used in C++, using the modern C++ standards ([C++11], [C++14], and [C++17]) as our basis, and we occasionally call out cases where the modern C++ standards enable or encourage different techniques than the prior standards.

### Overall Structure of the Book

Our goal is to provide the information necessary to start using templates and benefit from their power, as well as to provide information that will enable experienced programmers to push the limits of the state-of-the-art. To achieve this, we decided to organize our text in _parts_:

• [Part I] introduces the basic concepts underlying templates. It is written in a tutorial style.

• [Part II] presents the language details and is a handy reference to template-related constructs.

• [Part III] explains fundamental design and coding techniques supported by C++ templates. They range from near-trivial ideas to sophisticated idioms.

Each of these parts consists of several chapters. In addition, we provide a few appendixes that cover material not exclusively related to templates (e.g., an overview of overload resolution in C++). An additional appendix covers _concepts_, which is a fundamental extension to templates that has been included in the draft for a future standard (C++20, presumably).

The chapters of [Part I] are meant to be read in sequence. For example, [Chapter 3] builds on the material covered in [Chapter 2]. In the other parts, however, the connection between chapters is considerably looser. Cross references will help readers jump through the different topics.

Last, we provide a rather complete index that encourages additional ways to read this book out of sequence.

### How to Read This Book

If you are a C++ programmer who wants to learn or review the concepts of templates, carefully read [Part I], The Basics. Even if you're quite familiar with templates already, it may help to skim through this part quickly to familiarize yourself with the style and terminology that we use. This part also covers some of the logistical aspects of organizing your source code when it contains templates.

Depending on your preferred learning method, you may decide to absorb the many details of templates in [Part II], or instead you could read about practical coding techniques in [Part III] (and refer back to [Part II] for the more subtle language issues). The latter approach is probably particularly useful if you bought this book with concrete day-to-day challenges in mind.

The appendixes contain much useful information that is often referred to in the main text. We have also tried to make them interesting in their own right.

In our experience, the best way to learn something new is to look at examples. Therefore, you'll find a lot of examples throughout the book. Some are just a few lines of code illustrating an abstract concept, whereas others are complete programs that provide a concrete application of the material. The latter kind of examples will be introduced by a C++ comment describing the file containing the program code. You can find these files at the Web site of this book at `http://www.tmplbook.com`.

### Some Remarks About Programming Style

C++ programmers use different programming styles, and so do we: The usual questions about where to put whitespace, delimiters (braces, parentheses), and so forth came up. We tried to be consistent in general, although we occasionally make concessions to the topic at hand. For example, in tutorial sections, we may prefer generous use of whitespace and concrete names to help visualize code, whereas in more advanced discussions, a more compact style could be more appropriate.

We do want to draw your attention to one slightly uncommon decision regarding the declaration of types, parameters, and variables. Clearly, several styles are possible:

```cpp
void foo [(const int] &x);
void foo [(const int]& x);
void foo [(int const] &x);
void foo [(int const]& x);
```

Although it is a bit less common, we decided to use the order `int const` rather than `const int` for "constant integer." We have two reasons for using this order. First, it provides for an easier answer to the question, "_What_ is constant?" It's always what is in front of the `const` qualifier. Indeed, although

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

Our second reason has to do with a syntactical substitution principle that is very common when dealing with templates. Consider the following two type declarations using the `typedef` keyword:[1]

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

```cpp
[typedef char]\* const CPTR;      // constant pointer to [char]s
```

or:

```cpp
using CPTR = [char]\* const; // constant pointer to [char]s
```

However, if we write `const` _before_ the type it qualifies, this principle doesn't apply. Consider the alternative to our first two type definitions presented earlier:

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

```cpp
void foo [(int const]& x);
```

By doing this, we emphasize the separation between the parameter type and the parameter name. This is admittedly more confusing for declarations such as

```cpp
[char]\* a, b;
```

where, according to the rules inherited from C, `a` is a pointer but `b` is an ordinary `char`. To avoid such confusion, we simply avoid declaring multiple entities in this way.

This is primarily a book about language features. However, many techniques, features, and helper templates now appear in the C++ standard library. To connect these two, we therefore demonstrate template techniques by illustrating how they are used to implement certain library components, _and_ we use standard library utilities to build our own more complex examples. Hence, we use not only headers such as `<iostream>` and `<string>` (which contain templates but are not particularly relevant to define other templates) but also `<cstddef>`, `<utilities>`, `<functional>`, and `<type_traits>` (which do provide building blocks for more complex templates).

In addition, we provide a reference, [Appendix [D]], about the major template utilities provided by the C++ standard library, including a detailed description of all the standard type traits. These are commonly used at the core of sophisticated template programming

### The C++11, C++14, and C++17 Standards

The original C++ standard was published in 1998 and subsequently amended by a _technical corrigendum_ in 2003, which provided minor corrections and clarifications to the original standard. This "old C++ standard" is known as C++98 or C++03.

The C++11 standard was the first major revision of C++ driven by the ISO C++ standardization committee, bringing a wealth of new features to the language. A number of these new features interact with templates and are described in this book, including:

• Variadic templates
• Alias templates
• Move semantics, rvalue references, and perfect forwarding
• Standard type traits

C++14 and C++17 followed, both introducing some new language features, although the changes brought about by these standards were not quite as dramatic as those of C++11.[2] New features interacting with templates and described in this book include but are not limited to:

• Variable templates (C++14)
• Generic Lambdas (C++14)
• Class template argument deduction (C++17)
• Compile-time `if` (C++17)
• Fold expressions (C++17)

We even describe _concepts_ (template interfaces), which are currently slated for inclusion in the forthcoming C++20 standard.

At the time of this writing, the C++11 and C++14 standards are broadly supported by the major compilers, and C++17 is largely supported also. Still, compilers differ greatly in their support of the different language features. Several will compile most of the code in this book, but a few compilers may not be able to handle some of our examples. However, we expect that this problem will soon be resolved as programmers everywhere demand standard support from their vendors.

Even so, the C++ programming language is likely to continue to evolve as time passes. The experts of the C++ community (regardless of whether they participate in the C++ Standardization Committee) are discussing various ways to improve the language, and already several candidate improvements affect templates. [Chapter [17]] presents some trends in this area.

### Example Code and Additional Information

You can access all example programs and find more information about this book from its Web site, which has the following URL: [http://www.tmplbook.com](http://www.tmplbook.com)

### Feedback

We welcome your constructive input---both the negative and the positive. We worked very hard to bring you what we hope you'll find to be an excellent book. However, at some point we had to stop writing, reviewing, and tweaking so we could "release the product." You may therefore find errors, inconsistencies, and presentations that could be improved, or topics that are missing altogether. Your feedback gives us a chance to inform all readers through the book's Web site and to improve any subsequent editions.

The best way to reach us is by email. You will find the email address at the Web site of this book: [http://www.tmplbook.com](http://www.tmplbook.com)

Please, be sure to check the book's Web site for the currently known errata before submitting reports. Many thanks.

^[1]^ Note that in C++, a type definition defines a "type alias" rather than a new type (see Section [[2.8]] on page [[38]]).

For example:

```cpp
     >typedef int Length; *// define* Length *as an alias for* int\
    int i = 42;\
    Length l = 88;\
    i = l;        *// OK*\
    l = i;        *// OK*
```

^[2]^ The committee now aims at issuing a new standard roughly every 3 years. Clearly, that leaves less time for massive additions, but it brings the changes more quickly to the broader programming community. The development of larger features, then, spans time and might cover multiple standards.

## Part I The Basics

This part introduces the general concepts and language features of C++ templates. It starts with a discussion of the general goals and concepts by showing examples of function templates and class templates. It continues with some additional fundamental template features such as nontype template parameters, variadic templates, the keyword `typename`, and member templates. Also it discusses how to deal with move semantics, how to declare parameters, and how to use generic code for compile-time programming. It ends with some general hints about terminology and regarding the use and application of templates in practice both as application programmer and author of generic libraries.

### Why Templates?

C++ requires us to declare variables, functions, and most other kinds of entities using specific types. However, a lot of code looks the same for different types. For example, the implementation of the algorithm _quicksort_ looks structurally the same for different data structures, such as arrays of `int` s or vectors of strings, as long as the contained types can be compared to each other.

If your programming language doesn't support a special language feature for this kind of genericity, you only have bad alternatives:

1. You can implement the same behavior again and again for each type that needs this behavior.
2. You can write general code for a common base type such as `Object` or `void*`.
3. You can use special preprocessors.

If you come from other languages, you probably have done some or all of this before. However, each of these approaches has its drawbacks:

1. If you implement a behavior again and again, you reinvent the wheel. You make the same mistakes, and you tend to avoid complicated but better algorithms because they lead to even more mistakes.
2. If you write general code for a common base class, you lose the benefit of type checking. In addition, classes may be required to be derived from special base classes, which makes it more difficult to maintain your code.
3. If you use a special preprocessor, code is replaced by some "stupid text replacement mechanism" that has no idea of scope and types, which might result in strange semantic errors. Templates are a solution to this problem without these drawbacks. They are functions or classes that are written for one or more types not yet specified. When you use a template, you pass the types as arguments, explicitly or implicitly. Because templates are language features, you have full support of type checking and scope.

In today's programs, templates are used a lot. For example, inside the C++ standard library almost all code is template code. The library provides sort algorithms to sort objects and values of a specified type, data structures (also called _container classes_) to manage elements of a specified type, strings for which the type of a character is parameterized, and so on. However, this is only the beginning. Templates also allow us to parameterize behavior, to optimize code, and to parameterize information. These applications are covered in later chapters. Let's first start with some simple templates.

## Chapter 1

## Function Templates

This chapter introduces function templates. Function templates are functions that are parameterized so that they represent a family of functions.

### 1.1 A First Look at Function Templates

Function templates provide a functional behavior that can be called for different types. In other words, a function template represents a family of functions. The representation looks a lot like an ordinary function, except that some elements of the function are left undetermined: These elements are parameterized. To illustrate, let's look at a simple example.

#### 1.1.1 Defining the Template

The following is a function template that returns the maximum of two values:

```cpp
`basics/max1.hpp`

template<typename T>
T max (T a, T b)
{
    // if [b < a] then yield [a] else yield [b]\
    return b < a ? a : b;\
}
```

This template definition specifies a family of functions that return the maximum of two values, which are passed as function parameters `a` and `b`.[1] The type of these parameters is left open as _template parameter_ `T`. As seen in this example, template parameters must be announced with syntax of the following form:

```cpp
template< *comma-separated-list-of-parameters* >
```

In our example, the list of parameters is `typename T`. Note how the `<` and `>` tokens are used as brackets; we refer to these as _angle brackets_. The keyword `typename` introduces a _type parameter_. This is by far the most common kind of template parameter in C++ programs, but other parameters are possible, and we discuss them later (see [Chapter [3]]).

Here, the type parameter is `T`. You can use any identifier as a parameter name, but using `T` is the convention. The type parameter represents an arbitrary type that is determined by the caller when the caller calls the function. You can use any type (fundamental type, class, and so on) as long as it provides the operations that the template uses. In this case, type `T` has to support operator `<` because `a` and `b` are compared using this operator. Perhaps less obvious from the definition of `max()` is that values of type `T` must also be copyable in order to be returned.[2]

For historical reasons, you can also use the keyword `class` instead of `typename` to define a type parameter. The keyword `typename` came relatively late in the evolution of the C++98 standard. Prior to that, the keyword `class` was the only way to introduce a type parameter, and this remains a valid way to do so. Hence, the template `max()` could be defined equivalently as follows:

```cpp
template<class T>
T max (T a, T b)
{
    return b < a ? a : b;\
}
```

Semantically there is no difference in this context. So, even if you use `class` here, _any_ type may be used for template arguments. However, because this use of `class` can be misleading (not only class types can be substituted for `T`), you should prefer the use of `typename` in this context. However, note that unlike class type declarations, the keyword `struct` cannot be used in place of `typename` when declaring type parameters.

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

```cpp
max(7,i): 42\
max(f1,f2): 3.4\
max(s1,s2): mathematics
```

Note that each call of the `max()` template is qualified with `::`. This is to ensure that our `max()` template is found in the global namespace. There is also a `std::max()` template in the standard library, which under some circumstances may be called or may lead to ambiguity.[3]

Templates aren't compiled into single entities that can handle any type. Instead, different entities are generated from the template for every type for which the template is used.[4] Thus, `max()` is compiled for each of these three types. For example, the first call of `max()`

```cpp
int i = 42;\
... max(7,i) ...
```

uses the function template with `int` as template parameter `T`. Thus, it has the semantics of calling the following code:

```cpp
int max [(int] a, int b)
{
    return b < a ? a : b;\
}
```

The process of replacing template parameters by concrete types is called _instantiation_. It results in an _instance_ of a template.[5]

Note that the mere use of a function template can trigger such an instantiation process. There is no need for the programmer to request the instantiation separately.

Similarly, the other calls of `max()` instantiate the `max` template for `double` and `std::string` as if they were declared and implemented individually:

```cpp
[double] max [(double], [double]);
std::string max (std::string, std::string);
```

Note also that `void` is a valid template argument provided the resulting code is valid. For example:

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

```cpp
std::complex<[float]> c1, c2;        // doesn't provide operator [<]\
...
::max(c1,c2);                     // ERROR at compile time
```

Thus, templates are "compiled" in two phases:

1. Without instantiation at _definition time_, the template code itself is checked for correctness ignoring the template parameters. This includes:

-- Syntax errors are discovered, such as missing semicolons.
-- Using unknown names (type names, function names, ...) that don't depend on template parameters are discovered.
-- Static assertions that don't depend on template parameters are checked.

2. At _instantiation time_, the template code is checked (again) to ensure that all code is valid. That is, now especially, all parts that depend on template parameters are double-checked.

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

Note that some compilers don't perform the full checks of the first phase.[6] So you might not see general problems until the template code is instantiated at least once.

#### Compiling and Linking

Two-phase translation leads to an important problem in the handling of templates in practice: When a function template is used in a way that triggers its instantiation, a compiler will (at some point) need to see that template's definition. This breaks the usual compile and link distinction for ordinary functions, when the declaration of a function is sufficient to compile its use. Methods of handling this problem are discussed in [Chapter [9]]. For the moment, let's take the simplest approach: Implement each template inside a header file.

### 1.2 Template Argument Deduction

When we call a function template such as `max()` for some arguments, the template parameters are determined by the arguments we pass. If we pass two `int` s to the parameter types `T`, the C++ compiler has to conclude that `T` must be `int`.

However, `T` might only be "part" of the type. For example, if we declare `max()` to use constant references:

```cpp
template<typename T>
T max (T const& a, T const& b)
{
    return b < a ? a : b;\
}
```

and pass `int`, again `T` is deduced as `int`, because the function parameters match for `int const&`.

##### Type Conversions During Type Deduction

Note that automatic type conversions are limited during type deduction:

• When declaring call parameters by reference, even trivial conversions do not apply to type deduction. Two arguments declared with the same template parameter `T` must match exactly.

• When declaring call parameters by value, only trivial conversions that _decay_ are supported: Qualifications with `const` or `volatile` are ignored, references convert to the referenced type, and raw arrays or functions convert to the corresponding pointer type. For two arguments declared with the same template parameter `T` the _decayed_ types must match.

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

```cpp
`max<double>(4, 7.2);`                   // OK
```

3. Specify that the parameters may have different types.

Section [[1.3]] on page [[9]] will elaborate on these options. Section [[7.2]] on page [[108]] and [Chapter [15]] will discuss the rules for type conversions during type deduction in detail.

##### Type Deduction for Default Arguments

Note also that type deduction does not work for default call arguments. For example:

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

```cpp
template<typename T = std::string>
void f(T = "");
...
f();        // OK
```

### 1.3 Multiple Template Parameters

As we have seen so far, function templates have two distinct sets of parameters:

1. _Template parameters_, which are declared in angle brackets before the function template name:

```cpp
template<typename T>        // [T] is template parameter
```

2. _Call parameters_, which are declared in parentheses after the function template name:

```cpp
T max (T a, T b)            // [a] and [b] are call parameters
```

You may have as many template parameters as you like. For example, you could define the `max()` template for call parameters of two potentially different types:

```cpp
template<typename T1, typename T2>
T1 max (T1 a, T2 b)
{
    return b < a ? a : b; }
...
auto m = ::max(4, 7.2);        // OK, but type of first argument defines return type
```

It may appear desirable to be able to pass parameters of different types to the `max()` template, but, as this example shows, it raises a problem. If you use one of the parameter types as return type, the argument for the other parameter might get converted to this type, regardless of the caller's intention. Thus, the return type depends on the call argument order. The maximum of 66.66 and 42 will be the `double` 66.66, while the maximum of 42 and 66.66 will be the `int` 66.

C++ provides different ways to deal with this problem:

• Introduce a third template parameter for the return type.
• Let the compiler find out the return type.
• Declare the return type to be the "common type" of the two parameter types.

All these options are discussed next.

#### 1.3.1 Template Parameters for Return Types

Our earlier discussion showed that _template argument deduction_ allows us to call function templates with syntax identical to that of calling an ordinary function: We do not have to explicitly specify the types corresponding to the template parameters.

We also mentioned, however, that we can specify the types to use for the template parameters explicitly:

```cpp
template<typename T>
T max (T a, T b);
...
::max<[double]>(4, 7.2);        // instantiate [T] as [double]
```

In cases when there is no connection between template and call parameters and when template parameters cannot be determined, you must specify the template argument explicitly with the call. For example, you can introduce a third template argument type to define the return type of a function template:

```cpp
template<typename T1, typename T2, typename RT>
RT max (T1 a, T2 b);
```

However, template argument deduction does not take return types into account,[7] and `RT` does not appear in the types of the function call parameters. Therefore, `RT` cannot be deduced.[8]

As a consequence, you have to specify the template argument list explicitly. For example:

```cpp
template<typename T1, typename T2, typename RT>
RT max (T1 a, T2 b);
...
::max<int,[double],[double]>(4, 7.2);        // OK, but tedious
```

So far, we have looked at cases in which either all or none of the function template arguments were mentioned explicitly. Another approach is to specify only the first arguments explicitly and to allow the deduction process to derive the rest. In general, you must specify all the argument types up to the last argument type that cannot be determined implicitly. Thus, if you change the order of the template parameters in our example, the caller needs to specify only the return type:

```cpp
template<typename RT, typename T1, typename T2>
RT max (T1 a, T2 b);
...
::max<[double]>(4, 7.2)        //OK: return type is [double], [T1] and [T2] are deduced
```

In this example, the call to `max<double>` explicitly sets `RT` to `double`, but the parameters `T1` and `T2` are deduced to be `int` and `double` from the arguments.

Note that these modified versions of `max()` don't lead to significant advantages. For the one-parameter version you can already specify the parameter (and return) type if two arguments of a different type are passed. Thus, it's a good idea to keep it simple and use the one-parameter version of `max()` (as we do in the following sections when discussing other template issues).

See [Chapter [15]] for details of the deduction process.

#### 1.3.2 Deducing the Return Type

If a return type depends on template parameters, the simplest and best approach to deduce the return type is to let the compiler find out. Since C++14, this is possible by simply not declaring any return type (you still have to declare the return type to be `auto`):

```cpp
`basics/maxauto.hpp`

template<typename T1, typename T2>
auto max (T1 a, T2 b)
{
  return b < a ? a : b;\
}
```

In fact, the use of `auto` for the return type without a corresponding _trailing return type_ (which would be introduced with a `->` at the end) indicates that the actual return type must be deduced from the return statements in the function body. Of course, deducing the return type from the function body has to be possible. Therefore, the code must be available and multiple return statements have to match.

Before C++14, it is only possible to let the compiler determine the return type by more or less making the implementation of the function part of its declaration. In C++11 we can benefit from the fact that the _trailing return type_ syntax allows us to use the call parameters. That is, we can _declare_ that the return type is derived from what `operator?:` yields:

```cpp
`basics/maxdecltype.hpp`

template<typename T1, typename T2>
auto max (T1 a, T2 b) -> decltype(b<a?a:b)
{
  return b < a ? a : b;\
}
```

Here, the resulting type is determined by the rules for operator `?:`, which are fairly elaborate but generally produce an intuitively expected result (e.g., if `a` and `b` have different arithmetic types, a common arithmetic type is found for the result).

Note that

```cpp
template<typename T1, typename T2>
auto max (T1 a, T2 b) -> decltype(b<a?a:b);
```

is a _declaration_, so that the compiler uses the rules of `operator?:` called for parameters `a` and `b` to find out the return type of `max()` at compile time. The implementation does not necessarily have to match. In fact, using `true` as the condition for `operator?:` in the declaration is enough:

```cpp
template<typename T1, typename T2>
auto max (T1 a, T2 b) -> decltype[(true]?a:b);
```

However, in any case this definition has a significant drawback: It might happen that the return type is a reference type, because under some conditions `T` might be a reference. For this reason you should return the type _decayed_ from `T`, which looks as follows:

```cpp
`basics/maxdecltypedecay.hpp`

#include <type_traits>
template<typename T1, typename T2>
auto max (T1 a, T2 b) -> typename std::decay[<decltype][(true]?a:b)>::type\
 b < a ? a : b;\
}
```

Here, the type trait `std::decay<>` is used, which returns the resulting type in a member `type`. It is defined by the standard library in `<type_trait>` (see Section [[D.5]] on page [[732]]). Because the member `type` is a type, you have to qualify the expression with `typename` to access it (see Section [[5.1]] on page [[67]]).

Note that an initialization of type `auto` always decays. This also applies to return values when the return type is just `auto`. `auto` as a return type behaves just as in the following code, where `a` is declared by the decayed type of `i`, `int`:

```cpp
int i = 42;\
[int const]& ir = i;        // [ir] refers to
[i] auto a = ir;            // [a] is declared as new object of type int
```

#### 1.3.3 Return Type as Common Type

Since C++11, the C++ standard library provides a means to specify choosing "the more general type." `std::common_type<>::type` yields the "common type" of two (or more) different types passed as template arguments. For example:

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

```cpp
typename std::common_type<T1,T2>::type        //since C++11
```

However, since C++14 you can simplify the usage of traits like this by appending `_t` to the trait name and skipping `typename` and `::type` (see Section [[2.8]] on page [[40]] for details), so that the return type definition simply becomes:

```cpp
std::common_type_t<T1,T2>                    // equivalent since C++14
```

The way `std::common_type<>` is implemented uses some tricky template programming, which is discussed in Section [[26.5.2]] on page [[622]]. Internally, it chooses the resulting type according to the language rules of operator `?:` or specializations for specific types. Thus, both `::max(4, 7.2)` and `::max(7.2, 4)` yield the same value 7.2 of type `double`. Note that `std::common_type<>` also decays. See Section [[D.5]] on page [[732]] for details.

### 1.4 Default Template Arguments

You can also define default values for template parameters. These values are called _default template arguments_ and can be used with any kind of template.[9] They may even refer to previous template parameters.

For example, if you want to combine the approaches to define the return type with the ability to have multiple parameter types (as discussed in the section before), you can introduce a template parameter `RT` for the return type with the common type of the two arguments as default. Again, we have multiple options:

1. We can use `operator?:` directly. However, because we have to apply `operator?:` before the call parameters `a` and `b` are declared, we can only use their types:

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

Note also that this implementation requires that we are able to call default constructors for the passed types. There is another solution, using `std::declval`, which, however, makes the declaration even more complicated. See Section [[11.2.3]] on page [[166]] for an example.

2. We can also use the `std::common_type<>` type trait to specify the default value for the return type:

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

```cpp
auto a = ::max(4, 7.2);
```

or specify the return type after all other argument types explicitly:

```cpp
auto b = ::max[<double][,int][,long double]>(7.2, 4);
```

However, again we have the problem that we have to specify three types to be able to specify the return type only. Instead, we would need the ability to have the return type as the first template parameter, while still being able to deduce it from the argument types. In principle, it is possible to have default arguments for leading function template parameters even if parameters without default arguments follow:

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

For all these reasons, the best and easiest solution is to let the compiler deduce the return type as proposed in Section [[1.3.2]] on page [[11]].

### 1.5 Overloading Function Templates

Like ordinary functions, function templates can be overloaded. That is, you can have different function definitions with the same function name so that when that name is used in a function call, a C++ compiler must decide which one of the various candidates to call. The rules for this decision may become rather complicated, even without templates. In this section we discuss overloading when templates are involved. If you are not familiar with the basic rules of overloading without templates, please look at [Appendix [C]], where we provide a reasonably detailed survey of the overload resolution rules.

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

```cpp
::max(7, 42);        // both int values match the nontemplate function perfectly
```

If the template can generate a function with a better match, however, then the template is selected. This is demonstrated by the second and third calls of `max()`:

```cpp
::max(7.0, 42.0);        // calls the [max<double>] (by argument deduction)
::max(['a'], ['b']);          //calls the [max<char>] (by argument deduction)
```

Here, the template is a better match because no conversion from `double` or `char` to `int` is required (see Section [[C.2]] on page [[682]] for the rules of overload resolution).

It is also possible to specify explicitly an empty template argument list. This syntax indicates that only templates may resolve a call, but all the template parameters should be deduced from the call arguments:

```cpp
::max<>(7, 42);        // calls [max<int>] (by argument deduction)
```

Because automatic type conversion is not considered for deduced template parameters but is considered for ordinary function parameters, the last call uses the nontemplate function (while `’a’` and `42.7` both are converted to `int`):

```cpp
::max(['a'], 42.7);        //only the nontemplate function allows nontrivial conversions
```

An interesting example would be to overload the maximum template to be able to explicitly specify the return type only:

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

A useful example would be to overload the maximum template for pointers and ordinary C-strings:

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

```cpp
return max (max(a,b), c);
```

becomes a run-time error because for C-strings, `max(a,b)` creates a new, temporary local value that is returned by reference, but that temporary value expires as soon as the return statement is complete, leaving `main()` with a dangling reference. Unfortunately, the error is quite subtle and may not manifest itself in all cases.[11]

Note, in contrast, that the first call to `max()` in `main()` doesn't suffer from the same issue. There temporaries are created for the arguments (7, 42, and 68), but those temporaries are created in `main()` where they persist until the statement is done.

This is only one example of code that might behave differently than expected as a result of detailed overload resolution rules. In addition, ensure that all overloaded versions of a function are declared before the function is called. This is because the fact that not all overloaded functions are visible when a corresponding function call is made may matter. For example, defining a three-argument version of `max()` without having seen the declaration of a special two-argument version of `max()` for `int` s causes the two-argument template to be used by the three-argument version:

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

#### 1.6.1 Pass by Value or by Reference?

You might wonder, why we in general declare the functions to pass the arguments by value instead of using references. In general, passing by reference is recommended for types other than cheap simple types (such as fundamental types or `std::string_view`), because no unnecessary copies are created.

However, for a couple of reasons, passing by value in general is often better:

• The syntax is simple.
• Compilers optimize better.
• Move semantics often makes copies cheap.
• And sometimes there is no copy or move at all.

In addition, for templates, specific aspects come into play:

• A template might be used for both simple and complex types, so choosing the approach for complex types might be counter-productive for simple types.
• As a caller you can often still decide to pass arguments by reference, using `std::ref()` and `std::cref()` (see Section [[7.3]] on page [[112]]).
• Although passing string literals or raw arrays always can become a problem, passing them by reference often is considered to become the bigger problem. All this will be discussed in detail in [Chapter [7]]. For the moment inside the book we will usually pass arguments by value unless some functionality is only possible when using references.

#### 1.6.2 Why Not **inline**?

In general, function templates don't have to be declared with `inline`. Unlike ordinary noninline functions, we can define noninline function templates in a header file and include this header file in multiple translation units.

The only exception to this rule are full specializations of templates for specific types, so that the resulting code is no longer generic (all template parameters are defined). See Section [[9.2]] on page [[140]] for more details.

From a strict language definition perspective, `inline` only means that a definition of a function can appear multiple times in a program. However, it is also meant as a hint to the compiler that calls to that function should be "expanded inline": Doing so can produce more efficient code for certain cases, but it can also make the code less efficient for many other cases. Nowadays, compilers usually are better at deciding this without the hint implied by the `inline` keyword. However, compilers still account for the presence of `inline` in that decision.

#### 1.6.3 Why Not **constexpr**?

Since C++11, you can use `constexpr` to provide the ability to use code to compute some values at compile time. For a lot of templates this makes sense.

For example, to be able to use the maximum function at compile time, you have to declare it as follows:

```cpp
`basics/maxconstexpr.hpp`

template<typename T1, typename T2>
[constexpr auto] max (T1 a, T2 b)
{
  return b < a ? a : b;\
}
```

With this, you can use the maximum function template in places with compile-time context, such as when declaring the size of a raw array:

```cpp
int a[::max[(sizeof][(char]),1000u)];
```

or the size of a `std::array<>`:

```cpp
std::array<std::string, ::max[(sizeof][(char]),1000u)> arr;
```

Note that we pass `1000` as `unsigned int` to avoid warnings about comparing a signed with an unsigned value inside the template.

Section [[8.2]] on page [[125]] will discuss other examples of using `constexpr`. However, to keep our focus on the fundamentals, we usually will skip `constexpr` when discussing other template features.

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

### 2.1 Implementation of Class Template **Stack**

As we did with function templates, we declare and define class `Stack<>` in a header file as follows:

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

#### 2.1.1 Declaration of Class Templates

Declaring class templates is similar to declaring function templates: Before the declaration, you have to declare one or multiple identifiers as a type parameter(s). Again, `T` is usually used as an identifier:

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

If, for example, you have to declare your own copy constructor and assignment operator, it typically looks like this:

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

However, outside the class structure you'd need:

```cpp
template<typename T>
[bool operator]== (Stack<T> const& lhs, Stack<T> const& rhs);
```

Note that in places where the name and not the type of the class is required, only `Stack` may be used. This is especially the case when you specify the _name_ of constructors (not their arguments) and the destructor.

Note also that, unlike nontemplate classes, you can't declare or define class templates inside functions or block scope. In general, templates can only be defined in global/namespace scope or inside class declarations (see Section [[12.1]] on page [[177]] for details).

#### 2.1.2 Implementation of Member Functions

To define a member function of a class template, you have to specify that it is a template, and you have to use the full type qualification of the class template. Thus, the implementation of the member function `push()` for type `Stack<T>` looks like this:

```cpp
template<typename T>
void Stack<T>::push (T const& elem)
{
   elems.push_back(elem);        // append copy of passed [elem]\
}
```

In this case, `push_back()` of the element vector is called, which appends the element at the end of the vector.

Note that `pop_back()` of a vector removes the last element but doesn't return it. The reason for this behavior is exception safety. It is impossible to implement a completely exception-safe version of `pop()` that returns the removed element (this topic was first discussed by Tom Cargill in [CargillExceptionSafety] and is discussed as Item 10 in [SutterExceptional]). However, ignoring this danger, we could implement a `pop()` that returns the element just removed. To do this, we simply use `T` to declare a local variable of the element type:

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

```cpp
template<typename T>
T const& Stack<T>::top () const\
{
    assert(!elems.empty());
   return elems.back();        // return copy of last element
}
```

Of course, as for any member function, you can also implement member functions of class templates as an inline function inside the class declaration. For example:

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

Note that code is instantiated _only for template (member) functions that are called_. For class templates, member functions are instantiated only if they are used. This, of course, saves time and space and allows use of class templates only partially, which we will discuss in Section [[2.3]] on page [[29]].

In this example, the default constructor, `push()`, and `top()` are instantiated for both `int` and strings. However, `pop()` is instantiated only for strings. If a class template has static members, these are also instantiated once for each type for which the class template is used.

An instantiated class template's type can be used just like any other type. You can qualify it with `const` or `volatile` or derive array and reference types from it. You can also use it as part of a type definition with `typedef` or `using` (see Section [[2.8]] on page [[38]] for details about type definitions) or use it as a type parameter when building another template type. For example:

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

```cpp
Stack< [float]\*>     floatPtrStack;        // stack of [float] pointers
Stack<Stack< int>> intStackStack;        // stack of stack of ints
```

The only requirement is that any operation that is called is possible according to this type.

Note that before C++11 you had to put whitespace between the two closing template brackets:

```cpp
Stack<Stack< int> > intStackStack;        // OK with all C++ versions
```

If you didn't do this, you were using operator `>>`, which resulted in a syntax error:

```cpp
`Stack<Stack< int>> intStackStack;`        // ERROR before C++11
```

The reason for the old behavior was that it helped the first pass of a C++ compiler to tokenize the source code independent of the semantics of the code. However, because the missing space was a typical bug, which required corresponding error messages, the semantics of the code more and more had to get taken into account anyway. So, with C++11 the rule to put a space between two closing template brackets was removed with the "angle bracket hack" (see Section [[13.3.1]] on page [[226]] for details).

### 2.3 Partial Usage of Class Templates

A class template usually applies multiple operations on the template arguments it is instantiated for (including construction and destruction). This might lead to the impression that these template arguments have to provide all operations necessary for all member functions of a class template. But this is not the case: Template arguments only have to provide all necessary operations that _are_ needed (instead of that _could_ be needed).

If, for example, class `Stack<>` would provide a member function `printOn()` to print the whole stack content, which calls `operator<<` for each element:

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

```cpp
Stack<std::pair< int, int>> ps;        // note: [std::pair<>] has no [operator<<] defined
ps.push();                       // OK
ps.push();                       // OK
std::cout << ps.top().first << '\n';         // OK
std::cout << ps.top().second << '\n';        // OK
```

Only if you call `printOn()` for such a stack, the code will produce an error, because it can't instantiate the call of `operator<<` for this specific element type:

```cpp
ps.printOn(std::cout);     // ERROR: [operator<<] not supported for element type
```

#### 2.3.1 Concepts

This raises the question: How do we know which operations are required for a template to be able to get instantiated? The term _concept_ is often used to denote a set of constraints that is repeatedly required in a template library. For example, the C++ standard library relies on such concepts as _random access iterator_ and _default constructible_.

Currently (i.e., as of C++17), concepts can more or less only be expressed in the documentation (e.g., code comments). This can become a significant problem because failures to follow constraints can lead to terrible error messages (see Section [[9.4]] on page [[143]]).

For years, there have also been approaches and trials to support the definition and validation of concepts as a language feature. However, up to C++17 no such approach was standardized yet.

Since C++11, you can at least check for some basic constraints by using the `static_assert` keyword and some predefined type traits. For example:

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

However, more complicated code is necessary to check, for example, objects of type `T` provide a specific member function or that they can be compared using operator `<`. See Section [[19.6.3]] on page [[436]] for a detailed example of such code.

See [Appendix [E]] for a detailed discussion of concepts for C++.

### 2.4 Friends

Instead of printing the stack contents with `printOn()` it is better to implement `operator<<` for the stack. However, as usual `operator<<` has to be implemented as nonmember function, which then could call `printOn()` inline:

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

However, when trying to _declare_ the friend function and _define_ it afterwards, things become more complicated. In fact, we have two options:

1. We can implicitly declare a new function template, which must use a different template parameter, such as `U`:

```cpp
template<typename T>
class Stack {
   ...
   template<typename U>
   [friend] std::ostream& [operator]<< (std::ostream&, Stack<U> const&);
};
```

Neither using `T` again nor skipping the template parameter declaration would work (either the inner `T` hides the outer `T` or we declare a nontemplate function in namespace scope).

2. We can forward declare the output operator for a `Stack<T>` to be a template, which, however, means that we first have to forward declare `Stack<T>`:

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

In any case, you can still use this class for elements that don't have operator<< defined. Only calling operator<< for this stack results in an error:

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

To specialize a class template, you have to declare the class with a leading `template<>` and a specification of the types for which the class template is specialized. The types are used as a template argument and must be specified directly following the name of the class:

```cpp
template<>
class Stack<std::string> {
   ...
};
```

For these specializations, any definition of a member function must be defined as an "ordinary" member function, with each occurrence of `T` being replaced by the specialized type:

```cpp
void Stack<std::string>::push (std::string const& elem)
{
   elems.push_back(elem);        // append copy of passed [elem]\
}
```

Here is a complete example of a specialization of `Stack<>` for type `std::string`:

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

Another difference is to use a deque instead of a vector to manage the elements inside the stack. Although this has no particular benefit here, it does demonstrate that the implementation of a specialization might look very different from the implementation of the primary template.

### 2.6 Partial Specialization

Class templates can be partially specialized. You can provide special implementations for particular circumstances, but some template parameters must still be defined by the user. For example, we can define a special implementation of class `Stack<>` for pointers:

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

Note again that the specialization might provide a (slightly) different interface. Here, for example, `pop()` returns the stored pointer, so that a user of the class template can call `delete` for the removed value, when it was created with `new`:

```cpp
Stack<int*> ptrStack;        // stack of pointers (special implementation)
\
ptrStack.push([new int]);
std::cout << \*ptrStack.top() << '\n';\
delete ptrStack.pop();
```

##### Partial Specialization with Multiple Parameters

Class templates might also specialize the relationship between multiple template parameters. For example, for the following class template:

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

```cpp
MyClass< int, int> m;             // ERROR: matches [MyClass<T,T>]\
                                 //        and [MyClass<T,int>]\
MyClass<int*,int*> m;         // ERROR: matches [MyClass<T,T>]\
                              //         and [MyClass<T1\*,T2\*>]
```

To resolve the second ambiguity, you could provide an additional partial specialization for pointers of the same type:

```cpp
template<typename T>
class MyClass<T*,T*> {
   ...
};
```

For details of partial specialization, see Section [[16.4]] on page [[347]].

### 2.7 Default Class Template Arguments

As for function templates, you can define default values for class template parameters. For example, in class `Stack<>` you can define the container that is used to manage the elements as a second template parameter, using `std::vector<>` as the default value:

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

```cpp
template<typename T, typename Cont>
void Stack<T,Cont>::push (T const& elem)
{
   elems.push_back(elem);        // append copy of passed [elem]\
}
```

You can use this stack the same way it was used before. Thus, if you pass a first and only argument as an element type, a vector is used to manage the elements of this type:

```cpp
template<typename T, typename Cont = std::vector<T>>
class Stack {
   private:\
      Cont elems;        // elements
    ...
};
```

In addition, you could specify the container for the elements when you declare a Stack object in your program:

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

### 2.8 Type Aliases

You can make using a class template more convenient by defining a new name for the whole type.

##### Typedefs and Alias Declarations

To simply define a new name for a complete type, there are two ways to do it:

1. By using the keyword `typedef`:

```cpp
typedef Stack\
typedef Stack[<int]> IntStack;     *[// typedef]*\
void foo (IntStack const& s);    *[//]* [s *is stack ofint*[s]*\
IntStack istack[10];             *[//]* [istack] *[is array of 10 stacks of]* [int*[s]
```

We call this declaration a _typedef_[3] and the resulting name is called a _typedef-name_.

2. By using the keyword `using` (since C++11):

```cpp
using IntStack = Stack [<int]>;        // alias declaration
void foo (IntStack const& s);        // [s] is stack of ints
IntStack istack[10];                 // [istack] is array of 10 stacks of ints
```

Introduced by [DosReisMarcusAliasTemplates], this is called an _alias declaration_.

Note that in both cases we define a new name for an existing type rather than a new type. Thus, after the typedef

```cpp
typedef Stack [<int]> IntStack;
```

or

```cpp
using IntStack = Stack [<int]>;
```

`IntStack` and `Stack<int>` are two interchangeable notations for the same type.

As a common term for both alternatives to define a new name for an existing type, we use the term _type alias declaration_. The new name is a _type alias_ then.

Because it is more readable (always having the defined type name on the left side of the `=`, for the remainder of this book, we prefer the alias declaration syntax when declaring an type alias.

##### Alias Templates

Unlike a `typedef`, an alias declaration can be templated to provide a convenient name for a family of types. This is also available since C++11 and is called an _alias template_.[4]

The following alias template `DequeStack`, parameterized over the element type `T`, expands to a `Stack` that stores its elements in a `std::deque`:

```cpp
template<typename T>
using DequeStack = Stack<T, std::deque<T>>;
```

Thus, both class templates and alias templates can be used as a parameterized type. But again, an alias template simply gives a new name to an existing type, which can still be used. Both `DequeStack<int>` and `Stack<int, std::deque<int>>` represent the same type.

Note again that, in general, templates can only be declared and defined in global/namespace scope or inside class declarations.

##### Alias Templates for Member Types

Alias templates are especially helpful to define shortcuts for types that are members of class templates. After

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

For example, in all previous code examples, you can use a copy constructor without specifying the template arguments:

```cpp
Stack< int> intStack1;                 // stack of strings
Stack< int> intStack2 = intStack1;     // OK in all versions
Stack intStack3 = intStack1;           // OK since C++17
```

By providing constructors that pass some initial arguments, you can support deduction of the element type of a stack. For example, we could provide a stack that can be initialized by a single element:

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

Note the following:

• Due to the definition of the `int` constructor, you have to request the default constructors to be available with its default behavior, because the default constructor is available only if no other constructor is defined:

`Stack() = default;`

• The argument `elem` is passed to `elems` with braces around to initialize the vector `elems` with an initializer list with `elem` as the only argument:

`: elems()`

There is no constructor for a vector that is able to take a single parameter as initial element directly.[6]

Note that, unlike for function templates, class template arguments may not be deduced only partially (by explicitly specifying only _some_ of the template arguments). See Section [[15.12]] on page [[314]] for details.

##### Class Template Arguments Deduction with String Literals

In principle, you can even initialize the stack with a string literal:

```cpp
Stack stringStack = "bottom"; // `Stack<char const[7]>` deduced since C++17
```

**But** this causes a lot of trouble: In general, when passing arguments of a template type `T` by reference, the parameter doesn't _decay_, which is the term for the mechanism to convert a raw array type to the corresponding raw pointer type. This means that we really initialize a

`Stack< char const[7]>`

and use type `char const[7]` wherever `T` is used. For example, we may not push a string of different size, because it has a different type. For a detailed discussion see Section [[7.4]] on page [[115]].

However, when passing arguments of a template type `T` by value, the parameter _decays_, which is the term for the mechanism to convert a raw array type to the corresponding raw pointer type. That is, the call parameter `T` of the constructor is deduced to be `char const*` so that the whole class is deduced to be a `Stack<char const*>`.

For this reason, it might be worthwhile to declare the constructor so that the argument is passed by value:

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

You can define specific _deduction guides_ to provide additional or fix existing class template argument deductions. For example, you can define that whenever a string literal or C string is passed, the stack is instantiated for `std::string`:

```cpp
`Stack( char const*) -> Stack<std::string>;`
```

This guide has to appear in the same scope (namespace) as the class definition. Usually, it follows the class definition. We call the type following the `->` the _guided type_ of the deduction guide.

Now, the declaration with

```cpp
Stack stringStack[};        // OK: `Stack<std::string>` deduced since C++17
```

deduces the stack to be a `Stack<std::string>`. However, the following still doesn't work:

```cpp
Stack stringStack = "bottom"; // `Stack<std::string>` deduced, but still not valid
```

We deduce `std::string` so that we instantiate a `Stack<std::string>`:

class Stack {
   private:
      std::vector[std::string](std::string) elems;        // elements
   public:
      Stack (std::string const& elem)        // initialize stack with one element
      : elems() {
    }
    ...
};

However, by language rules, you can't copy initialize (initialize using `=`) an object by passing a string literal to a constructor expecting a `std::string`. So you have to initialize the stack as follows:

```cpp
Stack stringStack[}; // `Stack<std::string>` deduced and valid
```

Note that, if in doubt, class template argument deduction copies. After declaring `stringStack` as `Stack<std::string>` the following initializations declare the same type (thus, calling the copy constructor) instead of initializing a stack by elements that are string stacks:

```cpp
`Stack stack2;`        // `Stack<std::string>` deduced
`Stack stack3(stringStack);`        // `Stack<std::string>` deduced
`Stack stack4 = ;`     // `Stack<std::string>` deduced
```

See Section [[15.12]] on page [[313]] for more details about class template argument deduction.

### 2.10 Templatized Aggregates

Aggregate classes (classes/structs with no user-provided, explicit, or inherited constructors, no private or protected nonstatic data members, no virtual functions, and no virtual, private, or protected base classes) can also be templates. For example:

```cpp
template<typename T>
struct ValueWithComment {
    T value;\
    std::string comment;\
};
```

defines an aggregate parameterized for the type of the value `val` it holds. You can declare objects as for any other class template and still use it as aggregate:

```cpp
ValueWithComment< int> vc;\
vc.value = 42;\
vc.comment = "initial value";
```

Since C++17, you can even define deduction guides for aggregate class templates:

```cpp
`ValueWithComment( char const*, char const*)`\
  -> ValueWithComment<std::string>;\
ValueWithComment vc2 = [, "initial value"};
```

Without the deduction guide, the initialization would not be possible, because `ValueWithComment` has no constructor to perform the deduction against.

The standard library class `std::array<>` is also an aggregate, parameterized for both the element type and the size. The C++17 standard library also defines a deduction guide for it, which we discuss in Section [[4.4.4]] on page [[64]].

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

### 3.1 Nontype Class Template Parameters

In contrast to the sample implementations of a stack in previous chapters, you can also implement a stack by using a fixed-size array for the elements. An advantage of this method is that the memory management overhead, whether performed by you or by a standard container, is avoided. However, determining the best size for such a stack can be challenging. The smaller the size you specify, the more likely it is that the stack will get full. The larger the size you specify, the more likely it is that memory will be reserved unnecessarily. A good solution is to let the user of the stack specify the size of the array as the maximum size needed for stack elements.

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

Again, default arguments for the template parameters can be specified:

```cpp
template<typename T = int, std::size_t Maxsize = 100>
class Stack {
  ...
};
```

However, from a perspective of good design, this may not be appropriate in this example. Default arguments should be intuitively correct. But neither type `int` nor a maximum size of 100 seems intuitive for a general stack type. Thus, it is better when the programmer has to specify both values explicitly so that these two attributes are always documented during a declaration.

### 3.2 Nontype Function Template Parameters

You can also define nontype parameters for function templates. For example, the following function template defines a group of functions for which a certain value can be added:

```cpp
`basics/addvalue.hpp`

template<int Val, typename T>
T addValue (T x)
{
  return x + Val;\
}
```

These kinds of functions can be useful if functions or operations are used as parameters. For example, if you use the C++ standard library you can pass an instantiation of this function template to add a value to each element of a collection:

```cpp
std::transform (source.begin(), source.end(),  //start and end of source
                dest.begin(),                  //start of destination
                addValue<5,int>);              // operation
```

The last argument instantiates the function template `addValue<>()` to add 5 to a passed `int` value. The resulting function is called for each element in the source collection `source`, while it is translated into the destination collection `dest`.

Note that you have to specify the argument `int` for the template parameter `T` of `addValue<>()`. Deduction only works for immediate calls and `std::transform()` need a complete type to deduce the type of its fourth parameter. There is no support to substitute/deduce only some template parameters and the see, what could fit, and deduce the remaining parameters.

Again, you can also specify that a template parameter is deduced from the previous parameter. For example, to derive the return type from the passed nontype:

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

Floating-point numbers and class-type objects are not allowed as nontype template parameters:

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

See Section [[12.3.3]] on page [[194]] for a detailed discussion and Section [[17.2]] on page [[354]] for a discussion of possible future changes in this area.

#### Avoiding Invalid Expressions

Arguments for nontype template parameters might be any compile-time expressions. For example:

```cpp
template<int I, [bool] B>
class C;\
...
C<[sizeof](int) + 4, [sizeof][(int])==4> c;
```

However, note that if `operator>` is used in the expression, you have to put the whole expression into parentheses so that the nested `>` ends the argument list:

```cpp
C<42, [sizeof][(int]) > 4> c;    // ERROR: first [>] ends the template argument list
C<42, [(sizeof][(int]) > 4)> c;  // OK
```

### 3.4 Template Parameter Type **auto**

Since C++17, you can define a nontype template parameter to generically accept any type that is allowed for a nontype parameter. Using this feature, we can provide an even more generic stack class with fixed size:

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

Internally you can use both the value:

```cpp
std::array<T,Maxsize> elems;     // elements
```

and its type:

```cpp
    using size_type = decltype(Maxsize);
```

which is then, for example, used as return type of the `size()` member function:

```cpp
size_type size() const \
    return numElems;\
}
```

Since C++14, you could also just use `auto` here as return type to let the compiler find out the return type:

```cpp
auto size() const \
    return numElems;\
}
```

With this class declaration the type of the number of elements is defined by the type used for the number of elements, when using a stack:

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

```cpp
if (!std::is_same[<decltype](size1), decltype(size2)>::value) {
  std::cout << "size types differ" << '\n';\
}
```

Thus, the output will be:

size types differ

Since C++17, for traits returning values, you can also use the suffix `_v` and skip `::value` (see Section [[5.6]] on page [[83]] for details):

```cpp
if (!std::is_same_v[<decltype](size1), decltype(size2)>) {
  std::cout << "size types differ" << '\n';\
}
```

Note that other constraints on the type of nontype template parameters remain in effect. Especially, the restrictions about possible types for nontype template arguments discussed in Section [[3.3]] on page [[49]] still apply. For example:

```cpp
`Stack<int,3.14> sd;`        // ERROR: Floating-point nontype argument
```

And, because you can also pass strings as constant arrays (since C++17 even static locally declared; see Section [[3.3]] on page [[49]]), the following is possible:

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

### 4.1 Variadic Templates

Template parameters can be defined to accept an unbounded number of template arguments. Templates with this ability are called _variadic templates_.

#### 4.1.1 Variadic Templates by Example

For example, you can use the following code to call `print()` for a variable number of arguments of different types:

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

```cpp
void print (T firstArg, Types... args)
```

using different "`Types`" specified by a _template parameter pack_:

```cpp
template<typename T, typename... Types>
```

To end the recursion, the nontemplate overload of `print()` is provided, which is issued when the parameter pack is empty.

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

After printing `7.5` as `firstArg`, it calls `print()` again for the remaining arguments, which then expands to:

```cpp
print<[char const]\*, std::string> [(\"hello", s);
```

with

- `firstArg` having the value `"hello"` so that type `T` is a `char const*` here and
- `args` being a variadic template argument having the value of type `std::string`.

After printing `"hello"` as `firstArg`, it calls `print()` again for the remaining arguments, which then expands to:

```cpp
print<std::string> (s);
```

with

- `firstArg` having the value `"world"` so that type `T` is a `std::string` now and
- `args` being an empty variadic template argument having no value.

Thus, after printing `"world"` as `firstArg`, we calls `print()` with no arguments, which results in calling the nontemplate overload of `print()` doing nothing.

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

#### 4.1.3 Operator **sizeof...**

C++11 also introduced a new form of the `sizeof` operator for variadic templates: sizeof.... It expands to the number of elements a parameter pack contains. Thus,

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

This might lead us to think we can skip the function for the end of the recursion by not calling it in case there are no more arguments:

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

However, note that since C++17, a compile-time `if` is available, which achieves what was expected here with a slightly different syntax. This will be discussed in Section [[8.5]] on page [[134]].

### 4.2 Fold Expressions

Since C++17, there is a feature to compute the result of using a binary operator over _all_ the arguments of a parameter pack (with an optional initial value).

For example, the following function returns the sum of all passed arguments:

```cpp
template<typename... T>
auto foldSum (T... s) {
  return (... + s);   // [((s1 + s2) + s3)] [...]\
}
```

If the parameter pack is empty, the expression is usually ill-formed (with the exception that for operator `&&` the value is `true`, for operator `||` the value is `false`, and for the comma operator the value for an empty parameter pack is `void()`).

Table [[4.1]] lists the possible fold expressions.

**Fold Expression** **Evaluation**

---

`( …` _op pack_ `)` `(((` _pack1 op pack2_ `)` _op pack3_ `)` ... _op packN_ `)`
`(` _pack op_ `… )` `(` _pack1 op_ `(` ... `(` _packN-1 op packN_ `)))`
`(` _init op_ `…` _op pack_ `)` `(((` _init op pack1_ `)` _op pack2_ `)` ... _op packN_ `)`
`(` _pack op_ `…` _op init_ `)` `(` _pack1 op_ `(` ... `(` _packN op init_ `)))`

_Table 4.1. Fold Expressions (since C++17)_

You can use almost all binary operators for fold expressions (see Section [[12.4.6]] on page [[208]] for details). For example, you can use a fold expression to traverse a path in a binary tree using operator `->*`:

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

With such a fold expression using an initializer, we might think about simplifying the variadic template to print all arguments, introduced above:

```cpp
template<typename... Types>
void print (Types const&... args)
{
  (std::cout << ... << args) << '\n';\
}
```

However, note that in this case no whitespace separates all the elements from the parameter pack. To do that, you need an additional class template, which ensures that any output of any argument is extended by a space:

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

See Section [[12.4.6]] on page [[207]] for details about fold expressions.

### 4.3 Application of Variadic Templates

Variadic templates play an important role when implementing generic libraries, such as the C++ standard library.

One typical application is the forwarding of a variadic number of arguments of arbitrary type. For example, we use this feature when:

• Passing arguments to the constructor of a new heap object owned by a shared pointer:

```cpp
// create shared pointer to `complex<float>` initialized by `4.2` and `7.7: auto sp = std::make_shared<std::complex<float>>(4.2, 7.7);`
```

• Passing arguments to a thread, which is started by the library:

```cpp
std::thread t (foo, 42, "hello");        //call [foo(42,\"hello\")] in a separate thread
```

• Passing arguments to the constructor of a new element pushed into a vector:

```cpp
std::vector<Customer> v;\
...
v.emplace("Tim", "Jovi", 1962);        //insert a [Customer] initialized by three arguments
```

Usually, the arguments are "_perfectly forwarded_" with move semantics (see Section [[6.1]] on page [[91]]), so that the corresponding declarations are, for example:

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

```cpp
// [args] are copies with decayed types:
template<typename... Args> void foo (Args... args);
// [args] are nondecayed references to passed objects:
template<typename... Args> void bar (Args const&... args);
```

### 4.4 Variadic Class Templates and Variadic Expressions

Besides the examples above, parameter packs can appear in additional places, including, for example, expressions, class templates, using declarations, and even deduction guides. Section [[12.4.2]] on page [[202]] has a complete list.

#### 4.4.1 Variadic Expressions

You can do more than just forward all the parameters. You can compute with them, which means to compute with all the parameters in a parameter pack.

For example, the following function doubles each parameter of the parameter pack `args` and passes each doubled argument to `print()`:

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

```cpp
print(7.5 + 7.5,\
      std::string("hello") + std::string[(\"hello"),\
      std::complex<[float]>(4,2) + std::complex[<float]>(4,2);
```

If you just want to add 1 to each argument, note that the dots from the ellipsis may not directly follow a numeric literal:

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

```cpp
template<typename T1, typename... TN>
[constexpr bool] isHomogeneous (T1, TN...)
{
  return (std::is_same<T1,TN>::value && ...);  // since C++17
}
```

This is an application of fold expressions (see Section [[4.2]] on page [[58]]): For

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

#### 4.4.2 Variadic Indices

As another example, the following function uses a variadic list of indices to access the corresponding element of the passed first argument:

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

```cpp
template<typename... Elements>
class Tuple;\

Tuple<int, std::string, [char]> t;    // [t] can hold integer, string, *and* character
```

This will be discussed in [Chapter [25]].

Another example is to be able to specify the possible types objects can have:

```cpp
template<typename... Types>
class Variant;

`Variant<int, std::string, char> v;`        // `v` can hold integer, string, [or] character
```

This will be discussed in [Chapter [26]].

You can also define a class that _as a type_ represents a list of indices:

```cpp
// type for arbitrary number of indices:
template<std::size_t...>
struct Indices {
};
```

This can be used to define a function that calls `print()` for the elements of a `std::array` or `std::tuple` using the compile-time access with `get<>()` for the given indices:

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

#### 4.4.4 Variadic Deduction Guides

Even deduction guides (see Section [[2.9]] on page [[42]]) can be variadic. For example, the C++ standard library defines the following deduction guide for `std::array` s:

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

```cpp
std::array<int, 3> a;
```

The `std::enable_if<>` expression for the first `array` parameter is a fold expression that (as introduced as `isHomogeneous()` in Section [[4.4.1]] on page [[62]]) expands to:

```cpp
is_same_v<T, U1> && is_same_v<T, U2> && is_same_v<T, U3> ...
```

If the result is not `true` (i.e., not all the element types are the same), the deduction guide is discarded and the overall deduction fails. This way, the standard library ensures that all elements must have the same type for the deduction guide to succeed.

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

```cpp
template<typename... Bases>
struct Overloader : Bases...
{
    using Bases:[:operator]()...;  // OK since C++17
};
```

we can define a class derived from a variadic number of base classes that brings in the `operator()` declarations from each of those base classes. With

```cpp
using CustomerOP = Overloader<CustomerHash,CustomerEq>;
```

we use this feature to derive `CustomerOP` from `CustomerHash` and `CustomerEq` and enable both implementations of `operator()` in the derived class.

See Section [[26.4]] on page [[611]] for another application of this technique.

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

### 5.1 Keyword **typename**

The keyword `typename` was introduced during the standardization of C++ to clarify that an identifier inside a template is a type. Consider the following example:

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

Without `typename`, `SubType` would be assumed to be a nontype member (e.g., a static data member or an enumerator constant). As a result, the expression

```cpp
`T::SubType* ptr`
```

would be a multiplication of the static `SubType` member of class `T` with `ptr`, which is not an error, because for some instantiations of `MyClass<>` this could be valid code.

In general, `typename` has to be used whenever a name that depends on a template parameter is a type. This is discussed in detail in Section [[13.3.2]] on page [[228]].

One application of `typename` is the declaration to iterators of standard containers in generic code:

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

```cpp
class *stlcontainer* {
 public:
  using iterator = ...;        // iterator for read/write access
  using const_iterator = ...;  // iterator for read access
 ...
};
```

Thus, to access type `const_iterator` of template type `T`, you have to qualify it with a leading `typename`:

```cpp
typename T::const_iterator pos;
```

See Section [[13.3.2]] on page [[228]] for more details about the need for `typename` until C++17. Note that C++20 will probably remove the need for `typename` in many common cases (see Section [[17.1]] on page [[354]] for details).

### 5.2 Zero Initialization

For fundamental types such as `int`, `double`, or pointer types, there is no default constructor that initializes them with a useful default value. Instead, any noninitialized local variable has an undefined value:

```cpp
void foo()
{
  int x;       // [x] has undefined value
  int\* ptr;    // [ptr] points to anywhere (instead of nowhere)
}
```

Now if you write templates and want to have variables of a template type initialized by a default value, you have the problem that a simple definition doesn't do this for built-in types:

```cpp
template<typename T>
void foo()
{
  T x;*        [//]* [x *has undefined value if [T *is built-in type
}
```

For this reason, it is possible to call explicitly a default constructor for built-in types that initializes them with zero (or `false` for `bool` or `nullptr` for pointers). As a consequence, you can ensure proper initialization even for built-in types by writing the following:

```cpp
template<typename T>
void foo()
{
  T x;      *[//]* [x *is zero (or [false*) if* T *is a built-in type
}
```

This way of initialization is called _value initialization_, which means to either call a provided constructor or _zero initialize_ an object. This even works if the constructor is `explicit`.

Before C++11, the syntax to ensure proper initialization was

```cpp
`T x = T();`      // `x` is zero (or `false`) if `T` is a built-in type
```

Prior to C++17, this mechanism (which is still supported) only worked if the constructor selected for the copy-initialization is not `explicit`. In C++17, mandatory copy elision avoids that limitation and either syntax can work, but the braced initialized notation can use an initializer-list constructor[1] if no default constructor is available.

To ensure that a member of a class template, for which the type is parameterized, gets initialized, you can define a default constructor that uses a braced initializer to initialize the member:

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

We discuss this issue in Section [[13.4.2]] on page [[237]] in detail. For the moment, as a rule of thumb, we recommend that you always qualify any symbol that is declared in a base that is somehow dependent on a template parameter with `this->` or `Base<T>::`.

### 5.4 Templates for Raw Arrays and String Literals

When passing raw arrays or string literals to templates, some care has to be taken. First, if the template parameters are declared as references, the arguments don't decay. That is, a passed argument of `"hello"` has type `char const[6]`. This can become a problem if raw arrays or string arguments of different length are passed because the types differ. Only when passing the argument by value, the types decay, so that string literals are converted to type `char const*`. This is discussed in detail in [Chapter [7]].

Note that you can also provide templates that specifically deal with raw arrays or string literals. For example:

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

If you only want to provide a function template for string literals (and other `char` arrays), you can do this as follows:

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

```cpp
[extern int] i[];
```

And when this is passed by reference, it becomes a `int(&)[]`, which can also be used as a template parameter.[2]

See Section [[19.3.1]] on page [[401]] for another example using the different array types in generic code.

### 5.5 Member Templates

Class members can also be templates. This is possible for both nested classes and member functions. The application and advantage of this ability can again be demonstrated with the `Stack<>` class template. Normally you can assign stacks to each other only when they have the same type, which implies that the elements have the same type. However, you can't assign a stack with elements of any other type, even if there is an implicit type conversion for the element types defined:

```cpp
Stack<int> intStack1, intStack2;  // stacks for ints
Stack<[float]> floatStack;          // stack for [float]s
...
intStack1 = intStack2;            // OK: stacks have same type
floatStack = intStack1;           // ERROR: stacks have different types
```

The default assignment operator requires that both sides of the assignment operator have the same type, which is not the case if stacks have different element types.

By defining an assignment operator as a template, however, you can enable the assignment of stacks with elements for which an appropriate type conversion is defined. To do this you have to declare `Stack<>` as follows:

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
2. The stack now uses a `std::deque<>` as an internal container for the elements. Again, this is a consequence of the implementation of the new assignment operator.

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

```cpp
template<typename T>
 template<typename T2>
...
```

Inside the member function, you may expect simply to access all necessary data for the assigned stack `op2`. However, this stack has a different type (if you instantiate a class template for two different argument types, you get two different class types), so you are restricted to using the public interface. It follows that the only way to access the elements is by calling `top()`. However, each element has to become a top element, then. Thus, a copy of `op2` must first be made, so that the elements are taken from that copy by calling `pop()`. Because `top()` returns the last element pushed onto the stack, we might prefer to use a container that supports the insertion of elements at the other end of the collection. For this reason, we use a `std::deque<>`, which provides `push_front()` to put an element on the other side of the collection.

To get access to all the members of `op2` you can declare that all other stack instances are friends:

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

```cpp
template<typename> [friend class] Stack;
```

Now, the following implementation of the template assignment operator is possible:

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

```cpp
Stack<int> intStack;      // stack for ints
Stack<[float]> floatStack;  // stack for [float]s
...
floatStack = intStack;    // OK: stacks have different types,
                          //     but int converts to [float]
```

Of course, this assignment does not change the type of the stack and its elements. After the assignment, the elements of the `floatStack` are still `floats` and therefore `top()` still returns a `float`.

It may appear that this function would disable type checking such that you could assign a stack with elements of any type, but this is not the case. The necessary type checking occurs when the element of the (copy of the) source stack is moved to the destination stack:

```cpp
elems.push_front(tmp.top());
```

If, for example, a stack of strings gets assigned to a stack of `float` s, the compilation of this line results in an error message stating that the string returned by `tmp.top()` cannot be passed as an argument to `elems.push_front()` (the message varies depending on the compiler, but this is the gist of what is meant):

```cpp
Stack<std::string> stringStack;  // stack of [string]s
Stack<[float]> floatStack;         // stack of [float]s
...
floatStack = stringStack;        // ERROR: [std::string] doesn't convert to [float]
```

Again, you could change the implementation to parameterize the internal container type:

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

```cpp
// stack for ints using a vector as an internal container
Stack<int,std::vector<int>> vStack;\
...
vStack.push(42); vStack.push(7);
std::cout << vStack.top() << '\n';
```

Because the assignment operator template isn't necessary, no error message of a missing member function `push_front()` occurs and the program is fine.

For the complete implementation of the last example, see all the files with a name that starts with _stack7_ in the subdirectory _basics_.

##### Specialization of Member Function Templates

Member function templates can also be partially or fully specialized. For example, for the following class:

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

```cpp
`basics/boolstringgetbool.hpp`

// full specialization for [BoolString::getValue<>()] for [bool]\
template<>
[inline bool] BoolString::get[<bool]>() const {
  return value == "true" \|\| value == "1" \|\| value == "on";\
}
```

Note that you don't need and also can't declare the specializations; you only define them. Because it is a full specialization and it is in a header file you have to declare it with `inline` to avoid errors if the definition is included by different translation units.

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

This effect can be good and bad:

• It can happen that a template constructor or assignment operator is a better match than the predefined copy/move constructor or assignment operator, although a template version is provided for initialization of other types only. See Section [[6.2]] on page [[95]] for details.
• It is not easy to "templify" a copy/move constructor, for example, to be able to constrain its existence. See Section [[6.4]] on page [[102]] for details.

#### 5.5.1 The **.template** Construct

Sometimes, it is necessary to explicitly qualify template arguments when calling a member template. In that case, you have to use the `template` keyword to ensure that a `<` is the beginning of the template argument list. Consider the following example using the standard `bitset` type:

```cpp
template<[unsigned long] N>
void printBitset (std::bitset<N> const& bs) {
  std::cout << bs[.template] to_string[<char], std::char_traits[<char]>,\
                                     std::allocator<[char]>>();
}
```

For the bitset `bs` we call the member function template `to_string()`, while explicitly specifying the string type details. Without that extra use of `.template`, the compiler does not know that the less-than token (`<`) that follows is not really less-than but the beginning of a template argument list. Note that this is a problem only if the construct before the period depends on a template parameter. In our example, the parameter `bs` depends on the template parameter `N`.

The `.template` notation (and similar notations such as `->template` and `::template`) should be used only inside templates and only if they follow something that depends on a template parameter. See Section [[13.3.3]] on page [[230]] for details.

#### 5.5.2 Generic Lambdas and Member Templates

Note that generic lambdas, introduced with C++14, are shortcuts for member templates. A simple lambda computing the "sum" of two arguments of arbitrary types:

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

For example, you can use the following code to define the value of _ˇ_ while still not defining the type of the value:

```cpp
template<typename T>
[constexpr] T pi;
```

Note that, as for all templates, this declaration may not occur inside functions or block scope.

To use a variable template, you have to specify its type. For example, the following code uses two different variables of the scope where `pi<>` is declared:

```cpp
std::cout << pi[<double]> << '\n';\
std::cout << pi[<float]> << '\n';
```

You can also declare variable templates that are used in different translation units:

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

```cpp
std::cout << pi << '\n';        //ERROR
```

Variable templates can also be parameterized by nontype parameters, which also may be used to parameterize the initializer. For example:

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

##### Variable Templates for Data Members

A useful application of variable templates is to define variables that represent members of class templates. For example, if a class template is defined as follows:

```cpp
template<typename T>
class MyClass {
  public:
    [static constexpr int] max = 1000;\
};
```

which allows you to define different values for different specializations of `MyClass<>`, then you can define

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

To use a different internal container for stacks, the application programmer has to specify the element type twice. Thus, to specify the type of the internal container, you have to pass the type of the container _and_ the type of its elements again:

```cpp
`Stack<int, std::vector<int>> vStack;`  // integer stack that uses a vector
```

Using template template parameters allows you to declare the `Stack` class template by specifying the type of the container without respecifying the type of its elements:

```cpp
`Stack<int, std::vector> vStack;`        // integer stack that uses a vector
```

To do this, you must specify the second template parameter as a template template parameter. In principle, this looks as follows:[5]

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

```cpp
template<typename Elem> class Cont
```

The default value has changed from `std::deque<T>` to `std::deque`. This parameter has to be a class template, which is instantiated for the type that is passed as the first template parameter:

```cpp
`Cont<T> elems;`
```

This use of the first template parameter for the instantiation of the second template parameter is particular to this example. In general, you can instantiate a template template parameter with any type inside a class template.

As usual, instead of `typename` you could use the keyword `class` for template parameters. Before C++11, `Cont` could only be substituted by the name of a class template.

```cpp
template<typename T,\
         template<class Elem> class Cont = std::deque>
class Stack \
  ...
};
```

Since C++11, we can also substitute `Cont` with the name of an alias template, but it wasn't until C++17 that a corresponding change was made to permit the use of the keyword `typename` instead of `class` to declare a template template parameter:

```cpp
template<typename T,\
         template<typename Elem> typename Cont = std::deque>
class Stack \
  ...
};
```

Those two variants mean exactly the same thing: Using `class` instead of `typename` does not prevent us from specifying an alias template as the argument corresponding to the `Cont` parameter.

Because the template parameter of the template template parameter is not used, it is customary to omit its name (unless it provides useful documentation):

```cpp
template<typename T,\
         template<typename> class Cont = std::deque>
class Stack {
  ...
};
```

Member functions must be modified accordingly. Thus, you have to specify the second template parameter as the template template parameter. The same applies to the implementation of the member function. The `push()` member function, for example, is implemented as follows:

```cpp
template<typename T, template[<typename]> class Cont>
void Stack<T,Cont>::push (T const& elem)
{
    elems.push_back(elem);    // append copy of passed [elem]\
}
```

Note that while template template parameters are placeholders for class or alias templates, there is no corresponding placeholder for function or variable templates.

##### Template Template Argument Matching

If you try to use the new version of `Stack`, you may get an error message saying that the default value `std::deque` is not compatible with the template template parameter `Cont`. The problem is that prior to C++17 a template template argument had to be a template with parameters that _exactly_ match the parameters of the template template parameter it substitutes, with some exceptions related to variadic template parameters (see Section [[12.3.4]] on page [[197]]). Default template arguments of template template arguments were not considered, so that a match couldn't be achieved by leaving out arguments that have default values (in C++17, default arguments _are_ considered).

The pre-C++17 problem in this example is that the `std::deque` template of the standard library has more than one parameter: The second parameter (which describes an _allocator_) has a default value, but prior to C++17 this was not considered when matching `std::deque` to the `Cont` parameter.

There is a workaround, however. We can rewrite the class declaration so that the `Cont` parameter expects containers with two template parameters:

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

```cpp
template<typename, template[<typename], typename[>class]>
[friend class] Stack;
```

Still, not _all_ standard container templates can be used for `Cont` parameter. For example, `std::array` will not work because it includes a nontype template parameter for the array length that has no match in our template template parameter declaration.

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

Move semantics has a significant influence on the design of templates, and special rules were introduced to support move semantics in generic code. This chapter introduces these features.

### 6.1 Perfect Forwarding

Suppose you want to write generic code that forwards the basic property of passed arguments:

- Modifyable objects should be forwarded so that they still can be modified.
- Constant objects should be forwarded as read-only objects.
- Movable objects (objects we can "steal" from because they are about to expire) should be forwarded as movable objects.

To achieve this functionality without templates, we have to program all three cases. For example, to forward a call of `f()` to a corresponding function `g()`:

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

If we want to combine all three cases in generic code, we have a problem:

```cpp
template<typename T>
void f (T val) {
  g(T);
}
```

works for the first two cases, but not for the (third) case where movable objects are passed.

C++11 for this reason introduces special rules for _perfect forwarding_ parameters. The idiomatic code pattern to achieve this is as follows:

```cpp
template<typename T>
void f (T&& val) {
  g(std::forward<T>(val));  // perfect forward [val] to [g()]\
}
```

Note that `std::move()` has no template parameter and "triggers" move semantics for the passed argument, while `std::forward<>()` "forwards" potential move semantic depending on a passed template argument.

Don't assume that `T&&` for a template parameter `T` behaves as `X&&` for a specific type `X`. Different rules apply! However, syntactically they look identical:

• `X&&` for a specific type `X` declares a parameter to be an rvalue reference. It can only be bound to a movable object (a prvalue, such as a temporary object, and an xvalue, such as an object passed with `std::move()`; see [Appendix [B]] for details). It is always mutable and you can always "steal" its value.[2]

• `T&&` for a template parameter `T` declares a _forwarding reference_ (also called _universal reference_).[3] It can be bound to a mutable, immutable (i.e., `const`), or movable object. Inside the function definition, the parameter may be mutable, immutable, or refer to a value you can "steal" the internals from.

Note that `T` must really be the name of a template parameter. Depending on a template parameter is not sufficient. For a template parameter `T`, a declaration such as `typename T::iterator&&` is just an rvalue reference, not a forwarding reference.

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

### 6.2 Special Member Function Templates

Member function templates can also be used as special member functions, including as a constructor, which, however, might lead to surprising behavior.

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

• We provide a version for string object the caller still needs, for which `name` is initialized by a copy of the passed argument:

```cpp
Person(std::string const& n) : name(n) {
    std::cout << "copying string-CONSTR for '" << name << "'\\n";\
}
```

• We provide a version for movable string object, for which we call `std::move()` to "steal" the value from:

```cpp
Person(std::string&& n) : name(std::move(n)) {
   std::cout << "moving string-CONSTR for '" << name << "'\\n";\
}
```

As expected, the first is called for passed string objects that are in use (lvalues), while the latter is called for movable objects (rvalues):

```cpp
std::string s = "sname";\
Person p1(s);              // init with string object `=>` calls copying string-CONSTR
Person p2[(\"tmp");          // init with string literal `=>` calls moving string-CONSTR
```

Besides these constructors, the example has specific implementations for the copy and move constructor to see when a `Person` as a whole is copied/moved:

```cpp
Person p3(p1);             // copy Person [=>] calls COPY-CONSTR
Person p4(std::move(p1));  // move Person [=>] calls MOVE-CONSTR
```

Now let's replace the two string constructors with one generic constructor perfect forwarding the passed argument to the member `name`:

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

```cpp
Person (Person& p)
```

However, that is only a partial solution because for objects of a derived class, the member template is still a better match. What you really want is to disable the member template for the case that the passed argument is a `Person` or an expression that can be converted to a `Person`. This can be done by using `std::enable_if<>`, which is introduced in the next section.

### 6.3 Disable Templates with **enable_if<>**

Since C++11, the C++ standard library provides a helper template `std::enable_if<>` to ignore function templates under certain compile-time conditions.

For example, if a function template `foo<>()` is defined as follows:

```cpp
template<typename T>
typename std::enable_if<[(sizeof](T) > 4)>::type\
foo() {
}
```

this definition of `foo<>()` is ignored if `sizeof(T) > 4` yields `false`.[4] If `sizeof(T) > 4` yields `true`, the function template instance expands to

```cpp
void foo() {
}
```

That is, `std::enable_if<>` is a type trait that evaluates a given compile-time expression passed as its (first) template argument and behaves as follows:

• If the expression yields `true`, its type member `type` yields a type:

-- The type is `void` if no second template argument is passed.
-- Otherwise, the type is the second template argument type.

• If the expression yields `false`, the member `type` is not defined. Due to a template feature called SFINAE (substitution failure is not an error), which is introduced later (see Section [[8.4]] on page [[129]]), this has the effect that the function template with the `enable_if` expression is ignored.

As for all type traits yielding a type since C++14, there is a corresponding alias template `std::enable_if_t<>`, which allows you to skip `typename` and `::type` (see Section [[2.8]] on page [[40]] for details). Thus, since C++14 you can write

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

```cpp
MyType foo();
```

Note that having the `enable_if` expression in the middle of a declaration is pretty clumsy. For this reason, the common way to use `std::enable_if<>` is to use an additional function template argument with a default value:

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

### 6.4 Using **enable_if<>**

We can use `enable_if<>` to solve our problem with the constructor template introduced in Section [[6.2]] on page [[95]].

The problem we have to solve is to disable the declaration of the template constructor

```cpp
template<typename STR>
Person(STR&& n);
```

if the passed argument `STR` has the right type (i.e., is a `std::string` or a type convertible to `std::string`).

For this, we use another standard type trait, `std::is_convertible<` _FROM_ `,` _TO_ `>`. With C++17, the corresponding declaration looks as follows:

```cpp
template<typename STR,\
         typename = std::enable_if_t<\
                      std::is_convertible_v<STR, std::string>>>
Person(STR&& n);
```

If type `STR` is convertible to type `std::string`, the whole declaration expands to

```cpp
template<typename STR,\
         typename = [void]>
Person(STR&& n);
```

If type `STR` is not convertible to type `std::string`, the whole function template is ignored.[6]

Again, we can define our own name for the constraint by using an alias template:

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

```cpp
template<typename T>
using EnableIfString = std::enable_if_t<\
                         std::is_convertible<T, std::string>::value>;
```

And in C++11, we have to declare the special member template as follows, because as written the `_t` version is not defined for type traits that yield a type:

```cpp
template<typename T>
using EnableIfString\
  = typename std::enable_if<std::is_convertible<T, std::string>::value\
                           >::type;
```

But that's all hidden now in the definition of `EnableIfString<>`.

Note also that there is an alternative to using `std::is_convertible<>` because it requires that the types are implicitly convertible. By using `std::is_constructible<>`, we also allow explicit conversions to be used for the initialization. However, the order of the arguments is the opposite is this case:

```cpp
template<typename T>
using EnableIfString = std::enable_if_t<\
                         std::is_constructible_v<std::string, T>>;
```

See Section [[D.3.2]] on page [[719]] for details about `std::is_constructible<>` and Section [[D.3.3]] on page [[727]] for details about `std::is_convertible<>`. See Section [[D.6]] on page [[734]] for details and examples to apply `enable_if<>` on variadic templates.

##### Disabling Special Member Functions

Note that normally we can't use `enable_if<>` to disable the predefined copy/move constructors and/or assignment operators. The reason is that member function templates never count as special member functions and are ignored when, for example, a copy constructor is needed. Thus, with this declaration:

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

```cpp
C x;\
C y;  // still uses the predefined copy constructor (not the member template)
```

(There is really no way to use the member template because there is no way to specify or deduce its template parameter T.)

Deleting the predefined copy constructor is no solution, because then the trial to copy a `C` results in an error.

There is a tricky solution, though:[7] We can declare a copy constructor for `const volatile` arguments and mark it "deleted" (i.e., define it with `= delete`). Doing so prevents another copy constructor from being implicitly declared. With that in place, we can define a constructor template that will be preferred over the (deleted) copy constructor for nonvolatile types:

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

In principle, we just need a language feature that allows us to formulate requirements or constraints for a function in a way that causes the function to be ignored if the requirements/constraints are not met.

This is an application of the long-awaited language feature _concepts_, which allows us to formulate requirements/conditions for templates with its own simple syntax. Unfortunately, although long discussed, concepts still did not become part of the C++17 standard. Some compilers provide experimental support for such a feature, however, and concepts will likely become part of the next standard after C++17.

With concepts, as their use is proposed, we simply have to write the following:

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

```cpp
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
```
