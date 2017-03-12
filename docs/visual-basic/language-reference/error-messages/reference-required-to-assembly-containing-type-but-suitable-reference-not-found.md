---
title: "Necessario un riferimento all&#39;assembly &quot;&lt;identit&#224;assembly&gt;&quot; contenente il tipo &quot;&lt;nometipo&gt;&quot;. &#200; tuttavia impossibile trovare un riferimento appropriato a causa di ambiguit&#224; fra i progetti &quot;&lt;nomeprogetto1&gt;&quot; e &quot;&lt;nomeprogetto2&gt;&quot; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30969"
  - "vbc30969"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30969"
ms.assetid: 1b29dbc5-8268-45fe-bfc2-b2070a5c845c
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# Necessario un riferimento all&#39;assembly &quot;&lt;identit&#224;assembly&gt;&quot; contenente il tipo &quot;&lt;nometipo&gt;&quot;. &#200; tuttavia impossibile trovare un riferimento appropriato a causa di ambiguit&#224; fra i progetti &quot;&lt;nomeprogetto1&gt;&quot; e &quot;&lt;nomeprogetto2&gt;&quot;
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In un'espressione viene usato un tipo, ad esempio una classe, una struttura, un'interfaccia, un'enumerazione o un delegato, definito all'esterno del progetto. Tuttavia, sono presenti riferimenti di progetto a più assembly che definiscono quel tipo.  
  
 I progetti citati generano assembly con lo stesso nome. Pertanto, il compilatore non può determinare l'assembly da usare per il tipo a cui si accede.  
  
 Per accedere a un tipo definito in un altro assembly, il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] deve avere un riferimento a quell'assembly. Deve trattarsi di un riferimento unico, non ambiguo, che non generi riferimenti circolari tra i progetti.  
  
 **ID errore:** BC30969  
  
### Per correggere l'errore  
  
1.  Determinare quale progetto produce l'assembly migliore per il progetto a cui fare riferimento. Per questa decisione si potrebbero usare criteri quali la facilità di accesso al file e la frequenza di aggiornamenti.  
  
2.  Nelle proprietà del progetto aggiungere un riferimento al file contenente l'assembly che definisce il tipo in uso.  
  
## Vedere anche  
 [Gestione dei riferimenti in un progetto](/visual-studio/ide/managing-references-in-a-project)   
 [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [NIB Procedura: Aggiungere o rimuovere riferimenti utilizzando la finestra di dialogo Aggiungi riferimento](http://msdn.microsoft.com/it-it/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)   
 [NIB Procedura: Modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [Risoluzione dei problemi relativi ai riferimenti interrotti](/visual-studio/ide/troubleshooting-broken-references)