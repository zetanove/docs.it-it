---
title: "&lt;message&gt; Questo errore potrebbe essere dovuto anche all&#39;unione di un riferimento file con un riferimento progetto nell&#39;assembly &#39;&lt;assemblyname&gt;&#39;. | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc30971"
  - "vbc30971"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30971"
ms.assetid: 75d2e8b5-2fdc-4623-8b32-cba805dab7db
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &lt;message&gt; Questo errore potrebbe essere dovuto anche all&#39;unione di un riferimento file con un riferimento progetto nell&#39;assembly &#39;&lt;assemblyname&gt;&#39;.
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

\<message\> Questo errore potrebbe essere dovuto anche all'unione di un riferimento file con un riferimento progetto nell'assembly '\<assemblyname\>'. In questo caso, provare a sostituire il riferimento file a '\<assemblyfilename\>' nel progetto '\<projectname1\>' con un riferimento progetto a '\<projectname2\>'.  
  
 Il codice del progetto accede a un membro di un altro progetto, ma la configurazione della soluzione non permette al compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per risolvere il riferimento.  
  
 Per accedere a un tipo definito in un altro assembly, il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] deve avere un riferimento a quell'assembly. Deve trattarsi di un riferimento unico, non ambiguo, che non generi riferimenti circolari tra i progetti.  
  
 **ID errore:** BC30971  
  
### Per correggere l'errore  
  
1.  Determinare quale progetto produce l'assembly migliore per il progetto a cui fare riferimento. Per questa decisione si potrebbero usare criteri quali la facilità di accesso al file e la frequenza di aggiornamenti.  
  
2.  Nelle proprietà del progetto aggiungere un riferimento al progetto contenente l'assembly che definisce il tipo in uso.  
  
## Vedere anche  
 [Gestione dei riferimenti in un progetto](/visual-studio/ide/managing-references-in-a-project)   
 [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [NIB Procedura: Aggiungere o rimuovere riferimenti utilizzando la finestra di dialogo Aggiungi riferimento](http://msdn.microsoft.com/it-it/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)   
 [NIB Procedura: Modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [Risoluzione dei problemi relativi ai riferimenti interrotti](/visual-studio/ide/troubleshooting-broken-references)