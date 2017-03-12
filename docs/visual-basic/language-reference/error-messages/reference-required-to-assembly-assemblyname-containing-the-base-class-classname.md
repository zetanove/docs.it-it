---
title: "Necessario riferimento all&#39;assembly &quot;&lt;nomeassembly&gt;&quot; contenente la classe base &quot;&lt;nomeclasse&gt;&quot; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30007"
  - "vbc30007"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30007"
ms.assetid: 5f34cf47-6c6e-4954-bd8e-d6b020b75fb7
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Necessario riferimento all&#39;assembly &quot;&lt;nomeassembly&gt;&quot; contenente la classe base &quot;&lt;nomeclasse&gt;&quot;
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Necessario riferimento all'assembly "\<nomeassembly\>" contenente la classe base "\<nomeclasse\>". Aggiungerne uno al progetto.  
  
 La classe è definita in una libreria a collegamento dinamico \(DLL\) o in un assembly a cui non si fa direttamente riferimento nel progetto. Il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] richiede un riferimento per evitare ambiguità nel caso in cui la classe venga definita in più DLL o assembly.  
  
 **ID errore:** BC30007  
  
### Per correggere l'errore  
  
-   Includere il nome della DLL o dell'assembly senza riferimento nei riferimenti del progetto.  
  
## Vedere anche  
 [NIB Procedura: Aggiungere o rimuovere riferimenti utilizzando la finestra di dialogo Aggiungi riferimento](http://msdn.microsoft.com/it-it/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)   
 [Gestione dei riferimenti in un progetto](/visual-studio/ide/managing-references-in-a-project)   
 [Risoluzione dei problemi relativi ai riferimenti interrotti](/visual-studio/ide/troubleshooting-broken-references)