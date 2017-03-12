---
title: "Error creating assembly manifest: &lt;error message&gt; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30140"
  - "vbc30140"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30140"
ms.assetid: 1beb5aa0-7b79-4c85-946b-5c2d0a41d1d2
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# Error creating assembly manifest: &lt;error message&gt;
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] chiama Assembly Linker \(Al.exe, definito anche Alink\) per generare un assembly con un manifesto.  Il linker ha segnalato un errore nella fase di pre\-emissione della creazione dell'assembly.  
  
 Questo può accadere se si verificano errori con il file di chiave o il contenitore di chiavi specificato.  Per la firma completa di un assembly, è necessario fornire un file di chiave valido contenente informazioni sulle chiavi pubblica e privata.  Per ritardare la firma di un assembly, è necessario selezionare la casella di controllo **Solo firma ritardata** e fornire un file di chiave valido contenente informazioni sulla chiave pubblica.  Quando la firma di un assembly viene ritardata, la chiave privata non è necessaria.  Per altre informazioni, vedere [How to: Sign an Assembly \(Visual Studio\)](http://msdn.microsoft.com/it-it/f468a7d3-234c-4353-924d-8e0ae5896564).  
  
 **ID errore:** BC30140  
  
### Per correggere l'errore  
  
1.  Esaminare il messaggio di errore riportato e vedere l'argomento [Al.exe Tool Errors and Warnings](http://msdn.microsoft.com/it-it/7f125d49-0a03-47a6-9ba9-d61a679a7d4b) per spiegazioni e suggerimenti aggiuntivi sull'errore AL1019.  
  
2.  Se l'errore persiste, raccogliere informazioni sulla situazione contingente e informare il Servizio Supporto Tecnico Clienti Microsoft.  
  
## Vedere anche  
 [How to: Sign an Assembly \(Visual Studio\)](http://msdn.microsoft.com/it-it/f468a7d3-234c-4353-924d-8e0ae5896564)   
 [Pagina Firma, Progettazione progetti](/visual-studio/ide/reference/signing-page-project-designer)   
 [Al.exe \(Assembly Linker\)](../Topic/Al.exe%20\(Assembly%20Linker\).md)   
 [Al.exe Tool Errors and Warnings](http://msdn.microsoft.com/it-it/7f125d49-0a03-47a6-9ba9-d61a679a7d4b)   
 [Comunicazioni con Microsoft](/visual-studio/ide/talk-to-us)