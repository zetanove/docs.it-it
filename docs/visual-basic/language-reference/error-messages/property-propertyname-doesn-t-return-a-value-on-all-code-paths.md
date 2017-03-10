---
title: "Property &#39;&lt;propertyname&gt;&#39; doesn&#39;t return a value on all code paths | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc42107"
  - "vbc42107"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42107"
ms.assetid: 06800966-9c3b-4844-9f13-83ac95607d32
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# Property &#39;&lt;propertyname&gt;&#39; doesn&#39;t return a value on all code paths
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

La proprietà '\<nomeproprietà\>' non restituisce un valore in tutti i percorsi del codice.In fase di esecuzione, quando viene utilizzato il risultato, è possibile che si verifichi un'eccezione dovuta a un riferimento a un valore nullo.  
  
 Una routine `Get` della proprietà possiede almeno un possibile percorso all'interno del codice che non restituisce alcun valore.  
  
 Per restituire un valore dalla routine `Get` di una proprietà è possibile procedere come segue:  
  
-   Assegnare il valore al nome della proprietà, quindi eseguire l'istruzione `Exit Property`.  
  
-   Assegnare il valore al nome della proprietà, quindi eseguire l'istruzione `End Get`.  
  
-   Includere il valore in [Return Statement](../../../visual-basic/language-reference/statements/return-statement.md).  
  
 Se il controllo passa a `Exit Property` o `End Get` e non è stato assegnato alcun valore al nome della proprietà, la routine `Get` restituisce il valore predefinito del tipo di dati della proprietà.  Per ulteriori informazioni, vedere "Comportamento" in [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md).  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42107  
  
### Per correggere l'errore  
  
-   Verificare la logica del flusso di controllo e assicurarsi di assegnare un valore prima di ogni istruzione che provoca una restituzione.  
  
     È più semplice garantire che ogni restituzione della procedura restituisca un valore se si utilizza sempre l'istruzione `Return`.  In questo caso, l'ultima istruzione prima di `End Get` deve essere un'istruzione `Return`.  
  
## Vedere anche  
 [Routine Property](../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Get Statement](../../../visual-basic/language-reference/statements/get-statement.md)