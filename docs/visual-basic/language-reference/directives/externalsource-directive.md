---
title: "#ExternalSource Directive | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "#Externalsource"
  - "#ExternalSource"
  - "vb.ExternalSource"
  - "Externalsource"
  - "vb.#ExternalSource"
  - "ExternalSource"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "ExternalSource directive (#ExternalSource)"
  - "#ExternalSource directive"
ms.assetid: 243bc6a2-34c3-4eeb-a776-9fd2bf988149
caps.latest.revision: 160
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 160
---
# #ExternalSource Directive
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Indica un mapping tra righe di codice sorgente specifiche e testo esterno.  
  
## Sintassi  
  
```  
#ExternalSource( StringLiteral , IntLiteral )  
    [ LogicalLine+ ]  
#End ExternalSource  
```  
  
## Parti  
 `StringLiteral`  
 Il percorso al codice sorgente esterno.  
  
 `IntLiteral`  
 Il numero di riga della prima riga del codice sorgente esterno.  
  
 `LogicalLine`  
 La riga del codice sorgente esterno in cui si verifica l'errore.  
  
 `#End ExternalSource`  
 Termina il blocco `#ExternalSource`.  
  
## Note  
 Questa direttiva è utilizzata solo dal compilatore e dal debugger.  
  
 Un file di origine può includere direttive del codice esterno, che indicano un mapping tra righe specifiche di codice nel file di origine e testo esterno all'origine, quale un file ASPX.  Se vengono rilevati errori nel codice sorgente designato durante la compilazione, tali errori vengono identificati come provenienti dall'origine esterna.  
  
 Le direttive in codice sorgente esterno non influiscono in alcun modo sulla compilazione e non possono essere annidate.  Sono destinate all'uso interno da parte dell'applicazione.  
  
## Vedere anche  
 [Conditional Compilation](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)