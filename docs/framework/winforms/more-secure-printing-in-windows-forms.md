---
title: "More Secure Printing in Windows Forms | Microsoft Docs"
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
  - "Windows Forms, printing"
  - "PrintingPermission class, Windows Forms security"
  - "printing [Windows Forms], security"
  - "security [Windows Forms], printing"
ms.assetid: 48fd36ac-872f-4de0-902a-e52969cd4367
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# More Secure Printing in Windows Forms
Le applicazioni Windows Form includono spesso funzionalità di stampa.  In [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] viene utilizzata la classe <xref:System.Drawing.Printing.PrintingPermission> per controllare l'accesso alle funzionalità di stampa e il valore di enumerazione <xref:System.Drawing.Printing.PrintingPermissionLevel> associato per indicare il livello di accesso.  Per impostazione predefinita, la stampa è attivata nelle aree Intranet locale e Internet. Tuttavia, il livello di accesso è limitato in entrambe le aree.  Il fatto che l'applicazione possa o meno stampare oppure debba richiedere l'intervento dell'utente dipende dal valore di autorizzazione concesso all'applicazione.  Per impostazione predefinita, all'area Intranet locale viene concesso il diritto di accesso <xref:System.Drawing.Printing.PrintingPermissionLevel> e all'area Internet il diritto di accesso <xref:System.Drawing.Printing.PrintingPermissionLevel>.  
  
 Nella tabella seguente vengono illustrate le funzionalità disponibili a ciascun livello di autorizzazione di stampa.  
  
|PrintingPermissionLevel|Descrizione|  
|-----------------------------|-----------------|  
|<xref:System.Drawing.Printing.PrintingPermissionLevel>|Accesso completo a tutte le stampanti installate.|  
|<xref:System.Drawing.Printing.PrintingPermissionLevel>|Stampa a livello di codice dalla stampante predefinita e stampa protetta mediante una finestra di dialogo di stampa limitata.  <xref:System.Drawing.Printing.PrintingPermissionLevel> è un subset di <xref:System.Drawing.Printing.PrintingPermissionLevel>.|  
|<xref:System.Drawing.Printing.PrintingPermissionLevel>|Consente la stampa solo da una finestra di dialogo maggiormente ridotta.  <xref:System.Drawing.Printing.PrintingPermissionLevel> è un subset di <xref:System.Drawing.Printing.PrintingPermissionLevel>.|  
|<xref:System.Drawing.Printing.PrintingPermissionLevel>|Impedisce l'accesso alle stampanti.  <xref:System.Drawing.Printing.PrintingPermissionLevel> è un subset di <xref:System.Drawing.Printing.PrintingPermissionLevel>.|  
  
## Vedere anche  
 [More Secure File and Data Access in Windows Forms](../../../docs/framework/winforms/more-secure-file-and-data-access-in-windows-forms.md)   
 [Additional Security Considerations in Windows Forms](../../../docs/framework/winforms/additional-security-considerations-in-windows-forms.md)   
 [Security in Windows Forms Overview](../../../docs/framework/winforms/security-in-windows-forms-overview.md)   
 [Windows Forms Security](../../../docs/framework/winforms/windows-forms-security.md)