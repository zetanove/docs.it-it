---
title: Posticipata esecuzione e valutazione differita in LINQ to XML (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 31998eed-b95e-47fb-a865-9de1f337d1fb
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3b7318eb9853d633d152b93fafcf9570ccd03835
ms.lasthandoff: 03/13/2017


---
# <a name="deferred-execution-and-lazy-evaluation-in-linq-to-xml-visual-basic"></a>Esecuzione posticipata e valutazione differita in LINQ to XML (Visual Basic)
Operazioni di query e su asse vengono spesso implementate in modo da usare l'esecuzione posticipata. In questo argomento vengono illustrati requisiti e vantaggi dell'esecuzione posticipata e vengono fornite alcune considerazioni sull'implementazione.  
  
## <a name="deferred-execution"></a>Esecuzione posticipata  
 Esecuzione posticipata si intende che la valutazione di un'espressione viene ritardata finché il relativo *realizzato* valore risulta effettivamente necessario. L'esecuzione posticipata può contribuire a migliorare notevolmente le prestazioni quando è necessario modificare grandi raccolte di dati, in particolare in programmi che contengono una serie di modifiche o query concatenate. Nel migliore dei casi l'esecuzione posticipata consente di eseguire un'unica iterazione nella raccolta di origine.  
  
 Le tecnologie LINQ usano ampiamente l'esecuzione posticipata sia nei membri di base <xref:System.Linq?displayProperty=fullName>classi e nei metodi di estensione negli spazi dei nomi diversi di LINQ, ad esempio <xref:System.Xml.Linq.Extensions?displayProperty=fullName>.</xref:System.Xml.Linq.Extensions?displayProperty=fullName> </xref:System.Linq?displayProperty=fullName>  
  
## <a name="eager-vs-lazy-evaluation"></a>Valutazione eager e valutazione lazy  
 Quando si scrive un metodo che implementa l'esecuzione posticipata, è inoltre necessario decidere se implementare il metodo tramite la valutazione lazy o la valutazione eager.  
  
-   In *valutazione lazy*, durante ogni chiamata all'iteratore viene elaborato un singolo elemento della raccolta di origine. Si tratta della modalità di implementazione tipica degli iteratori.  
  
-   In *valutazione eager*, la prima chiamata all'iteratore comporterà l'intera raccolta in fase di elaborazione. Potrebbe inoltre essere necessaria una copia temporanea della raccolta di origine. Ad esempio, il <xref:System.Linq.Enumerable.OrderBy%2A>metodo deve ordinare l'intera raccolta prima di restituire il primo elemento.</xref:System.Linq.Enumerable.OrderBy%2A>  
  
 La valutazione lazy offre in genere prestazioni migliori perché implica una distribuzione uniforme dell'overhead di elaborazione in tutte le fasi della valutazione della raccolta e riduce al minimo l'uso di dati temporanei. Per alcune operazioni è naturalmente inevitabile dover materializzare i risultati intermedi.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Nel successivo argomento dell'esercitazione verrà illustrata l'esecuzione posticipata:  
  
-   [Esempio di esecuzione posticipata (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/deferred-execution-example.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazione: Posticipata esecuzione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/tutorial-deferred-execution.md)   
 [Concetti e terminologia (trasformazione funzionale) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/concepts-and-terminology-functional-transformation.md)   
 [Operazioni di aggregazione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/aggregation-operations.md)
