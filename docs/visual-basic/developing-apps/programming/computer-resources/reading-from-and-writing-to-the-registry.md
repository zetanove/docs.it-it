---
title: "Reading from and Writing to the Registry (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.Computer.Registry object, tasks"
  - "registry, writing to"
  - "registry, reading"
ms.assetid: a13da106-185b-41d7-b23c-416da65e21e4
caps.latest.revision: 21
caps.handback.revision: 21
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Reading from and Writing to the Registry (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questo argomento vengono descritte le attività e gli argomenti concettuali in cui sono associati al Registro di sistema.  
  
 Durante la programmazione in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] è possibile scegliere di accedere al Registro di sistema tramite le funzioni disponibili in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] o le classi Registry di .NET Framework.  Nel Registro di sistema sono memorizzate informazioni provenienti dal sistema operativo, nonché informazioni provenienti dalle applicazioni presenti nel computer.  L'utilizzo del Registro di sistema potrebbe comportare problemi di sicurezza, consentendo accesso non appropriato a risorse di sistema o informazioni protette.  
  
## In questa sezione  
 [How to: Create a Registry Key and Set Its Value](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-create-a-registry-key-and-set-its-value.md)  
 Viene descritto come utilizzare `CreateSubKey` e  `SetValue` metodi di  `My.Computer.Registry` oggetto per creare una chiave del Registro di sistema e per impostarne il valore.  
  
 [How to: Read a Value from a Registry Key](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-read-a-value-from-a-registry-key.md)  
 Viene descritto come utilizzare `GetValue` metodo di  `My.Computer.Registry` oggetto per leggere un valore da una chiave del Registro di sistema.  
  
 [How to: Delete a Registry Key](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-delete-a-registry-key.md)  
 Viene descritto come utilizzare `DeleteSubKey` metodo di  `My.Computer.Registry.CurrentUser` proprietà per eliminare una chiave del Registro di sistema.  
  
 [Lettura e scrittura nel Registro di sistema mediante lo spazio dei nomi Microsoft.Win32](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry-using-the-microsoft-win32-namespace.md)  
 Viene descritto come utilizzare `Registry` e  `RegistryKey` classi di  [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] per accedere al Registro di sistema.  
  
 [Security and the Registry](../../../../visual-basic/developing-apps/programming/computer-resources/security-and-the-registry.md)  
 Vengono illustrati i problemi di sicurezza relativi al Registro di sistema.  
  
## Sezioni correlate  
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>  
 Vengono elencati ed illustrati i membri dell'oggetto `My.Computer.Registry`.  
  
 <xref:Microsoft.Win32.Registry>  
 Viene fornita una descrizione generale della classe `Registry` e vengono forniti collegamenti a singole chiavi e singoli membri.