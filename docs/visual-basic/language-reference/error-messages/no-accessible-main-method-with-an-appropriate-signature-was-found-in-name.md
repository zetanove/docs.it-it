---
title: "No accessible &#39;Main&#39; method with an appropriate signature was found in &#39;&lt;name&gt;&#39; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30737"
  - "vbc30737"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30737"
ms.assetid: 3f40bacd-3fac-4741-b204-852f693d4340
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# No accessible &#39;Main&#39; method with an appropriate signature was found in &#39;&lt;name&gt;&#39;
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È necessario che per le applicazioni della riga di comando venga definito un oggetto `Sub Main`.  `Main` deve essere dichiarato come `Public Shared` se è definito in una classe o come `Public` se è definito in un modulo.  
  
 Per ulteriori informazioni su `Main`, vedere [NIB: Visual Basic Version of Hello, World](http://msdn.microsoft.com/it-it/9d030b60-e148-4366-a462-69532f02294c).  
  
 **ID errore:** BC30737  
  
### Per correggere l'errore  
  
-   Definire una routine `Public Sub Main` per il progetto.  La routine deve essere dichiarata come `Shared` esclusivamente se viene definita in una classe.  
  
## Vedere anche  
 [NIB: Visual Basic Version of Hello, World](http://msdn.microsoft.com/it-it/9d030b60-e148-4366-a462-69532f02294c)   
 [Structure of a Visual Basic Program](../../../visual-basic/programming-guide/program-structure/structure-of-a-visual-basic-program.md)   
 [Procedures](../../../visual-basic/programming-guide/language-features/procedures/index.md)