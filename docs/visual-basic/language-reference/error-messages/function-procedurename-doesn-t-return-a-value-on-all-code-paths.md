---
title: "Function &#39;&lt;procedurename&gt;&#39; doesn&#39;t return a value on all code paths | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc42105"
  - "vbc42105"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42105"
ms.assetid: b6929bf4-a365-4a70-8dc9-6b0fc09e1468
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Function &#39;&lt;procedurename&gt;&#39; doesn&#39;t return a value on all code paths
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La funzione '\<nomeroutine\>' non restituisce un valore in tutti i percorsi del codice.Verificare che non manchi un'istruzione 'Return'.  
  
 Una routine `Function` dispone di almeno un percorso possibile, tramite il codice, che non restituisce un valore.  
  
 È possibile restituire un valore da una routine `Function` in uno dei seguenti modi:  
  
-   Includere il valore in [Return Statement](../../../visual-basic/language-reference/statements/return-statement.md).  
  
-   Assegnare il valore al nome della routine `Function`, quindi eseguire un'istruzione `Exit Function`.  
  
-   Assegnare il valore al nome della procedura `Function`, quindi eseguire l'istruzione `End Function`.  
  
 Se il controllo passa a `Exit Function` o `End Function` e non si è assegnato alcun valore al nome della procedura, la procedura restituirà il valore predefinito del tipo di dati restituito.  Per ulteriori informazioni, vedere "Comportamento" in [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md).  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:**  BC42105  
  
### Per correggere l'errore  
  
-   Verificare la logica del flusso di controllo e assicurarsi di assegnare un valore prima di ogni istruzione che provoca una restituzione.  
  
     È più semplice garantire che ogni restituzione della procedura restituisca un valore se si utilizza sempre l'istruzione `Return`.  In tal caso, l'ultima istruzione prima di `End Function` dovrebbe essere un'istruzione `Return`.  
  
## Vedere anche  
 [Routine Function](../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Compilazione \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic)