---
title: "Interoperabilit&#224; (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, interoperabilità"
  - "interoperabilità COM"
  - "interoperabilità"
  - "platform invoke, accesso alle API con C#"
ms.assetid: 238bb95a-e962-4026-bbd5-197055bdb8ee
caps.latest.revision: 31
caps.handback.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Interoperabilit&#224; (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'interoperabilità consente di preservare e sfruttare gli investimenti effettuati nel codice non gestito.  Il codice eseguito sotto il controllo di Common Language Runtime \(CLR\) è denominato *codice gestito*, mentre quello eseguito all'esterno è definito *codice non gestito*.  Esempi di codice non gestito sono i componenti COM, COM\+, C\+\+, i componenti ActiveX e le API Microsoft Win32.  
  
 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] consente l'interoperabilità con il codice non gestito tramite i servizi platform invoke, lo spazio dei nomi <xref:System.Runtime.InteropServices>, l'interoperabilità C\+\+ e l'interoperabilità COM.  
  
## Argomenti della sezione  
 [Cenni preliminari sull'interoperabilità](../../../csharp/programming-guide/interop/interoperability-overview.md)  
 Vengono descritti i metodi per l'interazione tra codice gestito e non gestito.  
  
 [Procedura: accedere agli oggetti di interoperabilità di Office usando le funzionalità di Visual C\#](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md)  
 Descrive le funzionalità introdotte in Visual C\# 2010 per facilitare la programmazione di Office.  
  
 [Procedura: utilizzare proprietà indicizzate nella programmazione dell'interoperabilità COM](../../../csharp/programming-guide/interop/how-to-use-indexed-properties-in-com-interop-rogramming.md)  
 Descrive come utilizzare le proprietà indicizzate per accedere alle proprietà COM aventi parametri.  
  
 [Procedura: utilizzare platform invoke per riprodurre un file audio](../../../csharp/programming-guide/interop/how-to-use-platform-invoke-to-play-a-wave-file.md)  
 Viene descritto come utilizzare i servizi platform invoke per riprodurre un file audio con estensione wav nel sistema operativo Windows.  
  
 [Procedura dettagliata: programmazione di Office](../../../csharp/programming-guide/interop/walkthrough-office-programming.md)  
 Viene illustrato come creare una cartella di lavoro di Excel o un documento di Word contenente un collegamento alla cartella di lavoro.  
  
 [Esempio di classe COM](../../../csharp/programming-guide/interop/example-com-class.md)  
 Viene illustrato come esporre una classe C\# come oggetto COM.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A?displayProperty=fullName>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Interoperating with Unmanaged Code](../Topic/Interoperating%20with%20Unmanaged%20Code.md)   
 [Procedura dettagliata: programmazione di Office](../../../csharp/programming-guide/interop/walkthrough-office-programming.md)