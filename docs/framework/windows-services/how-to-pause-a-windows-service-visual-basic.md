---
title: "How to: Pause a Windows Service (Visual Basic) | Microsoft Docs"
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
  - "ServiceController.Pause"
helpviewer_keywords: 
  - "Windows Service applications, pausing"
  - "pausing Windows Service applications"
ms.assetid: eddb9409-942b-46b6-a2ce-fbd4c65f2790
caps.latest.revision: 17
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 15
---
# How to: Pause a Windows Service (Visual Basic)
Nell'esempio riportato di seguito viene utilizzato il componente <xref:System.ServiceProcess.ServiceController> per sospendere il servizio di amministrazione di IIS sul computer locale.  
  
## Esempio  
 [!code-vb[VbRadconService#11](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#11)]  
[!code-vb[VbRadconService#12](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#12)]  
  
 Questo esempio di codice è anche disponibile come frammento di codice IntelliSense.  Nella casella di selezione dei frammenti di codice l'esempio è incluso in **Sistema operativo Windows \> Servizi Windows**.  Per ulteriori informazioni, vedere [Frammenti di codice](../Topic/Code%20Snippets.md).  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Riferimento di progetto a System.serviceprocess.dll.  
  
-   Accesso ai membri dello spazio dei nomi <xref:System.ServiceProcess>.  Aggiungere un'istruzione `Imports` se i nomi dei membri all'interno del codice non sono specificati in modo completo.  Per ulteriori informazioni, vedere [Imports Statement \(.NET Namespace and Type\)](../../../ocs/visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md).  
  
## Programmazione efficiente  
 Per impostazione predefinita, la proprietà <xref:System.ServiceProcess.ServiceController.MachineName%2A> della classe <xref:System.ServiceProcess.ServiceController> corrisponde al computer locale.  Per fare riferimento a servizi Windows su un altro computer, impostare la proprietà <xref:System.ServiceProcess.ServiceController.MachineName%2A> sul nome del computer specifico.  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il servizio non può essere sospeso  \([classe InvalidOperationException](frlrfSystemInvalidOperationExceptionClassTopic)\)  
  
-   Si è verificato un errore durante l'accesso a un'API di sistema  \([classe Win32Exception](frlrfSystemComponentModelWin32ExceptionClassTopic)\)  
  
## Sicurezza di .NET Framework  
 È possibile che il controllo dei servizi sul computer sia limitato dall'utilizzo dell'[enumerazione ServiceControllerPermissionAccess](frlrfSystemServiceProcessServiceControllerPermissionAccessClassTopic) per l'impostazione delle autorizzazioni nella [classe ServiceControllerPermission](frlrfSystemServiceProcessServiceControllerPermissionClassTopic).  
  
 È possibile che l'accesso alle informazioni sui servizi sia limitato dall'utilizzo dell'[enumerazione PermissionState](frlrfSystemSecurityPermissionsPermissionStateClassTopic) per l'impostazione delle autorizzazioni nella [classe SecurityPermission](frlrfSystemSecurityPermissionsSecurityPermissionClassTopic).  
  
## Vedere anche  
 <xref:System.ServiceProcess.ServiceController>   
 <xref:System.ServiceProcess.ServiceControllerStatus>   
 <xref:System.ServiceProcess.ServiceController.WaitForStatus%2A>   
 [How to: Continue a Windows Service \(Visual Basic\)](../../../docs/framework/windows-services/how-to-continue-a-windows-service-visual-basic.md)