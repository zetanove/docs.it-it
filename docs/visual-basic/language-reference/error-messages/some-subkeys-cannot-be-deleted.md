---
title: "Some subkeys cannot be deleted | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
ms.assetid: 14562137-af43-4972-84c1-a380a90f7d6c
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Some subkeys cannot be deleted
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È stato compiuto il tentativo di eliminare una chiave del Registro di sistema, ma l'operazione ha avuto esito negativo in quanto è impossibile eliminare alcune sottochiavi.  La situazione è in genere causata dalla mancanza di autorizzazioni.  
  
### Per correggere l'errore  
  
-   Assicurarsi di disporre delle autorizzazioni sufficienti per eliminare le sottochiavi.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy?displayProperty=fullName>   
 <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%2A>   
 <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%2A>   
 <xref:System.Security.Permissions.RegistryPermission>