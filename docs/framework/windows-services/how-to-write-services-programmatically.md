---
title: "How to: Write Services Programmatically | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "services, creating"
  - "Windows Service applications, creating"
ms.assetid: 3abbb2ec-78d2-41e6-b9f9-6662d4e2cdc7
caps.latest.revision: 21
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 21
---
# How to: Write Services Programmatically
Se si sceglie di non utilizzare il modello di progetto dei servizi Windows, è possibile scrivere i propri servizi impostando l'ereditarietà e altri elementi di infrastruttura.  Quando si crea un servizio a livello di codice, è necessario attenersi a diversi passaggi gestiti automaticamente nel modello:  
  
-   Impostare la classe di servizio in modo che erediti dalla classe <xref:System.ServiceProcess.ServiceBase>.  
  
-   Creare un metodo `Main` per il progetto di servizio che definisca i servizi da eseguire e chiami il metodo <xref:System.ServiceProcess.ServiceBase.Run%2A>.  
  
-   Eseguire l'override delle routine <xref:System.ServiceProcess.ServiceBase.OnStart%2A> e <xref:System.ServiceProcess.ServiceBase.OnStop%2A> e scrivere il codice che devono eseguire.  
  
### Per scrivere un servizio a livello di codice  
  
1.  Creare un progetto vuoto, quindi creare un riferimento agli spazi dei nomi necessari seguendo le istruzioni riportate di seguito.  
  
    1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo **Riferimenti** e scegliere **Aggiungi riferimento**.  
  
    2.  Nella scheda **.NET Framework** scorrere su **System.dll** e fare clic su **Seleziona**.  
  
    3.  Scorrere su **System.ServiceProcess.dll** e fare clic su **Seleziona**.  
  
    4.  Fare clic su **OK**.  
  
2.  Aggiungere una classe, quindi configurarla in modo che erediti dalla classe <xref:System.ServiceProcess.ServiceBase>:  
  
     [!code-csharp[VbRadconService#7](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#7)]
     [!code-vb[VbRadconService#7](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#7)]  
  
3.  Per configurare la classe di servizio, aggiungere il codice seguente:  
  
     [!code-csharp[VbRadconService#8](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#8)]
     [!code-vb[VbRadconService#8](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#8)]  
  
4.  Creare un metodo `Main` per la classe, quindi utilizzarlo per definire il servizio che sarà contenuto nella classe. Il nome della classe è `userService1`:  
  
     [!code-csharp[VbRadconService#9](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#9)]
     [!code-vb[VbRadconService#9](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#9)]  
  
5.  Eseguire l'override del metodo <xref:System.ServiceProcess.ServiceBase.OnStart%2A>, quindi scrivere il codice da eseguire all'avvio del servizio.  
  
     [!code-csharp[VbRadconService#10](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#10)]
     [!code-vb[VbRadconService#10](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#10)]  
  
6.  Eseguire l'override degli altri metodi per i quali si desidera definire un comportamento personalizzato e scrivere il codice appropriato per ciascuno di essi.  
  
7.  Aggiunta dei programmi di installazione necessari per l'applicazione di servizio.  Per ulteriori informazioni, vedere [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md).  
  
8.  Compilare il progetto. Per effettuare questa operazione, scegliere **Compila soluzione** dal menu **Compila**.  
  
    > [!NOTE]
    >  Non è possibile eseguire un progetto di servizio premendo F5.  
  
9. Creare un progetto di installazione e le funzionalità personalizzate necessarie per l'installazione del servizio.  Per un esempio, vedere [Walkthrough: Creating a Windows Service Application in the Component Designer](../../../docs/framework/windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md).  
  
10. Installare il servizio.  Per ulteriori informazioni, vedere [How to: Install and Uninstall Services](../../../docs/framework/windows-services/how-to-install-and-uninstall-services.md).  
  
## Vedere anche  
 [Introduction to Windows Service Applications](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)   
 [How to: Create Windows Services](../../../docs/framework/windows-services/how-to-create-windows-services.md)   
 [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)   
 [How to: Log Information About Services](../../../docs/framework/windows-services/how-to-log-information-about-services.md)   
 [Walkthrough: Creating a Windows Service Application in the Component Designer](../../../docs/framework/windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md)