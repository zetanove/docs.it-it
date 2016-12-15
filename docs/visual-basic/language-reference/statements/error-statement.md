---
title: "Error Statement | Microsoft Docs"
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
  - "vb.error"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Error statement, syntax"
  - "Error statement"
  - "Error keyword"
  - "run-time errors, codes"
  - "errors [Visual Basic], simulating"
ms.assetid: 85cd5c59-5224-4f02-aaf5-fcfefab17a29
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Error Statement
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di simulare un evento di errore.  
  
## Sintassi  
  
```  
Error errornumber  
```  
  
## Parti  
 `errornumber`  
 Obbligatorio.  Può essere qualsiasi numero di errore valido.  
  
## Note  
 L'istruzione `Error` è supportata per garantire la compatibilità con le versioni precedenti.  Nel nuovo codice, specialmente in sede di creazione di oggetti, per generare errori di runtime è consigliabile utilizzare il metodo `Raise` dell'oggetto `Err`.  
  
 Se il valore `errornumber` è definito, l'istruzione `Error` richiama il gestore errori dopo che alle proprietà dell'oggetto `Err` vengono assegnati i valori predefiniti riportati di seguito.  
  
|Proprietà|Valore|  
|---------------|------------|  
|`Number`|Valore specificato come argomento nell'istruzione `Error`.  Può essere qualsiasi numero di errore valido.|  
|`Source`|Nome del progetto di Visual Basic corrente.|  
|`Description`|Espressione stringa corrispondente al valore restituito dalla funzione `Error` per la proprietà `Number` specificata, a condizione che la stringa esista.  Se la stringa non esiste, `Description` conterrà una stringa di lunghezza zero \(""\).|  
|`HelpFile`|Percorso, completo di unità e nome file, del relativo file della Guida di Visual Basic.|  
|`HelpContext`|ID di contesto del file della Guida di Visual Basic relativo all'errore corrispondente alla proprietà `Number`.|  
|`LastDLLError`|Zero.|  
  
 Se non esiste o non è attivato alcun gestore errori, verrà creato e visualizzato un messaggio di errore sulla base delle proprietà dell'oggetto `Err`.  
  
> [!NOTE]
>  Alcune applicazioni host Visual Basic non consentono la creazione di oggetti.  Per determinare se l'applicazione host in uso consente di creare classi e oggetti, consultare la documentazione relativa.  
  
## Esempio  
 In questo esempio viene utilizzata l'istruzione `Error` per generare il numero di errore 11.  
  
```  
On Error Resume Next   ' Defer error handling.  
Error 11   ' Simulate the "Division by zero" error.  
```  
  
## Requisiti  
 **Spazio dei nomi:** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **Assembly:** Visual Basic Runtime Library \(in Microsoft.VisualBasic.dll\)  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.ErrObject.Clear%2A>   
 <xref:Microsoft.VisualBasic.Information.Err%2A>   
 <xref:Microsoft.VisualBasic.ErrObject.Raise%2A>   
 [On Error Statement](../../../visual-basic/language-reference/statements/on-error-statement.md)   
 [Resume Statement](../../../visual-basic/language-reference/statements/resume-statement.md)   
 [Error Messages](../../../visual-basic/language-reference/error-messages/index.md)