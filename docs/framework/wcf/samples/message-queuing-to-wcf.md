---
title: "到 Windows Communication Foundation 的消息队列 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6d718eb0-9f61-4653-8a75-d2dac8fb3520
caps.latest.revision: 34
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 34
---
# 到 Windows Communication Foundation 的消息队列
本示例演示消息队列 \(MSMQ\) 应用程序如何将 MSMQ 消息发送到 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务。此服务是自承载控制台应用程序，通过它可以观察服务接收排队消息。  
  
 服务协定是 `IOrderProcessor`，它定义了适合与队列一起使用的单向服务。MSMQ 消息没有 Action 标头，因此无法将不同的 MSMQ 消息自动映射到操作协定。所以只能有一个操作协定。如果希望为服务定义多个操作协定，则应用程序必须提供有关 MSMQ 消息中的哪个标头（例如，标签或 correlationID）可用于确定要调度的操作协定的信息。这在[自定义多路分解器](../../../../docs/framework/wcf/samples/custom-demux.md)中进行了演示。  
  
 MSMQ 消息不包含有关哪些标头可映射到操作协定的不同参数的信息。该参数属于 <xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601>\(`MsmqMessage<T>`\) 类型，包含基础 MSMQ 消息。<xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601>\(`MsmqMessage<T>`\) 类中的“T”类型代表序列化到 MSMQ 消息正文中的数据。在此示例中，`PurchaseOrder` 类型序列化到 MSMQ 消息正文中。  
  
 下面的示例代码演示订单处理服务的服务协定。  
  
```  
// Define a service contract.  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]  
[ServiceKnownType(typeof(PurchaseOrder))]  
public interface IOrderProcessor  
{  
    [OperationContract(IsOneWay = true, Action = "*")]  
    void SubmitPurchaseOrder(MsmqMessage<PurchaseOrder> msg);  
}  
  
```  
  
 服务是自承载服务。使用 MSMQ 时，必须提前创建所使用的队列。可以手动或通过代码完成此操作。在此示例中，该服务检查队列是否存在并在必要时创建队列。从配置文件中读取队列名称。  
  
```  
public static void Main()  
{  
    // Get the MSMQ queue name from the application settings in   
    // configuration.  
    string queueName = ConfigurationManager.AppSettings["queueName"];  
    // Create the MSMQ queue if necessary.  
    if (!MessageQueue.Exists(queueName))  
        MessageQueue.Create(queueName, true);  
    …  
}  
  
```  
  
 该服务为 `OrderProcessorService` 创建和打开 <xref:System.ServiceModel.ServiceHost>，如下面的示例代码所示。  
  
```  
using (ServiceHost serviceHost = new ServiceHost(typeof(OrderProcessorService)))  
{  
    serviceHost.Open();  
    Console.WriteLine("The service is ready.");  
    Console.WriteLine("Press <ENTER> to terminate service.");  
    Console.ReadLine();  
    serviceHost.Close();  
}  
  
```  
  
 MSMQ 队列名称在配置文件的 appSettings 节中指定，如以下示例配置所示。  
  
> [!NOTE]
>  队列名称为本地计算机使用圆点 \(.\)，并在其路径中使用反斜杠分隔符。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点地址指定 msmq.formatname 方案，并为本地计算机使用 localhost。用于每个 MSMQ 格式名寻址指南的队列地址遵从 msmq.formatname 方案。  
  
```  
<appSettings>  
    <add key="orderQueueName" value=".\private$\Orders" />  
</appSettings>  
  
```  
  
 该客户端应用程序是一个 MSMQ 应用程序，它使用 <xref:System.Messaging.MessageQueue.Send%2A> 方法向队列发送持久的事务性消息，如下面的示例代码所示。  
  
```  
//Connect to the queue.  
MessageQueue orderQueue = new MessageQueue(ConfigurationManager.AppSettings["orderQueueName"]);  
  
// Create the purchase order.  
PurchaseOrder po = new PurchaseOrder();  
po.CustomerId = "somecustomer.com";  
po.PONumber = Guid.NewGuid().ToString();  
  
PurchaseOrderLineItem lineItem1 = new PurchaseOrderLineItem();  
lineItem1.ProductId = "Blue Widget";  
lineItem1.Quantity = 54;  
lineItem1.UnitCost = 29.99F;  
  
PurchaseOrderLineItem lineItem2 = new PurchaseOrderLineItem();  
lineItem2.ProductId = "Red Widget";  
lineItem2.Quantity = 890;  
lineItem2.UnitCost = 45.89F;  
  
po.orderLineItems = new PurchaseOrderLineItem[2];  
po.orderLineItems[0] = lineItem1;  
po.orderLineItems[1] = lineItem2;  
  
// Submit the purchase order.  
Message msg = new Message();  
msg.Body = po;  
//Create a transaction scope.  
using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))  
{  
  
    orderQueue.Send(msg, MessageQueueTransactionType.Automatic);  
    // Complete the transaction.  
    scope.Complete();  
  
}  
Console.WriteLine("Placed the order:{0}", po);  
Console.WriteLine("Press <ENTER> to terminate client.");  
Console.ReadLine();  
  
```  
  
 运行示例时，客户端和服务活动将显示在服务和客户端控制台窗口中。您可以看到服务从客户端接收消息。在每个控制台窗口中按 Enter 可以关闭服务和客户端。请注意：由于正在使用队列，因此不必同时启动和运行客户端和服务。例如，可以先运行客户端，再将其关闭，然后启动服务，这样服务仍然会收到客户端的消息。  
  
### 设置、生成和运行示例  
  
1.  请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  如果先运行服务，则它将检查以确保队列存在。如果队列不存在，则服务将创建一个队列。可以先运行服务以创建队列或通过 MSMQ 队列管理器创建一个队列。执行下面的步骤来在 Windows 2008 中创建队列。  
  
    1.  在 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 中打开服务器管理器。  
  
    2.  展开**“功能”**选项卡。  
  
    3.  右击**“私有消息队列”**，然后选择**“新建”**和**“专用队列”**。  
  
    4.  选中**“事务性”**框。  
  
    5.  输入 `ServiceModelSamplesTransacted` 作为新队列的名称。  
  
3.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
4.  若要用单一计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
### 跨计算机运行示例  
  
1.  将 \\service\\bin\\ 文件夹（在语言特定文件夹内）中的服务程序文件复制到服务计算机上。  
  
2.  将 \\client\\bin\\ 文件夹（在语言特定文件夹内）中的客户端程序文件复制到客户端计算机上。  
  
3.  在 Client.exe.config 文件中，更改 orderQueueName 以指定服务计算机名称，而不是使用“.”。  
  
4.  在服务计算机上，在命令提示符下启动 Service.exe。  
  
5.  在客户端计算机上，在命令提示符下启动 Client.exe。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Binding\MSMQIntegration\MsmqToWcf`  
  
## 请参阅  
 [WCF 中的队列](../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)   
 [如何：与 WCF 终结点和消息队列应用程序交换消息](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)   
 [消息队列（可能为英文网页）](http://go.microsoft.com/fwlink/?LinkId=94968)