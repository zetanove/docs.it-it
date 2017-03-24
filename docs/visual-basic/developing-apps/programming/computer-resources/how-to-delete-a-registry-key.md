---
title: "How to: Delete a Registry Key in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.DeleteSetting"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "GetSetting function"
  - "registry, deleting values"
  - "GetAllSettings function"
  - "registry keys, deleting"
  - "registry, deleting keys"
  - "examples [Visual Basic], registry"
ms.assetid: ab9aca0e-42b0-4ff7-8ff9-845a4bfdf9f2
caps.latest.revision: 28
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 28
---
# How to: Delete a Registry Key in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Per eliminare chiavi del Registro di sistema, è possibile utilizzare i metodi <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%28System.String%29> e <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%28System.String%2CSystem.Boolean%29>.  
  
## Procedura  
  
#### Per eliminare una chiave del Registro di sistema  
  
-   Utilizzare il metodo `DeleteSubKey` per eliminare una chiave del Registro di sistema.  Nell'esempio che segue viene eliminata la chiave Software\/TestApp nell'hive CurrentUser.  È possibile impostare la stringa appropriata nel codice o far sì che l'operazione si basi sulle informazioni fornite dall'utente.  
  
     [!code-vb[VbResourceTasks#19](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-delete-a-registry-key_1.vb)]  
  
## Programmazione efficiente  
 Se la coppia chiave\/valore non esiste, il metodo `DeleteSubKey` restituirà una stringa vuota.  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il nome della chiave è `Nothing` \(<xref:System.ArgumentNullException>\).  
  
-   L'utente non dispone delle autorizzazioni necessarie per l'eliminazione delle chiavi del Registro di sistema \(<xref:System.Security.SecurityException>\).  
  
-   Il nome della chiave supera il limite di 255 caratteri \(<xref:System.ArgumentException>\).  
  
-   La chiave del Registro di sistema è di sola lettura \(<xref:System.UnauthorizedAccessException>\).  
  
## Sicurezza di .NET Framework  
 Se non vengono concesse autorizzazioni sufficienti in fase di esecuzione \(<xref:System.Security.Permissions.RegistryPermission>\) o se l'utente non dispone dell'accesso corretto \(determinato dagli ACL\) per la creazione o la scrittura nelle impostazioni, le chiamate al Registro di sistema avranno esito negativo.  Un'applicazione locale che dispone dell'autorizzazione di sicurezza per l'accesso di codice potrebbe ad esempio non disporre dell'autorizzazione del sistema operativo.  
  
## Vedere anche  
 <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%2A>   
 <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%2A>   
 <xref:Microsoft.Win32.RegistryKey>   
 [Security and the Registry](../../../../visual-basic/developing-apps/programming/computer-resources/security-and-the-registry.md)   
 [Reading from and Writing to the Registry](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)