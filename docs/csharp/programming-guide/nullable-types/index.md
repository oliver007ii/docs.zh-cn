---
title: "可以为 null 的类型（C# 编程指南）| Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- nullable types [C#]
- C# language, nullable types
- types [C#], nullable
ms.assetid: e473cb01-28ca-42be-9cea-f717055d72c6
caps.latest.revision: 44
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 75726b9864abc0c9b556085e5215c6692d80fb12
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="nullable-types-c-programming-guide"></a>可以为 null 的类型（C# 编程指南）
可以为 null 的类型是 <xref:System.Nullable%601?displayProperty=fullName> 结构的实例。 可以为 null 的类型可以表示基础值类型正常范围内的值，再加上一个 `null` 值。 例如，`Nullable<Int32>` 读作“可以为 null 的 Int32”，可以将 -2147483648 到 2147483647 之间的任意值赋值给它，也可以将 `null` 赋值给它。 可以将 [true](../../../csharp/language-reference/keywords/true.md)、[false](../../../csharp/language-reference/keywords/false.md) 或 [null](../../../csharp/language-reference/keywords/null.md) 赋值给 `Nullable<bool>`。 处理数据库和其他包含不可赋值的元素的数据类型时，能够将 `null` 赋值给数值类型和布尔类型会特别有用。 例如，数据库中的布尔字段可以存储值 `true` 或 `false`，也可以处于未定义状态。  
  
 [!code-cs[csProgGuideTypes#3](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/index_1.cs)]  
  
 此示例将显示以下输出：  
  
 `num = Null`  
  
 `Nullable object must have a value.`  
  
 有关更多示例，请参阅[使用可以为 null 的类型](../../../csharp/programming-guide/nullable-types/using-nullable-types.md)  
  
## <a name="nullable-types-overview"></a>可以为 null 的类型概述  
 可以为 null 的类型具有以下特征：  
  
-   可以为 null 的类型表示可以向其赋值 `null` 的值类型变量。 不能根据引用类型创建可以为 null 的类型 （引用类型已支持 `null` 值）。  
  
-   语法 `T?` 是 <xref:System.Nullable%601> 的简写，其中 `T` 是值类型。 这两种形式是可互换的。  
  
-   向可以为 null 的类型赋值的方法与向一般值类型赋值的方法相同，如 `int? x = 10;` 或 `double? d = 4.108`。 也能够向可以为 null 的类型赋值 `null`：`int? x = null.`  
  
-   使用 <xref:System.Nullable%601.GetValueOrDefault%2A?displayProperty=fullName> 方法可返回所赋的值或基础类型的默认值（如果值为 `null` 的话），例如 `int j = x.GetValueOrDefault();`  
  
-   使用 <xref:System.Nullable%601.HasValue%2A> 和 <xref:System.Nullable%601.Value%2A> 只读属性可测试是否有 null 值并检索此值，如以下示例所示：`if(x.HasValue) j = x.Value;`  
  
    -   如果变量包含值，则 `HasValue` 属性返回 `true`；如果值为 `null`，则返回 `false`。  
  
    -   如果已赋值，则 `Value` 属性返回值。 否则，抛出 <xref:System.InvalidOperationException?displayProperty=fullName>。  
  
    -   `HasValue` 的默认值为 `false`。 `Value` 属性没有默认值。  
  
    -   还能将 `==` 和 `!=` 运算符与可以为 null 的类型结合使用，如以下示例所示：`if (x != null) y = x;`  
  
-   将当前值为 `null` 的可以为 null 的类型赋值给不可以为 null 的类型时，能够使用 `??` 运算符赋予默认值，例如 `int? x = null; int y = x ?? -1;`  
  
-   不得嵌套可以为 null 的类型。 无法编译下面的一行代码：`Nullable<Nullable<int>> n;`  
  
## <a name="related-sections"></a>相关章节  
 更多相关信息：  
  
-   [使用可以为 null 的类型](../../../csharp/programming-guide/nullable-types/using-nullable-types.md)  
  
-   [装箱可以为 null 的类型](../../../csharp/programming-guide/nullable-types/boxing-nullable-types.md)  
  
-   [??运算符](../../../csharp/language-reference/operators/null-conditional-operator.md)  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Nullable>   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C#](../../../csharp/csharp.md)   
 [C# 参考](../../../csharp/language-reference/index.md)   
 [“提升”的准确含义是什么？](http://go.microsoft.com/fwlink/?LinkId=112382)

