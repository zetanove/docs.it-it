---
title: "Using Objects That Implement IDisposable | Microsoft Docs"
ms.custom: ""
ms.date: "04/07/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Dispose method"
  - "try/finally block"
  - "garbage collection, encapsulating resources"
ms.assetid: 81b2cdb5-c91a-4a31-9c83-eadc52da5cf0
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Using Objects That Implement IDisposable
Il recupero della memoria utilizzata dagli oggetti non gestiti viene eseguito dal Garbage Collector di Common Language Runtime, ma i tipi che utilizzano le risorse non gestite implementano l'interfaccia <xref:System.IDisposable> per consentire il recupero di tale memoria non gestita.  Dopo avere utilizzato un oggetto che implementa <xref:System.IDisposable>, è necessario chiamare l'implementazione <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> dell'oggetto.  Questa operazione può essere eseguita in due modi:  
  
-   Con l'istruzione **using** in C\# o l'istruzione `Using` in Visual Basic.  
  
-   Implementando un blocco `try`\/`finally`.  
  
## Istruzione using  
 L'istruzione **using** in C\# e l'istruzione `Using` in Visual Basic semplificano il codice da scrivere per creare e pulire un oggetto.  L'istruzione **using** ottiene una o più risorse, esegue le istruzioni specificate, quindi elimina l'oggetto in modo automatico.  Tuttavia, tale istruzione è utile solo per gli oggetti utilizzati nell'ambito del metodo in cui vengono costruiti.  
  
 Nell'esempio seguente viene utilizzata l'istruzione `using` per creare e rilasciare un oggetto <xref:System.IO.StreamReader?displayProperty=fullName>.  
  
 [!code-csharp[Conceptual.Disposable#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using1.cs#1)]
 [!code-vb[Conceptual.Disposable#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using1.vb#1)]  
  
 Si noti che, anche se la classe <xref:System.IO.StreamReader> implementa l'interfaccia <xref:System.IDisposable>, a indicare che utilizza una risorsa non gestita, nell'esempio non viene chiamato il metodo <xref:System.IO.StreamReader.Dispose%2A?displayProperty=fullName> in modo esplicito.  Quando nel compilatore C\# o Visual Basic viene rilevata l'istruzione `using`, viene generato codice IL \(Intermediate Language\) equivalente al codice seguente, che contiene un blocco `try`\/`finally` in modo esplicito.  
  
 [!code-csharp[Conceptual.Disposable#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using3.cs#3)]
 [!code-vb[Conceptual.Disposable#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using3.vb#3)]  
  
 Con una singola istruzione **using** di C\# è possibile anche ottenere più risorse, mediante un meccanismo che equivale internamente all'utilizzo di più istruzioni **using** annidate.  Nell'esempio seguente viene creata l'istanza di due oggetti <xref:System.IO.StreamReader> per leggere il contenuto di due diversi file.  
  
 [!code-csharp[Conceptual.Disposable#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using4.cs#4)]  
  
## Blocco try\/finally  
 Anziché eseguire il wrapping di un blocco `try`\/`finally` in un'istruzione `using`, è possibile implementare direttamente il blocco `try`\/`finally`.  La scelta può essere espressione dello stile di codifica personale oppure essere dovuta a uno dei seguenti motivi:  
  
-   Includere un blocco `catch` per gestire eventuali eccezioni generate nel blocco `try`.  In caso contrario, tutte le eccezioni generate dall'istruzione `using` non vengono gestite, analogamente alle eccezioni generate all'interno del blocco `using` se un blocco `try`\/`catch` non è presente.  
  
-   Creare un'istanza di un oggetto che implementa <xref:System.IDisposable> il cui ambito non è locale rispetto al blocco in cui viene dichiarato.  
  
 L'esempio seguente è simile a quello precedente, con la differenza che in questo viene utilizzato un blocco `try`\/`catch`\/`finally` per creare un'istanza di un oggetto <xref:System.IO.StreamReader>, utilizzarla ed eliminarla e per gestire le eccezioni generate dal costruttore <xref:System.IO.StreamReader> e dal relativo metodo <xref:System.IO.StreamReader.ReadToEnd%2A>.  Si noti che il codice nel blocco `finally` controlla che l'oggetto che implementa <xref:System.IDisposable> non sia `null` prima di chiamare il metodo <xref:System.IDisposable.Dispose%2A>.  L'omissione di tale controllo può provocare un'eccezione <xref:System.NullReferenceException> in fase di esecuzione.  
  
 [!code-csharp[Conceptual.Disposable#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using5.cs#6)]
 [!code-vb[Conceptual.Disposable#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using5.vb#6)]  
  
 È possibile utilizzare questo modello di base se si decide di implementare o è necessario implementare un blocco `try`\/`finally`, poiché il linguaggio di programmazione non supporta un'istruzione `using` ma consente chiamate dirette al metodo <xref:System.IDisposable.Dispose%2A>.  
  
 Se il linguaggio non supporta le chiamate dirette al metodo <xref:System.IDisposable.Dispose%2A> \(ad esempio in C\+\+\), di solito è possibile utilizzare la sintassi del distruttore del linguaggio.  
  
## Vedere anche  
 [Cleaning Up Unmanaged Resources](../../../docs/standard/garbage-collection/unmanaged.md)   
 [Istruzione using](../Topic/using%20Statement%20\(C%23%20Reference\).md)   
 [Using Statement](../Topic/Using%20Statement%20\(Visual%20Basic\).md)