---
title: "如何：在 Visual Basic 中写入二进制文件 | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- files, binary access
- WriteAllBytes method
- binary files, writing in Visual Basic
ms.assetid: 59fae125-de5b-4c96-883c-209f4a55112c
caps.latest.revision: 16
author: dotnet-bot
ms.author: dotnetcontent
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
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 0d86e39b7150b4ae8fc4de0498b0b786c5669bb4
ms.contentlocale: zh-cn
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-write-to-binary-files-in-visual-basic"></a>如何：在 Visual Basic 中写入二进制文件
可使用 <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllBytes%2A> 方法将数据写入二进制文件。 如果 `append` 参数为 `True`，会将数据追加到文件中；否则将覆盖文件中的数据。  
  
 如果指定的路径（不包括文件名）无效，则将引发 <xref:System.IO.DirectoryNotFoundException> 异常。 如果该路径有效，但文件不存在，则将创建文件。  
  
### <a name="to-write-to-a-binary-file"></a>写入二进制文件  
  
-   使用 `WriteAllBytes` 方法，并提供文件路径和名称以及要写入的字节数。 本示例将数据组 `CustomerData` 追加到名为 `CollectedData.dat` 的文件中。  
  
     [!code-vb[VbVbcnMyFileSystem#27](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-write-to-binary-files_1.vb)]  
  
## <a name="robust-programming"></a>可靠编程  
 以下情况可能会导致异常：  
  
-   路径由于以下原因之一而无效：是零长度字符串；仅包含空白；包含无效字符。 (<xref:System.ArgumentException>)。  
  
-   路径无效，因为路径为 `Nothing` (<xref:System.ArgumentNullException>)。  
  
-   `File` 指向不存在的路径（<xref:System.IO.FileNotFoundException> 或 <xref:System.IO.DirectoryNotFoundException>）。  
  
-   文件正由另一个进程使用，或者出现 I/O 错误 (<xref:System.IO.IOException>)。  
  
-   路径超出了系统定义的最大长度 (<xref:System.IO.PathTooLongException>)。  
  
-   路径中的某个文件或目录名称包含冒号 (:) 或格式无效 (<xref:System.NotSupportedException>)。  
  
-   用户缺少必要的权限来查看路径 (<xref:System.Security.SecurityException>)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllBytes%2A>   
 [如何：向文件写入文本](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-write-text-to-files.md)
