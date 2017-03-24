---
title: "&#39;&lt;expression&gt;&#39; cannot be used as a type constraint | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc32061"
  - "vbc32061"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32061"
ms.assetid: b17821b7-fa14-4397-a211-6e2a14079f09
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# &#39;&lt;expression&gt;&#39; cannot be used as a type constraint
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un elenco di vincoli include un'espressione che non rappresenta un vincolo valido su un parmetro di tipo.  
  
 Un elenco di vincoli impone i requisiti sull'argomento di tipo passato al parametro di tipo.  È possibile specificare i requisiti seguenti in qualsiasi combinazione:  
  
-   È necessario che l'argomento di tipo implementi una o più interfacce  
  
-   È necessario che l'argomento di tipo erediti da una classe al massimo  
  
-   È necessario che l'argomento di tipo esponga un costruttore senza parametri accessibile dal codice di creazione \(compreso il vincolo `New`\)  
  
 Se non si include nessun altra classe o interfaccia specifica nell'elenco di vincoli, è possibile imporre un requisito più generale specificando una delle seguenti condizioni:  
  
-   L'argomento di tipo deve essere un tipo di valore \(compreso il vincolo `Structure`\)  
  
-   È necessario che l'argomento di tipo sia un tipo di riferimento \(compreso il vincolo `Class`\)  
  
 Non è possibile specificare `Structure` e `Class` per lo stesso parametro di tipo e non è possibile specificarne uno più di una volta.  
  
 **ID errore:** BC32061  
  
### Per correggere l'errore  
  
-   Verificare che l'espressione e i suoi elementi siano digitati correttamente.  
  
-   Se l'espressione non si qualifica per l'elenco di requisiti precedente, rimuoverlo dall'elenco di vincoli.  
  
-   Se l'espressione fa riferimento a un'interfaccia o una classe, verificare che il compilatore abbia accesso a quell'interfaccia o classe.  Potrebbe essere necessario qualificarne il nome, e aggiungere un riferimento al progetto.  Per ulteriori informazioni, vedere "Riferimenti ai progetti" in [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
## Vedere anche  
 [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Value Types and Reference Types](../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Procedura: aggiungere o rimuovere riferimenti utilizzando la finestra di dialogo Aggiungi riferimento](http://msdn.microsoft.com/it-it/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)