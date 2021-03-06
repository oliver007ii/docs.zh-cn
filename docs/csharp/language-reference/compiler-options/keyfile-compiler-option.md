---
title: "-keyfile（C# 编译器选项）| Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /keyfile
dev_langs:
- CSharp
helpviewer_keywords:
- /keyfile compiler option [C#]
- -keyfile compiler option [C#]
- keyfile compiler option [C#]
ms.assetid: 0815f9de-ace4-4e98-b4c6-13c55dea40c2
caps.latest.revision: 15
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
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 4f9ccbfe7126aac3214ccf08015353eec0490cd4
ms.contentlocale: zh-cn
ms.lasthandoff: 05/10/2017

---
# <a name="keyfile-c-compiler-options"></a>/keyfile（C# 编译器选项）
指定包含加密密钥的文件名。  
  
## <a name="syntax"></a>语法  
  
```  
/keyfile:file  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|----------|----------------|  
|`file`|含有强名称密钥的文件的名称。|  
  
## <a name="remarks"></a>备注  
 使用此选项时，编译器在程序集清单中插入指定字段的公钥，然后使用私钥对最终的程序集进行签名。 若要生成密钥文件，请在命令行键入 sn-k `file`。  
  
 如果使用 /target:module 进行编译，密钥文件的名称将保存在模块中，并在使用 [/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md) 编译程序集时包含到创建的程序集中。  
  
 也可以使用 [/keycontainer](../../../csharp/language-reference/compiler-options/keycontainer-compiler-option.md) 将加密信息传递给编译器。 如果需要部分签名的程序集，请使用 [/delaysign](../../../csharp/language-reference/compiler-options/delaysign-compiler-option.md)。  
  
 如果在同一编译中同时指定 /keyfile 和 /keycontainer（通过命令行选项或通过自定义特性），则 Al.exe 将首先尝试用密钥容器。 如果成功，则使用密钥容器中的信息对程序集签名。 如果编译器没有找到密钥容器，它将尝试用 /keyfile 指定的文件。 如果成功，则使用密钥文件中的信息对程序集签名，并且将密钥信息安装到密钥容器中（类似于 sn -i），以便在下一次编译中，密钥容器选项将生效。  
  
 请注意，密钥文件可能仅包含公钥。  
  
 有关详细信息，请参阅[创建和使用具有强名称的程序集](https://msdn.microsoft.com/library/xwb8f617)和[延迟为程序集签名](../../../framework/app-domains/delay-sign-assembly.md)。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的“属性”  页。  
  
2.  单击“签名”属性页。  
  
3.  修改“选择强名称密钥文件”属性。  
  
 可通过 <xref:VSLangProj.ProjectProperties.AssemblyOriginatorKeyFile%2A> 以编程方式访问此编译器选项。  
  
## <a name="see-also"></a>另请参阅  
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [NIB 如何：修改项目属性和配置设置](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)
