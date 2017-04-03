---
title: "Applicabilità della trasformazione funzionale (C#) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: c78107bd-b006-4574-a3d4-bbf808388ff3
caps.latest.revision: 4
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0f79ec1e5975a1197464785182a7e6d4af4ba61c
ms.lasthandoff: 03/13/2017


---
# <a name="applicability-of-functional-transformation-c"></a>Applicabilità della trasformazione funzionale (C#)
Le trasformazioni funzionali pure sono applicabili in un'ampia varietà di situazioni.  
  
 L'approccio della trasformazione funzionale è particolarmente indicato per l'esecuzione di query e modifiche di dati strutturati, pertanto si adatta perfettamente con le tecnologie LINQ. Tuttavia, la trasformazione funzionale presenta un'applicabilità molto più ampia rispetto all'utilizzo con LINQ. Qualsiasi processo il cui obiettivo principale è trasformare dati da un formato a un altro può essere considerato un candidato valido per la trasformazione funzionale.  
  
 Questo approccio è applicabile a molti problemi che a prima vista potrebbero non apparire indicati. Utilizzata insieme o separatamente rispetto a LINQ, la trasformazione funzionale deve essere considerata per le aree seguenti:  
  
-   Documenti basati su XML. I dati ben formati di qualsiasi sottolinguaggio XML possono essere facilmente modificati tramite la trasformazione funzionale. Per altre informazioni, vedere [Trasformazione funzionale di XML (C#)](../../../../csharp/programming-guide/concepts/linq/functional-transformation-of-xml.md).  
  
-   Altri formati di file strutturati. Dai file Windows.ini ai documenti di testo semplice, la maggior parte dei file presenta una struttura che si presta all'analisi e alla trasformazione.  
  
-   Protocolli di flusso dei dati. La codifica e la decodifica di dati dai protocolli di comunicazione possono essere spesso rappresentate da una semplice trasformazione funzionale.  
  
-   Dati RDBMS e OODBMS. I database relazionali e orientati a oggetti, quale XML, sono origini dati strutturate di largo utilizzo.  
  
-   Soluzioni matematiche, statistiche e scientifiche. In questi campi si tende a modificare grandi set di dati per assistere l'utente nella visualizzazione, nella stima o nella soluzione effettiva di problemi complessi.  
  
 Come descritto in [Refactoring in funzioni pure (C#)](../../../../csharp/programming-guide/concepts/linq/refactoring-into-pure-functions.md), l'uso di funzioni pure è un esempio di programmazione funzionale. Oltre a vantaggi immediati, l'uso di funzioni pure offre un'esperienza preziosa nel valutare i problemi da un punto di vista della trasformazione funzionale. Questo approccio può anche avere un impatto significativo sulla progettazione di programmi e classi. Ciò vale soprattutto quando un problema si presta a una soluzione di trasformazione dei dati come descritto in precedenza.  
  
 Pur esulando dall'ambito di questa esercitazione, le progettazioni influenzate dal punto di vista della trasformazione funzionale tendono a essere centrate sui processi piuttosto che sugli oggetti come attori e la soluzione risultante tende a essere implementata come una serie di trasformazioni su vasta scala, anziché come singole modifiche allo stato degli oggetti.  
  
 Ancora una volta, è opportuno tenere presente che C# supporta l'approccio imperativo e funzionale, quindi la progettazione ideale dell'applicazione potrebbe incorporare elementi di entrambi.  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione alle trasformazioni funzionali pure (C#)](../../../../csharp/programming-guide/concepts/linq/introduction-to-pure-functional-transformations.md)   
 [Trasformazione funzionale di XML (C#)](../../../../csharp/programming-guide/concepts/linq/functional-transformation-of-xml.md)   
 [Refactoring in funzioni pure (C#)](../../../../csharp/programming-guide/concepts/linq/refactoring-into-pure-functions.md)
