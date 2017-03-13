---
title: "Stop Statement (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Stop"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "breakpoints, Stop statements"
  - "Stop statements, syntax"
  - "Stop statements"
  - "execution, suspending"
  - "processing, interrupting"
  - "processes, interrupting"
  - "execution, stopping"
ms.assetid: c9a9fde0-d649-4662-9bef-bd0146ebc2a7
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Stop Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di sospendere l'esecuzione.  
  
## Sintassi  
  
```  
Stop  
```  
  
## Note  
 Le istruzioni `Stop` possono essere inserite in qualsiasi punto delle routine per sospendere l'esecuzione  e il loro utilizzo è analogo all'impostazione di un punto di interruzione nel codice.  
  
 L'istruzione `Stop` sospende l'esecuzione ma, diversamente da `End`, non chiude file né cancella variabili, a meno che non venga rilevata in un file eseguibile \(EXE\) compilato.  
  
> [!NOTE]
>  Se l'istruzione `Stop` viene rilevata nel codice in esecuzione al di fuori dell'ambiente IDE \(Integrated Development Environment \- ambiente di sviluppo integrato\), viene richiamato il debugger,  indipendentemente dal fatto che il codice sia stato compilato in modalità di debug o finale.  
  
## Esempio  
 Nell'esempio seguente l'istruzione `Stop` viene utilizzata per sospendere l'esecuzione a ogni iterazione del ciclo `For...Next`.  
  
 [!code-vb[VbVbalrStatements#56](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/stop-statement_1.vb)]  
  
## Vedere anche  
 [End Statement](../../../visual-basic/language-reference/statements/end-statement.md)