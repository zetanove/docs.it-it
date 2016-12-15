---
title: "Implements Statement | Microsoft Docs"
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
  - "vb.Implements"
  - "Implements"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Implements statement, syntax"
  - "Implements statement"
  - "interface implementation, Implements statement"
ms.assetid: 1fafb83f-f55a-4215-8ea9-681e8622613d
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Implements Statement
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica una o più interfacce o membri di interfaccia che è necessario implementare nella definizione di classe o di struttura in cui è inserita.  
  
## Sintassi  
  
```  
Implements interfacename [, ...]  
-or-  
Implements interfacename.interfacemember [, ...]  
```  
  
## Parti  
 `interfacename`  
 Obbligatorio.  Interfaccia le cui proprietà, routine ed eventi devono essere implementati dai membri corrispondenti nella classe o nella struttura.  
  
 `interfacemember`  
 Obbligatorio.  Membro di un'interfaccia da implementare.  
  
## Note  
 Un'interfaccia è una raccolta di prototipi che rappresentano i membri \(proprietà, routine ed eventi\) in essa contenuti.  Le interfacce contengono solo le dichiarazioni dei membri mentre le classi e le strutture li implementano.  Per ulteriori informazioni, vedere [Interfaces](../../../visual-basic/programming-guide/language-features/interfaces/index.md).  
  
 L'istruzione `Implements` deve seguire immediatamente l'istruzione `Class` o `Structure`.  
  
 Quando si implementa un'interfaccia, è necessario implementare tutti i membri in essa dichiarati.  L'omissione di un membro viene considerata un errore di sintassi.  Per implementare un singolo membro, specificare la parola chiave [Implements](../../../visual-basic/language-reference/statements/implements-clause.md), distinta dall'istruzione `Implements`, quando si dichiara il membro nella classe o nella struttura.  Per ulteriori informazioni, vedere [Interfaces](../../../visual-basic/programming-guide/language-features/interfaces/index.md).  
  
 Le classi possono utilizzare le implementazioni [Private](../../../visual-basic/language-reference/modifiers/private.md) di proprietà e routine, ma è possibile accedere a questi membri solo eseguendo il casting di un'istanza della classe che implementa in una variabile dichiarata come tipo dell'interfaccia.  
  
## Esempio  
 Nell'esempio seguente, viene illustrato come utilizzare l'istruzione `Implements` per implementare i membri di un'interfaccia.  Definisce un'interfaccia denominata `ICustomerInfo` con un evento, una proprietà e una routine.  La classe `customerInfo` implementa tutti i membri definiti nell'interfaccia.  
  
 [!code-vb[VbVbalrStatements#33](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/implements-statement_1.vb)]  
  
 Si noti che la classe `customerInfo` utilizza l'istruzione `Implements` in una riga del codice sorgente distinta per indicare l'implementazione di tutti i membri dell'interfaccia `ICustomerInfo`.  Ogni membro della classe, quindi, include la parola chiave `Implements` nella dichiarazione dei relativi membri per indicare l'implementazione di quel membro dell'interfaccia.  
  
## Esempio  
 Nelle seguenti due routine viene illustrato un possibile utilizzo dell'interfaccia implementata nell'esempio precedente.  Per eseguire il test dell'implementazione, aggiungere queste routine al progetto e chiamare la routine `testImplements`.  
  
 [!code-vb[VbVbalrStatements#34](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/implements-statement_2.vb)]  
  
## Vedere anche  
 [Implements](../../../visual-basic/language-reference/statements/implements-clause.md)   
 [Interface Statement](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Interfaces](../../../visual-basic/programming-guide/language-features/interfaces/index.md)