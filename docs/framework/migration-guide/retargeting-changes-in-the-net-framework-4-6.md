---
title: ".NET Framework 4.6 中的重定目标更改 | Microsoft 文档"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- retargeting changes, .NET Framework
- retargeting changes, .NET Framework 4.6
- application compatibility
ms.assetid: fa849255-f90f-4bf1-b0ff-b173c12110d7
caps.latest.revision: 15
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 19ad80233a79a4fdef89550696c1c3d33e14b355
ms.contentlocale: zh-cn
ms.lasthandoff: 05/22/2017

---
# <a name="retargeting-changes-in-the-net-framework-46"></a>.NET Framework 4.6 中的重定目标更改
在极少数情况下，重定目标更改可能影响那些编译为面向 [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] 的应用。 除非另行指定，否则这些更改不会影响面向以前版本的 .NET Framework 但在 [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] 下运行的二进制文件。  
  
 [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] 包括以下方面的重定目标更改：  
  
-   [核心](#Core)  
  
-   [ASP.NET 2.0](#ASP)  
  
-   [网络](#Net)  
  
-   [Windows Communications Foundation (WCF)](#WCF)  
  
-   [Windows 窗体](#WinForms)  
  
-   [Windows Presentation Foundation (WPF)](#WPF)  
  
-   [XML](#XML)  
  
<a name="Core"></a>   
## <a name="core"></a>核心  
  
|功能|更改|影响|范围|  
|-------------|------------|------------|-----------|  
|<xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName>、<xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> 以及 <xref:System.Threading.Tasks.Task> 和 <xref:System.Threading.Tasks.Task%601> 的基于任务的异步操作|对于面向 [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] 及更高版本的应用，<xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> 和 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> 存储在线程的 <xref:System.Threading.ExecutionContext> 中，该线程在异步操作之间流动。|对 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> 和 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> 属性的更改会反映在随后启动的异步任务中。 有关详细信息，请参阅[缓解：区域性和异步操作](../../../docs/framework/migration-guide/mitigation-culture-and-asynchronous-operations.md)。|次要|  
  
<a name="ASP"></a>   
## <a name="aspnet"></a>ASP.NET  
  
|功能|更改|影响|范围|  
|-------------|------------|------------|-----------|  
|具有 <xref:System.Web.UI.HtmlTextWriterTag?displayProperty=fullName> 的 `tagKey` 值的 <xref:System.Web.UI.HtmlTextWriter.RenderBeginTag%28System.Web.UI.HtmlTextWriterTag%29?displayProperty=fullName>|为符合 HTML 标准，<xref:System.Web.UI.HtmlTextWriter.RenderBeginTag%28System.Web.UI.HtmlTextWriterTag%29?displayProperty=fullName> 方法现在 HTML 响应中将 <xref:System.Web.UI.HtmlTextWriterTag?displayProperty=fullName> 呈现为非结束标记。|BR 标记现在会生成一个换行符。 以前，它会生成 2 个换行符。<br /><br /> 依赖于 `<BR>` 标记来生成 2 个换行符的应用，可以通过向具有 <xref:System.Web.UI.HtmlTextWriterTag?displayProperty=fullName> 自变量的 <xref:System.Web.UI.HtmlTextWriter.RenderBeginTag%28System.Web.UI.HtmlTextWriterTag%29?displayProperty=fullName> 方法添加额外调用来还原以前的行为。|次要|  
  
<a name="Net"></a>   
## <a name="networking"></a>网络  
  
|功能|更改|影响|范围|  
|-------------|------------|------------|-----------|  
|<xref:System.Net.ServicePointManager?displayProperty=fullName> 和 <xref:System.Net.Security.SslStream?displayProperty=fullName>|从面向 .NET Framework 4.6 的应用开始，<xref:System.Net.ServicePointManager?displayProperty=fullName> 和 <xref:System.Net.Security.SslStream?displayProperty=fullName> 类可以使用以下三种协议之一：Tls1.0、Tls1.1 或 Tls 1.2。<br /><br /> 面向以前版本的 .NET Framework 的应用即使在 NET Framework 4.6 上运行也不会受到影响。|此更改会影响面向 .NET Framework 4.6 并使用 SSL 与 HTTPS 服务器或与使用以下任何类型的套接字对话的任何应用：<xref:System.Net.Http.HttpClient>、<xref:System.Net.HttpWebRequest><xref:System.Net.FtpWebRequest>、<xref:System.Net.Mail.SmtpClient> 和 <xref:System.Net.Security.SslStream>。  有关详细信息，请参阅[缓解：TLS 协议](../../../docs/framework/migration-guide/mitigation-tls-protocols.md)。|次要|  
  
<a name="WCF"></a>   
## <a name="windows-communications-foundation-wcf"></a>Windows Communication Foundation (WCF)  
  
|功能|更改|影响|范围|  
|-------------|------------|------------|-----------|  
|<xref:System.IdentityModel.Policy.AuthorizationContext.CreateDefaultAuthorizationContext%2A?displayProperty=fullName>|调用具有 `null``authorizationPolicies` 自变量的 <xref:System.IdentityModel.Policy.AuthorizationContext.CreateDefaultAuthorizationContext%28System.Collections.Generic.IList%7BSystem.IdentityModel.Policy.IAuthorizationPolicy%7D%29> 所返回的 <xref:System.IdentityModel.Policy.AuthorizationContext> 实现更改了其在 [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] 中的实现。|在极少数情况下，使用自定义身份验证的 WCF 应用可能会看到行为差异。 如果需要这一旧行为，请参阅[缓解：默认 AuthorizationContext](../../../docs/framework/migration-guide/mitigation-default-authorizationcontext.md)。|次要|  
  
<a name="WinForms"></a>   
## <a name="windows-forms"></a>Windows 窗体  
  
|功能|更改|影响|范围|  
|-------------|------------|------------|-----------|  
|<xref:System.Drawing.Icon.ToBitmap%2A?displayProperty=fullName>|从面向 .NET Framework 4.6 的应用开始，<xref:System.Drawing.Icon.ToBitmap%2A?displayProperty=fullName> 方法成功将带 PNG 帧的图标转换为 <xref:System.Drawing.Bitmap> 对象。<br /><br /> 在面向 .NET Framework 4.5.2 和更早版本的应用中，<xref:System.Drawing.Icon.ToBitmap%2A?displayProperty=fullName> 方法在 <xref:System.Drawing.Icon> 对象具有 PNG 帧时引发 <xref:System.ArgumentOutOfRangeException> 异常。|此更改会影响以下应用：重新编译为面向 .NET Framework 4.6 的应用，以及对在 <xref:System.Drawing.Icon> 对象具有 PNG 帧时引发的 <xref:System.ArgumentOutOfRangeException> 异常提供特殊处理的应用。 如果不需要此行为，配置开关可还原以前的行为。 有关详细信息，请参阅[缓解：图标对象中的 PNG 帧](../../../docs/framework/migration-guide/mitigation-png-frames-in-icon-objects.md)。|次要|  
  
<a name="WPF"></a>   
## <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)  
  
|功能|更改|影响|范围|  
|-------------|------------|------------|-----------|  
|<xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> 和 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>|在面向 .NET Framework 4.6 和 .NET Framework 4.6.1 的应用中，在 <xref:System.Windows.Threading.Dispatcher> 中执行的 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> 或 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> 属性更改，会在调度程序操作结束时丢失。 同样，在调度程序操作外对 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> 或 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> 所做的更改在执行该操作时可能不会反映出来。|对 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> 和 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> 属性的更改可能不会在 WPF UI 回调和 WPF 应用程序中的其他代码之间流动。 有关详细信息，请参阅[缓解：区域性和 WPF 应用中的调度程序操作](../../../docs/framework/migration-guide/mitigation-culture-and-dispatcher-operations-in-wpf-apps.md)。|次要|  
|高 DPI 处舍入的布局|边距舍入的方式以及边框和边框内的背景已更改。|WPF 控件的布局可能稍有变化。 有关详细信息，请参阅[缓解：WPF 布局](../../../docs/framework/migration-guide/mitigation-wpf-layout.md)。|次要|  
  
<a name="XML"></a>   
## <a name="xml"></a>XML  
  
|功能|更改|影响|范围|  
|-------------|------------|------------|-----------|  
|XSD 架构验证|从 .NET Framework 4.6 开始，如果使用复合键且有一个键为空，则 XSD 架构验证将检测是否违反唯一约束。|请参阅[缓解：XML 架构验证](../../../docs/framework/migration-guide/mitigation-xml-schema-validation.md)|次要|  
|<xref:System.Xml.XmlWriter>|对于面向 .NET Framework 4.5.2 或以前的版本的应用程序，使用异常回退处理编写无效的代理项对并不会总是引发异常。<br /><br /> 对于面向 [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] 的应用程序，尝试编写无效的代理项对会引发 <xref:System.ArgumentException> 异常。|重新编译以面向 [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] 的应用与编写无效代理项的应用可能在之前没有引发异常时引发异常。|边缘|
