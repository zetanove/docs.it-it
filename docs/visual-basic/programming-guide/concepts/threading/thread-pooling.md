---
title: (Visual Basic) di pooling dei thread | Documenti di Microsoft
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
ms.assetid: 4903fb7a-eaad-435a-9add-1d1b32de3b83
caps.latest.revision: 4
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6037d7ea17e260d44bae571aa25d413996f5a123
ms.lasthandoff: 03/13/2017

---
# <a name="thread-pooling-visual-basic"></a>(Visual Basic) di pooling dei thread
Oggetto *pool di thread* è una raccolta di thread che può essere utilizzato per eseguire diverse attività in background. (Vedere [Threading (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/index.md) per le informazioni.) In questo modo il thread principale può eseguire altre attività in modo asincrono.  
  
 Pool di thread vengono spesso utilizzati nelle applicazioni server. Ogni richiesta in ingresso viene assegnato a un thread dal pool di thread, in modo che la richiesta può essere elaborata in modo asincrono, senza bloccare il thread principale o ritardare l'elaborazione delle richieste successive.  
  
 Una volta un thread nel pool di completamento dell'attività, viene restituito a una coda di thread in attesa, in cui può essere riutilizzato. In questo modo le applicazioni evitare il costo di creazione di un nuovo thread per ogni attività.  
  
 Pool di thread sono in genere un numero massimo di thread. Se tutti i thread sono occupati, attività aggiuntive vengono inserite nella coda finché non può essere gestite come diventano disponibili thread.  
  
 È possibile implementare un pool di thread, ma è più semplice utilizzare il pool di thread fornito da .NET Framework tramite la <xref:System.Threading.ThreadPool>classe.</xref:System.Threading.ThreadPool>  
  
 Pool di thread, si chiama il <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A?displayProperty=fullName>metodo con un delegato per la procedura da eseguire e Visual Basic viene creato il thread ed eseguita la procedura.</xref:System.Threading.ThreadPool.QueueUserWorkItem%2A?displayProperty=fullName>  
  
## <a name="thread-pooling-example"></a>Esempio di pooling dei thread  
 Nell'esempio seguente viene illustrato come utilizzare pooling dei thread per avviare diverse attività.  
  
```vb  
Public Sub DoWork()  
    ' Queue a task.  
    System.Threading.ThreadPool.QueueUserWorkItem(  
        New System.Threading.WaitCallback(AddressOf SomeLongTask))  
    ' Queue another task.  
    System.Threading.ThreadPool.QueueUserWorkItem(  
        New System.Threading.WaitCallback(AddressOf AnotherLongTask))  
End Sub  
Private Sub SomeLongTask(ByVal state As Object)  
    ' Insert code to perform a long task.  
End Sub  
Private Sub AnotherLongTask(ByVal state As Object)  
    ' Insert code to perform another long task.  
End Sub  
```  
  
 Un vantaggio del pool di thread consiste nel fatto che è possibile passare argomenti in un oggetto di stato per la routine dell'attività. Se la procedura che si sta chiamando richiede più di un argomento, è possibile impostare una struttura o un'istanza di una classe in un `Object` tipo di dati.  
  
## <a name="thread-pool-parameters-and-return-values"></a>Parametri del Pool di thread e i valori restituiti  
 Restituzione di valori da un thread di pool di thread non è semplice. Il metodo standard per la restituzione di valori da una chiamata di funzione non è consentito perché `Sub` procedure sono l'unico tipo di routine che può essere accodate al pool di thread. Un modo per fornire parametri e restituire valori è incapsulando i parametri, i valori restituiti, e i metodi in un classe wrapper come descritto in [parametri e valori restituiti per routine multithreading (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/parameters-and-return-values-for-multithreaded-procedures.md).  
  
 Un modo di soluzione per fornire parametri e valori restituiti è tramite facoltativo `ByVal` variabile oggetto di stato del <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A>(metodo).</xref:System.Threading.ThreadPool.QueueUserWorkItem%2A> Se si utilizza questa variabile per passare un riferimento a un'istanza di una classe, i membri dell'istanza possono essere modificati dal thread del pool di thread e utilizzati come valori restituiti.  
  
 Inizialmente potrebbe non essere evidente che è possibile modificare un oggetto a cui fa riferimento una variabile che viene passata per valore. È possibile farlo perché solo il riferimento all'oggetto viene passato per valore. Quando si apportano modifiche ai membri dell'oggetto a cui fa riferimento il riferimento all'oggetto, le modifiche applicate all'istanza di classe effettiva.  
  
 Le strutture non possono essere utilizzate per restituire i valori all'interno di oggetti di stato. Poiché le strutture sono tipi di valore, le modifiche apportate dal processo asincrono non modificano i membri della struttura originale. Utilizzare le strutture per fornire parametri quando non sono necessari i valori restituiti.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A></xref:System.Threading.ThreadPool.QueueUserWorkItem%2A>   
 <xref:System.Threading></xref:System.Threading>   
 <xref:System.Threading.ThreadPool></xref:System.Threading.ThreadPool>   
 [Procedura: utilizzare un Pool di Thread (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/how-to-use-a-thread-pool.md)   
 [Threading (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/index.md)   
 [Applicazioni multithreading (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/multithreaded-applications.md)   
 [Sincronizzazione dei thread (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/thread-synchronization.md)
