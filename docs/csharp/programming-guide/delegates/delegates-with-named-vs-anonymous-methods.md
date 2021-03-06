---
title: "带有命名方法的委托与带有匿名方法的委托（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "委托 [C#], 带有命名方法的与带有匿名方法的"
  - "方法 [C#], 委托中"
ms.assetid: 98fa8c61-66b6-4146-986c-3236c4045733
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# 带有命名方法的委托与带有匿名方法的委托（C# 编程指南）
[委托](../../../csharp/language-reference/keywords/delegate.md)可以与命名方法关联。  使用命名方法对委托进行实例化时，该方法将作为参数传递，例如：  
  
 [!code-cs[csProgGuideDelegates#1](../../../csharp/programming-guide/delegates/codesnippet/CSharp/delegates-with-named-vs-anonymous-methods_1.cs)]  
  
 这被称为使用命名的方法。  使用命名方法构造的委托可以封装[静态](../../../csharp/language-reference/keywords/static.md)方法或实例方法。  在早期版本的 C\# 中，命名方法是对委托进行实例化的唯一方式。  但是，在不希望付出创建新方法的系统开销时，C\# 使您可以对委托进行实例化，并立即指定委托在被调用时将处理的代码块。  代码块可以包含 lambda 表达式或匿名方法。  有关更多信息，请参见 [匿名函数](../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md)。  
  
## 备注  
 作为委托参数传递的方法必须与委托声明具有相同的签名。  
  
 委托实例可以封装静态或实例方法。  
  
 尽管委托可以使用 [out](../../../csharp/language-reference/keywords/out.md) 参数，但建议您不要将其用于多路广播事件委托，因为您无法知道哪个委托将被调用。  
  
## 示例 1  
 以下是声明及使用委托的一个简单示例。  注意，委托 `Del` 和关联的方法 `MultiplyNumbers` 具有相同的签名  
  
 [!code-cs[csProgGuideDelegates#2](../../../csharp/programming-guide/delegates/codesnippet/CSharp/delegates-with-named-vs-anonymous-methods_2.cs)]  
  
## 示例 2  
 在下面的示例中，一个委托被同时映射到静态方法和实例方法，并分别返回特定的信息。  
  
 [!code-cs[csProgGuideDelegates#3](../../../csharp/programming-guide/delegates/codesnippet/CSharp/delegates-with-named-vs-anonymous-methods_3.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [委托](../../../csharp/programming-guide/delegates/index.md)   
 [匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)   
 [如何：合并委托（多路广播委托）](../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)   
 [事件](../../../csharp/programming-guide/events/index.md)