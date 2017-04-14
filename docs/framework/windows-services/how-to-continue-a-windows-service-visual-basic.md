---
title: "How to: Continue a Windows Service (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ServiceController.Continue"
helpviewer_keywords: 
  - "Windows Service applications, pausing"
  - "pausing Windows Service applications"
ms.assetid: e5d13760-4c83-4b0d-abef-39852677cd7a
caps.latest.revision: 16
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 16
---
# How to: Continue a Windows Service (Visual Basic)
Nell'esempio riportato di seguito viene utilizzato il componente <xref:System.ServiceProcess.ServiceController> per continuare il servizio di amministrazione di IIS sul computer locale.  
  
## Esempio  
 [!code-vb[VbRadconService#11](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#11)]  
[!code-vb[VbRadconService#13](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#13)]  
  
 Questo esempio di codice è anche disponibile come frammento di codice IntelliSense.  Nella casella di selezione dei frammenti di codice l'esempio è incluso in **Sistema operativo Windows \> Servizi Windows**.  Per ulteriori informazioni, vedere [Frammenti di codice](../Topic/Code%20Snippets.md).  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Riferimento di progetto a System.serviceprocess.dll.  
  
-   Accesso ai membri dello spazio dei nomi <xref:System.ServiceProcess>.  Aggiungere un'istruzione `Imports` se i nomi dei membri all'interno del codice non sono specificati in modo completo.  Per ulteriori informazioni, vedere [Imports Statement \(.NET Namespace and Type\)](../../../ocs/visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md).  
  
## Programmazione efficiente  
 Per impostazione predefinita, la proprietà <xref:System.ServiceProcess.ServiceController.MachineName%2A> della classe <xref:System.ServiceProcess.ServiceController> corrisponde al computer locale.  Per fare riferimento a servizi Windows su un altro computer, impostare la proprietà <xref:System.ServiceProcess.ServiceController.MachineName%2A> sul nome del computer specifico.  
  
 Non è possibile chiamare il metodo <xref:System.ServiceProcess.ServiceController.Continue%2A> su un servizio fino a quando lo stato del controller servizi non è <xref:System.ServiceProcess.ServiceControllerStatus>.  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il servizio non può essere ripreso  \(<xref:System.InvalidOperationException>\)  
  
-   Si è verificato un errore durante l'accesso a un'API di sistema  \(<xref:System.ComponentModel.Win32Exception>\)  
  
## Sicurezza di .NET Framework  
 Il controllo dei servizi sul computer può essere limitato mediante l'enumerazione <xref:System.ServiceProcess.ServiceControllerPermissionAccess> per impostare le autorizzazioni nella classe <xref:System.ServiceProcess.ServiceControllerPermission>.  
  
 È possibile inoltre limitare l'accesso alle informazioni relative ai servizi mediante l'enumerazione <xref:System.Security.Permissions.PermissionState> per impostare le autorizzazioni nella classe <xref:System.Security.Permissions.SecurityPermission>.  
  
## Vedere anche  
 <xref:System.ServiceProcess.ServiceController>   
 <xref:System.ServiceProcess.ServiceControllerStatus>   
 [How to: Pause a Windows Service \(Visual Basic\)](../../../docs/framework/windows-services/how-to-pause-a-windows-service-visual-basic.md)