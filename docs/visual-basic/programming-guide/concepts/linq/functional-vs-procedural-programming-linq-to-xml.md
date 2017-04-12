---
title: Programmazione Programmazione procedurale (LINQ to XML) (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: ea1015a5-d4c8-4d79-8e1e-ba17a40a4f39
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9d5afe31c8c81f4b099853a5e6e274156a1baa7f
ms.lasthandoff: 03/13/2017

---
# <a name="functional-vs-procedural-programming-linq-to-xml-visual-basic"></a>Programmazione Programmazione procedurale (LINQ to XML) (Visual Basic)
Sono disponibili diversi tipi di applicazioni XML:  
  
-   In alcune applicazioni da documenti XML di origine vengono prodotti nuovi documenti XML con una forma diversa.  
  
-   In alcune applicazioni da documenti XML di origine vengono prodotti documenti risultanti in un formato completamente diverso, ad esempio file di testo CSV o HTML.  
  
-   In alcune applicazioni da documenti XML di origine vengono inseriti record in un database.  
  
-   In alcune applicazioni dai dati di un'altra origine, ad esempio un database, vengono creati documenti XML.  
  
 Quelli elencati non sono tutti i tipi di applicazioni XML disponibili, ma sono rappresentativi dei tipi di funzionalità che i programmatori XML devono implementare.  
  
 Con tutti questi tipi di applicazioni, gli sviluppatori possono adottare due approcci completamente diversi:  
  
-   Costruzione funzionale usando un approccio dichiarativo.  
  
-   Modifica dell'albero XML in memoria usando codice procedurale.  
  
 In LINQ to XML sono supportati entrambi gli approcci.  
  
 Quando si usa l'approccio funzionale, vengono scritte trasformazioni che dai documenti di origine generano documenti completamente nuovi con la forma desiderata.  
  
 Quando si modifica un albero XML sul posto, viene scritto un codice che attraversa e si sposta attraverso i nodi in un albero XML in memoria, inserendo, eliminando e modificando i nodi secondo necessità.  
  
 È possibile usare LINQ to XML con uno di questi due approcci. Si usano le stesse classe e in alcuni casi gli stessi metodi. Tuttavia, la struttura e gli obiettivi dei due approcci sono molto diversi. In situazioni diverse, ad esempio, un approccio offre in genere prestazioni più elevate dell'altro e usa una quantità maggiore o minore di memoria. Inoltre, un approccio sarà più facile da scrivere dell'altro e produrrà codice più facilmente gestibile.  
  
 Per i due approcci analogie, vedere [Visual Studio modifica dell'albero XML In memoria. Costruzione funzionale (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/in-memory-xml-tree-modification-vs-functional-construction.md).  
  
 Per un'esercitazione sulla scrittura di trasformazioni funzionali, vedere [Pure Functional Transformations of XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/pure-functional-transformations-of-xml.md).  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to Cenni preliminari sulla programmazione XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)
