---
title: "如何：在 Visual Basic 中读取二进制文件 | Microsoft Docs"
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
- binary files, reading from
- I/O [Visual Basic], reading from binary files
- ReadAllBytes method, reading from binary files
- My.Computer.FileSystem object, reading from binary files
ms.assetid: d2b1269e-24b6-42e0-9414-ae708db282d8
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
ms.openlocfilehash: 501257c051e0cba4d867acc4d32cdd5d891e950b
ms.contentlocale: zh-cn
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-read-from-binary-files-in-visual-basic"></a>如何：在 Visual Basic 中读取二进制文件
`My.Computer.FileSystem` 对象提供用于读取二进制文件的 `ReadAllBytes` 方法。  
  
### <a name="to-read-from-a-binary-file"></a>读取二进制文件  
  
-   使用 `ReadAllBytes` 方法可将文件的内容作为字节数组返回。 此示例读取文件 `C:/Documents and Settings/selfportrait.jpg`。  
  
     [!code-vb[VbVbcnMyFileSystem#78](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-binary-files_1.vb)]  
  
-   对于大型二进制文件，可以使用 <xref:System.IO.FileStream> 对象的 <xref:System.IO.FileStream.Read%2A> 方法从文件中一次只读取指定数量的内容。 然后，可以限制每次读取操作将文件加载进内存的数量。 以下代码示例将复制文件，并允许调用方指定每次读取操作将文件读入内存的数量。  
  
     [!code-vb[VbVbcnMyFileSystem#91](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-read-from-binary-files_2.vb)]  
  
## <a name="robust-programming"></a>可靠编程  
 以下情况可能会导致异常：  
  
-   路径由于以下原因之一而无效：是零长度字符串；仅包含空白；包含无效字符；是一个设备路径 (<xref:System.ArgumentException>)。  
  
-   路径无效，因为路径为 `Nothing` (<xref:System.ArgumentNullException>)。  
  
-   文件不存在 (<xref:System.IO.FileNotFoundException>)。  
  
-   文件正由另一个进程使用，或者出现 I/O 错误 (<xref:System.IO.IOException>)。  
  
-   路径超出了系统定义的最大长度 (<xref:System.IO.PathTooLongException>)。  
  
-   路径中的某个文件或目录名称包含冒号 (:) 或格式无效 (<xref:System.NotSupportedException>)。  
  
-   内存不足，无法将字符串写入缓冲区 (<xref:System.OutOfMemoryException>)。  
  
-   用户缺少必要的权限来查看路径 (<xref:System.Security.SecurityException>)。  
  
 不要根据文件的名称来判断文件的内容。 例如，文件 Form1.vb 可能不是 Visual Basic 源文件。  
  
 在应用程序中使用输入的数据之前，需验证所有的输入内容。 文件的内容可能不是预期内容，并且用来读取该文件的方法可能失败。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllBytes%2A>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllBytes%2A>   
 [从文件读取](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)   
 [如何：读取具有多种格式的文本文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md)   
 [将数据存储到剪贴板以及从剪贴板读取数据](../../../../visual-basic/developing-apps/programming/computer-resources/storing-data-to-and-reading-from-the-clipboard.md)
