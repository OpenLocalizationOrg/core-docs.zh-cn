---
title: Implicitly typed lambda expressions
description: Implicitly typed lambda expressions
keywords: .NET, .NET Core
author: BillWagner
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: a3851da9-e018-4389-9922-233db7d0f841
translationtype: Human Translation
ms.sourcegitcommit: 2d44b7e04c0fe2ca136ba6dfa9fc3a4368365ec8
ms.openlocfilehash: c43c1bd2ed95da0c3f8fc6061968e97671da43ee

---

# Implicitly typed lambda expressions

I'm not using `var` to declare this expression tree. You can't use an implicitly typed variable declaration to declare a lambda expression.
It creates a circular logic problem for the compiler. The `var` declaration tells the compiler to figure out the type of the variable from the type of expression on the right hand side of the assignment operator. A lambda expression does not have a compile time type, but is convertible to any matching delegate or expression type. When you assign a lambda expression to a variable of a delegate or expression type, you tell the compiler to try and convert the lambda expression into an expression or delegate that matches the signature of the 'assigned to' variable. The compiler must try to make the thing on the right hand side of the assignment match the type on the left hand side of the assignment. 

Both sides of the assignment can't be telling the compiler to look at the object on the other side of the assignment operator and see if my type matches.

You can get even more details on why the C# language specifies that behavior by reading [this article](http://download.microsoft.com/download/5/4/B/54B83DFE-D7AA-4155-9687-B0CF58FF65D7/type-inference.pdf) (PDF Download)





<!--HONumber=Aug16_HO2-->

