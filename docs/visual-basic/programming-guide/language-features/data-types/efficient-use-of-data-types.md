---
title: "Efficient Use of Data Types (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "performance, data type efficiency"
  - "data types [Visual Basic], weak typing"
  - "AscW function, preferred to Asc"
  - "data types [Visual Basic], using efficiently"
  - "optimization, data types"
  - "data types [Visual Basic], strong typing"
  - "strong typing"
  - "typing, strong"
  - "data types [Visual Basic], optimizing"
  - "ChrW function, preferred to Chr"
ms.assetid: 28f5e4ba-ec24-4f37-b90a-e8ee822f778a
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Efficient Use of Data Types (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Alle variabili non dichiarate o dichiarate senza un tipo di dati viene assegnato il tipo di dati `Object`.  Questo semplifica e velocizza la scrittura di programmi, ma ne può rendere più lenta l'esecuzione.  
  
## Tipizzazione forte  
 La specifica di tipi di dati per tutte le variabili è definita *tipizzazione forte*.  L'utilizzo di tale tipizzazione presenta vari vantaggi:  
  
-   Attiva il supporto IntelliSense per le variabili.  consentendo di visualizzarne le proprietà e gli altri membri mentre si digita il codice.  
  
-   Sfrutta la funzionalità di controllo dei tipi del compilatore.  In questo modo vengono rilevate le istruzioni destinate ad avere esito negativo in fase di esecuzione a causa di errori quale l'overflow.  Vengono inoltre rilevate le chiamate a metodi su oggetti che non li supportano.  
  
-   Comporta un'esecuzione più veloce del codice.  
  
## Tipi di dati più efficaci  
 Per le variabili che non contengono mai frazioni, i tipi di dati integrali sono più efficaci di quelli non integrali.  In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], `Integer` e `UInteger` sono i tipi numerici che offrono maggiore efficienza.  
  
 Per i numeri frazionari, il tipo di dati più efficace è `Double`, poiché i processori disponibili sulle attuali piattaforme eseguono operazioni a virgola mobile in precisione doppia.  Tuttavia, l'esecuzione delle operazioni con tipo di dati `Double` richiede più tempo rispetto a quella delle operazioni con i tipi integrali, ad esempio `Integer`.  
  
## Specifica del tipo di dati  
 Utilizzare l'[Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md) per dichiarare una variabile di un tipo specifico.  È possibile specificare contemporaneamente il relativo livello di accesso utilizzando la parola chiave [Public](../../../../visual-basic/language-reference/modifiers/public.md), [Protected](../../../../visual-basic/language-reference/modifiers/protected.md), [Friend](../../../../visual-basic/language-reference/modifiers/friend.md) o [Private](../../../../visual-basic/language-reference/modifiers/private.md), come illustrato nell'esempio riportato di seguito.  
  
```  
Private x As Double  
Protected s As String  
```  
  
## Conversione di caratteri  
 Le funzioni `AscW` e `ChrW` operano in Unicode  e si consiglia di utilizzarle in alternativa a `Asc` e `Chr`, che devono essere convertite in Unicode.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Strings.Asc%2A>   
 <xref:Microsoft.VisualBasic.Strings.AscW%2A>   
 <xref:Microsoft.VisualBasic.Strings.Chr%2A>   
 <xref:Microsoft.VisualBasic.Strings.ChrW%2A>   
 [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Numeric Data Types](../../../../visual-basic/programming-guide/language-features/data-types/numeric-data-types.md)   
 [Dichiarazione di variabili](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Utilizzo di IntelliSense](/visual-studio/ide/using-intellisense)