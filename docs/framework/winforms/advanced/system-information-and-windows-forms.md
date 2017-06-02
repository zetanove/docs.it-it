---
title: "System Information and Windows Forms | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "domain names, retrieving"
  - "SystemInformation class [Windows Forms]"
  - "user names, retrieving"
  - "system information [Windows Forms]"
ms.assetid: 30cf43a3-8cb2-4ff3-862b-6c34576616a8
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# System Information and Windows Forms
Talvolta, per specificare il codice appropriato, è necessario raccogliere informazioni sul computer in cui viene eseguita l'applicazione.  Se ad esempio si dispone di una funzione che può essere utilizzata solo durante la connessione a un particolare dominio di rete, può essere opportuno poter determinare il dominio, oppure disabilitare la funzione qualora il dominio designato non fosse disponibile.  
  
 Le applicazioni Windows Form consentono di utilizzare la classe <xref:System.Windows.Forms.SystemInformation> per definire numerose operazioni per il computer, in fase di esecuzione.  Nel seguente esempio viene illustrato l'utilizzo della classe <xref:System.Windows.Forms.SystemInformation> per il recupero di <xref:System.Windows.Forms.SystemInformation.UserName%2A> e <xref:System.Windows.Forms.SystemInformation.UserDomainName%2A>:  
  
```vb  
Dim User As String = Windows.Forms.SystemInformation.UserName  
Dim Domain As String = Windows.Forms.SystemInformation.UserDomainName  
  
MessageBox.Show("Good morning " & User & ". You are connected to " _  
& Domain)  
  
```  
  
```csharp  
string User = SystemInformation.UserName;  
string Domain = SystemInformation.UserDomainName;  
  
MessageBox.Show("Good morning " + User + ". You are connected to " _  
+ Domain)  
```  
  
 Tutti i membri della classe <xref:System.Windows.Forms.SystemInformation> sono di sola lettura, pertanto non è possibile modificare le impostazioni utente.  La classe dispone di oltre 100 membri che restituiscono qualsiasi tipo di informazione, dal numero di monitor collegati al computer \(<xref:System.Windows.Forms.SystemInformation.MonitorCount%2A>\) alla spaziatura delle icone in Windows Explorer \(<xref:System.Windows.Forms.SystemInformation.IconHorizontalSpacing%2A> e <xref:System.Windows.Forms.SystemInformation.IconVerticalSpacing%2A>\).  
  
 I membri più utili della classe <xref:System.Windows.Forms.SystemInformation> includono <xref:System.Windows.Forms.SystemInformation.ComputerName%2A>, <xref:System.Windows.Forms.SystemInformation.DbcsEnabled%2A>, <xref:System.Windows.Forms.SystemInformation.PowerStatus%2A> e <xref:System.Windows.Forms.SystemInformation.TerminalServerSession%2A>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.SystemInformation>   
 [Power Management in Windows Forms](../../../../docs/framework/winforms/advanced/power-management-in-windows-forms.md)